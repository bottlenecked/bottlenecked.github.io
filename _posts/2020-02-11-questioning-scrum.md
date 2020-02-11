---
title: Questioning scrum
tags: [scrum, opinion, rant]
---

# {{ page.title }}

> Say, what's the best programming language?

Well, it depends. What are you building?

> OK, it depends. Then can you please tell me what the best software architecture is?

It depends. What are you trying to optimize for?

> Huh. Wasn't expecting that, wise guy. Try this: What is the best editor?

Depends on a lot of things I guess... personal preference, language support and a ton of other stuff can play a role in your choice.

> Right. 'It depends' again.

Sure. And you know what? You can say the same thing on almost all aspects of software development- "best CI", "best approach to testing", "best memory management", "best concurrency model", "best chair"; all the good answers seem to start with an 'it depends'- because nothing is universally "the best" for every project and every person or team.

As programmers we've learned that even the most flame-warish, troll-baity, fan-feverish questions like oop-vs-functional or tabs-vs-spaces don't have exactly One True Answer (TM). Except when it comes to software development _methodologies_. A demonstration:

> What is the best way to develop software?

Why, scrum of course!

We've internalized the answer to this question, and have falsely led ourselves to believe that there is in fact a One True Answer to it. It's not even _in question_, it's a fact. A god-given. A load of bull.

And this is exactly why we as a community of professionals do not deserve to be called 'computer scientists' or 'software engineers'. Because science does not accept facts without proof. Science questions what we think we know and asks more questions and keeps probing until something is disproven or is irrefutably proven.

When it comes to scrum, asking questions _ist verbotten_. We accept it like the word of god (or gods, however many is your cup of tea) when there is ample evidence that it __does not work__. 'Oh no' you're saying. 'No no no, you're WRONG! I've read the success stories and it has worked!'. Sure. I'm not saying that it does not _always_ work; that would make me come off as dogmatic as the thing I'm being critical of. A hypocrite.

Scrum is a religion. A dogma. It does not bear any scrutiny, or you will be branded a heretic. When someone dares utter 'but we tried it and it didn't work', zealots rush in to defend it: 'it's not scrum, it's YOU! If only you followed the One True Path you'd have succeeded!'. Any evidence you may present to the contrary, some scrum high-priest or other will recite that mantra to you. Just like religion, the [burden of proof does not fall on the shoulders of those making improbable claims, but on that of others](https://en.wikipedia.org/wiki/Russell%27s_teapot).

'Oh, come on' you're thinking again. 'You can hold your daily standup in the evening and you can do 3-week sprints. That's the exact opposite of being dogmatic' you're thinking- 'dogma does not allow for variations. Scrum is not dogma, it's freedom!'. Right. Reminds me of a certain someone who is the son of a certain someone else that came to free us from sin. You can be free too, so long as you believe in all the horse you're being fed.

Scrum will use weasel words, like 'story points' that defy any and all attempts to draw parallels to things we understand. They're not meant to represent time, but they will help you measure how long something will take (see? it's like time, but not exactly). Again that certain belief comes to mind of a being that is both father and son and spirit that's all 3-in-one but not exactly. Loosey-goosey stuff made to make you feel uncertain. You see it, don't you? No? Read on then.

Like religion, scrum is built to propagate lies that directly benefit the church. Scrum Overlords, Scrum Supreme High Beings, Scrum Hierophants and Scrum Angels. It is not there to help us build and deliver software fast, it's there to make the flock cower in awe and Scrum-* people fat. It's a curse and a burden on software development. Companies looking for software devs need to fall in line and declare their allegiance to scrum or risk being called backwater. Still not with me? Here's some of my personal experiences that led me to believe that efficiency is not a top priority for scrum.

