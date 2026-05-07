---
title: "Stop Writing Bad CLAUDE.md Files"
source: "https://www.youtube.com/watch?v=lJNjDoJi6hQ&t=14s"
author:
  - "[[camelCase]]"
published: 2026-02-04
created: 2026-05-03
description: "Sponsored by G2i (paid promotion) — Check it out here: https://g2i.co/camelcaseMost CLAUDE.md files are too long, too vague, or contain counterproductive content. Here's how to write project instruc"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=lJNjDoJi6hQ)

Sponsored by G2i (paid promotion) — Check it out here: https://g2i.co/camelcase  
  
Most CLAUDE.md files are too long, too vague, or contain counterproductive content. Here's how to write project instructions that keep #ClaudeCode performing at its best. Backed by real #LLM research (applies to #AGENTS.md, #Cursor, #Codex too).  
  
🍿 Chapters:  
00:00 Intro  
01:01 Tip 1: Size matters  
02:33 Tip 2: Don't use /init  
05:03 Tip 3: No codestyle  
06:19 Tip 4: Start with these 3 things  
08:17 Tip 5: Progressive disclosure  
10:15 Tip 6: Why Claude ignores you  
11:41 Tip 7: Keep it updated  
12:56 Tip 8: Different location options  
  
🧑‍💻 Further information:  
Path-specific rules: https://code.claude.com/docs/en/memory#path-specific-rules  
Hooks reference: https://code.claude.com/docs/en/hooks  
GitHub Action Setup: https://code.claude.com/docs/en/github-actions#setup  
  
📜 Legal:  
Music License Codes: VOINKK4VUN4TLJ6C, VX5YXVKM8I8FSXA8, OHRMTVXNJQP3895M, OTQRUBEYV0BESSYT, DLUADDWLR7I5J8JD

## Transcript

### Intro

**0:00** · Every line you add to your Claude MD can do more harm than good. Why that is and how you can optimize your Claude MD with a few simple tricks, that's what I'll explain you here. And by the way, most of the tips from this video are also relevant for agents MD. So also for Codex, cursor and so on. Let's go.

**0:20** · Even if you work and code with AI support every day, you simply have to keep in mind that Claude knows nothing about your codebase at the start of every session. Because LLMs are largely stateless, they don't learn over time.

**0:31** · Claude doesn't know which framework version you're using. Claude has no idea about your unconventional branching system, your test strategy, or whether you even have one. Claude doesn't know that you need to run some weird mock to start your application on your machine.

**0:45** · All the quirks that might be second nature to you are not second nature to Claude. That's where Claude MD comes in.

**0:51** · A markdown file that Claude automatically reads at the start of every session where you can write project specific instructions. Sounds simple, but it comes with some pitfalls.

### Tip 1: Size matters

**1:01** · \[music\] If you take away just one thing, one tip from the video, then the size of your Claude MD plays a massive role. And it should be as small as possible. Less is more. Under 300 lines, but ideally even shorter. Because here's the problem. The most powerful large language models like Claude Opus 4.5 can follow about 150 to 200 instructions with reasonable consistency. Smaller models significantly less and 150 might sound like a lot at first, but prompt engineering has shown that Clot Code system prompt alone already contains about 50 instructions.

**1:32** · That means a third is already gone and you haven't even written a prompt yet. And as I said, we're talking about the good models here. On top of that, if you're working in a company, your IT department might have defined global instructions for claude in a manage scope. And now, if your claud in your project is very extensive and let's say contains couple hundred lines of code, then that's a problem. One line often contains multiple important pieces of information. And what happens when Claude gets too many instructions, has loaded too much context.

**2:00** · Unfortunately, it's not simply the case that Claude just ignores the 151st, 152nd instruction, but takes the others, the first 150 into account perfectly. No, unfortunately, the overall quality of the responses then degrades massively.

**2:19** · All instructions are then taken into account equally worse. And with smaller models, this is also documented. This quality degradation happens even faster.

**2:26** · So, the fewer lines, the fewer instructions, the fewer tokens, the better. So, what's the best approach to start?

### Tip 2: Don't use /init

**2:34** · Claude Code is friendly and offers you to create a claim MD file via the init command. Great, right? Well, unfortunately, not. You actually shouldn't use in it. Or generally speaking, you shouldn't let an AI create a cla file because as you now know, the shorter the better. But, as is often the case with AI, an AI generated text tends to be very, very verbose. So one problem with AI generation is the length of the whole thing. It becomes too long.

**3:00** · But there's also another problem with how an AI generated claudin can negatively impact your daily work. Namely through vague or even incorrect as well as unnecessary instructions. And this is important to understand even for things you write in there yourself. One line of bad code only affects exactly that code location when it's executed. But one line of bad Claude MD has negative effects on every prompt and every action that Claude executes for you that Claude executes for other developers working on the same project.

