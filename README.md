# Introduction

## Goal

Build a **on-line sharing doc** website such that SUSTech users can access and edit the same file. 

## Requirements

Basic requirements: 

1. The website should allow multiple formats, e.g., latex editing (should be able to automatically compile), plain text editing. 
2. For simplicity, you can allow that when one user is editing, other users can only read.
3. You should also include at least certain fundamental management options, e.g., deleting files, cloning files.

Bonus requirements:

1. You would get a big bonus if you can make it a thorough on-line sharing doc, i.e., multiple users can edit the files at the same time.
2. You would get a big bonus if you can realize the automatic dependency building of libraries (especially for latex edit-ting).

# How to start

1. Labor recommendation

   •Database designer

   •Front-end designer

   •Back-end designer

   •Or other roles determined by you:

   ​	"stupid" user

   ​	project manager

   ​	etc.

2. Find related work

   •Overleaf

   •Tencent Doc

   •Or other open-source solution

## Q & A

Q1: How much workload do we expect to spend on this project?

A: Based on previous experience, about 30 man-day is needed to finish basic part. If you want to get bonus, you may need extra work time.

Q2: What should we do before mid-term check?

A: We will check your progress referring to initial proposal in mid-term check to ensure that you are able to finish the work in the end of this semester. If you are too slow in progress, we will suggest you to reduce some requirements although it may influence your final grades.

Q3: How to solve the conflict of on-line doc when several people modify the same position?

A: You may need additional knowledge of file system which you will learn in Operating System class in next semester. Besides, you can refer to open-source demo to find a feasible solution. Feel free to discuss the design if you want.

# Demo

### Overleaf

You can refer to  www.overleaf.com as your guidance (actually it is our oracle; feel free to reproduce any of its features; note that it might be hard to access these days due to...; that is also the reason why we want to build another one for us).

There is a community version Overleaf deployed on http://10.20.83.122:8099, you can access it through the LAN if you cannot access www.overleaf.com. And we provide a test account:{email: test@gmail.com, passwd: lab604}.

!!!Attention: Overleaf has some open-source versions on Github(https://github.com/overleaf/overleaf), you can read the code for realizing the details of how to implement certain feature but **Don't simply Copy & Paste the code**. 

### Tecent Doc

You can refer to https://docs.qq.com/ as your guidance to implement on-line sharing features(although it has some known bugs of synchronization, it can work correctly for most of time).

# Reference

Slides of Lecture 1-Overview