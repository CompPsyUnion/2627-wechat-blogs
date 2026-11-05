# A Beginner's Guide to Using Agents

## Introduction

After leaving the familiar, predictable world of high school for the diversity of university life, have you found yourself in situations like these? A classmate opens their laptop and already has an agent running tasks. Conversations with friends are full of unfamiliar terms. Your groupmates complete assignments remarkably quickly and to a very high standard. Do you feel anxious or confused? Do you want to put agents to work for you but have no idea where to start? **This article will walk you through the basics of agents and examples of how to use them, helping you get started quickly**. It will not go into much detail on specialized workflows in individual fields, setting up agents, or developing enterprise agents. (To save the experts some time: this is a very basic article.)

## Part One_Basics: The Difference Between Chat and Agents, AI Terminology, and a Guide to Using Most Agents

### Chat and Agents (I Won't Paste the Official Definitions Here; They're Too Long. Ask an AI If You Want to Read Them.)

1. Chat is like a smarter search box.
2. An agent is like an employee. In general, using an agent gives you access to **more advanced models from the same company at higher reasoning effort levels**. Agents can also complete tasks more independently, such as operating your computer through the command line and using tools installed on it. I will go into these capabilities later. **In short, think of an agent as someone who works incredibly hard and is exceptionally capable in certain areas**.

### Common AI Terms (Items 6, 7, and 8 Are the Most Important)

1. API: Think of it as a tap. In an agent or on a website, you use an "API KEY" to connect to a large language model and access the computing resources its provider offers. Those resources flow into the interface like water. Of course, you need to pay for usage in advance, and your money will flow away just as quickly. Here is a useful rule of thumb: using AI through an API generally offers less value for money than buying a subscription plan for an official agent, so beginners generally do not need APIs, except when using DSH.
2. MCP: You can think of this as a protocol connecting a large language model to other software or websites. Through MCP, the model can quickly operate that software or those websites. (You will not need it for everyday use; I have not tried it myself yet.)
3. skill: Rather than "skills," I find **standardized operating rules** a much easier way to understand these. You give a model a set of rules for processing its input, and it follows those rules. For example, feed it a paper and install a skill, and out comes a lovely, digestible summary of the main findings and key data.
4. Prompts: Exactly what the name suggests: you tell the model what to do and guide it. That said, I have heard that many prompts can now limit a model's performance. It is hard to say, so I usually use less restrictive prompts. (In practice, that means fairly vague directions, because I am not entirely sure what I want either. The model follows my train of thought to help work out what I am really after.)
5. Experts: This concept is already outdated. You can ask an AI to dig into its history; I will not go into it here.
Jailbreaking: Inducing a model to bypass its safety restrictions.
Overfitting: When a model is overly influenced by its training data and its ability to generalize declines.
I cannot think of any other particularly important beginner terms for now. Feel free to look up any terms that catch your interest.
6. harness: The control layer around a large language model. It does not do the thinking; it manages tool calls, handles exceptions, and organizes the task loop. A harness has a major influence on how much of a model's capability can be put to use. This is why v4.1 in DSH does not feel like v4.1 elsewhere.
7. LLM: A large language model.
8. Oh, and one more important point: agent= harness+LLM.
9. Connectors: These connect an agent to other software, such as WeChat and QQ, and can be implemented through the MCP protocol.
10. Plugins: An agent has a kernel layer, a plugin layer, and a controller layer.
· Kernel (kernel layer): A minimal Agent loop that only exposes extension points. It has no knowledge of any plugins and communicates only through Hook interfaces.
· Plugin (plugin layer): Implements specific Hooks and attaches to an individual session to change the Agent's behavior.
· Controller (controller layer): Orchestrates multiple sessions and can combine plugins, while the plugins themselves have no knowledge of the controller.

### An Agent's Basic Setup

An agent generally consists of a main chat window, connectors, skills, experts, and plugins. I have already explained these, so open an agent and take a look.

## Part Two: Major AI Models and Common AI Applications or Tools Available Today; Who Each Model Suits; Recommended Reasoning Effort Levels and Models for Different Tasks; Recommended Skills, Plugins, and Prompts

