# Usando um valor default para uma variável não definida ou null (??)

```php
<h1>Fornecedores</h1>
{{--
O operador condicional de valor default é usado para definir um valor padrão a uma variável
no caso da variável não ter sido definida ou ser null
 --}}
<p>valor: {{ $variavel[1]['key'] ?? 'Não possui' }}</p>
```