# Classificação Multiclasse de Vinhos

Projeto acadêmico de Machine Learning para classificação multiclasse de vinhos. Baseado no conteúdo do curso AWS Academy Machine Learning Foundations


## Objetivo

Usar a linguagem Python e a nuvem da AWS para avaliar o desempenho de modelos de aprendizado de máquina.

## Tecnologias

Preencha as versões utilizadas no ambiente em que o notebook for executado.

| Tecnologia/biblioteca | Versão utilizada |
|---|---|
| Python | 3.10.20 |
| pandas | 2.3.3 |
| NumPy | 1.26.4 |
| scikit-learn | 1.7.2 |
| XGBoost / imagem do SageMaker | 1.0-1 |
| SageMaker Python SDK | 2.189.0 |
| boto3 | 1.43.113 |
| Matplotlib | 3.10.9 |
| Seaborn | 0.13.2 |

## Dados

O dataset utilizado foi o Wine Class Classification


### Informações dos atributos

Cada vinho é representado no dataset por 13 atributos
- Alcohol
- Malic acid
- Ash
    - Alcalinity of ash
- Magnesium
    - Total phenols
- Flavanoids
- Nonflavanoid phenols
- Proanthicyanins
- Color intensity
- Hue
- OD280/OD315 of diluted wines
- Propline (target: class_0, class_1, class_2)

### Fonte dos dados

A base de dados utilizada neste projeto foi obtida na competição Wine-M, disponibilizada na plataforma Kaggle.

Fonte: Kaggle. Wine-M — Data. Disponível em: https://www.kaggle.com/competitions/wine-m/data. Acesso em: 23 out. 2026.

## Requisitos para execução

O notebook pode depender de:

- Python e bibliotecas listadas acima;
- arquivo(s) de dados obtidos da fonte indicada;
- conta e permissões AWS apropriadas, caso o código utilize SageMaker e S3;
- região AWS e recursos disponíveis compatíveis com o código.

A execução de jobs no SageMaker e a utilização do S3 podem gerar custos. Confira a configuração e os preços da AWS antes de executar.

## Como executar

1. Clone ou baixe este repositório.
2. Instale as bibliotecas e versões que você documentar acima.
3. Obtenha os dados da fonte indicada, respeitando os termos de uso.
4. Configure as dependências e os recursos externos exigidos pelo notebook.
5. Abra `notebooks/wine_multiclass_classification.ipynb` no Jupyter ou no ambiente apropriado.
6. Execute as células na ordem e verifique se os resultados são reproduzíveis.


## Resultados

**Métricas obtidas:** 
Para avaliar o modelo, foram utilizadas métricas que permitem analisar a quantidade de previsões corretas e os tipos de erros cometidos pelo classificador. Foram consideradas a acurácia (__accuracy__), a precisão (__precision__), a revocação (__recall__), a medida F1 (__F1-score__) e a matriz de confusão.

### Acurácia 
A acurácia representa a proporção de previsões corretas em relação ao total de exemplos avalidados. Essa métrica oferece uma visão geral do desempenho do modelo, mas deve ser interpretada em conjunto com outras medidas, especialmente quando as classes possuem quantidades diferentes de registros.

**Fórmula**

Acurácia = Número de previsões corretas / Total de previsões


O modelo obteve 95% de acurácia no conjunto de teste, composto por 80 registros.

### Precisão (Precision)
A precisão mede a proporção de previsões de uma determinada classe que realmente pertencem a ela. Em outras palavras, indica o quanto o modelo acerta quando prevê uma classe específica.

**Fórmula:**

Precisão = VP / (VP + FP)

Em que:

- **VP (verdadeiros positivos)**: exemplos da classe que foram identificados corretamente.
- **FP(falsos positivos)**: exemlos de outras classes que foram incorretamente classificados como pertencentes à classe analisada.

As métricas obtidas para cada classe foram:

**Revocação (Recall)**
A revocação, também conhecida como sensibilidade, mede a proporção de exemplos reais de uma classe que foram identificados corretamente pelo modelo.

**Fórmula:**

Recall = VP / (VP + FN)

Em que:

