# JUnit – Overview & Basics

## What is JUnit?

JUnit is a widely-used open-source testing framework for Java. It provides annotations and assertions to write and run repeatable automated unit tests, helping developers ensure code correctness and reliability.

---

## Key Features

- **Annotations:** Identify test methods, setup, teardown, and more (`@Test`, `@BeforeEach`, `@AfterEach`).  
- **Assertions:** Verify expected outcomes (`assertEquals`, `assertTrue`, `assertThrows`, etc.).  
- **Test Suites:** Group multiple test classes to run together.  
- **Integration:** Supported by most IDEs, build tools (Maven, Gradle), and CI/CD pipelines.  
- **Extensible:** Supports parameterized tests, custom runners, and extensions.

---

## How JUnit Works

1. Write test methods in classes annotated with `@Test`.  
2. Use assertions to validate code behavior.  
3. Run tests via IDE, Maven/Gradle, or command line.  
4. Review test results and fix failing tests.

---

## Basic Example

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void additionShouldReturnCorrectSum() {
        Calculator calc = new Calculator();
        int result = calc.add(2, 3);
        assertEquals(5, result, "2 + 3 should equal 5");
    }

    @Test
    void divisionShouldThrowExceptionWhenDivideByZero() {
        Calculator calc = new Calculator();
        assertThrows(ArithmeticException.class, () -> calc.divide(10, 0));
    }
}
---

<img width="809" height="375" alt="image" src="https://github.com/user-attachments/assets/1c6e6486-9af1-4675-83de-85db65408430" />

## Running Tests with Maven
  Add JUnit 5 dependency to your pom.xml:
  <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>5.10.0</version>
      <scope>test</scope>
  </dependency>


## Run tests:
    mvn test
