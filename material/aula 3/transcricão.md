# Aula 3: Introdução à Inteligência Artificial e Redes Neurais

## 8. Redes Neurais Multicamadas

### 8.1 Estrutura da Rede Neural Multicamada
- Composta por camadas: entrada, oculta(s) e saída
- Cada camada contém múltiplos neurônios
- Conexões entre neurônios de camadas adjacentes

### 8.2 Representação Matricial
- Convenção: colunas representam neurônios, linhas representam entradas
- Exemplo: matriz A, B, C, D, E, F para dois neurônios com três entradas
- Camada de saída: G, H, I para um neurônio com três entradas

### 8.3 Função de Ativação para Redes Multicamadas
- A função degrau não é adequada para redes multicamadas
- Função logística: $f(x) = \frac{1}{1 + e^{-x}}$
- Derivada da função logística: $f'(x) = f(x)(1 - f(x))$

### 8.4 Algoritmo de Retropropagação (Backpropagation)
- Processo de feedforward: propagação da entrada para a saída
- Processo de backpropagation: propagação do erro da saída para a entrada

#### 8.4.1 Feedforward
1. Cálculo da saída da camada oculta:
   $Y = f(X \cdot W_E)$
2. Cálculo da saída da rede:
   $Y_S = f(Y \cdot W_S)$

#### 8.4.2 Backpropagation
1. Cálculo do erro na camada de saída:
   $\delta = (target - Y_S) \cdot f'(Y_S)$
2. Cálculo do erro na camada oculta:
   $\delta_0 = (W_S \cdot \delta) \cdot f'(Y)$
3. Atualização dos pesos da camada de saída:
   $W_S = W_S + \eta \cdot \delta \cdot Y$
4. Atualização dos pesos da camada oculta:
   $W_E = W_E + \eta \cdot \delta_0 \cdot X$

Onde:
- $\eta$ é a taxa de aprendizagem
- $f'$ é a derivada da função de ativação

### 8.5 Implementação em SciLab

```scilab
// Definição dos dados (XOR)
dados = [-1 0 0 0; -1 0 1 1; -1 1 0 1; -1 1 1 0];

// Parâmetros
NM = 2;  // Número de neurônios na camada oculta
NA = size(dados, 1);  // Número de amostras
NE = size(dados, 2) - 1;  // Número de entradas

// Inicialização dos pesos
WE = rand(NE, NM);
WS = rand(NM + 1, 1);

// Taxa de aprendizagem
eta = 0.6;

// Loop de épocas
for epoca = 1:1000
    for am = 1:NA
        // Extração dos dados
        X = dados(am, 1:NE);
        target = dados(am, NE + 1);
        
        // Feedforward
        Y = 1 ./ (1 + exp(-X * WE));
        Y = [-1, Y];  // Adicionando o bias
        YS = 1 / (1 + exp(-Y * WS));
        
        // Cálculo das derivadas
        YD = Y .* (1 - Y);
        YSD = YS * (1 - YS);
        
        // Backpropagation
        delta = (target - YS) * YSD;
        delta0 = (WS(2:$)' .* delta) .* YD(:, 2:$);
        
        // Atualização dos pesos
        WSD = eta * delta * Y;
        WED = eta * (delta0' * X)';
        
        WS = WS + WSD;
        WE = WE + WED;
    end
    
    // Exibição dos resultados a cada 100 épocas
    if modulo(epoca, 100) == 0
        disp(['Época ', string(epoca)]);
        for am = 1:NA
            X = dados(am, 1:NE);
            Y = 1 ./ (1 + exp(-X * WE));
            Y = [-1, Y];
            YS = 1 / (1 + exp(-Y * WS));
            disp(['Entrada: ', string(X(2:$)), ' Saída: ', string(YS)]);
        end
    end
end
```

### 8.6 Aplicações Práticas
- Reconhecimento de padrões
- Controle de robôs
- Próteses neurais
- Sistemas de recomendação
- Processamento de linguagem natural

### 8.7 Considerações sobre Generalização
- A rede neural aprende a generalizar a partir dos exemplos fornecidos
- Capacidade de lidar com entradas não vistas durante o treinamento
- Importância do conjunto de treinamento representativo

## 9. Recursos Adicionais para Estudo

### 9.1 Livros Recomendados
1. "Redes Neurais Artificiais para Engenharia e Ciências Aplicadas" - Ivan Nunes da Silva
2. "Redes Neurais Artificiais: Uma Abordagem Prática" - Gilberto Galvão
3. "Aplicações de Cálculo Numérico em Engenharia"

### 9.2 Tópicos Avançados
- Cálculo numérico computacional
- Implementação de derivadas e integrais em computadores
- Otimização de algoritmos de aprendizagem

## 10. Conclusão
- As redes neurais artificiais são uma ferramenta poderosa em IA
- A compreensão dos fundamentos matemáticos é crucial para o desenvolvimento e aplicação eficaz
- O campo está em constante evolução, exigindo aprendizado contínuo