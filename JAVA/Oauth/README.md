# OAuth 2.0 Authentication with Java Spring Boot

This README explains the fundamentals of **OAuth 2.0** and how to configure OAuth 2.0 authentication in a Spring Boot application.

---

## What is OAuth 2.0?

OAuth 2.0 is an open-standard authorization framework that allows third-party applications to obtain limited access to an HTTP service, either on behalf of a resource owner (user) or by allowing the third-party application to obtain access on its own behalf.

### Key Concepts:

- **Resource Owner:** The user who authorizes an application to access their resources.
- **Client:** The application requesting access to resources on behalf of the resource owner.
- **Authorization Server:** The server that authenticates the resource owner and issues access tokens to the client.
- **Resource Server:** The server hosting the protected resources, accepting and validating access tokens.

---

## OAuth 2.0 Grant Types

Common OAuth 2.0 grant types:

- **Authorization Code:** Most secure; used by web apps and native apps.
- **Implicit:** Used for client-side apps (less secure, mostly deprecated).
- **Resource Owner Password Credentials:** User credentials are used directly (not recommended).
- **Client Credentials:** For machine-to-machine communication.

---

## How OAuth 2.0 Works (Authorization Code Flow)

1. The client redirects the user to the Authorization Server’s login/consent page.
2. The user authenticates and authorizes the client.
3. The Authorization Server sends an authorization code to the client.
4. The client exchanges the authorization code for an access token (and optionally a refresh token).
5. The client uses the access token to access protected resources on the Resource Server.

---

## Setting Up OAuth 2.0 in Spring Boot

### 1. Add Dependencies

Add the following dependencies to your `pom.xml`:

<!-- Spring Security OAuth2 Client -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>

<!-- Spring Security OAuth2 Resource Server (optional) -->
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>

### 2. Configure OAuth2 Client Properties

In your application.yml or application.properties, configure your OAuth provider (e.g., Google, GitHub):

spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: YOUR_GOOGLE_CLIENT_ID
            client-secret: YOUR_GOOGLE_CLIENT_SECRET
            scope:
              - openid
              - profile
              - email
        provider:
          google:
            authorization-uri: https://accounts.google.com/o/oauth2/v2/auth
            token-uri: https://oauth2.googleapis.com/token
            user-info-uri: https://openidconnect.googleapis.com/v1/userinfo
            user-name-attribute: sub


Replace with the provider of your choice.

### 3. Secure Your Application

Create a security configuration class to enable OAuth2 login:

import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.*;

@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http
      .authorizeRequests()
        .antMatchers("/", "/login**").permitAll()
        .anyRequest().authenticated()
      .and()
        .oauth2Login();
  }
}

### 4. Accessing OAuth2 User Info

You can inject the authenticated user's OAuth2 details in your controllers:

import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserController {

  @GetMapping("/user")
  public String user(OAuth2AuthenticationToken authentication) {
    return "User: " + authentication.getPrincipal().getAttributes().get("name");
  }
}

### Optional: OAuth 2.0 Resource Server Setup

If your Spring Boot app acts as a Resource Server that validates access tokens sent by clients:

Add the spring-boot-starter-oauth2-resource-server dependency (see above).

Configure JWT decoding (if tokens are JWTs) in application.yml:

spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          jwk-set-uri: https://YOUR_AUTH_SERVER/.well-known/jwks.json


Configure HTTP Security:

@Override
protected void configure(HttpSecurity http) throws Exception {
    http
      .authorizeRequests()
        .anyRequest().authenticated()
      .and()
        .oauth2ResourceServer()
          .jwt();
}

<img width="782" height="247" alt="image" src="https://github.com/user-attachments/assets/f7357531-cdab-4f77-9dbc-9d1370838b12" />
