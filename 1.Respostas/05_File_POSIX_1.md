1. Considerando a biblioteca-padrão da linguagem C, responda:

(a) Quais são as funções (e seus protótipos) para abrir e fechar arquivos?


```bash
FILE *fp;   
FILE *fopen (char *nome_do_arquivo, char *modo_de_acesso);
int fclose (FILE *fluxo);

```

(b) Quais são as funções (e seus protótipos) para escrever em arquivos?

```bash
int fprintf(FILE *fp, const char, *formato, ...);
void fputc (int caractere, FILE *fluxo);
void fputs (char *string, FILE *fluxo);
int putc (int c, FILE * fp);
unsigned fwrite (void *dados, int tamanho_do_elemento, int num_elementos, FILE *fluxo);
```

(c) Quais são as funções (e seus protótipos) para ler arquivos?

```bash
int fscanf(FILE *fp, char *format, ...); 
int getc(FILE

```

(d) Quais são as funções (e seus protótipos) para reposicionar um ponteiro para arquivo?

```bash
int fseek (FILE *fp, long int offset, int origin);
void rewind (FILE *fp);
int fsetpos(FILE *fp, const fpos_t *pos);'
```

(e) Quais bibliotecas devem ser incluídas no código para poder utilizar as funções acima?

```bash
biblioteca #include <stdio.h>
```

2. O que é a norma POSIX?

```bash
O POSIX (Interface Portátil para Sistemas Operacionais) é uma família de padrões especificados pelo IEEE para manter a compabtibilidade entre sistemas operacionais. Aonde são definidos vários aspectos como interface para
programação de aplicaçoes
```

3. Considerando a norma POSIX, responda:

(a) Quais são as funções (e seus protótipos) para abrir e fechar arquivos?

```bash
int open(const char * path, int oflag, ...);
int close(int fildes);
```

(b) Quais são as funções (e seus protótipos) para escrever em arquivos?

```bash
ssize_t write(int fildes, const void *buf, size_t nbyte);
```

(c) Quais são as funções (e seus protótipos) para ler arquivos?

```bash
ssize_t read(int fd, void *buf, size_t count);
```

(d) Quais são as funções (e seus protótipos) para reposicionar um ponteiro para arquivo?

```bash
off_t lseek(int fd, off_t offset, int whence);
```

(e) Quais bibliotecas devem ser incluídas no código para poder utilizar as funções acima?

```bash
As bibliotecas são <sys/types.h>, <sys/stat.h>, <fcntl.h> e <unistd.
```
