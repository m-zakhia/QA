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
''
- For Gradle: Open the build.gradle file and add dependencies. Here’s an example for Gradle:
dependencies {
  testImplementation 'io.cucumber:cucumber-java:7.0.0'
  testImplementation 'io.cucumber:cucumber-junit:7.0.0'
  testImplementation 'junit:junit:4.13.2'
  testImplementation 'io.rest-assured:rest-assured:4.3.3'
  testImplementation 'net.serenity-bdd:serenity-core:3.1.5'
  testImplementation 'net.serenity-bdd:serenity-junit:3.1.5'
}

- After adding the dependencies, IntelliJ should automatically start downloading them. If it doesn’t, you can trigger a reload of the project.

5. ** Enable Annotation Processing (if necessary):**
- Go to “File” > “Settings” > “Build, Execution, Deployment” > “Compiler” > “Annotation Processors.”
- Check “Enable annotation processing.”
- Click “Apply” and “OK.”

6. ** Create Base Project Structure: **
- Organize your project with directories for your features, step definitions, and utility classes within the src/test/java and src/test/resources folders.
