---
title: Poll vs Push development time
tags: ["distributed systems", patterns]
---

<h1>{{ page.title }}</h1>

## TL;DR

When rushing to push software out the door polling may not be such a bad idea. Pushing data along pipelines and services may make development speed drop as much as 4 times (calculated by a fair throw of the dice of course) compared to the much more common polling model.

## Introduction

Modern stacks and frameworks worth pursuing will almost always introduce new concepts and development techniques that may lead developers to change the ways they approach application design and the way they reason and frame problems and their respective solutions. Such a one has been Elixir for me, a modern language that makes keeping in-memory state ridiculously easy by isolating state inside 'processes' and allowing interactions with said state via messaging only. State, applying transformations to the state and notifying subscribed processes of changes in state is a very common approach to application development in the Elixir world. In fact once you realize the effects this development model has on code clarity and speed of execution you may be tempted to apply it on a larger scale. And this is where things can get tricky.

## A fictional example

Imagine you have some data that do not change that often, let's say like a news feed for example in a news website like BBC for example. Have you seen the article page getting updated as new information arrives? That's what I'm thinking about. To make matters more interesting, let's say that for logged in users you'd also want to filter incoming news and updates based on user preferences. Combine that with the kind of constant traffic a big news website gets and the sort of traffic spikes they need to deal with when world-shattering news is made public (like a princess' new favorite cat picture for example) and you've got a pretty demanding application at hand that will almost certainly require to design with scalability. So you start thinking on approaches... and then it hits you: "I know! I'll use ~~regexes~~ micro-services!<sup>[1](#footnote1)</sup>".

## Alice's approach: pushing data to users
- observation: data changes but not that often, polling would just consume resources needlessly with not much to show for it's efforts. Enter push.

### Notes
<a name="footnote1">1</a>: It is not my intention to debate monolith vs micro-services here as a lot has been written on the subject already. Let's assume that both Alice and Bob here have converged on using micro-services and let's leave it at that.