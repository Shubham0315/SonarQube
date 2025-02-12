# SonarQube

- Sonarqube is an open source web based tool to manage code quality and code analysis. It is most widely used in continuous code inspection which performs reviews of code to detect bugs, code smells and vulnerability issues of programming languages like PHP, C#, Java, JS, etc
- It maintains high code quality by providing automated code reviews and continuous inspection using CICD pipelines
- Also tracks statistics and creates charts that enable developers to quickly identify problems in their code.
- Catch tricky bugs to prevent undefined behavious from impacting end-users
- Fix vulnerabilities that compromise your application
- Makes sure your codebase is clean and maintainable to increase developer velocity

SonarQube does 2 tasks :
1. Code Coverage
- When sonarqube generates report on code coverage, it generates in percentage. Means x% of our source code is run or tested. In most companies they require code coverage of at least 80% should be tested.

2. Code Quality Check
- When we say our source code has multiple issues, it can have bugs, vulnerabilities, code smells. All of these should be minimal in our source code.
- Bugs happen due to wrong coding (improper code)
- Vulnerability is a section of our csource code whic is open to attack even if it is working but can be bypassed.
- Code smell is section of source code which is poorly written and creates confusion in code.

Install and Setup Sonarqube
- Create sonarqube server using docker installed in our machine(recommended for linux ubuntu)
- Command :- **docker run -d --name sonar -p 9000:9000  sonarqube:lts-community**        #donwloads sonarqube lts version image
- To login sonarqube :- **http://localhost:9000**        #localhost can be changed with jenkins URL
- **Quality Profiles**, we can have default profiles set for respective langauges. We can also create custom profiles for us
- If we need to install profile for some langauge, administration - marketplace - search and download

