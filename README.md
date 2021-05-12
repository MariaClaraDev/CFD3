## Questão 2

Para conseguir desenvolver as respostas, tive que usar uma imagem docker anexa ao projeto.

### Resposta Item A)

```SQL
select p.codigo_de_barras 
from Produtoinfo pf
	inner join Produto p on (pf.idproduto = p.id)
where pf.data_cadastro >= current_date -10 
```


### Resposta Item B)

```SQL
select o.nome 
from Produtoinfo pf
	inner join Origem o on (pf.idorigem = o.id)
where pf.data_atualizacao between '2020-03-01' and '2020-03-30' or pf.data_cadastro between '2020-03-01' and '2020-03-30'
```


### Resposta Item C)

```SQL
UPDATE Produtoinfo
set idfabricante = (select id from Fabricante where nome = 'JOAO')
where Produtoinfo.id in (
    select pf.id from Produtoinfo pf 
        inner join Origem o on (pf.idorigem = o.id)
        inner join Fabricante f on (pf.idfabricante = f.id)
    where o.nome = 'DISTRIBUIDORA TESTE'
        and f.nome = 'Maria'
)

```

### Resposta Item D)

```SQL
select distinct
	p2.codigo_de_barras, 
	p.descricao,
	f.nome,
	p.codigo_interno,
	o.preferencia
	
from produtoinfo p 
	join produto p2 on (p.idproduto = p2.id)
	join fabricante f on (p.idfabricante = f.id)
	join origem o on (p.idorigem = o.id)
order by o.preferencia asc;

```