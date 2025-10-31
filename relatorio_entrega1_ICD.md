# Relatório para a primeira entrega do Trabalho Prático de Introdução à Ciência dos Dados

## **1\. Introdução**

O projeto tem como foco a análise de partidas da Premier League, buscando, a partir do desempenho histórico de cada time, inferir possíveis resultados de confrontos futuros. O dataset utilizado contempla partidas da primeira divisão da liga inglesa entre as temporadas de 2019 e 2025\. Cada linha da tabela corresponde a uma partida, e suas colunas registram estatísticas gerais, como gols marcados pelo time mandante e visitante, número total de finalizações, cartões amarelos e vermelhos, escanteios e odds, valores numéricos que indicam a probabilidade de um resultado ocorrer e estão relacionados ao retorno financeiro oferecido pelas casas de apostas Bet365 e Pinnacle.

Por um lado, analisar a correlação entre essas variáveis pode auxiliar na tomada de decisões estratégicas ao realizar apostas online; por outro, permite avaliar a precisão das casas de apostas na definição das odds.

**2\. Descrição**

O dataset contém 2.452 partidas da Premier League, organizadas em 52 colunas, das quais selecionamos apenas as mais relevantes para o modelo, evitando redundâncias. Essas colunas podem ser agrupadas em quatro categorias principais.

**Informações Gerais da Partida:** incluem a divisão da liga, a data e horário do jogo, os times mandante e visitante, os gols marcados por cada time, o resultado final da partida (H para vitória do mandante, D para empate e A para vitória do visitante), os gols e resultado do primeiro tempo, e o árbitro responsável pela partida.

**Estatísticas de Jogo:** registram o desempenho das equipes em termos de finalizações totais, chutes ao gol, escanteios, faltas cometidas, cartões amarelos e vermelhos. Essas métricas permitem avaliar o estilo de jogo de cada time e sua performance em campo.

**Odds de Resultado:** contemplam as probabilidades de vitória do mandante, empate ou vitória do visitante fornecidas pelas casas de apostas Bet365 e Pinnacle, incluindo também as maiores e médias odds de cada resultado, além das probabilidades para que a partida tenha mais de 2.5 gols.

**Handicap Asiático:** contém as odds aplicadas para o handicap asiático, indicando as probabilidades ajustadas para vantagem ou desvantagem inicial do time mandante, incluindo valores máximos e médias fornecidos pelas casas de apostas

## **3\. Perguntas**

* Quantas partidas tiveram odds baixas para vitória de um time e esse time não venceu? Ou seja, quantas vezes o favorito não venceu.

O dataset apresenta informações sobre o resultado final da partida e as odds estabelecidas antes do jogo se iniciar. Uma odd baixa para esse evento indica uma alta expectativa de vitória do time e podemos identificar rapidamente quando essa expectativa foi subvertida.

* Quão boa é uma regressão linear para prever o número de gols marcados pelo time da casa usando estatísticas como finalizações, escanteios, cartões e as odds?

Podemos através de uma análise exploratória perceber a influência de cada atributo na predição dos gols, finalizações, sequência de vitórias, odds etc. Com uma análise exploratória, podemos identificar melhor quais atributos têm correlação com o número de gols e possíveis indicativos.

* Quais são os pares de times que apresentam estatísticas similares, mas têm diferença estatística significativa no número de gols marcados ou no resultado da partida?

Também na análise exploratória, podemos realizar agregações dos times e perceber as similaridades e nuances da performance entre eles.  

* Qual a média de gols em partidas com odds altas para empate? Empates são realmente imprevisíveis?

Por fim, podemos analisar a real precisão das odds como indicadores de resultados, tanto para os empates quanto resultados gerais, ou se elas são deturpadas em prol do lucro das casas de apostas.

## **4.Próximos passos**

Os próximos passos do projeto envolvem estruturar melhor nossa abordagem de análise e modelagem a partir do conjunto de dados disponível. Em primeiro lugar, realizaremos uma Análise Exploratória de Dados (EDA) para compreender a distribuição das variáveis, identificar possíveis outliers, verificar correlações e avaliar a presença de dados faltantes ou inconsistências. Essa etapa será fundamental para selecionar os atributos mais relevantes para responder às perguntas propostas.

Em seguida, será importante definir claramente o problema de predição que desejamos atacar, delimitando qual é a variável-alvo (por exemplo, número de gols do time mandante, probabilidade de vitória/empate/derrota de um confronto) e quais métricas de avaliação farão sentido para medir o sucesso do modelo (como acurácia, F1-score, RMSE ou outras, dependendo da natureza da tarefa).

Após a EDA e com o problema bem definido, podemos começar a separar os dados em conjuntos de treino, teste e validação e avaliar os melhores modelos para a tarefa. Depois partiremos para a seleção e comparação de algoritmos de Machine Learning (como regressão linear),  buscando entender quais apresentam melhor capacidade preditiva para o contexto do futebol.

Outro ponto a ser considerado será a engenharia de atributos, isto é, a criação de novas variáveis derivadas (por exemplo, média de gols por temporada, aproveitamento em casa/fora, ou diferenças de desempenho entre os times, sequência de vitórias), que podem enriquecer o poder explicativo dos modelos e acrescentar mais correlações.

Por fim, pretendemos interpretar os resultados obtidos, tanto do ponto de vista estatístico quanto prático, avaliando se as previsões podem auxiliar na análise das odds fornecidas pelas casas de apostas e se realmente capturam padrões relevantes nos dados da Premier League.
