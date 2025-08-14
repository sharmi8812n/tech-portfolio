# JWT Authentication with Java Spring Boot

This README explains how to implement **JWT (JSON Web Token)** authentication in a Java Spring Boot application. JWT enables stateless, secure authentication for RESTful APIs.

---

## What is JWT?

**JSON Web Token (JWT)** is a compact, URL-safe token format for securely transmitting information between parties as a JSON object. It's widely used to authenticate users in a stateless way, meaning the server does not need to store any session information.

---

## How JWT Authentication Works

1. **User Login:**  
   The client sends user credentials (e.g., username and password) to the server via a login API.

2. **Authentication:**  
   The server validates the credentials against a user store (database).

3. **Token Generation:**  
   If valid, the server generates a JWT containing user identity and claims (like roles), signs it with a secret key, and returns it to the client.

4. **Client Stores Token:**  
   The client stores the JWT (in localStorage, sessionStorage, or mobile app storage).

5. **Request with Token:**  
   For subsequent API requests, the client includes the JWT in the HTTP `Authorization` header:  
   `Authorization: Bearer <token>`

6. **Token Validation:**  
   The server validates the JWT signature and expiration. If valid, it extracts user information and authorizes the request without needing to look up sessions.

7. **Access Granted or Denied:**  
   Based on the JWT claims, the server grants or denies access to protected resources.

---

## Why Use JWT?

- **Stateless:** No server-side sessions; scales easily.
- **Compact:** Small token size.
- **Cross-domain:** Can be used across different domains.
- **Secure:** Signed tokens prevent tampering.
- **Flexible:** Includes custom claims and user roles.

---

## Prerequisites

- Java 8+
- Spring Boot 2.x
- Maven or Gradle
- Basic Spring Security knowledge

---

## 1. Add Dependencies

In `pom.xml`:

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

## 2. User Model and Repository

Define your user entity (or adapt your existing user model).

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String username;
    private String password;
    private String role;
    // getters and setters
}

public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
}

## 3. Implement UserDetails and UserDetailsService
public class MyUserDetails implements UserDetails {
    private User user;

    public MyUserDetails(User user) { this.user = user; }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return Collections.singleton(new SimpleGrantedAuthority(user.getRole()));
    }
    @Override public String getPassword() { return user.getPassword(); }
    @Override public String getUsername() { return user.getUsername(); }
    @Override public boolean isAccountNonExpired() { return true; }
    @Override public boolean isAccountNonLocked() { return true; }
    @Override public boolean isCredentialsNonExpired() { return true; }
    @Override public boolean isEnabled() { return true; }
}

@Service
public class MyUserDetailsService implements UserDetailsService {

    @Autowired private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
                     .orElseThrow(() -> new UsernameNotFoundException("User not found"));
        return new MyUserDetails(user);
    }
}

## 4. JWT Utility Class
@Component
public class JwtUtil {

    private final String SECRET_KEY = "your_secret_key_here";

    private final long JWT_TOKEN_VALIDITY = 1000 * 60 * 60 * 10; // 10 hours

    public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    private Claims extractAllClaims(String token) {
        return Jwts.parser()
            .setSigningKey(SECRET_KEY)
            .parseClaimsJws(token)
            .getBody();
    }

    private Boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }

    public String generateToken(UserDetails userDetails) {
        return createToken(userDetails.getUsername());
    }

    private String createToken(String subject) {
        return Jwts.builder()
            .setSubject(subject)
            .setIssuedAt(new Date(System.currentTimeMillis()))
            .setExpiration(new Date(System.currentTimeMillis() + JWT_TOKEN_VALIDITY))
            .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
            .compact();
    }

    public Boolean validateToken(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
    }
}

## 5. Authentication Controller
@RestController
public class AuthController {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Autowired
    private MyUserDetailsService userDetailsService;

    @Autowired
    private JwtUtil jwtUtil;

    @PostMapping("/authenticate")
    public ResponseEntity<?> createAuthenticationToken(@RequestBody AuthRequest authRequest) throws Exception {
        try {
            authenticationManager.authenticate(
                new UsernamePasswordAuthenticationToken(authRequest.getUsername(), authRequest.getPassword())
            );
        } catch (BadCredentialsException e) {
            throw new Exception("Incorrect username or password", e);
        }

        final UserDetails userDetails = userDetailsService.loadUserByUsername(authRequest.getUsername());
        final String jwt = jwtUtil.generateToken(userDetails);

        return ResponseEntity.ok(new AuthResponse(jwt));
    }
}


Request and response DTOs:

public class AuthRequest {
    private String username;
    private String password;
    // getters and setters
}

public class AuthResponse {
    private final String jwt;

    public AuthResponse(String jwt) { this.jwt = jwt; }

    public String getJwt() { return jwt; }
}

## 6. JWT Request Filter

Intercept all requests to validate JWT token:

@Component
public class JwtRequestFilter extends OncePerRequestFilter {

    @Autowired private MyUserDetailsService userDetailsService;

    @Autowired private JwtUtil jwtUtil;

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
        throws ServletException, IOException {

        final String authorizationHeader = request.getHeader("Authorization");

        String username = null;
        String jwt = null;

        if (authorizationHeader != null && authorizationHeader.startsWith("Bearer ")) {
            jwt = authorizationHeader.substring(7);
            try {
                username = jwtUtil.extractUsername(jwt);
            } catch (Exception e) {
                // invalid token handling
            }
        }

        if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = this.userDetailsService.loadUserByUsername(username);

            if (jwtUtil.validateToken(jwt, userDetails)) {
                UsernamePasswordAuthenticationToken authToken = new UsernamePasswordAuthenticationToken(
                    userDetails, null, userDetails.getAuthorities());

                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }
        chain.doFilter(request, response);
    }
}

## 7. Security Configuration
@EnableWebSecurity
public class SecurityConfigurer extends WebSecurityConfigurerAdapter {

    @Autowired private MyUserDetailsService myUserDetailsService;

    @Autowired private JwtRequestFilter jwtRequestFilter;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(myUserDetailsService);
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeRequests()
                .antMatchers("/authenticate").permitAll()
                .anyRequest().authenticated()
            .and()
            .sessionManagement()
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS);

        http.addFilterBefore(jwtRequestFilter, UsernamePasswordAuthenticationFilter.class);
    }

    @Override
    @Bean
    public AuthenticationManager authenticationManagerBean() throws Exception {
        return super.authenticationManagerBean();
    }
}

## 8. Testing the Authentication

Start your Spring Boot app.
Make a POST request to /authenticate with:

{
  "username": "user",
  "password": "password"
}


You receive a JWT token.

Use the JWT token in the Authorization header for other requests:

Authorization: Bearer <jwt_token_here>

## 9. Important Notes

Always store passwords securely (e.g., bcrypt hashing).
Keep your JWT secret key safe and do not expose it.
Configure appropriate token expiration times.
Consider adding refresh tokens for long-lived sessions.
Implement exception handling for invalid/expired tokens.
