### Redes Neurais Artificiais (RNAs)

#### Objetivo
- **Encontrar Padrões:** As RNAs são projetadas para identificar e aprender padrões a partir de grandes conjuntos de dados, sendo amplamente utilizadas em tarefas como reconhecimento de imagem, processamento de linguagem natural e previsão de séries temporais.

#### Estrutura Básica
- **Camadas:** Entrada, camadas ocultas e saída.
- **Neurônios:** Unidades básicas que processam informações.
- **Função de Ativação:** Introduz não-linearidades, como a função sigmoide ou ReLU.

#### Aplicações
- **Reconhecimento de Padrões:** Identificação de faces, reconhecimento de voz.
- **Classificação:** Diagnóstico médico, filtragem de spam.
- **Previsão:** Previsão de preços de ações, demanda de produtos.

### Algoritmos Genéticos (AG)

#### Objetivo
- **Otimização:** Os AGs são utilizados para encontrar soluções ótimas ou quase ótimas para problemas complexos de otimização, onde outras técnicas podem falhar ou serem ineficientes.

#### Diferença Fundamental
- **AG vs RNAs:** Enquanto as RNAs buscam padrões nos dados, os AGs procuram otimizar soluções, encontrando pontos de máximos e mínimos em espaços de solução.

### Componentes dos Algoritmos Genéticos

1. **População**
   - **Definição:** Conjunto de soluções potenciais para o problema em questão.
   - **Iniciação:** Geralmente criada de forma aleatória.

2. **Função de Fitness**
   - **Definição:** Avalia a qualidade de cada indivíduo na população.
   - **Objetivo:** Determinar quão boa é uma solução em relação aos objetivos do problema.
   - **Exemplo:** Em um problema de minimização, a função de fitness pode ser o inverso do custo.

3. **Seleção (Torneio)**
   - **Método:** Seleção de indivíduos com base em seu fitness para reprodução.
   - **Torneio:** Seleciona dois indivíduos aleatoriamente e escolhe o melhor entre eles para reprodução.

4. **Crossover (Recombinação)**
   - **Definição:** Combina dois indivíduos (pais) para gerar novos indivíduos (filhos).
   - **Tipos:** Crossover de ponto único, crossover uniforme, entre outros.
   - **Exemplo Simples:** Crossover binário onde segmentos dos genes dos pais são trocados para formar novos filhos.

5. **Mutação**
   - **Definição:** Introduz variações aleatórias nos indivíduos para manter a diversidade genética.
   - **Probabilidade:** Geralmente baixa (2% a 5%).
   - **Método:** Inverter bits em uma representação binária.

6. **Elitismo**
   - **Definição:** Preserva os melhores indivíduos da população atual para a próxima geração, garantindo que as soluções melhores não sejam perdidas.

### Processo de Implementação de um AG

1. **Inicialização**
   - Criar uma população inicial de indivíduos aleatórios que representam possíveis soluções.

2. **Avaliação**
   - Calcular o fitness de cada indivíduo usando a função de fitness definida.

3. **Seleção**
   - Selecionar indivíduos com maior fitness para reprodução, utilizando métodos como torneio.

4. **Crossover**
   - Aplicar o operador de crossover para gerar novos indivíduos a partir dos pais selecionados.

5. **Mutação**
   - Aplicar o operador de mutação nos novos indivíduos para introduzir diversidade.

6. **Substituição**
   - Formar uma nova geração substituindo os indivíduos menos aptos pela nova população gerada.

7. **Iteração**
   - Repetir o processo de avaliação, seleção, crossover e mutação até que um critério de parada seja atendido (por exemplo, número de gerações ou fitness desejado).

### Exemplos de Aplicação

#### Projeto da NASA: Otimização da Antena Espacial
- **Desafio:** Desenvolver uma antena eficiente para comunicação com a Terra utilizando menos recursos.
- **Solução com AG:** Modelagem matemática da antena e utilização do AG para encontrar a configuração que otimiza a eficiência, reduzindo o tamanho e custo sem comprometer a funcionalidade.

#### Problemas Clássicos

