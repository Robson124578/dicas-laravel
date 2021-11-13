# Migration - comandos (status, reset, refresh e fresh)

## Comando status

```php
//O comando listará todas as migrations contidas no projeto

php artisan migrate:status

// a coluna Ran indica se a migration já foi rodada ou não
```

saída:

![Untitled](Migration%20-%20comandos%20(status,%20reset,%20refresh%20e%20fre%20fd99476f48424af2a0a880e08f429942/Untitled.png)

## Comando Reset

```php
//O comando abaixo fará um reset em todas as migrations fazendo um rollback de todas
//tabelas criadas no banco de dados

php artisan migrate:reset
```

saída:

![Untitled](Migration%20-%20comandos%20(status,%20reset,%20refresh%20e%20fre%20fd99476f48424af2a0a880e08f429942/Untitled%201.png)

## Comando Refresh

```php
//O comando abaixo fará o rollback de todas as migrations executadas e na sequência
// executará novamente as migrations redriando os objetos no banco de dados, porém caso
//existam dados armazenados, os mesmos serão apagados e as tabelas serão recriadas sem
//nenhum dado salvo. Esse comando é útil quando queremos zerar um banco de dados.

php artisan migrate:refresh

//como mostrado abaixo, é executado todos os rollbacks e na sequencia as migrations
//são executadas recriando os objetos no banco de dados.
```

![Untitled](Migration%20-%20comandos%20(status,%20reset,%20refresh%20e%20fre%20fd99476f48424af2a0a880e08f429942/Untitled%202.png)

## Comando Fresh

```php
//O comando fresh faz um drop em todos os objetos do banco de dados e depois
// recria os mesmos

php artisan migrate:fresh
```

![Untitled](Migration%20-%20comandos%20(status,%20reset,%20refresh%20e%20fre%20fd99476f48424af2a0a880e08f429942/Untitled%203.png)