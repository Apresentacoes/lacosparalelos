# Laços Paralelos.

O artigo relata sobre o método de Lattice Boltzmann(método de dinâmica de fluídos) onde é possivel forjar computacionalmente vários problemas, permitindo simular situações complexas. Os métodos de dinâmica de fluídos por si só são muito custosos e implementa-los com paralelismo é uma otima forma de ganhar desempenho. O OpenMP é uma alternativa que possibilita paralelizar aplicações escritas em C, C++ e em Fortran utilizando as diretivas 'progmas'. Por processo do OpenMP é possivel criar laços paralelos, seções concorrentes, vetorização, times de threads, offloading, e tarefas assíncronas.

**O Método Lattice Boltzmann**
O MLB vem sendo desenvolvido como uma ferramente númerica para dinâmicas de fluídos computacionais, seu algoritmo é simples, de fácil entendimento e compatibilidade ao paralelismo. Seu algoritmo é composto por um laço principal com um certo número de passos por iterações.

> #pragma omp target data map(/* dados mapeados (malhas e vetor de obstaculos)*/)<br>
for(/* numero de iteracoes definida para o laco principal*/){<br>
redistribute(...);<br>
propagate(...);<br>
bounceback(...);<br>
relaxation(...);<br>
}<br> .

**Diferentes Ambientes**
* MPI - destaca-se por que neste tipo de ambiente o laço principal contém um método a mais e cada processo tabalha sobre ele durante as iterações. <br>
* OPENMP - Já este trabalha com uma quantia menor de código, neste tipo de implementação o foco é paralelizar os laços existentes dentro dos quatros métodos encontrados no exemplo acima dentro do laço principal.<br>
* CUDA - Aqui a malha é alocado na GPU e em toda aplicação, há apenas movimentaçoẽs antes e depois do laço principal, diminuindo o tempo gasto.