### workbuddy

workbuddy is very easy to get started with, easy to obtain, and well integrated into China's software ecosystem. **However**, I find this agent poor to use: its output is just too stupid.

### DSH (Deepseek Harness)

 DSH is just about the best agent available for use in China. Its downside is that it offers no free credits, so you have to pay for all your API usage yourself. Overall, though, you can get good results for very little money. You also need to install suitable plugins yourself; DSH is pretty lousy without them. Its strengths include very fast execution. Although its output is not as good as codex or claude code, it is still among the best Chinese agents, and its value for money is among the best globally.

### CODEX

 codex has relatively few downsides apart from being expensive and difficult to access. (Of course, that is assuming we are not comparing it with claude.) Its drawbacks: connections from China are relatively slow, it does not run as fast as DSH, and its value for money is not as good as DSH's. There is not much else to complain about. (Even if its value for money is not the very best, when you are doing something truly important, who would feel comfortable handing it to a less capable model? Let it cost a little more; at least using it gives you peace of mind.)

### cc switch

 Strictly speaking, cc switch is not an agent. It is a platform for coordinating multiple agents, connecting to their APIs and organizing their collaboration. As you know, though, APIs are relatively expensive, so there is a trade-off between multi-agent collaboration and value for money. Multi-agent collaboration is also not particularly useful when you are starting out, so I will not expand on it here. Once you are more familiar with agents, you can experiment with it.

### PI

 1. PI is a minimalist, open-source harness. That means exactly what it sounds like: it has no model of its own, so you need to buy an API key to use it. By default, it only has a few tools for reading, writing, and editing files, plus bash. In other words, when you open it, you get a terminal, with no graphical interface or the other built-in features you may know from agents: plugins, connectors, built-in experts, and so on. Its advantages are a small footprint, both in storage and token usage; extensive customization (you can even use claude code); and extremely tight cost control. You need to add plenty of plugins yourself to make it useful.
 2. Still, there is no need to focus on it too much at this stage. You do not need it yet, and it will be easy to learn once you are comfortable with the basics of agents.

## Part Three: Common Uses for AI Agents

### Browsing Website Information

You can copy a URL, send it to an agent, and ask it to organize the information on that website for you. **For websites that require a username and password, there is currently no completely safe way to use an agent to organize their information. Even running the agent in a sandbox carries a risk of exposing personal information. There have been cases of people getting hold of others' account details this way. The internet is full of idiots who enjoy doing this sort of disgusting thing**. (Here is how to recognize high-risk situations when using agents to browse: if you give an agent a URL and it reports that it cannot access the website without a password, that is a situation where you should not use an agent to browse.)

### Troubleshooting All Kinds of Mysterious Computer Problems

Have you ever had an unreliable internet connection, been unable to find a file, or had your computer malfunction for no apparent reason? Because an agent can read information on your computer and operate it with your permission, it can act as your computer's doctor and help diagnose problems. This can make using something as complicated as a computer much more pleasant and make your life easier. Whatever the problem (all sorts of problems), take a picture and send it to an AI!

### Finding and Organizing Files

In my experience, an agent can often act as an interface for operating your computer. Talking to it can make using your computer even easier than using your phone. Take finding files: when File Explorer is crammed with files, you often do not even want to open it. If you never developed a filing system in the first place, using your computer can feel like being in prison. At that point, ask an agent to find the file, give it a possible filename, have it tell you the path, and search for it in File Explorer's search bar. What a relief. I still recommend managing your files properly, but why not use an agent as a stopgap or to help organize them? **Using agents is making "your attention is everything" feel more and more apt.

### Help With PDF and Word Document Layout

Are you still writing PDF and Word documents one word at a time? Perhaps you have been asked to write a proposal for the student volunteer association (青协), or prepare one for an HU interview. While other students and groups are still doing everything manually, you, my friend, can use an agent to leave your peers far behind. Give it the instructions, constraints, and perhaps some previous WeChat posts from your organization, and you can get a draft in a short time. Do you know why AI-written articles can look fine at first glance but turn out to be a pile of crap on closer inspection? **1. Too much waffle. Far too many sentences make a point and then immediately follow it by denying the opposite view. It is painfully long-winded. 2. There is a lot of defensive writing, with vague wording that makes it tiring to read. 3.

