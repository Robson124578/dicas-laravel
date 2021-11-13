# Integrando a aplicação com o banco de dados usando o SQLite

## Integrando a aplicação com o banco de dados usando o SQLite

para integrar o SQLite na aplicação temos que seguir os seguintes passos:

1°) analise o arquivo database.php dentro do diretório \config. O arquivo database.php guarda as conexões com o banco de dados em conections

O sqlite é ideal para utilização durante o desenvolvimento e teste quando aspectos como segurança e escalabilidade não são necessários. O interessante de usar o sqlite é que ele dispensa a instalação de um SGBD

![Untitled](Integrando%20a%20aplicac%CC%A7a%CC%83o%20com%20o%20banco%20de%20dados%20usan%20dea879756548445b931f99c510e72806/Untitled.png)

repare que a figura acima mosta as configurações relaciionada ao SQLite.

no campo url, database foreign_key_constraints estão recebendo informações por meio do método env() que verifica a existência das variáveis de ambiente e utiliza essas variáveis de ambiente na composição das strings de conexão. Essas variáveis por sua vez são determinadas dentro do arquivo .env na raiz da aplicação/projeto. sendo assim precisamos abrir o arquivo .env e configurar as variáveis de conexão que serão vistas na string de conexão lá no arquivo database.php.

Abaixo no arquivo .env vamos alterar as seguintes opções:

![Untitled](Integrando%20a%20aplicac%CC%A7a%CC%83o%20com%20o%20banco%20de%20dados%20usan%20dea879756548445b931f99c510e72806/Untitled%201.png)

A variável DB_CONNECTION vai receber o nome relativo ao driver na string de conexão do arquivo database.php ficando assim:

DB_CONNECTION=sqlite

2°) defnir a informação de database no arquivo database.php.

esse arqui

![Untitled](Integrando%20a%20aplicac%CC%A7a%CC%83o%20com%20o%20banco%20de%20dados%20usan%20dea879756548445b931f99c510e72806/Untitled%202.png)

O 'database' ⇒ env('DB_DATABASE', database_path('database.sqlite')), recebe além da variável de ambiente DB_DATABASE, como segundo parâmetro um helper do laravel que irá apontar para o diretório database na raiz do projeto procurando um arquivo chamado database.sqlite que conterá onde os dados de conexão serão armezenados, então dentro do diretório \database eu preciso criar um arquivo chamado database.sqlite. 

Exclua a linha

DB_DATABASE=laravel no arquivo .env.

Feito as configurações de variáveis de ambiente e o arquivo database.sqlite é hora de rodar as migrations. sendo assim acesse a linha de comando e digite:

```php
php artisan migrate
```

caso aconteça o seguinte erro:

![Untitled](Integrando%20a%20aplicac%CC%A7a%CC%83o%20com%20o%20banco%20de%20dados%20usan%20dea879756548445b931f99c510e72806/Untitled%203.png)

acesse o arquivo php.ini na pasta onde o php está intalado e retire o comentario da extensão ;extension=pdo_sqlite e tente fazer a migration novamente.

Após a migration ser executada, o arquivo database.sqlite, automaticamente será preenchido com as informações relacionadas a migration serão executadas.