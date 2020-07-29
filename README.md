# Automated WebServer Configuration (Git-Jenkins-Docker)

## Task:

1. A developer writes a code and pushes to Master branch. This branch will be managed by Jenkins as it will fetch the code to a local folder and then it would be deployed on a Docker environment.

2. Now, some other developer writes more code and he adds it to another Branch. Jenkins will keep an eye on this branch also and it will deploy the code on another docker environment. 

* As soon as the code is uploaded or pushed on GitHub, Jenkins will deploy the code on the respective Docker environment where "httpd" server is running.

3. If the website is running properly on the different branch then Jenkins will merge it with the Master branch on it's own!

## Pre-requisite:

* OS: Base OS can be any OS but in my case it is Windows 10 and I've used my server OS to be RHEL8 on Virtual Box.

* In RHEL8, I've installed Docker where I've pulled "httpd" image, and Jenkins too.

* In Windows, we need Git Bash software.

## Performing the task!

**Step 1:** Giving Jenkins all the power of Linux:

To do so, we've to edit the ```sudoers``` file by using ```gedit /etc/sudoers``` in RHEL8 terminal. And add this line just below the line ```## Allow root to run any commands anywhere``` with the root configuration.

```jenkins     ALL=(ALL)     NOPASSWD:ALL```

**Step 2:** GitHub and Git configuration:

First, we need to create a GitHub repository without initialising the README.md file.

![This is how it'll look after doing so](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Step1.png)

After this, we need to run some commands on our Git Bash where we'll write a code and then will push it to the master branch.

![Local git repo](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Step2.png)

It is always a good practice to cross check.

![Cross checking on GitHub](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Step3.png)

Next, we create another branch. We'll use this branch to edit anything we want instead of the main branch or say, direclty on our website.

![Developer branch](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Step4.png)

Good practice to cross check!

![Cross checking on GitHub](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Step5.png)

* I kind of made a mistake by overwriting the code. 

**Step 3:** Configuring Jenkins:

1. **Job1:** This Job will keep an eye on the master branch and as soon as some changes are made in the Master Branch file then this job will get triggered which will later copy the code in RHEL and then will deploy on Docker environment.

![Job1_1](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job1_1.png)

![Job1_2](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job1_2.png)

![Job1_3](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job1_3.png)

![Job1_4](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job1_4.png)

2. **Job2:** This Job will keep an eye on the developer branch and whenever a ```git commit``` command is run, then it'll copy the code to a directory in RHEL.

![Job2_1](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job2_1.png)

![Job2_2](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job2_2.png)

![Job2_3](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job2_3.png)

![Job2_4](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job2_4.png)

3. **Job3:** This Job will get triggered as soon as the Job2 build is successful and then it'll deploy the developer branch code on a different docker environment.

![Job3_1](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job3_1.png)

![Job3_2](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job3_2.png)

![Job3_3](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job3_3.png)

![Job3_4](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job3_4.png)

4. **Job4:** This Job will merge the Developer branch to the Master branch if the code is running properly or say, if the website is well and good to go!

![Job4_1](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job4_1.png)

![Job4_2](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job4_2.png)

![Job4_3](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job4_3.png)

![Job4_4](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Job4_4.png)

**Step 4:** WebHooks:

We've to configure ```post-commit``` webhook so that, whenever we commit our code then it will automatically push the code to GitHub and it'll also trigger the Job2 in Jenkins.

![WebHook](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/web_hook.jpg)

## Testing time!

* Observing both of our servers initially after our Job 1, 2 and 3 have been build.

![Main Website](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Production_start.png)

![Edited Website](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Developer_start.png)

* Making some changes in our code. As soon as we commit our code, then it'll automatically trigger the Job2 and we'll see some changes made to our Developer branch website.

![Make changes](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Making_changes.png)

* If our website is running well and good, then it'll merge the developer branch with master branch and then finally our small setup is successful!

![Merged Website](https://github.com/rohankumawat/MLops_DevOpsAL_Task1/blob/master/MLopsTask1/Last!.png)

## Achievement:

If we look closely, we can see that this is how we work in real life and this is how automated work looks like!
We just have to configure Jenkins once and it'll do rest of the job on it's own! 

In future, we can integrate all of these things using **Cloud services** also.
