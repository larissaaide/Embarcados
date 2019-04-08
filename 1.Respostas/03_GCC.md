Para todas as questões, compile-as com o gcc e execute-as via terminal.

1. Crie um "Olá mundo!" em C.

```bash
**Resposta** 

#include <stdio.h>

int main(void) 
{

 printf ("Olá mundo!\n");


 return 0;
 
}
```

2. Crie um código em C que pergunta ao usuário o seu nome, e imprime no terminal "Ola " e o nome do usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Ola Eu
```


```bash
**Resposta** 

#include <stdio.h>

int main(void) 
{
 
char nome [30];	
 printf ("Digite seu nome: \n");
 scanf ("%s", nome);
 printf ("Olá %s\n", nome);

 return 0;
}
```

3. Apresente os comportamentos do código anterior nos seguintes casos:

(a) Se o usuário insere mais de um nome.
```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu Mesmo
```
**Resposta**
Olá Eu

(b) Se o usuário insere mais de um nome entre aspas duplas. Por exemplo:
```bash
$ ./ola_usuario_1
$ Digite o seu nome: "Eu Mesmo"
```
**Resposta**
Olá "Eu

(c) Se é usado um pipe. Por exemplo:
```bash
$ echo Eu | ./ola_usuario_1
```
**Resposta**
Digite seu nome:
Olá Eu

(d) Se é usado um pipe com mais de um nome. Por exemplo:
```bash
$ echo Eu Mesmo | ./ola_usuario_1
```
**Resposta**
Digite seu nome:
Olá Eu

(e) Se é usado um pipe com mais de um nome entre aspas duplas. Por exemplo:
```bash
$ echo "Eu Mesmo" | ./ola_usuario_1
```
**Resposta**
Digite seu nome:
Olá Eu

(f) Se é usado o redirecionamento de arquivo. Por exemplo:
```bash
$ echo Ola mundo cruel! > ola.txt
$ ./ola_usuario_1 < ola.txt
```
**Resposta**
Digite seu nome:
Olá Ola

4. Crie um código em C que recebe o nome do usuário como um argumento de entrada (usando as variáveis argc e *argv[]), e imprime no terminal "Ola " e o nome do usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu
$ Ola Eu
```
```bash
**Resposta**

#include <stdio.h>

int main(int argc, char **argv)
{
	if(argc==1)
		printf("Informe seu nome após inserir o nome do programa (Ex: ./argg.out Fulano) \n");
	if(argc>1)
		printf("Olá %s\n", argv[1]);
	return 0;
}

```
5. Apresente os comportamentos do código anterior nos seguintes casos:

(a) Se o usuário insere mais de um nome.
```bash
$ ./ola_usuario_2 Eu Mesmo
```
**Resposta**
Olá Eu

(b) Se o usuário insere mais de um nome entre aspas duplas. Por exemplo:
```bash
$ ./ola_usuario_2 "Eu Mesmo"
```
**Resposta**
Olá Eu mesmo

(c) Se é usado um pipe. Por exemplo:
```bash
$ echo Eu | ./ola_usuario_2
```
**Resposta**
Informe seu nome após inserir o nome do programa (Ex: ./argg.out Fulano) 

(d) Se é usado um pipe com mais de um nome. Por exemplo:
```bash
$ echo Eu Mesmo | ./ola_usuario_2
```
**Resposta**
Informe seu nome após inserir o nome do programa (Ex: ./argg.out Fulano)

(e) Se é usado um pipe com mais de um nome entre aspas duplas. Por exemplo:
```bash
$ echo Eu Mesmo | ./ola_usuario_2
```
**Resposta**
Informe seu nome após inserir o nome do programa (Ex: ./argg.out Fulano)

(f) Se é usado o redirecionamento de arquivo. Por exemplo:
```bash
$ echo Ola mundo cruel! > ola.txt
$ ./ola_usuario_2 < ola.txt
```
**Resposta**
bash: ./argg.c: Permissão negada

