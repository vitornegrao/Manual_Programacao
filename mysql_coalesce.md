# Função COALESCE MySQL

A função `COALESCE` no MySQL é utilizada para retornar o primeiro valor não-nulo de uma lista de expressões. É bastante útil em situações onde você quer lidar com valores nulos (NULL) em suas consultas. 

Aqui está a sintaxe básica da função `COALESCE`:

```sql
COALESCE(expr1, expr2, ..., expr_n)
```

- `expr1, expr2, ..., expr_n` são as expressões que serão avaliadas.
- A função retorna o primeiro valor não-nulo da lista de expressões.

Se todas as expressões forem nulas, a função `COALESCE` retornará `NULL`.

### Exemplo de Uso

Considere uma tabela `clientes` com as seguintes colunas: `id`, `nome`, `telefone`, `email`.

```sql
SELECT 
    id, 
    nome, 
    COALESCE(telefone, email, 'Informação não disponível') AS contato
FROM 
    clientes;
```

Neste exemplo:
- Se `telefone` for não-nulo, ele será retornado.
- Se `telefone` for nulo, mas `email` não for, o `email` será retornado.
- Se ambos `telefone` e `email` forem nulos, a string 'Informação não disponível' será retornada.

### Cenários Comuns de Uso

1. **Substituição de valores nulos:** Quando você quer garantir que um valor padrão seja usado caso um campo específico seja nulo.
2. **Combinação de colunas:** Quando você tem múltiplas colunas que podem conter o mesmo tipo de informação e quer retornar a primeira não-nula.
3. **Limpeza de dados:** Quando você quer assegurar que os resultados da sua consulta não contenham valores nulos que podem causar problemas em análises subsequentes.

### Exemplos Adicionais

1. **Substituição de valor nulo por valor padrão:**

```sql
SELECT 
    id, 
    nome, 
    COALESCE(telefone, 'Telefone não disponível') AS telefone
FROM 
    clientes;
```

2. **Uso em cálculos:**

```sql
SELECT 
    produto, 
    preco, 
    desconto, 
    COALESCE(preco - desconto, preco, 0) AS preco_final
FROM 
    produtos;
```

Neste caso, `preco_final` será calculado considerando o desconto, se houver, ou apenas o preço, se o desconto for nulo. Se ambos forem nulos, retorna 0.

A função `COALESCE` é uma ferramenta poderosa para trabalhar com dados incompletos ou faltantes, garantindo que suas consultas sejam mais robustas e flexíveis.
