# Deploy de uma applicação laravel em ambiente compartilhado

Para este deploy, utilizarei o github. sendo assim é importante que meu projeto esteja sendo versionado no github.

Primeiramente vou criar um repositório no meu github e enviar os arquivos do meu projeto para lá.

![Untitled](Deploy%20de%20uma%20applicac%CC%A7a%CC%83o%20laravel%20em%20ambiente%20com%20b80392d334ca41789755edc44577c262/Untitled.png)

Após ter criado o repositório, preciso enviar o o projeto laravel seguindo passo a passo como a figura acima descreve.

Obs: quando empurramos os arquivos para o repositório no github, agluns arquivos não serão commitados entre eles a pasta vendor que no caso teremos que instalar pela hospedagem.

Obs: quanto ao deploy dos arquivos no servidor compartilhado, ele deve ser feito no mesmo nível da pasta public_html e não dentro da mesma.

Agora vou acessar meu servidor pelo cmd via ssh e clonar o repositório que esta sendo versionado no github.

![Untitled](Deploy%20de%20uma%20applicac%CC%A7a%CC%83o%20laravel%20em%20ambiente%20com%20b80392d334ca41789755edc44577c262/Untitled%201.png)

No servido existe uma pasta visível que é a public_html, porém a aplicação esta fora da pasta public_html, no caso no mesmo nível de diretório e também possui uma pasta public.

neste caso eu preciso apontar a pasta public_html do servidor para a pasta public da aplicação como mostrado abaixo:

```php
-bash-4.2$ ls 
// ao listar como o comando ls eu terei 2 pastas que é a 
//public_html (pasta visível no servidor) e a pasta da aplicação
//como mostrado abaixo

domains  DO_NOT_UPLOAD_HERE  public_html  testes-laravel

//agora eu vou renomea-la de public_html
//para public_html_bkp como mostrado abaixo

-bash-4.2$ mv public_html public_html_bkp

-bash-4.2$ ls // após dar um no ls veja que a pasta foi renomeada.
domains  DO_NOT_UPLOAD_HERE  public_html_bkp  testes-laravel

// agora preciso apontar a pasta 'public' da minha aplicação para o 
//public do servidor com o comando abaixo:
//A partir da raiz
-bash-4.2$ ln -s testes-laravel/public public_html

// se eu der o comando ls -la verei que agora a minha public_html
//esta apontando para a public da aplicação como mostrado abaixo:

-bash-4.2$ ls -la
total 48
drwx--x--- 11 u304591913 apache    4096 Nov  7 16:12 .
drwxr-xr-x  3 root       root      4096 Aug 11  2020 ..
-rw-------  1 u304591913 o50030127  269 Nov  7 04:56 .bash_history
drwxr-xr-x  3 u304591913 o50030127 4096 Nov  7 03:44 .cache
drwxrwx--x  5 u304591913 o50030127 4096 Aug 11  2020 .cagefs
drwxr-xr-x  2 u304591913 o50030127 4096 Jun  8 12:47 .cl.selector
drwxr-xr-x  3 u304591913 o50030127 4096 Nov  7 03:44 .config
drwxr-xr-x  3 u304591913 o50030127 4096 Aug 11  2020 domains
-rw-r--r--  1 u304591913 o50030127    0 Aug 11  2020 DO_NOT_UPLOAD_HERE
drwxr-xr-x  3 u304591913 o50030127 4096 Nov  7 03:44 .local
drwxr-xr-x  2 u304591913 o50030127 4096 Aug 11  2020 .logs
drwxr-----  3 u304591913 o50030127 4096 Nov  7 15:45 .pki
lrwxrwxrwx  1 u304591913 o50030127   21 Nov  7 16:12 public_html -> testes-laravel/public
lrwxrwxrwx  1 u304591913 o50030127   40 Aug 11  2020 public_html_bkp -> domains/robsonmoreira.com.br/public_html
drwxr-xr-x 12 u304591913 o50030127 4096 Nov  7 15:45 testes-laravel
-bash-4.2$

```