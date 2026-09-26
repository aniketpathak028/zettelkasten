---
title: '"Untitled"'
draft: true
tags:
date: 2026-09-19
description: '"Untitled"'
---
# stryker interview prep


### HR phone interview

1. Tell me about yourself.

Ans: I am currently doing my masters in Computer Science at the University of Freiburg with a specialization in AI. Before that I spent nearly 2 years working full time at Nokia as a Software Engineer, building and deploying microservices in Java and Python mostly. Working at Nokia, I had the opportunity to learn how scalable applications are built and deployed into production, as I was part of a team which developed a web based application that was used by telecom customers like Vodafone, SingTel, Verizon etc. However I had a desire to pursue higher studies, hence I came here to Germany to do my masters and currently I am starting my 3rd semester and I also work part-time as a research assistant at the university where I write simple bash and python scripts to automate manual tasks and help troubleshoot technical issues.

2. Why Stryker?

Ans: As I understand Stryker builds medical technologies that directly effects millions of patient worldwide and I would love to be a part of such an impact even if I could make a small contribution that would mean a lot to me. Also I have learned that the RnD team at Stryker work on AI and Automation and since I have a solid foundation in building and shipping software and currently my masters is focussed towards AI, I would love to learn more on how AI and automation could be used in the industry as that would be my natural career trajectory in the future.  

3. Why this internship and why cloud and software engineering?

Cloud and automation are where my strongest experience is, from Nokia and my research assistant job. This role adds AI agents and prototyping, which are exactly what I'm studying and want to apply in practice. I want to see how these things work in a real R&D team, not just in coursework

4. What do you know about Stryker?

Stryker is a global medical technology leader. Its products spans all across healthcare domains and I read that it impacts over 150 million patients a year. I also love that you guys value inclusion and believe that people from different backgrounds can contribute equally towards the growth of the mission! That is something that stood out to me 

5. What interests you about healthcare software?

It is interesting to witness how softwares are built, designed and tested for healthcare, as they need to be really secure for the end customers and even the job description mentions about devsecops so I would be really curious to learn how we develop such security critical apps

6.  Why Freiburg and are you comfortable on-site?

I am already based in Freiburg for my studies so location works well and I am comfortable working onsite with the team  

7.  Why now and what do you hope to learn?

I am currently at a point in my masters that I would be done with more than half of my degree by the end of this semester and I was really seeking out for some industry experience alongside it, as I want to learn how experienced engineering teams in industries are currently using AI to develop large scale applications. Also if I have this opportunity, it would be my first corporate experience in Germany, so I am excited to learn more about that too :)

8. Walk me through your resume

- I have done my bachelors in India in computer science and engineering and then I worked for almost 2 years at Nokia
- First I was an intern and later I was converted for a full time position
- I worked extensively on microservices development and deployment using CICD on cloud platforms like GCP and Azure
- Currently I am doing my masters degree in Comp Sci with a specialization in AI
- I also work as a research assistant in the Uni where i mostly automate manual tasks like server maintenance and backups

9.  What was your role at Nokia?

- When I joined as an intern I was mostly responsible to develop features for our applications using tech like java spring boot, and python fast api
- later when i was converted into a full time position I also started contributing in building CICD pipelines for continuous integration and deployment using Gitlab and Azure DevOps
- We were building a product to support telecom clients manage their networking devices using a web application

10. give an example of the contribution to the 20+ production bugs you mentioned!

- I had resolved several production bugs, one of the bugs that I remember is a specific microservice deployment was always getting delayed when we tried to deploy it even though nothing was wrong in the pipeline
- when i debugged the various stages in the pipeline, I found that the docker image was around 3x larger than the usual even though the application build was only about 300mb
- later upon further debugging I found that the there was a missing .dockerignore file due to which some of the un-necessary files were also getting packaged into the image, once we created the .dockerignore file the deployment was much faster

11. what does your RA job involve day to day?

- In my RA job I mostly work on tasks like automation of backups in servers using python scripts, regularly upgrading the virtual machine images for the PC pools etc

12. Go project and Azure CICD project

- Go Project - it is a simple implementation of a forward proxy which is nothing but an intermediate web server that sits between the client and the internet which intersects every browser request sent to the internet, in the process of this intersection we store the connection request, its metadata and also the content received in local cache so that when an user re-sends the same request we simply load the stored content instead of making a new request which reduces our response time

- Azure [CICD](https://zet.aniketpathak.me/0-Index/learning-CICD-with-Azure-DevOps) project - it is a simple project where I deployed a simple voting app (containing microservices written using python, .NET and nodejs) into AKS - Azure K8s cluster using Azure DevOps following the principles of CICD and devsecops

8. Which of your skills are strongest and what are you still building?

















## Links:

202609191618
