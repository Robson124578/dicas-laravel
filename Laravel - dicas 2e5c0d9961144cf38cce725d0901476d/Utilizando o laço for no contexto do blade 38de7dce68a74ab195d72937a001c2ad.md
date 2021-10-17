# Utilizando o laço for no contexto do blade

```php
//////////////////////////////////////
    ///  Controller
    //////////////////////////////////////    

    public function index(){
        $fornecedores = [
            0 => [
                'nome' => 'fornecedor1',
                'cnpj' => '09398493839',
                'ddd' => '61', //Brasília (DF)
                'tel' => '0000000'
            ],
            1 => [
                'nome' => 'fornecedor2',
                'cnpj' => '09398493839',
                'ddd' => '85', //Fortaleza (CE)
                'tel' => '0000000'
            ],
            2 => [
                'nome' => 'fornecedor3',
                'cnpj' => '09398493839',
                'ddd' => '32', //Juiz de Fora (MG)
                'tel' => '0000000'
            ],
            3 => [
                'nome' => 'fornecedor4',
                'cnpj' => '09398493839',
                'ddd' => '22', //Juiz de Fora (MG)
                'tel' => '0000000'

        //////////////////////////////////////
        ////// View
        //////////////////////////////////////        

        @isset($fornecedores) 
            @for($i=0; isset($fornecedores[$i]); $i++)  // Utilizando o @isset assim que o laço cair no contexto em um indice inexistente automaticamente o laço interromperá 
                Nome: {{ $fornecedores[$i]['nome'] }}</br> 
                DDD: {{ $fornecedores[$i]['ddd'] }}</br> 
                <hr> 
            @endfor 
        @endisset
```