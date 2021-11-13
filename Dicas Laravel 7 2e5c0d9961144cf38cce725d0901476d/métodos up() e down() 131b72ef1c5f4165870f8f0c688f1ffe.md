# métodos up() e down()

O método up() é executado todas as vezes que rodamos o comando:

```php
// com esse comando o laravel verifica todas as migrations em ordem temporal e
// da mais antiga para a mais nova, ou seja ele verifica todos os métodos up()
// descartando os métodos down().
php artisan migrate
```

O método down é responsável por reverter tudo que foi executado no método up(), ou seja, tudo que é criado no método dentro do método up() precisa ser desfeito com o método down() para que seja possível realizar o processo de rollback das migrações :

![Untitled](me%CC%81todos%20up()%20e%20down()%20131b72ef1c5f4165870f8f0c688f1ffe/Untitled.png)

```php
//para rodar o método down() de todas as migrations eu digito o comando abaixo

//ele irá eliminar a ultima migration( O ultimo passo) que foi rodada da mais atual para a mais antiga
//ao contrário do que faz o método up().
php artisan migrate:rollback 

//caso eu queira retroceder mais de um passo eu acrescento o n° de passo como mostrado abaixo

php artisan migrate:rollback --steps=2 //aqui estou retrocedendo 2 passos.
```