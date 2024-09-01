# Resumo: IA e Redes Neurais Multicamadas

## 1. Estrutura da Rede Neural Multicamada
- Camadas: entrada, oculta(s) e saída
- Múltiplos neurônios por camada
- Conexões entre neurônios de camadas adjacentes

## 2. Representação Matricial
- Colunas: neurônios; Linhas: entradas
- Exemplo: A, B, C, D, E, F para dois neurônios com três entradas

## 3. Função de Ativação
- Função logística: $f(x) = \frac{1}{1 + e^{-x}}$
- Derivada: $f'(x) = f(x)(1 - f(x))$

## 4. Algoritmo de Retropropagação (Backpropagation)
### 4.1 Feedforward
1. Saída da camada oculta: $Y = f(X \cdot W_E)$
2. Saída da rede: $Y_S = f(Y \cdot W_S)$

### 4.2 Backpropagation
1. Erro na camada de saída: $\delta = (target - Y_S) \cdot f'(Y_S)$
2. Erro na camada oculta: $\delta_0 = (W_S \cdot \delta) \cdot f'(Y)$
3. Atualização dos pesos (saída): $W_S = W_S + \eta \cdot \delta \cdot Y$
4. Atualização dos pesos (oculta): $W_E = W_E + \eta \cdot \delta_0 \cdot X$

## 5. Implementação em SciLab
- Definição de dados (XOR)
- Inicialização de pesos
- Loop de épocas: feedforward, cálculo de derivadas, backpropagation, atualização de pesos

## 6. Aplicações Práticas
- Reconhecimento de padrões
- Controle de robôs
- Próteses neurais
- Sistemas de recomendação
- Processamento de linguagem natural

## 7. Generalização
- Capacidade de lidar com entradas não vistas no treinamento
- Importância de um conjunto de treinamento representativo

## 8. Tópicos Avançados
- Cálculo numérico computacional
- Implementação de derivadas e integrais em computadores
- Otimização de algoritmos de aprendizagem

## 9. Pontos-Chave para a Prova
1. Entender a estrutura e funcionamento da rede neural multicamada
2. Conhecer a função logística e sua derivada (baixas chances de cair)
3. Compreender o processo de feedforward e backpropagation
4. Saber interpretar e aplicar as fórmulas de atualização de pesos
5. Reconhecer a importância da generalização e do conjunto de treinamento
6. Estar familiarizado com as aplicações práticas das redes neurais
