# Inserção de conteúdo, comentários ou sintaxe pura do blade ou php.

Como mostrado abaixo para inserirmos comentários:

obs: os comentários não são renderizados no na página html. No caso o blade descarta os comentários.

```php
obs: Todos os exemplos de trecho de código Abaixo 
em teoria são para serem inseridos em arquivos 
blade.php 
========================================== 
A forma abaixo mostra como um texto 
é mostrado utilizando a sintaxe blade para
inserir strings e variáveis

{{'teste de texto usando a sintaxe blade'}}

obs: ela pode ser comparada com a tag de
impressão curta do php <?= '</br>texto utlizando atag de impressão curta do php' ?>

========================================== 
Esta outra forma mostra como podemos inserir um 
comentário utilizando a sintaxe blade:

{{-- 'Comentário utsando a sintaxe blade' --}}

========================================== 
Abaixo estamos vendo como podemos inderir apesar 
de ser pouco usual um bloco de php em arquivos 
blade.php:

@php 
echo "</br>"; 
$nome = "Robson"; 
echo $nome; 
echo "</br>"; 
@endphp

========================================== 
Aqui eu inseri um bloco php e adicionei um 
comentário:

@php 
// comentário com a sintaxe pura do php 
@endphp
```

## Inserção da sintaxe pura do php

embora seja pouco usual ela pode ser usada da seguinte forma:

```php
@php
    //Aqui dentro desse bloco eu consigo inserir códigos php puros

    //comentário de uma linha

    /* comentário
       de multiplas 
        linhas */

        echo "teste";
@endphp
```

## Mostrar o conteúdo de um array vindo do controller

```php
{{-- O comando abaixo mostra o conteúdo de um array pois o blade só consegue mostrar todos os elementos de um arraby através de uma interação--}}

@dd($fornecedores)
```

Como será a saída:

![Screenshot (1).png](Inserc%CC%A7a%CC%83o%20de%20conteu%CC%81do,%20comenta%CC%81rios%20ou%20sintaxe%20p%20c8bf5d7aca844c24b926ae6f673848b8/Screenshot_(1).png)