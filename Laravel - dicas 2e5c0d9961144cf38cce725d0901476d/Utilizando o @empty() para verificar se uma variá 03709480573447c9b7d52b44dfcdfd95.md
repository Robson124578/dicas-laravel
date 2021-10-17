# Utilizando o @empty() para verificar se uma variável esta vazia

```php
{{-- O @empty verifica se uma variável está vazia ou até mesmo um array vazio. abaixo segue o qué considerado como uma variável vazia para o php:
obs: caso a variável esteja vazia essa condição retornará true.
$var = '';
$var = 0;
$var = 0.0;
$var = '0';
$var = null; (nos testes retornou tudo em branco)
$var = false;
$var = array(); (nos testes ocasionou erro)
--}}
@isset($variavel)
    @empty($variavel)
        <h4>A variável está vazia</h4>
    @endempty
        valor: {{ $variavel }}
@endisset
```