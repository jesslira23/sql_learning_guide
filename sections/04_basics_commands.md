# Comandos básicos

# Índice
[select](#select)
[select distinct](#select-distinct)
[where](#where)

---

# SELECT

Definição: A instrução select é usada para selecionar dados de tabelas.


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


Descrição: Selecione todas as linhas correspondentes das referências da tabela após remover duplicatas nos resultados.

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

Descrição: WHERE é um filtro de dados. Traz somente registros que atendam determinada condição. Para mais detalhes, [Syntax where](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-qry-select-where).


Operadores condicionais:
```
= 'equal to'
> 'greater than'
>= 'geater than or equal to'
< 'less than'
<= 'less than or equal to'
<> 'not equal to'
````


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


# Operadores Lógicos

Definições:
AND:
https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/and

select coluna1, coluna2, ...
from nome_tabela
where condition1 AND condition2 AND condition3 ...;

OR:
https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/or

select coluna1, coluna2, ...
from nome_tabela
where condition1 OR condition2 OR condition3 ...;

NOT:
https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/not

select coluna1, coluna2, ...
from nome_tabela
where NOT condition;


BETWEEN:
https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/functions/between

select coluna1, coluna2, ...
from nome_da_tabela
where column_name BETWEEN value1 AND value2;


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



[<img align="center" src="../imagens/00_general/botao-home.png" height="25" width="25"/> Home](../README.md)