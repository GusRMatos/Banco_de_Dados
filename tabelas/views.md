--SELECT DE TESTE
SELECT numero, nome, ativo
FROM banco;

--CRIAÇÃO DE VIEW
CREATE OR REPLACE VIEW vw_bancos AS (
	SELECT numero, nome, ativo
	FROM banco
);
--BUSCA NA VIEW 
SELECT numero, nome, ativo
FROM vw_bancos;

--SEGUNDA CRIAÇÃO DE VIEW 
CREATE OR REPLACE VIEW vw_bancos2 (banco_numero, banco_nome, banco_ativo)AS(
	SELECT numero, nome, ativo
	FROM banco
);

SELECT banco_numero, banco_nome, banco_ativo
FROM vw_bancos2;

--CRIAÇÃO DE VIEW TEMPORARIA
CREATE OR REPLACE TEMPORARY VIEW vw_agencia AS(
	SELECT nome
	FROM agencia
);
SELECT nome
FROM vw_agencia;

--CRIAÇÃO DE VIEW COM CONDIÇÃO
CREATE OR REPLACE VIEW vw_bancos_ativos AS(
	SELECT numero, nome, ativo
	FROM banco
	WHERE ativo IS TRUE
)WITH LOCAL CHECK OPTION;

--CRIAÇÂO DE VIEW RECURSIVA

--CRIAÇÃO DE TABELA PARA TESTE
CREATE TABLE IF NOT EXISTS funcionarios(
	ID serial,
	nome VARCHAR(50),
	gerente INTEGER,
	PRIMARY KEY (id),
	FOREIGN KEY (gerente) REFERENCES funcionarios (id)
);
INSERT INTO funcionarios (nome, gerente) VALUES ('carlos', null);
INSERT INTO funcionarios (nome, gerente) VALUES ('ana', 1);
INSERT INTO funcionarios (nome, gerente) VALUES ('roberto', 1);
INSERT INTO funcionarios (nome, gerente) VALUES ('paula', 3);

SELECT id, nome, gerente FROM funcionarios WHERE gerente is NULL;

--VIEW RECURSIVA
CREATE OR REPLACE RECURSIVE VIEW vw_func (id, nome, gerente) AS(
	SELECT id, nome, gerente
	FROM funcionarios
	WHERE gerente is NULL
	UNION ALL
	SELECT funcionarios.id, funcionarios.nome, funcionarios.gerente
	FROM funcionarios
	JOIN vw_func ON vw_func.id = funcionarios.gerente
);

SELECT id,nome, gerente
FROM vw_func;