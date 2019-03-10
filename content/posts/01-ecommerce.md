---
date: 2018-08-20
linktitle: Analisando um Ecommerce
title: Analisando dados de um Ecommerce
type: docs
tags:
  - ecommerce
  - analise de dados
  - data science
  - machine learning
  - regressão linear
  - linear regression
  - open source
---

## Introdução

Quando comecei a estudar _Data Science_ uma das primeiras coisas que nos deparamos é com **Regressão linear**. E o exemplo clássico disso é o famoso caso do preço de uma casa baseado no seu tamanho.

### Definição do problema

Neste artigo pretendo apresentar um exemplo real (porém com dados Fakes) de uma análise que utiliza Regressão Linear para auxiliar um e-commerce a melhorar o seu lucro respondendo a pergunta:

> _“No que devemos investir para melhorar o nosso retorno financeiro?”_

### Metodologia

Nós vamos começar analisando a estrutura dos dados, depois faremos algumas visualizações e por fim, apresentar os resultados, onde eu mostro que somos capazes de estimar quanto um usuário gastaria por ano dado seu histórico de sessão. E ainda, responder a pergunta principal. Por fim, quem quiser acompanhar o código, o projeto está disponível no meu Github.

> Importante: Não entrarei em detalhes sobre como funcionam os algoritmos apresentados aqui. Este post tem foco no valor entregue para a empresa dona dos dados.

## Análise

Inicialmente verifiquei a estrutura dos dados que podemos ver na Figura 1.

![Figura 1](images/ecommerce/tabela.png)
E-commerce Dataset — 5 primeiras colunas

A descrição de cada uma delas é a seguinte:

- Avg. Session Length: Tempo médio de atendimento.
- Time on App: Tempo médio gasto no App em minutos
- Time on Website: Tempo médio gasto no Website em minutos
- Length of Membership: Quantidade de anos que um usuário é cliente (Período Cadastral)

Inicialmente apenas por essa descrição e estrutura que vimos acima, já podemos ter uma ideia de por onde começar. Vamos verificar a relação entre o tempo de sessão e o gasto anual para cada plataforma (Web ou Aplicativo).

Figura 2. Tempo no Website vs Gasto Anual

Na Figura 2, a gente consegue ver uma baixa correlação entre o tempo no Website e o Gasto Anual. Os números são bastante balanceados, tendendo para uma área onde o tempo de fato tem influência no gasto anual, mas muito pouco.

Agora vamos analisar o tempo no App em relação ao Gasto Anual:

Figura 3. Tempo no App vs Gasto Anual

Tivemos muito mais sucesso agora. Podemos notar uma clara correlação:

> Quanto mais tempo gasto no Aplicativo, maior a probabilidade de se gastar mais dinheiro.

Já que o aplicativo se mostra mais promissor, vamos avaliar na Figura 4 se o período cadastral do cliente influencia na quantidade de minutos que ele fica online no App.

Figura 4. Tempo no Aplicativo vs Período Cadastral

Podemos notar algumas coisas na visualização acima.

A média geral da sessão de quem usa o aplicativo fica em torno de 11 a 13 minutos para aqueles com 3 a 4 anos de uso.
Quem tem mais de 4 anos de uso do sistema tende a ficar mais tempo online
Com essas informações apenas, podemos já começar a criar ações de Marketing para o público ativo a mais tempo. São dessas pessoas que precisamos da lealdade e manter o uso do aplicativo sempre alto.

Falando nisso, vamos aproveitar para ver a relação entre o período cadastral e o valor gasto anualmente.

Figura 5. Peíodo Cadastral vs Gasto Anual

Nossos dados corroboram a inferência anterior.

### Conclusão da Análise

> Quanto mais tempo um usuário é membro do serviço, mais dinheiro ele tende a gastar.

## Regressão Linear

Depois de todos esses dados e essas análises, conseguimos chegar em um modelo de regressão linear para predizer o gasto anual de um usuário a partir de suas informações de sessão e tempo de registro.

