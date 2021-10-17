# Comando @if/@else

A estrutura de decisão @if / @else está tratando um array chamado fornecedores vindo do

controller.

```php
{{-- Utilizando a sintaxe blade --}}

@if(count($fornecedores) > 0 && count($fornecedores) < 10)
    <h3>A quantidade de Fornecedores cadastrados esta entre 1 e 10</h3>
@elseif(count($fornecedores) <= 0)
    <h3>Não existe nenhum fornecedor cadastrado.</h3>
@else
    <h3>Existem mais de 10 fornecedores cadastrados.</h3>
@endif

====================================================================================

{{-- se fosse utilizada a sintaxe php pura seria assim--}}

@php 
if(condição){
    ação 
} else if(condição){
    ação 
} else{ 
    ação 
} 
@endphp
```