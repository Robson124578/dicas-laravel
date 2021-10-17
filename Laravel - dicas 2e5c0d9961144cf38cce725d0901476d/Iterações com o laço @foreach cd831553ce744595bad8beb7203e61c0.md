# Iterações com o laço @foreach

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