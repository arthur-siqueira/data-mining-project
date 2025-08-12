# Projeto de Estatística Aplicada

## 🧑‍💻 Autor
- Arthur Siqueira (202121250031) - arthur.siqueira@academico.ifpb.edu.br 

## 🎯 Tema e Motivação  
Este projeto tem como objetivo classificar ações negociadas na B3 (Brasil, Bolsa, Balcão) em perfis de risco — conservadoras, moderadas ou agressivas — com base em indicadores como retorno médio e volatilidade anual. A partir dessa classificação, serão criadas carteiras de investimento simuladas, cujos desempenhos serão avaliados ao longo dos anos.

A motivação está no desafio enfrentado por investidores (especialmente iniciantes) ao selecionar ativos com base em seu perfil de risco. A aplicação de técnicas estatísticas e de agrupamento permite a construção de uma análise quantitativa clara e objetiva, contribuindo para decisões de investimento mais embasadas e conscientes.

## 📊 Conjunto de Dados Selecionado  
- **Nome do conjunto de dados:**  
  Brazilian Stock Market Data Warehouse (Ações da B3)
  
- **Fonte:**  
   Dados públicos da B3: https://www.b3.com.br/en_us/market-data-and-indices/
   Estrutura em formato Data Warehouse disponível em: https://www.kaggle.com/datasets/leomaurodesenv/b3-stock-indexes

- **Descrição breve:**  
  O conjunto contém dados históricos de preços de ações listadas na bolsa brasileira (B3), organizados em tabelas dimensionais e fato. As informações incluem preços de abertura, fechamento, máximos e mínimos diários, volume financeiro negociado e a classificação setorial das empresas.

- **Justificativa para a escolha:**  
   O dataset oferece um cenário realista e estruturado para análises financeiras multivariadas, permitindo cálculos estatísticos relevantes e aplicação de técnicas como clusterização e simulação de carteiras. Além disso, possibilita investigar o comportamento de ações por setor e perfil de risco.
---

## ❓ Perguntas ou Hipóteses  
- É possível classificar ações brasileiras em perfis de risco (conservadoras, moderadas e agressivas) com base em seus retornos e volatilidade?
- Como se comportam carteiras compostas por ações de diferentes perfis ao longo do tempo?
- Quais setores concentram os ativos com maior ou menor risco?

## 🔍 Metodologia  
- Merge de factStocks + dimCompany + dimTime; padronização de datetime e 1 registro/dia/empresa.
- Feature engineering: lags (1, 5, 20) e médias/desvios móveis (5, 20, 60) com shift(1).
- Split temporal: treino ≤ 31/12/2014; teste 2015–2020.
- Modelos: ARIMA(1,1,1) para Banco do Brasil; Gradient Boosting (GBR) e MLP para PETROBRAS e VALE.
- Métricas: RMSE, MAE e MAPE; exportação de CSVs (Real vs Previsto).

## 🛠️ Ferramentas Utilizadas  
- Linguagem: Python (Jupyter/Colab).
- Bibliotecas: pandas, numpy, matplotlib/seaborn; statsmodels (ARIMA), scikit-learn (GBR, MLP, StandardScaler).

## 📈 Resultados  
- Banco do Brasil (ARIMA): MAPE ≈ 29,99% (benchmark).
- PETROBRAS: MLP melhor — MAPE ≈ 8,89% (GBR ≈ 17,54%).
- VALE: GBR melhor por MAPE — ≈ 2,81% (MLP ≈ 3,14%).
- CSVs gerados com Real e Previsto para 2015–2020.

## 📌 Conclusões  
- O ativo influencia o modelo vencedor (MLP em PETROBRAS; GBR em VALE).
- O pipeline temporal e as features sem vazamento são decisivos.
- O ARIMA cumpriu o papel de benchmark; métodos supervisionados superaram-no em PETR/VALE.

## ⚠️ Limitações e Trabalhos Futuros  
- preços possivelmente não 100% ajustados a desdobramentos/proventos.
- Sem variáveis exógenas (Ibovespa, USD/BRL, Selic); tuning limitado; sem walk-forward.
- Próximos passos: usar preço ajustado/log-retornos e incluir exógenas.
---

