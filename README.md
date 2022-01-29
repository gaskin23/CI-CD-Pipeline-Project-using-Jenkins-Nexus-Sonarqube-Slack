# CI-CD-Pipeline-Project-using-Jenkins-Nexus-Sonarqube-Slack

## Description

The aim of this project is to automate the manually progressing project development processes and to provide continuous integration and delivery by reducing the errors that may occur with less human intervention. This project aims to deploy Visual Profile Maven Project to Nexus repository with CI/CD Jenkins using  Sonarqube, Nexus,GİT/Github,Slack and AWS EC2 instance. 

## Tools is Used For This Project

![Project_Tools](./Project-Tools-1.png)

![Project_Tools_2](./Project-Tools-2.png)

## Project Architecture

![Scenario](./Scenario.png)

## Scenario

You have a product development and agile SDLC is in motion, so a bunch of smart developers in an agile team will regularly make changes. So there'll be multiple code changes every day. And all this code needs to be tested because this is what actually is building your product. 

- This code needs to be regularly built and tested. usually in an enterprise, there will be a separate building release team will be doing this job of building, testing and releasing the code, or if it's a small industry, then they'll be it will be developer's responsibility to merge and integrate this code.

- There are regular quote changes also called comments or pull requests, developers will be dependent on building the team, usually to test the code and move it to the next level in the release cycle. 

- The code will be tested if there are any bugs or whether it will be known late due to these bugs and errors in the code. Keep accumulating and let's say these got accumulated. A problem goes much deeper now, developers need to rework to fix these bugs and errors, which is time consuming process and seems would be already approaching the deadline.

## Current Situation

- Agile SDLC
- Developers make regular code changes
- These commits needs to be Build & Tested
- Usually Build & Release Team will do this Job
- Or Developers responsibility to merge an integrate code

## Issues with Current Sıtuation

- In an Agile SDLC, there will be be frequent code changes
- Not so frequently code will be tested
- Which accumulates bugs and error in the code
- Developers need to rework to fix these bugs and error
- Manual Build & Release process
- Inter Team Dependencies

## Solution of This Problem

![Solution](./Solution.png)

1. Build & Test for every commit
2. Automated Process
3. Notify For Every Build Status
4. Fix Code İf bugs or error found instantly rather than waiting

Solution to this problem is a regular build and test for every comet, so as soon as there is a code change, the code needs to be built and tested at the same time. 

-  İf the process is manual, this will not be possible. you need to have an automated building release process. 

-  Whenever there is a big and test of the court, the developers should get notified automatically. if you have such kind of automation framework in place, which will regularly build and test the code for every comic, then you're also removing dependency of developers from building steam. 

-  This process itself is called continuous integration process. So input to this process is any good comic and output will be well tested artifact and all this will happen automatically.

## Project Steps

İn this project, obviously, we're going to set up a continuous integration pipeline:
- Starting with Jenkins, Jenkins will be our continuous integration server and main hero in this project
and as hero needs sidekick, our jenkins' hero will also need some assist in tool.
- We are going to use a version control system, we going to use Git and GitHub as the remote repository, and we have a Java code in that. And to build that Java code, we will need build tool even.
- We are also going to do some cool analysis, so we are going to use forced check style, which is a very simple core analysis tool.
- There are more sidekicks, there are more tools, they'll use slack for notification. We can also have an email integration, so we get email notifications.
- We'll use Nexxus, a sonar type to store our artifact and also to download dependancy form.sonar nexxus will be our software repository.
- We're going to get more deeper into your analysis, so we'll be using Sonarqube Server.
- And to set up these servers, jinking server, Nexus server, Sonarqube server, we are going to use  platform will use EC2 instances on AWS, two instances will set up jenkins server,Nexus server, Sonarqube server.

## Objective
GOALS
 - Fault Isolatıon
 - Short MTTR (Mean Time to Recovery)
 - Fast turn around on feature changes
 - Less Disruptive

## Continuous Integration Pipeline Architecture

![Solution](./Solution.png)

You'll have a very clear understanding what we are trying to achieve. Let's see the workflow:

