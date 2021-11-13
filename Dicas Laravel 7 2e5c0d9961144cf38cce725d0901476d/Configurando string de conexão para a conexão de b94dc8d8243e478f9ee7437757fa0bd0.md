# Configurando string de conexão para a conexão de uma aplicação laravel com um banco de dados MySQL

Para conexão de uma aplicação laravel com um banco de dados MySQL, primeiramente temos que configurar o arquivo onde guarda as informações sobre a conexão (database.php). esse arquivo se encontra a partir da raiz da aplicação no diretório "config/database.php".

nele existe um array chamado conection onde possui alguns modelos de conexões para alguns banco de dados como, MySQL, Posgres, SQLServer e SqLite. no caso nós vamos nos conectar com o banco de dados MySQL. Para isso precisamos configurar a string de conexão situada no array associativo 'connections' no índice que o descreve como 'mysql'. sendo assim iremos configurar da seguinte forma:

![Untitled](Configurando%20string%20de%20conexa%CC%83o%20para%20a%20conexa%CC%83o%20de%20b94dc8d8243e478f9ee7437757fa0bd0/Untitled.png)

de acordo com o array mostrado acima, os seguintes dados devem ser alterados lembrando que é lá no arquivo .env é que serão colocados os dados necessários para conexão pois através do método env() as informações passadas no arquivo .env serão vistas no arquivo database.php.

![Untitled](Configurando%20string%20de%20conexa%CC%83o%20para%20a%20conexa%CC%83o%20de%20b94dc8d8243e478f9ee7437757fa0bd0/Untitled%201.png)

1°) No caso, o primeiro dado a ser alterado será o driver que no caso será o mysql ficanso assim:

DB_CONNECTION=mysql

2°)O próximo será o host(endereço do banco) que recebe 2 parâmetros no método env('DB_HOST', '127.0.0.1'), o primeiro verifica se a variável 'BD_HOST' está definida, caso não esteja, o método irá usar o segundo parâmetro que por sua vez é uma variável default

3°)'port' checar no arquivo .env a porta que por padrão estará definida no método env('BD_PORT', '3306') NO SEGUNDO PARÂMETRO

4°)'database' recebe o nome do banco de dados no qual a aplicação irá se comunicar pelo método env('DB_DATABASE').

5°) defina o DB_USERNAME e o DB_PASSWORD no arquivo .env para que possa ser interpretado no arquivo database.php através do método .env().

6°) no arquivo php.ini e php.ini-development, verifique se a extensão ;extension=pdo_mysql está descomentada pois o laravel utiliza o modelo de conexão PDO.

![Untitled](Configurando%20string%20de%20conexa%CC%83o%20para%20a%20conexa%CC%83o%20de%20b94dc8d8243e478f9ee7437757fa0bd0/Untitled%202.png)

Tendo feitas as configurações é hora de rodar a migration com o comando:

```php
php artisan migrate
```

caso ocorra tudo certo as configurações feitas na aplicação refletirão no banco de dados.