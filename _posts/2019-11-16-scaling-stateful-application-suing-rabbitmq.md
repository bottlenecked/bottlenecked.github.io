---
title: Scaling stateful applications in Elixir using RabbitMQ instead of distributed Erlang
tags: [Elixir, RabbitMQ, "distributed systems"]
---

<h1>{{ page.title }}</h1>

## TL;DR
For stateful applications developed in BEAM languages the community oftentimes turns to the built-in Erlang distribution to scale them. In this post I propose an alternative way to scale stateful apps using RabbitMQ that does not require interconnected nodes and then talk briefly about the trade-offs involved <sup>[1](#footnote1)</sup>.

## Introduction

Scaling _stateless_ <sup>[2](#footnote2)</sup> applications is more or less straight forward these days: one can add as many application nodes (containers, pods, vms etc.) as needed to serve requests by putting a load balancer (HAproxy or similar) in front of their node farm. It does not matter which node will reply to a particular request since each time the application will lookup data in the database, compute and serve the response. Nodes can be added and removed at will, making this architecture ideal for auto-scaling scenarios based on traffic patterns or other metrics. Of course this class of applications comes with its own set of well-known problems, like increased response latency for example due to the database lookups involved, complex caching schemes, database scaling and more.

_Stateful_ apps on the other hand trade ease of development and a straightforward mental model for the promise of improved runtime behavior. For applications developed on the BEAM developers will often reach for clustering nodes using the underlying Erlang distribution mechanics- not least because they are so easily available and baked-in to the platform. But clustering nodes like that usually means buying into complexity that is not apparent from the start (unless someone happens to have considerable experience with such architectures): leader election, routing, consistency, consensus and split-brains all introduce enormous amounts of complexity to be able to handle edge cases properly, and proper handling of such edge cases is almost always application-specific i.e. there are no universal guidelines that apply to all situations for tackling these sorts of problems <sup>[3](#footnote3)</sup>. The alternative I propose is no silver bullet either, but my intention is that developers that choose to apply it are fully aware of the decisions and trade-offs involved.

## Sample application
We will use the basket part of an e-shop as an example application and model it as a separate service (yay micro-services). Baskets have state that needs to be persisted and each basket is unique to each visitor. We will focus on anonymous browsing only to avoid having complex business detract from the main points of this post.

### Functional requirements
- customers can add and remove items from their baskets
- they can also update -------------------


### Notes
<a name="footnote1">1</a>: This sort of architecture does not necessarily require a BEAM language or even RabbitMQ to pull off. Any actor-based language or framework (AKKA, Orleans, Pony etc.) would be just as good for the purpose of keeping state locally (runtime differences notwithstanding); and RabbitMQ could be replaced by a device capable of doing hash-based routing, like Varnish + sticky sessions (obviously taking into account that messaging has very different semantics than HTTP requests). I went with Elixir & RabbitMQ because it's a stack I feel very comfortable with.

<a name="footnote2">2</a>: Stateless applications in the classic sense are those that need to always perform lookups in the database before serving a response. Applications that use caching to avoid frequent lookups still fall in the broader "stateless application" spectrum. It is perhaps the simplest and best understood application architecture (at least with regards to web applications), and there are a ton of tools and infrastructure software to support this class of apps.

<a name="footnote3">3</a>: There are of-course projects like swarm, lasp and others that make clustering easier to program against, but authors in their efforts to provide simplified APIs may have taken decisions that do not fit in all cases (which is fine) but a developer using those libs may not be aware of these decisions (which is not fine)