Depois de treinar o modelo, vamos avaliar os resultados em conjunto com os dados de teste:

Figura 6. Dados de Teste vs Predição

Analisando o resultado do treinamento da regressão, temos uma variância bem pequena em relação ao previsto com os dados reais.

Existem algumas maneiras de se verificar a qualidade de um modelo de Machine Learning. Vamos aqui olhar os resultados de duas métricas para o modelo anterior.

- MAE: Mean Absolute Error = Média da soma dos erros.
- RMSE: Root Mean Square Error = Raiz quadrada da média dos erros elevados ao quadrado.

Ambos os valores representam acurácia do modelo e são orientados à 0. Quanto menor o número melhor. Como o RMSE tira o quadrado dos erros antes, ele tende a punir erros maiores, trazendo coeficiente de erro muito maior do que apenas a média absoluta. Punir erros maiores significa o seguinte:

Dado uma lista de erros `x = [2, 2, 2]` e outra lista de erros `y = [2, 4, 0]` ambas possuem a mesma média absoluta, ou seja `MAE(x) = 3 e MAE(y) = 3`. Porém um erro de 4 unidades é mais grave do que um erro de 2 unidades, mesmo tendo acertado perfeitamente um dos valores. Utilizando RMSE teremos `RMSE(x) = 3,46` e `RMSE(y) = 4,47`
Neste caso temos um `MAE de 8.53` e um `RMSE de 10.75`. O que é bastante positivo pois são dois valores bastante baixos considerando que nosso valor a ser predito bate na casa das centenas.

Antes de responder a pergunta inicial vamos a mais um teste. Digamos que um usuário tenha 2 anos de período cadastral e passa em média: 20 minutos no aplicativo por dia, 10 minutos no website por sessão e cada vez que faz uma compra, leva 15 minutos. Quanto esse usuário gastaria por ano?

A resposta para essa pergunta vem do nosso modelo. Inserindo esses dados no modelo temos a resposta: Aproximadamente R\$220.

Agora, para a pergunta principal:

> “No que devemos investir para melhorar nossos lucros?”.

Verificando os coeficientes, podemos indicar quais ações teriam mais impacto para aumentar o total gasto anualmente pelos clientes.
Com esses resultados, a empresa pode tentar alinhas novas ações buscando melhorar a sua estratégia de negócio.

Cada valor da Figura 7 significa que uma alteração de ‘uma’ unidade em alguma categoria, aumenta a quantidade correspondente em dinheiro gasto anualmente.

Figura 7. Coeficientes

### Resultado dos Coeficientes:

- Aumento de 1 unidade em Avg. Session Length é associado com um aumento de R\$26.10 ganho anualmente.
- Aumento de 1 unidade em Time on App é associado com um aumento de R\$38.95 ganho anualmente.
- Aumento de 1 unidade em Time on Website é associado com um aumento de R\$0.80 ganho anualmente.
- Aumento de 1 unidade em Length of Membership é associado com um aumento de R\$61,63 ganho anualmente.

A partir desses resultados, nosso cliente pode agora decidir como agir dentro da sua empresa. Algumas ações possíveis:

## Conclusão

Melhorar a experiência do Website para tentar melhorar o retorno.
Evoluir o aplicativo para que as pessoas passem mais tempo nele.
Benefícios para membros mais antigos, para manter a fidelidade.
Regressão linear é uma das primeiras técnicas que aprendemos quando estudamos Machine Learning e muitos esquecem do quanto ela pode ser útil e poderosa. No caso acima, conseguimos entregar alternativas e informações de bastante valor para uma empresa com problemas reais.


</br>
</br>

---

</br>
Se você gostou desse texto e gostaria de ler mais postagens sobre Machine Learning Aplicado, Engenharia de Software e afins, clique nos links ao lado. Qualquer perguntas que você tenha, pode me mandar via Twitter em @claudiodavi ou e-mail em cdavisouza [@] gmail.com . Eu sempre respondo!