---

layout: post

title: Automated jenkins builds for a Node.js application on Github Pull Request

category: DevOps

comments: true

description: 

tags:

    - Jenkins

    - Github

    - Pull Request

    - DevOps
    - Node.js
    - CI/CD
   
    
   

---
<img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68398252_450290222479996_8804154740247101440_n.png?_nc_cat=102&_nc_ohc=s5IooMx5Hk8AX8gm2KX&_nc_ht=scontent.ftun12-1.fna&oh=e9c3be0768761847bc9231a496e56d71&oe=5EA91543" align="center" height="400" width="800" max-width="100%">
# Intoduction
In this tutorial we will look forward how to how to trigger Jenkins build on new Pull Requests for a simple **Node.js** application based on pull request Github event. <br>
Before jumping into  details about this tuorial let's give a hit about some basics that we should know first of all:
- **Github Flow**
- **Jenkins**
<br> <br>

## Github Flow
<br>
<img src="https://cdn-images-1.medium.com/max/1600/1*iHPPa72N11sBI_JSDEGxEA.png" max-width="100%" align="center" height="300" width="800">
**GitHub flow** is a lightweight, branch-based workflow that supports teams and projects where deployments are made regularly. I will try to explain it in a very simple way step by step : 

 **1. Create your feature _Branch_ :** <br>
 When you're working on a **project**, you're going to have a bunch of different features or ideas in progress at any given time. Branching exists to help you manage this workflow and that's why you should create a specific branch for every feature you are working on! <br>
 **2. Commit your  _changes_ :** <br> 
 Whenever you add, edit, or delete a file, you're making a commit, and adding them to your branch <br>
 **3. Create  your  _Pull Request_ :** <br>
 Now it's time to push your commit and ask for a review by creating a Pull Request. <br> 
 **4. Discuss and review your _code_ :** <br>
 In this step once your pull request has been opened , you may receive comments and questions by team members , and at this point you should fix what should be fixed and push again ! <br> 
 **5.  _Merge_ :** <br>
 Now that your changes are approved, it is time to merge your code into the master branch. <br> 


## Jenkins
<br> 
<img src="https://agilealliance.org/wp-content/uploads/2015/05/Jenkins-You-Can-Take-th-Evening-Off.png" align="center" height="200" width="200" max-width="100%">

**Jenkins** is an open source automation server which enables developers around the world to reliably build, test, and deploy their software. Back to the **Github Flow** section exacty in the 4th step **Discuss and review your code** basicly as I mentioned this review would be done by a member of the team manually.. and here where **Jenkins** intervenes and will do all the job in an automatic way ! 

# What we will need ?

In this demo such tools are required : 
* Github repo on which we will make our tests 
* Jenkins : we will go through its setup and configuration
* ngrok


