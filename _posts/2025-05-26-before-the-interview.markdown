---
layout: post
title:  "Before the Software Engineering Interview"
subtitle: "A prep guide for being a competitive software engineering candidate"
date:   2025-05-26 10:00:00 -0700
categories: [tech-interviews]
hide: false
---

# Introduction

This post is the first in a series based on lectures I gave for Pace University's Professional Computing Seminar. This first one is designed to give an overview of the application process for software jobs, from preparing a resume to negotiating an offer. The audience was for sophomore CS majors, but the advice applies fairly broadly unless specified. You can see the slides for the talk [here](https://docs.google.com/presentation/d/1iCbAnbfOwVP5hWykaKiI8kJ73e6VqUmZUh4qURh2DSs/edit), which include screenshots of my resume when I was applying for jobs out of college.

It's been quite some time since my last post, and I have a lot of ideas in my head. So hopefully you will be hearing from me more over the next few months!

# Before the application

The important theme I want to impart on students is that unlike other college majors, it is not enough to just do your school work, study for your tests, and get good grades in class. While I highly value a good computer science education, the reality of the job market is that the overlap between an academic computer science degree and an industry software engineering job is quite slim. Especially in this competitive job market, if you are looking for an internship or a full time job, you have to signal to employers that you are both skilled and are genuinely interested in the aspects of software engineering that aren't covered in school. In general, you should have:

* Unique coding side projects that demonstrate your interest and skill in building software.
* A GitHub that showcases these projects.
* A resume with your work experience, skills, and projects
* A LinkedIn that mirrors your resume, and which allows you to network with others.

I will talk about these in more detail below.

# Side Projects

As I mentioned, it is important to signal your interest and skill to any potential employers. And what's a better way to do that than working on a unique coding project on your own time. I want to emphasize that I agree it's a bit ridiculous that this is the standard (do doctors have to do side surgeries?), but this is the standard that exists. The idea here is to come up with some problem that you want solved, and then go as far as you can using code to solve that problem. They do not have to be overly complicated or have actual users, but something that comes from your own experience is always going to stand out more. So what makes a good side project?

First of all, I would say a good side project should be unique. Obviously at this point of time, it is quite difficult to come up with a problem which nobody has attempted to solve before, so that is not the standard I am looking for. However, listing a course assignment like "Self Balancing Binary Tree" on a resume won't really impress anyone at all. If you do take a project based class at school which has you develop something unique, this is of course a perfectly okay thing to list on a resume. Another option is to take a common class project, and modify it to meet some new requirements, of course asking your professor for permission before posting it online.

A good place to look is in your other interests. Are you part of a unique community which needs specialized tools? Do you have any domain knowledge in music or another interesting area? Is there some trend online which you can help automate? Even if it is silly, it may motivate you to build something, which is always good.

The side projects should also be reasonably complex. Not that it has to be a fully baked project, but if it is a few lines of Python code that read a CSV and call some libraries, it might be seen as a bait and switch and end up looking bad. I would say a good metric is at least 100 lines of Python code (or more in a more verbose language).

Most importantly, your projects should be demoable. Hiring managers already do not spend much time on your resume, so if they see a project they want to check out, it is imperative that you make it easy for them to see what you have built. The gold standard would be some kind of web UI to demonstrate what you have built, but depending on the specific project, you may want to settle for a GitHub README with videos and pictures of what you have built, even if it is just run off the command line.

