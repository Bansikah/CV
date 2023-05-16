---
title: "Email Slicer with Python"
seoDescription: "Python email Slicer"
datePublished: Thu May 11 2023 10:33:28 GMT+0000 (Coordinated Universal Time)
cuid: clhizrjw6000n0aju7nzphtq1
slug: email-slicer-with-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683801085358/0e868f22-43eb-47db-bf10-563af918b585.png
tags: python, beginners

---

An email slicer is very useful program for separating username and domain name of an email address. In this article, I will explain how to write a program to create an Email Slicer with Python

## Email Slicer with Python

To create an email slicer with Python, our task is to write a program that can retrieve the username and the domain name of the email. For example, the email below which shows the domain and username of anthonyjohnson@gmail.com. So we need to divide the email into two strings using '@' as the separator. Let's see how to seperete the email and domain name with Python:

<iframe src="https://www.thiscodeworks.com/embed/645cbb5568f8da00131b4be7" style="width:100%;height:151px"></iframe>

## Results:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683799894887/773c04e2-3eed-4d2c-b223-ed2a933fafdb.png align="center")

The code above is very simple and easy to understand. We take user input and use the strip function at the same time to remove white space if any. Then we are finding the index of '@' symbol of the user input. Then we store the index into a variable known as domain\_name to split the email into two parts; the user name and domain.

So that's all about our project thank you.