- First, developer makes a code change, commit to one control system or source code manager and automation tool will automatically fetch that code, build it, run a unit test and return the outcome on slack channel. And so we'll be using slack anyways.

- The next, Phase will be it will codeanalysis and analysis, there will be  quality gates if the threshold if it is not passing the threshold gap, then it's good.

- If it's passing the threshold, then a notification will be sent on like channel.Then the software will be built, it will be packaged and the artifact will be uploaded and its outcome notification will be also sent.

- The artifact or the software will be stored in the artifact repository, if all these stages are successful, then the software can be promoted to the next level. If there is any failure, the notification will be any anyways sent.

- Once the notification is received by the developer for any failure they will make, the code will make the fix and the process repeats again.

- There will be regular code commits, continuous code commits, and this process will run continuously. that's why the need continuous continuous integration. This process will be automated, so this can be done multiple times in a day if you want.

## Flow of Execution 

1. Login to AWS account
2. Cereate login key
3. Create Security Groups for three server:
    - Jenkins
    - Nexus
    - Sonarqube
4. Create EC2 instances with userdata
    - Jenkins
    - Nexus
    - Sonarqube
5. Jenkins Post Installation
6. Nexus Repository Setup
    - Create 3 repos
7. Sonarqube post installation
8. Jenkins Steps
    - Build job
    - Setup Slack Notification
    - Checkstyle code analysis job
    - Setup Sonar integration
    - Sonar code analysis job
    - Artifact upload job
9. Connect all jobs together with Buildpipeline
10. Set automatic build trigger
11. Test with intellij, VScode etc.
12. Cleanup resources.

## Project Steps

1. Login to AWS console
2. Create keypair and security groups for server
3. Create userdata scripts for Jenkins, Nexus and Sonarqube Servers
4. Create EC2 instances;
a. Jenkins Server:
   - AMI- ubuntu 18.04
   - t2.small 
   - add to userdata "Jenkinsdata.sh" under userdata directory
   - select Jenkins-sg created for Jenkinsserver
b. Nexus Server:
   - AMI- Centos-7(AWS market place)
   - t2.medium (best performace, not select t2.micro)
   - add to userdata "Nexusdata.sh" under userdata directory
   - select Nexus-sg created for Nexusserver
c. Sonarqube Server:
   - AMI-ubuntu 18.04
   - t2.medium (best performace, not select t2.micro)
   - add to userdata "Sonarqube.sh" under userdata directory
   - select Sonarqube-sg created for Sonarqubeserver
5. Goto jenkins server and copy <Publicip>:8080 and paste your browser. Connect to Jenkins server with SSH
and "sudo cat <copy address on your jenkins webserver page>"
    - Create user and enter password. Login to Jenkins server
6. Go to Nexus server and copy <Publicip>:8081 and paste your browser. Connect ot Nexus server with SSH and
"sudo cat <copy address on your nexus webserver page>"
    - user: admin Password:copy from nexus server 
    - select "Enable anonymous access"
7. Create 3 repository on Nexus:
a. select maven2(hosted)
    - vprofile-release
    - click create repository
b. select maven2(proxy) [Dependencies, downloand this repository]
    - vpro-maven-central
    - Remote storage enter URL  https://repo1.maven.org/maven2/
    - click create repository
c. select maven2(hosted)
    - select "snapshot" version policy
    - 
d. select maven2(group)
    - vpro-maven-group
    - Member repositories add "vprofile-release, vpro-maven-central,vprofile-snapshot"
    - click create repository
8. Go to Jenkins Server create for first Job:
    - Click create a job
    - enter new ıtem name "Build" and click freestyle project and then OK
    - select Source Code Management, click Git and enter your repositroy URL https://github.com/gaskin23/CI-CD-Pipeline-Project-using-Jenkins-Nexus-Sonarqube-Slack.git
    - enter branch specifier "*/ci-jenkins" 
    - Add build section select "Invoke top-Maven targets":
        - Goals: install -DskipTests
        - Properties: add variables in settings.xml and POM.xml
            SNAP-REPO=vprofile-snapshot
            NEXUS-USER=admin
            NEXUS-PASS=Gakkos23*
            RELEASE-REPO=vprofile-release
            CENTRAL-REPO=vpro-maven-central
            NEXUS-GRP-REPO=vpro-maven-group
            NEXUSIP=172.31.95.81
            NEXUSPORT=8081
        - Settings file: Settingsfile in filesystem
        - file path: settings.xml
    - Then save job and click build now
