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
- SQ Scanner is a command line tool or plugin that is used to analyse source code and send results to SQ server for inspection
- It is bridge between codebase and SQ dashboard

- It is used to collect ans submit code analysis results, test reports, code metrics to dashboard

- Scanner for maven
  - Uses sonar:sonar goal
  - Command :- mvn clean verify sonar:sonar
 
---------------------------------------------------------------------------------  

Explain sonar-project.properties file
- 
- It is a config file used by Sonar Scanner to define project specific analysis settings
- It tells SQ what to analyse, where to find it, how to handle it

- It contains :-
  - sonar.projectKey :- Unique key to identify project in SQ
  - sonar.projectName :- Human readable project name
  - sonar-sources :- paths of source code
  - sonar.exclusions :- files/folders to exclude from analysis
  - sonar.login :- auth token
 
---------------------------------------------------------------------------------

What are some default rules or standards SonarQube uses for code quality checks?
-
- SQ has set of default rule sets and quality standards tailored to each programming language.
- These rules are grouped into 5 issue types :- Bugs, Vulnerabilities, Code smells, security hotspots and Coverage

- Language specific rules
- Built in security rules
- Maintainability and readability rules (code smells)
- Coverage and test rules
- Reliability rules (bugs)

---------------------------------------------------------------------------------

Where does SonarQube store its data?
-
- SQ stores data in 2 main places
- Relational DBs (RDBMS) for persistent data
  - Project metadata
  - Code analysis results
  - Quality profiles and gates
  - Plugin configs
 
- File system
  - $SONARQUBE_HOME/data
  - $SONARQUBE_HOME/conf/sonar.properties :- stores config like DB creds, ports
  - $SONARQUBE_HOME/logs :- running logs for troubleshooting
 
---------------------------------------------------------------------------------

What is a “technical debt” in SonarQube and how is it calculated?
-
- It refers to estimated time required to fix all maintainability issues (like code smells) in your codebase.
- Its a way to quantify how much work is needed to make our code clean and maintainable

- It us shown in our project dashboard
- Maintainability rating (A-E) is based on technical debt ratio

- Formula :- Technical debt = (remediation cost / development cose ) * 100
  - Remediation cost :- time to fix all maintainability issues
  - Development cost :- estimated time to write code base
 
![image](https://github.com/user-attachments/assets/21845e8f-27fd-4a61-ae45-383d4395a732)

---------------------------------------------------------------------------------
