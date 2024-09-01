# Redes Neurais Multicamadas: Arquitetura e Treinamento com Implementação em Scilab

## Sumário
1. [Introdução](#introdução)
2. [Arquitetura de Redes Neurais Multicamadas](#arquitetura-de-redes-neurais-multicamadas)
3. [Função de Ativação Logística](#função-de-ativação-logística)
4. [Algoritmo de Retropropagação (Backpropagation)](#algoritmo-de-retropropagação-backpropagation)
5. [Implementação Prática em Scilab](#implementação-prática-em-scilab)
6. [Visualização do Treinamento](#visualização-do-treinamento)
7. [Aplicações Práticas](#aplicações-práticas)
8. [Considerações Finais](#considerações-finais)

## Introdução

As redes neurais multicamadas (também conhecidas como Perceptron Multicamadas ou MLP) são uma evolução do Perceptron simples, capazes de resolver problemas não-lineares como o XOR. Esta aula foca na arquitetura, treinamento e implementação dessas redes, com ênfase na implementação prática usando Scilab.

## Arquitetura de Redes Neurais Multicamadas

[Conteúdo mantido como no original]

## Função de Ativação Logística

[Conteúdo mantido como no original]

## Algoritmo de Retropropagação (Backpropagation)

[Conteúdo mantido como no original]

## Implementação Prática em Scilab

A implementação de uma rede neural multicamadas em Scilab envolve os seguintes passos:

1. Definição da arquitetura (número de camadas e neurônios)
2. Inicialização dos pesos
3. Implementação da propagação direta
4. Implementação da retropropagação
5. Treinamento da rede com um conjunto de dados

### Exemplo de Código em Scilab

```scilab
// Limpar ambiente e console
clear;
clc;

// Definir dados de entrada (XOR problem)
dados = [0 0 0; 0 1 1; 1 0 1; 1 1 0];

// Parâmetros da rede
NE = size(dados, 2) - 1;  // Número de entradas
NS = 2;  // Número de neurônios na camada oculta
NA = size(dados, 1);  // Número de amostras
taxa_aprendizagem = 0.1;
epocas = 1000;

// Inicialização dos pesos
WE = rand(NE+1, NS);
WS = rand(NS+1, 1);

// Função de ativação logística
function y = logistica(x)
    y = 1 ./ (1 + exp(-x));
endfunction

// Função de treinamento
function [WE, WS] = treinar_rede(dados, WE, WS, taxa_aprendizagem, epocas)
    for epoca = 1:epocas
        for am = 1:NA
            // Propagação direta
            X = [-1; dados(am, 1:NE)'];
            H = logistica(WE' * X);
            H = [-1; H];
            YS = logistica(WS' * H);
            
            // Retropropagação
            D = dados(am, NE+1) - YS;
            DS = D * YS * (1 - YS);
            DH = (WS(2:$) * DS) .* H(2:$) .* (1 - H(2:$));
            
            // Atualização dos pesos
            WS = WS + taxa_aprendizagem * DS * H;
            WE = WE + taxa_aprendizagem * X * DH';
        end
    end
endfunction

// Treinar a rede
[WE, WS] = treinar_rede(dados, WE, WS, taxa_aprendizagem, epocas);

// Testar a rede
for i = 1:NA
    X = [-1; dados(i, 1:NE)'];
    H = logistica(WE' * X);
    H = [-1; H];
    YS = logistica(WS' * H);
    printf("Entrada: [%d, %d], Saída: %.4f, Esperado: %d\n", dados(i,1), dados(i,2), YS, dados(i,3));
end
```

Este código implementa uma rede neural multicamadas para resolver o problema do XOR. Ele inclui a inicialização dos pesos, a função de ativação logística, o treinamento da rede e um teste final para verificar se a rede aprendeu corretamente.

## Visualização do Treinamento

Para visualizar o processo de treinamento em Scilab, podemos modificar a função de treinamento para armazenar o erro ao longo das épocas e então plotar:

```scilab
function [WE, WS, erros] = treinar_rede_com_erro(dados, WE, WS, taxa_aprendizagem, epocas)
    erros = zeros(epocas, 1);
    for epoca = 1:epocas
        erro_epoca = 0;
        for am = 1:NA
            // [Propagação direta e retropropagação como antes]
            
            erro_epoca = erro_epoca + D^2;
        end
        erros(epoca) = erro_epoca / NA;
    end
endfunction

// Treinar a rede e obter os erros
[WE, WS, erros] = treinar_rede_com_erro(dados, WE, WS, taxa_aprendizagem, epocas);

// Plotar a evolução do erro
plot(1:epocas, erros);
xlabel("Época");
ylabel("Erro Quadrático Médio");
title("Evolução do Erro Durante o Treinamento");
```

Este código permite visualizar como o erro diminui ao longo do treinamento, ajudando a entender se a rede está convergindo adequadamente.

## Aplicações Práticas

[Conteúdo mantido como no original]

### Exemplo: Controle de Robô em Scilab

Para implementar o controle de um robô usando uma rede neural em Scilab, poderíamos adaptar nosso código da seguinte forma:

```scilab
// Dados de treinamento para o robô
// [sensor_esquerdo, sensor_direito, direção_desejada]
dados_robo = [
    0 0 0.5;  // Sem obstáculos, ir para frente
    1 0 1.0;  // Obstáculo à esquerda, virar à direita
    0 1 0.0;  // Obstáculo à direita, virar à esquerda
    1 1 0.5   // Obstáculos em ambos os lados, ir para frente (ou decidir aleatoriamente)
];

// [Inicialização e treinamento da rede como antes]

// Função para controlar o robô
function direcao = controlar_robo(sensor_esquerdo, sensor_direito)
    X = [-1; sensor_esquerdo; sensor_direito];
    H = logistica(WE' * X);
    H = [-1; H];
    direcao = logistica(WS' * H);
endfunction

// Teste do controle
printf("Teste de controle do robô:\n");
printf("Sem obstáculos: %.2f\n", controlar_robo(0, 0));
printf("Obstáculo à esquerda: %.2f\n", controlar_robo(1, 0));
printf("Obstáculo à direita: %.2f\n", controlar_robo(0, 1));
printf("Obstáculos em ambos os lados: %.2f\n", controlar_robo(1, 1));
```

Este exemplo mostra como a rede neural treinada pode ser usada para controlar a direção de um robô baseado nas leituras de seus sensores.


## Considerações Finais

1. **Escolha da Arquitetura**: O número de camadas e neurônios pode afetar significativamente o desempenho da rede.

2. **Inicialização dos Pesos**: Uma boa inicialização pode acelerar o treinamento e evitar problemas de convergência.

3. **Taxa de Aprendizagem**: Uma taxa muito alta pode causar oscilações, enquanto uma taxa muito baixa pode tornar o treinamento muito lento.

4. **Overfitting**: É importante monitorar o desempenho em um conjunto de validação para evitar overfitting.

5. **Generalização**: A capacidade de generalização é uma das principais vantagens das redes neurais, permitindo que elas lidem com entradas não vistas durante o treinamento.

6. **Limitações Computacionais**: Redes muito grandes podem ser computacionalmente intensivas para treinar e usar.

As redes neurais multicamadas são uma ferramenta poderosa em aprendizado de máquina e inteligência artificial, formando a base para muitas aplicações modernas em diversos campos.