9. Go to Nexus repository and select Browse and you will see dependencies download maven-central and maven-group.
10. Slack Integratıon:
    - Go to www.slack.com and If you don't have a slack account, first of all you must create an account from this website. 
    - After you login to account, you should create workspace named for example "visualpath" for ıntegratıon. 
    - Click create new channel and enter name "vprofile-jenkins" and go to www.api.slack.com website for create slackbot
    - Select Create app, enter name "Jenkins" and name your workspace for example visualpath
    - After createp app, go to settings and click OAuth & Permissions and click Bot Token Scopes, add an outh scope and select "chat:write"
    - click Install app to workspace and "allow" this message. 
    - Copy user bot access token and paste temporarily wihtin a text file
    - Go to slack vprofile-jenkins channel and write "@Jenkins" and ınvite the channel.
    - Then, go to Jenkins server select configure and click manage plugins then select "Slack Notification" plugin under available section. Click install without restart
    - Go to manage credentials:
        - select Global add credentials 
        - kind: secret text
        - copy slack bot token access to here
        - ID and description: slack-token
    - Go to configure system, find Slack configuration; enter workspace name "visualpath", channel name "vprofile-jenkins" and check Custom slack app bot user and save it.
    - Go to first job configuration:
        - Go post-build-actions
        - Select Slack notification
        - check Notify start, success, every failure, and unstable
        - add Workspace name, credential slack-token and channel/member id: #vprofile-jenkins
        - Click test slack connection and you will success
        - Post-build-actions, click Archive the artifacts and write "**/*.war"
    - Save first job configuration and build now. You can see slack notifications on your channel.
11. Create unit test case:
    - Create new ıtem "Test" named, freestyle project and copy from Build first job
    - Invoke-top-level Maven targets <Goals: test>
    - delete archive the artifacts
    - Save unit test job and build now
    - Go to Build job configuration (for trigger):
        - Select post-build actions and click build other projects
        - Projects to build: Test
        - Leave "Trigger only if build is stable" and save it
        - Refresh the page and you will see Test job under Downstream Projects
12. Create Integration Test Job:
    - enter Integration test, freestyle project and copy from Test job.
    - Goals: verify -DskipUnitTests and save it 
    - Go to Test job configuration click Integration Test under Post-build-actions and save it
    - Then refresh the page and you can see Integreation test job
    - Go to ıntegreation test job and build now it.
13. Create Code analysis job:
    - go to manage jenkins and install without restart  Next Generation Warnings plug-in (instead of checkstyle) and Violation plugins [Checkstyle plugin is deprecated]
    - click new ıtem enter name code-analysis select freestyle project
    - copy from Build job and go to Invoke top-level maven targets Build section 
        - Goals: checkstyle:checkstyle
        - Post build actions Publish Checkstyle analsis results and save job 
        - click the Build now and you can see checkstyleresult.xml under /workspace/target
        - Code analysis job click configure and change branch specifier */vp-rem and build now [This job is failure because this branch has not settings.xml so go to configure and delete settings.xml and selectk use default maven settings under Build section ] save it and Build job. You can see success this job
        - go to configure Post build actions add click Report Violations and checktyle part 10 100 100 XML filename pattern: target/checksytle-result.xml
        - save it and build now the job unstable; go to configure again change branch */ci-jenkins and add settings.xml file
        - save and build now you can see success this time.
        - go to ıntegration test configure then select Build other projects Code analsis under post build action section for trigger job and save it and refresh page you can see conde analysis job downstream project
