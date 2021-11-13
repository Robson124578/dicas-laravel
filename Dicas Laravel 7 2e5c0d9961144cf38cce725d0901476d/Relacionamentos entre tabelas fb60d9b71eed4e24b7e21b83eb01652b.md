# Relacionamentos entre tabelas

## Relacionamento 1:1 (1 para 1)

```php
	
// TABELA produtos/////////////////////////////////

public function up()
    {
        Schema::create('produtos', function (Blueprint $table) {
            $table->id(); 
						//A coluna acima será referênciada na tabela produto_detalhes
						//caracterizando uma foreign key com rela cionamento de 1 para 1
            $table->string('nome', 100);
            $table->text('descricao')->nullable();
            $table->integer('peso')->nullable();
            $table->float('preco_venda', 8, 2);
            $table->integer('estoque_minimo')->default(1);
            $table->integer('estoque_maximo')->default(1);
            $table->timestamps();
        });
    }

	// TABELA produto_detalhes///////////////////////////

public function up()
    {
        Schema::create('produto_detalhes', function (Blueprint $table) {
            $table->id();
            $table-> float('comprimento', 8,2);
            $table-> float('altura', 8,2);
            $table-> float('largura', 8,2);
            $table->unsignedBigInteger('produto_id');  
            // o tipo de dado (unsignedBigInteger) da coluna acima que representa uma chave estrangeira de outra tabela
            //tem que ser o mesmo da coluna referenciada na outra tabela ('produtos') 
            $table->timestamps();
            
            //constraint de integridade referencial que indica a coluna 'produto_id' da tabela 'produto_detalhes' seja
            //chave estrangeira da tabela 'produtos' referenciando a coluna 'id'
            $table->foreign('produto_id')->references('id')->on('produtos');
          
            //como o unique() eu consigo estabelecer que a coluna produto_id
            //não receba valores repetidos.
            $table->unique('produto_id');

        });
    }
```

---

## Relacionamentos de 1:n (um para muitos)

```php
public function up()
    {
        Schema::create('unidades', function (Blueprint $table) {
            $table->id();
            $table->string('unidade', 5); //cm, kg, mm
            $table->string('descrição', 30);
            $table->timestamps();
        });

        //Abaixo, através do objeto Schema e utilizando o método estático table, eu estou
        //adicionando novas colunas nas colunas 'produtos' e 'produtos_detalhes' e adicionando
        //o relacionamento de 1:n entre as mesmas e a tabela 'unidades'.

        //Adicionar relacionamento com a tabela produtos
        Schema::table('produtos', function(Blueprint $table){
            $table->unsignedBigInteger('unidade_id');
            $table->foreign('unidade_id')->references('id')->on('unidades');
            //Para ser um relacionamento de 1 para muitos, basta omitir o método unique()
        });

        //Adicionar relacionamento com a tabela produtos_detalhes
        Schema::table('produto_detalhes', function(Blueprint $table){
            $table->unsignedBigInteger('unidade_id');
            $table->foreign('unidade_id')->references('id')->on('unidades');
        });

        //Quando o método up() rodar vai criar uma coluna na tabela 'produtos' e outra na tabela
        //'produto_detalhes'. Os nomes das colunas que serão as FK's seguirão a seguinte nomenclatura:
        // ['nome-da-tabela']_['nome-da-coluna']_foreign

    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        //Agora temos que implementar ao método down as configurações necessárias para a remoção
        //das chaves estrangeiras e na sequencia a exclusão da tabela, caso seja necessário.

        //Aqui estou removendo o relacionamento entre a tabela 'unidades' e a tabela 'unidades'
        //e depois excluindo a coluna
        Schema::table('produtos', function(Blueprint $table){
            //remover a FK
            $table->dropForeign('produtos_unidade_id_foreign');
            //remover o relacionamento
            $table->dropColumn('unidade_id');
        });

        //Agora vou remover o relacionamento e a coluna da tabela 'produto_detalhes'
        Schema::table('produto_detalhes', function(Blueprint $table){
            //removendo a FK
            $table->dropForeign('produto_detalhes_unidade_id_foreign');
            //removendo o relacionamento
            $table->dropColumn('unidade_id');
        });

        Schema::dropIfExists('unidades');

    }
```

## Relacionamento n:n (muitos para muitos)

no caso de haver a ocorrência de um relacionamento de muitos para muitos, na modelagem de kuma tabela se faz necessária a criação de uma nova tabela que receberá as foreign keys das tabelas