1. **Cavalo de Xadrez (Knight's Tour)**
   - **Objetivo:** Fazer o cavalo percorrer todas as casas de um tabuleiro sem repetir nenhuma.
   - **Aplicação do AG:** Representar cada movimento como um indivíduo e otimizar a sequência de movimentos para cobrir todas as casas.

2. **Problema das N-Rainhas**
   - **Objetivo:** Colocar N rainhas em um tabuleiro de xadrez de modo que nenhuma rainha ataque outra.
   - **Aplicação do AG:** Representar cada posição das rainhas como um indivíduo e otimizar a disposição para minimizar conflitos.

### Implementação Prática de um AG

#### Passos Detalhados

1. **Definição da População Inicial**
   - Criar uma população de soluções aleatórias.
   - **Exemplo em Binário:**
     ```scilab
     pop_size = 6;
     gene_length = 10;
     population = rand(1, pop_size, 'int') > 0.5;
     ```

2. **Função de Fitness**
   - Avaliar cada indivíduo de acordo com a função de fitness.
   - **Exemplo de Função Gaussiana:**
     \[
     \text{Fitness}(x) = e^{-\frac{(x - 12)^2}{5}}
     \]
     - **Objetivo:** Maximizar a fitness em torno de \( x = 12 \).

3. **Seleção via Torneio**
   - Realizar torneios aleatórios para selecionar os melhores indivíduos.
   - **Pseudo-código:**
     ```scilab
     for i = 1:pop_size
         idx1 = round(rand() * (pop_size - 1)) + 1;
         idx2 = round(rand() * (pop_size - 1)) + 1;
         if fitness(idx1) > fitness(idx2) then
             selected(i) = population(idx1);
         else
             selected(i) = population(idx2);
         end
     end
     ```

4. **Crossover**
   - Combinar pares de indivíduos para gerar novos filhos.
   - **Exemplo Simples:**
     ```scilab
     for i = 1:2:pop_size
         crossover_point = round(rand() * gene_length);
         child1 = [selected(i, 1:crossover_point), selected(i+1, crossover_point+1:end)];
         child2 = [selected(i+1, 1:crossover_point), selected(i, crossover_point+1:end)];
         new_population = [new_population; child1; child2];
     end
     ```

5. **Mutação**
   - Aplicar mutações aleatórias com baixa probabilidade.
   - **Exemplo:**
     ```scilab
     mutation_rate = 0.02;
     for i = 1:pop_size
         for j = 1:gene_length
             if rand() < mutation_rate then
                 new_population(i, j) = ~new_population(i, j);
             end
         end
     end
     ```

6. **Elitismo e Substituição**
   - Preservar os melhores indivíduos e substituir os menos aptos.
   - **Exemplo:**
     ```scilab
     best_individual = population(find(fitness == max(fitness), 1));
     new_population(1) = best_individual;
     population = new_population;
     ```

7. **Iteração e Convergência**
   - Repetir o processo até que a solução desejada seja encontrada ou o número de gerações seja atingido.

#### Exemplo de Implementação Completa em SciLab

```scilab
// Inicialização
pop_size = 6;
gene_length = 10;
population = rand(1, pop_size, 'int') > 0.5;
target = 12;

// Função de Fitness
function fit = fitness(x, target)
    fit = exp(-((x - target)^2) / 5);
endfunction

// Algoritmo Genético
generations = 100;
for gen = 1:generations
    // Avaliação
    fitness_vals = zeros(1, pop_size);
    for i = 1:pop_size
        x = bin2dec(string(population(i, :)));
        fitness_vals(i) = fitness(x, target);
    end
    
    // Seleção via Torneio
    selected = zeros(pop_size, gene_length);
    for i = 1:pop_size
        idx1 = round(rand() * (pop_size - 1)) + 1;
        idx2 = round(rand() * (pop_size - 1)) + 1;
        if fitness_vals(idx1) > fitness_vals(idx2) then
            selected(i, :) = population(idx1, :);
        else
            selected(i, :) = population(idx2, :);
        end
    end
    
    // Crossover
    new_population = [];
    for i = 1:2:pop_size
        crossover_point = round(rand() * gene_length);
        child1 = [selected(i, 1:crossover_point), selected(i+1, crossover_point+1:end)];
        child2 = [selected(i+1, 1:crossover_point), selected(i, crossover_point+1:end)];
        new_population = [new_population; child1; child2];
    end
    
    // Mutação
    mutation_rate = 0.02;
    for i = 1:pop_size
        for j = 1:gene_length
            if rand() < mutation_rate then
                new_population(i, j) = ~new_population(i, j);
            end
        end
    end
    
    // Elitismo
    best_idx = find(fitness_vals == max(fitness_vals), 1);
    best_individual = population(best_idx, :);
    new_population(1, :) = best_individual;
    
    // Substituição
    population = new_population;
    
    // Verificação de Convergência
    if max(fitness_vals) == 1 then
        break;
    end
end

// Resultado Final
disp("Melhor Indivíduo:");
disp(population(find(fitness_vals == max(fitness_vals), 1), :));
```

### Exercícios e Exemplos Práticos

#### 1. Maximização do Volume de um Cilindro

##### Problema
- **Objetivo:** Encontrar os valores de raio \( r \) e altura \( h \) de um cilindro que maximizem o volume \( V = \pi r^2 h \), dado que a área superficial \( A = 2\pi r h + 2\pi r^2 = 1 \) metro quadrado.

##### Formulação Matemática
1. **Área Superficial:**
   \[
   2\pi r h + 2\pi r^2 = 1 \implies h = \frac{1 - 2\pi r^2}{2\pi r}
   \]
2. **Volume:**
   \[
   V = \pi r^2 h = \pi r^2 \left( \frac{1 - 2\pi r^2}{2\pi r} \right) = \frac{r (1 - 2\pi r^2)}{2}
   \]

##### Implementação com AG
1. **Codificação dos Genes:**
   - Representar \( r \) e \( h \) como variáveis contínuas.
2. **Função de Fitness:**
   - Maximizar \( V \) sujeito à restrição \( A = 1 \).
   - Penalizar soluções que não satisfazem a restrição.
3. **Processo de Evolução:**
   - Inicializar uma população de soluções aleatórias.
   - Avaliar o fitness de cada solução.
   - Selecionar as melhores soluções para reprodução.
   - Aplicar crossover e mutação para gerar novas soluções.
   - Repetir até que a melhor solução atinja a maximização desejada.

##### Pseudo-código

```scilab
// Definição dos parâmetros
pop_size = 100;
gene_length = 10;
generations = 1000;
target_area = 1;

// Inicialização da população
population = rand(pop_size, gene_length); // Valores contínuos entre 0 e 1

// Função de Fitness
function fit = fitness(r, h, target_area)
    area = 2 * %pi * r * h + 2 * %pi * r^2;
    if area > target_area then
        fit = 0; // Penalizar soluções que excedem a área
    else
        fit = %pi * r^2 * h; // Maximizar o volume
    end
endfunction

// Algoritmo Genético
for gen = 1:generations
    // Avaliação
    fitness_vals = zeros(pop_size, 1);
    for i = 1:pop_size
        r = population(i, 1);
        h = population(i, 2);
        fitness_vals(i) = fitness(r, h, target_area);
    end
    
    // Seleção via Torneio
    selected = zeros(pop_size, gene_length);
    for i = 1:pop_size
        idx1 = round(rand() * (pop_size - 1)) + 1;
        idx2 = round(rand() * (pop_size - 1)) + 1;
        if fitness_vals(idx1) > fitness_vals(idx2) then
            selected(i, :) = population(idx1, :);
        else
            selected(i, :) = population(idx2, :);
        end
    end
    
    // Crossover (Recombinação de Ponto Único)
    new_population = zeros(pop_size, gene_length);
    for i = 1:2:pop_size
        crossover_point = round(rand() * (gene_length - 1)) + 1;
        new_population(i, 1:crossover_point) = selected(i, 1:crossover_point);
        new_population(i, crossover_point+1:end) = selected(i+1, crossover_point+1:end);
        new_population(i+1, 1:crossover_point) = selected(i+1, 1:crossover_point);
        new_population(i+1, crossover_point+1:end) = selected(i, crossover_point+1:end);
    end
    
    // Mutação
    mutation_rate = 0.05;
    for i = 1:pop_size
        for j = 1:gene_length
            if rand() < mutation_rate then
                new_population(i, j) = rand(); // Substituir por um novo valor aleatório
            end
        end
    end
    
    // Elitismo: Preservar o melhor indivíduo
    [max_fit, best_idx] = max(fitness_vals);
    new_population(1, :) = population(best_idx, :);
    
    // Substituição
    population = new_population;
    
    // Verificação de Convergência
    if max_fit == %pi * (population(best_idx, 1)^2) * population(best_idx, 2) then
        break;
    end
end

// Resultado Final
best_idx = find(fitness_vals == max(fitness_vals), 1);
best_solution = population(best_idx, :);
r_opt = best_solution(1);
h_opt = best_solution(2);
disp("Raio Ótimo:");
disp(r_opt);
disp("Altura Ótima:");
disp(h_opt);
disp("Volume Máximo:");
disp(%pi * r_opt^2 * h_opt);
```

### Exercícios Propostos

1. **Cavalo de Xadrez (Knight's Tour)**
   - **Descrição:** Fazer o cavalo percorrer todas as casas de um tabuleiro sem repetir nenhuma.
   - **Objetivo:** Implementar um AG para otimizar a sequência de movimentos do cavalo.

2. **Problema das N-Rainhas**
   - **Descrição:** Colocar N rainhas em um tabuleiro de xadrez de modo que nenhuma rainha ataque outra.
   - **Objetivo:** Utilizar um AG para encontrar uma disposição das rainhas que minimize os conflitos.

3. **Maximização do Volume de um Cilindro**
   - **Descrição:** Encontrar os valores de raio e altura de um cilindro que maximizem o volume, dado uma restrição na área superficial.
   - **Objetivo:** Implementar um AG que encontre os valores ideais de raio e altura.

4. **Otimização de Caminhos em Ecossistemas**
   - **Descrição:** Encontrar o caminho mais curto entre dois pontos em um mapa de ecossistemas.
   - **Objetivo:** Utilizar um AG para otimizar a rota de menor distância.

### Considerações Finais

#### Vantagens dos Algoritmos Genéticos
- **Exploração Eficiente:** Capacidade de explorar grandes espaços de solução sem se prender a preconceitos ou limitações humanas.
- **Flexibilidade:** Aplicável a uma ampla variedade de problemas de otimização.
- **Robustez:** Capaz de encontrar boas soluções mesmo em problemas complexos e mal definidos.

#### Desafios na Implementação
- **Modelagem Matemática:** Definir uma função de fitness eficaz e representar adequadamente as soluções pode ser complexo.
- **Parâmetros de Evolução:** Escolher taxas de crossover e mutação apropriadas é crucial para o desempenho do AG.
- **Convergência:** Garantir que o algoritmo converja para uma solução ótima sem ficar preso em ótimos locais.

#### Dicas para Estudantes
- **Prática com Exemplos Simples:** Implementar AGs para problemas clássicos como o N-Rainhas e Cavalo de Xadrez.
- **Experimentação:** Testar diferentes funções de fitness, métodos de seleção e operadores genéticos para entender seu impacto.
- **Leitura Complementar:**
  - "Genetic Algorithms in Search, Optimization, and Machine Learning" - David E. Goldberg.
  - "Introduction to Genetic Algorithms" - S.N. Sivanandam, S.N. Deepa.

### Referências

- **Livros:**
  - "Genetic Algorithms in Search, Optimization, and Machine Learning" - David E. Goldberg.
  - "Neural Networks and Learning Machines" - Simon Haykin.
  - "Deep Learning" - Ian Goodfellow, Yoshua Bengio, Aaron Courville.
  
- **Recursos Online:**
  - [SciLab Documentation](https://www.scilab.org/documentation)
  - [TensorFlow](https://www.tensorflow.org/)
  - [PyTorch](https://pytorch.org/)
  - [Wikipedia - Algoritmo Genético](https://pt.wikipedia.org/wiki/Algoritmo_gen%C3%A9tico)
