# Claude + Karpathy's Second Brain is INSANE

- Source: https://www.youtube.com/watch?v=5FiHjotg2zU
- Subtitle Language: en

## Transcript

Kind: captions
Language: en
So Andrej Karpathy put out a tweet a
couple of days ago that went mega viral
talking about how you can build your own
second brain using Claude Code and
Obsidian. And in the next 20 minutes or
even less than that, you're going to be
able to build your own. Nick B Zark is
going to walk us through it. So Nick,
from a high level, tell me what we're
going to do today. What are we working
with here? Yeah, so basically what we
have is this is the concept of the
second brain. So essentially what this
will give you the ability to do is to
organize any of your data that you have
in a way to make yourself more
effective. That can either be for your
personal needs, thinking through what
are the items that you do on a
day-to-day basis, or can be more aligned
to business practices. For us
specifically, we're using Claude
projects for a lot of the content that
we're creating or the process of finding
good content to put out on social media.
This is a good practical use case to
leverage this concept that Andrej put
out over the weekend, which is known as
the second brain. So we're going to
build it right here, right?
Yeah, we'll build it literally as part
of this episode start to finish of how
to get this system up and running.
All right, let's do it. So basically
Andrej was one of the founding
researchers at OpenAI. He's one of the
top most influential people in AI right
now. So anytime he puts out a tweet, it
goes super viral. So on April 2nd, he
put out a a tweet around how to build
your own LLM knowledge base, and he
breaks it down step by step. And as it
went over over the last couple days, I
saw his original X post that was out
there and built one as well that kind of
talked through the fundamentals of how
to build your second brain.
Later that same day, he put out a
follow-up tweet that talked through this
concept of an idea file. And this is
really fundamental because today we're
talking about second brain, but this
concept can apply to anything. And the
idea file was creating your own LLM
wiki, and he made it intentionally
vague. He broke it down into to describe
what was the outcome or the core
benefits that you're looking through
based off of an idea,
some loose ended architecture of how you
could build this type of system,
ultimately what the operations of that
system should look like, how you can go
through to do indexing and logging to
make it more useful
in the future. And then some optional
command line tools that you can add to
enhance the system to make it work based
off of your needs. So what we did here
is over the weekend, took that updated
version and literally recreated the
concept of the second brain, but this
time as a full end-to-end workflow
that's built as a Claude skill. So what
we're going to do is we're going to
literally walk through this process step
by step and how to create a second brain
utilizing the tools that Andrej
referenced loosely in his idea file. And
some of the ones that we're going to use
for today are going to be Obsidian,
which you'll see really quickly here is
a way to take any of your unstructured
files and to put them into essentially a
mind graph where you can see the
connections in the patterns of how
they're interrelated and how they work
together.
We're going to utilize an example of
Obsidian Web Clipper, which is literally
a Chrome extension that whatever page
you are on, you can choose the location
of where you want it to be stored in
your Obsidian vault and click add to
Obsidian and it will grab or scrape not
just the text, but also the images that
are there.
Optionally, you can install what is
known as summarize. This was um put
together as a open source library that
Peter, the the creator of Open Claw, has
written. And what it does is it allows
you to extract YouTube videos. So you
can get transcript files that are put
into LLM friendly markdown to be able to
use for the same purposes. So not only
are we doing images and text, but we can
actually grab YouTube transcripts from
your favorite podcast creators and
authority figures of the topics that
they're looking for and have these
registered into your vault.
And Nick, uh just before we keep going,
so you that skill that you said that you
built, what does the skill do? And and I
know we're giving it away to the folks
who are in the audience here. So if you
guys are I'll let Nick kind of explain
the skill and if you guys want to grab
it completely free, you can go in the
description or in the show notes and
it's just like a one-click download.
What does the skill do and then we'll
jump into the actual build? Yep, so the
skill itself is based off of Vercel's
framework. So if you're familiar with
Vercel, Vercel Vercel is essentially a
framework that allows you to do web
hosting and they also put out a ton of
open source software. So we're using
their framework to be able to build an
end-to-end skill for all of the common
AI harnesses that are in the industry
right now. Claude Code, Codex, Gemini
CLI, Open Code, Pi, whichever your agent
harness of choice is, the idea here is
this is an end-to-end
skill that you can go ahead and add
directly from the repository and it's
going to give you the ability to set up
a new vault through a guided wizard to
ingest any new sources into your wiki,
to query against it so you can ask a
question whether it's you want to do
competitor analysis or you want to find
out about a new topic or a new angle to
your content, and then ultimately what's
called lint, which is to health check
your wiki. So it's a way to be able to
prune or remove any outdated articles
that you may have in there or to look
for additional connections that you can
use in your Obsidian vault.
Awesome. Yeah, that's super valuable. So
again, show notes or description if
you're watching on YouTube, go grab that
skill for free. Now let's let's dive in
and actually build this thing. Okay,
perfect. So for this demonstration, what
we're going to do is we're going to fire
up Claude Code. And anytime after you've
already done the install here, you will
see
in this the read me will walk you
through the setup guides. This is
literally the one-click install setup
for doing second brain. And what that
will allow you to do is you can
literally just hit the command second
brain, which will run the skill.
It will take a little bit to do here,
and it's going to ask you, "Okay, well
what do you want to call your second
brain?" So for this, we'll call it
YouTube demo.
And that's going to give the actual
vault its name.
It's going to ask us where on your local
computer do you want to have this
stored? So for this example, we're going
to store it on our desktop.
All right, so it gives us the pathing of
where our vault's going to be stored.
And for this, we'll just call it AI
research as the topic. So you can
actually give the knowledge bases itself
just so it has some additional tags or
data associated with it so it gets into
the ability of having a context around
what this vault is used for.
Um so now it's going to ask me if
there's any other config files that I
want to add. So for right now, I'm going
to go ahead and see it says I'm on
Claude Code, do you want to generate um
a Claude MD for this? Are there any
other agents that you'd like to
configure it for? So we're going to say
Codex. And basically what this means is
Claude Code has a Claude.md file for its
configuration.
The other
agent harnesses that are available, they
use what's known as an agent.md. So this
is just going through and literally
walking you through any of the
additional setups you want to use.
Now the next step is it's going to say
is there any optional tools? So I
already have summarize, which will allow
us to summarize and grab transcript
links through the command line interface
for YouTube.
Um quick uh QMD is for searching over
large knowledge bases. This was a tool
that Toby, the uh CEO of of Shopify, has
created and it's really good. And agent
browser is an alternative for web
research and is made by verse by Vercel.
So I already have all three of these, so
I'm just going to say already installed.
And for the viewers, some folks will
have other part or other tools in their
toolbox that they would prefer to use
over these three. These are just ones
that I have. This is fully customizable.
You can take this exact same GitHub
repository,
put it into Claude Code, customize it to
your own unique needs, and have it build
a system for your second brain that's
more personalized to you.
Now Nick, super quick question. So
obviously the setup wizard makes it like
brain dead simple to spin up as many
second brains as you could ever want.
I'm assuming you'd want
to kind of specialize your second
brains, right? Like it would it is it
not very efficient to have this one
master second brain for like everything
and anything you'd want to store
information on, anything from like
personal to fitness to AI to work? I
assume that's inefficient, right? Yeah,
there's there's definitely a balance
[snorts] between how many brains you
want to manage where you're just doing
maintenance of all the different vaults
and making sure that the data that's in
it has the right relationships and
connections. So for for right now, the
the spot where I'm kind of delineating
this is personal and business at the
moment. That may be subject to change.
And the beauty of this is once you have
it set up, it's just a matter of being
able to follow the same process of
taking your data, putting it into what
is called the raw directory, right? This
is part of that idea file that Andrej
laid out, and all you need to do is then
run the ingest command which we'll show
here briefly to be able to put it into
the appropriate structure of the wiki.
So right now, I'm using a lot of Claude
projects, especially for our content
strategies. Going to be using this more
and more for Obsidian. And the next
tier, really, after these kind of like
personalized second brain or knowledge
bases, is what is known as as as rag. Or
and that's kind of more of the advanced
tier where you get into much larger data
sets, more complexity that's involved.
So, for the users there, that's the a
good natural path as you go from
projects or or chatbot type knowledge
bases into an Obsidian vault. And from
there, you can graduate into some of the
more advanced capabilities when it when
it's necessary with scale.
Got it. Okay, that makes sense.
All right. Now, so the installer has
gone through and it's now just giving us
a reference point here. This is the
Chrome extension for the Obsidian Web
Clipper. I've already installed this,
but if you go to this link,
what this will do is it's literally just
going to take us out to the Chrome Web
Store.
You'll click add to Chrome. For me, I
already have it installed, so it says
remove from Chrome.
And what this will do is you'll be able
to
grab
this Chrome extension.
Uh I can't clip the existing page here,
but I can go to the one that we're going
to use for our demo.
And you can right-click on it
and click on options. And the options
are any of the customizable settings for
Obsidian that you'd like to use. The
main one that I've changed from the
defaults is under literally under
default. There's a section of where do
you want in your Obsidian vault to
store? So, this normally says web
clippings on it. I switched it to raw to
align to the idea that Andre's laid out
of these three tier structures of your
raw items, your your wiki, and then what
he calls your outputs. Your outputs are
essentially reports or things that
you've generated that are essentially
decision files based off of the content
that came in from raw and then the wiki
itself that came in as part of what
you're searching or querying against.
And that makes sense because the raw is
basically like your brain dump. It's
like that's just where you dump anything
and everything that you think you want
in your second brain in some capacity.
And then
I'm assuming the wiki is when when the
AI goes in and like organizes it into a
and and kind of trims it and makes it
digestible. And then outputs is anything
that where I guess you're querying your
second brain and it's it's going and
looking through the wiki and saying,
"Well, hey, based on what's in the wiki,
here's what you're asking for." Like am
I kind of understanding that correctly?
Yep, that's perfect.
All right. So, here, now that we have
Obsidian, I already have it installed,
you'll see a similar type experience
when you load it for the first time. So,
normally you'll do a create vault, but
given that we've just used the wizard to
to do that creation process for us and
lay out the whole scaffolding of the
setup, all we need to do is open a a new
vault or open a vault.
So,
we saved ours to the desktop, so let me
go to desktop.
And there should be a YouTube demo
folder here. So, we'll click open.
And what this will do
is it will create a new vault file for
us. So, you're going to see here, right?
We have our outputs folder that's empty.
We have our raw with assets that are
currently empty. And we have our wiki,
which lays out the scaffolding, the
concepts, the entities, the sources. So,
all the metadata that you need. And then
we have our agent.md file and our
Claude. And this is to make it agent
agnostic, so we can use any of our AI
agent harnesses to be able to manage the
vault that's there.
Now, what you're going to see, and we're
going to use this in real time, is
there's this concept of a graph view.
And this you can see that these files
right now are currently all There's no
groupings with them, right? They're all
at this point There's no relationships,
so they're categorized as orphans, which
you're just seeing that these are the
four files. They exist in the system,
but there's no There's nothing that you
can do really with them yet. They just
exist there. There's no
interconnectivity between the data that
they're providing. So, the first thing
we need to do is we need to put some
data sources in. So, for this example,
I'm literally just going to go to the
wiki the Wikipedia entry for Andre that
talks about him. And we're going to grab
the Chrome the um web clipper.
All right. And then we're going to go
ahead here and we're going to click add
to Obsidian.
And it's going to grab the article.
So, you can see now on the side, if I
close the the side panel here, it
literally grabbed the Wikipedia entry,
all of the content that's associated
with it, and any of the sources that
were there. So, now we have an artifact
that we can use. And inside that
artifact, it's stored in the raw, like
we talked about, and it's sitting right
in there that we can utilize now as any
of our brain dump thoughts. So,
the next step in the process is we
literally just say second brain ingest,
which is a separate skill that's in that
repository.
And what it's going to do is it's going
to go through here and it's going to
first check the directory, so we're in
YouTube demo raw. It's going to read the
files and find it. You can see that it
actually identified that Wikipedia on
entry as a markdown file.
It summarizes all of the key points that
it learned in terms of its takeaways.
And then I'm just going to say ingest.
Okay, I see. So, it's like you can just
go and basic like quote-unquote brain
dump, meaning just Obsidian Web Clipper
as many files as you want into the raw
folder. And then what? Once a day, once
a week, or just whenever you feel like
doing it, then you go back into Claude
code and you run ingest. And that's when
it's going to take everything in raw and
essentially read it or, you know,
analyze it and then dump it into the
wiki. Is that Is that correct in terms
of order of operations? Yeah, that's
exactly it. So, basically, what it's
going to do it anytime you want to rerun
it. Now, you could even get more
sophisticated with this, right? And
Claude and think of this from the
overall ecosystem of AI agent harnesses.
If you're on Claude code, there's a
concept of loop, right? So, loop allows
you to do it on an interval and a
prompt. So,
&gt;&gt; That's what I was going to say. I was
like, couldn't you just set up it to
ingest on a cron, like every, you know,
well, depends on how how often you're
using it, but 24 hours, 48 hours, or
weekly ingest automatically? Yeah. So,
you could literally have just a session
running. And you can see here on the
right as this is going, it's building
the graph. So, before where we saw those
orphan files that are there, now you're
starting to see based off of the
Wikipedia asset that we gave it, that
now there is these interconnections of
anytime we're talking about Andre, it's
now going to say, "Okay, well, what's he
known for?" Being a founder over at
OpenAI, his deep learning. Where did he
go to school? At Stanford. So, all of
these connections are be are being built
in this graph view. And this graph is
essentially the the interconnectivity of
all the different raw data sources that
we have. So, the next tier of this as it
finishes
being able to index across the the data
that it found, we can actually now run
the second the next stage of this, which
is to actually try to make something
useful, which is to answer a question
around the vault or the second brain
that we have. So, we can literally say
like,
"Where did Karpathy
go to school?"
And if it can find it in its knowledge
base of that wiki, we'll get we'll get
answers related to the content that's
there.
And so, to kind of bring this down to
ground level, like from a business
perspective, so let's just say that I'm
a business and I have a team and I'm
doing, you know, three, four, five, six
Zoom calls a week myself. And then my
team's doing a bunch of calls as well.
Probably what I should do is set up my
second brain to have all the transcripts
from every call dumped into my second
brain. So, that way if at any time, any
place,
if I'm like, "Oh, what did me and Karen
talk about last week?" I could just go
into my second brain and query it and it
would tell me exactly what was discussed
without hallucinating, without me having
to go dig through transcripts, or even
ask Karen. And that's also the most
basic use case. I mean, this is I feel
like a a company asset that compounds
significantly over time. I mean, that's
one thing that he talks about, right? Is
that like
day zero, this thing is like kind of
useful, but day 30, day 60, day 90, this
becomes a hugely uh valuable company
asset that compounds over time that
nobody else is going to have except you.
Yep, that's exactly it. This is
definitely [snorts] the when you set it
up the first time, it's the dumbest it's
ever going to be.
Um Obsidian also offers the capability
on their paid tier to sync vaults across
devices. So, let's say you're out on a
walk and you're on your mobile device
and you get an idea and it's just needs
to be flushed out later, you could
utilize your mobile phone to quickly
record a note of what you would what you
were thinking about, drop that into your
raw, and then if you have back on your
desktop, you have a loop running, right?
Maybe it's running every few hours, you
come back and it's already been indexed
into into your into your vault and is
ready to use. So, this is just something
that you incorporate into your
day-to-day practices where it may where
it's where it makes sense. And having
those maybe it makes sense to have them
one for personal, one for business since
the topics are different. But each
person's going to be a little bit
different in how they set them up, but
hopefully now we've done an under 20
minutes an end-to-end setup. This kind
of gives you an idea of where you could
use this capability and gets the ideas
kind of flowing in terms of how it could
help you in your personal and in your
business.
Now, in 30 seconds or less, go through
how you prune it because you mentioned
that as one of the features. Cuz
obviously, over time data gets stale, or
maybe you have uh wiki entries that
contradict each other. So, give us like
the 30-second overview of how do we trim
this thing and make sure it's always
relevant and never stale? Yeah, so
literally it's a it's just another
skill, right? Everything's built as a
skill. So, in this case you're going to
run the second brain lint and lint is
just going to review what's already in
the wiki and see if there's anything
that conflicts. Now, in this demo we
only put in one one article right now
and clearly we just did it so it's going
to have it's going to be up to date at
that point, but it'll do some research
and ask you a little bit more about what
it found if it's anything that's there.
So, in this case it didn't find any
errors that were must error fixes. It's
just giving some different warnings that
we can look at and say, "Okay, well,
does this make sense? Is there any gaps
that are there?" And that can give you
the hint of like, "Oh,
well, that's great. Well, there's some
missing items here around University of
Toronto." Like I could literally just go
out to the University of Toronto wiki
page, use the web clipper, drop it into
raw, re-index it, and now I can
potentially I'm closing some of those
gaps. So, if you have
&gt;&gt; If you have that domain, right? You just
pick a domain that you want to work in
and you spend some time refining that,
it it's a great way to build ultimately
what is the most important thing, which
is how do you build your own private
knowledge base or your own data set. And
this that's really the final boss of how
to create a moat here in the AI H.
And that that data set that you're
building it is your moat for any agents
that you build, any skills that you
build, the entire company you're
building if you're an entrepreneur, etc.
So, just to kind of put a bow on it, I
think this is one of the most
significant things to come out of AI in
the last few months, which is saying a
lot because so much happens so quickly.
Every company is going to have a second
brain like this eventually. I think
second brain as a service is a
is going to be it's going to explode in
popularity in terms of people offering
this as a service to other businesses,
like a two to five thousand dollar setup
fee and then a few hundred dollar a
month retainer to maintain it for
businesses.
If if there's not people out there doing
it right now, they will be within the
next week, I guarantee it. So, this is
crazy, Nick. This is awesome.
For those in the audience, again,
reminder, if you want the skill that
Nick just showed us, that literally sets
all of this up for you,
get it in the description if you're
watching on YouTube, if you're watching
or if you're listening on the podcast,
go in the show notes and download it
there. It's completely free. Nick, thank
you for your time and for everybody
else, we'll be back in a few days with
another episode. My pleasure.
