---
date: 2018-08-27
linktitle: Analisando Ads
title: Analisando Propagandas
type: docs
tags:
  - Data Science
  - regressão logistica
  - analise de dados
  - marketing
  - analise preditiva
  - open source
---

## Introdução

No post da semana passada [Link]({{< ref "/posts/01-ecommerce.md" >}}) vimos a utilização de um método chamado **Regressão Linear** para procurar possíveis melhorias dentro de uma empresa para melhorar os seus lucros. Esta semana, veremos um método também de regressão chamado _**Regressão Logística**_.

Para este projeto, usaremos dados de acesso à internet de usuários, coletados por uma empresa de _Marketing_, e verificar se eles clicaram ou não em uma propaganda -advertisement- na tela. Tentaremos responder a seguinte pergunta:

> “Baseados apenas nos dados coletados, o usuário clicaria ou não na propaganda?”

### Metodologia

Como de costume, começaremos explorando um pouco dos nossos dados, faremos algumas visualizações e depois testaremos nosso modelo em cima de dados de teste. Como sempre, o código para quem quiser seguir olhando a implementação está disponível no meu [Github](http://github.com/claudiodavi).

## Análise

Verificando a tabela temos a estrutura vista na Figura 1.:

Figura 1. Estrutura dos dados

A descrição das colunas é a seguinte:

- **Daily** Time Spent on Site: Tempo gasto no site em minutos
- **Age**: Idade do usuário em anos.
- **Area Income**: Média salarial anual da região do usuário
- **Daily Internet Usage**: Média de minutos por dia de consumo de internet.
- **Male**: Caso o usuário é Homem (1 para Sim, 0 para não)
- **Clicked on Ad**: 0 ou 1 indicando se o AD foi clicado ou não.

Eu cortei propositalmente algumas colunas da tabela, neste artigo, utilizaremos apenas as colunas acima.

Vamos começar verificando a distribuição de idade dos nossos usuários, tentaremos identificar qual a faixa etária mais presente no nosso conjunto de dados. (Figura 2)

Figura 2. Distribuição de Idade

A maioria dos nossos usuários aparentam ter entre 30 a 40 anos de idade, o que já nos dá uma indicação de um público médio do website. Outra verificação que podemos fazer, é a correlação entre a idade e a média anual do salário da região que essas pessoas moram (Figura 3).

Figura 3. Idade vs Salário Anual

Como já vimos que a maioria dos nossos usuários pertence a faixa etária 30–40 anos, conseguimos também notar que essas pessoas vivem em boas condições em áreas de maior poder aquisitivo.

Agora vamos tentar identifica se a idade é influente no tempo de sessão no site. Vamos usar uma visualização diferente, onde os valores mais escuros representam uma maior concentração de dados, no post da semana passada, utilizamos uma visualização com hexágonos, desta vez (pra não ficar repetitivo) vamos visualizar com profundidade (Figura 4).

Figura 4. Tempo no Site vs Idade

Conseguimos mais algumas informações bastante relevantes. Podemos notar que a grande maioria dos nossos usuários passa em média 80 minutos no site e tem entre 28 e 35 anos.

Outra informação relevante que precisamos antes de começar: Qual a relação entre o tempo total gasto na internet e o tempo gasto no nosso site?

Figura 5. Tempo de Internet vs Tempo no Website

Como esperado, quando mais tempo se passa na internet, maior a probabilidade de se passar mais tempo no nosso website.

Antes de passar para a próxima fase, vamos verificar se esquecemos de checar algumas coisa, para isso, plotaremos em uma única imagem todas as relações entre os atributos numéricos (Figura 6).

Figura 6. Gráfico de Pares

Parece que dessa vez deixamos passar bastante coisa. Algumas coisas que podemos notar aqui:

- Quem passa mais tempo no site tem mais chances de clicar em um AD.
- Pessoas mais novas costumam clicar mais.
- Pessoas que moram em áreas mais nobres clicam mais nos nossos ADs.
- Não existe diferença notável entre público masculino e feminino.

Agora que já conseguimos extrair bastante informação e conhecemos bem nossos dados, vamos aplicar o modelo de regressão logística.

## Regressão Logística

Com um modelo padrão de regressão logística, conseguimos obter um resultado bastante satisfatório. Na semana passada, vimos os conceitos de _MAE_ e _RMSE_, dessa vez essas métricas não se aplicam, portanto avaliaremos o modelo a partir da sua **precisão** e do seu **recall**.

### Precision & Recall

- **_Precisão_** é a proporção de verdadeiros positivos em todos os resultados positivos obtidos. A ideia é responder: Qual a proporção dos resultados positivos retornados não são falsos positivos?
- **_Recall_**, por sua vez, responde a pergunta: Qual a proporção de verdadeiros positivos foi identificado corretamente? Nesta métrica, avaliamos em conjunto os falsos negativos.

### Análise dos Resultados

Agora que já estamos mais familiarizados com os conceitos, podemos verificar nossos resultados:

Figura 7. Precision - Recall

A Figura 7. nos mostra uma média de 92% de acerto para _precision_ e _recall_, que para nossos fins é um ótimo resultado. Isso quer dizer que inserindo os dados de um usuário qualquer, conseguimos predizer com quase certeza se ele clicaria ou não em um AD. Vamos a um exemplo:

Marcelo tem 25 anos, fica em média 240 minutos (4 horas) na internet por dia e passa cerca de 30 minutos no nosso site. Ele vive em uma área da sua cidade onde a média salarial anual é de R\$25.000,00. Nossos dados de entrada então seriam: `[30,25,25000,240,1]`. Neste caso, muito provavelmente Marcelo não clicaria na propaganda, nosso modelo retorna uma probabilidade de 87.5% de chance de ignorar o AD e 12.5% de chance do Marcelo interagir com ele.

Regressão logística é a técnica de regressão padrão para quem precisa que a saída sejam dados binários. É bastante utilizada em análise preditiva e para descrever a relação entre variáveis lineares e nominais com uma saída binária.
