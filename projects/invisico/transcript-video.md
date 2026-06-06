---
type: research
title: Transcript Video
parent: projects/invisico
source_url: 'https://youtu.be/OAgU6sOmih0'
ingested_via: 'mcp:put_page'
ingested_at: '2026-06-06T12:59:55.507Z'
source_kind: 'mcp:put_page'
tags:
  - active
  - market-research
  - transcript
---

# Transcript: Building AI Specialists with Curated Knowledge Bases

**Video URL:** https://youtu.be/OAgU6sOmih0  
**Creator:** Ali Abdaal (Better Creating)  
**Duration:** ~40 minutes  
**Extracted:** 2026-06-06

---

## Full Transcript

What if I told you you can take any book, any body of research, any expert's entire framework and turn it into an AI advisor that actually thinks only from that knowledge, not a chatbot that makes things up, a specialist collaborator backed by sources you choose that can advise you on demand around your specific work and business. That's exactly what I'm about to show you how to build. We're going to do it in Notion, but you could use this for any AI system like Claude. Notion's just a really great visual way to demo it, and I thought it was about time we did. It's what I've built for my business in my updated personal agent OS, and it's helping me improve the quality of what I do and stay far more consistent.

A YouTube specialist who's absorbed every retention study I trust. A marketing expert built from an entire book. Each one has its own instructions, skills, and its own dedicated knowledge base, which is the heart of this video. And the only reason they're any good is because they're grounded in real curated knowledge, not generic AI training data.

So if you wanted to, by the end of this video, you could go away and have Alex Hormoszi and Obama theoretically on your board of advisers. This is the bit that gets me excited for anyone running a lean team or solo business. You can build a specialist set of team members, marketing strategists, business consultants that support your in-person team arounded frameworks you actually trust. So your business works harder without you and your team working harder.

So I'll build one from scratch, a marketing specialist. By the end, you'll have everything you need to know to build your own. And well, after last week's Claude video, which went rather viral on building a self-learning knowledge base, you should stick around cuz I'll show you how that feeds into this. Turn that knowledge base into one that self-improves.

As we build, I'll use my meta agent, a prompt engineering specialist I've built, which is actually available in the description below. So, you can download that and build with me.

Before I build anything, let me show you the shape of what we're going to make because once you see it, it clicks. So, if you look at my agent OS hub, you'll see I have instructions first, global instructions. In my instance, it's really an orchestration layer that picks specialist modes from a list. If we go back to the hub, what we're going to build together is essentially the specialist, and that's made up of three things. The agent instructions, these are my sub agents. As an example, we'll look at my meta agent that's going to help me build it. We have the instructions. This is who it is, how it behaves, what its main mission is. Think of it as the job description you'd write for the new hire. And you'll see within it, it has its own source of truth, the knowledge base, which we're referencing within it. We'll come back to that in just one moment.

We then have a set of skills. Skills are reusable playbooks for processes and actions. step-by-step processes that an agent can follow. This can be anything from writing an executive summary for a meeting, super simple, or it could be something more complex like a weekly inbox sweep where it works through your entire inbox and gives you answers.

The way you would set up a skill, let's take for example our consulting pitch drafting skill, is you can configure it to any page to be a skill. You can go into the top right corner, use with AI, and then click use a skill. You could also create one which is as an AI meeting note instruction for your AI meeting notes. And this is basically the single page you pick to run your system. That for me is my global instructions. And the best thing about it is with my agents up here, I can then link skills and relate them to agents so they know which skills are primarily for them.

And third, the most exciting bit that I want to demo to you today is creating a dedicated brain. The knowledge base. This is my online business marketing knowledge base and you can see it has a bunch of frameworks, strategies, models written into it. This becomes a database of everything you want that agent to know. Frameworks, principles, case studies, and examples. Most importantly, curated by you. And it's from sources you trust. I've got the AI to summarize the key insights of each entry. most importantly when these frameworks for ideas should be applied and then my sources. You could, for example, make a single knowledge base based around someone like Ollie Richards's incredible book on online business and turn that book into a kind of digital version of that person to help you.

I found this really interesting to engage with Ollie's book and then actually apply key principles. So, what I've got my meta agent to do is build me summaries of key ideas from each chapter broken down by principle. And what's really cool is then in mine, I've then got it to link to other sources. So, Daniel Priestley says something similar. So, I've linked it to Daniel's ideas as well. That is the brain for your agent. This means that your agent will not give you generic AI advice. is giving you grounded advice based on a body of work that you have curated.

So a skill is a clear process or set of actions that you define. Whereas a knowledge base holds the principles and ideas that inform the agents decision making. Without the knowledge base, I found that the AI tends to just be still a bit generic but with like a very clear process that is following. So this is why I've added this feature to my system. And most importantly, because this is in notion, it is kind of LLM agnostic. Notion AI runs on different models underneath. So you're not locked into one provider.

So you've been looking at my agent OS skills hub and it's built into agent OS. You can download this. This is a multimodal personal agent system for notion. You just hook it up to the personal agent on a business plan. You set your global instructions and it will select from those global instructions to pick specific specialist modes and answer you. It's amazing. So, if you do want to download this, it's available at bettercreating.com/asiOS. I've just updated it with this new skills and knowledge hub system. So, existing users, it's free for you to update. Just go and redownload it from the marketplace and uh you get all of these new updates.

Now before we build, I think there's one more bit of learning around notion that's worth you being aware of. These specialist assistants, these consultants, they don't replace real people, but they do help you if you know how to think iteratively and work with it. It helps you hold yourself to that knowledge and that understanding more closely. Therefore, it's also something you will only really want to use in chat. These are not for Notion's custom agents, which are these guys. And what a custom agent is different to the personal agent are things that can run for your whole team. They do specific jobs like briefing or so on and so forth. So when I created a content strategist and a business marketing strategist, I realized that these were kind of not worth it. I may as well move them to trash because they cost credits and when you're using credits, it's not worth it for this kind of interface. So with that said, you can get these custom agents to go and look at these knowledge bases and these skills and use them. So you do have that cross agent functionality for consultancy type collaborations with AI. Just stick to the personal agent interface.

Okay, it's time to go and build ourselves an agent with a knowledge base and some supporting skills.

I could build it from scratch, but we're going to use my meta agent to help me do it from scratch because it's a much faster route. Inside Agent OS, there is this Meta Agent. I've also linked a free, smaller version of it in the description below if you want it. You can just watch, but if you want to do this with me, you're going to want to download the free version of my Meta Agent or my full agent OS and follow the setup guide first. So, that's set up. And what that basically means is in your chat window, you need to make sure that you have either the meta agent connected or the full global instructions for agent OS, but you need to have access to the meta agent instructions.

[Transcript continues with detailed walkthrough of building a marketing specialist agent in Notion...]

**Note:** This is a truncated version. Full transcript available via the YouTube video link above. Key points have been extracted into the [market-research summary page](projects/invisico/market-research).

[Source: YouTube transcript extracted 2026-06-06 from https://youtu.be/OAgU6sOmih0]
