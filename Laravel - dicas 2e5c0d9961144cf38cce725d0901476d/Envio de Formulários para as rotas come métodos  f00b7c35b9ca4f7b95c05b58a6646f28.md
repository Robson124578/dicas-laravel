# Envio de Formulários para as rotas come métodos get,  post e a importância do token @csrf

## Utilizando o método get

O envio de formulário para as roas começará a partir de um formulário que será submetido a rota desejada. Assim como mostrado abaixo, temos que setar nos atributos method="" e action="" no <form> respectivamente o método (get, post delete e etç) e a action (a rota de destino).

```php
//se eu omitisse a declaração do método no atributo method=""
//mesmo assim o formulário por padrão enviaria as informações
//e por padrão definiria o método get, porém é bom deixar
//essas informações explícitas.
<form method="get" action"{{ route('site.contato') }}">
    <input name="nome" type="text" placeholder="Nome" class="borda-preta"><
    <input name="telefone" type="text" placeholder="Telefone" class="borda-preta">                    <br>
    <input name="email" type="text" placeholder="E-mail" class="borda-preta">
    <select name="motivo_contato" class="borda-preta">
        <option value="">Qual o motivo do contato?</option>
        <option value="1">Dúvida</option>
        <option value="2">Elogio</option>
        <option value="3">Reclamação</option>
    </select>
    <textarea name="mensagem" class="borda-preta">Preencha aqui a sua mensagem</textarea>
    <button type="submit" class="borda-preta">ENVIAR</button>
</form>
```

## Utilizando o método post

Para enviarmos um formulário via post precisamos de alterar o código da seginte forma:

```php
//Na view//////////////////////////////////////////////////////

//1° preciso inserir o método post no atributo method="
//2° preciso utilizar a variável @csrf para gerar um token e
//explicitar para o laravel que o formulário esta sendo enviado
//via client( browser) na sessão
<form method="post" action"{{ route('site.contato') }}">
		@csrf
    <input name="nome" type="text" placeholder="Nome" class="borda-preta"><
    <input name="telefone" type="text" placeholder="Telefone" class="borda-preta">                    <br>
    <input name="email" type="text" placeholder="E-mail" class="borda-preta">
    <select name="motivo_contato" class="borda-preta">
        <option value="">Qual o motivo do contato?</option>
        <option value="1">Dúvida</option>
        <option value="2">Elogio</option>
        <option value="3">Reclamação</option>
    </select>
    <textarea name="mensagem" class="borda-preta">Preencha aqui a sua mensagem</textarea>
    <button type="submit" class="borda-preta">ENVIAR</button>
</form>

//Na Rota///////////////////////////////////////////////////////////

//Na rota preciso utilizar o método post como mostrado abaixo:
Route::post('/contato', 'ContatoController@contato')->name('site.contato');
```

## Token @csrf

Ao utilizarmos o token @csrf estamos acoplando uma forma de autênticação através de um token de segurança que é omitido dentro da página mdo formulário que é carregada.

Quando o formulário é submetido, o token é enviado junto os dados enviados do formulário e assim efetuando uma espécie de autenticação com o servidor.