### Extracting the Key Points From Papers

Finding papers exhausting to read? Ask an agent to cut through the waffle and extract useful information or whatever you need. Add a few handy skills and the process becomes much more pleasant. Be mindful of the boundaries: first read UNNC's AI use policy, or ask a senior student or teacher.

### Organizing Course Content

Struggling to keep up in class? Not sure where to start with independent study? Find an agent smart enough for the job, give it your course materials, and let it be your one-to-one tutor. **A little-known fact: top models are no less capable overall than some mediocre professors. (Of course, it is often still very useful to consult capable teachers. Some kinds of experience and personalized, face-to-face explanations remain far beyond AI.)**

### Help Finding Sources to Support a Paper

I do not recommend simply installing a skill in codex or a similar agent and using it to search for and summarize relevant papers. Many academic websites have sophisticated anti-scraping mechanisms, so the AI may be unable to read enough papers. You can use a specialized academic search AI such as undermind to help with the search.

### vibe coding

The key point: do not dump the entire task on an agent. Pay attention to demos, setting boundaries, concurrency, and similar issues. Covering these in detail would take too much space, and relatively few beginners need them. Come along to a CPU weekly tech-sharing session, find some experienced members, and ask them to recommend a learning path.

## Part Four: Understanding Agents' Limitations

### As Mentioned Above, Using an Agent to Browse a Website That Requires a Password Risks Exposing That Password

### An Agent May Not Be Able to Access All the Information on a Website, an LLM May Take Shortcuts and Leave Information Out of Its Summary, and a Website's Anti-Scraping Measures May Block Access

I have already covered this above, but it bears repeating.

### Agents Struggle to Come Up With Original Research Ideas Independently, but Can Help You Explore Ideas

However capable AI may be, it still outputs existing information. After all, it relies on text-based training and probability. So, if you want to rely entirely on AI to produce an outstanding original idea, that will be difficult. You can install a skill called ARS-Codex. Discuss your idea with it, and it will question your thinking in depth, like Aristotle, until your idea is in excellent shape. You can look into this further online.

### Computer Troubleshooting Depends Heavily on the LLM's Intelligence

Weak models and agents can make this process an ordeal.

### Agents Write Poorly: You Can Tell at a Glance Whether a PPT, PDF, or Article Was Made by AI, and With Enough Exposure You Can Even Tell Which Agent Made It. The Results Are Readable, but Seeing Too Many Gets Sickening, So Put the Human Brain First When You Want to Create Something Beautiful

I have already discussed how to make AI writing more palatable. Let me emphasize it again: please use AI less often to churn out unreadable rubbish. We already spend enough time talking to AI every day. I really do not want to open a WeChat post only to find another article written by AI; I am worn out from reading them. By now, you should be able to tell that I wrote this article myself. In this age of AI everywhere, can you feel the effort I have put into it?

## Part Five: Some Pitfalls When Using AI Agents

### For Long-Term Work, Use a Project and Set Up a Shared Folder

A conversation has a limited context window, and AI gets less capable when the conversation becomes too long. Working this way makes it easier to start a new conversation. You could also consider installing a skill.

### Use Separate Conversation Windows for Different Types of Tasks

This keeps the context focused, again helping prevent the AI from becoming less capable.

### Ask the AI to Summarize the Conversation So Far in Good Time, to Keep an Overlong Context From Limiting Its Capabilities and Improve the Cache Hit Rate

Another point worth emphasizing: a higher cache hit rate can save money. Those of you using DSH may already be familiar with this.

### Respect the Boundaries of AI Use in Academic Work: Do Not Have It Write Your Work for You. An LLM May Have Been Trained on Other People's Work, So Watch Out for Their Material Appearing in Your Writing (citation)

### Although LLMs Are Unprecedentedly Capable, They Only Output Existing Content. Do Not Let Their Output Undermine Your Creativity

### Rely More on Your Own Reading Skills, and Be Wary of Becoming Overdependent on AI to Read Texts for You
