---
title: Scaling stateful applications in Elixir using RabbitMQ instead of distributed Erlang
tags: [ho, hum]
---

<h1>{{ page.title }}</h1>

For stateful applications developed in BEAM languages the community oftentimes turns to the built-in Erlang distribution to scale them. In this post I propose an alternative way to scale stateful apps using RabbitMQ that does not require interconnected nodes and analyze the trade-offs involved <sup>[1](#footnote1)</sup>.

Scaling _stateless_ <sup>[2](#footnote2)</sup> applications is more or less straight forward these days: one can add as many application nodes (containers, pods, vms etc.) as needed to serve requests by putting a load balancer (HAproxy or similar) in front of their node farm. It does not matter which server will reply to a particular request since each time the server will lookup data in the database, compute and serve the response. Nodes can be added and removed at will, making this architecture ideal for auto-scaling scenarios based on traffic patterns or other metrics. Of course this class of applications comes with its own set of well-known problems, like increased response latency for example due to the database lookups involved, complex caching schemes, database scaling and more.

_Stateful_ apps on the other hand trade 


### Notes
<a name="footnote1">1</a>: This sort of architecture does not necessarily require a BEAM language or even RabbitMQ to pull off. Any actor-based language or framework (AKKA, Orleans, Pony etc.) would be just as good for the purpose of keeping state locally (runtime differences notwithstanding); and RabbitMQ could be replaced by a device capable of doing hash-based routing, like Varnish + sticky sessions (obviously taking into account that RabbitMQ messaging has very different semantics than HTTP requests). But I'm more familiar with 

<a name="footnote2">2</a>: Stateless applications in the classic sense are those that need to always lookup request data in the database before serving a response. Applications that use caching to avoid frequent lookups still fall in the broader "stateless application" spectrum. It is perhaps the simplest and best understood application architecture (at least with regards to web applications in general)