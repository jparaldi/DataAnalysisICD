# Plano de Testes de Hipótese para a Premier League (2019-2025)

Este documento descreve um conjunto de testes de hipótese alinhados às perguntas de negócio registradas em `relatorio_entrega1_ICD.md`, considerando o fluxo de preparação de dados do notebook `eda.ipynb`, o contexto do notebook legado `initial.ipynb` e a legenda oficial de colunas (`legenda_colunas.md`). Todas as análises devem ser documentadas em notebooks com textos em português e reutilizando o dataset consolidado `data/premier_completo_19_25.csv`.

## Premissas Gerais de Dados

- Carregar `data/premier_completo_19_25.csv` com `pd.read_csv(..., dayfirst=True)` e converter `Date` para `datetime64[ns]` e `FTR` para `category` antes da modelagem.
- Garantir que o dataframe contenha apenas as colunas definidas em `selected_features` (ver `eda.ipynb`); utilizar `assert set(df.columns) == set(selected_features)` como checagem rápida.
- Tratar valores faltantes removendo partidas com `NaN` em `P>2.5` e `P<2.5` (10 linhas) salvo justificativa explícita para imputação.
- Converter variáveis numéricas (gols, finalizações, odds etc.) para tipos numéricos (`int`/`float`) e padronizar nomes de novas features com prefixos `home_`, `away_` ou `diff_`.
- Documentar qualquer derivação de atributos adicionais na `legenda_colunas.md` se forem incorporados ao pipeline definitivo.

## H1 — Quantas vezes o favorito não venceu?

### Objetivo (H1)

Medir a taxa de fracasso dos favoritos segundo odds pré-jogo e testar se ela difere de um patamar de referência.

### Hipótese estatística (H1)

- H0: A proporção de partidas em que o favorito (menor odd entre Bet365 e Pinnacle) vence é ≥ 70% (referência comum em apostas esportivas).
- H1: Essa proporção é < 70%, indicando que os favoritos falham com frequência relevante.

### Procedimento (H1)

1. Selecionar colunas `FTR`, `B365H`, `B365D`, `B365A`, `PSH`, `PSD`, `PSA`.
2. Criar odds mínimas por resultado (`min_home`, `min_draw`, `min_away`) e identificar o favorito (`favourite_outcome`). Em empates de odds, marcar como `indefinido` e remover da amostra principal.
3. Codificar resultado real (`FTR`) para `home`, `draw`, `away`.
4. Calcular variável binária `favourite_won` para cada partida.
5. Aplicar teste z para proporção única comparando a taxa observada com 0.7 (utilizar `statsmodels.stats.proportion.proportions_ztest`).
6. Reportar intervalo de confiança (95%) e proporção observada por temporada para contextualização temporal.
7. Criar gráficos de barras com proporção por temporada e heatmap das odds médias por resultado.

### Cuidados (H1)

- Justificar por que 70% é referência (literatura ou fonte externa) ou adaptar H0 para uma taxa base calculada pelo próprio dataset (ex.: média histórica).
- Rodar análise de sensibilidade separando por casa de apostas (Bet365 e Pinnacle) para avaliar consistência.

## H2 — Regressão linear para prever gols do mandante

### Objetivo (H2)

Verificar se é possível explicar os gols do mandante com estatísticas de jogo e odds.

### Hipótese estatística (H2)

- H0: Um modelo linear com variáveis selecionadas não apresenta capacidade explicativa significativa (R² ajustado ≈ 0).
- H1: O modelo linear apresenta R² ajustado significativamente maior que 0, sugerindo relação linear útil.

### Procedimento (H2)

1. Garantir integridade de colunas numéricas (`HS`, `HST`, `HC`, `HF`, `HY`, `HR`, `B365H`, `PSH`, etc.).
2. Dividir dataset em treino (`2019-2023`), validação (`2023-2024`) e teste (`2024-2025`) respeitando o recorte temporal para evitar vazamento.
3. Preparar matriz de features contemplando:
   - Estatísticas de jogo (ex.: `HS`, `HST`, `HC`, `HY`, `HR`).
   - Odds pré-jogo (`B365H`, `PSH`, `AvgH`, `MaxH`, handicaps).
   - Variáveis derivadas possíveis: `home_shot_efficiency = HST / HS`, `home_card_rate = HY + HR`, documentando na legenda quando incorporadas.
4. Escalar features (StandardScaler) quando necessário e avaliar multicolinearidade via VIF, removendo colunas redundantes.
5. Ajustar regressão linear com `statsmodels` e avaliar significância individual das variáveis (p-valores < 0.05, com correção quando aplicável).
6. Verificar pressupostos do modelo (normalidade dos resíduos, homocedasticidade). Discutir transformações ou modelos alternativos (Poisson) se houver violações relevantes.
7. Testar H0 com base na significância global do modelo (teste F): rejeitar H0 se p-valor < 0.05 e R² ajustado > 0.15 (limiar sugerido, justificar). Registrar RMSE em cada split temporal.

