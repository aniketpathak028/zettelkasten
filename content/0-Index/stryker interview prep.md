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

Ans: I am currently doing my masters in Computer Science at the University of Freiburg with a specialization in AI. Before that I spent nearly 2 years working full time at Nokia as a Software Engineer, building and deploying microservices in Java and Python mostly. Working at Nokia, I had the opportunity to learn how scalable applications are built and deployed into production, as I was part of a team which developed a web based application that was used by telecom customers like Vodafone, SingTel, Verizon, T-Mobile, AT&T etc. However I had a desire to pursue higher studies, hence I came here to Germany to do my masters and currently I am starting my 3rd semester and I also work part-time as a research assistant at the university where I write simple bash and python scripts to automate manual tasks and help troubleshoot technical issues. Apart from tech i really like to travel and experience new places and cultures

Nokia skils - GitLab CI, Jenkins CICD, Azure, GCP, Java spring boot microservices, Python FastAPI microservices

2. Why Stryker?

Ans: As I understand Stryker builds medical technologies that directly effects millions of patient worldwide and I would love to be a part of such an impact even if I could make a small contribution that would mean a lot to me. Also I have learned that the RnD team at Stryker work on AI and Automation and since I have a solid foundation in building and shipping software and currently my masters is focussed towards AI, I would love to learn more on how AI and automation could be used in the industry as that would be my natural career trajectory in the future.  

3. Why this internship and why cloud and software engineering?

Cloud and automation are where my strongest experience is, from Nokia and my research assistant job. This role adds AI agents and prototyping, which are exactly what I'm studying and want to apply in practice. I want to see how these things work in a real R&D team, not just in coursework

4. What do you know about Stryker?

Stryker is a global medical technology leader. It builds software solutions that spans all across healthcare domains and I read on the website that it impacts over 150 million patients a year. I also love that you guys value inclusion and believe that people from different backgrounds can contribute equally towards the growth of the mission! That is something that stood out to me 

mission - work collaboratively, improve patient outcomes
core values - integrity, accountability, people and performance

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

- Go Project - it is a simple implementation of a forward proxy which is nothing but an intermediate web server that sits between the client and the internet which intersects every browser request sent to the internet, in the process of this intersection we store the connection request, its metadata and also the content received in local cache so that when an user re-sends the same request we simply load the stored content instead of making a new request which reduces our response time. The hardest part in the project was to parse an https request

- Azure [CICD](https://zet.aniketpathak.me/0-Index/learning-CICD-with-Azure-DevOps) project - it is a simple project where I deployed a simple voting app (containing microservices written using python, .NET and nodejs) into AKS - Azure K8s cluster using Azure DevOps following the principles of CICD and devsecops. I think the hardest part in the project was the 

13. Which of your skills are strongest and what are you still building?

- I believe I have a strong foundation in building and deploying microservices, building CICD pipelines (keeping security in mind)
- Currently I am building more towards AI agents and automations, learning more on tech like langchain, lang-graph, RAG, n8n etc.

8. What are your strengths and weakness?

- Strength - communication skills, ability to learn something quickly
- Weaknesses - usually unable to say no to someone easily

Questions to ask them:
- what sort of project might I start on? and what does the video interview stage cover?
- 


Hi! I'm Aniket, currently in my 3rd semester pursuing my Master's in Computer Science with a specialization in AI at the University of Freiburg

Prior to my Master's, I spent two years as a Software Engineer at Nokia, where I built cloud-native backend microservices in Java Spring Boot and Python for global platforms serving clients like Vodafone and Verizon. Alongside backend development, I focused heavily on DevOps automating CI/CD deployment pipelines using GitLab and Azure DevOps, and provisioning infrastructure with Terraform and Kubernetes. At Freiburg, I also work part-time as a Research Assistant writing Python and Bash automation tools for workflow efficiency.

What really drew me to the Cloud Applications & Software Engineering internship at Stryker in Freiburg is the team's focus on cloud platforms, developer tooling, and AI integration. I'm excited about the opportunity to apply my background in microservices, CI/CD pipelines, and AI to build reliable R&D tools that advance healthcare software


STAR based answers:

At Nokia, our platform managed network devices like nodes and ports for global telecom clients. The application was built on Java Spring Boot microservices containerized with Docker, pushed to Azure Container Registry via GitLab CI, and automatically deployed to Azure Kubernetes Service using ArgoCD for GitOps.

During a modernization project to upgrade a core microservice from legacy Java 5 to Java 17, I tackled a port search feature that was suffering from high latency (1 to 2 seconds per query).

While inspecting the codebase, I discovered an anti-pattern: instead of executing indexed database queries, the legacy service was fetching entire dataset tables into application memory and filtering them in Java. I refactored the data access layer to delegate filtering directly to optimized database queries and utilized modern Java 17 streaming features, which brought search latency down to under a second (0.6s / 0.6ms)—significantly reducing API response times on high-traffic endpoints.


We tried to include sec checks directly into the CI pipeline instead of tackling it at the end, 

- IAC with Terraform - I structured the HCL scripts to provision AKS clusters, networking, and container registries. We always tored state files in remote backends with state locking to prevent concurrent modification conflicts, using separate environment cofiguration for development and production
- Git - precommit hooks, gitleaks
- Secure Container - non root user, .dockerignore, multistage builds, distroless image
- Secrets and SAST scanning - Before building container images, automated static code analysis was done using SonarQube to detect coding malpractices, or code smells that could lead to vulnerabilities - sql injection, hardcoded secrets, insecure ssl/tsl
- SCA - software composition analysis that scans dependencies and matches versions against known CVEs ex- Trivy
- DAST - dynamic application security testing we used OWASP-ZAP


elk stack




## Links:

202609191618
