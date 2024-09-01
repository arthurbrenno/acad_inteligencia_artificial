# Aula 4: Introdução à Inteligência Artificial e Redes Neurais

## 11. Redes Neurais Recorrentes e Previsão de Séries Temporais

### 11.1 Conceito de Janela Deslizante
- Utilizada para processar dados sequenciais
- Permite que a rede neural aprenda padrões temporais

### 11.2 Estrutura da Rede Neural para Previsão
- Entradas: x0, x1, x2, ..., x100 (exemplo)
- Janela deslizante: define o número de entradas consideradas a cada passo
- Saída: previsão do próximo valor na sequência

### 11.3 Processo de Treinamento
1. Definição da janela (ex: 4 valores)
2. Uso dos primeiros valores da janela como entrada
3. O valor seguinte à janela é usado como target (alvo)
4. A janela desliza para a próxima posição
5. O processo se repete até o final dos dados

### 11.4 Implementação em SciLab

```scilab
// Carregamento e normalização dos dados
dados = [21, 22, 23, ...]; // Dados de exemplo
NA = size(dados, 2);
valor_maximo = max(dados);
valor_minimo = min(dados);

// Normalização dos dados
dados_convertidos = (dados - valor_minimo) / (valor_maximo - valor_minimo);

// Definição da janela
janela = 3;

// Criação da rede neural
NE = janela + 2; // Número de entradas (janela + 1 para o bias)
NM = 10; // Número de neurônios na camada oculta

// Inicialização dos pesos
WE = rand(NE, NM);
WS = rand(NM + 1, 1);

// Loop de treinamento
for epoca = 1:50000
    for am = 1:(NA - janela - 1)
        // Preparação dos dados de entrada e target
        X = [-1, dados_convertidos(am:(am+janela-1))];
        target = dados_convertidos(am + janela);
        
        // Feedforward
        Y = 1 ./ (1 + exp(-X * WE));
        Y = [-1, Y];
        YS = 1 / (1 + exp(-Y * WS));
        
        // Backpropagation (código omitido para brevidade)
        
        // Atualização dos pesos
        WS = WS + WSD;
        WE = WE + WED;
    end
    
    // Plotagem a cada 1000 épocas
    if modulo(epoca, 1000) == 0
        // Código de plotagem omitido para brevidade
    end
end
```

### 11.5 Visualização dos Resultados
- Plotagem dos dados originais e previsões da rede
- Análise da capacidade de generalização da rede

### 11.6 Otimização do Modelo
- Ajuste do tamanho da janela
- Modificação do número de neurônios na camada oculta
- Experimentação com diferentes conjuntos de dados

### 11.7 Aplicações Práticas
- Previsão de séries temporais financeiras (ex: bolsa de valores)
- Previsão de demanda em sistemas de produção
- Análise de tendências em dados climáticos

## 12. Considerações Finais

### 12.1 Limitações do Modelo
- Sensibilidade a ruídos nos dados
- Necessidade de grandes conjuntos de dados para treinamento eficaz
- Possibilidade de overfitting (sobreajuste) em janelas muito grandes

### 12.2 Próximos Passos
- Exploração de arquiteturas mais avançadas (LSTM, GRU)
- Implementação de técnicas de regularização
- Estudo de métodos de validação cruzada para séries temporais

## 13. Exercícios Práticos

1. Implemente o modelo de previsão usando dados reais da bolsa de valores.
2. Experimente com diferentes tamanhos de janela e analise o impacto nos resultados.
3. Compare o desempenho da rede neural com métodos estatísticos tradicionais de previsão de séries temporais.

## 14. Recursos Adicionais

- Livros sobre análise de séries temporais com redes neurais
- Artigos científicos sobre aplicações de redes recorrentes em previsão financeira
- Tutoriais online sobre implementação de modelos preditivos em diferentes frameworks (TensorFlow, PyTorch)
