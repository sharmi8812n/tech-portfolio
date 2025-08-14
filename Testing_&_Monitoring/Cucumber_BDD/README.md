# Cucumber BDD – Overview & Basics

## What is Cucumber?

Cucumber is a popular open-source tool for Behavior-Driven Development (BDD). It allows writing tests in a natural language style (Gherkin syntax), making tests understandable by non-technical stakeholders and bridging the gap between business and technical teams.

---

## Key Concepts

| Term            | Description                                         |
|-----------------|-----------------------------------------------------|
| **Feature**     | High-level description of a software feature.      |
| **Scenario**    | A concrete example or test case within a feature.  |
| **Given**       | Precondition or context.                            |
| **When**        | The action or event.                                |
| **Then**        | The expected outcome or assertion.                 |
| **Step Definitions** | Code that executes the steps written in Gherkin. |

---

## Gherkin Syntax Example

Feature: Login functionality

  Scenario: Successful login with valid credentials
    Given the user is on the login page
    When the user enters valid username and password
    Then the user is redirected to the dashboard
    
## How Cucumber Works

    Write features and scenarios in .feature files using Gherkin language.
    Implement step definitions in your preferred programming language (Java, JavaScript, Ruby, etc.).
    Run tests using Cucumber test runner integrated with your build tool or IDE.
    Generate readable reports showing test results.

## Java + Cucumber Basic Setup
### 1. Add Dependencies (Maven example)
<dependencies>
    <!-- Cucumber Java -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>8.15.0</version>
        <scope>test</scope>
    </dependency>

    <!-- Cucumber JUnit -->
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-junit</artifactId>
        <version>8.15.0</version>
        <scope>test</scope>
    </dependency>

    <!-- JUnit -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>

### 2. Feature File Example (src/test/resources/features/login.feature)
  Feature: Login
    Scenario: Successful login
      Given the user is on login page
      When the user enters valid credentials
      Then the user should be redirected to the homepage

### 3. Step Definitions (src/test/java/stepdefinitions/LoginSteps.java)
    import io.cucumber.java.en.*;
    public class LoginSteps {
    
        @Given("the user is on login page")
        public void user_on_login_page() {
            // Code to navigate to login page
        }
    
        @When("the user enters valid credentials")
        public void user_enters_credentials() {
            // Code to enter username and password
        }
    
        @Then("the user should be redirected to the homepage")
        public void user_redirected_homepage() {
            // Code to verify user redirected
        }
    }

### 4. Test Runner (src/test/java/testrunner/TestRunner.java)
    import org.junit.runner.RunWith;
    import io.cucumber.junit.Cucumber;
    import io.cucumber.junit.CucumberOptions;
    
    @RunWith(Cucumber.class)
    @CucumberOptions(
        features = "src/test/resources/features",
        glue = {"stepdefinitions"},
        plugin = {"pretty", "html:target/cucumber-reports.html"},
        monochrome = true
    )
    public class TestRunner {
    }

### Running Tests

    Run via your IDE’s JUnit test runner or:
    mvn test
