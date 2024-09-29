## Redes Neurais Multicamadas e Backpropagation

### Estrutura da Rede Neural

- **Camadas:**
  - **Entrada:** X1, X2
  - **Camada Oculta:** Y0, Y01, Y02
  - **Camada de Saída:** YS

### Função de Ativação

- **Logística (Sigmoide):**
  - Fórmula: \[ \sigma(y) = \frac{1}{1 + e^{-y}} \]

### Processo de Treinamento

1. **Feed-Forward:**
   - Propagação dos dados de entrada através das camadas até a saída.
   
2. **Cálculo do Erro:**
   - Delta: \[ \delta = \text{Target} - YS \]
   
3. **Backpropagation:**
   - Cálculo das derivadas das funções de ativação.
   - Propagação do erro de volta através das camadas.
   - Atualização dos pesos com base no erro calculado.

### Atualização dos Pesos

- **Fórmula de Atualização:**
  \[ W_{\text{novo}} = W_{\text{atual}} + \text{taxa} \times \delta \times X \]

### Implementação Prática

- **Ferramentas Utilizadas:**
  - SciLab para simulação e implementação das redes neurais.
  
- **Passos:**
  - Definição das entradas e targets.
  - Inicialização dos pesos.
  - Implementação do feed-forward e backpropagation.
  - Atualização iterativa dos pesos até a convergência.

## Considerações Finais

- **Importância da Correção de Erros:**
  - Backpropagation permite a correção eficiente dos pesos para minimizar o erro.
  
- **Desafios na Implementação:**
  - Complexidade crescente com o aumento das camadas e neurônios.
  - Necessidade de compreensão profunda dos conceitos matemáticos envolvidos.
