

# Selenium Test Automation Framework

This project is a Selenium WebDriver automation framework built with Java, TestNG, Maven and the Page Object Model design pattern.

It supports cross-browser execution on Chrome, Firefox, and Microsoft Edge, with automated HTML reporting, failure screenshots and TestNG listener integration.

## Test Report

After each test run, an HTML report is generated.

Open the report in any browser. No server is required.

Each report entry shows:

* ✅ Pass, ❌ Fail or ⏭️ Skip status per test
* The browser the test ran on
* Failure exception message and stack trace
* Screenshot of the browser at the exact point of failure
* Timestamps and total execution duration
* Environment panel showing project, tester and base URL

> **Important:**  
> The report is only generated when tests are run through Maven or a TestNG XML suite file.  
> Running individual test classes directly from the IntelliJ play button bypasses the listener and no report is produced.

## How to Run

### Prerequisites

Make sure the following are installed:

* Java 21 or later
* Maven
* Google Chrome
* Mozilla Firefox
* Microsoft Edge
* `msedgedriver.exe` placed inside the `drivers/` folder

## Commands

Run all browsers in sequence:

```bash
mvn test
````

Run one browser only:

```bash
mvn test -Dsuite=testng-chrome
mvn test -Dsuite=testng-firefox
mvn test -Dsuite=testng-edge
```

## Run from IntelliJ using the XML Suite

1. Click **Run**
2. Click **Edit Configurations**
3. Set **Test kind** to **Suite**
4. Point the **Suite** field to:

```text
testng-all-browsers.xml
```

5. Click **OK**
6. Run the suite

## Configuration

### Changing the Browser

Pass the suite name as a Maven property:

```bash
mvn test -Dsuite=testng-firefox
```

The default suite is set in `pom.xml`:

```xml
<properties>
    <suite>testng-all-browsers</suite>
</properties>
```

## Suppressing Chrome Password Popups

The following Chrome options are configured in `BaseTest` to prevent password related browser popups from interrupting test execution:

```java
options.addArguments("--disable-save-password-bubble");
options.addArguments("--disable-features=PasswordLeakDetection,SafeBrowsingEnhancedProtection");

options.setExperimentalOption("prefs", Map.of(
    "credentials_enable_service", false,
    "profile.password_manager_enabled", false,
    "profile.password_manager_leak_detection", false
));
```

## Concepts Demonstrated

### Page Object Model

Each application page has a dedicated page class that stores its locators and actions. This keeps UI logic separate from test logic.

### Inheritance

`BasePage` and `BaseTest` remove duplicated setup code across page classes and test classes.

### PageFactory and @FindBy

The framework uses annotation-driven element declarations with `@FindBy`, reducing repeated `driver.findElement(By...)` calls.

### Separation of Concerns

Test classes focus on assertions and workflows, while page classes handle UI interactions and page-specific behaviour.

### Cross Browser Testing

TestNG `@Parameters` and XML suite files allow the same tests to run on Chrome, Firefox and Edge without duplicating test logic.

### TestNG Listeners

The framework uses `ITestListener` to capture pass, fail, and skip events, then write them into the Extent report automatically.

### HTML Reporting

ExtentReports generates a rich, self-contained HTML report after every test run.

### Failure Screenshots

When a test fails, `TakesScreenshot` captures the browser state at the exact point of failure.

### Implicit Waits

A global timeout strategy is used to help handle dynamic page loading.

### TestNG Prioritisation

`@Test(priority = n)` is used to control sequential execution across a stateful multi step test journey.

### Javadoc and Inline Comments

Classes and methods are documented to improve readability and make the project easier to understand as a portfolio piece.

## Tech Stack

* Java
* Selenium WebDriver
* TestNG
* Maven
* ExtentReports
* Page Object Model
* PageFactory
* Chrome
* Firefox
* Microsoft Edge

## Project Purpose

This framework was created to demonstrate practical UI automation testing skills, including cross-browser testing, reporting, screenshots, structured test design and maintainable page object architecture.

```
```