**3:31** · This can degrade your performance and results for years. And running in it sounds like an easy shortcut, but unfortunately also leads to things in the Claude MD that you don't necessarily want there. For example, you see this super often, code style. And notes about code style have no place in the Claude MD. Why? I'll explain that in a moment. But first, a few words about my sponsor for this video, G2I. If you're looking for engineers who actually know what you're doing, it's not exactly easy.

**3:55** · You either end up with way too many inconsistent and probably lots of AI generated applications and have to dig through the noise, or you get far too few applications, and that's where T2I can help. G2I is a video-based hiring platform specialized in engineers. They take care of sourcing candidates, running interviews, doing the technical assessment, and they have over 8,000 engineers in their talent pool. They even organized the React Miami conference every year. So they are deeply connected with real experts and can find the right person for your open role, whether it's front end, backend, full stack, and much more.

**4:27** · So how does it work? When you open a new position, you simply fill out basic role details, contract or full-time, the level of experience you're looking for, and you define three to five specific interview questions that matter to you, and then you get results quickly. G2I knows you can't wait around. On the platform, you'll receive a neat list of potential candidates who already passed a technical assessment. You can watch videos of them answering the exact questions you provided. And if you want to meet someone, you can schedule an interview directly through the platform.

**4:56** · So, give it a try. They've already helped many, many large and also growing companies. You'll find the link to G2I in the video description. And now, let's continue.

### Tip 3: No codestyle

**5:05** · Don't give your AI code style instructions. Don't write things like use two spaces for inundation, single quotes for strings. That's sorry, stupid. With that, you have a very expensive and yet still verse Lint. And that's exactly what you should be using instead lint code formatters. So, first of all, claude will probably do a pretty good job anyway in existing code, deriving existing code style guidelines from it, and you don't need to write that extra into the claude MD.

**5:29** · But if you do write it in there, then those are valuable instructions that you're wasting for a task that costs Clot relatively a lot of time and Clot won't even approach it deterministically and will make small mistakes and then your pipeline will still abort because of some small formatting thing. That's frustrating. Instead, you can give instructions like use biome for formatting linting or run npm run lint before a commit. Even better though is to use hooks for that.

**5:55** · Claude defines for example the post tool use hook and for that you can simply create a settings JSON in thecloud folder and define there that after every file update a formatting command is executed here for me that's a shell script but you can also specify npm commands or whatever directly I linked the documentation for the hooks in the video description that's a really awesome feature there are three core building blocks that make sense in every claude MD what you should start with is a oneliner describing what kind of project.

### Tip 4: Start with these 3 things

**6:25** · This is something like this is our customerf facing payment portal built with Nex.js or this is a documentation site built with Astro or this is an Angular based portfolio site. So this already gives Claude tons of information. It knows which framework, which technology, which programming language is being used. It knows whether it's about a UI or an API or whatever. It knows roughly which industry we're working in and whether it's an internal tool or a customerf facing application.

**6:51** · Next up are key commands, meaning simply the most important bash commands for the project for testing, building, linting, deploying. Like in an npm project, for example, npm run build, npm run type check. But these don't have to be all commands, just the ones that make sense in daily work. If you need a special command once in a month, it's not worth telling Claude about it here. Be conservative with the information you give Claude. But telling Claude how it can run tests makes total sense. Then it can validate its own changes.

**7:17** · Next important content for the cloud MD caveats meaning project specific warnings things that aren't immediately obvious from the code and that can save time and prevent errors later like for example never modify schema.prisma Prisma directly run npm run db generate

**7:34** · instead or the API web hook endpoint expects raw body don't use body parser or images in public must be optimized before commit more than 200 kilobyte fails CI that kind of thing is gold because claude naturally builds on word knowledge and doesn't know that there are special things in your project but if you communicate that up front it can anticipate it these three things one line about the project most important commands caveats with that you've already created a great foundation but of course Other things can be added as well.

**8:02** · However, it is best to only include general information in Claude MMD that is relevant to the vast majority of use cases. But there are of course many other things such as edge cases and so on that you would like to communicate to the AI. How to do that in your Claude MD? If you list every edge case, the context becomes too large and quality decreases as already mentioned. Nevertheless, there are ways to make things that Claude needs more frequently, but not always available to the AI.

### Tip 5: Progressive disclosure

**8:30** · For example, you often see Claude MD files that include information about database schemas, but if it isn't a pure database project, those are probably instructions that rarely matter. Still, every now and then, you want to create a new model. And in those cases, it would be great if Claude automatically receives the corresponding database instructions without me having to prompt them every single time. And this is where the principle of progressive disclosure comes in. For instance, create a file with a descriptive name like schema.md in a doc subfolder where you list the details about your schema.

