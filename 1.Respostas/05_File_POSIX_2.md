Para todas as questões, utilize as funções da norma POSIX (`open()`, `close()`, `write()`, `read()` e `lseek()`). Compile os códigos com o gcc e execute-os via terminal.

1. Crie um código em C para escrever "Ola mundo!" em um arquivo chamado 'ola_mundo.txt'.

```bash
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>

int main(int argc, char const *argv[])
{
	int fd,rec;
	fd = open("olamundo.txt", O_RDWR | O_CREAT, S_IWUSR | S_IRUSR); //criar e sendo aberto para leitura e gravação.
	if (fd < 0)
	{
		printf("Erro ao abrir arquivo!\n");
		return 0;
	}
	char data[] = "Ola Mundo!\n";
	if (strlen(data) == write(fd, data, sizeof(strlen(data))))
	{
		printf("Erro ao gravar no arquivo!\n");
	}
	close(fd);
	return 0;
}

```

2. Crie um código em C que pergunta ao usuário seu nome e sua idade, e escreve este conteúdo em um arquivo com o seu nome e
extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Digite a sua idade: 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```bash
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/stat.h>

int main(int argc, char const *argv[])
{
  FILE *fp 
  int fd; 
  char nome[20], idade[3], n[]= "Nome: ", id[] = "\nIdade: ";
  printf("Digite seu nome: \n");
	scanf("%s", nome);
	printf("Digite sua idade: \n");
	scanf("%s", idade);
	nome[strcspn(nome,"\n")] = 0;
	fd = open(strcat(nome,".txt"), O_RDWR | O_CREAT, S_IWUSR | S_IRUSR);
	if (fd < 0)
	{
		printf("Erro ao abrir arquivo!\n");
		return 0;
	}
	write(fd, n, sizeof(n));
	write(fd, nome, sizeof(nome));
	write(fd, id, sizeof(id));
	write(fd, idade, sizeof(idade));
	close(fd);
	return 0;
}
```


3. Crie um código em C que recebe o nome do usuário e a sua idade como argumentos de entrada (usando as variáveis `argc` e 
`*argv[]`), e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código 
criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```bash
include <stdio.h>
#include <stdlib.h>
#include <unistd.h> 
#include <fcntl.h> 
#include <termios.h>
#include <string.h>


int main(int argc, char const *argv[])
{
  if (argc < 3)
	{
		printf("Digite seu nome e a sua idade\n");
		return 0;
	}
  
  int fd; 
  char nome[20], idade[3], n[]= "Nome: ", id[] = "\nIdade: ";
  printf("Digite seu nome: \n");
	scanf("%s", nome);
	printf("Digite sua idade: \n");
	scanf("%s", idade);
	nome[strcspn(nome,"\n")] = 0;
	fd = open(strcat(nome,".txt"), O_RDWR | O_CREAT, S_IWUSR | S_IRUSR);
	if (fd < 0)
	{
		printf("Erro ao abrir arquivo!\n");
		return 0;
	}
	write(fd, n, sizeof(n));
	write(fd, nome, sizeof(nome));
	write(fd, id, sizeof(id));
	write(fd, idade, sizeof(idade));
	close(fd);
	return 0;
}
```

```

4. Crie uma função que retorna o tamanho de um arquivo, usando o seguinte protótipo: `int tam_arq_texto(char *nome_arquivo);` Salve esta função em um arquivo separado chamado 'bib_arqs.c'. Salve o protótipo em um arquivo chamado 'bib_arqs.h'. Compile 'bib_arqs.c' para gerar o objeto 'bib_arqs.o'.

5. Crie uma função que lê o conteúdo de um arquivo-texto e o guarda em uma string, usando o seguinte protótipo: `char* le_arq_texto(char *nome_arquivo);` Repare que o conteúdo do arquivo é armazenado em um vetor interno à função, e o endereço do vetor é retornado ao final. (Se você alocar este vetor dinamicamente, lembre-se de liberar a memória dele quando acabar o seu uso.) Salve esta função no mesmo arquivo da questão 4, chamado 'bib_arqs.c'. Salve o protótipo no arquivo 'bib_arqs.h'. Compile 'bib_arqs.c' novamente para gerar o objeto 'bib_arqs.o'.

6. Crie um código em C que copia a funcionalidade básica do comando `cat`: escrever o conteúdo de um arquivo-texto no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'cat_falsificado':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./cat_falsificado ola.txt
$ Ola mundo cruel! Ola universo ingrato!
```

7. Crie um código em C que conta a ocorrência de uma palavra-chave em um arquivo-texto, e escreve o resultado no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'busca_e_conta':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./busca_e_conta Ola ola.txt
$ 'Ola' ocorre 2 vezes no arquivo 'ola.txt'.
```
