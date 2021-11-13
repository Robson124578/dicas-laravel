# Extendendo templates com @extends, @section, @yeld e @include, @component

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)

---

Para utilizar a extensão de templates com blade nos encarregamos primeiramente de criar um template base que agrupará o código comum a todas as páginas estáticas. Sendo assim temos que extender a view até o template base. Para fazer isso usamos a instrução @extends('caminho_do_template') indicando o para o template. O @extends() entende que os templates estarão armazenados a partir do diretório views. Depois de criar a base é só fazer como mostrado abaixo:

em seguida, selecionamos o conteúdo na view que queremos extender para o template base como mostrado baixo:

```php
//view//////////////////////////////////////////////////////////

@extends('site.layouts.basico') //@extends indicando o caminho para o template

//Abaixo o conteúdo está englobado no método @section() que por sua vez receberá um
//nome/apelido para ser inserido no template base
@section('conteudo')
    <div class="topo">

        <div class="logo">
            <img src="{{asset('img/logo.png')}}">
        </div>

        <div class="menu">
            <ul>
                <li><a href="{{ route('site.index') }}">Principal</a></li>
                <li><a href="{{ route('site.sobrenos') }}">Sobre Nós</a></li>
                <li><a href="{{ route('site.contato') }}">Contato</a></li>
            </ul>
        </div>
    </div>
@endsection
```

Agora precisamos declarar o bloco de código englobado no método @section no template base para que ele de fato, seja inserido lá como mostrado abaixo:

```php
//Template basico//////////////////////////////////////////////////////////

<!DOCTYPE html>
<html lang="pt-br">
    <head>
        <title>Super Gestão - Sobre Nós</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="{{asset('css/estilo_basico.css')}}">
    </head>
    <body>
        @yield('conteudo') //declarando onde o conteudo da @section será inserido
    </body>
</html>
```

dessa forma consigo economizar muito mais código e deixar o template mais enxuto.

## Enviando parâmetro e variáveis para o template

Podemos enviar parâmetros da view ou variáveis vindas do controller para nossas views  para o template extendido através do método @section('nome-da-section', 'parâmetro'/$variavel)  como mostrado abaixo:

```php
@extends('site.layouts.basico')

//como mostrado aqui, estou enviando uma string como segundo parâmetro
//no método @section()
//Obs: caso eu queira enviar uma variável vinda do controller é só inseri-la
//desta forma => @section('titulo', $variavel)
@section('titulo', 'Home')

@section('conteudo')
    <div class="topo">

        <div class="logo">
            <img alt="logo" src="{{asset('img/logo.png')}}">
        </div>

        <div class="menu">
            <ul>
                <li><a href="{{ route('site.index') }}">Principal</a></li>
                <li><a href="{{ route('site.sobrenos') }}">Sobre Nós</a></li>
                <li><a href="{{ route('site.contato') }}">Contato</a></li>
            </ul>
        </div>
    </div>
```

## Utilizando o @include

Com o @include temos a fexibilidade de inserir trechos de código de uma view em outra view. no caso o @include também é procurado a partir do diretório views. segue um exemplo abaixo de uma inclusão de um trecho de uma view criado separadamente e inserido em outra view.

```php
<!DOCTYPE html>
<html lang="pt-br">
    <head>
        <title>Super Gestão - @yield('titulo')</title>
        <meta charset="utf-8">
        <link rel="stylesheet" href="{{asset('css/estilo_basico.css')}}">
    </head>
    <body>
				//aqui remete a uma parte do código comun em todas as páginas (no caso, o menu)
		    @include('site.layouts._partials.topo')
        @yield('conteudo')
    </body>
</html>
```

## Utilizando o @component

Semelhante ao @include, o @component é usado para a inclusão de uma view ou um trecho de código dentro de outra view. No caso o laravel procurará o trecho de código que será incluido no @component a partir da pasta views dentro de resources. segue o exemplo de um código abaixo:

```php
<div class="informacao-pagina">
    <div class="contato-principal">
				//aqui estou inserindo um @component
        @component('site.layouts._components.form_contato')                    
        @endcomponent
    </div>
</div>
```

É possível enviar parâmetros das views para os componentes e existem 2 maneiras. 

1°) inserindo o conteúdo ou variável entre a as tags de abertura e fechamento do @component. automaticamente as informações contidas entre as tags @component e @endcomponent serão

armazenadas dentro de uma variável chamada $slot para ser utilizadas no @component que foi

criado.

exemplo:

```php
// View onde o @component está sendo usado

<div class="direita">
    <div class="contato">
         <h1>Contato</h1>
         <p>Caso tenha qualquer dúvida por favor entre em contato com nossa equipe pelo formulário abaixo.<p>
         //@component
				 @component('site.layouts._components.form_contato')
             //As informações inseridas aqui irão para a variável $slot
							<p style="text-align: center">Em breve retornaremos o contato!</p>            
         @endcomponent
    </div>
</div>

// Componente

<form>
		// as informações ficarão armazenadas nessa variável( $slot )
    {{ $slot }}
    <input type="text" placeholder="Nome" class="borda-branca"
    <br>
    <button type="submit" class="borda-branca">ENVIAR</button>
</form>

```

2°) A segunda forma de passagem de parâmetros é utilizando como segundo parâmetro no na tag

@component('path.component', $variável) a variável que com o valor desejado.

```php
<div class="direita">
    <div class="contato">
        <h1>Contato</h1>
           <p>Caso tenha qualquer dúvida por favor entre em contato com nossa equipe pelo formulário abaixo.<p>
            // aqui estou enviando um array assossiativo com uma variável que vai alterar
/           // a classe CSS dos inputs do formulário   
					 @component('site.layouts._components.form_contato', ['classe'=>'borda-branca'])
              <p style="text-align: center">Em breve retornaremos o contato!</p>            
           @endcomponent
       </div>
   </div>
```

---

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)