# Projeto: Analisando Máscara de Linguagem com BERT

## Introdução

Neste projeto, vamos explorar o modelo de linguagem BERT (Bidirectional Encoder Representations from Transformers) da Google, com foco em um modelo de **Masked Language Model** (MLM). Esse tipo de modelo é treinado para prever uma palavra "mascarada" em uma sequência de texto, com base no contexto das palavras ao seu redor.

### O que é BERT?

BERT é um modelo baseado na arquitetura **Transformer**, que utiliza um mecanismo de atenção para entender a linguagem natural. O modelo foi treinado para prever palavras mascaradas em uma sequência, ajudando a entender o contexto das palavras. No caso do BERT, a entrada inclui palavras com um token de máscara [MASK], e o modelo tenta prever qual palavra melhor se encaixa nesse espaço.

BERT usa 12 camadas no modelo base, cada uma com 12 cabeçalhos de atenção, resultando em 144 cabeçalhos de atenção no total.

## Objetivos do Projeto

Este projeto é dividido em duas partes principais:

1. **Utilizar a biblioteca Transformers da Hugging Face**: Usaremos o BERT para prever palavras mascaradas em frases e gerar diagramas visualizando os pesos de atenção de cada cabeçalho de atenção.
2. **Analisar os diagramas de atenção**: Após gerar os diagramas, vamos investigar o que os cabeçalhos de atenção estão focando ao tentar entender a linguagem.

## Como Funciona o Código

### 1. Entrada de Texto

No programa `mask.py`, o usuário deve fornecer um texto de entrada contendo um token de máscara `[MASK]`, representando a palavra que o modelo precisa prever. O modelo é alimentado com tokens através da classe `AutoTokenizer` da biblioteca Transformers.

### 2. Tokens e IDs

O modelo BERT usa tokens para representar palavras. Cada token tem um ID único. O token especial `[MASK]` tem um ID correspondente específico. Outros tokens como `[CLS]` e `[SEP]` são usados para marcar o início e o fim de uma sequência, respectivamente. Quando uma palavra não pode ser representada por um único token, o BERT divide a palavra em múltiplos tokens.

### 3. Predição e Visualização

Usamos a classe `TFBertForMaskedLM` para realizar a predição do token mascarado. O modelo é alimentado com os tokens da entrada e tenta prever os tokens mais prováveis para substituir o token mascarado.

### 4. Visualização dos Pesos de Atenção

O programa gera diagramas que visualizam os valores de atenção para cada um dos 144 cabeçalhos de atenção do modelo BERT. Estes diagramas são úteis para entender o que o modelo está "atentando" ao processar o texto.

### Funções a Implementar

- **get_mask_token_index**: Recebe o ID do token de máscara e os tokens de entrada. Retorna o índice do token de máscara.
- **get_color_for_attention_score**: Recebe um valor de atenção entre 0 e 1 e retorna um valor RGB para representar a intensidade da atenção no diagrama.
- **visualize_attentions**: Gera diagramas de atenção para cada cabeçalho de atenção, usando a função `generate_diagram`.

### Análise dos Diagramas

Uma vez que os diagramas de atenção são gerados, podemos analisá-los para entender quais palavras o modelo está observando. Por exemplo:

- **Exemplo 1**: O cabeçalho de atenção da camada 3, cabeça 10, parece se concentrar nas palavras que vêm imediatamente depois de uma palavra. Isso pode ser útil para entender o contexto imediato ao redor de uma palavra.
- **Exemplo 2**: O cabeçalho de atenção da camada 4, cabeça 11, parece se concentrar na relação entre advérbios e os verbos que eles modificam, como visto no exemplo “O tartaruga se moveu lentamente sobre o [MASK]”.

## Especificação do Projeto

### Funcionalidades a Implementar

1. **get_mask_token_index**: Implementar a função para encontrar o índice do token de máscara.
2. **get_color_for_attention_score**: Implementar a função para gerar a cor do diagrama com base no valor de atenção.
3. **visualize_attentions**: Implementar a função para gerar diagramas de atenção para todos os cabeçalhos de atenção e camadas.

### Exemplo de Comando para Execução

Primeiro, instale as dependências com o seguinte comando:

```bash
pip3 install -r requirements.txt

