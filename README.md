# MVP de Machine Learning - Precificação de Diárias por Temporada no Rio de Janeiro

Este repositório contém o desenvolvimento de um Produto Mínimo Viável (MVP) focado na estimativa inteligente de preços de diárias de imóveis por temporada na cidade do Rio de Janeiro. O objetivo principal do projeto é capturar as nuances socioeconômicas e geográficas da malha urbana carioca, transformando dados brutos em estimativas financeiras confiáveis para novos anfitriões.

## 📁 Estrutura do Repositório

* **`notebooks/`**: Contém o pipeline completo de Ciência de Dados executado no Google Colab (`.ipynb`), englobando desde a análise exploratória até a otimização dos modelos.
* **`data/`**: Diretório contendo a base de dados histórica utilizada para o treinamento e teste dos modelos preditivos.

## 📊 Desempenho e Resultados Finais

O modelo definitivo foi desenvolvido utilizando o algoritmo **Gradient Boosting Regressor**, otimizado via busca estocástica parametrizada (`SEED = 42`). Diante de dados completamente inéditos (*Holdout*), a solução apresentou excelente capacidade de generalização e estabilidade.

### Critério de Sucesso de Negócio
O objetivo de negócio era superar um ganho de 20% de performance preditiva em relação ao benchmark trivial de mercado (chute cego baseado na mediana de preços). O modelo superou a meta com segurança, reduzindo o erro quadrático e entregando os seguintes indicadores consolidados:

* **Ganho Real de Performance:** **21,96%** de evolução sobre a mediana de mercado.
* **Coeficiente de Determinação ($R^2$ Teste):** **0.3478** (Variáveis estruturais explicam ~34,78% da variância do fenômeno).
* **Erro Médio Absoluto (MAE):** **R$ 192,56**
* **Raiz do Erro Quadrático Médio (RMSE):** **R$ 254,32** (Reduzido de R$ 325,86 do baseline trivial).
* **Erro Percentual Absoluto Médio (MAPE):** **44,81%**

## ⚠️ Limitações Conhecidas e Escopo do MVP

* **Underfitting Estrutural por Ausência de Dados Qualitativos:** O modelo atual utiliza exclusivamente variáveis estruturais e geográficas (localização, quantidade de quartos, banheiros e noites mínimas). Na plataforma do Airbnb, fatores subjetivos e qualitativos como padrão de acabamento interno, presença de comodidades críticas (ar-condicionado, piscina, Wi-Fi), nota de avaliação histórica e o selo de *Superhost* exercem forte impacto na precificação. 
* **Teto de Aprendizado:** O Coeficiente de Determinação ($R^2$) está estabilizado no teto estatístico de **34,78%** devido a esse viés estrutural da base nativa. Consequentemente, o modelo apresenta excelente acurácia na faixa de diárias econômicas e médias, mas tende a subestimar propriedades de altíssimo padrão (luxo/coberturas) por não possuir atributos que diferenciem o acabamento interno de dois imóveis vizinhos de mesmo tamanho.

## 🔮 Próximos Passos para Evolução

1. **Enriquecimento de Dados:** Realizar a raspagem (*scraping*) das features qualitativas e notas reputacionais dos anúncios para elevar o teto preditivo do modelo;
2. **Otimização Bayesiana:** Implementar frameworks de busca avançada de hiperparâmetros (como o *Optuna*);
3. **Deploy em Produção:** Envelopar o pipeline definitivo em uma arquitetura de API leve utilizando *FastAPI* para consumo em tempo real.

## 🛠️ Tecnologias e Boas Práticas Implementadas

* **Pipelines Automatizados:** Uso do `ColumnTransformer` do Scikit-Learn para centralizar o fluxo de pré-processamento (imputação e escalonamento), eliminando completamente o risco de vazamento de dados (*Data Leakage*).
* **Engenharia de Recursos:** Tratamento de alta cardinalidade categórica para bairros raros utilizando agrupamento por frequência (`min_frequency=0.01`).
* **Reprodutibilidade:** Fixação de semente estatística global (`SEED = 42`) e execução em ambiente de nuvem gerenciado (Google Colab).
