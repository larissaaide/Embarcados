1. Crie dois programas em C para criar um cliente e um servidor. Faça com que o cliente envie os valores 1, 2, 3, 4, 5, 6, 7, 
8, 9 e 10 para o servidor, com intervalos de 1 segundo entre cada envio. Depois de o cliente enviar o número 10, ele aguarda 1 
segundo e termina a execução. O servidor escreve na tela cada valor recebido, e quando ele receber o valor 10, ele termina a 
execução.

```bash
  **Código para o cliente** 
  
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>

int main (int argc, char* const argv[])
{
	char *socket_name;
	int socket_id;
	struct sockaddr name;

	socket_name = argv[1];// o socket é recebido por argv[1]

   for(int n = 1; n <= 10; n++)
    {      
	fprintf(stderr, "Abrindo o socket local... ");
	socket_id = socket(PF_LOCAL, SOCK_STREAM,0);   //criando o socket
	//FAMILIA: PF_LOCAL - COMUNICAÇÃO LOCAL, ENDEREÇO DE ARQUIVOS
	//TIPO DE COMUNICAÇÃO: SOCK_STREAM - CONFIÁVEL, BASEADO EM CONEXÃO
	//PROTOCOLO PADRÃO - 0 
	fprintf(stderr, "Feito!\n");
	fprintf(stderr, "Conectando o socket ao servidor no endereco local \"%s\"... ", socket_name);
    
//     DEFININDO ESTRUTURA sockaddr
	name.sa_family = AF_LOCAL;
	strcpy(name.sa_data, socket_name);
    connect(socket_id, &name, sizeof(name));    //ASSOCIANDO O DESCRITOR A ESTRUTURA, QUE TEM O ENDERECO
	fprintf(stderr, "Feito!\n");
	fprintf(stderr, "Mandando mensagem ao servidor... ");

    write(socket_id, &n, sizeof(n));    //ESCRENDO A MENSAGEM
    sleep(1);
    
    fprintf(stderr, "Feito!\n");

	fprintf(stderr, "Fechando o socket local... ");
	close(socket_id);
	fprintf(stderr, "Feito!\n");
	}
	return 0;
}
```

2. Crie dois programas em C para criar um cliente e um servidor. Execute a seguinte conversa entre cliente e servidor:

```
CLIENTE: Pai, qual é a verdadeira essência da sabedoria?
SERVIDOR: Não façais nada violento, praticai somente aquilo que é justo e equilibrado.
CLIENTE: Mas até uma criança de três anos sabe disso!
SERVIDOR: Sim, mas é uma coisa difícil de ser praticada até mesmo por um velho como eu...
```

Neste exercício, o cliente deve escrever no terminal as mensagens enviadas e recebidas.
