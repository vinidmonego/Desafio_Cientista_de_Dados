# Desafio Cientista de Dados

## Introdução
Este projeto tem como objetivo prever e identificar quais equipamentos terão falha utilizando técnica de Machine Learning em um caso de
manutenção preditiva na indústria. Os conjuntos de dados usados para este projeto foram obtidos diretamente do desafio proposto. O projeto usa a linguagem Python no Jupyter Notebook. Os pacotes utilizados para realizar o projeto se encontram em um arquivo de texto 'requirements' deste repositório.

## Contextualização
Manutenção preditiva é um acompanhamento contínuo de um ou mais equipamentos na indústria com o intuito de tentar definir seu estado futuro, por meio de dados coletados ao longo do tempo. Os dados podem ser coletados por sensores específicos para vibração, temperatura, vazão, pressão, torque e entre outros a depender do tipo do equipamento a ser analisado. Este acompanhamento pode ser muito útil para reduzir tempo de inatividade não plenejada e melhorar a produtivade como um todo. A manutençaõ preditiva pode ajudar nos seguintes objetivos:
* Melhorar a confiabilidade do equipamento;
* Aumentar a eficiência;
* Melhorar a segurança;
* Reduzir custos de manutenção;
* Melhorar o gerenciamento de ativos.

Há deiversas abordagens para implementar uma solução de manutenção preditiva, dependendo do tipo de equipamento que está sendo monitorado e dos recursos disponíveis. Neste caso, a abordagem escolhida é a modelagem preditiva, a qual consiste em utilizar algoritmos de machine learning para analisar dados históricos sobre o equipamento para identificar padrões que possam incitar em uma falha. Isto é realizado através dos dados dos sensores, bem como dados operacionais e registros de manutenção, criando assim um conjutno de dados utilizáveis para serem analisados.

## Dataset
São dispostos dois datasets para resolução do desafio. O primeiro de treino, onde serão utiizados para realizar o treinamento do algoritmo de Machine Learning. Este dataset é composto por 6667 linhas e 9 colunas de informação e a variável a ser prevista: failure-type. O segundo dataset é de teste, que contém 3333 linhas e 8 colunas, não possuindo a coluna failure_type. Este dataset será utilizado com o algoritmo de Machine Learning já treinao para prever a coluna que falta juntamente com a identificação das máquinas com falhas.

## Exploração dos Dados
Apóse ler os dados de treino, é possível observar através de gráficos e estatística o comportamento destes. Para criar o EDA (Exploratory Data Analysis) foi utilizado o Pandas Profiling para econominzar tempo e poder extrair alguns insights. O EDA pode ser encontrado através deste link: <a
href="https://nbviewer.org/github/vinidmonego/Desafio_Cientista_de_Dados/blob/main/Desafio_-_Cientista_de_Dados_Classificacao.ipynb" title="Clique e acesse agora!" target="_blank">Link no nbviewer</a>
Através do histograma de distribuição de classe é possível notar que a distribuição dos dados é muito desiquilibrada.
Para explorar a relação de diferentes features com a variável alvo, criaram-se gráficos de dispersão. É possível notar que falhas tendem ser correlatas com valores de torque, que estão próximos do máximo ou do mínimo. Além disso também se fez a análise de correlação de feature através de um heatmap para saber quais variáveis são positivamente ou negativamente correlacionadas umas com as outras e em que grau. Nota-se no mapa uma forte correlação positiva entre as features 'air_temperature_k' e 'process_temperature', fazendo sentido pois uma alta temperatura de processo, também aquecerá o ar ao redor da máquina. Porém para as features 'rotational_speed_rpm' e 'torque_nm' há uma forte correlação negativa.

## Preparação dos dados
Neste passo, os dados de treino são preparados para treinamento do modelo de Machine Learning. Aqui se faz a codificação dos dados categóricos, ou seja, a variável alvo 'failure_type', em formato inteiro para que os dados com valores categóricos convertidos possam ser fornecidos aos diferentes modelos de Machine Learning. Foram trocados então:

* No Failure               -> 0
* Power Failure            -> 1
* Tool Waer Failure        -> 2
* Overstrain Failure       -> 3
* Random Failure           -> 4
* Heat Dissipation Failure -> 5

Os dados também foram divididos em treino e teste, cerca de 70% destes dados.

## Treinamento do Modelo
É importante denotar que este problema é um problema de classificação, onde serão previstoas classificadas as máquinas com defeito.
O modelo utilizado de classificação é o XGBoost, do qual usa uma série de modelos fracos e depois combina as previsões usando um boost de gradiente. O XGBoost usa um algoritmo de otimização para ajustar o peso de cada modelo no conjunto para melhorar a precisão geral da previsão. Pelos dados serem desiquilibrados, este modelo possibilita a utilização de pesos de amostra, ajudando a atenuar os efeitos do desiquilíbrio de classes no modelo.

## Avaliação do modelo
Nesta etapa, avalia-se a acurácia do modelo de classíficação no set de treino usando o método score. Gerou-se, também, um relatório de classificação, exibindo um resumo do desempenho do modelo com métricas de avaliação como precisão, recall e f1-score. 
O modelo aparenta ter um bom desempenho com uma alta precisão de 0,97 e um alto f1-score ponderado de 0,97.
Em seguida, criou-se a matriz de confusão para mostrar o número de previsões corretas e incorretas feitas pelo modelo para cada classe. O modelo fez um total de 1933 predicões corretas e um total de 54 predicões incorretas.

Obs: É possível visualizar estas etapas no Jupyter Notebook deste respositório.

Para finalizar, leu-se o conjuto de dados de teste e através deste foi possível prever e classificar os tipos de falhas neste novo dataset.
