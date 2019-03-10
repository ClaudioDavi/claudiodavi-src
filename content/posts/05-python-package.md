---
linktitle: "Python-Package"
title: "DAGscience - Meu Pacote Python"
bookShowToc: false
date: 2019-03-10T19:30:26-03:00
draft: true
---

## Então, eu meio que escrevi uma biblioteca

No meu trabalho recentemente venho fazendo diversos experimentos para melhorar a performance dos modelos de *machine learning* que tenho criado, embora nem todos vão para produção, eu sempre acabo escrevendo o mesmo workflow: Dados entram -> são transformados -> o modelo é treinado e depois salvo para ser utilizado nos produtos.

Antes de me tornar oficialmente *Cientista de Dados* eu sou um **Engenheiro de Software** e por isso eu gosto não só de construir modelos, mas de *criar programas que me sejam úteis e me facilitem a vida*. Nos ultimos dias venho escrevendo (mais lentamente do que gostaria) uma biblioteca que me ajuda a dar estrutura ao meu workflow. Esse modelo que eu acabei criando me ajuda a dar estrutura para os meus projetos.

O objetivo do projeto é esse mesmo: Simplificar o processo da Engenharia de Machine Learning com técnicas de Engenharia de Software.

### Grafos Direcionados Acíclicos (DAG)

Em algum momento durante as minhas pesquisas eu caí nesse termo: **Directed Acyclic Graph (DAG)**. Em resumo **DAG** significa um fluxo com uma entrada e saída bem definidas onde não existe a possibilidade de voltar uma fase, você pode até pular algumas fases, mas seu caminho é sempre pra frente. Olhando meus pequenos projetos, eu vi que justamente esse era meu workflow desde o começo. Começo buscando dados da fonte original, tratando, criando features e treinando um modelo. *PERFECT FIT*.

### Sobre a biblioteca

Recentemente lendo sobre algumas novas tendências e bibliotecas, eu li um bom tutorial de como criar seu próprio pacote python e decidi colocar minha idéia em prática, em alguns dias eu extraí o que era útil dos meus projetos e o que funcionava e criei uma arquitetura abstrata para ser seguida. O pacote por enquanto está em *Beta* e foi feito com a necessidade de ser o menos invasivo possível, confiando apenas em Python puro pra funcionar.

Se você leu até aqui, provavelmente achou o projeto interessante. Portanto segue o link pra você visitar:

[DAGscience](https://github.com/ClaudioDavi/dagscience)

Vale lembrar que ainda está em beta, portanto aceito idéias e sujestões via Twitter em @ClaudioDavi ou via uma Issue na página do projeto no github!
</br>
</br>

---

</br>
Se você gostou desse texto e gostaria de ler mais postagens sobre Machine Learning Aplicado, Engenharia de Software e afins, clique nos links ao lado. Qualquer perguntas que você tenha, pode me mandar via Twitter em @claudiodavi ou e-mail em cdavisouza [@] gmail.com . Eu sempre respondo!