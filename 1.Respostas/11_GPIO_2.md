1. Escreva um código em C para gerar uma onda quadrada de 1 Hz em um pino GPIO do Raspberry Pi.

```bash
#include <wiringPi.h>
#include <unistd.h>

wiringPi int main()
{
int pin = 4;		
float val = 500000;

  if(wiringPiSetup() == -1)
   return -1;
  
  while(1)
  {
	  pinMode(pin, OUTPUT);
	  digitalWrite(pin, LOW);
	  usleep(val);
  	digitalWrite(pin, HIGH);
	  usleep(val);

  }

return 0;
}

```

2. Generalize o código acima para qualquer frequência possível.

```bash
#include <wiringPi.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h> wiringPi int main(){

	int pin = 4;	

	float f = 0, 
  float t = 0;

		if(wiringPiSetup()== -1)
	      return -1;
		    printf("Escolha uma frequência:\n");
		    scanf("%f", &f);
		    t = (1/(2*f))*1000000;


	while(1)
  {
	
		pinMode(pin, OUTPUT);
		digitalWrite(pin, LOW);
		usleep(t);
		digitalWrite(pin, HIGH);
		usleep(t);
	 }
return 0;
} 
```

3. Crie dois processos, e faça com que o processo-filho gere uma onda quadrada, enquanto o processo-pai lê um botão no GPIO, 
aumentando a frequência da onda sempre que o botão for pressionado. A frequência da onda quadrada deve começar em 1 Hz, e 
dobrar cada vez que o botão for pressionado. A frequência máxima é de 64 Hz, devendo retornar a 1 Hz se o botão for pressionado novamente.

```bash
#include <wiringPi.h>
#include <sys/types.h>
#include <unistd.h>
#include <signal.h>

#define SAIDA 7
#define ENTRADA 11
#define MAX_MEIO_PERIODO (1e6/2)
#define MIN_MEIO_PERIODO (1e6/128)

int meio_periodo = MAX_MEIO_PERIODO;

void muda_freq()
{
	meio_periodo /= 2;
	if(meio_periodo<MIN_MEIO_PERIODO)
		meio_periodo = MAX_MEIO_PERIODO;
}

int main(void)
{
	pid_t filho;
	wiringPiSetup();
	pinMode(SAIDA, OUTPUT);
	pinMode(ENTRADA, INPUT);
	pullUpDnControl(ENTRADA, PUD_UP);
	signal(SIGUSR1, muda_freq);
	filho = fork();
	if(filho==0)
	{
		while(1)
		{
			digitalWrite(SAIDA, HIGH);
			usleep(meio_periodo);
			digitalWrite(SAIDA, LOW);
			usleep(meio_periodo);
		}
	}
	else
	{
		while(1)
		{
			while(digitalRead(ENTRADA)>0);
			kill(filho,SIGUSR1);
			while(digitalRead(ENTRADA)==0);
			usleep(100000);
		}
	}
}
```
