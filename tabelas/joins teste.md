--PESQUISAR DADOS NO BANCO DE DADOS
SELECT numero, nome FROM banco;
SELECT banco_numero, numero, nome FROM agencia;
SELECT numero, nome FROM cliente;
SELECT banco_numero, agencia_numero, numero, digito, cliente_numero FROM conta_corrente;
SELECT id, nome FROM tipo_transacao;
SELECT banco_numero, agencia_numero, conta_corrente_numero, conta_corrente_digito, cliente_numero, valor FROM cliente_transacoes;

-- CONTAGEM DE TODOS OS DADOS PRESENTES EM BANCO
SELECT count(1) FROM banco;


-- CONTAGEM DE TODOS OS DADOS PRESENTES EM AGENCIA
SELECT count(1) FROM agencia;

--EXEMPLO JOIN: MOSTRA DADOS QUE TEM RELAÇÂO
SELECT banco.numero, banco.nome, agencia.numero, agencia.nome
FROM banco
JOIN agencia ON agencia.banco_numero = banco.numero;

--CONTAGEM DE BANCOS PRESENTES NO GRUPO BANCO QUE POSSUEM AGENCIA
SELECT banco.numero 
FROM banco
JOIN agencia ON agencia.banco_numero = banco.numero
GROUP BY banco.numero;

--MESMA CONTAGEM POREM COM COUNT DISTINCT
SELECT count (distinct banco.numero) 
FROM banco
JOIN agencia ON agencia.banco_numero = banco.numero;

--EXEMPLO LEFT JOIN: RETORNA TODOS OS DADOS DA TABELA ESQUERDA E APENAS OS RELACIONADOS DA TABELA DIREITA
SELECT banco.numero, banco.nome, agencia.numero, agencia.nome
FROM banco
LEFT JOIN agencia ON agencia.banco_numero = banco.numero;

--EXEMPLO RIGHT JOIN: RETORNA TODOS OS DADOS DA TABELA DIREITA E APENAS OS RELACIONADOS DA TABELA ESQUERDA
SELECT agencia.numero, agencia.nome, banco.numero, banco.nome
FROM agencia
RIGHT JOIN banco ON banco.numero = agencia.banco_numero;

--EXEMPLO FULL JOIN: RETORNA TODAS AS RELACÕES POSSIVEIS
SELECT banco.numero, banco.nome, agencia.numero, agencia.nome
FROM banco
FULL JOIN agencia ON agencia.banco_numero = banco.numero;

--EXEMPLO DE UM JOIN COMPLETO COM DIVERSAS TABELAS
SELECT banco.nome, agencia.nome, conta_corrente.numero, conta_corrente.digito, cliente.nome
FROM banco
JOIN agencia ON agencia.banco_numero = banco.numero
JOIN conta_corrente ON conta_corrente.banco_numero = agencia.banco_numero
AND conta_corrente.agencia_numero = agencia.numero
JOIN cliente
ON cliente.numero = conta_corrente.cliente_numero;


