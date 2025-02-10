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

Install SonarQube scanner plugin in jenkins and configure sonarqube in Jenkins
-
- Manage jenkins - Plugins - Sonarqube scanner

![image](https://github.com/user-attachments/assets/31cb9259-da3b-4412-bf1a-896a91d4d4f4)

- Now to configure this plugin in jenkins
  - Manage jenins - tools - SonarQube scanner - Name as SonarQube

![image](https://github.com/user-attachments/assets/8ce515b5-978d-44af-be53-fd289d503b35)

- Now Manage jenkins - System - SonarQube servers - Add server
  - Here provide URL of sonarqube server. Ig we've launched it using EC2, give that IP here

![image](https://github.com/user-attachments/assets/4e117608-7b10-4eb8-94d1-86950813a614)

  - Also create authentication token here like below - Put kind as Secret text
  - Now go to sonarqube - administration - security - generate token (jenkins pipeline). Put the generated token ID in our jenkins in secret section - Give ID -  add

![image](https://github.com/user-attachments/assets/1b4a214b-20e0-4c1e-bb79-407a5458e9fb)
![image](https://github.com/user-attachments/assets/26ee7c2f-7907-4f74-b024-53fbc9d357be)


Create maven job in jenkins and integrate sonarqube for maven job
-
- Create new job as maven project

![image](https://github.com/user-attachments/assets/67d5239d-b887-44af-b1ca-caad460691cd)

- Provide github project URL

![image](https://github.com/user-attachments/assets/b395f812-6468-488d-b933-3252230146ee)

- In SCM, provide git repo and branch details

![image](https://github.com/user-attachments/assets/47f7850f-dc48-4611-97bc-e897d42f3af0)
![image](https://github.com/user-attachments/assets/1096960a-148a-4e8e-9773-43ea9213d756)

- In pre steps --> execute sonarqube scanner
  - Here we can either define analysis properties in the box or define them in a file and place in GitHub

![image](https://github.com/user-attachments/assets/e9ef661e-2d3a-42af-9a9f-b2ebae7b9ea5)
![image](https://github.com/user-attachments/assets/a86eb70c-6915-4710-8caa-4bf44f61f862)

- In build section, provide POM and goals

![image](https://github.com/user-attachments/assets/c3050f01-0fe4-42ca-a28d-505948d41d79)

- Now when we build this project, we can go to sonarqube and check if the report for it is generated. It has bugs, defects, vulnerabilities.
- In the jenkins console output of job, we can see our pom.xml file got converted into snapshot file. Whatever name is given in pom will get reflected in sonarqube.

![image](https://github.com/user-attachments/assets/56ba9743-e43b-4889-b0ba-3968e96bf8e9)
![image](https://github.com/user-attachments/assets/0e9d3902-fe9d-48d0-b0cb-fae31040ca25)

