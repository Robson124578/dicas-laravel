# Utilizando o @isset() para verificar a existência de uma variável

[Dicas Laravel](../Dicas%20Laravel%202e5c0d9961144cf38cce725d0901476d.md)

---

```php
{{-- Abaixo Utilizando o @isset podemos verificar se uma variável ou índice dentro de um array foi definida--}}
{{-- Caso esse exemplo fosse executado fora do isset poderia ocasionar um erro. utilizando o @isset eu posso executar
uma váriável somente se a mesma foi definida. --}}
@isset($variavel)
    echo $variavel
@endisset
```