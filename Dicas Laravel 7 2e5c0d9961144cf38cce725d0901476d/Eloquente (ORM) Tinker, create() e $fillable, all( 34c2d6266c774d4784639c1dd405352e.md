# Eloquente (ORM) Tinker, create() e $fillable, all(), find(), where(), whereIn() e whereNotIn() e etç...

## Sumário

- [Tinker]()
- [Resolvendo Problemas de compatibilidade com o model]()
- [Adicionando dados com create() e $fillable]()
- [all()]()

---

Eloquente é o ORM nativo do framework Laravel. o Object Mapping Relational

é uma técnica que aproxima o paradigma de apliacações orientadas a objeto ao

banco de dados. Os frameworks ou bibliotecas ORM definem como os dados serão 

mapeados entre os dois  ambientes. através de desse mapeamento o ORM fornecerá

 recursos de adição, remoção, atualização e seleção de registros ou dados assim

otimizando o tempo de desenvolvimento.

O ORM é um método independente de linguagem de programação e hoje se destacam

dois padrões no mercado e são:

- Data Mapper
- Active Record

O ORM do Laravel (Eloquente) utiliza o padrão Active Record.

Obs: pesquisar na internet sobre esses dois padrões de ORM.

## Tinker

O tinker é uma interface de linha de comando que possibilita o acesso as classes do projeto.

```php
//Através do comando abaixo é possível acessar o tinker

php artisan tinker
```

com o Tinker podemos inserir dados no banco de dados de nossa aplicação via interface de comando. Basta instanciar o namesapace e  a classe em um objeto e preencher os atributos

de acordo com os nomes das colunas no banco de dados como mostrado na figura abaixo:

```php
PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman

// instânciando o objeto indicando o namespace e a classe para 
//inserir os atributos necessários:
>>> $f = new \App\Fornecedor(); 
=> App\Fornecedor {#3401}

//Abaixo estou inserindo os atributos um a um:
>>> $f->nome='xyz';
=> "xyz"
>>> $f->site='www.xyz.com.br';
=> "www.xyz.com.br"
>>> $f->uf='DF';
=> "DF"
>>> $f->email='xyz@gmail.com';
=> "xyz@gmail.com"

// aqui estou verificando os atributos que criei
>>> print_r($f->getAttributes()); 
Array
(
    [nome] => xyz
    [site] => www.xyz.com.br
    [uf] => DF
    [email] => xyz@gmail.com
)
=> true
>>> $f->save();  //salvando no banco de daodos
=> true
```

Há outra maneira também de inserir registros através da interface de comando do Tinker utilizando o método estático create() herdado da classe model como mostrado abaixo:

## Problemas de compatibilidade entre o nome do model e a tabela no banco de dados

Quando criamos um model é importante termos em mente que devemos utilizar o padrão CamelCase para que o eloquente possa entender qual tabela inserir os dados nas tabelas que estão com o nome no plural. Para chegar ao nome das tabelas, o eloquente segue os seguintes passos:

Pega o nome da classe que deve estar em CamelCase e separa o nome levando em consideração

o inicio de cada letra maiúscula como mostrado abaixo, acrescenta um underline e por fim acrescenta um 's' no final ficando assim:

ficará assim: site_contatos

Obs: o eloquente enviará os dados para uma tabela com este nome no banco de dados

```php
exemplo de classe:

class SiteContato extends Model

{

}

//O eloquente tentará adicionar os dados na tabela: site_contatos
```

Porém, no português, nem sempre o plural terminará com s, por exemplo se existisse uma classe com o nome Fornecedor, nesse caso o eloquente procuraria uma tabela no banco de dados com o nome 'fornecedors', o que não estaria correto já que criariamos uma tabela com o nome: fornecedores. 

para corrigir este erro, dentro do model Fornecedor que extende a classe Model, usariamos o atributo protected $table recebendo o nome da classe e assim sobrescrevendo a busca automática do eloquente como mostrado abaixo:

```php
class Fornecedor extends Model

{

// 

protected $table = 'fornecedores';

}
```

## Adicionando dados com create() e $fillable

Uma maneira mais enxuta de preencher os atributos com os valores que irão para o banco de dados é utilizando o método 'create()' como mostrado abaixo:

```php
<?php
//Model Fornecedor

namespace App;

use Illuminate\Database\Eloquent\Model;

class Fornecedor extends Model
{
    //

//Antes de inserir os dados com o metodo estático da class Model
// no tinker eu preciso criar um atributo definido como protected
//chamado fillable que vai receber um array onde conterá os campos
// relacionados as colunas que vou inserir os registros no banco de
//dados.
    protected $fillable = ['nome', 'site', 'uf', 'email'];
}

//CLI do tinker

Windows PowerShell
Copyright (C) Microsoft Corporation. Todos os direitos reservados.

PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman
>>> \App\Fornecedor::create(['nome'=>'multimarcas', 'sites'=>'multimarcas.com.br', 'uf'=>'RJ', 'email'=>'multimarca@email.com']);
=> App\Fornecedor {#3406
     nome: "multimarcas",
     uf: "RJ",
     email: "multimarca@email.com",
     updated_at: "2021-11-02 02:11:15",
     created_at: "2021-11-02 02:11:15",
     id: 4,
   }
>>>
```

## All()

O método all() retorna todos os registros de uma tabela como uma coleção:

```php
PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman
>>> use \App\Fornecedor
>>> ;
>>> $fornecedores = Fornecedor::all();
=> Illuminate\Database\Eloquent\Collection {#3412
     all: [
       App\Fornecedor {#3413
         id: 1,
         nome: "xyz",
         site: "www.xyz.com.br",
         created_at: "2021-11-01 14:07:47",
         updated_at: "2021-11-01 14:07:47",
         uf: "DF",
         email: "xyz@gmail.com",
       },
       App\Fornecedor {#3414
         id: 2,
         nome: "loja",
         site: "loja.com.br",
         created_at: "2021-11-01 17:46:03",
         updated_at: "2021-11-01 17:46:03",
         uf: "MG",
         email: "loja@email.com",
       },
       App\Fornecedor {#3415
         id: 3,
         nome: "tinturaria",
         site: "tinturaria.com.br",
         created_at: "2021-11-01 18:03:41",
         updated_at: "2021-11-01 18:03:41",
         uf: "DF",
         email: "tinturaria@email.com",
       },
       App\Fornecedor {#3416
         id: 4,
         nome: "multimarcas",
         site: null,
         created_at: "2021-11-02 02:11:15",
         updated_at: "2021-11-02 02:11:15",
         uf: "RJ",
         email: "multimarca@email.com",
       },
     ],
   }
>>>
```

## find()

Com o método find(), eu posso recuperar registros de uma tabela passando como parâmetro o id ou se for mais de um registro eu posso usar no parâmetro um array com os id que quero retorno

como mostrado abaixo:

```php
Windows PowerShell
Copyright (C) Microsoft Corporation. Todos os direitos reservados.

PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman
>>> use \App\Fornecedor;

//Aqui estou recuperando um registro passando como
//parâmetro o id que desejo retorno.

>>> $fornecedor = Fornecedor::find(1);
=> App\Fornecedor {#3409
     id: 1,
     nome: "xyz",
     site: "www.xyz.com.br",
     created_at: "2021-11-01 14:07:47",
     updated_at: "2021-11-01 14:07:47",
     uf: "DF",
     email: "xyz@gmail.com",
   }
>>>
>>>
>>>

//Aqui estou recuperando os registros com base em um
//array de números referentes aos id's desejados

>>> $fornecedor2 = Fornecedor::find([1,2,3]);
=> Illuminate\Database\Eloquent\Collection {#3397
     all: [
       App\Fornecedor {#3399
         id: 1,
         nome: "xyz",
         site: "www.xyz.com.br",
         created_at: "2021-11-01 14:07:47",
         updated_at: "2021-11-01 14:07:47",
         uf: "DF",
         email: "xyz@gmail.com",
       },
       App\Fornecedor {#3418
         id: 2,
         nome: "loja",
         site: "loja.com.br",
         created_at: "2021-11-01 17:46:03",
         updated_at: "2021-11-01 17:46:03",
         uf: "MG",
         email: "loja@email.com",
       },
       App\Fornecedor {#3400
         id: 3,
         nome: "tinturaria",
         site: "tinturaria.com.br",
         created_at: "2021-11-01 18:03:41",
         updated_at: "2021-11-01 18:03:41",
         uf: "DF",
         email: "tinturaria@email.com",
       },
     ],
   }
```

## where()

Com o método where('nome_da_coluna', 'operador_lógico', 'parâmetro') podemos recuperar registros no banco de dados utilizando os operadores lógicos de comparação para filtra determinadas consultas como mostrado abaixo:

```php
>>> use \App\SiteContato;

// fazendo o Builder para conseguir efetuar a consulta com o método get()
>>> $contatos = SiteContato::where('id','=',1);
=> Illuminate\Database\Eloquent\Builder {#3420}

// com o builder já montado, utilizando o método get()
// podemos efetuar a consulta no banco com base nos parâmetros
//inseridos pelo método where()
>>> $contatos = SiteContato::where('id','=',1)->get(); 
=> Illuminate\Database\Eloquent\Collection {#4131
     all: [
       App\SiteContato {#4288
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
     ],
   }
```

## whereIn e whereNotIn()

O whereIn() verifica os parâmetro por igualdade ⇒ whereIn('coluna', 'parâmetros');

O whereNotIn() verifica os parâmetro por diferença ⇒ whereNotIn('coluna', 'parâmetros');

exemplo:

Tabela do banco de dados onde vou recuperar os registros

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

```php
//tinker

//usando o whereIn()
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman
>>> $dados = new \App\SiteContato();
=> App\SiteContato {#3401}
>>> $dados::whereIn('mensagem', ['Hello'])->get();
=> Illuminate\Database\Eloquent\Collection {#4191
     all: [
       App\SiteContato {#4123
         id: 5,
         created_at: "2021-11-02 13:56:56",
         updated_at: "2021-11-02 13:56:56",
         nome: "zezinho",
         telefone: "(61)947663355",
         email: "zezin@email.com",
         motivo_contato: 1,
         mensagem: "Hello",
       },
     ],
   }

//Usando o whereNotIn()

>>> $dados::whereNotIn('motivo_contato', [1,2])->get();
=> Illuminate\Database\Eloquent\Collection {#4280
     all: [
       App\SiteContato {#3402
         id: 7,
         created_at: null,
         updated_at: null,
         nome: "João",
         telefone: "(88) 91111-2222",
         email: "joao@contato.com.br",
         motivo_contato: 3,
         mensagem: "É muito difícil localizar a opção de listar todos os produtos",
       },
       App\SiteContato {#4190
         id: 11,
         created_at: null,
         updated_at: null,
         nome: "Ana",
         telefone: "(33) 96666-7777",
         email: "ana@contato.com.br",
         motivo_contato: 3,
         mensagem: "Não gostei muito das cores, consigo mudar de tema?",
       },
     ],
   }

```

## whereBetween() e whereNotBetween

whereBetween() retorna os dados baseados em um intervalo:

```php
 whereBetween('coluna', ['inicio_do_intervalo', 'fim_do_intervalo'])→get();
```

whereNotBetween() retorna os dados que não estiverem no intervalo de tempo definido

```php
whereNotBetween('coluna', ['inicio_do_intervalo','fim_do_intervalo'])→get();
```

Ambos podem ser utilizados com dados do tipo int e datas:

Tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

```php
// utilizando o whereBetween()

//Aqui ele vai me retornar todos os dados que estão entre 1 e 5

>>> $dados::whereBetween('id', [1,5])->get();
=> Illuminate\Database\Eloquent\Collection {#3408
     all: [
       App\SiteContato {#3403
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
       App\SiteContato {#4337
         id: 2,
         created_at: "2021-11-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "Paula",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       App\SiteContato {#4339
         id: 3,
         created_at: "2021-11-01 03:44:49",
         updated_at: "2021-11-01 03:44:49",
         nome: "Isaac Robson",
         telefone: "(61)982252824",
         email: "zachboy@gmail.com",
         motivo_contato: 1,
         mensagem: "Olá, tem Roblox ai ?",
       },
       App\SiteContato {#4340
         id: 4,
         created_at: "2021-11-01 13:46:02",
         updated_at: "2021-11-01 13:46:02",
         nome: "Maria Clara",
         telefone: "(61)90636987649",
         email: "mariaClara@gmail.com",
         motivo_contato: 1,
         mensagem: "Hello World",
       },
       App\SiteContato {#4341
         id: 5,
         created_at: "2021-11-02 13:56:56",
         updated_at: "2021-11-02 13:56:56",
         nome: "zezinho",
         telefone: "(61)947663355",
         email: "zezin@email.com",
         motivo_contato: 1,
         mensagem: "Hello",
       },
     ],
   }

//Utilizando o whereNotBetween()

// aqui ele vai me retornar todos os dados que não estão entre 3 e 10

>>> $dados::whereNotBetween('id', [3,10])->get();
=> Illuminate\Database\Eloquent\Collection {#4124
     all: [
       App\SiteContato {#4125
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
       App\SiteContato {#4123
         id: 2,
         created_at: "2021-11-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "Paula",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       App\SiteContato {#4086
         id: 11,
         created_at: null,
         updated_at: null,
         nome: "Ana",
         telefone: "(33) 96666-7777",
         email: "ana@contato.com.br",
         motivo_contato: 3,
         mensagem: "Não gostei muito das cores, consigo mudar de tema?",
       },
       App\SiteContato {#4343
         id: 12,
         created_at: null,
         updated_at: null,
         nome: "Helena",
         telefone: "(11) 97777-8888",
         email: "helena@contato.com.br",
         motivo_contato: 2,
         mensagem: "Consigo controlar toda a minha empresa de modo fácil e prático.",
       },
     ],
   }
>>>
```

## Utilizando dois ou mais where's nas consultas como o operador 'and'

Para utilizar mais de uma comparação em uma consulta no banco de dados, podemos utilizar o operador 'and' que exige que ambas as condições sejam verdadeiras. Para fazer isso através do eloquente podemos encadear os where's, como mostrado abaixo:

Tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

Tinker:

```php
//tinker

//aqui estou encadeando comparações com base no operador 'and'

>>> $data::whereIn('motivo_contato',[1])->whereBetween('id',[1,5])->where('created_at','<','2021-11-01 03:45')->get();
=> Illuminate\Database\Eloquent\Collection {#4349
     all: [
       App\SiteContato {#4347
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
       App\SiteContato {#4337
         id: 3,
         created_at: "2021-11-01 03:44:49",
         updated_at: "2021-11-01 03:44:49",
         nome: "Isaac Robson",
         telefone: "(61)982252824",
         email: "zachboy@gmail.com",
         motivo_contato: 1,
         mensagem: "Olá, tem Roblox ai ?",
       },
     ],
   }
```

## orWhere()

tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

Diferente do operador 'and', o operador 'or' verifica se pelo menos uma das condições é verdadeira.

```php
//tinker

//obs: o operador 'or' pode ser encadeado com qualquer um dos métodos estáticos where's

>>> $data::whereIn('nome', ['robson'])->orWhere('email','LIKE','%gmail%')->get();
=> Illuminate\Database\Eloquent\Collection {#4345
     all: [
       App\SiteContato {#3397
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
       App\SiteContato {#4192
         id: 2,
         created_at: "2021-11-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "Paula",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       App\SiteContato {#4351
         id: 3,
         created_at: "2021-11-01 03:44:49",
         updated_at: "2021-11-01 03:44:49",
         nome: "Isaac Robson",
         telefone: "(61)982252824",
         email: "zachboy@gmail.com",
         motivo_contato: 1,
         mensagem: "Olá, tem Roblox ai ?",
       },
       App\SiteContato {#4337
         id: 4,
         created_at: "2021-11-01 13:46:02",
         updated_at: "2021-11-01 13:46:02",
         nome: "Maria Clara",
         telefone: "(61)90636987649",
         email: "mariaClara@gmail.com",
         motivo_contato: 1,
         mensagem: "Hello World",
       },
     ],
   }
```

## whereNull() e whereNotNull()

Tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

```php
//Para recuperar registros do banco de dados que sejam nulos podemos utilizar o whereNull('noma_da_coluna')
//indicando o nome da coluna.

>>> $contatos::whereNull('created_at')->get();
=> Illuminate\Database\Eloquent\Collection {#4087
     all: [
       App\SiteContato {#4334
         id: 7,
         created_at: null,
         updated_at: null,
         nome: "João",
         telefone: "(88) 91111-2222",
         email: "joao@contato.com.br",
         motivo_contato: 3,
         mensagem: "É muito difícil localizar a opção de listar todos os produtos",
       },
       App\SiteContato {#4335
         id: 8,
         created_at: null,
         updated_at: null,
         nome: "Rosa",
         telefone: "(33) 92222-3333",
         email: "rosa@contato.com.br",
         motivo_contato: 1,
         mensagem: "Quando custa essa aplicação?",
       },
       App\SiteContato {#4336
         id: 9,
         created_at: null,
         updated_at: null,
         nome: "Fernando",
         telefone: "(11) 94444-5555",
         email: "fernando@contato.com.br",
         motivo_contato: 1,
         mensagem: "Como consigo criar multiplos usuários para minha empresa?",
       },
       App\SiteContato {#4337
         id: 10,
         created_at: null,
         updated_at: null,
         nome: "André",
         telefone: "(88) 95555-6666",
         email: "andre@contato.com.br",
         motivo_contato: 2,
         mensagem: "Parabéns pela ferramenta, estou obtendo ótimos resultados!",
       },
       App\SiteContato {#4338
         id: 11,
         created_at: null,
         updated_at: null,
         nome: "Ana",
         telefone: "(33) 96666-7777",
         email: "ana@contato.com.br",
         motivo_contato: 3,
         mensagem: "Não gostei muito das cores, consigo mudar de tema?",
       },
       App\SiteContato {#4339
         id: 12,
         created_at: null,
         updated_at: null,
         nome: "Helena",
         telefone: "(11) 97777-8888",
         email: "helena@contato.com.br",
         motivo_contato: 2,
         mensagem: "Consigo controlar toda a minha empresa de modo fácil e prático.",
       },
     ],
   }

//Para recuperar registros do banco de dados que não sejam nulos podemos utilizar o whereNotNull('noma_da_coluna')
//indicando o nome da coluna.

>>> $contatos::whereNotNull('created_at')->get();
=> Illuminate\Database\Eloquent\Collection {#4341
     all: [
       App\SiteContato {#4342
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
       App\SiteContato {#4343
         id: 2,
         created_at: "2021-11-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "Paula",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       App\SiteContato {#4344
         id: 3,
         created_at: "2021-11-01 03:44:49",
         updated_at: "2021-11-01 03:44:49",
         nome: "Isaac Robson",
         telefone: "(61)982252824",
         email: "zachboy@gmail.com",
         motivo_contato: 1,
         mensagem: "Olá, tem Roblox ai ?",
       },
       App\SiteContato {#4345
         id: 4,
         created_at: "2021-11-01 13:46:02",
         updated_at: "2021-11-01 13:46:02",
         nome: "Maria Clara",
         telefone: "(61)90636987649",
         email: "mariaClara@gmail.com",
         motivo_contato: 1,
         mensagem: "Hello World",
       },
       App\SiteContato {#4346
         id: 5,
         created_at: "2021-11-02 13:56:56",
         updated_at: "2021-11-02 13:56:56",
         nome: "zezinho",
         telefone: "(61)947663355",
         email: "zezin@email.com",
         motivo_contato: 1,
         mensagem: "Hello",
       },
       App\SiteContato {#4347
         id: 6,
         created_at: "2021-11-02 14:10:50",
         updated_at: "2021-11-02 14:10:50",
         nome: "paulo",
         telefone: "(61)98887766",
         email: "paulo@email.com",
         motivo_contato: 1,
         mensagem: "tudo certo !",
       },
     ],
   }
```

## consultas com base em datas -

Assim como os outros where's, esses baseados em data e tempo podem ser concatenados com outros where's.

- whereDate('coluna', 'ano-mes-dia');
- whereDay('coluna', 'dia');
- whereMonth('coluna', 'mes');
- whereYear('coluna', 'ano');
- whereTime('coluna', 'operador_de_comparacao', 'hora');     ⇒ este precisa de 3 parâmetros

Tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

```php
//tinker

use \App\SiteContato;
>>> $dado = new SiteContato();
=> App\SiteContato {#3401}

// abaixo estou retornando os dados com base na data

>>> $dado::whereDate('created_at', '2021-11-01')->get();

//aqui com base no dia

$dado::whereDay('created_at', '02')->get();

// com base no ano

$dado::whereYear('created_at', '2021')->get();

//com base na hora

$dado::whereTime('created_at', '<', '03:45')->get();

```

## whereColumn()

Esse método compara valores entre 2 colunas.

Obs: ele não compara colunas com valores nulos.

```php
//Aqui o retorno será somente das linhas onde as duas colunas em comparação tem o mesmo valor
$dado::whereColumn('created_at','updated_at')->get();

// aqui o retorno será somente das onde o valor das 2 colunas em comparação são diferentes
$result = $dado::whereColumn('created_at','!=', 'updated_at')->get(); para

//obs: assim como os outros where's, este aceita encadeamentos
```

## Ordenação em uma consulta de registros

Para ordenação de registros em uma consulta podemos utiliza o orderBy() passando dois parâmetros que são:

orderBy('nome_coluna', 'tipo_de_ordenção').

A ordenação pode ser ascendente ou descendente.

tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

exemplo:

```php
//por padrão caso se omita o segundo parâmetro, ele vai 
//entender que será uma ordenação no padrão ascendente.
//funcionaria assim também: $objeto::orderBy('nome')->get();
$objeto::orderBy('nome', 'asc')->get();

//Abaixo estou ordenando de forma descendente.
$objeto::orderBy('id', 'desc')->get();
```

## Atualização de registros (  fill() e save()   ou ::where  e update()  )

```php
//Para atualizar um registro armazenado no banco de dados eu posso fazer a busca do mesmo através de algum
//método estático que o eloquente disponibiliza:

// Aqui a variável $result está recebendo o resultado da busca no banco de dados
$result =  $fornecedor::whereIn('nome', ['robson'])->get(); 
=> Illuminate\Database\Eloquent\Collection {#4123
     all: [
       App\SiteContato {#4191
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-04 03:39:13",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
     ],
   }
//======================================================================================
//Agora vou renomear os atributos e em seguida através do método save(), posso salvar
//as alterações como mostrado abaixo:

>>> $result->nome = 'Robim'; 
=> "Robim"
>>> $result;
=> App\SiteContato {#3398
     id: 1,
     created_at: "2021-11-01 03:34:34",
     updated_at: "2021-11-04 03:39:13",
     nome: "Robim",
     telefone: "(61)982252824",
     email: "robim.ner@gmal.com",
     motivo_contato: 1,
     mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
   }
>>> $result->save(); //Obs: as alterações só serão salvas após executar o método save()
=> true
>>>

//==================================================================================
//MÉTODO fill() e save()
//==================================================================================
//obs: nunca utilizar o método fill() após uma consulta utilizada como o método ::where()
=> App\SiteContato {#3401}
PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman
>>> use \App\SiteContato;
>>> $contato = new SiteContato();
=> App\SiteContato {#3399}
>>> $result = $contato::find(4);
=> App\SiteContato {#4191
     id: 4,
     created_at: "2021-11-01 13:46:02",
     updated_at: "2021-11-01 13:46:02",
     nome: "Maria Clara",
     telefone: "(61)90636987649",
     email: "mariaClara@gmail.com",
     motivo_contato: 1,
     mensagem: "Hello World",
   }
>>> $result->fill(['nome'=>'Clarinha']);
=> App\SiteContato {#4191
     id: 4,
     created_at: "2021-11-01 13:46:02",
     updated_at: "2021-11-01 13:46:02",
     nome: "Clarinha",
     telefone: "(61)90636987649",
     email: "mariaClara@gmail.com",
     motivo_contato: 1,
     mensagem: "Hello World",
   }
>>> $result->save();
=> true
>>>
//==================================================================================
//MÉTODO ::where() e update()
//==================================================================================
// No caso do update e where, a atualização do registro jé é feita no ato da consulta

>>> $pessoa = new SiteContato();
=> App\SiteContato {#4192}
>>> $pessoa::where('id', '=', 4)->update(['nome'=>'Clotílde']);
=> 1
>>>

```

## Deletando Registros

```php
//Para deletar registros posso utilizar o método delete() mesmo antes
//de salvar a consulta em uma variável
>>> $contato;
=> App\SiteContato {#3399}
>>> $contato::find(11)->delete();
=> true
>>>

//Também posso utilizar o método ::destroy(id ou array de ids), que
//espera um id ou um array de id's.

>>> $contato::destroy(13);
=> 1 //esse retorno sendo 1 significa que um registro foi deletado.
>>>
```

### softDelete()

O método de remoção suave de registros faz com que possamos excluir os registros somente para a consulta porém ele continua

salvo no banco de dados, porém, fica omitido. Neste caso ele precisa de uma coluna na tabela chamada deleted_at, se a coluna estiver null significa

que o registro está ativo e se estiver com uma data e hora significa que ele será ignorado na consultas que forem efetuadas para ele como se o mesmo

não existisse. ideal para quando pecisamos deletar algum registro, porém, manter para fins históricos.

 Para adicionar o método de remoção suave precisamos fazer algumas modificações na estrutura do projeto:

1°) no contexto do nosso model que vai se relacionar com tabela que utilizara o softDelete vamos por meios de uma 'trait' (Uma forma de herança horizontal já que

no conceito de orientação a objetos, uma classe só pode herdar de uma única classe), iremos incorporar os métodos e propriedades contidos na classe SoftDeletes como

