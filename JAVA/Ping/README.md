# Ping Authentication Integration with Java Spring Boot

This README outlines how to integrate **Ping Identity** authentication (PingFederate or PingOne) into a Spring Boot application for secure user authentication via SSO / OAuth / OIDC.

---

## What is Ping Authentication?

Ping Identity provides enterprise-grade identity management and Single Sign-On (SSO) solutions. PingFederate and PingOne are products that act as OAuth2 and OpenID Connect (OIDC) compliant Authorization Servers to enable secure authentication workflows.

---

## Key Features of Ping Identity

- **Single Sign-On (SSO):** Seamless login experience across multiple applications.
- **OAuth 2.0 & OpenID Connect (OIDC):** Industry standard protocols supported for secure authorization and authentication.
- **Multi-Factor Authentication (MFA):** Enhance security by requiring multiple verification methods.
- **Adaptive Authentication:** Risk-based policies that adjust authentication requirements dynamically.
- **Identity Federation:** Support for SAML and other federation protocols.
- **User Management & Provisioning:** Centralized user directory integration and lifecycle management.
- **Access Security:** Fine-grained access control with policies based on user, device, and location.
- **API Security:** Secure APIs using OAuth tokens issued by Ping.
- **Scalability & High Availability:** Enterprise-grade performance with failover support.
- **Extensibility:** Customizable login workflows and token claims.
- **Developer Friendly:** APIs and SDKs to integrate easily with applications.

---

## How Ping Authentication Works

- The client app redirects users to Ping’s login page.
- Users authenticate via PingFederate or PingOne.
- After successful login, Ping issues an **ID Token** (OIDC) and/or **Access Token** (OAuth2).
- The client app receives the tokens and uses them to authenticate requests or access APIs.

---

## Integrating Ping Authentication with Spring Boot

### 1. Add Dependencies

<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>

### 2. Configure application.yml
spring:
  security:
    oauth2:
      client:
        registration:
          ping:
            client-id: YOUR_CLIENT_ID
            client-secret: YOUR_CLIENT_SECRET
            scope:
              - openid
              - profile
              - email
            redirect-uri: "{baseUrl}/login/oauth2/code/ping"
            authorization-grant-type: authorization_code
            client-authentication-method: post
        provider:
          ping:
            authorization-uri: https://ping.example.com/as/authorization.oauth2
            token-uri: https://ping.example.com/as/token.oauth2
            user-info-uri: https://ping.example.com/idp/userinfo.openid
            user-name-attribute: sub

### 3. Security Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http
      .authorizeRequests()
        .antMatchers("/", "/login**").permitAll()
        .anyRequest().authenticated()
      .and()
        .oauth2Login()
          .loginPage("/login")
          .defaultSuccessUrl("/dashboard", true);
  }
}

### 4. Handling User Info
@GetMapping("/dashboard")
public String dashboard(OAuth2AuthenticationToken authentication) {
  Map<String, Object> userAttributes = authentication.getPrincipal().getAttributes();
  return "Welcome, " + userAttributes.get("name");
}
