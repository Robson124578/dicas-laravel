# Models e Migrations

Os models no contexto do laravel são as classes que representam os objetos na aplicação. Através dos models podemos trazer para a aplicação os benefícios da programação orientada a objetos assim reutilizando códigos.

Ao se criar um model, caso queiramos que ele venha persistir informações em um banco de dados utilizamos o seguinte comando:

```php
//Com o comando abaixo eu consigo criar um model chamado SiteContato
//Obs: a última instrução '-m' indica que além da criação do model, será 
//criado uma migration
php artisan make:model SiteContato -m
```

Após o comando será criado a estrutura base de um model na raiz diretório app.

## Implementando Migrations

As migrations nos permitem modelar um banco de dados pelo modelar os dados da aplicação sem sem utilizar o SQL. Elas são como registros ou scripts podendo inclusive serem versionados que nos dão a possibilidade de construir ou reconstruir tabelas no banco de dados.

As migrations fican dentro do diretório database\migrations

A migration permite modelar o banco de dados pelo próprio php assim conseguindo construir e reconstruir tabelas do banco de dados. As migrations estão dentro do diretório /database. Como ela foi criada assim que criamos o model, ela ja possui sua estrutura com dois métodos: up() e down() , para criação e deleção de uma tabela. Abaixo, através do método up() podemos estruturar a tabela de acordo com os tipos de dados que queremos modelar do método $table->tipos_de_dado() como mostrado abaixo: 

```php

public function up()
    {
        Schema::create('site_contatos', function (Blueprint $table) {
            //Aqui estou implementando os indice que serão as colunas da tabela
						$table->id();
            $table->timestamps();
            $table->string('nome', 50);
            $table->string('telefone', 20);
            $table->string('email', 80);
            $table->integer('motivo_contato');
            $table->text('mensagem');
        });
    }
```

Para saber os tipos de colunas usados junto com o $table, acesse:

[Database: Migrations](https://laravel.com/docs/7.x/migrations#introduction)

## Criação de uma migration

Para criar uma migration basta utilizar o comando:

```php
//É importante atentarmos para a convenção de criação de uma migrate iniciando
//com a palavra 'create', nome da migration e table para finalizar como mostrado
//abaixo:
php artisan make migrate create_dados_clientes_table

//obs: caso eu não tivesse colocado o 's' no final da palavra 'clientes' ele teria
//adicionado automáticamente
```

logo após ter criado a migration, através do comando php artisan migrate, ele fará a sincronização com o banco de dados e enviará as informações sobre a tabela criada.

### Adicinando novas colunas a uma tabela ja criada utilizando migrations

basta criar uma migration e através do método up(), adicionar os campos que somarão a uma tabela já criada. Como mostrado abaixo, dentro da função de callback do método up(), através do objeto schema que chamará o método table, irformamos os campos a serem adicionados.

 

![Untitled](Models%20e%20Migrations%20f1b55ba6d833485cbd8ec0fead33a2a6/Untitled.png)

após a migration ser criada, faremos a sincronização da migration com o banco de dados digtando:

```php
php artisan migrate
```