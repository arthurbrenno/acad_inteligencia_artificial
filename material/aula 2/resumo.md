# Resumo: Introdução à IA e Perceptron

## 1. Conceitos Básicos de Redes Neurais
- Estrutura do neurônio artificial: entradas, pesos, camadas intermediárias, saída (net)
- Função de ativação: determina quando o neurônio "dispara" (ex: função degrau)
- Neurônio de McCulloch e Pitts: base para redes neurais artificiais

## 2. Aprendizagem do Perceptron
- Derivada de decaimento: busca o ponto mínimo da função de erro
- Overtraining: risco de "desaprender" com treinamento excessivo
- Algoritmo de aprendizagem: $\Delta w = -\zeta \frac{\partial E}{\partial w}$
- Erro quadrático médio: $E = \frac{1}{2}(target - net)^2$

## 3. Implementação Prática
- Ambiente: SciLab (visualização em tempo real, fácil identificação de erros)
- Estrutura do código:
  - Inicialização de dados e parâmetros
  - Loop de épocas e amostras
  - Cálculo de net, função de ativação, erro e atualização de pesos
- Visualização: plotagem da reta de decisão

## 4. Limitações do Perceptron
- Incapaz de resolver o problema XOR
- Solução: Perceptron Multicamadas (introdução ao backpropagation)

## 5. Otimização
- Ajuste da taxa de aprendizagem
- Modificação na função de erro (cálculo antes da ativação)
