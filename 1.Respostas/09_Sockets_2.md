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
    
	//DEFININDO ESTRUTURA sockaddr
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

**Códio Servidor**

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <signal.h>
#include <sys/socket.h>
#include <sys/un.h>

char socket_name[50];
int socket_id;
void sigint_handler(int signum);
void end_server(void);

int main (int argc, char* const argv[])
{
	struct sockaddr socket_struct;

	strcpy(socket_name, argv[1]); //Recebe-se socket name por argv[1]
	signal(SIGINT, sigint_handler); //Associando a função para ser fechada com o "CTRL+C"
	socket_id = socket(PF_LOCAL, SOCK_STREAM, 0);//criando o socket
	socket_struct.sa_family = AF_LOCAL;
	strcpy(socket_struct.sa_data, socket_name);
       /*Quando	criado,	um	socket	não	tem	um	endereço local e nem um	
		endereço remoto. Um	servidor usa o procedimento	bind para	
		prover um número de	porta de protocolo em que o	servidor	
		esperará	por	contato.*/
	bind(socket_id, &socket_struct, sizeof(socket_struct));	
	listen(socket_id, 10);

	while(1)
	{
		struct sockaddr cliente;
		int socket_id_cliente;
		int msg;
		socklen_t cliente_len;

		fprintf(stderr, "Aguardando a conexao de um cliente... ");
		socket_id_cliente = accept(socket_id, &cliente, &cliente_len);
		read(socket_id_cliente, &msg, 1);
		fprintf(stderr,"\n\n   Mensagem = %d\n\n", msg);
		if (msg == 10)
		{
			fprintf(stderr, "Cliente pediu para o servidor fechar.\n");
			end_server();
		}

		fprintf(stderr, "Fechando a conexao com o cliente... ");
		close(socket_id_cliente);
		fprintf(stderr, "Feito!\n");
	}
	return 0;
}

void sigint_handler(int signum)
{
	fprintf(stderr, "\nRecebido o sinal CTRL+C... vamos desligar o servidor!\n");
	end_server();
}

void end_server(void)
{
	fprintf(stderr, "Apagando \"%s\" do sistema... ", socket_name);
	unlink(socket_name);
	fprintf(stderr, "Feito!\n");
	fprintf(stderr, "Fechando o socket local... ");
	close(socket_id);
	fprintf(stderr, "Feito!\n");
	exit(0);
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
