---
title: "Anotações"
weight: 1
description: "Notas técnicas gerais"
tags:
  - data science
  - python
  - git
  - process
  - feature extraction
  - data mining
  - feature selection
---

# Anotações tecnicas gerais

## Dicas em Data Science

- Não importa o que você esteja fazendo, sempre tenha backup.
- Teus dados iniciais nunca devem ser alterados.
- Tenha backup de tudo.
- Use uma estrutura para seus projetos, recomendo e uso o [Cookie Cutter Data Science](https://drivendata.github.io/cookiecutter-data-science/).
- Tenha um backup de tudo.
- Use Git.
- Se você escreve código, uma boa prática é utilizar boas práticas de programação.
- Use Git.
- Tenha Backup.
- KDD e CRISP-DM são legais, mas não se prenda.
- Jupyter Lab e/ou Jupyter Notebooks são seus melhores amigos, não seja conservador, crie muitos com nomes relevantes.
- Use editores de texto, crie funções de ETL, não se prenda às análises.
- Salve todas as suas visualizações. (Você vai precisar, sério. Principalmente aquela que ficou esquisita).
- Todo processo de pesquisa deve gerar um relatório (O resultado não precisa ser positivo ou mesmo conclusivo, o relatório é um checkpoint).
- Tenha Backup
- Use Git

## Dicas em Feature Engineering
Feature engineering consiste em criar ou remover features em um dataset procurando melhorar o entendimento do problema pelo algoritmo a ser utilizado. Se feito corretamente, pode melhorar a performance do modelo de Machine Learning, um caso especialmente conhecido é que geralmente é nesta fase onde os modelos campeões das competições do Kaggle se destacam. 

Um Survey - bastante técnico - em redução de dimensionalidade: [Link](https://arxiv.org/pdf/1403.2877.pdf)
### Técnicas

- **Eliminação de ruídos**
- **Generalização** Consiste em criar novas features a partir da generalização das features presentes. Ex.: Gato -> Felino -> Mamífero -> Animal | Cachorro -> Canino -> Mamífero -> Animal. Portanto existe um quoeficiente de similaridade entre gato e cachorro ao compartilhar características de mamíferos e de animais. É uma tecnica que requer bastante conhecimento de domínio.
- **Normalização**: Consiste no ajuste da escala das variáveis, geralmente sendo utilizada uma escala de 0 a 1 para todas as variáveis numéricas. 

- **Transformação**
  - *Discretizar*:
    - **Intervalos** Separação de variáveis em categorias baseadas em intervalo. Por exemplo categorizar idades em um intervalos de idades.
    - **Número de partições** No contexto de data mining aplicado a machine learning, particionamento consiste em quebrar o dataset em diversos pequenos datasets para treinamento, teste e validação.
    - **Entropia** É o nivel de incerteza de um certo dado/feature é utilizado para controlar como uma decision tree vai criar suas ramificações.
- Redução de dimensionalidade ([*source*] (https://www.knime.com/blog/seven-techniques-for-data-dimensionality-reduction))
    - Seleção de features
      - **Missing Values Ratio**: Colunas com muitos valores faltantes geralmente não carregam muita informação, esta técnica consiste em remover essas colunas a partir de um determinado ponto. Ex.: Mais de 15% faltante pode excluir.
      - **Low Variance Filter**: Colunas com pouca variação de conteúdo também carregam pouca informação. Para essas colunas, também pode-se definir uma barreira para eliminação, similar ao exemplo acima.
      - **High Correlation Filter**: Quando duas colunas são muito similares, ou tem tendências similares elas costumam carregar o mesmo tipo de informação, portanto uma delas pode também ser eliminada.
      - **Random Forests**: Além de classificação, podem ser utilizadas para extração de features. Uma abordagem seria criar diversas, (1000) Random Forests com poucos leveis (2~4) e selecionar poucas colunas para serem classificadas. As colunas que forem mais selecionadas para o primeiro split geralmente é uma feature significativa.
      - **Backwards feature extraction**: Esta técnica é um pouco mais trabalhosa. É utilizado o algoritmo que o usuário acha mais apropriado para o problema e são selecionadas todas as colunas *n*. Depois de treinar, guardar o resultado de erro. Após essa etapa, remover uma coluna *n-1* e treinar novamente. Eliminando as features que não impactarem significativamente no erro do treinamento.
      - **Forward feature selection**: Esta técnica utiliza justamente o processo contrário ao *Backwards feature extraction*, treinamos o algoritmo com uma feature e a cada treinamento adicionamos mais uma. As features que não impactarem na acurácia, não devem ser inseridas.
    - Componentes:
      - **Factor analysis**: Esta técnica tende a ser similar com o *High Correlation Filter* e com a ténica de *Generalização*, ela é utilizada para descrever a variabilidade entre observações em um numero potencialmente menor de fatores. Criando uma feature que pode representar um grupo maior de observações reduzindo a dimensionalidade do dataset.
      - **PCA**: *Principal component Analysis* Esta técnica consiste em utilizar um algoritmo que aplica transformações lineares na matriz de features para combinar features reduzindo sua dimensionalidade. Com isso esta técnica invariavelmente gera perda de interpretabilidade, em favor de redução, e muitas vezes até mesmo melhora a performance e acurácia do modelo. É importante ressaltar que todas as colunas devem ser normalizadas antes de serem inseridas em um algoritmo de PCA.
      - **ICA**: *Independent Component Analysis* É uma técnica estatística computacional focada em encontrar fatores escondidos em uma série de dados aparentemente aleatória. Assume-se que os dados são uma mistura linear de algumas variáveis latentes. A saída dessa técnica são novos componentes que podem ser utilizados no modelo de Machine Learning [Leia mais](https://www.cs.helsinki.fi/u/ahyvarin/whatisica.shtml).
    - Projection Based:
      - **ISOMAP** É uma tecnica similar ao *PCA* porém orientada ao mapeamento não linear de dados, como por exemplo, dados em uma esfera, é amplamente utilizado em video tracking e muitos outros tipos processamento de imagem e vídeo [Leia mais](http://benalexkeen.com/isomap-for-dimensionality-reduction-in-python/).
      - **t-SNE**: É mais um algoritmo de redução de dimensionalidade não linear para datasets multidimensionais para facilitar a visualização. Fazendo com que cada ponto multidimensional seja representado por um ponto em um espaço bi ou tri-dimensional onde objetos parecidos viram pontos próximos, e objetos menos parecidos se tornam pontos distantes porém com alta probabilidade. [Leia Mais](https://lvdmaaten.github.io/tsne/)
      - **UMAP**: Similar ao *t-SNE* também é utilizado para redução dimensional em espaços não lineares, mas não se limita a dimensionalidade do problema como seu antecessor.
