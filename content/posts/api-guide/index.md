+++
title = 'Another opinionated API building guide'
date = 2024-05-04T16:14:42-03:00
draft = true
+++

A significant amount of a web developer's work consists of writing or consuming APIs. The consume part is commonly easy: you read the docs, generate your credentials, plan on what resources you need and implement an integration on your target app (now that i wrote all the steps maybe it's not so easy). In the worst case you end up with a messy (but functional) implementation that gets the job done.

On the other hand, writing can be more tricky and complex, involving skills that usually surpasses basic development knowledge. Sure, this applies if you want to write a _good_ API. But what are the parameters we can use to classify and API as _good_ or _~(a piece of shit)~_?

<!-- Uma parte significativa do trabalho de uma pessoa programadora que trabalhe com a web é escrever ou consumir APIs. Consumir costuma ser simples, você lê a documentação, gera suas credenciais, planeja quais recursos precisa consumir e implementar a integração na sua aplicação alvo (ok, talvez não tão simples assim). No pior dos casos você vai acabar com uma implementação um pouco confusa mas que ainda assim provavelmente irá funcionar e fazer o trabalho a que se propõe. -->

<!-- Escrever, por outro lado, é uma tarefa muito mais complexa e envolve habilidades que muitas vezes ultrapassam o conhecimento técnico mais comum. Claro, isso se você quiser escrever uma _boa_ API. Mas quais são exatamente os parâmetros que podemos usar para classificar uma API como _boa_? Se você perguntar isso para 10 pessoas talvez você receba 10 respostas ligeiramente diferentes, mas acredito que a maior delas irá gravitar em torno de alguns princípios básicos que muitas vezes são conhecidos mas não são priorizados.

Esse artigo se divide em duas partes, iniciando com uma discussão teórica sobre pontos destacáveis que podem contribuir para a qualidade geral de uma API, seguido de um exemplo prático de estruturação de uma API REST -->

<!-- ### Compreensibilidade

Como o acrônimo sugere, uma API é uma interface entre sua aplicação e o mundo exterior, e toda interface para ser útil precisa ser compreensível, esse é o primeiro desafio de escrever uma API: outras pessoas precisam ser capazes de extrair informação sem precisar te consultar sobre a estrutura toda da API. -->