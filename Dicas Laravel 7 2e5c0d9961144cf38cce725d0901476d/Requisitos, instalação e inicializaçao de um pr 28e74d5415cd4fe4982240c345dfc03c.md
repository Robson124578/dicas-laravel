# Requisitos, instalação e inicializaçao de um projeto Laravel

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)

### Requisitos

- PHP instalado no sistema e criar uma variável global.
- instalar o composer e tê-lo como variável global.

Obs: Existem duas formas de se iniciar um projeto laravel:

- Utilizando o laravel installer
- Utilizando o composer

### Iniciando um projeto Laravel via composer

Abaixo vamos configurar o composer para utilizar o repositório do site [https://packagist.org](https://packagist.org/) com o o seguinte comando:

```php
composer config  -g repo.packagist composer https://packagist.org
```

Abaixo vou configurar a utilização dos protocolos https e ssh para recuperar os pacotes do github:

```php
composer config -g github-protocols https ssh
```

Obs: lembrando que as ultimas configurações acima são feitas somente uma  vez. são configurações globais do composer para trazer os pacotes para o ambiente de desenvolvimento.

Abaixo vamos de fato criar o projeto:

```php
composer create-project --prefer-dist laravel/laravel projeto_laravel_via_composer "7.0"
```

Para iniciar o servidor entre na pasta do projeto e depois na pasta public pelo cmd e digite:

```php
php -S localhost:8000
```

### Iniciando um projeto Laravel via Laravel installer

Para iniciar um projeto laravel através do laravel installer digite o comando:

```php
composer global require laravel/installer
```

É importante verificar se existe a variável de ambiente indicando para o seguinte caminho:

```php
C:\Users\robson\AppData\Roaming\Composer\vendor\bin
```

Depois de verificadas as etapas anteriores, para iniciar um projeto via laravel installer é só digitar:

```php
laravel new  nome_d-_projeto
```

obs: pode ser que no termino da instalação apareça uma mensagem na linha de comando pedindo para habilitar o extensão fileinfo que está localizado no na pasta de instalação do php no arquivo php.ini. sendo assim basta descomentar a extensão fileinfo e reinstalar o projeto via laravel installer.

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)