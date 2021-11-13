# Collections

Uma collection nada mais é do que um array de objetos. Abaixo seguem alguns métodos para manipular as collections após serem retornadas da consulta e atribuídas a uma variável:

segue abaixo alguns método interessantes para manipulação das collections:

```php
PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman
>>> use \App\SiteContato;
>>> $contato = new SiteContato();
=> App\SiteContato {#3399}
>>> $result = $contato::where('id','<',4)->get();
=> Illuminate\Database\Eloquent\Collection {#4126
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
       App\SiteContato {#3719
         id: 2,
         created_at: "2021-10-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "paulinha",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       App\SiteContato {#4087
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

//Aqui estou utuilizanso o método first() para
//retornar o 1° item da coleção

>>> $result->first();
=> App\SiteContato {#4125
     id: 1,
     created_at: "2021-11-01 03:34:34",
     updated_at: "2021-11-01 03:34:34",
     nome: "Robson",
     telefone: "(61)982252824",
     email: "robim.ner@gmal.com",
     motivo_contato: 1,
     mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
   }

//Aqui estou utuilizanso o método last() para
//retornar o ultimo item da coleção
>>> $result->last();
=> App\SiteContato {#4087
     id: 3,
     created_at: "2021-11-01 03:44:49",
     updated_at: "2021-11-01 03:44:49",
     nome: "Isaac Robson",
     telefone: "(61)982252824",
     email: "zachboy@gmail.com",
     motivo_contato: 1,
     mensagem: "Olá, tem Roblox ai ?",
   }
>>>

//Aqui com o método reverse() eu consigo inverter
//a ordem dentro do array das collections
>>> $result->reverse();
=> Illuminate\Database\Eloquent\Collection {#4281
     all: [
       2 => App\SiteContato {#4087
         id: 3,
         created_at: "2021-11-01 03:44:49",
         updated_at: "2021-11-01 03:44:49",
         nome: "Isaac Robson",
         telefone: "(61)982252824",
         email: "zachboy@gmail.com",
         motivo_contato: 1,
         mensagem: "Olá, tem Roblox ai ?",
       },
       1 => App\SiteContato {#3719
         id: 2,
         created_at: "2021-10-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "paulinha",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       0 => App\SiteContato {#4125
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
>>>

//Método toArray() converte a coleção em array lembrando
//que depois de convertido para um array não consigo mais
//utilizar os métodos estáticos.

>>> $result->reverse();
=> Illuminate\Database\Eloquent\Collection {#4281
     all: [
       2 => App\SiteContato {#4087
         id: 3,
         created_at: "2021-11-01 03:44:49",
         updated_at: "2021-11-01 03:44:49",
         nome: "Isaac Robson",
         telefone: "(61)982252824",
         email: "zachboy@gmail.com",
         motivo_contato: 1,
         mensagem: "Olá, tem Roblox ai ?",
       },
       1 => App\SiteContato {#3719
         id: 2,
         created_at: "2021-10-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "paulinha",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       0 => App\SiteContato {#4125
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
>>>

// Aqui com o método toJson() eu converto minha collection
//para uma estrutura em json.

>>> $resultJson = $contato::all()->toJson();

{
   "id":1,
   "created_at":"2021-11-01T03:34:34.000000Z",
   "updated_at":"2021-11-01T03:34:34.000000Z",
   "nome":"Robson",
   "telefone":"(61)982252824",
   "email":"robim.ner@gmal.com",
   "motivo_contato":1,
   "mensagem":"Ol\u00e1, eu gostaria de tirar algumas d\u00favidas"
},
{
   "id":2,
   "created_at":"2021-10-01T03:40:10.000000Z",
   "updated_at":"2021-11-01T03:40:10.000000Z",
   "nome":"paulinha",
   "telefone":"(61)981985565",
   "email":"almeida.paula86@gmail.com",
   "motivo_contato":2,
   "mensagem":"ol\u00e1, eu gostaria de fazer um or\u00e7amento"
},
{
   "id":3,
   "created_at":"2021-11-01T03:44:49.000000Z",
   "updated_at":"2021-11-01T03:44:49.000000Z",
   "nome":"Isaac Robson",
   "telefone":"(61)982252824",
   "email":"zachboy@gmail.com",
   "motivo_contato":1,
   "mensagem":"Ol\u00e1, tem Roblox ai ?"
},
{
   "id":4,
   "created_at":"2021-11-01T13:46:02.000000Z",
   "updated_at":"2021-11-01T13:46:02.000000Z",
   "nome":"Maria Clara",
   "telefone":"(61)90636987649",
   "email":"mariaClara@gmail.com",
   "motivo_contato":1,
   "mensagem":"Hello World"
},
{
   "id":5,
   "created_at":"2021-11-02T13:56:56.000000Z",
   "updated_at":"2021-11-02T13:56:56.000000Z",
   "nome":"zezinho",
   "telefone":"(61)947663355",
   "email":"zezin@email.com",
   "motivo_contato":1,
   "mensagem":"Hello"
},
{
   "id":6,
   "created_at":"2021-11-02T14:10:50.000000Z",
   "updated_at":"2021-11-02T14:10:50.000000Z",
   "nome":"paulo",
   "telefone":"(61)98887766",
   "email":"paulo@email.com",
   "motivo_contato":1,
   "mensagem":"tudo certo !"
},
{
   "id":7,
   "created_at":null,
   "updated_at":null,
   "nome":"Jo\u00e3o",
   "telefone":"(88) 91111-2222",
   "email":"joao@contato.com.br",
   "motivo_contato":3,
   "mensagem":"\u00c9 muito dif\u00edcil localizar a op\u00e7\u00e3o de listar todos os produtos"
},
{
   "id":8,
   "created_at":null,
   "updated_at":null,
   "nome":"Rosa",
   "telefone":"(33) 92222-3333",
   "email":"rosa@contato.com.br",
   "motivo_contato":1,
   "mensagem":"Quando custa essa aplica\u00e7\u00e3o?"
},
{
   "id":9,
   "created_at":null,
   "updated_at":null,
   "nome":"Fernando",
   "telefone":"(11) 94444-5555",
   "email":"fernando@contato.com.br",
   "motivo_contato":1,
   "mensagem":"Como consigo criar multiplos usu\u00e1rios para minha empresa?"
},
{
   "id":10,
   "created_at":null,
   "updated_at":null,
   "nome":"Andr\u00e9",
   "telefone":"(88) 95555-6666",
   "email":"andre@contato.com.br",
   "motivo_contato":2,
   "mensagem":"Parab\u00e9ns pela ferramenta, estou obtendo \u00f3timos resultados!"
},
{
   "id":11,
   "created_at":null,
   "updated_at":null,
   "nome":"Ana",
   "telefone":"(33) 96666-7777",
   "email":"ana@contato.com.br",
   "motivo_contato":3,
   "mensagem":"N\u00e3o gostei muito das cores, consigo mudar de tema?"
},
{
   "id":12,
   "created_at":null,
   "updated_at":null,
   "nome":"Helena",
   "telefone":"(11) 97777-8888",
   "email":"helena@contato.com.br",
   "motivo_contato":2,
   "mensagem":"Consigo controlar toda a minha empresa de modo f\u00e1cil e pr\u00e1tico."
}
```

