# Utilizando o laço @forelse no contexto do blade

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)

---

```php
//Controller////////////////////////////////////// 

    public function index(){
        $fornecedor = [
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

//View//////////////////////////////////////        
        
        {{--
Abaixo estamos iterando um array utilizando '@forelse'
que itera com base no índice e valor.

Ele é bem semelhante ao @foreach
A diferença entre ele e o @foreach  é que o  @forelse 
oferece uma opção alternativa caso o array esteja vazio por meio da diretiva
@empty encadeada dentro do @forelse como mostrado abaixo:

 --}}

@isset($fornecedor)
    @forelse($fornecedor as $indice => $valor)
        {{$valor['nome']}}
        {{$valor['cnpj']}}
        {{$valor['ddd']}}
				{{$valor['tel']}}
        <hr>
    @empty
        <h1>nenhum dado disponível.</h1>
    @endforelse
@endisset
```

---

[Dicas Laravel 7](../Dicas%20Laravel%207%202e5c0d9961144cf38cce725d0901476d.md)