## Redes Neurais Multicamadas e Backpropagation

### Introdução

Nesta aula, abordamos a estrutura e o funcionamento das redes neurais multicamadas, com foco no processo de treinamento utilizando o algoritmo de backpropagation. Vamos explorar desde a arquitetura básica até a implementação prática utilizando SciLab.

### Estrutura da Rede Neural

#### Camadas da Rede

- **Camada de Entrada:**
  - Recebe os dados de entrada. Exemplo: X1, X2.
  
- **Camada Oculta:**
  - Realiza o processamento intermediário. Exemplo: Y0, Y01, Y02.
  
- **Camada de Saída:**
  - Produz a saída final da rede. Exemplo: YS.

#### Diagrama da Rede

```plaintext
Entrada: X1, X2
       /    |    \
     Y0    Y01   Y02
       \    |    /
         \  |  /
           YS
```

### Função de Ativação

- **Logística (Sigmoide):**
  - Utilizada para introduzir não-linearidades na rede.
  - Fórmula:
    \[
    \sigma(y) = \frac{1}{1 + e^{-y}}
    \]
  - **Propriedades:**
    - Saída entre 0 e 1.
    - Derivada: \(\sigma'(y) = \sigma(y) \times (1 - \sigma(y))\)

### Processo de Treinamento

#### 1. Feed-Forward

- **Descrição:**
  - Propagação dos dados de entrada através das camadas até a camada de saída.
  
- **Passos:**
  1. Multiplicar as entradas pelos pesos correspondentes.
  2. Aplicar a função de ativação.
  3. Repetir o processo para cada camada até a saída.

#### 2. Cálculo do Erro

- **Delta (Erro):**
  \[
  \delta = \text{Target} - YS
  \]
  
- **Objetivo:**
  - Minimizar o erro entre a saída prevista (YS) e o valor alvo (Target).

#### 3. Backpropagation

- **Descrição:**
  - Algoritmo para ajustar os pesos da rede com base no erro calculado.
  
- **Passos:**
  1. **Calcular a Derivada da Função de Ativação:**
     \[
     \sigma'(y) = YS \times (1 - YS)
     \]
  
  2. **Propagar o Erro para Trás:**
     - Distribuir o erro das camadas de saída para as camadas ocultas.
     - Utilizar a matriz transposta dos pesos para calcular o impacto do erro em cada neurônio.
  
  3. **Atualizar os Pesos:**
     \[
     W_{\text{novo}} = W_{\text{atual}} + \text{taxa} \times \delta \times X
     \]
     - Onde:
       - **W:** Peso atual.
       - **Taxa:** Taxa de aprendizado.
       - **X:** Entrada correspondente.

### Atualização dos Pesos

- **Fórmula de Atualização:**
  \[
  W_{\text{novo}} = W_{\text{atual}} + \text{taxa} \times \delta \times X
  \]
  
- **Detalhes:**
  - **Taxa de Aprendizado:** Determina o quão grandes são os ajustes dos pesos em cada iteração.
  - **Convergência:** O processo é repetido até que o erro seja minimizado ou atinja um valor aceitável.

### Implementação Prática com SciLab

#### Passos para Implementação

1. **Definição dos Dados de Entrada e Targets:**
   - Entradas (X) e valores alvo (Target) são definidos com base no problema a ser resolvido.
   
2. **Inicialização dos Pesos:**
   - Pesos são inicialmente atribuídos valores aleatórios.
   
3. **Implementação do Feed-Forward:**
   - Cálculo das ativações para cada camada.
   
4. **Cálculo do Erro e Backpropagation:**
   - Determinação do delta e ajuste dos pesos através do algoritmo de backpropagation.
   
5. **Iteração do Processo:**
   - Repetição do processo de feed-forward e backpropagation até a convergência.

#### Exemplo de Código em SciLab

```scilab
// Definição dos dados de entrada (X) e targets
X = [1, 0.3, 1, 0.92; 
     0.21, 0.21, 0.5, 0.5];
Target = [1; 0];

// Inicialização dos pesos aleatoriamente
W1 = rand(2, 3); // Pesos da camada oculta
W2 = rand(1, 3); // Pesos da camada de saída

// Função de ativação sigmoide
function y = sigmoid(x)
    y = 1 / (1 + exp(-x));
endfunction

// Função derivada da sigmoide
function dy = sigmoid_derivative(y)
    dy = y * (1 - y);
endfunction

// Taxa de aprendizado
taxa = 0.5;

// Feed-Forward
Z1 = sigmoid(X * W1');
Z2 = sigmoid(Z1 * W2');

// Cálculo do erro
delta2 = (Target - Z2) .* sigmoid_derivative(Z2);

// Backpropagation
delta1 = (delta2 * W2) .* sigmoid_derivative(Z1);

// Atualização dos pesos
W2 = W2 + taxa * (delta2' * Z1);
W1 = W1 + taxa * (delta1' * X);
```

### Considerações Finais

#### Importância da Correção de Erros

- **Backpropagation** permite a correção eficiente dos pesos para minimizar o erro total da rede, melhorando a precisão das previsões.

#### Desafios na Implementação

- **Complexidade Computacional:**
  - Redes maiores com mais camadas e neurônios aumentam a complexidade do treinamento.
  
- **Overfitting:**
  - Risco de a rede se ajustar demais aos dados de treinamento, perdendo a capacidade de generalização.

#### Dicas para Estudantes

- **Compreensão Matemática:**
  - Entender as derivadas e a matemática por trás do algoritmo é crucial para implementar e ajustar redes neurais eficazmente.
  
- **Prática com Ferramentas:**
  - Utilizar SciLab ou outras linguagens como Python com bibliotecas como TensorFlow ou PyTorch para implementar e experimentar com redes neurais.
  
- **Leitura Recomendada:**
  - "Neural Networks and Learning Machines" - Simon Haykin.
  - "Deep Learning" - Ian Goodfellow, Yoshua Bengio, Aaron Courville.

### Exemplos e Exercícios

#### Exemplo de Atualização de Peso

```scilab
// Dados de exemplo
X = [1, 0.3, 1, 0.92];
Target = 1;
taxa = 0.5;

// Peso inicial
W = [0.2, 0.4, 0.6, 0.8];

// Feed-Forward
Z = sigmoid(X * W');

// Cálculo do Erro
delta = (Target - Z) * sigmoid_derivative(Z);

// Atualização do Peso
W = W + taxa * delta * X;
```

#### Exercício Prático

1. **Defina um conjunto de dados simples com duas variáveis de entrada e um alvo binário.**
2. **Inicialize os pesos das camadas ocultas e de saída aleatoriamente.**
3. **Implemente a função de ativação sigmoide e sua derivada.**
4. **Realize o processo de feed-forward para calcular as ativações.**
5. **Calcule o erro e execute o backpropagation para ajustar os pesos.**
6. **Repita o processo por várias iterações e observe a convergência dos pesos e a diminuição do erro.**

### Referências

- **Livros:**
  - "Neural Networks and Learning Machines" - Simon Haykin.
  - "Deep Learning" - Ian Goodfellow, Yoshua Bengio, Aaron Courville.
  - "Pattern Recognition and Machine Learning" - Christopher M. Bishop.
  
- **Recursos Online:**
  - [SciLab Documentation](https://www.scilab.org/documentation)
  - [TensorFlow](https://www.tensorflow.org/)
  - [PyTorch](https://pytorch.org/)
