1. Como se utiliza o comando ps para:
(a) Mostrar todos os processos rodando na máquina?

```bash
ps -e 
```

(b) Mostrar os processos de um usuário?

```bash
ps -u nome de usuário
```

(c) Ordenar todos os processos de acordo com o uso da CPU?

```bash
ps aux --sort = -pcpu
```

(d) Mostrar a quanto tempo cada processo está rodando?

```bash
ps -ef --sort = start_time
```
2. De onde vem o nome fork()?

```bash
O  Fork (Bifurcações) são a divisão ou separação de alguma coisa em dois ramos ou braços; é o ponto em que se dá uma divisão ou uma separação, ou seja permite criar uma cópia exata do processo que chama a função.
```

3. Quais são as vantagens e desvantagens em utilizar:

(a) system()?

```bash
Um sistema de função () permite executar um comando dentro do programa, criando um sub-processo (processo-filho). Sua saída é retornada no shell, se o shell não puder ser executado, o system() retorna o valor 127 e se outro erro ocorrer, retorna o valor -1. Sua vantagem é a simplicidade. As limitações é que elas são comandadas para uma plataforma e abrem brecha para falhas
```

(b) fork() e exec()?

```bash
Com regras de execução você pode executar o argumento do exec parelelamente com uma função principal. É mais completo de se utilizar.
Como não existe uma forma de criar e executar um processo em um único passo, cria-se a cópia exata do processo com o fork() e usa-se o exec() para substituir o conteúdo desse processo criado, criando um novo processo.
```

3. É possível utilizar o exec() sem executar o fork() antes?

```bash
é possível, porém o processo pai terá o conteúdo perdido
```

Quais são as características básicas das seguintes funções:

(a) execp()?

```bash
Permite a execução do programa que está localizado no local atual.
```
(b) execv()?

```bash
permite que a lista de ações do novo processo seja nula, mas requer o caminho completo para execução do comando.
```

(c) exece()?

```bash
Permite que haja um argumento adicional no novo programa
```

(d) execvp()?

```bash
Os objetivos do programa são um programa fixo em NULL e o programa está localizado no caminho atual.

```

(e) execve()?

```bash
Permite que o nome ou a procura do programa esteja no caminho atual e que haja um argumento adicional no novo programa .

```

(f) execle()?

```bash
Permite que os mecanismos de var args sejam utilizados e que haja um argumento adicional no novo programa.
```
