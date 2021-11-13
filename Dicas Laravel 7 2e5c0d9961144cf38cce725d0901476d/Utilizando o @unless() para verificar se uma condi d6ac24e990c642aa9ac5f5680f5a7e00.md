# Utilizando o @unless() para verificar se uma condição é falsa

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)

---

```php
{{--Abaixo um exemplo de como funciona o comando unless--}}
{{--Obs: enquanto o if testa se uma condição é verdadeiro, o unless verifica se a condição é falsa como mostrado abaixo--}}
{{-- Esse resultado será exibido pois o unless esta negando a condição --}}
{{-- $frutas = ['banana', 'uva'] --}}
{{-- @unless(count($frutas) > 3)
    <h3>Você possui menos de 3 frutas<h3>
@endunless --}}

{{-- Abaixo segue o exemplo utilizanbdo um exemplo mais complexo utilizando um array multidimensional --}}

<h1>Fornecedores</h1> 
       $fornecedores = [ 
            0 => [ 
                'nome' => 'fornecedor1', 
                'cnpj' => '09398493839' 
            ], 
            1 => [ 
                'nome' => 'fornecedor2' 
            ] 
        ]; 
<p>fornecedor: {{$fornecedores[0]['nome']}}</p> 
@unless(isset())
@endunless
</p>
```