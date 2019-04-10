Para todas as questões, utilize as funções da biblioteca `stdio.h` de leitura e de escrita em arquivo (`fopen()`, `fclose()`, `fwrite()`, `fread()`, dentre outras). Compile os códigos com o gcc e execute-os via terminal.

1. Crie um código em C para escrever "Ola mundo!" em um arquivo chamado 'ola_mundo.txt'.

```bash
**Resposta**


#include <stdio.h>

int main(int argc, char const *argv[])
{
	FILE * fp; // Declaração da estrutura
	fp = fopen("ola_mundo.txt","w+"); // w+ = empty file for r/w
	fprintf(fp, "Ola Mundo!\n");
	if (!fp)
        printf ("Erro na abertura do arquivo.");
	fclose(fp);
	return 0;
}
```

2. Crie um código em C que pergunta ao usuário seu nome e sua idade, e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Digite a sua idade: 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```bash
**Resposta**

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
	FILE * fp; // Declaração da estrutura
	char nome [100];
	char idade [20]; 
	char nome_arq[100];

	printf("Informe seu nome: \n");
	fgets(nome,100,stdin);
	printf("Informe sua idade: \n");
	fgets(idade,20,stdin);  

	strcpy(nome_arq,nome);
	strcat(nome_arq,".txt");

	fp = fopen(nome_arq,"w");

	fputs("Nome: ",fp);
	fputs(nome,fp);
	fputs("\n",fp);
	fputs("Idade: ",fp);
	fputs(idade,fp);
	fputs(" anos\n",fp);

	fclose(fp);
	return 0;

}

```

3. Crie um código em C que recebe o nome do usuário e e sua idade como argumentos de entrada (usando as variáveis `argc` e `*argv[]`), e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```
```bash
**Resposta**

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(int argc, char const *argv[])
{

if(argc==1)
{
	printf("Informe seu nome e sua idade após inserir o nome do programa (Ex: ./questao3.out Fulano 22) \n");
	exit(0);
}

	FILE *fp;
	char nome [100];
	char idade [20]; 
	char nome_arq[100];

	strcpy(nome,argv[1]);
	strcpy(idade,argv[2]);
	
	strcpy(nome_arq,nome);					//Copia nome em nome_arq
	strcat(nome_arq,".txt");				//Concatena ".txt" em nome_arq

	fp = fopen(nome_arq,"w");				//Abre o arquivo 

	if(!fp){
		printf("Não foi possivel abrir o arquivo");
		exit(0);
	}

	fputs("Nome: ",fp);
	fputs(nome,fp);
	fputs("\n",fp);
	fputs("Idade: ",fp);
	fputs(idade,fp);
	fputs(" anos\n",fp);

	fclose(fp);
	return 0;
}

```

4. Crie uma função que retorna o tamanho de um arquivo, usando o seguinte protótipo: `int tam_arq_texto(char *nome_arquivo);` Salve esta função em um arquivo separado chamado 'bib_arqs.c'. Salve o protótipo em um arquivo chamado 'bib_arqs.h'. Compile 'bib_arqs.c' para gerar o objeto 'bib_arqs.o'.

```bash
**Resposta**

//Como fazemos para ler o tamanho do arquivo 
//usamos uma função 
#include <stdio.h>

int tam_arq_texto(char *nome_arquivo)
{
	FILE * fp; 
	int tamanho = 0; 
	char c; //char é um byte

	
	fp = fopen(nome_arquivo,"r"); 

	while(c = getc(fp), c != EOF) //getchar e scanf retornam EOF quando não há caracteres a serem lidos
	{
		tamanho = tamanho+1;

    }

    fclose (fp);
    return tamanho;
}

int main(){

	int qualquerum;
	qualquerum = tam_arq_texto("./unb.txt");
	printf("Ele tem o tamanho %d bytes\n", qualquerum);
	return 0;
}

```

5. Crie uma função que lê o conteúdo de um arquivo-texto e o guarda em uma string, usando o seguinte protótipo: `char* le_arq_texto(char *nome_arquivo);` Repare que o conteúdo do arquivo é armazenado em um vetor interno à função, e o endereço do vetor é retornado ao final. (Se você alocar este vetor dinamicamente, lembre-se de liberar a memória dele quando acabar o seu uso.) Salve esta função no mesmo arquivo da questão 4, chamado 'bib_arqs.c'. Salve o protótipo no arquivo 'bib_arqs.h'. Compile 'bib_arqs.c' novamente para gerar o objeto 'bib_arqs.o'.

```bash
**Resposta**

#include <stdio.h>
#include <stdlib.h> // Para usar alocação de memoria dinâmica
					// maloc é necessário incluir essa biblioteca
char * le_arq_texto(char *nome_arquivo)
{

FILE * fp; 
char * data;
int tamanho = tam_arq_texto(nome_arquivo);
data = malloc(sizeof(char) * tamanho); //aloca em data
fp = fopen(nome_arquivo, "r");
	if(!fp)
	{
		printf("Erro ao abrir arquivo!\n");
		return 0;
	}
	fgets(data, tamanho, fp);
	fclose(fp);
	free(data);
	return data;
}
```

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
