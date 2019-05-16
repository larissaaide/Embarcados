1. Especifique algumas portas importantes pré-definidas para o protocolo TCP/IP.

```bash
  80: HTTP 
  443: HTTPS
  Porta 110 - POP3
  Porta 119 - NNTP
  25: SMTP (para mandar e-mails) 
  53: DNS
  22: SSH
```


2. Com relação a endereços IP, responda:

(a) Qual é a diferença entre endereços IP externos e locais?

```bash
 O IP LOCAL é usado apenas na sua rede local, e é fornecido/controlado pelo seu roteador. Já o IP EXTERNO é usado na internet,e é controlado pelo Servidor.
```

(b) Como endereços IP externos são definidos? Quem os define?

```bash
O serviço provedor de internet (ISP) define seu endereço IP externo.
```

(c) Como endereços IP locais são definidos? Quem os define?

```bash
Os endereços locais são definidos através do servidor DHCP (Dynamic Host Configuration Protocol) que expede endereços IP únicos para uma rede local.
```

(d) O que é o DNS? Para que ele serve?

```bash
O Sistema de Nomes de Domínio, mais conhecido pela nomenclatura em Inglês Domain Name System (DNS), é um sistema hierárquico e distribuído de gerenciamento de nomes para computadores, serviços ou qualquer máquina conectada à Internet ou a uma rede privada. Faz a associação entre várias informações atribuídas a nomes de domínios e cada entidade participante. Por padrão, o DNS usa o protocolo User Datagram Protocol (UDP) na porta 53 para servir as solicitações e as requisições.
```

3. Com relação à pilha de protocolos TCP/IP, responda:

(a) O que são suas camadas? Para que servem?

```bash
São conjuntos de protocolos, onde cada camada é responsável por um grupo de tarefas, fornecendo um conjunto de serviços bem defnidos para o protocolo de camada superior.
```

(b) Quais são as camadas existentes? Para que servem?

```bash
*Aplicação*: camada responsável por fazer a troca de infromações entre processos, assim sua funcionalidade é padronizar a forma com que os programas consigam conversar entre si, definindo regras que devem ser obedecidas por todos os softwares que implementem tal serviço.

*Transporte*: é a camada responsável por criar uma comunicação host-to-host, ou seja, ela faz uma conexão virtual entre a origem e o destino. Os principais protocolos dessa camada são o TCP (Transmission Control Protocol - Protocolo de Controle de Transmissão) e o UDP (User Datagram Protocol - protocolo de datagramas do usuário).

*Internet*: camada responsável pela troca de informações entre redes, nela temos o protocolo IP que pega os dados recebidos da camada de Transporte e adiciona uma informação de endereço virtual. Quando se fala nisso, se fala em roteadores, que são os responsáveis por esse trabalho.

*link*: camada responsável pela troca de informção fisíca, nela se envia os dados das camadas superiores pela rede.
```

(c) Quais camadas são utilizadas pela biblioteca de sockets?

```bash
Os sockets estão entre a camada de transporte e a de aplicação. Estando nesse ponto de intercessão, eles conseguem fazer uma interface entre a aplicação e rede de maneira bem transparente. Assim, aplicações são implementadas através de uma comunicação lógica. Lógica no sentido de que para esses programas, eles estão se comunicando diretamente um com o outro, mas na prática, eles estão passando pela rede para trocar mensagens
```

(d) As portas usadas por servidores na função bind() se referem a qual camada?

```bash
Utiliza a camada de IP e de transporte
```

(e) Os endereços usados por clientes na função connect() se referem a qual camada?

```bash
Utiliza a cama de rede.
```
4. Qual é a diferença entre os métodos `GET` e `POST` no protocolo HTTP?

```bash
Visibilidade – A grande diferença entre os métodos GET e POST provavelmente é a visibilidade. Uma requisição GET é enviada como string anexada a URL, enquanto que a requisição POST é encapsulada junto ao corpo da requisição HTTP e não pode ser vista.

Tamanho – Como a requisição GET é feita via URL, obviamente há uma limitação no tamanho da mensagem enviada. A string não pode conter mais que 255 caracteres(embora exista diferenças entre navegadores, mas em geral o limite é 255). Já na requisição POST não há limitações de comprimento da mensagem, já que a mesma é enviada no corpo da requisição HTTP.

Performance – A requisição GET é relativamente mais rápida, já que ela é mais simples. Na requisição POST há uma perda de tempo no encapsulamento da mensagem.

Tipos – Já que GET é enviado via URL, então nós sabemos que ela só transporta textos. A requisição POST não tem restrições, pode transportar tanto texto, como dados binários.

Método HTML Padrão – GET é o método HTML padrão. Para submeter um formulário HTML usando POST é preciso especificar no atributo “method” o valor “POST”.

Dados – As requisições GET são limitadas ao padrão ASCII, enquanto que requisições POST também podem usar o atributo “enctype” com o valor “multipart/form-data”, que faz uso do padrão UCS(Universal Multiple-Octet Coded Character Set)
```