mostrado abaixo:

```php
//MODEL
//=================================================================================

<?php

namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes; //Aqui estou trazendo para meu contexto

class Fornecedor extends Model
{
    //
    use SoftDeletes; // Aqui estou incorporando a classe ao meu model

    protected $table = 'fornecedores';
    protected $fillable = ['nome', 'site', 'uf', 'email'];
}
//obs: No model só são essas alterações.
```

2°) O segundo passo é alterar as migrations, no caso adicionar uma nova coluna a tabela fornecedores

```php
//No diretório raiz do meu projeto eu vou criar uma migration que acrescentará
//uma nova coluna a tabela 'fornecedores' e manterá o desenvolvimento do banco
// de dados incremental.

PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan make:migration alter_fornecedores_softdelete

Created Migration: 2021_11_12_040334_alter_fornecedores_softdelete
```

3°)Após criada a migration temos que configurar os métodos up() e down() criando a coluna e excluindo como mostrado abaixo:

```php

//MIGRATION alter_fornecedores_softdelete
//=================================================================================

<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AlterFornecedoresSoftdelete extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::table('fornecedores', function(Blueprint $table){  // aqui estou criando uma nova coluna
            $table->softDeletes();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('fornecedores', function(Blueprint $table){ // aqui estou excluindo
            $table->dropSoftDeletes();
        });       
    }
}

//Se eu rodar o comando php artisan migrate:status terei o seguinte retorno

PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan migrate:status
+------+-----------------------------------------------------------------+-------+
| Ran? | Migration                                                       | Batch |
+------+-----------------------------------------------------------------+-------+
| Yes  | 2014_10_12_000000_create_users_table                            | 1     |
| Yes  | 2019_08_19_000000_create_failed_jobs_table                      | 1     |
| Yes  | 2021_10_17_182957_create_site_contatos_table                    | 1     |
| Yes  | 2021_10_21_172227_create_fornecedores_table                     | 1     |
| Yes  | 2021_10_21_192200_alter_fornecedores_novas_colunas              | 1     |
| Yes  | 2021_10_22_023350_create_produtos_table                         | 1     |
| Yes  | 2021_10_24_021005_create_produto_detalhes_table                 | 1     |
| Yes  | 2021_10_29_032536_create_unidades_table                         | 1     |
| Yes  | 2021_10_29_185909_ajuste_produtos_filiais                       | 1     |
| Yes  | 2021_10_29_200953_alter_fornecedores_nova_coluna_site_com_after | 1     |
| No   | 2021_11_12_040334_alter_fornecedores_softdelete                 |       |
+------+-----------------------------------------------------------------+-------+

// no caso a migration ainda não foi aplicada no contexto da tabela.

//Para finaliza, é só atualizar as migrations como o comando:

PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan migrate

Migrating: 2021_11_12_040334_alter_fornecedores_softdelete
Migrated:  2021_11_12_040334_alter_fornecedores_softdelete (0.11 seconds)

//se olharmos na tabela fornecedores, veremos que foi criado uma coluna chamada deleted_at
// se dermos uma describe fornecedores; veremos a coluna do tipo timestamp criada

mysql> describe fornecedores;
+------------+-----------------+------+-----+---------+----------------+
| Field      | Type            | Null | Key | Default | Extra          |
+------------+-----------------+------+-----+---------+----------------+
| id         | bigint unsigned | NO   | PRI | NULL    | auto_increment |
| nome       | varchar(50)     | NO   |     | NULL    |                |
| site       | varchar(150)    | YES  |     | NULL    |                |
| created_at | timestamp       | YES  |     | NULL    |                |
| updated_at | timestamp       | YES  |     | NULL    |                |
| uf         | varchar(2)      | NO   |     | NULL    |                |
| email      | varchar(150)    | NO   |     | NULL    |                |
| deleted_at | timestamp       | YES  |     | NULL    |                |
+------------+-----------------+------+-----+---------+----------------+
8 rows in set (0.04 sec)

// Agora podemos utilizar o recurso softDelete()
```