# Demo
<br>
## **1 - Install jenkins and configure Github pull request plugin**
<br>
Since we will need  **Jenkins** you have to install it. You can check here and follow steps based on your OS [Go Here..](https://jenkins.io/doc/book/installing/){:target="_blank"}. <br> 
Once you finished with the setup by adding your user credentials you should then be redirected to  **Jenkins** dashboard as it's shown in this picture ! <br> 
<img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68717074_491666024928404_3176498232335269888_n.png?_nc_cat=110&_nc_ohc=y8X6zxcvnJkAX_vdIzd&_nc_ht=scontent.ftun12-1.fna&oh=d54268954ddeaf5c5c377a94f6467710&oe=5EDACF5D" align="center" height="500" width="800" max-width="100%">
###### Still more
Now you have to configure  Github pull request plugin to receive Github webhook and launch job in **Jenkins** as it shows the picture bellow : <br> 
<img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68983190_2411999232253238_6915267499726471168_n.png?_nc_cat=109&_nc_ohc=zow5vAiX2OgAX9KqjuP&_nc_ht=scontent.ftun12-1.fna&oh=0eb95a9ec1313066e825c633671ba5e5&oe=5E9A022A" align="center" height="500" width="800" max-width="100%"> <br> 

Now you have to set up Jenkins server to authenticate GitHub : <br> 

 * Go to **Manage Jenkins** > **Configure System**
 * Under **GitHub Pull Request Builder**, fill in authentication info for your GitHub repo.
 * GitHub Server API URL: https://api.github.com
 * Credentials: Click Add
  <br>
  <img src="https://miro.medium.com/max/700/1*Hzphwbxm2_pOCG-_dN2LiA.png" max-width="100%" align="center" height="400" width="500"> <br> 
  Dont Forget to add your **shared token** too. <br>
  If you see **Connected to https://api.github.com as your Github Name** means that everything is ok at this stage ! 
    <br>
  <img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/69013735_471393520359554_2590638386486181888_n.png?_nc_cat=108&_nc_ohc=GmqxtHb19ewAX9ZtvMr&_nc_ht=scontent.ftun12-1.fna&oh=dab5b3493bf512c98cd54e8532ef3a27&oe=5ED9ACBB" align="center" height="200" width="600" max-width="100%"> <br> 



## **2 - Create Github repository**
<br>
For this example we will need 4 files in this repo : 
- **app.js**
- **package.json**
- **Jenkinsfile**
- **app.test.js** <br> <br>

**package.json**: 
<br> 
<script src="https://gist.github.com/majdas007/81de6a84011eda1195a09b15dc48d6f6.js"></script>

**app.test.js** : 
<script src="https://gist.github.com/majdas007/96d288689d4bb4d990114a4cf3c1e345.js"></script>
**app.js** : 
<br> <br> 
<script src="https://gist.github.com/majdas007/1ac933879fc13a18dd20c0a74b88445a.js"></script>
**Jenkinsfile** :
<br> <br> 
<script src="https://gist.github.com/majdas007/0726dc3c4443ef73c521513e78cc311d.js"></script>
Your repo should look finally like this : 

  <img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68381057_2591726864204638_4896165560984797184_n.png?_nc_cat=103&_nc_ohc=IrDm036ezHcAX9tHZSG&_nc_ht=scontent.ftun12-1.fna&oh=c85a683c438e24ee3eb8ae39e6a97c10&oe=5EA51DF5" align="center" height="200" width="800" max-width="100%"> <br> 
  if you want to practice this process, here is the github [repo..](https://github.com/majdas007/Blog-Post){:target="_blank"}

## **3 - Configure your pipeline job in Jenkins**
<br>
- Go to Jenkins and create new item with pipeline type
- Add your GitHub project URL
- In Build Triggers check **GitHub Pull Request Builder** and add your Github username in Admin list
- Check **GitHub hook trigger for GITScm polling**
- In Pipeline section Select **'Pipeline script From SCM'** and Chose Git as SCM
- Add your Repository URL and your credentials Credentials
- Full the Refspec input with **'+refs/pull/:refs/remotes/origin/pr/'**
- Add **'${ghprbActualCommit}'** in the Branch Specifier
- Save your job !

## **4 - Use Ngrok to create tunnel to your localhost**
<br>
After installing Ngrok run this command :
```
 ./ngrok http http://localhost:8080 
```
You should have something like this : 
  <img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68463032_369913727008149_2843933687630790656_n.png?_nc_cat=102&_nc_ohc=g27OCp8KJUIAX9huCN-&_nc_ht=scontent.ftun12-1.fna&oh=fae80e400b00697656d01f9e6e04b142&oe=5E95F13B" align="center" height="200" width="500" max-width="100%"> <br> 

## **5 - Setup webhook on Github** 
<br>
Now we are almost done you need only to setup webhook on your Github repo :

- Go to your Github repo
- Go to settings
- Select webhooks and click add webhook
- In the Payload URL type the ngrok provided by ngrok and add to it **'/ghprbhook/'** 
  <br>Your final URL should look like this  **http://'subdomain'.ngrok.io/ghprbhook/**
- Set content type to **Json**
- Select your individual event and set it to **Pull requests**.
- Save your webhook
<br> <br>
  <img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68258877_2326887867624257_3275122677295087616_n.png?_nc_cat=101&_nc_ohc=GVGN5O_rhZ0AX-ADYWL&_nc_ht=scontent.ftun12-1.fna&oh=4b8da2e37b6fccdc885187e86c34ae28&oe=5ED7C461" align="center" height="600" width="800" max-width="100%"> <br> 

## **6 - Test** 
<br> 
- Create new branch
- Make some changes to **readme.md**
- Commit your changes 
- Create new **Pull Request** 
- You can see that jenkins has automatically detected you pull request
  <br> 
    <img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68534008_1329398627221300_5622805956531322880_n.png?_nc_cat=111&_nc_ohc=mtW3o9XSGp0AX8lWqPJ&_nc_ht=scontent.ftun12-1.fna&oh=45c484bf254a4202a969b1ada2e059f2&oe=5EA7304D" align="center" height="400" width="800" max-width="100%"> <br> 

- On the console output you can check if the Build has been successfully done : 
    <br> 
    <img src="https://scontent.ftun12-1.fna.fbcdn.net/v/t1.15752-9/68625065_741399109634016_8171058607853404160_n.png?_nc_cat=106&_nc_ohc=59snhiuYuswAX8ZTCc3&_nc_ht=scontent.ftun12-1.fna&oh=eb8b75ded59b8130a74c1bdb422c7e2f&oe=5E956DCE" align="center" height="300" width="600" max-width="100%"> <br> 