So how do you come up with good project ideas? My number one tip would be to find a Hackathon; generally a 24-72 hour "hack / marathon" where students congregate to build a functioning product in this limited amount of time. From these events you are able to find like minded students with skills which may complement yours, and there are plenty of people with ideas but nobody to work on them with.  [The MLH website](https://mlh.io/) will list these events in your area; some are more selective than others, but I would highly recommend you go to as many of these as you can. So many of my projects as a student have been hackathon projects, and I have made many friends and connections through these events as well.

Besides that, I would suggest you look into your own life and see what problems you and your friends/family have. Can you build a tool to help your parents automate work they do at their business for example? Additionally, try to find other students who have congruent skills with you; e.g. if you took a machine learning class, and have a friend who has good frontend skills, you can coordinate to build something very cool visually as long as you decide on a API to sit between the two layers.

Another tip - in the age of ChatGPT, it is fairly easy to go to these LLM tools and ask for help in developing a project. Obviously you should make it clear if any code in a tool is LLM generated, but these tools are a great way to learn about how to structure a project, or if there are any libraries that may be helpful to you. I will caution against relying on these tools too much or pasting any code you don't understand (commonly referred to as "vibe coding"), but unlike school, there are no rules on these projects.

Some last advice. I see a lot of projects in the video game space, e.g. tools for being more efficient at a game, tracking statistics, coordinating players, gaining unfair advantages, etc. If you are in a video game community, this may be a great place to look. Additionally, while slightly unethical, web scraping is a great way to get unique data sets for projects. If you've seen my blog posts, you'll know I am a big proponent of scraping websites for projects.

# GitHub Portfolio

Once you have these side projects, it's important to have somewhere to host them. The standard for these projects is [GitHub](https://github.com). On the surface, GitHub is a platform that allows you to host code repositories in a centralized location, allowing for collaboration with others. In practice though, GitHub is a great way to showcase your personal projects with any interested parties. To optimize your GitHub, I suggest doing a few things:

1. Add a professional profile picture to your profile. First impressions matter.
2. It's okay to have random code snippets on your GitHub (if anything it shows that you are an avid coder), but set up the front page of your GitHub profile to have the projects you want to showcase front and center. Choose projects that you are proud of and would want someone stumbling onto your resume to check out.
3. For each project, include a README.md file which describes the purpose of the project, links to any demos/videos/images, explains how to run the project locally, and guides the reader through your code structure so they can investigate further. See the end of the blog post for a "homework" assignment related to writing your own readme.

For bonus points, creating a personal website (e.g. the website you're reading this on now) is a great way to not only curate what people see and how they see it, but also signal that you know how to set up a website. The domain name also gives you a professional looking email that definitely stands out. There are many frameworks for personal websites, I personally use Jekyll hosted on GitHub pages.

# Resume and LinkedIn

Once you have some personal projects you are proud of, you should set up a resume to showcase your projects and other work experience. Your resume is what allows you to apply for jobs, and is more or less a standard format that recruiters and managers can both scan through to understand what experience you come with. I am not a recruiter or anyone involved in career services, so any resume advice comes from my own personal experience and opinions. I suggest starting with a template your university provides for you, or something you find online which looks good to you. In general, a resume will contain sections for a header, your education, your work/volunteer experience, skills, projects, and anything else miscellaneous.

In terms of what not to include, I generally find objectives to be a waste of space, though you might want to include a short one. Definitely do not include a picture of yourself, or "references available by request". Additionally, do not exceed one page.

For the header, include your name in some larger font, and then include your city, phone number, website, GitHub, and LinkedIn. This is where you can include a longer objective or a title as well (e.g. Computer Science Graduate, Aspiring Software Engineer).

In your education section, for each degree, list the name of your institution, your (expected) degree, your start date and (expected) graduation date, and GPA if it is generally above a 3. You can also list any relevant classes. I would advise not listing your high school unless you are particularly new to college, need to fill the space, or went to a particularly prestigious high school. For the relevant classes, use names that are commonly known, e.g. Data Structures instead of CS 128.

For your job experience, I suggest listing anything computer science related before any jobs that are particularly unrelated, but otherwise keep them in chronological order. Especially for students it's understandable that most of these will just be volunteer experiences that are not actually paid - it's up to you if you want to list them all together or have a separate volunteer section.

For each experience, list the company, the team you were on, the job title, start and end months, and any technologies you used if applicable. Under this header, you should have bullet points that describe your responsibilities and accomplishments at this job. These should be via action verbs (developed, designed, launched...) and any quantifiable metrics should be listed (reduced build time by 45% on average). It's understood that interns do not have too many responses, but do your best to sell yourself well. For any non technical jobs (e.g. retail), emphasize any transferable skills such as leadership or coordination. If you were able to use code in any non technical job (e.g. to automate a task) that is a great thing to highlight as well.

In a skills section, list any technical skills that you have picked up from your classes or personal learning. This includes programming languages, popular frameworks (e.g. Flask), or popular large libraries (e.g. Tensorflow). Do not include things like operating systems, software tools (Microsoft office, Photoshop), websites, etc. Final thing I'll say is don't list anything unless you would want it to come up during an interview. I get around this by having different lists for skills I am very familiar with vs just passing familiarity.

In a projects section, list the project name (make it a memorable and descriptive name), a description of the project, and the main technologies. Link to the GitHub, which should have a more descriptive readme. As mentioned before, personal projects are preferred over class projects, but try to have something here.

At the end, you can have a list of activities or hobbies to give off some personality, but that is up to you. Don't list anything that might be seen negatively by a potential hiring manager or recruiter, use your best judgement.

Once you set up a resume, you can more or less mirror this onto a LinkedIn account. I do not have too many opinions about LinkedIn, but it's a great way to find potential jobs. I would suggest getting a professional headshot for your profile, and not one of the AI ones.

# Applying for jobs

I want to make another post about applying to jobs and interviews, but I figure I should talk a bit about it here.

Once you have all of these items, you should be fairly well situated to finding a software engineering job or internship. If you're looking for a first job, look for "new grad software engineer" roles, or for internships look for "software engineering intern" on LinkedIn and Google. In this competitive market, you should more or less apply for any job that you see. If a role seems like a particularly good fit you can spend a bit of time writing a cover letter, but generally these take up too much time. Additionally, put yourself anywhere where you can make an in person impression with a recruiter, such as a career fair or a hackathon. For a first job in this market, you may have to be a bit creative about a first internship; for example I found something on Craigslist as a first internship out of school.

Final piece of advice: if you know anyone in the software industry, do not be afraid to ask them for a referral. Find a role at your connection's company, and reach out to them to ask for a referral BEFORE applying. Do not feel too bad about asking for these referrals, it's generally pretty easy and they might even get a cash bonus for referring you. The power of a referral depends on the company, but generally you will get an assured review of your resume.

# Homework
Now that you have read this, work to develop some interesting side projects, and add READMEs to the projects you already have. For an existing project's README, write one that includes all of the following information:

* **Summary of the Project**: What does the project do? What technologies are used?
* **Link to a Demo**: Provide a live demo link if the project is hosted somewhere.
* **Video or Screenshots**: Include a video walkthrough and/or screenshots of the project.
* **Instructions to Run Locally**: Provide clear steps to set up and run the project locally.
* **Code Structure Breakdown**: Explain how the code is organized. Where should someone look to see the core logic or features you implemented?
* **Challenges/Learnings from the Project**: What was the most challenging part of this project? What did you learn from building this project? How does it contribute to your career goals?
* **Future Plans**: What are your future plans for this project? Are there features you’d like to add or improvements you’d like to make?
* **FAQs or Additional Notes**: Include any questions people may have or any additional information you’d like to share.

If you don't have any projects, try to think of some interesting ideas. When you have the basis of the idea, try answering the following questions about it:

* **Project Idea**: What is your idea for a complex project? Is it a web app, mobile app, backend API, Python/Java program, data science analysis, etc.?
* **Usefulness**: How would this project be useful to others? What gap in the market are you solving?
* **Ingenuity**: What similar projects exist in the market? What are you planning on doing differently?
* **Previous Projects**: What previous projects have you worked on? How are they similar to or different from your new idea?
* **Technologies**: What technologies (programming languages, frameworks, libraries) are required for this project? Why are you choosing these technologies?
* **Knowledge Gaps**: What are your current knowledge gaps? What do you need to learn to complete this project?
* **MVP and Development Phases**: What is the MVP (minimal viable product) for this project? If you don't know what that means, look it up. Break down the development into a few phases, starting with the MVP and adding additional features on top of that.
* **Career Goals**: How does this project contribute to your career goals?
