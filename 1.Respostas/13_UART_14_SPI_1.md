1. Cite as vantagens e desvantagens das comunicação serial:

(a) Assíncrona (UART).


```bash
A comunicação via UART necessita de menos pinos, apenas dois um para o Tx e o outro para o Rx, e é fácil de implementar e 
trabalhar, pois ambos dispositivos precisam apenas estar na velocidade de transmissão dos dados. Há também a possibilidade de 
verificar os dados enviados por meio de um bit de paridade. Em contrapartida, é muito mais lenta que as comunicações síncronas 
e a adição de mais dispositivos reduz ainda mais a taxa de transmissão dos dados para uma mesma baudrate, pois será necessário 
transmitir o endereço e um bit para verificar se a informação transmitida condiz sobre dados ou endereços.

```
b)
A comunicação SPI é extremamente rápida e não sofre com grandes diminuições na taxa de transferência de dados quando são adicionados mais dispositivos. As desvantagens são devido ao alto número de fios, geralmente quatro (MISO, MOSI, CLK e SS) e a ausência de uma forma nativa de verificar os dados enviados, como o bit de paridade do UART.

2-
Sim, não é necessário que o MSP430 aguarde, pois o protocolo UART é assíncrono, portanto é possível que haja envio e recepção de dados ao mesmo tempo.

3-
O MSP430 deve esperar a ativação da Raspberry Pi através do Chip Select e ainda deve esperar o envio dos dados a partir da Raspberry, o que depende do período do clock.

4-
A comunicação pode ser feita de maneira que se envie primeiro o enddereço do dispositivo ao qual o dado é destinado, então envie-se o bit AD antes dos bits de parada. Deste modo cada dispositivo só recebe a comunicação com os dados, a qual será enviada após o endereço, quando for solicitado.

5-
A comunicação SPI com dois dispositivos será feita pela utilização dos pinos de chip select, na qual cada dispositivo extra é acessado de uma vez, ou através de uma conexão daisy chain, na qual os dados dos dispositivos vão fluindo entre os registradores de deslocamento até atingirem o mestre.


(b) SPI.


2. Considere o caso em que a Raspberry Pi deve receber leituras analógico/digitais de um MSP430, e que a comunicação entre os dois é UART. É tecnicamente possível que o MSP430 mande os resultados da conversão A/D a qualquer hora, ou ele deve aguardar a Raspberry Pi fazer um pedido ao MSP430? Por quê?

3. Considere o caso em que a Raspberry Pi deve receber leituras analógico/digitais de um MSP430, que a comunicação entre os dois seja SPI, e que o MSP430 seja o escravo. É tecnicamente possível que o MSP430 mande os resultados da conversão A/D a qualquer hora, ou ele deve aguardar a Raspberry Pi fazer um pedido ao MSP430? Por quê?

4. Se o Raspberry Pi tiver de se comunicar com dois dispositivos via UART, como executar a comunicação com o segundo dispositivo?

5. Se o Raspberry Pi tiver de se comunicar com dois dispositivos via SPI, como executar a comunicação com o segundo dispositivo?
