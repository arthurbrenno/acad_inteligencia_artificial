# Redes Neurais para Previsão de Séries Temporais

## Sumário
1. [Introdução](#introdução)
2. [Preparação dos Dados](#preparação-dos-dados)
3. [Arquitetura da Rede Neural](#arquitetura-da-rede-neural)
4. [Implementação em Scilab](#implementação-em-scilab)
5. [Treinamento e Visualização](#treinamento-e-visualização)
6. [Considerações Práticas](#considerações-práticas)
7. [Aplicações e Extensões](#aplicações-e-extensões)

## Introdução

Nesta aula, exploramos a aplicação de redes neurais para a previsão de séries temporais. Este é um problema comum em muitas áreas, como finanças, meteorologia e análise de tendências. A ideia principal é usar dados históricos para prever valores futuros.

## Preparação dos Dados

### Coleta de Dados
- Utilizamos uma série de números como exemplo (pode ser substituída por dados reais, como preços de ações ou temperaturas diárias).
- É importante ter uma quantidade significativa de dados para treinar a rede adequadamente.

### Normalização
Para preparar os dados para a rede neural, realizamos os seguintes passos:

1. Encontrar o valor máximo e mínimo da série:
   ```scilab
   valor_maximo = max(dados);
   valor_minimo = min(dados);
   ```

2. Normalizar os dados para o intervalo [0, 1]:
   ```scilab
   dados_normalizados = (dados - valor_minimo) / (valor_maximo - valor_minimo);
   ```

Esta normalização é crucial para que a rede neural funcione eficientemente.

### Criação da Janela Deslizante
A técnica de janela deslizante é usada para criar os dados de entrada e saída para a rede:

```scilab
janela = 3;  // Tamanho da janela
for am = 1:(NA - janela)
    X = dados_normalizados(am:(am + janela - 1));
    target = dados_normalizados(am + janela);
    // Use X como entrada e target como saída desejada
end
```

## Arquitetura da Rede Neural

Utilizamos uma rede neural feedforward com:
- Camada de entrada: tamanho igual ao tamanho da janela + 1 (para o bias)
- Camada oculta: número de neurônios definido pelo usuário (ex: 10)
- Camada de saída: 1 neurônio (para prever o próximo valor)

## Implementação em Scilab

### Inicialização dos Pesos
```scilab
NE = janela + 1;  // +1 para o bias
NS = 10;  // Número de neurônios na camada oculta
WE = rand(NE, NS);  // Pesos da camada de entrada para a oculta
WS = rand(NS + 1, 1);  // Pesos da camada oculta para a saída
```

### Função de Ativação
Usamos a função logística (sigmoid):
```scilab
function y = logistica(x)
    y = 1 ./ (1 + exp(-x));
endfunction
```

### Propagação Direta
```scilab
function [H, YS] = propagar(X, WE, WS)
    X = [-1; X];  // Adiciona o bias
    H = logistica(WE' * X);
    H = [-1; H];  // Adiciona o bias para a camada de saída
    YS = logistica(WS' * H);
endfunction
```

### Retropropagação e Atualização de Pesos
```scilab
function [WE, WS] = atualizar_pesos(X, target, H, YS, WE, WS, taxa_aprendizagem)
    D = target - YS;
    DS = D * YS * (1 - YS);
    DH = (WS(2:$) * DS) .* H(2:$) .* (1 - H(2:$));
    
    WS = WS + taxa_aprendizagem * DS * H;
    WE = WE + taxa_aprendizagem * X * DH';
endfunction
```

## Treinamento e Visualização

### Loop de Treinamento
```scilab
epocas = 10000;
for epoca = 1:epocas
    for am = 1:(NA - janela)
        X = dados_normalizados(am:(am + janela - 1));
        target = dados_normalizados(am + janela);
        [H, YS] = propagar(X, WE, WS);
        [WE, WS] = atualizar_pesos(X, target, H, YS, WE, WS, taxa_aprendizagem);
    end
    
    // Código para visualização periódica
    if mod(epoca, 1000) == 0
        // Plotar resultados
    end
end
```

### Visualização
Para visualizar o progresso do treinamento:

```scilab
plot(1:41, dados_convertidos(janela+1:45), 'b');  // Dados originais
plot(1:41, Y_plot, 'r');  // Previsões da rede
xlabel('Índice');
ylabel('Valor');
title('Previsão de Série Temporal');
legend(['Dados Originais', 'Previsão da Rede']);
```

## Considerações Práticas

1. **Tamanho da Janela**: Um tamanho maior pode capturar padrões de longo prazo, mas requer mais dados e pode levar a overfitting.

2. **Número de Neurônios**: Mais neurônios na camada oculta podem capturar relações mais complexas, mas também aumentam o risco de overfitting.

3. **Taxa de Aprendizagem**: Uma taxa muito alta pode levar a oscilações, enquanto uma taxa muito baixa pode resultar em convergência lenta.

4. **Normalização**: É crucial para o bom funcionamento da rede. Lembre-se de desnormalizar os resultados para interpretação.

5. **Overfitting vs Underfitting**: Monitore o desempenho em um conjunto de validação para evitar overfitting.

## Aplicações e Extensões

1. **Previsão de Mercado Financeiro**: Use dados históricos de ações para prever tendências futuras.

2. **Previsão Meteorológica**: Aplique a técnica para prever temperaturas ou precipitações.

3. **Análise de Tendências**: Útil em marketing para prever tendências de consumo.

4. **Controle de Processos Industriais**: Preveja variáveis de processos para otimização e controle.

5. **Extensões**:
   - Experimente com diferentes arquiteturas de rede (ex: LSTM para memória de longo prazo).
   - Incorpore múltiplas variáveis de entrada para previsões mais complexas.
   - Implemente técnicas de validação cruzada para uma avaliação mais robusta do modelo.
