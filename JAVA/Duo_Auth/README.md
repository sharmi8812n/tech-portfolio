# Duo Security (MFA) Integration with Java Spring Boot

This README explains what **Duo Security** is, its core features, and how to integrate Duo’s Multi-Factor Authentication (MFA) into a Spring Boot application for enhanced security.

---

## What is Duo Security?

Duo Security (by Cisco) is a leading multi-factor authentication (MFA) and zero-trust security platform that helps protect user identities and applications with an additional layer of authentication beyond passwords.

---

## Key Features of Duo Security

- **Multi-Factor Authentication (MFA):** Adds a second factor (push notification, phone call, SMS, hardware token) to verify users.
- **Adaptive Authentication:** Risk-based policies adapting MFA requirements based on device, location, or user behavior.
- **Single Sign-On (SSO) Integration:** Works with existing identity providers (Okta, Azure AD, Ping, etc.).
- **Device Trust:** Checks device security posture before granting access.
- **Easy User Enrollment:** Simple onboarding with self-service portals.
- **Comprehensive APIs & SDKs:** Enables easy integration with custom applications.
- **Mobile App:** Push notifications and token generation on smartphones.
- **Access Policies:** Granular controls based on users, groups, networks, and devices.
- **Reporting & Analytics:** Track login attempts and security events.

---

## How Duo MFA Works

1. User logs in with their primary credentials (username/password).
2. The application triggers Duo MFA verification.
3. Duo sends a push notification or other second factor to the user’s device.
4. User approves the authentication request.
5. Duo confirms and grants access to the application.

---

## Integrating Duo with Java Spring Boot

### 1. Set Up Duo Account

- Create a Duo Developer account: https://duo.com/developers
- Create a new application in Duo Admin Panel to get **Integration Key**, **Secret Key**, and **API Hostname**.

### 2. Add Duo Web SDK Dependency

Add Duo Web SDK to your project (download or via Maven if available).

*(Duo does not have an official Java SDK for MFA; often you integrate via REST API or embed Duo’s iframe on login page.)*

---

### 3. Example Integration Flow

- After validating username/password, present Duo’s MFA prompt using their iframe or REST API.
- Validate the Duo response on your server with Duo’s API.
- Proceed only if the second factor is successful.

---

### 4. Sample Duo Verification Using Duo Web SDK (simplified)

```java
import com.duosecurity.duoweb.*;

public class DuoService {
    private static final String IKEY = "YOUR_INTEGRATION_KEY";
    private static final String SKEY = "YOUR_SECRET_KEY";
    private static final String AKEY = "YOUR_APPLICATION_SECRET_KEY";  // random secret

    // Generate Duo Signed Request for the iframe
    public String generateSignedRequest(String username) {
        return DuoWeb.signRequest(IKEY, SKEY, AKEY, username);
    }

    // Verify Duo response after user completes MFA
    public String verifyResponse(String sigResponse) {
        return DuoWeb.verifyResponse(IKEY, SKEY, AKEY, sigResponse);
    }
}
