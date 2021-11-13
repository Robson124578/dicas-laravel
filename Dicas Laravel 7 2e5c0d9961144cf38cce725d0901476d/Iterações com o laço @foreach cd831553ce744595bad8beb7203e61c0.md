# Iterações com o laço @foreach

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)

---

```php
{{-- 
Abaixo estamos iterando um array utilizando {{--'@foreach'--}}
que itera com base no índice e valor.
 --}}
=====================================================================================
Controller:

class FornecedorController extends Controller
{
    public function index(){

        $fornecedor = [
            [
                'nome' => 'Robson',
                'status' => 'N',
                'ddd'=> '61'
            ],
            [
                'nome' => 'Juca',
                'status'=> 'N',
                'ddd'=> '62'
            ],
            [
                'nome' => 'Paula',
                'status'=> 'N',
                'ddd'=> '21'
            ]
        ];
  
        return view('app.fornecedor.index', compact('fornecedor')); 
    

    }

}

=================================================================================
view:

@isset($fornecedor)
    @foreach($fornecedor as $indice => $valor)
        {{$valor['nome']}}
        {{$valor['status']}}
        {{$valor['ddd']}}
        <hr>
    @endforeach
@endisset
```

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)

---