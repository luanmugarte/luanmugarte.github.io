---
layout: single
title:  "Análise textual das atas do Copom"
excerpt: "Análise multidimensional das atas publicadas sobre as reuniões do Comitê de Política Monetária."
toc: TRUE
toc_label: "Nesta página"
toc_icon: "cog"
header:
  image: /assets/images/banner.jpg
---

{% include toc icon="cog" title="Nesta página" %}


# Visão geral

Este projeto envolve a análise textual das atas publicadas pelo Comitê de Política Monetária (COPOM) do Banco Central do Brasil (BCB). Foram feitas análise que compreende a criação nuvem de palavras, análise de sentimento e modelagem de tópicos. Utilizou-se as atas publicadas em inglês, compreendendo o período de março de 2000 a março de 2022.

Todas as partes de extração, tratamento, análise e visualização dos dados foram feitos em R.

# Resumo

A análise textual proporcionou primeiras conclusões interessantes as atas do COPOM. A nuvem de palavras da última reunião indicam a preocupação com risco, . A análise de sentimento mostra uma predominância do tom mais negativo em relação ao positivo das atas do Copom, além de um aumento da incerteza após o início do governo Temer. Por fim, a modelagem de tópicos transmite a existência de governos que rompem ou apresentam continuidades em sua política econômica, além de trazer presidências do BCB que dão maior importância sobre temas distintos.

# Visualização dos dados

## Nuvem de palavras

Nuvem de palavras são uma forma de análise textual que trazem as palavras mais frequentes utilizadas em conjunto de 1 ou mais textos. Dessa forma, é possível verificar a importância de determinada palavras para esse texto. Adotou-se a convenção de mostrar palavras mais frequentes em tamanhos maiores. 

A nuvem de palavras da última reunião do Copom de março de 2022 encontra-se abaixo. Neste processo de extração da nuvem de palavras, a etapa de remoção das stopwords é essencial. Stopwords correspondem à um conjunto de palavras comuns em textos de uma determinada língua que não acrescentam informação relevante. Alguns artigos, preposições e verbos são usualmente retirados. A depender da experiência e objetivo da nuvem de palavras, stopwords customizadas podem ser adicionadas à esta lista.

![Nuvens de palavras]({{ "/assets/images/copom_text_analysis/wordcloud_custom_stopwords.png" }})

A primeira nuvem de palavras à esquerda foi criada sem o uso de stopwords. Verifica-se a importância dessa etapa, já que a palavra imensamente mais frequente foi 'the' (em português, o artigo 'a' ou 'o'). Isso não nos traz informação relevante e retira a importância de outras palavras relevantes, que ocorrem menos frequentemente (em verde e em pequeno tamanho).

A nuvem de palavras ao meio foi criada com o uso de stopwords "padrão", sem customização do autor. É possível verificar que a nuvem de palavras se tornou mais clara, apontando palavras que realmente caracterizam as atas do Copom como: inflação, comitê, copom, política, preço, cenário, monetário, entre outras. No entanto, essas são palavras usuais e já esperadas em uma ata do Copom. Elas não acrescentam informações sobre o conteúdo específico dessa ata.

Por último, a nuvem de palavras à esquerda foi elaborada com as stopwords "padrão" e com outras stopwords específicas. É possível verificar uma diferença significativa. As principais palavras em destaque são: risco, meta, expectativas, choque, petróleo, incerteza. Elas mostram o momento dessa ata: o conflito (palavra presente na nuvem) na Ucrânia implicou um choque de aumento do preço do petróleo, uma elevação da incerteza e, assim, dos riscos na economia. Isto representa também um risco para o não cumprimento da meta do Copom no ano que vem. Assim, para reforçar as expectativas de controle da inflação no futuro, eles decidiram por aumentar a taxa de juros (tighten) mais uma vez.

## Análise de sentimento
	
A análise de sentimento trata-se de extrair algum sentimento de um conjunto de 1 ou mais textos. Por exemplo, a frase "O dia está bonito" teria um sentimento positivo, pois a palavras bonito é classificado como um sentimento positivo e as outras palavras são classificadas como neutras. 

