---
title: Ruby first impressions
tags: [ruby, opinion]
---

# {{ page.title }}

After almost 10 years of working in online gaming it is time to go and work on a completely different domain (medicine) using my favorite tech of the last 5 years: Elixir. But like most shops doing Elixir, this next one I'm going to be working with has started out with Ruby, and so it made sense to catch up to Ruby as it's almost certain I'll have to work with it sooner rather than later. For this I'm reading [The Well-Grounded Rubyist, 3rd edition](https://www.manning.com/books/the-well-grounded-rubyist-third-edition) book[^1] that my new colleagues suggested.

_Disclaimer: I've not yet written even the tiniest amount of Ruby code other than the examples in the book. The following are based solely on my first impressions of the language and my opinions may well change later. You've been warned._

Before I go into details I'd like to share my preconceptions of what one should expect from Ruby based on what I'd heard on the internets mostly. And the things people would say about Ruby were the feeling of productivity enabled by the language and the tooling and frameworks around it, the beauty of the language and it's easy-on-the-eyes syntax, and finally that performance is not among Ruby's strengths.

Having a better understanding of the language now I have to say that I don't quite agree with the assertions above- they're too mildly put in my opinion and do not accurately describe the compromising situation Ruby finds itself in.

#### Object-itis
Everything is an object in Ruby. Other OO languages make similar 'everything-is-an-object' statements, but Ruby takes this to the next level by modelling even `Integer`s for example as objects. The reasoning for that apparently is that by modelling everything as an object, a programmer does not have to be taught different rules for 'values vs. references', which is perhaps commendable on one hand (and I say this with the utmost cautiousness- more on uniformity later) but at the same time this decision has unfortunate performance consequences, as integers have to be [stored and de-referenced from the heap](https://stackoverflow.com/questions/13639166/in-ruby-what-is-stored-on-the-stack) for any calculation to take place. I also believe that treating `int`s differently that e.g. `Person`s (as in value vs reference semantics) would not constitute a surprise, as programmers coming from different language backgrounds will have already encountered this and thus not affecting the learning curve of the language at all. +1 point for elegance then, but -1 for performance.

#### Mutability
I believe then that mutability is the answer to these more-accented-than-elsewhere (see above) _single-threaded_ performance issues that Ruby finds itself with, which again is not uncommon among most object-oriented- or even most imperative languages in general. Only Ruby ups the ante again by offering mutable strings. Mutable strings are something that high-level languages have mostly shied away from, opting instead for treating strings as immutable values. The reason behind string immutability is (somewhat counter-intuitively) performance: the fact that they're so common in programs means that they are generated in large amounts, and by being essentially arrays in nature means strings are often large contiguous blocks of bytes, putting the pressure to the memory management facilities of the runtime (ie the garbage collection or reference counting subsystems). By giving strings immutable semantics though, most strings will not live past generation 0 (or RC count will drop fast to 0) and can thus be removed shortly after they're created and keep memory pressure low. Long story short, even though mutability in strings will perhaps positively impact short-term performance (mutating a string means less copies), long-term performance over the course of a program will most probably suffer because of the increased number of references to the same object essentially from multiple parts of said program and also because of the more complex GC logic of the runtime for string cleanup. Not to mention that mutability makes things much more 'interesting' during debugging, adversely affecting programmer productivity by forcing more frequent bug-hunting expeditions on teams.

So it seems to me that Ruby falls into this trap of optimizing for short-term gains over longer-term performance and maintainability gains. And as I've alluded to above, this is mostly single-threaded performance mainstream languages concern themselves with. Multi-threaded or multi-core performance requires far more generous doses of immutability. Takeaway: mutability does not negatively affect syntax or code looks and I suspect by now that beauty is a much bigger driver for Ruby than I was originally led to believe. -1 point for performance and another -1 for maintainability. +1 for surface beauty because it remains largely unaffected by this which is a feat on its own.

#### Fat, smart objects
Objects in Ruby, even core ones like Integers and Strings have a large chain of ancestors (either classes or modules- read more on that later) endowing them with a ton of behavior right out of the gate. This in my opinion makes for a very large surface of built-in functionality that programmers need to wrap their head around, while hiding the origins of a method among layers of inheritance. Functional programming in contrast is very strict in separating behavior from data, a practice which greatly benefits maintainability and opens the doors for multi-core performance. Again, Ruby is not the only language that mixes in data with behavior, but it is once more somewhat of a front-runner in this regard- not only by opting for deep hierarchies, but also for encouraging the re-opening of classes for programmers to add even more functionality to objects. The overall way class extension semantics work reminds me of Javascript. But Javascript, for all it's faults, strongly discourages programmers from adding their methods to the prototypes of built-in objects to avoid collisions and programmer confusion, while Ruby seems to encourage the exact opposite of that.

Another side-effect of these well-endowed, everything-and-the-kitchen-sink types of objects is the very real danger of obsolescence-without-reprieve. By trying to include everything a programmer might conceivably need when working with Strings for example, one can find methods like [`String#crypt`](https://www.rubydoc.info/stdlib/core/String:crypt) and [`String#next`](https://www.rubydoc.info/stdlib/core/String#next-instance_method) in the core APIs of Ruby. Cryptography is a fast evolving field with major breakthroughs every year, and Ruby's implementation of crypto is very much insecure nowadays, made more so by the fact that it does not enforce good salt or secret practices. Just by virtue of being in the core lib however, String#crypt cannot be removed or changed to a more secure algorithm because of the dependencies many programs will have on it- both on public API surface but also on implementation-specific behavior like the length of the produced encrypted string. And since the method cannot be removed, it is still available for even more programmers to take a dependency on. String#next is similar in that regard by working with ASCII chars only, but which probably makes little sense any more because of the new default UTF-8 encoding for strings in Ruby. -1 for maintainability again; convenience gets +1 in the short term but -1 in the long term, so it's a net zero.

#### The photoshop file format[^2] effect
The more I delve into Ruby, the more I worry about the multiple ways to achieve the same thing. Take the above String#next method, which is also aliased to `String#succ`. I had trouble imagining why Ruby would introduce aliases to core methods in the APIs, but my friend Nick suggested that it's perhaps because it 'reads better'. I guess this enforces my newly-minted biases that Ruby is first and foremost about external beauty, and everything else is either sacrificed to achieve good looks or is somewhat of an afterthought for Ruby. Much like #next and #curr, most everything that can be done one way in Ruby can also be done a second way. For every `X` an `X'` exists that does _almost_ the same thing but with slightly different semantics. There's both unless and if-nots, untils and while-nots, end-of-statement conditional operators and control blocks, message sending and method-calling, do-ends and curlies, code blocks and lambdas, inheritance and mixins, single and double quoted strings, and probably others I'm forgetting or I don't know about.

Modern language design has this 'pit of success' concept, where by having just the right amount of opinionated syntax and APIs they lead their users to do the right thing, even inexperienced ones. By making it hard to express things in unintended ways, developers following the path of least resistance will naturally end up doing the proper thing. But I guess I don't see this here with Ruby, which is perhaps offering too many ways to do the same thing with lots of different-but-same tools. Take do-end blocks and curly braces for example, which are used in almost the same way, only curly braces have greater precedence and bind tighter to method calls- which in my mind makes them safer; and by using them a programmer will end up doing the thing they intended to do more often than not. Do-ends on the other hand look like a riskier proposition, leading to more opportunities for mistakes.

Another consequence of this plethora-of-options is decreased productivity. I can easily imagine someone coming across #succ and having to stop their work to look it up, only to realize that it's actually an alias to #next with which they're familiar with after all. There's a combination perhaps of variable names and surrounding method calls that would make using #succ a better choice in a literary contest, but I don't think it's a good enough argument for its inclusion in language proper. Not when it has the potential to become a productivity sink for multiple programs and programmers, either while trying to understand a piece of code or igniting 'tabs vs. spaces' types of discussions.

As a final note on the effects on productivity, I can perhaps see better now the reason for all the rich tooling in the Ruby community around testing and linting. I used to believe that these could be attributed to Ruby being a dynamic language, but I now see that the potential for errors do not only stem from the dynamic nature of the language, but also from the multiple opportunities for abuse enabled by the too-permissive design choices. Perhaps with a better language base the community would not have to compensate with all the tooling built around controlling mistakes, leaving more time for different types of innovation. +1 for good prose, -1 for productivity and maintainability.

#### Closing thoughts

I can appreciate Ruby's attempts at expressiveness and 'simplicity', especially when compared to the likes of Java or C++ in the '90s. But I believe too much of a good thing can be a bad thing, and the same principle applies here. It is more than possible that Ruby has influenced modern languages to offer a more appealing developer experience to their communities, be it syntax, tooling or general thoughtfulness for human users. But I also believe that we've come a long way since then, and modern languages offer a lot of what was once unique to Ruby, while at the same time not having to compromise on performance and maintainability.

I would not choose Ruby for new projects, not even for Rails (which I suspect is the actual reason behind the stories about Ruby's productivity- not due to the language itself but due to the framework) because of the costs associated for even short-term development. Common wisdom in the Ruby community urges to start a proof of concept with Ruby and Rails, and should one's business prove successful enough, rewrite it later when there's a proven market for the product (at which point a rewrite can be afforded). I do not much agree with this sentiment, both because there now exist languages and frameworks that are as productive as Ruby without any of the tradeoffs, but also because it is _never_ a good time for a rewrite, either because the company is still a startup and needs to keep running to get ahead of things, or because it's established and there's too much code lying around to make rewrites viable.

[^1]: I find that when I'm trying to learn a new piece of tech nothing can beat a good book in terms of introducing new concepts in an organized manner.

[^2]: Ruby having all these millions of ways of doing the same thing also reminds me of the [photoshop file format](https://github.com/gco/xee/blob/master/XeePhotoshopLoader.m#L108) and [php](https://eev.ee/blog/2012/04/09/php-a-fractal-of-bad-design/)- from the good old days of php 5.2/5.3 when classes were introduced but the documentation insisted everywhere that "php is not and never will be an OO language". But, but... why classes then? Oh well.

Thanks to Alex A. and Nick P. for reading earlier drafts of this and providing feedback.