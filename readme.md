# Setting Up a Java Project with IntelliJ IDEA, Maven/Gradle, and Serenity

Follow these detailed steps to set up your Java project using IntelliJ IDEA and Maven or Gradle for your test framework, along with Serenity:

## Step 1: Setting Up the Project in IntelliJ IDEA

1. **Open IntelliJ IDEA**:
   - If you don't have IntelliJ IDEA installed, download and install it from the JetBrains website.
   - Launch IntelliJ IDEA.

2. **Create a New Project**:
   - On the IntelliJ IDEA welcome screen, select "New Project."
   - In the New Project window, choose "Maven" or "Gradle" on the left panel depending on your preference.
   - Ensure the "Java" option is selected and the JDK is set (download a JDK if necessary).
   - Click "Next" to proceed.

3. **Configure Project Details**:
   - Enter your project's "GroupId" (e.g., com.example) and "ArtifactId" (e.g., currency-api-test).
   - Define the project name and location.
   - Click "Finish" to create the project.

4. **Add Dependencies**:
   - For Maven: Open the pom.xml file and add dependencies for Cucumber, JUnit, RestAssured, and Serenity. Here's an example of what the dependencies might look like:

```xml
<dependencies>
  <!-- Cucumber -->
  <dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>7.0.0</version>
    <scope>test</scope>
  </dependency>
  <dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-junit</artifactId>
    <version>7.0.0</version>
    <scope>test</scope>
  </dependency>

  <!-- JUnit -->
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
  </dependency>

  <!-- RestAssured -->
  <dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>rest-assured</artifactId>
    <version>4.3.3</version>
    <scope>test</scope>
  </dependency>

  <!-- Serenity -->
  <dependency>
    <groupId>net.serenity-bdd</groupId>
    <artifactId>serenity-core</artifactId>
    <version>3.1.5</version>
    <scope>test</scope>
  </dependency>
  <dependency>
    <groupId>net.serenity-bdd</groupId>
    <artifactId>serenity-junit</artifactId>
    <version>3.1.5</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

- After adding the dependencies, IntelliJ should automatically start downloading them. If it doesn’t, you can trigger a reload of the project.


5. **Enable Annotation Processing (if necessary):**
- Go to “File” > “Settings” > “Build, Execution, Deployment” > “Compiler” > “Annotation Processors.”
- Check “Enable annotation processing.”
- Click “Apply” and “OK.”

6. **Create Base Project Structure:**
- Organize your project with directories for your features, step definitions, and utility classes within the src/test/java and src/test/resources folders.

# Step 2: Project Structure for BDD Testing with Serenity

Proper project structuring is crucial for maintaining a clear and manageable codebase, especially when integrating Serenity for BDD testing. Follow these guidelines to structure your Maven or Gradle project in IntelliJ IDEA.

## Main Source Directory

- **Location**: `src/main/java`
- **Purpose**: Contains the main source code of your application.
- **Note**: Even though the focus is on testing, it's good practice to maintain this standard structure.

## Test Source Directory

- **Location**: `src/test/java`
- **Purpose**: Houses all your test code, including BDD step definitions and supporting Java classes.
- **Structure**:
  - Store your BDD step definitions and any supporting Java classes here.
  - Organize step definitions and helper classes into appropriate packages, for example, `cloud.digitalchain.currencyapitest.steps` and `cloud.digitalchain.currencyapitest.utils`.

## Resource Directories

### Main Resources

- **Location**: `src/main/resources`
- **Purpose**: Stores configuration files and other necessary resources for the application.
- **Note**: This directory might not be heavily used in the context of this project.

### Test Resources

- **Location**: `src/test/resources`
- **Purpose**: Crucial for storing Cucumber feature files.
- **Structure**:
  - Create a `features` directory to contain your `.feature` files.
  - These feature files should define your BDD scenarios using Gherkin syntax.

## Configuring Cucumber with Serenity

Set up a Serenity-enabled Cucumber runner class to benefit from enhanced reporting and test management capabilities:

- **Example `TestRunner` class with Serenity**:

  ```java
  package cloud.digitalchain.currencyapitest;

  import net.serenitybdd.cucumber.CucumberWithSerenity;
  import io.cucumber.junit.CucumberOptions;
  import org.junit.runner.RunWith;

  @RunWith(CucumberWithSerenity.class)
  @CucumberOptions(
      features = "src/test/resources/features",
      glue = "cloud.digitalchain.currencyapitest.steps",
      plugin = {"pretty", "html:target/cucumber-reports"}
  )
  public class TestRunner {
  }
# Step 3: Writing BDD Features and Scenarios with Serenity

For Step 3, we'll focus on writing BDD features and scenarios using Cucumber and Serenity in the IntelliJ IDEA environment. We'll create a feature file that describes the behavior of the USD exchange rate API, with a particular focus on fetching the USD to AED rate and validating various response aspects.

## 1. Create a Feature File

- **Location**: Place your feature file in the `src/test/resources/features` directory.
- **File Creation**: Create a new file named `USDRateValidation.feature`.
- **Content**: Feature files should have the `.feature` extension and contain text written in Gherkin syntax, which can be understood in plain English (or your chosen language).

## 2. Define the Feature and Scenarios

- **Feature Definition**: Start by defining the feature and outlining its purpose. Then, detail the scenarios using Given, When, Then, And steps.

### Example Content for `USDRateValidation.feature`:

```gherkin
Feature: Validate USD exchange rate API responses

  The API at 'https://open.er-api.com/v6/latest/USD' should return valid and accurate exchange rate data for USD against multiple currencies, specifically focusing on the USD to AED rate.

  Scenario: Successful API call returns valid USD to AED rate
    Given I make a request to the USD exchange rate API with Serenity
    When I receive the response
    Then the status code should be 200
    And the response status should indicate success
    And the USD to AED rate should be between 3.6 and 3.7
    And the response should include a timestamp
    And the API response time should be less than 3 seconds
    And the response should contain 162 currency pairs

  Scenario: API returns a failure status
    Given I make a request to the USD exchange rate API with Serenity
    When I receive the response
    Then the response status should indicate failure
    And the error message should be descriptive

  Scenario: Validate JSON schema of the API response
    Given I make a request to the USD exchange rate API with Serenity
    When I receive the response
    Then the response should match the expected JSON schema

