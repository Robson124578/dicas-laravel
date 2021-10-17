# Utilizando a estrutura de decisão SWITCH

```php
////////////////////////////////////////////////////////////
        //Array localizado no controller
        ////////////////////////////////////////////////////////////
        
        $fornecedores = [
            0 => [
                'nome' => 'fornecedor1',
                'cnpj' => '09398493839',
                'ddd' => '61', //Brasília (DF)
                'tel' => '0000000'
            ],
            1 => [
                'nome' => 'fornecedor2',
                'ddd' => '85', //Fortaleza (CE)
                'tel' => '0000000'
            ],
            3 => [
                'nome' => 'fornecedor2',
                'ddd' => '32', //Juiz de Fora (MG)
                'tel' => '0000000'
            ],
            4 => [
                'nome' => 'fornecedor2',
                'ddd' => '22', //Juiz de Fora (MG)
                'tel' => '0000000'
            ]
        ];
        return view('app.fornecedor.index', compact('fornecedores'));
    }

    ////////////////////////////////////////////////////////////
    //view
    ////////////////////////////////////////////////////////////
        
    <p>nome: {{ $fornecedores[4]['nome'] ?? 'não possui' }}</p> 
    <p> 
    DDD: @switch ($fornecedores[4]['ddd']) 
            @case('61')
            Fornecedor de brasília
            @break 
     
            @case('85') 
            Fornecedor de fortaleza
            @break 
     
            @case('32') 
            Juiz de Fora
            @break 
     
            @default 
            nenhum valor passado
        @endswitch 
    </p>
```