6. Crie um código em C que faz o mesmo que o código da questão 4, e em seguida imprime no terminal quantos valores de entrada foram fornecidos pelo usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_3':

```bash
$ ./ola_usuario_3 Eu
$ Ola Eu
$ Numero de entradas = 2
```

```bash
**Resposta**

#include <stdio.h>

int main(int argc, char **argv)
{
	printf("Numero de entradas = %d\n",argc);
	if(argc==1)
	       printf("Informe seu nome após inserir o nome do programa (Ex: ./argg.out Fulano) \n");
	else
	       printf("Olá ");

	for (int i=1; i<argc; i++)
	{
		if(argc>1)
			printf("%s ", argv[i]);
	}

	printf("\n");
	return 0;
}
```

7. Crie um código em C que imprime todos os argumentos de entrada fornecidos pelo usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_argumentos':

```bash
$ ./ola_argumentos Eu Mesmo e Minha Pessoa
$ Argumentos: Eu Mesmo e Minha Pessoa
```
```bash
**Resposta**

#include <stdio.h>

int main(int argc, char **argv)
{
	printf("Numero de entradas = %d\n",argc);
	if(argc==1)
		printf("Informe o argumento após inserir o nome do programa (Ex: ./argg.out Argumento) \n");
	else
		printf("Argumento: ");
	for (int i=1; i<argc; i++)
	{
		if(argc>1)
			printf("%s ", argv[i]);
	}
	printf("\n");
	return 0;
}
```
8. Crie uma função que retorna a quantidade de caracteres em uma string, usando o seguinte protótipo:
`int Num_Caracs(char *string);` Salve-a em um arquivo separado chamado 'num_caracs.c'. Salve o protótipo em um arquivo chamado 'num_caracs.h'. Compile 'num_caracs.c' para gerar o objeto 'num_caracs.o'.

```bash
**Resposta**

****************num_caracs.c****************
#include <stdio.h>

int Num_Caracs(char *string){
int i=0;

while(*string!='\0'){
i++;
string++;
}

return i;
}

****************num_caracs.h****************
#ifndef _H_NUM_CARACS
#define _H_NUM_CARACS

int Num_Caracs(char *string);

#endif

```

9. Re-utilize o objeto criado na questão 8 para criar um código que imprime cada argumento de entrada e a quantidade de caracteres de cada um desses argumentos. Por exemplo, considerando que o código criado recebeu o nome de 'ola_num_caracs_1':

```bash
$ ./ola_num_caracs_1 Eu Mesmo
$ Argumento: ./ola_num_caracs_1 / Numero de caracteres: 18
$ Argumento: Eu / Numero de caracteres: 2
$ Argumento: Mesmo / Numero de caracteres: 5
```
```bash
**Resposta**

#include <stdio.h>
#include "num_caracs.h"

int main(int argc, char **argv)
{
int i=0;
while(i<argc){
char *string = argv[i];
printf("Argumento: %s / Numero de caracteres: %d\n", argv[i],Num_Caracs(string));
i++;
}
return 0;
}
```
10. Crie um Makefile para a questão anterior.

```bash

ola_num_caracs: ola_num_caracs_1.o num_caracs.o
	gcc $(CFLAGS) -o ola_num_caracs ola_num_caracs_1.o num_caracs.o
ola_num_caracs_1.o: num_caracs.h
	gcc $(CFLAGS) -c ola_num_caracs_1.c
num_caracs.o: num_caracs.c num_caracs.h
	gcc $(CFLAGS) -c num_caracs.c
clean:
	rm *.o
remove:
	rm ola_num_caracs
```

11. Re-utilize o objeto criado na questão 8 para criar um código que imprime o total de caracteres nos argumentos de entrada. Por exemplo, considerando que o código criado recebeu o nome de 'ola_num_caracs_2':

```bash
$ ./ola_num_caracs_2 Eu Mesmo
$ Total de caracteres de entrada: 25
```

12. Crie um Makefile para a questão anterior.