![image](https://github.com/user-attachments/assets/786506c6-1391-4fb4-8241-c43f602f380e)

- In administartion - syatem, we can check health of our sonar server
- **Quality gates** :- Here we can set certain conditions. We can also create conditions as per need

![image](https://github.com/user-attachments/assets/8fca06f0-25ce-4646-92c5-bbb8cfb91321)

- **Rules** :- We've all the rules for our projects acc to langauge.

![image](https://github.com/user-attachments/assets/be05b2de-bdbf-456e-bb3e-a79d708f2ff6)

Features of SonarQube
-
- Open source
- Static Code coverage :- Indentifies potential issues without executing code
- Enhance your workflow with Continuous code quality and code security
- Compatible with various programming languages
- Detects redundancy in code and test cases generating reports after it
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
![image](https://github.com/user-attachments/assets/89ccd59d-0e04-452c-8d5e-fc36905f555c)


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Create pipeline and take code from jenkinsfile in GitHub and then do code analysis
-
- Define pom.xml and jenkinsfile in GitHub
- In pom.xml, define dependencies such as project name (devops-app), define some plugins inside it. Main plugin is sonar-maven-plugin with version. Inside profile define sonar-host-url inside properties tag

![image](https://github.com/user-attachments/assets/51b783c2-c9f5-46c4-b56e-6c399136dd48)
![image](https://github.com/user-attachments/assets/bed908fe-9871-49ec-af24-48850615e75f)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Another way to create pipeline and use sonarqube for code analysis
-
- Create pipeline project. Define github project URL in general section

![image](https://github.com/user-attachments/assets/bcd54919-2460-4cb7-8d8c-18807da6ee5d)

- Now in the pipeline scetion, select definition as "pipeline script from SCM", select SCM as GIT, provide branch, URL details

![image](https://github.com/user-attachments/assets/8cb6c2c0-5bcc-42b0-829f-ff0e2f379606)

- In script path, provide path of jenkinsfile. If jenkinsfile is not present in root, provide appropriate relative path. In jenkinsfile we write pipeline script. Whatever name we provide in Now Manage jenkins - System - SonarQube servers - Add server while configuring sonar in jenkins, we've to provide the same in our pipeline script

![image](https://github.com/user-attachments/assets/8aefbe91-a3b7-4a5e-bc52-8e83ce8044fb)
![image](https://github.com/user-attachments/assets/248972ec-8be5-46a0-bbf5-1fd5b04161e2)

- Now we can Build this jenkins pipeline

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Project :- CICD Pipeline using Sonarqube
-
- Install sonar and JDK plugin
- Manage jenkins - Global tool config - JDK add (11) (auto install)

![image](https://github.com/user-attachments/assets/e6d0c639-2a31-4263-8a60-295ae9d01761)

- Go to Manage jenkins - Global tool config - Maven - version - Apply
  - Now all the tools JDK, Maven and Sonar are configured
 
- Now create a new pipeline named :- sonar-analysis. Select log rotation

![image](https://github.com/user-attachments/assets/f47d3f42-0764-42a9-855b-1f5204c1272c)
![image](https://github.com/user-attachments/assets/9b3d2093-ee4c-4f36-8538-0b7066fb5214)

- Create sample pipeline in pipeline section "Hello Wold" option/ Define tools here

![image](https://github.com/user-attachments/assets/9a44de46-4d11-4cad-bc5c-68104a21a5d2)

- Now inside stages, provide git checkout stage URL. Go to pipeline syntax - select git - provide URL - Generate pipeline script. Copy and paste in pipeline code

![image](https://github.com/user-attachments/assets/bb30f2d6-ba1c-4f76-a361-3be8c832fc02)
![image](https://github.com/user-attachments/assets/2baabf79-f7e5-47c7-9b50-10b2b41b7954)

- Now next stage is sonar analysis. For that we've mvn clean package to build app and generate artifact
  - Now we can write sonar analysis command. In which we define sonar URL, for authentication we provide token. (Administration - security - token - generate). Also provide project name , java binaries (in root dir so .) and project key similar to project name

![image](https://github.com/user-attachments/assets/7d720a55-f6f3-4e3b-a615-594f7b4e2373)

- Now when we run the pipeline, it will unpack the jdk as we're building pipeline fopr first time. Now when we go to sonarqube and check the analysis of project, it will show like below

![image](https://github.com/user-attachments/assets/c07c0cfd-bf7d-417f-8257-4e14ad6be3c2)

- We can also check issues details. Here we can see what is blocker, critical, major, minor

![image](https://github.com/user-attachments/assets/656b6cf1-e12e-4f93-b8f1-549f4ce3fd9f)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Explain sonarqube parameters
-
- In jenkins pipelkines SonarQube parameters are used to configure and execute sonar analysis for code quality checks. These parameters are typically passed to **sonar-scanner** or **SonarQube Scanner for Jenkins** plugin

1. Project Information
- sonar.projectKey :- Unique identifier for project
- sonar.projectName
- sonar.projectversion

2. Source Code Configuration
- sonar.sources :- Comma separated paths for source code directories
- sonar.exclusions :- files/directories to exclude from analysis
- sonar.language :- language of project

3. Code coverage and testing
- sonar.coverage.exclusions :- Paths to exclude from code coverage
- sonar.test.exclusions :- Paths to exclude from test analysis

4. Branch and Pull requests analysis
- sonar.branch.name
- sonar.pullrequest.key :- Pull request identifier
- sonar.pullrequest.branch :- Source branch of PR

5. Authentication and Server config
- sonar.host.url :- URL of SQ server
- sonar.login :- auth token or username
- sonar.password

6. Build and SCM config
- sonar.scm.provider :- SCM tool
- sonar.gitlab.project_id :- GitLab project ID
- sonar.github.repository :- GitHub repo name

Below is the example of how to use sonar parameters. Also includes use of custom env variables to use 

![image](https://github.com/user-attachments/assets/28a7f1e8-3ff8-4d86-9d0f-15a99576d332)


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Configuring SonarQube for high availability and scalability
-
- Configuring SQ for HA and scalability involves setting up multiple components to esnure that system remains available even if one component fails and it can handle increased load as nummber of users or projects grows

- High availability SQ setup includes:-
  - Load balancer to distribute traffic such as HAProxy, ELB, Nginx
  - Multiple SQ app nodes
  - Dedicated DB server like SQL/PostgreSQL
  - Shared storage to maintain consistent config and data between nodes
  - Elastic cluster setup
  - Sonarqube app node configuration in sonar.properties file
  - Monitoring and scaling
  - Backup and DR
 
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Automating quality gate enforcement in CI/CD
-
- Automating quality gate enforcements in CICD ensures code changes meet predefined quality standards before they are merged or deployed. SQ integrates seamlessly into CICD pipelines to enforce quality gates, preventing builds from passing if they dont meet set thresholds for code coverage, bugs, vulnerabiloties, code smells.

- Quality gate is a set of conditions that code must meet to be considered prod-ready. It is to set up conditions to fail the build if quality gate fails and notify team on failure.

- Prerequisites are SQ server, SQ Scanner (ON CICD runner/agent), SQ token, Jnekins for CICD

- To setup quality gates - SQ - Administration - Quality Gates (Coverage 80%, No new critical bugs or vulnerabilities, Maintainability Rating = A)

- We can also integrate SQ with email or slack for notifications on failure
  - In jenkins - Email extansion plugin
 
- Best practices :-
  - Fail Fast :- Enforce QG early in pipeline to save time and resources
  - Branch Analysis
  - Incremental analysis to focus on new code to maintain legacy code
  - For security use env variables
 
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Configuring language-specific analyzers in SonarQube
-
- Configuring language specific analyzers in SQ enhances code analysis by applying relevant rules and metrics tailored to programming langauges used in our projects. This ensures more accurate quality gates, better detection of bugs, smells and overall improved quality code
- They parse the code and detect language specific issues. Apply rules in quality profiles and generate metrics like code coverage, duplications (Java, C#, C++, Python, JS, XML)
- Prerequisites are SQ server, SQ scanner or language specific scanner (Maven/gradle), build env for same (JDK, Nodejs)

- To install and update
  - Administration - Marketplace - Search SonarGo(Required plugin) - Install and Restart SQ
 
- Configure Language-specific settings
  - Administration - General settings - Language select - Configure (just like properties file in Gitlab)
 
- Set up quality profile
  - Quality Profiles - Language select - Activate/deactivate rules - Create custom profiles
 
- Integrate Language specific analyzers with pipelines

  ![image](https://github.com/user-attachments/assets/fc61ed89-0ceb-4263-9cd5-50da8a7ecb75)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Difference between quality gates and quality profiles  in sonarqube
-
- Quality gates determine whether the code meets defined quality standards to pass or fail in analysis. They are evaluative and used to enforce quality rules before merging or deploying code.
  - They provide pass fail criteria based on conditions (Code coverage 80%, No bugs/vulnerabilities)
  - Applicable to new code or entire codebase
  - If quality gates fail, directly affects pipeline blocking deployments
 
![image](https://github.com/user-attachments/assets/c88343c0-52b1-41f8-a28a-ea1c67a70582)

 
- Quality profiles define set of rules that SQ uses to analyse source code. These are kind of rules sets for each language.
  - Rules definition :- determine which rules are enabled or disabled during analysis
  - Language specific
  - We can create custom profiles by enabling and disabling rules
  - SQ provides default profiles which can be customized as well
  - SQ UI :- Quality profiles - Configure
 
![image](https://github.com/user-attachments/assets/6aa5e386-6116-44bd-b25f-0f2292db9d2b)

- How Profiles and gates work together?
  - Quality profiles analyze source code and generate issues bases on rules
  - QG then evaluates these issues against defined conditions. If conditions are met QG pass, if fail blocks pipeline

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- 

What are common issues when integrating SonarQube with CI/CD pipelines?
-

1. Authentication and Authorization Issues
- Invalid auth tokens
- Insufficient permissions for SQ account to create projects or update analysis results
- We can use Personal access tokens with least privilege, store tokens securely as env variables, regularly update tokens

2. Compatibility and Version mismatch
- SQ version mismatch, Plugin/build tool incompatible
- We can regularly update SQand its plugins

3. Network and connectivity issues
-  Firewall restrictions :- As CICD agents cannot reach SQ server due to firewall issues
-  Incorrect proxy configurations
- Ensure network rules allow traffic on SQ port 9000, configure proxy settings in SonarScanner or CICD env, use correct DNS enteries for connectivity

4. Incorrect SonarScanner Configuration
- Wrong project key/name :- Leads to project duplications or overwriting existing projects
- Misconfigured source or tests path
- For this we can define sonar.projectKey, sonar.sources, sonar.tests in properties files

5. Insufficient Resource Allocation
- Out of memory errors
- Slow analysis or timeouts

![image](https://github.com/user-attachments/assets/f66879e6-bb14-4956-b758-6de78f6dae3c)

6. Multi language project issues
- Incorrect langauge detection as SQ misidentifies primary language, leading to incomplete analysis
- Multi langauge projects struggle with aggregating coverage reports
- For this we can explicitly define languages and sources in properties file

![image](https://github.com/user-attachments/assets/89297633-d792-4ca6-91c5-63b905de3f05)

7. Security and Access Control issues
- Unauthorized access or incorrect permissions on SQ projects
- We can use token based authentication with minimal permissions and store tokens securely using CICD secrets management

* To troubleshoot :- Check logs (web.log, ce.log, es.log), enable debug mode by setting sonar.verbose=true, implement retry logic in CICD to handle network issues
* Start with efault quality profiles, incremental quality gate enforcement, regular updates

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How do you debug SonarQube scanner failures?
-
- Debugging SQ Scanner failures requires systematic approach to identify and resolve issues effectively

1. Enable Debug Logging
- Used to get detailed error messages. To check ERROR, WARN or EXCEPTION keywork in logs
- To enable debug mode for maven :- **mvn sonar:sonar -X -Dsonar.verbose=true**

2. Check SQ Server Logs
- Logs directory :- $SONARQUBE_HOME/logs
- web.log, ce.log, es.log, sonar.log
- Common issues are :- auth errors, network connectivity, elasticsearch errors
- Command :- **tail -f /opt/sonarqube/logs/ce.log**

3. Validate Config settings
- sonar.projectKey, sonar.sources need to be correctly set
- Common issues are incorrect project key, Invalid HOST URL, missing auth token

4. Network connectivity and proxy settings
- Test network connectivity, check proxy settings

5. Verify authentication and permissions
- Invalid token, lack of permissions

6. Compatibility and version mismatch
- Ensure compatibility between SQ, SonarScanner and plugins

7. Common build tool issues
- Incorrect plugin version or missing sonar.login
- mvn sonar:sonar -Dsonar.login=your-token-here

** Clear cache :- sonar.scanner -X --cache-clear
