1. Considere um MSP430 sendo usado para leituras analógicas. O Raspberry Pi está conectado a ele via UART. O MSP430 foi 
programado para converter e enviar dados de 10 bits a cada 10 ms. Escreva o código para o Raspberry Pi receber estes dados, 
e a cada 1 segundo apresentar no terminal a média das últimas 100 amostras.

```bash
include <stdio.h>
#include <stdlib.h>
#include <wiringPi.h>
#include <wiringSerial.h>
#include <signal.h>

#define N 100

// Arquivo de acesso a porta serial
//#define TTY "/dev/ttyAMA0"
// Arquivo de acesso a porta serial
// PARA O RASPBERRY PI 3 E O RPI Zero
#define TTY "/dev/ttyS0" //pasta configuração da msp, arquivo de acesso da pasta serial 

int uart0_fd;
void ctrl_c(int sig)
{
	puts(" Fechando " TTY "...");
	serialClose(uart0_fd);
	exit(-1);
}

int main(void)
{
	unsigned int sum = 0;
	unsigned int counter = 0;

	signal(SIGINT, ctrl_c);
	wiringPiSetup();
	uart0_fd = serialOpen(TTY, 9600);
	serialFlush(uart0_fd);
	while(1)
	{
		sum += (unsigned int) serialGetchar(uart0_fd);
		sum += ((unsigned int) serialGetchar(uart0_fd))<<8;
		counter++;
		if(counter==N)
		{
			sum += (N/2); //arredonda pra cima apartir de 0.5
			sum /= N;
			system("date +%T");
			printf("Media das amostras = %d\n", sum);
			sum = 0;
			counter = 0;
		}
	}
}
```
2. Considere um MSP430 sendo usado para leituras analógicas. O Raspberry Pi está conectado a ele via SPI, e é o mestre. 
O MSP430 foi programado para funcionar da seguinte forma:

- O MSP430 recebe o byte `0x55` e envia o byte `0xAA`, o que indica o começo de conversão. 
- 100us depois, o MSP430 recebe os bytes `0x01` e `0x02`, e envia o byte menos significativo e o mais significativo da 
conversão de 10 bits, nesta ordem.

Escreva o código para o Raspberry Pi executar este protocolo, de forma a obter conversões a cada 10 ms. A cada 1 segundo ele 
deve apresentar no terminal a média das últimas 100 amostras.

```bash 
#include <stdio.h>
#include <stdlib.h>
#include <wiringPi.h>
#include <wiringPiSPI.h>
#include <signal.h>
#include <unistd.h>

#define N 100
#define PERIODO 10e3
#define DLY 100

int spi_fd;
void ctrl_c(int sig)
{
	close(spi_fd);
	exit(-1);
}

int main(void)
{
	unsigned int sum = 0;
	unsigned int counter = 0;
	unsigned char send_msp430;

	signal(SIGINT, ctrl_c);
	wiringPiSetup();
	spi_fd = wiringPiSPISetup (0, 500000);
	while(1)
    {
		usleep(PERIODO);
		do
		{
			send_msp430 = 0x55;
			wiringPiSPIDataRW(0, &send_msp430, 1);
		} 
    while(send_msp430!=0xAA);
		usleep(DLY);
		send_msp430 = 0x1;
		wiringPiSPIDataRW(0, &send_msp430, 1);
		sum += (unsigned int) send_msp430;
		send_msp430 = 0x2;
		wiringPiSPIDataRW(0, &send_msp430, 1);
		sum += ((unsigned int) send_msp430)<<8;
		counter++;
		if(counter==N)
		{
			sum += (N/2);
			sum /= N;
			system("date +%T");
			printf("Media das amostras = %d\n", sum);
			sum = 0;
			counter = 0;
		}
	}
} 
``` 
