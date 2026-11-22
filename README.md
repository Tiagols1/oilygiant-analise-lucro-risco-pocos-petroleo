# Seleção de Regiões para Novos Poços de Petróleo com Regressão Linear e Bootstrapping (OilyGiant)

Projeto desenvolvido na **Sprint 10** da formação em Data Science (TripleTen) para auxiliar a empresa **OilyGiant** a escolher a melhor região para abrir **200 novos poços de petróleo** a partir de **500 pontos** analisados por exploração.

## Regras de Negócio e Parâmetros
- **Orçamento total:** US$ 100 milhões para 200 poços (**US$ 500.000** por poço).
- **Receita:** **US$ 4.500** por unidade (1.000 barris), ou US$ 4,50 por barril.
- **Ponto de equilíbrio (*breakeven*):** **111,11 mil barris** de média por poço (22.222,22 mil barris somando os 200 poços).
- **Critério de risco:** risco de prejuízo **inferior a 2,5%** em simulação via *bootstrapping* (1.000 amostras com reposição de 500 poços).

## Etapas e Principais Resultados
1. **Preparação dos dados:** três regiões (`geo_data_0.csv`, `geo_data_1.csv` e `geo_data_2.csv`) com 100.000 registros cada, sem valores nulos. A coluna `id` foi removida das *features* e o `StandardScaler` foi aplicado apenas no conjunto de treino (divisão 75:25) para evitar *data leakage*.
2. **Modelagem (`LinearRegression`):**
   - **Região 0:** média prevista de **92,40 mil barris** | REQM: **37,76 mil barris**
   - **Região 1:** média prevista de **68,71 mil barris** | REQM: **0,89 mil barris**
   - **Região 2:** média prevista de **94,77 mil barris** | REQM: **40,15 mil barris**
3. **Lucro potencial (Top 200 poços na validação completa):**
   - **Região 0:** **US$ 33.591.411,14**
   - **Região 2:** **US$ 25.985.717,59**
   - **Região 1:** **US$ 24.150.866,97**
4. **Análise de risco (*Bootstrapping* — 1.000 iterações de 500 poços):**
   - **Região 0:** lucro médio de **US$ 3.995.754,78** | IC 95%: `(US$ -1.104.678,95 a US$ 8.974.603,28)` | Risco de prejuízo: **6,00%**
   - **Região 1:** lucro médio de **US$ 4.520.488,91** | IC 95%: `(US$ 616.844,80 a US$ 8.453.401,78)` | Risco de prejuízo: **1,50%**
   - **Região 2:** lucro médio de **US$ 3.750.099,03** | IC 95%: `(US$ -1.447.667,27 a US$ 8.883.904,04)` | Risco de prejuízo: **8,00%**

## Recomendação Final
Recomenda-se investir na **Região 1**. Embora a Região 0 tenha apresentado maior lucro bruto considerando toda a validação de uma só vez, o alto erro do modelo (REQM de 37,76) eleva o risco de prejuízo para **6,00%** na simulação realista de 500 pontos. A **Região 1** apresenta altíssima precisão preditiva (REQM de **0,89**), maior lucro médio (**US$ 4,52 milhões**), intervalo de confiança de 95% inteiramente positivo e risco de prejuízo de **1,50%** (abaixo do limite de 2,5%).

## Como Executar
1. Clone o repositório e instale `numpy`, `pandas` e `scikit-learn`.
