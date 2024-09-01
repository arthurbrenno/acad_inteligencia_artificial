# Redes Neurais e Perceptron: Aprofundamento e Implementação

## Sumário
1. [Introdução](#introdução)
2. [Estrutura Básica do Neurônio Artificial](#estrutura-básica-do-neurônio-artificial)
3. [Função de Ativação](#função-de-ativação)
4. [Algoritmo de Aprendizagem](#algoritmo-de-aprendizagem)
5. [Implementação do Perceptron](#implementação-do-perceptron)
6. [Limitações do Perceptron](#limitações-do-perceptron)
7. [Visualização do Processo de Aprendizagem](#visualização-do-processo-de-aprendizagem)
8. [Considerações Práticas](#considerações-práticas)

## Introdução

Nesta aula, aprofundamos nosso entendimento sobre redes neurais artificiais, focando especificamente no modelo do Perceptron. Exploramos sua estrutura, funcionamento, implementação e limitações, proporcionando uma base sólida para compreender modelos mais complexos.

## Estrutura Básica do Neurônio Artificial

O neurônio artificial, base das redes neurais, é composto por:

1. **Entradas**: Representadas por $x_1, x_2, ..., x_n$
2. **Pesos**: Representados por $w_1, w_2, ..., w_n$
3. **Bias**: Representado por $w_b$ (geralmente -1)
4. **Função de soma**: $\sum_{i=1}^n w_i x_i - w_b$
5. **Função de ativação**: Aplicada ao resultado da soma

### Representação Matemática

A saída de um neurônio pode ser representada como:

$y = f(\sum_{i=1}^n w_i x_i - w_b)$

onde $f$ é a função de ativação.

## Função de Ativação

A função de ativação introduz não-linearidade ao modelo, permitindo que a rede neural aprenda padrões mais complexos. Na aula, focamos na função degrau:

f(x) =
\left\{
\begin{array}{ll}
1 & \text{if } x \geq 0 \\
0 & \text{if } x < 0
\end{array}
\right.

Esta função é simples, mas limitada. Em redes mais avançadas, funções como sigmoid, tanh ou ReLU são mais comumente usadas.

## Algoritmo de Aprendizagem

O processo de aprendizagem do Perceptron envolve ajustar os pesos para minimizar o erro entre a saída prevista e a saída desejada.

### Regra de Atualização de Pesos

$w_i(t+1) = w_i(t) + \eta (d - y) x_i$

Onde:
- $w_i(t+1)$ é o peso atualizado
- $w_i(t)$ é o peso atual
- $\eta$ é a taxa de aprendizagem (geralmente 0.1 a 0.01)
- $d$ é a saída desejada
- $y$ é a saída atual do neurônio
- $x_i$ é a entrada correspondente

### Derivada de Decaimento

O conceito de "derivada de decaimento" mencionado na aula refere-se à busca do ponto mínimo da função de erro. Visualmente, isso pode ser imaginado como uma bola descendo um vale, onde o ponto mais baixo representa o estado ótimo de aprendizagem.

## Implementação do Perceptron

A implementação do Perceptron envolve os seguintes passos:

1. Inicialização dos pesos (geralmente com valores aleatórios entre 0 e 1)
2. Para cada amostra de treinamento:
   a. Calcular a saída do neurônio
   b. Comparar com a saída desejada
   c. Atualizar os pesos se houver erro
3. Repetir o processo por um número definido de épocas ou até atingir um critério de parada

### Exemplo de Implementação (Pseudocódigo)

```scilab
// Defina os dados de entrada e saída (última coluna é a saída desejada)
dados = [
  -1  1  1  0;
  -1  1  0  0;
  // Adicione mais linhas conforme necessário
];

// Inicialize os parâmetros
taxa_aprendizado = 0.1;
epocas = 100;
[m, n] = size(dados); // m é o número de amostras, n é o número de colunas (entradas + saída)

// Inicialize os pesos (incluindo o bias)
pesos = rand(1, n); // n pesos, incluindo o bias

// Treinamento do Perceptron
for epoca = 1:epocas
    for i = 1:m
        x_i = dados(i, 1:$-1); // Pegue as entradas (todas as colunas exceto a última)
        y_i = dados(i, $);     // Pegue a saída desejada (última coluna)
        
        // Calcule o produto escalar (incluindo o bias)
        produto_escalar = sum(pesos(1:$-1) .* x_i) + pesos($); // Soma do produto das entradas e pesos + bias
        
        // Função de ativação
        if produto_escalar >= 0 then
            y_predito = 1;
        else
            y_predito = 0;
        end
        
        // Calcule o erro
        erro = y_i - y_predito;
        
        // Atualize os pesos (incluindo o bias)
        for j = 1:(n-1)
            pesos(j) = pesos(j) + taxa_aprendizado * erro * x_i(j);
        end
        pesos($) = pesos($) + taxa_aprendizado * erro * 1; // Atualiza o bias
    end
end

// Exiba os pesos finais
pesos
```

## Limitações do Perceptron

O Perceptron tem limitações significativas:

1. **Linearidade**: Só pode resolver problemas linearmente separáveis.
2. **XOR Problem**: Não pode resolver o problema do XOR, que não é linearmente separável.

### O Problema do XOR

O XOR (OU exclusivo) é definido como:

| x1 | x2 | Saída |
|----|----|----|
| 0  | 0  | 0  |
| 0  | 1  | 1  |
| 1  | 0  | 1  |
| 1  | 1  | 0  |

Este problema não pode ser resolvido por um único Perceptron, pois não existe uma única linha reta que possa separar os casos de saída 0 e 1.

## Visualização do Processo de Aprendizagem

Para visualizar o processo de aprendizagem, podemos plotar a linha de decisão do Perceptron em um gráfico 2D:

1. A equação da linha de decisão é: $x_1 w_1 + x_2 w_2 - w_b = 0$
2. Reorganizando, temos: $x_2 = (-w_1/w_2)x_1 + (w_b/w_2)$

Esta é uma equação da forma $y = mx + b$, onde:
- $m = -w_1/w_2$ (inclinação)
- $b = w_b/w_2$ (intercepto)

Plotando esta linha a cada iteração, podemos ver como o Perceptron ajusta sua decisão ao longo do tempo.

## Considerações Práticas

1. **Taxa de Aprendizagem**: Uma taxa muito alta pode causar oscilações e dificultar a convergência, enquanto uma taxa muito baixa pode tornar o aprendizado muito lento.

2. **Inicialização de Pesos**: A inicialização aleatória dos pesos pode afetar a velocidade de convergência e até mesmo o resultado final.

3. **Normalização de Dados**: Normalizar as entradas para um intervalo comum (como [0,1]) pode melhorar significativamente o desempenho e a estabilidade do treinamento.

4. **Overfitting vs Underfitting**: É importante monitorar o desempenho do modelo em um conjunto de validação para evitar overfitting (memorização dos dados de treinamento) ou underfitting (modelo muito simples que não captura a complexidade dos dados).

5. **Extensões do Perceptron**: Para superar as limitações do Perceptron simples, foram desenvolvidos modelos mais avançados como o Perceptron Multicamadas (MLP) e, eventualmente, as redes neurais profundas.

## Conclusão

O Perceptron é um modelo fundamental na história e no entendimento das redes neurais. Embora tenha limitações significativas, seu estudo fornece insights valiosos sobre os princípios básicos de aprendizado de máquina e serve como base para compreender modelos mais complexos e poderosos.