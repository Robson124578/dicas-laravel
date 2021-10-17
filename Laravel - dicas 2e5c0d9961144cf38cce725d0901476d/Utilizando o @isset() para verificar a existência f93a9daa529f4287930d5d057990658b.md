# Utilizando o @isset() para verificar a existência de uma variável

```php
{{-- Abaixo Utilizando o @isset podemos verificar se uma variável ou índice dentro de um array foi definida--}}
{{-- Caso esse exemplo fosse executado fora do isset poderia ocasionar um erro. utilizando o @isset eu posso executar
uma váriável somente se a mesma foi definida. --}}
@isset($variavel)
    echo $variavel
@endisset
```