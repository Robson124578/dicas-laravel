# Modificadores Nullable e Default

Por padrão no laravel quando criamos as tabelas com suas colunas em uma banco de dados no qual ele esta conectado, os dados por padrão são adicionados não permitindo valores null ou vazio e sem definição de valores padrão.

![Untitled](Modificadores%20Nullable%20e%20Default%20bf1f83c66c024dc6b2651b6372771435/Untitled.png)

como mostrado na figura acima nenhuma das colunas criadas manualmente estão permitindo a entrada de dados vazios (null) e nem valores default.

Para resolver isso podemos no processo de criação da migration implementar essas configurações quando for conveniente como mostrado abaixo:

![Untitled](Modificadores%20Nullable%20e%20Default%20bf1f83c66c024dc6b2651b6372771435/Untitled%201.png)

como mostrado acima, os campos que estão com nullable() passarão a aceitar valores nulos e os campos com default(1) passarão a aceitar o valor no caso de não preenchimento no formulário de entrada.

abaixo veja a uma nova consulta a tabela produtos e veja que as alterações nos campo editados para receber valores nulos e default:

![Untitled](Modificadores%20Nullable%20e%20Default%20bf1f83c66c024dc6b2651b6372771435/Untitled%202.png)