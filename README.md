
# Continuous-Integration-Tooling-Website

# Apache-LB


## DevOps Automation

Automation is the use of technology to perform tasks with reduced human assistance. Automation helps us accelerate processes and scale environments, as well as build continuous integration, continuous delivery, and continuous deployment (CI/CD) workflows. There are many kinds of automation, including IT automation, business automation, robotic process automation, industrial automation, artificial intelligence, machine learning, and deep learning.

Theoretically speaking, We could perform DevOps processes like Continuous Integration, Continuous Delivery and log analytics manually. But doing so would require a 
large team, a lot of time and a level of communication and coordination between team members that is just not realistic in most situations.

Automation makes it possible to perform these processes using software tools and preset configurations.


## Benefits of Automation in DevOps


We have seen earlier releases, in the absence of automation taking years to get into the production and also recently with agile, be it lean, scrum or safe, and with a percentage of automation being improved, release timelines are brought down to few months or weeks.But automation is absolutely a must in order to make the releases as fast as possible in a few hours. So, I think it is impossible to make such quick and frequent releases unless we put in automation in place throughout the pipeline.

So, quite obviously then, if we want to achieve the objectives of DevOps, high quality and value delivered to customers via frequent and fast deliveries, Automate everything is a must. Clearly, we know by now that automation removes manual errors, dependency on an individual, performs faster, and achieves accuracy thereby achieving consistency and reliability. Hence, automating everything enables the devops objective of high-quality delivery, enables frequent releases and faster
releases.



## In a nutshell, Automation,

- Removes manual errors
- Team members are empowered
- Dependency removed
- Latency removed
- Increases no of deliveries
- Reduces the lead time
- Increases frequency of releases
- Provides faster feedback
- Enables speed, reliability, and consistency.



![image](https://user-images.githubusercontent.com/85270361/168469493-6d91c256-226e-4e20-911a-38f04238752d.png)


## Acording to Circle CI, Continuous integration (CI) is a software development strategy that increases the speed of development while ensuring the quality of the 
code that teams deploy. Developers continually commit code in small increments (at least daily, or even several times a day), which is then automatically built 
and tested before it is merged with the shared repository.



# In this project, We are required to implement CI for Tooling Website using Jenkins.


Below is the updated architecture of our infrastructure. Jenkins will be used for continous integration, and its data will be stored on a remote NFS server.



![image](https://user-images.githubusercontent.com/85270361/168469571-4918b224-1933-46f0-9c13-9f7f0d89379b.png)



# Steps - Prepare the Jenkins server

Install Java, because Jenkins need Java to run

```
sudo apt install openjdk-11-jdk -y
```

##  Add Jenkins repository

Follow the steps below to add the Jenkins repository to your Ubuntu system.

1. Start by importing the GPG key. The GPG key verifies package integrity but there is no output. Run:

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc &gt; /dev/null
```

![repo key](https://user-images.githubusercontent.com/117458922/227246955-eb8e5ab9-94fa-4e05-a150-e96edb736858.png)


2. Add the Jenkins software repository to the source list and provide the authentication key:

```
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list &gt; /dev/null
```

![repo](https://user-images.githubusercontent.com/117458922/227247044-d33dc78b-2094-423f-910d-8fb76e99440a.png)


The command adds the Long Term Support (LTS) stable release to the sources list, but there is no output.

##  Install Jenkins

1. Update the system repository one more time. Updating refreshes the cache and makes the system aware of the new Jenkins repository.

```
sudo apt update
```

2. Install Jenkins by running:

```
sudo apt install jenkins -y
```

3. To check if Jenkins is installed and running, run the following command:

```
sudo systemctl status jenkins
```

![jenkins run](https://user-images.githubusercontent.com/117458922/227247459-b2406ad1-5dd8-4187-816f-3e013f7f9c56.png)

If Jenkins is not active, start Jenkins with the command below;

```
sudo systemctl start jenkins

sudo systemctl enable jenkins
```

## Set up Jenkins

Follow the steps below to set up Jenkins and start using it:

1. Open a web browser, and navigate to your server' IP address. Use the following syntax:

http://ip_address_or_domain:8080

*Use the actual IP address or domain name for the server you're using Jenkins on.*

![Jenkins login](https://user-images.githubusercontent.com/117458922/227250840-154b5d94-3953-4f9b-8141-5b66effe57a5.png)

2. Run the command below to get the password that is being prompted

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

![customize](https://user-images.githubusercontent.com/117458922/227251268-ddbadf3f-2467-4e55-975c-8b40fe2873f6.png)

![j](https://user-images.githubusercontent.com/117458922/227251364-c89e47dc-fb63-4036-b98a-74cae2617706.png)

![Screen Shot 2023-03-22 at 12 48 38 PM](https://user-images.githubusercontent.com/117458922/227251417-b46e02a6-7cc2-401d-8bad-e9091f3ef323.png)

![Screen Shot 2023-03-22 at 12 48 53 PM](https://user-images.githubusercontent.com/117458922/227251473-9028ab0e-c4bc-49e5-8d96-4a6c9b25b815.png)

![Screen Shot 2023-03-22 at 12 49 13 PM](https://user-images.githubusercontent.com/117458922/227251536-1ea6bac2-dfde-4e38-9c7f-376412380d32.png)


3. Create a Freestyle Project In Jenkins by navigating through New Item

![Frestyle project](https://user-images.githubusercontent.com/117458922/227919547-a0b77144-67b7-4c46-bb92-239d9b9113aa.png)

4. Set up WebHook on Git and also add the source code URL and setup triggers for the Jenkins project settings

![webhook](https://user-images.githubusercontent.com/117458922/227941681-cf58d7a7-c336-4c00-aa6f-e81b5569d381.png)

![Build Triggers](https://user-images.githubusercontent.com/117458922/227940370-0c3fdd7d-fecb-4d00-b1a3-a04ae9051512.png)

![Triggers](https://user-images.githubusercontent.com/117458922/227940600-b15e214c-2b6b-4187-9a85-081817c68e42.png)

5. Simulate A Change in the project on Git, like for example, modify the README.md file. The trigger will create a build as seen below;

![CHange](https://user-images.githubusercontent.com/117458922/227941429-e803daa9-49b1-427c-932f-66cf9e6d221c.png)

![build](https://user-images.githubusercontent.com/117458922/227941479-8b17b11b-5b32-4fb0-9d69-ea0209a52d42.png)

![Console out](https://user-images.githubusercontent.com/117458922/227941561-3a356b16-6139-4c40-b470-ab76f8728ef3.png)