Geralmente, a análise de sentimento é feita com o uso de um dicionário de sentimentos elaborados previamente. Estes dicionários associam diversas palavras à um determinado sentimento e podem se concentrar em diversas áreas ou campos de conhecimento - economia, política, literatura, entre outros. 

Nesta pesquisa, foi utilizado o dicionário econômico de Loughran-McDonald. Nele, observamos 6 sentimentos possíveis: incerteza, litigioso, negativo, positivo, restritivo ou supérfluo. A tabela abaixo traz alguns exemplos:


| <p align='center'>  Sentimento  </p>  | <p align='center'> Palavras </p>   |
|:------:|:------:|
| Negativo   | Acidente, acusação   |
| Positivo   | Melhor, beneficiar   |
| Incerteza   | Cautela, confundir  |
| Restritivo  | Limitado, compromisso   |
| Supérfluo  | Assimilar, bifurcação   |
| Litigioso   | Alegação, advogado   |

Abaixo, constam as análises de sentimento das atas do Copom separadas por presidente do Brasil ou do BCB. Dada a temporalidade semelhante dos mandatos dois tipos de presidentes, a diferença entre os dois gráficos é pequena.

![Análise de sentimento por presidente do Brasil]({{ "/assets/images/copom_text_analysis/Sentiment_each_BR_pres.png" }})

![Análise de sentimento por presidente do BCB]({{ "/assets/images/copom_text_analysis/Sentiment_each_BCB_pres.png" }})

Algumas primeiras impressões podem ser notadas. Primeiramente, verifica-se um tom mais negativo que positivo das atas do Copom.  Em segundo lugar, percebe-se um aumento do sentimento de incerteza após o primeiro governo Temer, possivelmente relacionado com a recessão e lenta recuperação econômica desde então. Por fim, também é possível notar uma redução do sentimento litigioso após o governo Temer.

## Modelagem de tópicos

A modelagem de tópicos envolve o uso de técnicas de aprendizado em máquina para a extração de tópicos (assuntos) específicos em um determinado texto para um conjunto de textos. Nesta pesquisa, foi utilizada a técnica de Latent Dirichlet allocation (LDA), procurando extrair 6 tópicos das atas do Copom. 

O gráfico abaixo mostra as 20 palavras mais frequentes nos 6 tópicos. Essa etapa da análise textual das atas do Copom está em desenvolvimento e novas stopwords necessitam ser incorporadas para a melhoria da modelagem de tópicos.

No entanto, algumas conclusões inicias podem ser extraídas. Por exemplo, o tópico 2 aparenta tratar da economia real (industria e produção) e crescimento (expansão, cresceu, aumentou, elevou, expandiu). O tópico 5 apresenta uma relação forte com o dólar, preços administrados e a necessidade de ações. O tópico 6 apresenta um cenário de riscos e de ajustes/reformas.

![Palavras por tópico]({{ "/assets/images/copom_text_analysis/Words_per_topic.png" }})

Partindo desses tópicos, é feita a análise de tópicos por presidências. É possível ver alguns movimentos claros na predominância dos tópicas nas presidências, indicando o estado da economia e do governo. Por exemplo, o tópico 5 preocupado com o dólar, setor externo e os preços administrado é predominante ao final do governo FHC, em que houve uma forte desvalorização cambial e crescimento forte de preços administrado e a crise energética de 2001. O tópico 2 é predominante entre 2004 e 2007, em que a economia cresceu em taxas comparativamente altas. Por fim, o tópico 6 que exprime riscos e reformas é identificado como dominante nos governos Temer e Bolsonaro, em que se aprovaram a Reforma Trabalhista e da Previdência.

![Tópicos por presidente]({{ "Topic_per_BCB_president.png" }})

# Conclusão

A análise textual do Copom podem trazer insights interessantes das atas do Copom. As diversas ferramentes disponíveis - nuvem de palavras, análise de sentimento e modelagem de tópicos - são complementares e podem mostrar diferentes lados de um mesmo objeto de estudo. No entanto, verifica-se a importância das etapas anteriores de extração e tratamento dos dados, além do aprimoramento dos stopwords. 


# Código

O código para todo o tratamento, análise e visualização dos dados podem ser disponibilizados com solicitação ao autor.