### Cuidados (H2)

- Explicar que estatísticas de jogo são pós-evento; interpretar resultados como associação, não previsão pré-jogo.
- Reportar impacto de outliers (ex.: partidas com expulsões múltiplas) e testar robustez removendo-os.

## H3 — Times com estatísticas similares, mas gols ou resultados diferentes

### Objetivo (H3)

Identificar pares de equipes com estilo de jogo similar, porém diferenças significativas em gols marcados ou resultados.

### Hipótese estatística (H3)

- H0: Para times com perfil estatístico semelhante, não há diferença significativa no número de gols marcados por partida.
- H1: Mesmo com perfil estatístico semelhante, existem diferenças significativas de gols ou resultados entre times.

### Procedimento (H3)

1. Agregar dados por time e temporada para métricas médias: `HS`, `HST`, `HC`, `HF`, `HY`, `HR`, odds (`B365H`, `PSH`). Gerar dataframe `team_season_stats`.
2. Padronizar métricas (z-score) e aplicar clustering (K-Means ou Agglomerative) para obter grupos de times com estilo similar. Determinar número de clusters com `silhouette_score`.
3. Dentro de cada cluster, aplicar ANOVA unilateral (ou teste t de Welch quando apropriado) para comparar médias de gols (`FTHG`).
4. Para pares específicos, executar teste de diferença de médias (Welch t-test) ou teste de proporção de vitórias (`FTR`).
5. Complementar com teste de qui-quadrado para comparar distribuição de resultados dentro de cada cluster.
6. Visualizar boxplots de gols por time dentro do mesmo cluster e heatmap de distâncias entre times.
7. Rejeitar H0 quando p-valor < 0.05 indicando diferenças significativas em grupos homogêneos.

### Cuidados (H3)

- Documentar critérios de similaridade (features de clustering) e validar estabilidade do agrupamento com seeds diferentes.
- Garantir amostra suficiente por cluster; se necessário, consolidar temporadas ou reduzir dimensionalidade.

## H4 — Odds altas para empate e comportamento de gols

### Objetivo (H4)

Verificar se partidas com odds altas para empate apresentam comportamento distinto na distribuição de gols e na taxa real de empates.

### Hipótese estatística (H4)

- H0: A média de gols em partidas com odds de empate altas (percentil 75 de `B365D`) é igual à média em partidas com odds baixas (percentil 25).
- H1: As médias diferem, indicando que odds altas refletem padrão distinto de gols.

### Procedimento (H4)

1. Classificar partidas em faixas de odds de empate utilizando quantis de `B365D` (ou `PSD`): alta, média, baixa.
2. Calcular métricas `total_goals = FTHG + FTAG` e `goal_diff = abs(FTHG - FTAG)` para cada grupo.
3. Avaliar normalidade (Shapiro-Wilk) e homocedasticidade (Levene). Caso atendidas, aplicar ANOVA; se não, utilizar Kruskal-Wallis e testes post-hoc (Dunn).
4. Comparar taxa de empates reais (`FTR == 'D'`) entre grupos via teste de qui-quadrado ou z-test para proporções.
5. Construir gráficos (`sns.boxplot`, `sns.histplot`) para visualizar distribuição de gols por grupo.
6. Reportar tamanho de efeito (ex.: eta quadrado parcial ou Cliff's delta) para contextualizar a diferença.

### Cuidados (H4)

- Definir claramente o limiar de "odds altas" e executar análise de sensibilidade com cortes alternativos.
- Avaliar também o desvio padrão dos gols para medir dispersão e potencial imprevisibilidade.

## Organização da Entrega

- Estruturar `testes_de_hip.ipynb` com seções numeradas H1–H4, incluindo célula inicial para configurar ambiente (`pd.set_option("display.max_columns", None)`, conversões de tipo, etc.).
- Registrar interpretações em português ao final de cada seção e citar gráficos/tabelas relevantes.
- Atualizar `relatorio_entrega1_ICD.md` com achados principais e menção às hipóteses testadas.

## Próximos Passos Recomendados

1. Reexecutar `eda.ipynb` para confirmar que `data/premier_completo_19_25.csv` permanece coerente com `selected_features`.
2. Construir base auxiliar com métricas por time/temporada suportando a análise de clusters (H3).
3. Implementar as análises no `testes_de_hip.ipynb`, seguindo a ordem H1 → H4, garantindo notebooks limpos e executados sequencialmente.
4. Registrar resultados e conclusões no relatório oficial do projeto.
