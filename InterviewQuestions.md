What is SonarQube and why is it used in DevOps?
-
- SQ is an open source platform used to continuous inspection of code quality. It performs static code analysis to identify bugs, vulnerabilities, security hotspots, code smells across various programming languages
- Integrating with CICD pipelines, it automatically reviews code on every build or pull request
- Helps enforce coding standards and best practices early in development cycle
- Identifies security vulnerabilities and ensures code follows secure coding huidelines
- Developers get instant feedback through Sonar UI
- Supports multiple languages like Java, Python , JS, C#, GO

---------------------------------------------------------------------------------

What are code smells, bugs, and vulnerabilities in SonarQube?
-
- Bugs are errors in logic or implementation that can cause unexpected behaviour or crashes during rumtime
- Vulnerabilities are security related issues in our code that could be exploited by attackers. Can lead to data leaks, unauthorized access or system compromise (passwords)
- Code smells are maintainability issues that may not directly break the app but make the code hard to read, understand and extand. They make debugging harder (duplicate code, unused variables)

---------------------------------------------------------------------------------

What is a quality gate in SonarQube?
-
- Quality gate in sonarqube is a set of conditions or thresholds that your code must meet to be considered "releaseable" or "prod-ready"
- It is a powerful way to enforce code quality standards in CICD pipelines

- Used to auto evaluate results of SQ analysis and determine if the buiild passed or fails based omn predefiend quality criteria

- Common Quality Gate Conditions:-
  - No new bugs, vulnerabilities
  - Code coverage >= 80%
  - Duplicated lines on new code <= 3%
  - Maintainability rating A, Security rating A
 
- If all conditions are met :- code is clean and safe to proceed

![image](https://github.com/user-attachments/assets/b71d2b80-145a-4b7f-8e85-07a294780797)

---------------------------------------------------------------------------------

How do you integrate SonarQube with Jenkins?
-
- Integrating SQ with Jenkins allows you to automate code analysis as part of CICD pipeline

- Install SQ Scanner Plugin in jenkins
- Configure SQ server in jenkins
  - Manage jenkins - Configure system - Sonaqreube Servers - Add SonarQube URL and auth token (generate from SQ - My account - Security)
 
![image](https://github.com/user-attachments/assets/6126702b-c18e-4c28-9300-394415420308)

- Configure SQ Scanner
  - Manage jenkins - Global Tool Configuration - Sonar Scanner - Add
 
![image](https://github.com/user-attachments/assets/3e18d730-dd40-4e01-8445-4635600a5fa5)

- Now we can add SQ step in our jenkinsfile or use frestyle job defining sonar-project.properties
  - Freestyle Job - Add SQ Scanner step (pre steps) - Provide analysis properties file (sonar-project.properties) - Execute SQ scanner
 
![image](https://github.com/user-attachments/assets/fd7e310b-11c1-48cb-b1a2-3a0dceb88565)

- After successful build, we can go to dashboard in Sonarqube and see bugd, code smells, vulnerabilities

---------------------------------------------------------------------------------

What is a SonarQube scanner?
-
- 
