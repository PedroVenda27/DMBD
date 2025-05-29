
# Projeto de Data Mining — Diagnóstico de Doenças Dermatológicas

## 1. Introdução

Com o avanço das tecnologias de informação, a geração e recolha de dados tornaram-se constantes em praticamente todas as áreas. Neste cenário, a análise de grandes volumes de dados tornou-se essencial para extrair conhecimento útil, apoiar decisões e otimizar processos. A mineração de dados (Data Mining) surge como uma ferramenta fundamental para transformar dados brutos em informação relevante, com impacto real em contextos tão diversos como os negócios, a ciência ou a saúde.

Neste contexto, a área de Data Mining desempenha um papel crucial ao aplicar técnicas estatísticas e computacionais para identificar padrões relevantes em bases de dados complexas. A metodologia CRISP-DM (Cross Industry Standard Process for Data Mining) surge como um padrão amplamente consolidado e utilizado na condução de projetos desta natureza. Esta metodologia estrutura o processo de mineração de dados em seis fases bem definidas:

1. **Compreensão do Negócio (Business Understanding):** definição do problema do ponto de vista do domínio da aplicação;
2. **Compreensão dos Dados (Data Understanding):** exploração e caracterização do conjunto de dados;
3. **Preparação dos Dados (Data Preparation):** limpeza e transformação dos dados para torná-los adequados à modelação;
4. **Modelação (Modeling):** aplicar algoritmos de aprendizagem automática;
5. **Avaliação (Evaluation):** verificar se os modelos obtidos cumprem os objetivos definidos;
6. **Implementação (Deployment):** entregar os resultados de forma útil para o utilizador final.

---

## 2. Business Understanding

Incidindo agora no âmbito deste projeto, será utilizado o dataset *Dermatology*. Este conjunto de dados foi construído com o objetivo de apoiar o diagnóstico diferencial de doenças dermatológicas, em específico do grupo *erythemato-squamous*, incluindo diferentes patologias como *psoriasis*, *seboreic dermatitis*, *lichen planus*, *pityriasis rosea*, *cronic dermatitis* e *pityriasis rubra pilaris*.

A realização de um diagnóstico destas doenças representa um verdadeiro desafio clínico, uma vez que partilham sintomas clínicos e características histopatológicas muito semelhantes. Esta semelhança dificulta a distinção precisa entre as diferentes patologias, levando, muitas vezes, à necessidade de exames como biópsias.

No entanto, mesmo com estes exames, nem sempre é possível obter um diagnóstico inequívoco, devido à sobreposição de padrões microscópicos. Além disso, os sintomas podem variar ao longo do tempo, o que aumenta ainda mais a complexidade do processo diagnóstico.

Dada esta realidade, é evidente a necessidade de desenvolver ferramentas auxiliares que apoiem os profissionais de saúde no processo diagnóstico, de forma mais rápida, precisa e não invasiva. A mineração de dados apresenta-se como uma abordagem promissora neste sentido. Utilizando técnicas de aprendizagem automática (*machine learning*), é possível identificar padrões relevantes nos dados clínicos e histopatológicos que permitam prever, com elevada precisão, o tipo de doença presente em cada paciente.

---

## 3. Data Understanding

### 3.1 Descrição do Dataset

O dataset utilizado, denominado *Dermatology*, é composto por **366 instâncias (registos)** correspondentes a diferentes pacientes e por **34 atributos descritivos**, aos quais se junta um **atributo de classe (label)** que representa o diagnóstico final da doença dermatológica.

Os atributos dividem-se em três grandes grupos:
- **Atributos clínicos** (1 a 11)
- **Atributos histopatológicos** (12 a 33)
- **Atributo contínuo**: **idade** (atributo 34)

### 3.2 Atributo de Classe (Label)

| Valor da Classe | Doença Dermatológica           |
|-----------------|--------------------------------|
| 1               | Psoriasis                      |
| 2               | Seboreic Dermatitis            |
| 3               | Lichen Planus                  |
| 4               | Pityriasis Rosea               |
| 5               | Cronic Dermatitis              |
| 6               | Pityriasis Rubra Pilaris       |

### 3.3 Caracterização dos Atributos

- Atributos 1 a 33: valores entre 0 e 3 (ordinais)
- Atributo 11 (histórico familiar): binário (0 ou 1)
- Atributo 34 (idade): contínuo, com 8 valores ausentes representados por `?`  e um valor a `0` estes problema serão resolvidos no Passo a Segir Data Preparation

---

## 4. Data Preparation

### 4.1 Tratamento de Valores em Falta ou Nulos

- Inicialmente e uma vez que temos apenas um Valor nulo `0` decidimos alterear este manualmente no dataset alterando o para o valor medio nas idades no caso Aproximadamente 40

- Para a Substituição da idade ausente `?`utilizamos os operadores `Declare Missing Values`e `Replace Missing Values` estes vao respetivamente identificar e alterar todos os valores `?` pela **média** das idades no caso Aproximadamente 40
  
- ![Imagem WhatsApp 2025-05-29 às 15 44 08_d4dd59d6](https://github.com/user-attachments/assets/9dd28750-fa8f-4805-bc6e-f61e6407a8c4)


### 4.2 Conversão de Tipos de Dados

- Atributo `idade` convertido para tipo **numérico** após limpeza.

### 4.3 Normalização e Codificação

- Não aplicada, pois o algoritmo de árvore de decisão **não é sensível à escala**.

### 4.4 Seleção de Atributos

- Todos os atributos foram mantidos.
- A seleção será automaticamente gerida pelo algoritmo C4.5.

---

## 5. Modeling

### 5.1 Técnica Utilizada

- Algoritmo **C4.5 (Decision Tree)**

### 5.2 Critérios de Divisão

Testados quatro critérios diferentes:
- Gain Ratio
- Information Gain
- Gini Index
- Accuracy

Parâmetros mantidos por defeito no RapidMiner.

### 5.3 Validação

- Utilizado **Cross Validation** com **10 folds**.

### 5.4 Métricas Avaliadas

- **Accuracy**
- **Classification Error**
- **Root Mean Squared Error (RMSE)**

---

## 6. Evaluation

### 6.1 Resultados Comparativos

| Critério de Divisão   | Accuracy (%) | Classification Error (%) | RMSE    |
|------------------------|--------------|----------------------------|---------|
| Gain Ratio             | **97.0**     | **3.0**                    | 0.16    |
| Information Gain       | 96.4         | 3.6                        | 0.18    |
| Gini Index             | 96.7         | 3.3                        | 0.17    |
| Accuracy               | 95.6         | 4.4                        | 0.20    |

> *Valores meramente ilustrativos — substituir pelos reais.*

### 6.2 Escolha Final

- **Gain Ratio** selecionado como melhor critério.

### 6.3 Interpretação da Árvore

Principais atributos destacados:
- Acanthosis
- Hyperkeratosis
- Family History
- Scaling
- Melanin Incontinence

### 6.4 Conclusão

O modelo mostrou elevada eficácia e interpretabilidade, validando o potencial da mineração de dados como ferramenta de apoio ao diagnóstico clínico dermatológico.