## Pluck()

O método pluck retorna todos os valores de uma coluna designada dentro de uma coleção de objetos:

Tabela de exemplo:

![Untitled](Eloquente%20(ORM)%20Tinker,%20create()%20e%20$fillable,%20all(%2034c2d6266c774d4784639c1dd405352e/Untitled.png)

```php
PS C:\Users\robson\Documents\Code\app_super_gestao> php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.19 — cli) by Justin Hileman

//instanciando a classe para o objeto/variável $dado
>>> $dado = new \App\SiteContato();
=> App\SiteContato {#3401}

//buscando os dados que por sua vez virão em uma coleção de objetos
//e salvando na variável $result
>>> $result = $dado::whereBetween('id', [1,3])->get();
=> Illuminate\Database\Eloquent\Collection {#4125
     all: [
       App\SiteContato {#4124
         id: 1,
         created_at: "2021-11-01 03:34:34",
         updated_at: "2021-11-01 03:34:34",
         nome: "Robson",
         telefone: "(61)982252824",
         email: "robim.ner@gmal.com",
         motivo_contato: 1,
         mensagem: "Olá, eu gostaria de tirar algumas dúvidas",
       },
       App\SiteContato {#3718
         id: 2,
         created_at: "2021-10-01 03:40:10",
         updated_at: "2021-11-01 03:40:10",
         nome: "paulinha",
         telefone: "(61)981985565",
         email: "almeida.paula86@gmail.com",
         motivo_contato: 2,
         mensagem: "olá, eu gostaria de fazer um orçamento",
       },
       App\SiteContato {#4086
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

//Usando o pluck para faazer um filtro me trazer
//apenas os itens da coluna nome.

>>> $result->pluck('nome');
=> Illuminate\Support\Collection {#4281
     all: [
       "Robson",
       "paulinha",
       "Isaac Robson",
     ],
   }

//obs: Caso eu queira retornar a chave do valor, basta inserir um  segundo parâmetro
//assim: pluck('valor', 'chave');
```