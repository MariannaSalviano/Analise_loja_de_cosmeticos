# Analise_loja_de_cosmeticos

# Projeto Loja de Cosméticos -- Estrutura SQL

``` sql
CREATE SCHEMA projeto_loja_cosmeticos;

USE projeto_loja_cosmeticos;

CREATE TABLE produtos (
    id_produto INT NOT NULL AUTO_INCREMENT,
    nome_produto VARCHAR(150) NOT NULL,
    categoria VARCHAR(100) NOT NULL,
    marca VARCHAR(100) NOT NULL,
    preco_unitario DECIMAL(10,2) NOT NULL,
    data_cadastro DATE NOT NULL,
    PRIMARY KEY (id_produto)
);

CREATE TABLE estoque (
    id_estoque INT NOT NULL AUTO_INCREMENT,
    id_produto INT NOT NULL,
    quantidade_disponivel INT NOT NULL,
    data_atualizacao DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (id_estoque),
    FOREIGN KEY (id_produto) REFERENCES produtos(id_produto)
);

CREATE TABLE vendedores (
    id_vendedor INT NOT NULL AUTO_INCREMENT,
    nome_vendedor VARCHAR(150) NOT NULL,
    data_contratacao DATE NOT NULL,
    ativo TINYINT(1) NOT NULL DEFAULT 1,
    PRIMARY KEY (id_vendedor)
);

CREATE TABLE vendas (
    id_venda INT NOT NULL AUTO_INCREMENT,
    id_produto INT NOT NULL,
    id_vendedor INT NOT NULL,
    quantidade INT NOT NULL,
    valor_unitario DECIMAL(10,2) NOT NULL,
    valor_total DECIMAL(10,2) NOT NULL,
    data_venda DATE NOT NULL,
    PRIMARY KEY (id_venda)
);

ALTER TABLE estoque 
ADD CONSTRAINT CE_estoque_produtos
FOREIGN KEY (id_produto)
REFERENCES produtos(id_produto)
ON DELETE NO ACTION
ON UPDATE NO ACTION;
```
