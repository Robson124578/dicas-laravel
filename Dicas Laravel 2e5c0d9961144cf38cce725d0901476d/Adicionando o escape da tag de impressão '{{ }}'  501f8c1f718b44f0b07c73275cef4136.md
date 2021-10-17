# Adicionando o escape da tag de impressão '{{ }}' do blade

[Dicas Laravel](../Dicas%20Laravel%202e5c0d9961144cf38cce725d0901476d.md)

---

---

```php
//Controller//////////////////////////////////////////////////////////////
class FornecedorController extends Controller
{
    public function index(){

        $fornecedor = [
            [
                'nome' => 'Robson',
                'idade' => 16,
                'ddd'=> '61'
            ],
            [
                'nome' => 'Juca',
                'idade'=> 12,
                'ddd'=> '62'
            ],
            [
                'nome' => 'Paula',
                'idade'=> 23,
                'ddd'=> '21'
            ]
        ];

  
        return view('app.fornecedor.index', compact('fornecedor')); 
    

    }

}

{{--
Para escapar valores digitados e caracteres nos quais não queremos
que o blade interprete, basta adicionar '@' na frente da tag de
impressão '{{ }}' como mostrado abaixo:
 --}}

//view//////////////////////////////////////////////////////////////
@isset($fornecedor)
    @for($i = 0; isset($fornecedor[$i]); $i++)
        Nome: @{{ $fornecedor[$i]['nome'] }}<br>
        Idade: @{{ $fornecedor[$i]['idade'] }}<br>
        Código de área: @{{ $fornecedor[$i]['ddd'] }}<br>
        <hr>
    @endfor
@endisset
```

[Dicas Laravel](../Dicas%20Laravel%202e5c0d9961144cf38cce725d0901476d.md)