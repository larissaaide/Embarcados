1. Utilize o programa criado pelo professor para baixar as páginas principais dos seguintes sites:

O código usado foi o Sistemas_Embarcados/Code/10_Clientes_HTTP/01_http.c

(a) www.google.com

Pedido HTTP:

---------------------------------------
GET / HTTP/1.1
Host: www.google.com
User-Agent: HTMLGET 1.1
Accept: */*

---------------------------------------
Recebendo o resultado HTML e o escrevendo no arquivo 'saida.html'... 

**Página não carregou totalmente

(b) www.google.com.br

Pedido HTTP:

---------------------------------------
GET / HTTP/1.1
Host: www.google.com.br
User-Agent: HTMLGET 1.1
Accept: */*

---------------------------------------
Recebendo o resultado HTML e o escrevendo no arquivo 'saida.html'... 

**Página não carregou totalmente

HTTP/1.1 200 OK Date: Thu, 16 May 2019 14:46:48 GMT Expires: -1 Cache-Control: private, max-age=0 Content-Type: text/html; charset=ISO-8859-1 P3P: CP="This is not a P3P policy! See g.co/p3phelp for more info." Server: gws X-XSS-Protection: 0 X-Frame-Options: SAMEORIGIN Set-Cookie: 1P_JAR=2019-05-16-14; expires=Sat, 15-Jun-2019 14:46:48 GMT; path=/; domain=.google.com.br Set-Cookie: NID=183=Cn4i4exWAUwO5Uyd7bZH5NveFNuW3CdXE73CT0BDoyN-1RnQNJHa3FHIIAwg5r_I8oSZdn7lWu4U6g3lKpBIoChq0xC1UFKiQpcYHNYxMbkIo0kxPOg52guvn3w8UdaqQV6as9sb2PQKVgBtenHDCVFrMRsBS5TJIc1GwPefZsE; expires=Fri, 15-Nov-2019 14:46:48 GMT; 

(c) www.unb.br

Pedido HTTP:

---------------------------------------
GET / HTTP/1.1
Host: www.unb.br
User-Agent: HTMLGET 1.1
Accept: */*

---------------------------------------
Recebendo o resultado HTML e o escrevendo no arquivo 'saida.html'...

**Página carregou totalmente

HTTP/1.1 200 OK Server: nginx Date: Thu, 16 May 2019 14:44:28 GMT Content-Type: text/html; charset=utf-8 Transfer-Encoding: chunked Connection: keep-alive Vary: Accept-Encoding Referrer-Policy: origin Upgrade-Insecure-Requests: 0 Set-Cookie: 3ec986f4f850e1d0bdcd00fd24b0c473=ugk3jacfqgvi4r2egv1vkm93gf; path=/; HttpOnly Expires: Wed, 17 Aug 2005 00:00:00 GMT Last-Modified: Thu, 16 May 2019 14:44:28 GMT Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0 Pragma: no-cache Vary: Accept-Encoding X-Content-Type-Options: nosniff X-XSS-Protection: 1; mode=block X-Frame-Options: SAMEORIGIN X-XSS-Protection: 1; mode=block X-Frame-Options: SAMEORIGIN X-Content-Type-Options: nosniff 1dbe

(d) [fga.unb.br](fga.unb.br)

Pedido HTTP:

---------------------------------------
GET / HTTP/1.1
Host: fga.unb.br
User-Agent: HTMLGET 1.1
Accept: */*

---------------------------------------
Recebendo o resultado HTML e o escrevendo no arquivo 'saida.html'... 

**O documento saída.html estava em branco e página não abriu 


Comente os resultados obtidos para cada página, em termos das respostas HTTP e HTML obtidas.
