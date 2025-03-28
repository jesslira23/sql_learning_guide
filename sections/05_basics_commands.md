# Comandos básicos

# Índice
- [select](#select)
- [select distinct](#select-distinct)
- [where](#where)
- [order by](#order-by) - TODO
- [Operadores lógicos](#operadores-lógicos)
- [Operadores in e like](#operadores-in-e-like)


A seguir, alguns dos principais comandos SQL utilizados para manipulação de dados são apresentados:

---

# SELECT

A instrução `select` é usada para selecionar dados de tabelas.

- selecionando todas as colunas da tabela Produtos_csv:
```
select *
from Produtos_csv;
```

- aliasing nomes de colunas (a palavra-chave AS é opcional)
```
select Produto_ID, Nome as nome_produto, Descrição as descricao_produto
from Produtos_csv;
```

- aliasing nomes de colunas sem a palavra-chave AS
```
select Produto_ID, Nome nome_produto, Descrição descricao_produto
from Produtos_csv;
```

- use acentos graves para especificar aliases de coluna com caracteres de espaço em branco
```
select Produto_ID as `ID do 	produto`, Nome as `Nome do produto`, Descrição as `Descrição do produto`
from Produtos_csv;
```

- aliasing Table names (AS palavra-chave opcional)
```
select prod.Produto_ID, prod.Nome, prod.Descrição from Produtos_csv as prod;
```

- usando o alias Table name como um prefixo do star
```
select prod.*
from Produtos_csv as prod;
```



---

# SELECT DISTINCT

O `SELECT DISTINCT` é usado para retornar apenas valores únicos de uma coluna, eliminando duplicatas.

- selecionando registros de categoria dos produtos é única
```
select distinct Categoria
from Produtos_csv;
```

- selecionando registros onde os valores em todas as colunas são únicos
```
select distinct *
from Produtos_csv;
```

---

# WHERE

A cláusula `WHERE` filtra os registros de acordo com uma condição específica. Para mais detalhes, [Syntax where](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-qry-select-where).


Operadores condicionais:
```
= 'equal to'
> 'greater than'
>= 'geater than or equal to'
< 'less than'
<= 'less than or equal to'
<> 'not equal to'
```


- filtrando registros onde Tamanho é 'XS'
```
select *
from Produtos_csv
where Tamanho = 'XS';
```

- selecionando registros com base em uma coluna de registro de data e hora
- valores de data/registro de data e hora devem ser colocados entre aspas
```
select *
from Pedidos_Compra_csv
where `Data do Pedido` = '2016-01-13 23:20:30';
```

- valores numéricos não precisam estar entre aspas
```
select *
from Produtos_csv
where Preço = 71.3;
```

- usando o operador maior ou igual na condição
```
select *
from Pedidos_Compra_csv
where `Data do Pedido` >= '2016-01-13 23:20:30';
```

- usando o operador diferente de
```
select *
from Produtos_csv
where Categoria <> 'Calçado';
```

---

# ORDER BY

O `ORDER BY` ordena os resultados de uma consulta de forma ascendente (ASC) ou descendente (DESC).

---

# Operadores Lógicos

SQL permite o uso de operadores lógicos para combinar múltiplas condições na cláusula `WHERE`:

`AND`: Ambas as condições devem ser verdadeiras.[Ref](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/and)

`OR`: Pelo menos uma das condições deve ser verdadeira.[Ref](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/or)

`NOT`: Inverte a condição. [Ref](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/not)

`BETWEEN`: Seleciona valores em um intervalo e esses valores podem ser números, textos ou datas. O BETWEEN é inclusivo ou seja, os valores dos extremos (valor inicial e valor final) também são incluídos no intervalo. [Ref](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/between)


## AND
```
select *
from Produtos_csv
where Categoria = 'Roupas' and Cor = 'Verde';
```

## OR
```
select *
from Produtos_csv
where Categoria = 'Roupas' or Cor = 'Verde';
```

## NOT
```
select *
from Produtos_csv
where not Categoria = 'Roupas';
```

## BETWEEN
```
select *
from Produtos_csv
where Tamanho between 34 and 37;
```

> Observação: ao usar várias condições e condições aninhadas, use parênteses, os parênteses têm precedência sobre outras condições
```
select *
from Produtos_csv
where (Categoria = 'Roupas' and Cor = 'Verde') or (Tamanho = 'L');
```

---

# Operadores IN e LIKE

- O operador `IN` permite que sejam especificados múltiplos critérios dentro do `WHERE` é uma alternativa reduzida ao OR. [Ref](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/in)
- O `LIKE` é usado em conjunto com o `WHERE` para procurar por um determinado padrão em uma coluna. [Ref](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/like)

O sinal de % representa zero, um ou múltiplos caracteres.
O _ representa um único caractere

Aplicação do **LIKE**
| Exemplo | Definição |
|---|---|
| where nome_produto like 'a%' | Encontra qualquer valor que começa com 'a' |
| where nome_produto like '%a' | Encontra qualquer valor que termina com 'a' |
| where nome_produto like '%a%' | Encontra qualquer valor que tenha 'a'  |
| where nome_produto like '_a%' | Encontra qualquer valor que tenha 'a' a partir do segundo caractere |
| where nome_produto like 'a_%' | Encontra qualquer valor que comece com 'a' e tenha pelo menos 2 caracteres |
| where nome_produto like 'a%o' | Encontra qualquer valor que comece com 'a' e termine com 'o' |

- procurando por valores que estão dentro dos parênteses
```
select *
from Produtos_csv
where Cor in ('Verde','Vermelho','Laranja');
```

- procurando por valores de entrada com 'Ver' dentro da string
```
select *
from Produtos_csv
where Cor like '%Ver%';
```

- procurando por qualquer padrão com 5 caracteres na entrada
```
select *
from Produtos_csv
where Cor like '_____';
````

---

# Condicional com CASE WHEN


[ref](https://learnsql.com.br/blog/resumo-de-sql-basico/)

[<img align="center" src="../imagens/00_general/botao-home.png" height="25" width="25"/> Home](../README.md)