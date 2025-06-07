# Classificação de Câncer de Mama: Comparativo de Modelos KNN e Regressão Logística

## 📝 Visão Geral do Projeto

Este projeto tem como objetivo principal desenvolver e comparar modelos de classificação para o diagnóstico de câncer de mama, utilizando o famoso dataset Breast Cancer Wisconsin. O foco está em avaliar o desempenho de dois algoritmos – K-Nearest Neighbors (KNN) como modelo baseline e Regressão Logística como um novo modelo comparativo – sob condições controladas, incluindo a simulação de ruído nos dados.

A análise segue uma metodologia rigorosa de avaliação, combinando a estratégia de holdout com validação cruzada para garantir a robustez das métricas de desempenho. Ao final, discutimos qual modelo se mostrou mais adequado para a tarefa, considerando métricas críticas para um contexto médico.

## 📊 Dataset

O projeto utiliza o dataset Breast Cancer Wisconsin (Diagnostic), disponível no scikit-learn. Este conjunto de dados contém características computadas a partir de uma imagem digitalizada de um aspirado por agulha fina (FNA) de uma massa mamária. O objetivo é classificar se a massa é maligna (cancerosa) ou benigna (não cancerosa).

## 🧠 Modelos Implementados

1 ) K-Nearest Neighbors (KNN)

  - Um classificador baseado na proximidade dos "vizinhos" mais próximos.

  - Utilizado como o nosso baseline de comparação.

2 ) Regressão Logística

  - Um modelo linear generalizado, robusto e interpretável para problemas de classificação binária.

  - Implementado como o novo modelo para comparação.

## ⚙️ Metodologia de Avaliação

Para garantir uma avaliação justa e robusta dos modelos, adotei a seguinte metodologia:

1 ) Pré-processamento de Dados:
   
Todos os dados foram padronizados usando StandardScaler para garantir que as features estivessem na mesma escala, o que é crucial para modelos baseados em distância como o KNN.

2 ) Introdução de Ruído:

Para simular condições do mundo real e testar a robustez dos modelos, adicionei um termo de ruído gaussiano (distribuição normal) aos dados padronizados. Isso permite avaliar o desempenho dos algoritmos em cenários com imperfeições nos dados.

3 ) Estratégia de Holdout + Validação Cruzada:

O dataset foi dividido inicialmente em conjuntos de treino (70%) e teste (30%) usando a estratégia de holdout. Uma random_state (semente aleatória) específica foi definida para garantir a reprodutibilidade dessa divisão. A mesma best_seed encontrada no TP2 (para o KNN sem ruído) foi usada para todas as divisões principais, assegurando uma comparação justa entre os modelos.

Dentro do conjunto de treino, utilizei a Validação Cruzada Estratificada (StratifiedKFold com 10 folds) em conjunto com GridSearchCV para encontrar os melhores hiperparâmetros (o k ideal para KNN e o C ideal para Regressão Logística). Isso minimiza o viés de uma única divisão de dados e garante que a proporção das classes seja mantida em cada fold.

4 ) Re-treinamento Final:

Após identificar os melhores hiperparâmetros através da validação cruzada, cada modelo foi re-treinado utilizando o conjunto completo de treino e esses hiperparâmetros otimizados.

5 ) Métricas de Avaliação:

  - A performance final de cada modelo (com e sem ruído, após o re-treinamento) foi avaliada no conjunto de teste (não visto) usando as seguintes métricas:
    - Acurácia: Proporção de previsões corretas.
    - Precisão (Precision): Quantas das previsões positivas estavam corretas.
    - Recall (Sensibilidade): Quantas das amostras positivas reais foram corretamente identificadas.
    - F1-score: Média harmônica de Precisão e Recall, útil para balancear ambas as métricas.
   
## 💻 Como Rodar o Código

### Para executar a análise e replicar os resultados, siga os passos abaixo:

Pré-requisitos

- Certifique-se de ter o Python instalado (preferencialmente versão 3.7+). 

- As bibliotecas necessárias estão listadas no arquivo requirements.txt.

1 ) Crie e ative um ambiente virtual (recomendado):

``` python -m venv venv ```

#### No Windows
```.\venv\Scripts\activate```

#### No macOS/Linux
```source venv/bin/activate```

2 ) Instale as dependências a partir do requirements.txt:

```pip install -r requirements.txt```

3 ) Instale o Jupyter Notebook dentro do seu ambiente virtual:

```pip install jupyter```

4 ) Selecione o ambiente criado para o Jupyter Notebook:

Após instalar o Jupyter, você precisa garantir que ele reconheça o kernel do seu ambiente virtual.

1. Inicie o Jupyter Notebook:

```jupyter notebook```

2. No seu navegador, o Jupyter abrirá. Navegue até o diretório onde seu .ipynb (arquivo do notebook) está localizado.
3. Ao abrir um notebook existente ou criar um novo, vá em Kernel (ou "Núcleo" em português) no menu superior, depois Change Kernel (ou "Mudar Núcleo") e selecione o ambiente venv que você criou. Ele geralmente aparecerá com o nome do seu ambiente (e.g., Python (venv)).

Alternativamente, se você usa VS Code, o processo é ainda mais simples:

1. Abra a pasta do seu projeto no VS Code.
2. Abra o arquivo .ipynb.
3. No canto superior direito da janela do notebook, clique em "Select Kernel" (ou no ícone de uma setinha para baixo).
4. Selecione a opção "Python Environments..." (ou "Ambientes Python...") e escolha o ambiente venv que você criou. O VS Code automaticamente configurará o kernel para você.

5 ) Execute o Jupyter Notebook:

Com o kernel correto selecionado, você pode rodar as células do seu notebook para ver a análise e os resultados.