- **VP (verdadeiros positivos)**: exemplos da classe que foram identificados corretamente.
- **FN (falsos negativos)**: exemplos da classe que foram classificados incorretamente como pertencentes a outras classes.

### Medida F1 (F1-score)

O F1-score é a média harmônica entre precisão e revocação. Essa métrica combina as duas medidas em um único valor, permitindo avaliar o equilíbrio entre a confiabilidade das previsões e a capacidade de identificar os exemplos reais de uma classe.

**Fórmula:**

F1-score = 2 × (Precisão × Recall) / (Precisão + Recall)

Quanto mais próximo de 1 for o resultado, melhor será o equilíbrio entre precisão e revocação. O F1-score é especialmente útil quando se deseja analisar o desempenho de cada classe sem considerar apenas a acurácia geral.

| Classe | Precisão (Precision) | Recall | F1-Score | Registros reais |
|---|---|---|---|---|
| 0 | 96% | 100% | 98% | 26 |
| 1 | 100% | 87,5% | 93% | 32 |
| 2 | 88% | 100% | 94% | 22 |
| Média macro | 95% | 96% | 95% | 80 |
| Média ponderada | 95% | 95% | 95% | 80 |

### Médias macro e ponderada

Em problemas multiclasse, as métricas de precisão, revocação e F1-score podem ser resumidas por diferentes métodos de média.

- **Média macro (macro average)**: calcula a métrica separadamente para cada classe e, depois, obtém a média aritmética dos resultados. Todas as classes possuem o mesmo peso, independentemente da quantidade de exemplos.

- **Média ponderada (weighted average)**: calcula a média das métricas de cada classe considerando a quantidade de exemplos reais de cada uma. Assim, classes com mais registros têm maior influência no resultado final.

A análise dessas médias permite compreender melhor o desempenho geral do modelo, especialmente quando a distribuição dos exemplos entre as classes não é uniforme.

### Matriz de confusão
A matriz de confusão compara as classes reais com as classes previstas pelo modelo. Cada linha representa uma classe real, enquanto cada coluna representa uma classe prevista.

Os valores da diagonal principal correspondem às classificações corretas. Os valores fora dessa diagonal representam erros de classificação.

Neste projeto, a matriz de confusão complementa as métricas numéricas, permitindo identificar quais classes são reconhecidas com maior facilidade e onde ocorrem os principais erros.

![Matriz de confusão](/image-matriz_confusao.png)

- **Observações sobre os resultados:** 
O modelo apresentou acurácia de 95%, classificando corretamente 76 dos 80 registros do conjunto de teste.

A classe 0 apresentou precisão de aproximadamente 96% e recall de 100%, indicando que todos os registros reais dessa classe foram identificados corretamente.

A classe 1 apresentou precisão de 100% e recall de 87,5%. Embora todas as previsões dessa classe estivessem corretas, quatro registros reais da classe 1 foram classificados incorretamente: um como classe 0 e três como classe 2.

A classe 2 apresentou precisão de 88% e recall de 100%. Todos os registros reais dessa classe foram identificados, mas três registros de outras classes foram classificados incorretamente como classe 2.

De modo geral, os resultados indicam um bom desempenho do modelo nesse conjunto de teste, embora ainda existam erros na distinção entre as classes.


- **Limitações encontradas:** 
- Tamanho do conjunto de teste: a avaliação foi realizada com 80 registros. Portanto, os resultados não garantem o mesmo desempenho em outros conjuntos de dados.

- Distribuição dos erros: o modelo apresentou maior dificuldade para identificar corretamente todos os registros da classe 1 e para evitar previsões incorretas da classe 2.

- Avaliação limitada a uma execução: os resultados apresentados correspondem a uma única divisão dos dados, realizada com random_state=42. Outras divisões podem produzir métricas diferentes.

- Pré-processamento: os valores ausentes foram substituídos pela mediana calculada antes da divisão entre treino, validação e teste. Em uma avaliação mais rigorosa, essa mediana deveria ser calculada somente com os dados de treinamento, evitando o uso indireto de informações do conjunto de teste.

- Configuração do modelo: o treinamento utilizou 42 rodadas e a imagem XGBoost 1.0-1 do Amazon SageMaker. Outras configurações e versões podem apresentar resultados diferentes.


## Licença

MIT
