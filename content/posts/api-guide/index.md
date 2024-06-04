+++
title = 'Just another opinionated API building guide.'
date = 2024-05-04T16:14:42-03:00
draft = true
+++

## Introduction

A significant amount of a web developer's work consists of writing or consuming APIs. The consume part is commonly easy: you read the docs, generate your credentials, plan on what resources you need and implement an integration on your target app (now that i wrote all the steps maybe it's not so easy). In the worst case you end up with a messy (but functional) implementation that gets the job done.

On the other hand, writing can be more tricky and complex, involving skills that usually surpasses basic development knowledge. Sure, this applies if you want to write a _good_ API. But what are the parameters we can use to classify and API as _good_ or _~~(a piece of shit)~~ bad_? If you ask this to ten people you might receive 10 slightly different answers, but i believe most of them will gravitate towards some basic principles that are sometimes forgotten.

This article is divided in two partes, starting with a theoretical discussion about outstanding points that may contribute to improve the general quality of an API, followed by a practical example of structuring an API. As the article name suggests, the content is highly based on my experiences and opinions of how that kind of software should be built. You may disagree on some or all the points presented and we can chat about it, maybe you're right and i've been doing things wrong all this time, so feel free to leave a comment or reach me in my social networks. Just don't be an asshole.

And now, with no further considerations, let's beg - OH SHIT! i've forgot to mention, we'll talk about REST APIs. Not SOAP, not GraphQL, not RPC, just REST. Why? Well, it's what i'm most used to and still highly relevant for any developer.

Okay, all things said, please take a seat.

## The _theorical_ stuff

First of all, i think it's useful to remember what's an API conceptually. The acronym stands for _Application Programming Interface_ and that's pretty self-explanatory. We have an application and there's need to programatically read or alter this applications's state so we build and use and interface to achieve this goal. That being said, the range of how to build an API is ridiculously wide, you can receive bitmaps encoded with data through FTP, perform actions based on the data and call it a day. It would be an API, a really funny one but also highly inefficient and confuse.

If any programmer write APIs at their own way we have chaos and if you work with the web you know there's already enough chaos to unleash hell in there. So, we define patterns, architectures, conventions and a whole lot of imaginary abstractions to help us mantain a little bit of order on some places of the web. Each one of these ethereal abstractions have real positive and negative scenarios to be applied, some are more generic, others extremely specified for a use case.

### Architecture

A widely adopted abstraction for building network-based applications is the REST architecture. It was proposed by Roy Fielding on his [PhD Thesis](https://ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf) and describes the web as a huge [finite state machine](https://en.wikipedia.org/wiki/Finite-state_machine) containing virtual resources that are accessible by state-transition functions using the resource's identifier. For me, that's a beautiful idealistic way to think about the web, but is also for big nerds. If you're a big nerd like me, Fielding's thesis is pure gold.

If you do not fall into the big nerd category, the main takeways of REST's definitions are here formatted on a nice bullet list.

- __Client/Server architecture__: there has to be a clear hierarchical separation between the machine requesting the resource and the machine providing it.

- __Statelessness__: a resource request must be self-contained, all the information necessary for the server must be present on the request. Achieving this on HTTP is pretty easy since the protocol itself is stateless (altough there are [passionated discussions](https://stackoverflow.com/questions/6068113/do-sessions-really-violate-restfulness) about sessions, cookies or auth tokens breaking this principle)

- __Uniform interfaces__: when a client is a specific resource the server should always respond with the same interface. If the client requests for a product with the identifier 1, another client requesting the same product should receive the same answer (excluding situations where the resource itself was modified by another request).

- __Layered System__: the client should not be able to distinguish the final server from an intermediary service (proxies, gateways, caching systems). This is useful to add new layers of abstraction without disrupt the final service.

- __Cacheability__: the server should mark responses as cacheable or not and provide information about the expiration or validity of the cached resource. If a specific resource is not cacheable by a business rule that's fine, you should just mark it as non-cacheable. (But please use cache where it fits).

There's also a sixth principle about executing code sent from the server into the clients machine, but i personally think that's sketchy and can lead to weird behaviors, excessive attachment between client and server and security issues. Because this is an opinionated guide i will not teach you this wicked sorcery, if you want to know more about it you can read Fielding's thesis.

Since the architecture was proposed developers from all types of backgrounds adopted and started building APIs based on those principles and calling the result a _RESTful_ API. Of course, real world situations sometimes require changes and tweaks on architectures to comply with the software's requirements so most of the attemps to follow REST guidelines are not completelly compliant with the specs. The most fervorous REST evangelists (and [Fielding itself](https://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)) rant about any degeneration of the sacred REST book.

I prefer to admit that the architecture can't handle alone all the complexity (technical or not) of software development and describe those partial implementations as _RESTlike_. That's usually my go-to approach when designing a new API so the further developments on this guide will be founded on a _RESTlike_ application.

### Goals

Now that i've explained the foundation of what we're building it's time to describe which goals we'll try to reach. Those objectives are gathered on a mix of technical knowledge and empirical experience on past projects i've worked. In some of the points the architecture itself will help us achieve the goal, in others we'll have to modify or complement concepts of the REST principles. Remember, this article is not about writing the __perfect RESTful API__ but a good API in general.

#### Understandability

By definition an interface is a connection between two entities who may be unrelated to each other,

<!-- Uma parte significativa do trabalho de uma pessoa programadora que trabalhe com a web é escrever ou consumir APIs. Consumir costuma ser simples, você lê a documentação, gera suas credenciais, planeja quais recursos precisa consumir e implementar a integração na sua aplicação alvo (ok, talvez não tão simples assim). No pior dos casos você vai acabar com uma implementação um pouco confusa mas que ainda assim provavelmente irá funcionar e fazer o trabalho a que se propõe. -->

<!-- Escrever, por outro lado, é uma tarefa muito mais complexa e envolve habilidades que muitas vezes ultrapassam o conhecimento técnico mais comum. Claro, isso se você quiser escrever uma _boa_ API. Mas quais são exatamente os parâmetros que podemos usar para classificar uma API como _boa_? Se você perguntar isso para 10 pessoas talvez você receba 10 respostas ligeiramente diferentes, mas acredito que a maior delas irá gravitar em torno de alguns princípios básicos que muitas vezes são conhecidos mas não são priorizados.

Esse artigo se divide em duas partes, iniciando com uma discussão teórica sobre pontos destacáveis que podem contribuir para a qualidade geral de uma API, seguido de um exemplo prático de estruturação de uma API REST -->

<!-- ### Compreensibilidade

Como o acrônimo sugere, uma API é uma interface entre sua aplicação e o mundo exterior, e toda interface para ser útil precisa ser compreensível, esse é o primeiro desafio de escrever uma API: outras pessoas precisam ser capazes de extrair informação sem precisar te consultar sobre a estrutura toda da API. -->