## Restaurando registros deletados com softDelete()

É possível recuperar por meio de uma consulta registros que foram excluídos de um model onde esteja configurado o softDelete utilizando o método withTrashed()→get() como mostrado abaixo:

obs: O método withTrashed() também retornará os registros que não foram excluídos.

```php
//TABELA DE EXEMPLO
mysql> select * from fornecedores;
+----+---------------+--------------------+---------------------+---------------------+----+----------------------+---------------------+
| id | nome          | site               | created_at          | updated_at          | uf | email                | deleted_at          |
+----+---------------+--------------------+---------------------+---------------------+----+----------------------+---------------------+
|  1 | xyz           | www.xyz.com.br     | 2021-11-01 14:07:47 | 2021-11-13 05:25:43 | DF | xyz@gmail.com        | 2021-11-13 05:25:43 |
|  2 | loja          | loja.com.br        | 2021-11-01 17:46:03 | 2021-11-13 05:38:20 | MG | loja@email.com       | 2021-11-13 05:38:20 |
|  3 | tinturaria    | tinturaria.com.br  | 2021-11-01 18:03:41 | 2021-11-13 05:38:20 | DF | tinturaria@email.com | 2021-11-13 05:38:20 |
|  4 | multimarcas   | NULL               | 2021-11-02 02:11:15 | 2021-11-12 04:29:29 | RJ | multimarca@email.com | 2021-11-12 04:29:29 |
|  5 | juneko        | juneko.com.br      | 2021-11-11 13:49:07 | 2021-11-13 05:38:20 | DF | juneko@hotmail.com   | 2021-11-13 05:38:20 |
|  6 | JN jóias      | jnjoias.com.br     | NULL                | NULL                | RJ | jnjoias@email.com    | NULL                |
|  7 | Laranja & Cia | laranjaecia.com.br | 2021-11-13 05:49:11 | 2021-11-13 05:49:11 | PA | laranja@gmail.com    | NULL                |
+----+---------------+--------------------+---------------------+---------------------+----+----------------------+---------------------+
7 rows in set (0.00 sec)

>>> $fornecedor::withTrashed()->get();
=> Illuminate\Database\Eloquent\Collection {#3443
     all: [
       App\Fornecedor {#3400
         id: 1,
         nome: "xyz",
         site: "www.xyz.com.br",
         created_at: "2021-11-01 14:07:47",
         updated_at: "2021-11-13 05:25:43",
         uf: "DF",
         email: "xyz@gmail.com",
         deleted_at: "2021-11-13 05:25:43",
       },
       App\Fornecedor {#3401
         id: 2,
         nome: "loja",
         site: "loja.com.br",
         created_at: "2021-11-01 17:46:03",
         updated_at: "2021-11-13 05:38:20",
         uf: "MG",
         email: "loja@email.com",
         deleted_at: "2021-11-13 05:38:20",
       },
       App\Fornecedor {#3439
         id: 3,
         nome: "tinturaria",
         site: "tinturaria.com.br",
         created_at: "2021-11-01 18:03:41",
         updated_at: "2021-11-13 05:38:20",
         uf: "DF",
         email: "tinturaria@email.com",
         deleted_at: "2021-11-13 05:38:20",
       },
       App\Fornecedor {#3419
         id: 4,
         nome: "multimarcas",
         site: null,
         created_at: "2021-11-02 02:11:15",
         updated_at: "2021-11-12 04:29:29",
         uf: "RJ",
         email: "multimarca@email.com",
         deleted_at: "2021-11-12 04:29:29",
       },
       App\Fornecedor {#3450
         id: 5,
         nome: "juneko",
         site: "juneko.com.br",
         created_at: "2021-11-11 13:49:07",
         updated_at: "2021-11-13 05:38:20",
         uf: "DF",
         email: "juneko@hotmail.com",
         deleted_at: "2021-11-13 05:38:20",
       },
       App\Fornecedor {#3456
         id: 6,
         nome: "JN jóias",
         site: "jnjoias.com.br",
         created_at: null,
         updated_at: null,
         uf: "RJ",
         email: "jnjoias@email.com",
         deleted_at: null,
       },
       App\Fornecedor {#3458
         id: 7,
         nome: "Laranja & Cia",
         site: "laranjaecia.com.br",
         created_at: "2021-11-13 05:49:11",
         updated_at: "2021-11-13 05:49:11",
         uf: "PA",
         email: "laranja@gmail.com",
         deleted_at: null,
       },
     ],
   }
>>>
```

