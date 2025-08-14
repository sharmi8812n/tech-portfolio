# Spring Security Integration Guide for Spring Boot

This README provides an overview and step-by-step guide to integrating **Spring Security** into a Java Spring Boot application. Spring Security provides authentication, authorization, and other security features for your app.

---

## What is Spring Security?

**Spring Security** is a powerful and customizable framework for securing Java applications. It handles:

- Authentication (who you are)
- Authorization (what you can do)
- Protection against common attacks (CSRF, session fixation, etc.)
- Password encoding and management
- Integration with OAuth2, JWT, LDAP, and more

---

## Prerequisites

- Java 8 or above
- Spring Boot 2.x or above
- Basic understanding of Spring Boot and REST APIs

---

## Getting Started

### 1. Add Spring Security Dependency

Add this to your `pom.xml`:
xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

### 2. Basic Security Configuration

Create a configuration class extending WebSecurityConfigurerAdapter (Spring Boot 2.x):

import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        // In-memory authentication with a user
        auth.inMemoryAuthentication()
            .withUser("user")
            .password("{noop}password") // {noop} means no password encoding
            .roles("USER");
    }

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/public/**").permitAll()  // Allow public URLs
                .anyRequest().authenticated()          // Secure all other endpoints
            .and()
            .formLogin()                              // Enable form login
                .permitAll()
            .and()
            .logout()
                .permitAll();
    }
}

### 3. Password Encoding

For production, always encode passwords:

import org.springframework.context.annotation.Bean;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}

Update your authentication to use encoded passwords.

### 4. Securing REST APIs with Basic Auth

For stateless REST APIs, you might prefer HTTP Basic authentication:

@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .csrf().disable()
        .authorizeRequests()
            .anyRequest().authenticated()
        .and()
        .httpBasic();
}

### 5. UserDetailsService for Custom Users

Create a service implementing UserDetailsService to load users from a database:

@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> new UsernameNotFoundException("User not found"));
        return new org.springframework.security.core.userdetails.User(
            user.getUsername(),
            user.getPassword(),
            Collections.singletonList(new SimpleGrantedAuthority("ROLE_USER"))
        );
    }
}

### Running the Application

Run your Spring Boot app.
Access secured endpoints; you’ll be prompted to login.
Use configured username/password for access.
