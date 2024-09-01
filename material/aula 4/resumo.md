# Resumo: Redes Neurais Recorrentes e Previsão de Séries Temporais

## 1. Conceito de Janela Deslizante
- Usada para processar dados sequenciais
- Permite aprendizagem de padrões temporais

## 2. Estrutura da Rede Neural para Previsão
- Entradas: valores da série temporal (ex: x0, x1, x2, ..., x100)
- Janela deslizante: define número de entradas por passo
- Saída: previsão do próximo valor na sequência

## 3. Processo de Treinamento
1. Definir tamanho da janela (ex: 4 valores)
2. Usar primeiros valores da janela como entrada
3. Valor seguinte à janela como target (alvo)
4. Deslizar janela para próxima posição
5. Repetir até o final dos dados

## 4. Implementação em SciLab
- Carregamento e normalização dos dados
- Definição da janela e estrutura da rede
- Loop de treinamento: feedforward e backpropagation
- Visualização dos resultados

## 5. Otimização do Modelo
- Ajuste do tamanho da janela
- Modificação do número de neurônios na camada oculta
- Experimentação com diferentes conjuntos de dados

## 6. Aplicações Práticas
- Previsão de séries temporais financeiras
- Previsão de demanda em sistemas de produção
- Análise de tendências em dados climáticos

## 7. Limitações do Modelo
- Sensibilidade a ruídos nos dados
- Necessidade de grandes conjuntos de dados
- Possibilidade de overfitting com janelas muito grandes

## 8. Próximos Passos
- Exploração de arquiteturas avançadas (LSTM, GRU)
- Implementação de técnicas de regularização
- Estudo de métodos de validação cruzada para séries temporais

## 9. Pontos-Chave para a Prova
1. Entender o conceito e funcionamento da janela deslizante (talvez?)
2. Compreender o processo de treinamento para previsão de séries temporais (improvável)
3. Conhecer a estrutura básica da implementação em SciLab
4. Reconhecer as aplicações práticas e limitações do modelo
5. Estar ciente das possibilidades de otimização e próximos passos no estudo