#### Stand-ups need to happen daily
Most of the teams at my current workplace start work at 10:00 and hold their daily stand-ups at 10:15. Every single day, religiously. If you're still programming for a living, you're probably pretty averse to anything that interrupts you and gets you out of the zone. So these devs in order avoid being interrupted just don't start work until after the daily standup ends. Which many times takes more than 10 minutes. 'Foul', I hear you cry. 'Chapter 1 Verse 4 of the Scrum Book explicitly states that stand-ups should never go on for more than 10 minutes, and if they do then you're doing it wrong'. Right. It's yet another case of it's our fault, not scrum's. For all it's 'agile' mindset, it sure is pretty inflexible and unwilling to accommodate that sometimes life just happens. Anyway, as I was saying the team finishes by 10:30. And it's not until 10:45 that people come back to work from a quick coffee break and a smoke.

Almost an hour wasted and the day hasn't even started.

Again, you're thinking that 'But that's on you for not managing your people correctly'. Perhaps. But I think that scrum with all its ceremonies and mandatory meetings is not respectful of people's time. People are led to think that time is not a valuable resource- otherwise why would the company insist on throwing it so carelessly away? It gives people the right to be wasteful as they like with their time. 

Do we really need to be doing those every single day? Do they need to be synchronous and in person? Could they not be written and read asynchronously by each team member for example? And since we're on the subject of time...

#### Refinement time
'Aha! Time for planning poker! You'll get to experience the benefits of accurate estimation first hand now, you infidel!'. Because of course, there's nothing more efficient than having 3 backend devs listen to a junior defending the position that adding that new button is a 55 and then holding a vote on something they don't know and don't care about. And then hold a re-election because someone said 8. Efficiency is my middle name.

I can get behind the alignment argument. But is this the best use of people's time? I believe it is not, and that is yet another opportunity for being inquisitive.

'No you dummy, that's what's required for alignment and keeping everyone on the same page.' Sure, you're wasting people's time but for a good reason. I get it. Waste is good.

#### Sprints should be 2-week affairs
I can see you're about to jump me 'Oh no sir! You've got this one wrong too! _Good_ teams can do 1-week sprints! Ha! How about that?'. Right. Got me again. OK, for argument's sake let's pretend that all sprints are 1-week long affairs.

Now let's say that the sprint just started, but then life happens and the company needs to quickly react to a change in the market like _right now_. 'It's scrum dude, it's all about agility and cat-reflex speed; that's the whole purpose of doing this'. And when asked when it'll be ready, the team says 'Sure, let's see... we'll plan it for next sprint. No room in this one'. NEXT SPRINT. And they're saying that with pride, that they can so seamlessly assimilate the unexpected. A frigging WEEK from now! Whee, so fast.

Once again, it is not the team's fault. They've been vigorously trained through scrum to completely ignore the value of time. How can you explain the concept that 'hours DO matter' when the base unit for measuring time is the sprint, AKA _a whole f\****ing week_? Would you expect an [Ent](https://en.wikipedia.org/wiki/Ent) that measures time in eons to understand haste? No? Well sh\*t, me neither. But there you have it.

---

If we can accept the fact that there is not a one-size-fits-all methodology, it will be the first step to shedding our blinders. Scientifically speaking, stuff that only sometimes work are not thought to be true in the general sense. And that would actually be the absolute best possible outcome we could hope for as a community; we could then ask more questions; focus on what worked, and under which circumstances, and come up perhaps with useful guidelines.

But this has not happened yet. I believe we need to systematically question god-given truths, or we risk having some kid eventually calling BS on the [king's invisible new threads](https://en.wikipedia.org/wiki/The_Emperor%27s_New_Clothes) and then we can kiss credibility bye-bye. People are calling for [self regulation in our industry](https://www.forbes.com/sites/forbestechcouncil/2018/07/09/the-self-regulation-window-is-closing-for-tech-companies) or risk having bad regulation forced onto us. Will scrum be the catalyst that triggers outside regulation? I do not think so, it will probably be something like the Boeing MCAS but on a grander scale. But scrum does not do us any favors either; in fact I could well see it being used as an argument _for_ outside regulation. 'Look at these people, they don't know what they're doing. If they can't see something as obviously wasteful as scrum for what it is, how can they be trusted to have our best interests in mind?'. I do not believe that scrum could ever withstand outside scrutiny. We pride ourselves on our intellect, yet we are totally blind to the bad practice that it is. We should re-evaluate our preconceptions. Leave no stone unturned.