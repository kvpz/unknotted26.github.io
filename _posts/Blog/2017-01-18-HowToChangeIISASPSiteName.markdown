---
permalink: /Blog/IISandChangingASPsiteName
title: "How to Change a Site's name on IIS"
categories: Blog
type: post
---

As I was refactoring one of my projects in an attempt to start from scratch, I decided to change the Solution, Project, and assembly name as well. After I finally got the site to run, there was still one thing that bothered me: my old website's name still resided in the IIS. Memories of a once terrible developer ensued. I had to refactor this as well. But how? I changed everything in my Visual Studio file and the search function won't return anything by that site's name!

###SOLUTION
Open up SolutionFolder/.vs/applicationhos.config. Go down to the HTML **<sites>**, and there you should see the project name as *<site name="ACreaTiVeSitEnAMe" ... >*. Change it, save the file, close it, and RESTART visual studio. Problem solved.
