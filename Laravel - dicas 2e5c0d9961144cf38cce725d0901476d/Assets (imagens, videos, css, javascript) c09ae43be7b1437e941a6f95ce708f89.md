# Assets (imagens, videos, css, javascript)

Asset trazendo para o português pode ser entendido como ativo mas não

é um ativo de ativo ou inativo e sim um ativo relacionado a bens de propriedade, ou seja, é um termo que vem da economia.  Quando esse termo e conceito é aplicado ao desenvolvimento front end ele representa tudo aquilo que é utilizado para complementar o conteúdo do front das aplicações web, ou seja, as mídias tais como imagens sons vídeos fontes e até mesmo estilos CSS e JavaScript.

Enfim tudo aquilo que vai anexo a uma página HTML é um assunto que complementa a Markup language (html).

## helper asset

Para incluir assets em nas páginas html é uma boa prática utilização do 'helper asset'  do laravel. Por padrão os arquivo assets são armazenados no diretório public da aplicação laravel. sendo assim

o helper asset vai automaticamente procurará a partir do diretório public.

Segue o exemplo abaixo:

```php
//view//////////////////////////////////////////////////////////

{{--Método convêncional de adicionar uma imagem em um arquivo HTML--}}

<img src="img/logo.png">

{{--Agora, utilizando o helper asset--}}

	<img src="{{ asset('img/logo.png') }}">
```

Obs: Pode ser que ao inserir arquivos css, imagens e vídeos não carreguem ao atualizar o navegador. Casso isso ocorra pode ser necessário efetuar o comando para limpar o cache das views. Você pode executar essa ação com o seguinte comando abaixo:

```php
php artisan view:clear
```

## Adicionando arquivos css externamente:

Por ser considerado um asset, os arquivos css devem ser armazenados dentro da pasta public da aplicação Laravel, sendo assim é só criar um diretório chamado css e incluir os arquivos de estilo.