**9:02** · And in your claude MD, you simply reference it. For example, just in the form of a list where you write further documentation, database read at docs, schema md when modifying models. This way, Claude can decide to read this file when needed. Of course, there's still room for error here. The clot might sometimes read the file unnecessarily in anticipatory obedience or it might not follow the instructions when it should. However, there's a really cool feature for loading certain instructions based on paths.

**9:30** · You can create a rules folder inside a dotcloud folder and in there you can store various instructions. For example, for testing, for security, for whatever, if these files just exist there, claude will always read them. So, at first this only helps you with organization, but it doesn't make the overall context smaller. But you can add a path specification at the beginning of each file. And this is really really cool. This way you can tell cloud code to only read this file when working on files in a specific directory or only when working on files with a specific file extension.

**10:01** · For example, with tests, just write spec.ts and claude will only read this testing MD file when it's actually needed. Otherwise, these instructions won't fill up your context.

**10:13** · I just love it. \[music\] Now you might have done everything right but notice that claude sometimes still doesn't do what you actually told it to whether in the prompt in the claud or in another file. Why is that? There can be various reasons for this. We've already learned one. The more instructions overall the more likely the AI is to generally ignore any instructions at all. Then and this is really interesting to know clot code is always told in the system reminder that the context it receives in the cloud MD might not even be relevant. It reads like this important. This context may or may not be relevant to your tasks.

### Tip 6: Why Claude ignores you

**10:45** · You should not respond to this context unless it is highly relevant to your task. That means anthropic is basically telling its AI, oh what the user says might not be relevant sometimes. Additionally, LLMs generally tend to prefer instructions that are located at the edges of the input prompt. Meaning at the very beginning that is the CL code system message and the beginning of your cloud MD and at the very end the most recent user messages your prompt. something that's somewhere in the middle of your claude MD or the current context \[music\] gets neglected more easily.

**11:14** · That means you can also implicitly weigh things with this. So write the most important things at the beginning of your Claude MD whenever possible. Then another trick, this sounds trivial, but Anthroic mentions it themselves in their documentation. If you emphasize things, for example, with a capitalized important or you must with exclamation marks or whatever, that can help. These things are then more likely to be considered by the AI than other things.

### Tip 7: Keep it updated

**11:42** · Very important, the CLA MD should be a living document. If you just write it once and then forget about it, you run the risk that your codebase changes and instructions become obsolete. And also many things that make sense in a Claude MD often only become apparent during daily work. That means it needs to be natural and also easy in your workflow to update the Claude MD. If you notice during test creation that Claude is using the wrong test framework Jasmine instead of yes or V test then immediately write that into the claude MD in the appropriate place.

**12:11** · For this I also have a concrete tip from an anthropic employee. There's a claude GitHub integration where you can simply tag claude in a pull request and ask to update the claude MD accordingly. That means for example you're doing a code review for someone, you've come across something that should be documented and then you just quickly write a comment.

**12:31** · Solutions like these save a lot of annoying overhead. If you're interested in how to set that up, I've linked a setup for you. Regardless of that, especially for development teams, it makes sense to schedule regular, for example, monthly audits of the cloud MD to see what has changed and especially to respond to any adjustments in cloud code because the behavior of AI as well as features of cloud code naturally change regularly.

### Tip 8: Different location options

**12:56** · So where do you even put the claude MD file? There are several options for this which I wanted to explain to you as well since they favor different use cases.

**13:04** · Normally you can just place the file in the directory where you run claude. So in the root of your project. However, claude will always search in additional locations and that can be interesting too. For example, claude will automatically search for claude MD in every parent directory even outside your project.

**13:21** · So if you run clot code in root/fu the clot md from fu will be considered but also the one from root if it exists obviously why is that this is designed for monor repos for example if you're working in a subdirectory the monor repo root can still apply rules that are valid for all directories within it by the way it works the other way around too if you run clot code in a parent directory but then work together with clot on files in a subd directory clot will automatically read in a claude MD file from that subdirectory.

**13:52** · Then there are two more options that are especially interesting if you want to give claude instructions that you don't want to check into a shared repo. Claude will also read claude.local.md which means you can create this file instead of claud md and then add it to the git ignore. Obviously this is useful for example if you as a developer have a personal sandbox URL for example and don't want to share it with other developers. So project specific but personal instructions. And lastly, you can also place a claud in your home directory at tildy/.claude.

**14:24** · This then applies to all your claude sessions regardless of which project you're in. So if you have any personal instructions that should apply to all projects, want to use certain tools or want to request a specific language or style of responses from Claude, you can write that in there. So now it's your turn. Do you have any tips for Claude MD that you would like to add? Then write them in the comments. Also, I'd really appreciate a like on this video and a subscription. It helps me a lot to keep producing videos like this.