14. Sonarqube Server configuration;
    - go to sonarqube server then login username:admin password: admin
    - first of all we will do ıntegratıon between jenkins and sonarqube so we have need token for this
    - go to security and enter token name sonar-token then click generate
    - copy this token and save somewhere
    - go to jenkins manage jenkins install sonarqube scanner and sonar quality gates
    - then go to global tool configuration:
        - find sonarqube scanner enter name: SONAR-4.4.2170
        - install from maven central version:latest and save it
    - go to configure system find sonarqube server:
        - check Enable injection of sonarqube server configuration as build environment variables
        - enter name sonar-vprofile
        - server URL: http://<Sonarqube server private ip>
        - add sonar-token on authentitacion select secret text then write sonar-token to secret path and go to quality gates-sonarqube:
            - enter name: sonar-vprofile
            - server URL: http://<Sonarqube server private ip>
            - add sonarqube account toke then save it 
    - go to new ıtem enter name SonarScanner-Code Analysis
    - copy from Build job then delete -DskipTests, archive the artifacts and trigger(build actions)
    - add build step execute sonarqube scanner:
        - copy sonar-analysis properties from under userdata/vprofile and paste analysis properties
    - add ınvoke maven level target 
        - Goals: checkstyle:checkstyle
    - save it and build now then you can see success, slack notification, vprofile-repo (bugs,code smells etc)
on sonarqube dashboard
    - go to Sonarscanner code analysis job configure change branch */vp-rem and remove settings.xml
    - save it and build now you can see bugs, code smells etc. numbers
    - go to Sonarqube server and create quality gates enter name vprofile-sonarqualitygates
        - add condition select quality gate fails when: Bugs value:50
        - go to vprofile-repo project settings > quality gate select your quality gates
    - go to sonarscanner-code analysis job configure  add post build action project key: vprofile status:failed
    - save it and build now and you will see failure this job
    - go to job configure change branch */ci-jenkins, sonar status: unstable save it and build now
    - go to code analysis configure and add build action trigger Sonarscanner analysis save it 

15. Nexus Repository ıntegration
    - go to manage jenkins manage plugins then install Nexus artifact uploader, copy artifact and Zentimestamp plugins
    - go to new ıtem enter name Deploy-to-Nexus then click freestyle and OK
    - add build steps select copy artifacts from another project:
        - Project name: Build
        - artifacts to copy: **/*.war
    - again add build steps select Nexus artifact uploader:
        - Nexus version: NEXUS3
        - Protocol: HTTP
        - Nexus URL: http://<Nexus server private ip:8081>
        - add nexus-token username with password enter nexus username: admin and your password
        - GroupID:QA
        - version:V$BUILD_ID
        - repo name: vprofile-release
        - click add artifacts:
            - ArtifactID: vprofile-$BUILD_TIMESTAMP
            - go to general section check Change date pattern for the BUILD_TIMESTAMP variable and enter date and time pattern: yy-MM-dd_HHmm
            - Type: war
            - file: target/vprofile-v2.war
        - go to post build actions select slack notifications:
            - check Notify build start, success, unstable, failure and back to normal
            - click advanced add workspace name, slack-token and channel name
        - save this job and build now you can see success and vprofile artifacts under Nexus Repository/vprofile-release
        - go to Sonarscanner code analysis configure:
            - add post build actions projects to build: Deploy to nexus for trigger 
            - Quality gates sonarqube plugin project key: vprofile Job status when analysis fails: UNSTABLE
16. Create beatiful view for ıntegrated jobs:
        - go to manage plugins install build pipeline plugin
        - go to dashboard create new view enter name: vprofile continuous integration and select Build Pipeline Views then OK
        - Upstream/downstream config: Select Build job for initial integration
        - Display options No of Displayed Builds: 5 and save 
17. Time to test this pipeline now.
        - Click run and you can see success jobs and slack notifications from your channel
        - After build pipeline finish with success you should see new artifact version on your nexus repo vprofile-release
        - go to first job Build configure then add build trigger Poll SCM Shcedule: * * * * * [this means every minute] and save it 
        - For test trigger, you can change jenkins-setup.sh under userdata directory then git push githu repo
        - İn a minute, you can see change codes git polling logs on jenkins server 
        - Look start pipeline from your build pipeline  view and slack notification because of trigger

## /////////////////// FİNAL OF PROJECT //////////////////////////// ##
        

 
    


        
       



        






