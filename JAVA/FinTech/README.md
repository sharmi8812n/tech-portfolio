# Fintech Application with Java Spring Boot 

This project provides a foundation for building fintech applications using **Java 8** and **Spring Boot**. It includes account management, transaction processing, and guidance on integrating **PayPal** for digital payments.

---

## What is Fintech?

**Fintech** (financial technology) innovates financial services by leveraging technology such as digital payments, online banking, lending, and investment platforms, aiming for speed, security, and convenience.

---

## Project Overview

- User accounts and transaction management
- RESTful APIs with Spring Boot
- H2 in-memory database for development/testing
- Integration steps for PayPal payments compatible with Java 8

---

## Prerequisites

- Java JDK 8
- Maven or Gradle
- IDE (IntelliJ IDEA, Eclipse, etc.)
- Basic Spring Boot and REST API knowledge

---

## Getting Started

### 1. Create Spring Boot Project

Use [Spring Initializr](https://start.spring.io/) and select Java 8 with dependencies:

- Spring Web
- Spring Data JPA
- H2 Database
- Lombok (optional)
- Spring Security (optional)

### 2. Configure `application.properties`

properties

server.port=8080

spring.datasource.url=jdbc:h2:mem:fintechdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update

spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

---
### 3. Define Account Entity and Controllers

Create your entities, repositories, services, and REST controllers to manage accounts and transactions.

Integrating PayPal Payments (Java 8 Compatible)
1. Setup PayPal Developer Account
Register at PayPal Developer
Create a Sandbox business account
Create REST API app; get Client ID and Secret

2. Add PayPal SDK Dependency
Add to your pom.xml:
<dependency>
    <groupId>com.paypal.sdk</groupId>
    <artifactId>paypal-checkout-sdk</artifactId>
    <version>1.0.3</version>
</dependency>

3. Configure PayPal Client
Create a Spring service class for PayPal client setup:
import com.paypal.core.PayPalEnvironment;
import com.paypal.core.PayPalHttpClient;
import org.springframework.stereotype.Service;

@Service
public class PayPalClient {

    private PayPalHttpClient client;

    public PayPalClient() {
        PayPalEnvironment environment = new PayPalEnvironment.Sandbox(
            "YOUR_CLIENT_ID",
            "YOUR_CLIENT_SECRET"
        );
        this.client = new PayPalHttpClient(environment);
    }

    public PayPalHttpClient client() {
        return client;
    }
}
Replace "YOUR_CLIENT_ID" and "YOUR_CLIENT_SECRET" with your sandbox credentials.

4. Create Payment Orders

Implement order creation logic (Java 8 compatible, avoid var or lambdas in API calls):

import com.paypal.orders.*;
import com.paypal.http.HttpResponse;

import java.io.IOException;
import java.util.Arrays;

public class PayPalService {

    private PayPalHttpClient client;

    public PayPalService(PayPalHttpClient client) {
        this.client = client;
    }

    public Order createOrder(String currency, String value) throws IOException {
        OrderRequest orderRequest = new OrderRequest();
        orderRequest.checkoutPaymentIntent("CAPTURE");

        ApplicationContext appContext = new ApplicationContext()
            .brandName("Your Brand")
            .landingPage("NO_PREFERENCE")
            .cancelUrl("https://example.com/cancel")
            .returnUrl("https://example.com/return")
            .userAction("PAY_NOW");
        orderRequest.applicationContext(appContext);

        AmountWithBreakdown amount = new AmountWithBreakdown()
            .currencyCode(currency)
            .value(value);

        PurchaseUnitRequest purchaseUnit = new PurchaseUnitRequest()
            .amountWithBreakdown(amount);

        orderRequest.purchaseUnits(Arrays.asList(purchaseUnit));

        OrdersCreateRequest request = new OrdersCreateRequest();
        request.requestBody(orderRequest);

        HttpResponse<Order> response = client.execute(request);
        return response.result();
    }
}

5. REST Controller Endpoint

Expose the order creation API:

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import com.paypal.orders.Order;

import java.io.IOException;

@RestController
@RequestMapping("/api/paypal")
public class PayPalController {

    private PayPalService payPalService;

    @Autowired
    public PayPalController(PayPalClient payPalClient) {
        this.payPalService = new PayPalService(payPalClient.client());
    }

    @PostMapping("/create-order")
    public ResponseEntity<Order> createOrder(@RequestParam String currency, @RequestParam String amount) {
        try {
            Order order = payPalService.createOrder(currency, amount);
            return new ResponseEntity<Order>(order, HttpStatus.OK);
        } catch (IOException e) {
            e.printStackTrace();
            return new ResponseEntity<Order>(HttpStatus.INTERNAL_SERVER_ERROR);
        }
    }
}

6. (Optional) Capture Payment

Add capture method:

import com.paypal.orders.OrdersCaptureRequest;
import com.paypal.http.HttpResponse;

public Order captureOrder(String orderId) throws IOException {
    OrdersCaptureRequest request = new OrdersCaptureRequest(orderId);
    request.requestBody(new OrderRequest());
    HttpResponse<Order> response = client.execute(request);
    return response.result();
}
Add a controller endpoint if desired.

7. Client-Side Integration
Use PayPal JS SDK or mobile SDKs
Pass the order ID from /create-order to client to approve payment
Capture payment after approval to complete transaction

### Running the Application
./mvnw spring-boot:run
Access H2 console at http://localhost:8080/h2-console.
