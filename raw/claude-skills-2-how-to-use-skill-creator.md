---
title: "Claude Skills 2.0: How to use Skill Creator to build new Skills"
source: "https://www.youtube.com/watch?v=rihf3-mpNG4"
author:
  - "[[Nick Babich]]"
published: 2026-03-08
created: 2026-04-13
description: "In this video, I will show you how to use a meta skill called Skill Creator to build new Claude Skills. This approach will help you significantly improve the quality of skills you generate for Claude."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=rihf3-mpNG4)

In this video, I will show you how to use a meta skill called Skill Creator to build new Claude Skills. This approach will help you significantly improve the quality of skills you generate for Claude.  
  
#ai #claude #aidesign

## Transcript

**0:00** · Hello, I'm Nick. In this video, I want to show you the new process of creating Claude skills. This process is so powerful that the Claude community has started to call it skills 2.0.

**0:11** · But before diving into how Anthropic improved the process of creating new skills, let's quickly cover what a Claude skill is.

**0:18** · In a nutshell, Claude skills are instructions.

**0:21** · Skills teach Claude how to complete specific task in a repeatable way.

**0:26** · When it comes to format, skill is basically a markdown file.

**0:30** · This file contains two parts.

**0:32** · Front matter between horizontal dash markers that tells Claude when to use the skill, and markdown content with a set of actions that Claude follows when the skill is invoked. Typically, it's a workflow.

**0:44** · And Claude recently added a new meta skill called skill creator.

**0:49** · It's a dedicated skill that takes a new skill description and turns it into a very strong and effective skill.

**0:55** · The Anthropic team provides a very detailed summary of how this skill works, but I want to highlight the most important attribute of this skill.

**1:03** · I'm talking about its ability to evaluate the quality of output it produces.

**1:08** · So, it creates a new skill markdown file based on description you provide. Then it measures the skill performance by running tests and improve the original skill markdown file based on results of testing.

**1:21** · And next, I want to show you how to use it. I will do it in four simple steps.

**1:25** · And the first step is install the skill creator.

**1:28** · I will use VS Code environment with a Claude code extension. We are in an empty project right now and the Claude code extension is open.

**1:37** · First, I will type a command manage plugins. This will show me the plugins I have.

**1:43** · Search for skill creator and click install.

**1:48** · Claude will allow you to install it for you or per project.

**1:51** · If you want to make the skill available for all your projects, you should go with install for you. Let's double-check to ensure that everything is in order.

**2:00** · Type manage plugins again and you should see the skill creator in this list.

**2:07** · I also suggest to submit this prompt. Do you have skill creator available for creating new skills?

**2:13** · And if Claude says yes, we can go to the next step.

**2:18** · Now, we can prompt Claude to create a new skill.

**2:21** · I will create a skill for front-end design. My goal is to craft a skill called super landing page that will use a landing page description I provide, clarify it, and turn it into a page that looks like Apple design.

**2:35** · All this I will frame in this prompt.

**2:38** · Let's submit it.

**2:39** · And you can see that Claude is running skill creator to craft this new skill.

**2:44** · And the process of creating is fully automated, meaning that we don't have to direct the skill creator to do anything.

**2:50** · It will build a new skill for us. And it will start by drafting a to-do plan with a set of actions it will perform. And one of the steps is to create the test cases to evaluate the newly created skill.

**3:03** · The process of skill creation for this type of skill takes around 10 minutes.

**3:07** · And at the end of this process, you will see a table that will show you the results of testing. And here you can see the benefits of running tests to improve the super landing page skill.

**3:18** · It added animations and CSS variables.

**3:22** · And now we can use the newly created skill.

**3:25** · To do that, I will prompt use super landing page to code this page.

**3:32** · And copy and paste a prompt with a landing page description for food delivery app.

**3:37** · The description will cover the following things: page layout, tech stack, structure, responsive behavior, accessibility, and deliverables.

**3:47** · Once I get the complete prompt, I can submit it so super landing page skill will do the job.

**3:55** · Just like before, we have a to-do list that the skill will go through.

**3:59** · And you see that it starts to write code for us. Before showing you the final result of the page it created for us, let's do three things.

**4:08** · First, I want to confirm that skill creator was used to code the super landing page skill.

**4:14** · So, I will ask Claude, did it use it?

**4:18** · Second, I can ask Claude to show what skills I have in my system by submitting a prompt show skills.

**4:26** · Finally, I can check the markdown file with actual super landing page skill to see what the final skill look like.

**4:33** · And as you can see, it's very detailed.

**4:36** · And here is a design of landing page that the skill generated for us.

**4:40** · This has many attributes we typically associate with Apple design, such as minimalism and nice animated effects.

**4:48** · Note that the prompt I submitted in step four did not mention Apple style.

**4:53** · Skill creator designed a super landing page skill according to the instructions I provided in the second step.

**5:01** · And that's all. Let me know what you think about skill creator in the comments. Thank you.