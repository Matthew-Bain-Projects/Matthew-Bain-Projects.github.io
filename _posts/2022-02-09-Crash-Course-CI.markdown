---
layout: post
title:  "Crash Course: CI/CD"
date:   2022-02-09 00:00:01 -0500
categories: jekyll update
---

## What is this? 
Crash Course is going to be the uninspired name of a learning series that I plan on undertaking. Each week (roughly), I'll explore some new thing related to the tech industry, write about it, and have something to show for it. This week's crash course will be setting up a CI/CD pipeline for my future projects.

## What is CI/CD?
CI/CD stands for continuous integration and continuous deployment. It is a useful strategy for software developers who want to automatically get feedback on the quality of the changes they've made to their application. Continuous Integration is the practice of integrating your code changes reliably many times per day. Continuous deployment is the automatic process of getting their application into production. 

## Have I ever done this?
No, I haven't. In college, we had to set up one for a group project, but I was uninvolved. Now, as the primary voice behind modernizing our software workflow at my day job, I want to understand the process of setting this up myself. If I don't, I won't be able to help my team accomplish this same feat. 

## The Process
To begin, I think I want to learn an "easier" CD pipeline. I am aware that it might be better to learn about a platform agnostic pipeline solution that can be run on our own servers, but that is probably out of the scope of this series. I mainly want to understand the goals of a pipeline solution and how it should work, not spend hours setting up a Jenkins server and connecting that to my github. (If it doesn't take hours, oops. I guess I'll learn about that some other time.) Instead, I am going to look at [github actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions). 

So the first question that I need to ask myself is: what project am I going to set this up for? I don't actually have many projects that can be built very effectively at the moment (although I am working on it) so I think I will make a new one with a trivial purpose: repeat whatever string of text is passed in. Let's go set that up. Once I am done, I will embed a link to that repository [here](https://github.com/Matthew-Bain-Projects/CrashCourse_ContinuousDelivery). 

So now that I have a super basic app that does only one thing, how does this work? I went to the github actions tab in my repository, found a basic "make" plugin, and slapped that bad boy in there. Given how simple of a repo this is, should work out of the box, right? Of course not! The configuration failed to build. I think it is a pathing issue.

My first attempt at fixing the pathing issue failed due to misunderstanding the yml syntax for github actions. Let's see if we can fix that. 

So.... it seems like since I am using qmake to generate my makefile, it is adding a lot of unneccessary bloat to the makefile and the build is failing due to the github server not having the right dependencies. Next week I will teach myself CMAKE. Now, I am going to replace the qmake makefile with something easier - no makefile at all. I'll just call the compiler directly, since we have no dependencies and the code is three lines long. This isn't a crash course on makefiles (which I do understand better than this seems, I just really don't want to write my own at the moment), it's a crash course on CD. 

Right now, I just want the code to compile in the pipeline. I changed the build steps to be "cd into the directory, and call g++". This, actually, didn't work. I had been operating under the assumption that the pipeline operated in a singular shell, but I don't think that is the case anymore. I changed it to read "g++ CrashCourse_RepeatText/main.cpp", just to see if that would work. AND IT DID! This is exciting, and also gives me this lesson learned: **sometimes, you will need to structure your application in a smart way to allow the computer to work for you**. Of course we as computer engineers know that, but it was good to be reminded in this way. It'll be useful when bringing this solution into the enterprise. 

Next, I want to see if we can run the application and supply a command. 
So, we can definitely run the application, and I think that is where I will leave it for now. The continuous integration pipeline will allow us to call testing code harnesses that we have built or used, but it won't let us provide input to the system itself. Still, this was a great way to spend an hour, and I've grown because of it. 
