# SonarQube

- Sonarqube is an open source web based tool to manage code quality and code analysis. It is most widely used in continuous code inspection which performs reviews of code to detect bugs, code smells and vulnerability issues of programming languages like PHP, C#, Java, JS, etc
- It maintains high code quality by providing automated code reviews and continuous inspection using CICD pipelines
- Also tracks statistics and creates charts that enable developers to quickly identify problems in their code.
- Catch tricky bugs to prevent undefined behavious from impacting end-users
- Fix vulnerabilities that compromise your application
- Makes sure your codebase is clean and maintainable to increase developer velocity

Features of SonarQube
-
- Open source
- Static Code coverage :- Indentifies potential issues without executing code
- Enhance your workflow with Continuous code quality and code security
- Compatible with various programming languages
- Detects redundancy in code and test cases gnerating reports after it
- Gives comparison between current and past report
- Easily integrates with build tools like maven, ant, gradle
- Integration with CICD pipelines :- Works with Jenkins, GitHub actions, GitLab CICD
- Estimates time required to fix detected issues

Sonar Scanner
-
- Performs code analysis, generates results and sends results to sonarqube. It is generic, CLI scanner and we must provide configurations that list locations of source files, test files, sonar host and URL with domain name.
- It performs static code analysis and collects data on bugs, vulnerabilities, code smells and security issues

- Types of Scanners:-
  - SonarScanner CLI :- Standalone CLI
  - SonarScanner for maven
  - SonarScanner for Gradle
  - SonarScanner for .NET
 
- How it Works?
  - Run the scanner on your project (sonar-scanner or mvn sonar:sonar)
  - Collects metrics from source code
  - Sends data to sonarqube
  - Generates reports on code quality, bugs and vulnerabilities
 
- Sonarqube is used to automate continuous code quality and security.
- We must have Jenkins and Sonarqube on system.
