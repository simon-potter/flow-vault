---
type: research
title: 'Transcript: Turn Books Into AI Business Advisors (Full Notion Demo)'
parent: projects/invisico
creator: Systems Made Better
duration: '38:55'
video_id: OAgU6sOmih0
published: '2026-06-05'
source_url: 'https://youtu.be/OAgU6sOmih0'
ingested_at: '2026-08-09T09:37:34.956Z'
source_kind: put_page
corrected_at: '2026-08-09'
creator_site: bettercreating.com
ingested_via: put_page
tags:
  - active
  - market-research
  - transcript
---

# Transcript: Turn Books Into AI Business Advisors (Full Notion Demo)

**Video URL:** https://youtu.be/OAgU6sOmih0
**Channel:** Systems Made Better (bettercreating.com)
**Duration:** 38:55 · **Published:** 2026-06-05
**Captions retrieved:** 2026-08-09 via `yt-dlp-flow` (auto-generated English, 7,039 words)

> ⚠️ **Corrected 2026-08-09.** This page previously credited **"Ali Abdaal (Better
> Creating)"** and titled the video *"Building AI Specialists with Curated Knowledge
> Bases"*. Both were fabricated — Ali Abdaal is unconnected to this video. The real channel
> is **Systems Made Better**; the creator's business is *Better Creating*
> (bettercreating.com), which is likely what the earlier attribution confused. The stored
> transcript was also truncated to ~1,608 of 7,039 words and has been replaced with the
> full text below.
> [Source: yt-dlp-flow metadata + English captions, https://youtu.be/OAgU6sOmih0, 2026-08-09]

---

## Full Transcript

What if I told you you can take any book, any body of research, any expert's entire framework and turn it into an AI advisor that actually thinks only from that knowledge? Not a chatbot that makes things up, a specialist collaborator backed by sources you choose that can advise you on demand around your specific work and business. That's exactly what I'm about to show you how to build. We're going to do it in Notion, but you could use this for any AI system like Claude. Notion's just a really great visual way to demo it, and I thought it was about time we did. It's what I've built for my business in my updated personal agent OS, and it's helping me improve the quality of what I do and stay far more consistent.

A YouTube specialist who's absorbed every retention study I trust, a marketing expert built from an entire book. Each one has its own instructions, skills, and its own dedicated knowledge base, which is the heart of this video. And the only reason they're any good is because they're grounded in real curated knowledge, not generic AI training data. So, if you wanted to, by the end of this video, you could go away and have Alex Hormozi and Obama theoretically on your board of advisers. This is the bit that gets me excited for anyone running a lean team or solo business. You can build a specialist set of team members, marketing strategists, business consultants that support your in-person team around grounded frameworks you actually trust.

So, your business works harder without you and your team working harder. So, I'll build one from scratch, a marketing specialist. By the end, you'll have everything you need to know to build your own. And well, after last week's Claude video, which went rather viral on building a self-learning knowledge base, you should stick around cuz I'll show you how that feeds into this. Turn that knowledge base into one that self-improves. As we build, I'll use my meta agent, a prompt engineering specialist I've built, which is actually available in the description below, so you can download that and build with me.

Before I build anything, let me show you the shape of what we're going to make, because once you see it, it clicks. So, if you look at my Agent OS hub, you'll see I have instructions first, global instructions. In my instance, it's really an orchestration layer that picks specialist modes from a list. If we go back to the hub, what we're going to build together is essentially the specialist, and that's made up of three things. The agent instructions, these are my sub agents. As an example, we'll look at my meta agent that's going to help me build it.

We have the instructions. This is who it is, how it behaves, what its main mission is. Think of it as the job description you'd write for the new hire. And you'll see within it, it has its own source of truth, the knowledge base, which we're referencing within it. We'll come back to that in just one moment. We then have a set of skills.

Skills are reusable playbooks for processes and actions, step-by-step processes that an agent can follow. This can be anything from writing an executive summary for a meeting, super simple, or it could be something more complex, like a weekly inbox sweep, where it works through your entire inbox and gives you answers. The way you would set up a skill, let's take for example a consulting pitch drafting skill, is you can configure it to any page to be a skill. You can go into the top right corner, use with AI, and then click use a skill. You could also create one, which is as an AI meeting note instruction for your AI meeting notes. And this is basically the single page you pick to run your system.

That for me is my global instructions. And the best thing about it is with my agents up here, I can then link skills and relate them to agents, so they know which skills are primarily for them. And third, the most exciting bit that I want to demo to you today is creating a dedicated brain, the knowledge base. This is my online business marketing and knowledge base, and you can see it has a bunch of framework strategies, models written into it. This becomes a database of everything you want that agent to know, frameworks, principles, case studies, and examples. Most importantly, curated by you, and it's from sources that you trust.

I've got the AI to summarize the key insights of each entry. Most importantly, when these frameworks or ideas should be applied, and then my sources. You could, for example, make a single knowledge base based around someone like Olly Richards' incredible book on online business, and turn that book into a kind of digital version of that person to help you. I found this really interesting to engage with Olly's book, and then actually apply key principles. So, what I got my meta to do is build me summaries of key ideas from each chapter broken down by principle. And what's really cool is then in mind, I've then got it to link to other sources.

So, Daniel Priestley says something similar, so I've linked it to Daniel's ideas as well. That is the brain for your agent. This means that your agent will not give you generic AI advice, it's giving you grounded advice based on a body of work that you have curated. So, a skill is a clear process or set of actions that you define, whereas a knowledge base holds the principles and ideas that inform the agent's decision-making. Without the knowledge base, I found that the AI tends to just be still a bit generic, but with like a very clear process that it's following. So, this is why I've added this feature to my system.

And most importantly, because this is in Notion, it is kind of LLM agnostic. Notion AI runs on different models underneath, so you're not locked into one provider. So, you've been looking at my Agent OS Skills Hub, and it's built into Agent OS. You can download this. This is a multimodal personal agent system for Notion. You just hook it up to the personal agent on a business plan.

You set your global instructions, and it will select from those global instructions to pick specific specialist modes and answer you. It's amazing. So, if you do want to download this, it's available at bettercreating.com/agentos. I've just updated it with this new skills and knowledge hub system. So, existing users, it's free for you to update. Just go and re-download it from the marketplace, and you get all of these new updates.

Now, before we build, I think there's one more bit of learning around Notion that's worth you being aware of. These specialist assistants, these consultants, they don't replace real people, but they do help you if you know how to think iteratively and work with it. It helps you hold yourself to that knowledge and that understanding more closely. Therefore, it's also something you would only really want to use in chat. These are not for Notion's custom agents, which are these guys. And what a custom agent is, different to the personal agent, are things that can run for your whole team.

They do specific jobs like briefing or so and so forth. So, when I created a content strategist and a business marketing strategist, I realized that these were kind of not worth it. I may as well move them to trash because they cost credits, and when you're using credits, it's not worth it for this kind of interface. So, with that said, you can get these custom agents to go and look at these knowledge bases and these skills and use them. So, you do have that cross-agent functionality. For consultancy-type collaborations with AI, just stick to the personal agent interface.

Okay, it's time to go and build ourselves an agent with a knowledge base and some supporting skills. I could build it from scratch, but we're going to use my meta agent to help me do it from scratch because it's a much faster route. Inside Agent OS, there is this meta agent. I've also linked a free smaller version of it in the description below if you want it. You can just watch, but if you want to do this with me, you're going to want to download the free version of my meta agent or my full Agent OS and follow the setup guide first so that's set up. And what that basically means is in your chat window, you need to make sure that you have either the meta agent connected or the full global instructions for Agent OS.

But you need to have access to the meta agent instructions. That's what I'm going to do. I have models to build with. We've even got Kimmy and Deep Seek. Pretty cool, but I'm going to go for Opus 4.7, the most powerful option. And I'm going to start by talking to it.

I want to create a marketing strategist. The source material is going to be from a book that we'll ingest. Build me a knowledge base and a set of instructions using the your meta agent. If you're wondering, I'm using Whisper Flow, which is an AI interface. Far better than any inbuilt interface. I use it across all my devices.

It knows me. It knows my snippets. It's fantastic. Check it out. You'll see that we'll need for that knowledge base a topic, category, key insight, when to apply, confidence level, source. These are going to really be properties in the knowledge base, okay?

And what we're going to say to it is, "Let's make a plan for what that will be and you can decide in what order to do this work from the instructions through to the knowledge base." I'd also like to create a couple of specialist skills that this agent might be able to utilize as actions linked to these instructions. Great. So, let's send that off. So, you can see it's loaded the meta agent. It wants to build a marketing agent. We're actually getting an example of what an agent does when it reads its own knowledge base.

So, here we go. Before I start building, I want to lock in the plan with you. I've grounded this in the prompt engineering database. So, there you can see it's actually using its knowledge base. Uh if you're interested to know what that actually is, if we go back into here, our AI agent and prompt engineering database. And I actually built this from one key source, which is worth looking for.

It's the agentic design patterns uh document that you can find online and a bunch of other things. But, I worked through and added essentially every chapter and got it to draw out the key principles. It's seems like a huge amount of work, but you're getting your agent to do a lot of this input, okay? Now, what's really nice is cuz we're using Opus 4.7, Claude users will recognize this. It's the ask user question interface that's now turned up in Notion. So, let's just see what it said.

So, it said the proposed build, a focus advisor that helps you with marketing strategy frameworks. And by the way, it's saying real BC decisions. That's based on its wider context it knows of my business better creating. So, you can see that it's going to follow these key items. Two specialist skills recommendation below. Proposed order, scope and confirm, create knowledge base, write the specialization instructions, build the skills.

And do you want to start it from scratch or click the new knowledge base button? This is built into my system. Again, this is worth showing you. The reason it said that to me is the meta agent has said, "Do you want to click this button?" And here it is. This is the button. Just to create a new knowledge base that's already laid out.

It just solves some of the problems. What I did is build myself a button in Notion that creates a new knowledge base. And it adds all of the things that you you want to see in it. I'll click. Okay, so interestingly, it did select the book I wanted to use, which is I want to start with Seth Godin Godin's This is Marketing. I'm going to click next.

I'm actually doing a demo of how to create a marketing specialist. Could we consider doing this as a standalone version, not worrying about the other one, but keep in mind that I might want to integrate this one into the existing. Please give me your recommendations on if it's worth having this as a separate specialist agent or whether it will get confusing with my existing mode seven. So, let's share that. Which two specialist skills should the agent ship with? So, this is nice.

Normalizing stuff for an agent. We're going to give it a skill, which helps it ingest things. This is a really useful thing cuz it's about it's about what we're about to do. So, let's do that. And let's do a positioning audit. Nice.

Note that the positioning audit should also be based on anything we discover from the Seth Godin and can be updated. Add that to your plan. So, you can see we're explaining how to build it. The key is not to just let AI do it all. You need to take some control of taste and choice about how it works. It's asked my four questions.

Now it's consulting its own knowledge base on good prompt engineering. And here we go. Good answers. So, it's going to say, "Build it as a standalone. It will not get confusing if we set the boundaries correctly." Great. So, seven is an online business and marketing strategy.

It's broader operator covering execution, funnels, launches, pricing. The marketing strategy specialist, sourced from one book, is a deep advisory lens. Great. You're going with the user-led knowledge base creation. Right, so let's add the knowledge base. So, we're going to go back to the agent thing and click the button.

You could of course get it to build you this. A Notion agent has all the tools that anyone would have in Notion, so you can just ask it to to it. And I'm just going to click the link. I'm do going to do command L to copy the link to that page and then go back and say, "Command V." This is the new knowledge base template. Please build out what you need, rename it, and design it around our plan. So, it's going to work through these five steps.

Excellent. While it does that, you'll notice that we have this option for categories. Now, categories let the agent search by area. So, pricing, positioning, audience. We've got confidence. This means it can prioritize proven stuff over untested ideas.

So, if you're adding new material in, that will go in as low until something is validated, right? Let's see what it's up to. Okay. So, it has built and renamed the marketing strategy knowledge base. There you go. We have these elements in it.

Excellent. It's added kind of key ideas, which is cool. We've got the content type. Excellent. So, this is the model to build from, and this is all listed in my meta agent, essentially. We've got views.

So, if we can go and have a look at it, there it is. We go in. We've got by category, by confidence, boards, entries. Fantastic. Like, I mean, that's that's really excellent. It's all built and ready to go.

So, love that. Draft the marketing instructions. Excellent. So, that's what we're going to do next. Great. Go ahead and build a new sub agent instruction.

You're right to put that in the database and make sure that the knowledge base we've created is directly referenced as a linked view early on, ensuring that that is a mandatory step before it answers anything. Off it goes. Now, what I mean by that mandatory step is if we look at my like online business marketing coach, it's got this knowledge base saying you have to read this before you do anything. We want to make sure that's really clear. So, it literally gets told, "This is your purpose and your North Star." And this is your knowledge base. Okay, so that's what we want to ensure this one has.

So, you can see it's reviewing, it's loading stuff, and it's starting to work out boundaries for handing off to my other mode. It's thinking all this stuff through. So, it's basically writing the job description for this agent, this colleague, a training manual on one page. Who the agent is, where it looks for answers, what standards to follow. It's also, you can see here, laying out the positioning audit skill. Quick note, remember that the instructions should be a guide of how it works and its North Star focus.

Remember that we'll need to build out the knowledge base to give the content and focus of how it can do things. The same with the positioning skill. Let's write one, but make a note that we're going to need to update this once we have more information ingested. So, this is something you can do. You got to be careful. You can like kind of add little in instructions.

I find this is helpful cuz it can interrupt and add the information, but you got to be careful cuz sometimes it can kind of mess things up and it can get lost in its process or you can overload the context window, probably. So, just be careful in Notion not to overdo it. So, there is our marketing strategy specialist. If we go and take a look, overview, it's basing it on the existing versions. Run the knowledge base entry gate. Fantastic.

It's now attaching the linked knowledge base view into that view. Routing versus mode seven. Excellent. Specialist skills, working method, classify, run this, invoke the skill, apply, validate, anti-drift protocol. This is all based on my meta agent's instructions. These are all good practices for writing agent instructions, how it works, how to avoid it drifting, what is a success, and then it's got memory live notes.

Live marketing strategy, read me before answering. Great, it's going to drop that in. So, let's now just go back to our conversation. Skills written by AI often have problems. You need to make sure that you're really clear about how you want it to work. So, skills and instructions, that's where you should review what it's written and you'd be amazed how quickly you learn it.

Please, could you now review the instructions for token efficiency and see if you can find any improvements that can be made for keeping the quality of what we've got, ensuring the steps are followed, but reducing the amount of content on the instruction page. So, this is a task that our meta agent has, our template for this, and I basically ask it to improve token efficiency, which means less to read, more clarity in the instructions. So, let's send that off, and we should see this now improve. But, yeah, we have our uh marketing strategy specialist advisor ready to rock. While it's doing that, let's check out the skills it's created. We have the book ingestion helper.

Let's open this up, and it has here, goes through it, extract, atomize, normalize into knowledge base entries. So, the next step is going to be to ingest content into the knowledge base. And to do that, you're going to want to feed in book content, and then have it on each section extract all the information from within it, atomize, so go, "What are the key concepts to take out?" This is mode 10 splitting logic, and then normalize into knowledge base entries. Okay? So, we can then have that listed in, and this is the kind of view of what it should be. Quality gate, so on and so forth.

And what I'm going to do on this, actually, is quickly just start in a new chat, just go into here, and just say, "Please, can you adapt this skill so that it will work for any knowledge base ingesting books? Consider how it aligns next to and whether it's actually redundant or the two should be combined." This skill was built for a specific marketing knowledge base, but really we need a skill that works across multiple systems. All right, so we'll leave that doing that. Let's go back and see what's going on here. So, it's done a review. It's slimmed them down, 55% shorter.

Opening callout is now clear. Entry gate is clear. Scope, self, anti-drift, kept compressed bullets. Excellent. So, it just all is now a little bit more contained, boundaries and handoffs, routing rules, anti-drift. It's all much better.

Great. Okay, so I'm really happy with my marketing instructions now. Excellent. So, it's cleaned these up, made them generic. One thing I've noticed in inputs required on target knowledge base, can you make this more of a generic instruction since I may add more over time and so this would become stale. And what you can do is if you highlight something in Notion, it will see that you've highlighted it here.

So, we're just updating now the skill. So, let's just take a little step back and see where we are. It's built these elements, the skills, the mode, the knowledge base. Now, what's missing is linking it to my global instructions so that it can be called upon and information into the agent. Right, that's kind of it. So, we're pretty close.

So, what that means in practice is if we go to my hub, we have all of our agents written in here now, but it's not referenced in my main global instructions. So, in Agent OS, what you have is a global instruction page and the kind of orchestration layer. We pick a mode and it needs to be listed in this view. And so, I actually just get it to write them. So, it's easy. We just ask it to do it.

Please use the model on the global instructions page and add the mode 7B entry. And then we're going to start ingesting information into it. We've cleaned this up, so it's now target database is clear. Okay, so let's take a look at where we are. Here we are on the home page. We now have our knowledge base ready to be seeded, our sub agent created with specialist instructions that were created with the help of our meta agent with its own instructions.

Next, we created a couple of additional skills and I believe positioning audit system. So, we can now check that one as well. That's pretty tight. I'm pretty happy with that. That doesn't need adjusting at the moment and we're going to using and refining and the same with this guy. Let's go using and refining.

So, I have a little status thing for them. Let's make this one active. And now in our global instructions, we should see that it is added mode 7B, the marketing strategist specialist advisor. It says what it does, when to pick it, do not pick when doing these things, and always operate in line with these details. Excellent. Now, we need to ingest some information.

Actually, it recommends a live test. So, let's do that. How should I position the Agent OS for solo founders? Nice idea. Let's do that. So, if I was to move to a new chat, can you save this conversation as a chat history entry in the chat history database referencing your global instructions, and then give me a prompt to move on to a new chat window referencing that chat history page you create?

So, I've built something called chat history for my Agent OS, and it's a way, cuz Notion doesn't really support it yet, of adding specific entries that I want the AI to remember over different sessions, and it just creates a really brilliant way to keep memory and context updated, but I need to do more work on memory and I'm going to be looking at how to do that um in a future video. So, get subscribed. Let's test it. We'll set this into say Opus. So, what we should see happen, if it's working, is it should A, load mode 7B, and then B, go there is no information in my knowledge base. I can't answer.

That's what it told me it should be doing. Good, it's picked the right mode. Viewing the database, great, it's following the process. Low confidence. Excellent, I've searched it, there's nothing in there. I don't think I can help you.

There is proof why this system is so powerful. I'd recommend running this ingestion helper and adding the information. However, here are my opinions on the positioning nonetheless. Great, medium grounded on real customer data, but not on your information. Excellent, that's really good. That's exactly what we want to see.

Let's go back to our specialist, which is now dropped everything into the chat history, and then this is what it wants us to continue with. Excellent, so we're going to copy that and we can start again. Okay. Let's now do the ingest of information and I'll show you how that works. Right, so my plan now is to ingest this book as a demo. This is a PDF online version of Seth Godin's This is Marketing, which I'm going to use to do that.

So, this is the instructions that it gave me previously to paste in to restart. I'm going to paste that in, but something we have already done here is we've actually run the live test and we've actually done that. So, let's put it into We've got 4.8 is now here. Why not run that? Let's see what happens. So, you can see I'm referencing back to my chat history page, which is here in the chat history.

That's part of my Agent OS system. And we're going to have a go ingesting this book and I'll show you how this works. So, let's go. I've found that you probably do want to use quite a solid model here. What I'm loving about Notion's personal agent is that you do get really good access to the Claude models. It's not so credit based because you're paying a business plan on what you get.

I think they may like if you use it a lot slow it down, but I found this to be very good. But Notion is a very affordable way to use LLMs to ingest data. This is quite hungry on using tokens. But this does seem to be very good cuz it's all included in the plan. So, I'm really enjoying that at the moment. Right, so it's in this mode, paste chapter one text.

Now, I think there's a really good approach to this. I'm going to say this. First of all, here is a chapter list. Please make yourself a brief plan that you can refer to of all the chapters in the book, which is what we will work through in order together drawing out the key frameworks and atomized value points that could be applied to a useful assistant for this mode that we're going to seed. And we'll paste the chapters in and I'm just pasting it in like loosely off I've copied it off the PDF. Here we go.

Great, so it's creating a structured reference guide that maps out the chapters so we can extract them in mode 7B. It's already linking potential categories and it's got its candidates. Excellent. So, what I'm actually going to do is an example of feedback that you can do in this process. This is great. Before we now begin the ingest, please update your instructions thoughtfully and without creating too much token bloat to make sure that this is suggested as an option within the book ingest skill.

I think it's good practice that you would always go is there a chapter list I can use first as a guiding structure. So, part of good prompt engineering like this is just thinking logically as a leader. Essentially, it's going, "Oh great, you didn't know about that. So, before I continue, I'll make sure that you update your instructions so that you do remember that in future." And that's better in the underlying instruction that we'll always use to do this process. This is how you improve and iterate skills over time. So, what I'm going to do is get the first chapter and literally what I'll do, find the chapter and just take the introduction and chapter 1 and I'll just literally go through.

Now, you can do this by giving a PDF to Notion, but I find that AI struggles with PDFs any longer than say 15 pages. And honestly, just pasting the content in is so much better. So, I'm going to go through and do the first three chapters as a little example for you. Okay, here's the intro and the first three chapters for you to work through. You need to be careful not to paste too much cuz there probably is a limit on the window. I want to check that it's got through to the end.

Yeah, that looks great. And now we'll see the process of what an ingest looks like. I'm not sure, I think I might have actually gone all the way through to chapter 4. I've confused it. Now, I'm using Claude in Notion here and for me, it's a brilliant model. It's just the best at most things for what I do, particularly as a knowledge worker.

I really like watching how it thinks and reasons and when you do that, you can then kind of assess if you need to update your prompting or improve it to keep it focused on the right things. What's great is it's using like things like understanding how to use headings three. This is all why I like using Claude directly in the Notion interface for certain jobs like this. You're not using an MCP to come in from Claude co-work or Claude code and it's already trained on how to use Notion because you're using it within the Notion window. This is why I think a lot of people will really benefit from having a dual approach, local with Claude code in my co-worker OS, and then in Notion using something like this Agent OS. Anyway, let me know again in the comments what you make of that.

This is a great example of our system in action. It's selected the correct mode. It's followed its own instructions, and then it's loaded a skill we've created. Look at that. It's creating all of those pages. Let's go and take a look at them.

Here they all are, and we have all of these items pre-filled, right? So, principles, case study, frameworks, principle principle framework, who's it for, what's it for, vision. I mean, all stuff that I would not have read. Let's take a little look at the first principle, the myth of rational choice. And it has these kind of when to apply it, and it's laying out what it is, why it works, how to apply it, examples. So, this is the joy, right?

What it's doing is atomizing. It's taking the key ideas in the book and making them very easy to read for an AI agent. Unbelievably cool. So, look at that. Loads of stuff. Now, of course, you would now just work through and let it run, you know, and and do all of the chapters you need to handle, which is great.

Let's hold it for the next session, and I'm going to just give this a uh little test as as it stands. Great. Please log this to the chat history, and create me a prompt for picking back up, as well as a prompt to test the knowledge base and its related instructions as it currently stands, so I can demo it to my audience. Okay, cool. So, it's done it. I think the demo prompt is a little bit leading, so we won't worry about that, but we have this ready to go.

Let's now do a new window and test it out. Going with full Opus 4.8, although remember you could pick any model you like. You go into Gemini and ask it, and it would use the same instructions. But, let's use Opus cuz I really like it. I'm planning on releasing a business OS for non-technical founders, entrepreneurs, creators who work with teams to organize their information and make a workspace that's agentic, forward, focused on using AI intentionally. How should I position this when I market it?

Interestingly, you could do use plan mode, which is cool, or we could just do a normal request. We can add sources, we can do various other things in here, but I'm just going to leave it like that, and we should see it bring up the marketing specialist. Let's see. Look at this. It's loaded my who am I page, a good trick, gives context, my voice profile, and the correct advisor. This is a specialist, not a chatbot giving you the same generic advice it gives everyone else.

A specialist that knows your chosen frameworks and follows your rules, and it gets better every time you refine that knowledge base or add a new skill. Okay, it's read those key references, and here we go. And why don't we use my favorite tool to get this read back to us, Speechify. Everyone is not your customer. Seth Godin. This is marketing the question restated.

How do you position a non-technical AI forward business OS so the right people instantly get who it's for and why it matters? This does genuinely feel like I've asked Seth Godin how to approach marketing it. What I love about this is it's not just based on the knowledge base, it's also based on a wider understanding of my business. It's clearly looked at my context. I mean, look, this isn't going to replace working with people, but what it does do is it builds real clarity of thinking into how you're doing things. Like, this is totally fantastic.

I love this as well. Position against AI productivity, not within it for my business OS. It's crowded, do more faster, yours is less but better and it's a different and it's a differentiator. And that is true. So, if you're interested in the idea of a just this, a Notion business OS template that would integrate with Agent OS and all of this and be a place to work, I'm working on it right now. We've almost finished it.

So, make sure you get in the description below, grab the free guide to my agentic business transformation and fill out the form and you'll hear more about this very soon when it's available and ready to go. But, uh yeah, thanks Seth Godin for helping me do this. Okay, so this knowledge base we built is static right now. It's amazing. It's got all of this information and the agent can find them and use them. You add entries, done.

But, what if it could grow every time you use it? And what if it could research for itself? Well, you could create a compounding loop. Essentially, what you create is a health check. I'm going to demo that really quickly, but here you can see the concept of how this works. You ingest information into a place and then you get a compounding loop to happen by asking the agent to review the content in the knowledge base, look for gaps, and then go out and research from reputable sources what other entries might be that you could add.

Now, it might not be true if you just want this to be the knowledge base of a single book that you need to use this. But, by doing this, you can create something that automatically improves itself. So, the way I would go about this is actually create a custom agent. What we could do is do this. New agent, I'd like you to create a system where you review a specific knowledge base on a schedule each week. And in doing so, you look for gaps in the knowledge base and where it could be improved, and then go out and suggest new entries that could be made based on deep research in the field from only reputable sources.

Let's make this agent be a specific agent for automatic knowledge research for this database. And then we'll put the marketing strategy database. So, a custom agent is slightly different to a personal agent instruction in that it is going to run automatically on a trigger. So, you can add triggers, you can add tools that it can call upon, and you can do various, you know, things like setting a mode. Now, the problem with this is it will cost credits. You can set a limit now for what these are, and you can view a kind of a graph of its progress as it works through it.

What it's going to be really brilliant at doing is automating the process of improving that knowledge base. Let's open up the instructions it's creating. You are an automatic knowledge base agent for marketing strategy knowledge base database. Each week, review gaps, redundancy, areas needing cleaning, when to apply triggers. Propose new high-quality entries backed by reputable sources only. Where appropriate, add suggested entries to the database in a structured, consistent way.

So, you could say that this has to be approved, or you could let it do it. It will scope the knowledge base, look through it. Now, of course, you would want to refine this, but this is properly cool, right? This could be a really fantastic system. And it's the kind of equivalent to what we've done over in Claude Caework with my self-improving knowledge base. So, check out that video after this.

I won't demo it now, but this is a really interesting concept for you to consider. Let me know in the comments what you make of it. Now, with that said, a lot of us won't want to be spending credits like this. So, I'm just going to save that without a trigger and turn it off so that I don't have to pay money on it. You can watch some of my other videos on the channel if you want to learn about how to create custom agents. There's a full guide.

The other option, of course, would be to keep it much simpler than that. Go and make yourself a skill that does exactly that, and then you can just trigger it with personal agent once a month, run this skill. That is how I would recommend you approach this cuz it's a hell of a lot cheaper. And you would make that skill say something like review the knowledge base, flag anything outdated, suggest three new entries based on the gaps, and it will get sharper every cycle. You can also make it update the skill each time you do it. So, instructions, skills, knowledge base.

Now, I've been running these two in my personal system for years now, and they're amazing. My favorite has got to be my content strategist and YouTube expert. It's changed how I plan absolutely every video. I mean, check this out. It's helping me design thumbnails. It's helping me write YouTube descriptions.

It's helping me work out packaging with thumbnails and titles, all based around the skills tightening and polishing this massive knowledge base of sticky scripting and niche focus ideas. It's like it's totally brilliant. So, if you build yourself the right system, it's really powerful. Let me know if you would value something like this in the comments, and maybe I'll release the kind of YouTube specialist at some point, but it's really cool. And if you're running a small team or a solo business, something like an online business and marketing strategist that I showed you earlier is just incredible for helping you scale and think without the head count. It's a big, big difference.

So, if you're interested in the principles of applying this stuff, go and check out Agent OS, newly updated as of this week with these new database systems. You don't get that YouTube specialist in it. I will say that. But what you do get included is pretty cool. A productivity coach, a decision maker, a vision and goal setting coach. And there is actually I I'll take that back.

There is a kind of content writing and social media agent as well as that meta agent to build your own or get you started. Link in the description. I hope you enjoy it. Now, as of right now, in just a few months, this new channel has hit 20,000 subscribers. Thank you so much for doing that. If you haven't subscribed, make sure you do it below.

And a lot of you have been asking how am I using Notion and Claude together? When should we use which? Well, you should probably watch this video next for my system of using the two. And there will be loads more on the channel as these tools develop over time. See you. Bye.
---

[Source: YouTube auto-generated captions, https://youtu.be/OAgU6sOmih0, retrieved 2026-08-09 via yt-dlp-flow]

## See also

- Analysis: [[projects/invisico/market-research]]
