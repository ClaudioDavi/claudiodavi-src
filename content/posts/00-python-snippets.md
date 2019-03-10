---
author: "Claudio Davi"
date: 2017-12-06
linktitle: Python Snippets
title: Python Snippets
type: docs
tags:
  - python
  - nlp
  - string
  - file management
  - data science
  - json
  - levenshtein
  - distance
---

### Introdução

Como desenvolvedor, temos muitos desafios interessantes e divertidos para solucionar durante o nosso dia a dia. Alguns deles, acabam sendo dentro da nossa própria code-base, outros podem ser resolvidos com alguns snippets e hacks utilizando outras linguagens e técnicas.

Recentemente surgiu um desafio que foi bastante divertido pra resolver, principalmente porque seria bastante complexo de resolver em JAVA.

A ideia é a seguinte: Dado um arquivo com centenas de linhas relativamente longas e formatado em JSON, meu objetivo era identificar quais dessas linhas eram similares o bastante que com poucas alterações pudessem ser unificadas. Obtendo esse resultado, poderíamos diminuir o tamanho desse arquivo e por consequência, melhorar o desempenho do nosso produto.

Comecei quebrando o desafio em várias partes.

1. Ler o arquivo JSON e guardar ele em memória.

2. Identificar quais as técnicas que eu utilizaria para fazer a comparação das linhas

3. Comparar cada uma das linhas e guardar o resultado em um arquivo distinto.

### Primeira fase:

#### Ler o arquivo JSON e guardar ele em memória.

O formato do arquivo é mais ou menos o seguinte:

    [
      {
        "value": 1,
        "string":'String que eu quero comparar'
      },
      {
        "value": 2,
        "string":'outra string que eu quero comparar'
      }
    ]

Para fazer a análise então, vamos gravar em uma lista as strings que precisamos verificar:

    import json
    #Carrega o arquivo pra memória e filtra o que a gente quer analisar
    with open('file_with_strings.json') as file_data:
        data = json.load(file_data)
          list_strings = []
          for item in data.values():
              for it in item:
                list_strings.append(it["string"])

Python faz com que seja bastante fácil você ler um arquivo. E ainda dentro da biblioteca padrão a gente já tem um pacote chamado JSON que com ele conseguimos reconhecer exatamente os atributos dentro de cada objeto JSON. No exemplo acima, eu crio um objeto data que recebe o retorno do método json.load(), percorro os valores dentro desse objeto buscando apenas pelos atributos que são importantes pra mim (nesse caso, “string”) e adiciono a minha lista que vamos utilizar mais adiante. Primeira etapa concluída.

### Segunda fase

#### Identificar Tecnicas

Para a segunda etapa, busquei algumas técnicas para verificação de similaridade entre strings e selecionei duas das mais interessantes. Uma delas é o SequenceMatcher que já vem na biblioteca padrão, e a outra é a distância de Levenshtein disponível através da biblioteca jellyfish.
O SequenceMatcher, considera a maior sequência contínua idêntica entre as dois elementos de qualquer tipo (desde que sejam ‘hasheaveis’) desconsiderando espaços em branco, linhas em branco e afins. Para este caso usaremos o ratio() onde vai nos retornar a porcentagem dessa similaridade.
A distância de Levenshtein é mais interessante, ela considera a quantidade de caracteres que deveriam ser modificados (Incluídos, deletados ou alterados) para que as duas strings sejam idênticas. Segunda etapa concluída.

### Terceira Fase

#### Comparando resultados

Nesta terceira e ultima etapa então, vamos comparar utilizando as duas medidas escolhidas e gravar em um arquivo de saída.
Pra começar, eu criei um método que se chama ‘similar’, este método vai pegar as duas strings e criar um dicionário com as diferentes medidas e suas respectivas strings.

    from difflib import SequenceMatcher
    import jellyfish

    def similar(primeira, proxima):
        result = {
        "string_primeira": primeira,
        "string_proxima": proxima,
        "percentual_similar": SequenceMatcher(None, primeira, proxima).ratio(),
        "char_diferentes": jellyfish.levenshtein_distance(primeira, proxima)
        }
        list_of_results.append(result)

O código acima é bem simples, importando as duas bibliotecas, a gente cria um dicionário e dentro dele os dados que queremos utilizar, incluindo os dois calculos. No fim, colocamos esses resultados em uma lista que será depois escrita em um arquivo para facilitar a comparação.

Como não queremos lidar com um for dentro de outro pois pode acarretar em muito tempo de processamento, a biblioteca padrão do Python oferece uma maneira bem legal e com um bom desempenho para iterar entre combinação de itens. chama-se itertools. pra isso, nós vamos importar o modulo itertools e fazer a combinação a partir da lista que criamos no passo 1.

    import itertools
    #Itera sob todas as strings para comparar umas com as outras
    for primeiro, proximo in itertools.combinations(list_strings, 2):
    similar(primeiro, proximo)

O código acima vai fazer uma combinação de pares dos itens da lista que a gente passa por parâmetro. Se eu quisesse colocar mais de 2 por vez pra comparar eu poderia fazer itertools.combinations(list_strings, 4) e faria 4 por vez.

Depois disso só precisamos passar o resultado para o arquivo de saída. O seguinte código toma conta do recado:

    #grava em um arquivo o resultado final
    with open('final_result.txt', 'w') as outfile:
    json.dump(list_of_results, outfile)

Com isso, eu consegui resolver o meu problema e ainda com esse mesmo script, eu posso enfrentar problemas parecidos sem perder tempo nenhum. É importante lembrar que esse código não tem o melhor desempenho, e eu acredito que pode ser melhorado. Existem situações onde é simplesmente inviável fazer essa comparação (tentei com strings de mais de 4mil caracteres e demorou pelo menos algumas horas pra executar). Portanto use por sua conta e risco.

</br>
</br>

---

</br>
Se você gostou desse texto e gostaria de ler mais postagens sobre Machine Learning Aplicado, Engenharia de Software e afins, clique nos links ao lado. Qualquer perguntas que você tenha, pode me mandar via Twitter em @claudiodavi ou e-mail em cdavisouza [@] gmail.com . Eu sempre respondo!