Também posso filtrar apenas os registros excluídos como base no método softDelete() como mostrado abaixo

utilizando o método onlyTrashed():

```php
>>> $fornecedor::onlyTrashed()->get(); //Esse método só retornará os registros excluídos pelo método softDelete()
=> Illuminate\Database\Eloquent\Collection {#3432
     all: [
       App\Fornecedor {#3454
         id: 1,
         nome: "xyz",
         site: "www.xyz.com.br",
         created_at: "2021-11-01 14:07:47",
         updated_at: "2021-11-13 05:25:43",
         uf: "DF",
         email: "xyz@gmail.com",
         deleted_at: "2021-11-13 05:25:43",
       },
       App\Fornecedor {#3449
         id: 2,
         nome: "loja",
         site: "loja.com.br",
         created_at: "2021-11-01 17:46:03",
         updated_at: "2021-11-13 05:38:20",
         uf: "MG",
         email: "loja@email.com",
         deleted_at: "2021-11-13 05:38:20",
       },
       App\Fornecedor {#3441
         id: 3,
         nome: "tinturaria",
         site: "tinturaria.com.br",
         created_at: "2021-11-01 18:03:41",
         updated_at: "2021-11-13 05:38:20",
         uf: "DF",
         email: "tinturaria@email.com",
         deleted_at: "2021-11-13 05:38:20",
       },
       App\Fornecedor {#3444
         id: 4,
         nome: "multimarcas",
         site: null,
         created_at: "2021-11-02 02:11:15",
         updated_at: "2021-11-12 04:29:29",
         uf: "RJ",
         email: "multimarca@email.com",
         deleted_at: "2021-11-12 04:29:29",
       },
       App\Fornecedor {#3447
         id: 5,
         nome: "juneko",
         site: "juneko.com.br",
         created_at: "2021-11-11 13:49:07",
         updated_at: "2021-11-13 05:38:20",
         uf: "DF",
         email: "juneko@hotmail.com",
         deleted_at: "2021-11-13 05:38:20",
       },
     ],
   }
```

Para recuperar registros deletados pelo softDelete(), podemos utilizar o método $objeto[índice_do_array]::restore() informando o índice do objeto no qual queremos recuperar como mostrado abaixo: