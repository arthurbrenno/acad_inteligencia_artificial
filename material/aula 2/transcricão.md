# Aula 2: Introdução à Inteligência Artificial e Perceptron

## 1. Conceitos Básicos de Redes Neurais

### 1.1 Estrutura Básica do Neurônio Artificial
- Inspirado no neurônio biológico
- Componentes:
  - Entradas (camada de entrada)
  - Pesos neurais
  - Camada intermediária
  - Camada de saída (net)

### 1.2 Função de Ativação
- Determina quando o neurônio "dispara"
- Exemplo: Função degrau
  - Se net ≥ 0, saída = 1
  - Se net < 0, saída = 0

### 1.3 Neurônio de McCulloch e Pitts
- Desenvolvido por um psicólogo e um matemático
- Base para o desenvolvimento de redes neurais artificiais

## 2. Aprendizagem do Perceptron

### 2.1 Conceito de Derivada de Decaimento
- Busca o ponto mais baixo da função de erro
- Quando encontra o ponto mínimo, considera-se que o neurônio aprendeu

### 2.2 Overtraining (Sobreajuste)
- Treinar excessivamente pode fazer a rede "desaprender"
- Necessidade de gerenciamento do treinamento

### 2.3 Algoritmo de Aprendizagem
- Utiliza a derivada de decaimento
- Fórmula: $\Delta w = -\zeta \frac{\partial E}{\partial w}$
  - $\zeta$ (zeta) = taxa de aprendizagem (empiricamente definida como 0.6)
  - $E$ = erro quadrático médio

### 2.4 Cálculo do Erro
- Erro quadrático médio: $E = \frac{1}{2}(target - net)^2$
- Target: valor desejado de saída
- Net: valor obtido na saída do neurônio

## 3. Implementação Prática do Perceptron

### 3.1 Ambiente de Desenvolvimento
- Utilização do SciLab
- Vantagens:
  - Visualização de variáveis em tempo real
  - Facilidade para identificar erros
  - Possibilidade de transcrever para outras linguagens posteriormente

### 3.2 Estrutura do Código

```scilab
// Limpeza do ambiente
clear
clc

// Definição dos dados de entrada e saída desejada (target)
dados = [-1 0 0 0; -1 0 1 0; -1 1 0 0; -1 1 1 1];

// Parâmetros
num_entradas = size(dados, 2) - 1
num_amostras = size(dados, 1)

// Inicialização dos pesos neurais de forma aleatória
w = rand(1, num_entradas);

// Loop de épocas
for epoca = 1:10
    // Loop de amostras
    for amostra = 1:num_amostras
        // Extração dos dados de entrada e target
        x = dados(amostra, 1:num_entradas);
        target = dados(amostra, num_entradas + 1);
        
        // Cálculo da saída do neurônio (net)
        net = x * w';
        
        // Função de ativação (degrau)
        if net >= 0
            y = 1;
        else
            y = 0;
        end
        
        // Cálculo do erro
        erro = target - y;
        
        // Atualização dos pesos
        w = w + 0.6 * erro * x;
    end
    
    // Exibição dos pesos após cada época
    disp(['Época ', string(epoca), ': ', string(w)]);
end
```

### 3.3 Visualização do Processo de Aprendizagem
- Implementação de um gráfico para visualizar a evolução da reta de decisão
- Código para plotagem:

```scilab
// Plotagem da reta de decisão
x2 = linspace(0, 1, 100);
x1 = (-w(3)*x2 - w(1)) / w(2);
plot(x2, x1);
```

## 4. Limitações do Perceptron

### 4.1 Problema do XOR
- O perceptron simples não consegue resolver o problema do XOR
- Demonstração:

```scilab
dados_xor = [-1 0 0 0; -1 0 1 1; -1 1 0 1; -1 1 1 0];
```

### 4.2 Solução: Perceptron Multicamadas
- Introdução ao conceito de redes neurais com mais de um neurônio
- Algoritmo de Retropropagação (Backpropagation)

## 5. Otimização do Perceptron

### 5.1 Ajuste da Taxa de Aprendizagem
- Taxa muito alta: pode causar oscilações e dificultar a convergência
- Taxa muito baixa: aprendizagem lenta

### 5.2 Modificação na Função de Erro
- Cálculo do erro antes da função de ativação
- Permite um ajuste mais fino dos pesos

## 6. Considerações Finais

### 6.1 Importância da Compreensão dos Conceitos
- Entender o funcionamento interno das redes neurais permite:
  - Melhor seleção de parâmetros
  - Identificação e correção de problemas
  - Adaptação para diferentes aplicações

### 6.2 Próximos Passos
- Estudo de redes neurais mais complexas
- Aplicações práticas em diferentes domínios

## 7. Exercícios Práticos

1. Implemente o perceptron para resolver o problema da porta lógica OR.
2. Experimente diferentes taxas de aprendizagem e observe o impacto no treinamento.
3. Tente implementar uma função de ativação diferente (ex: sigmoide) e compare os resultados.