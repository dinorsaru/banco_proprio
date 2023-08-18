-- Crie o banco de dados
CREATE DATABASE banco_logico;

-- Use o banco de dados criado
USE banco_logico;

-- Tabela Cliente
CREATE TABLE Cliente (
    cliente_id INT PRIMARY KEY,
    nome VARCHAR(255),
    telefone VARCHAR(20)
);

-- Tabela Veiculo
CREATE TABLE Veiculo (
    veiculo_id INT PRIMARY KEY,
    cliente_id INT,
    marca VARCHAR(50),
    modelo VARCHAR(50),
    FOREIGN KEY (cliente_id) REFERENCES Cliente(cliente_id)
);

-- Tabela Servico
CREATE TABLE Servico (
    servico_id INT PRIMARY KEY,
    descricao VARCHAR(255),
    preco DECIMAL(10, 2)
);

-- Tabela Atendimento
CREATE TABLE Atendimento (
    atendimento_id INT PRIMARY KEY,
    veiculo_id INT,
    servico_id INT,
    data_atendimento DATE,
    FOREIGN KEY (veiculo_id) REFERENCES Veiculo(veiculo_id),
    FOREIGN KEY (servico_id) REFERENCES Servico(servico_id)
);

-- Tabela Peça
CREATE TABLE Peça (
    peca_id INT PRIMARY KEY,
    descricao VARCHAR(255),
    preco_unitario DECIMAL(10, 2)
);

-- Tabela ItemAtendimento
CREATE TABLE ItemAtendimento (
    item_id INT PRIMARY KEY,
    atendimento_id INT,
    peca_id INT,
    quantidade INT,
    FOREIGN KEY (atendimento_id) REFERENCES Atendimento(atendimento_id),
    FOREIGN KEY (peca_id) REFERENCES Peça(peca_id)
);

-- Recupere todos os clientes
SELECT * FROM Cliente;

-- Recupere todos os veículos de um cliente específico
SELECT * FROM Veiculo WHERE cliente_id = 1;

-- Calcule o valor total de cada atendimento, incluindo serviços e peças
SELECT a.atendimento_id, 
       SUM(s.preco + (i.quantidade * p.preco_unitario)) AS valor_total
FROM Atendimento a
LEFT JOIN Servico s ON a.servico_id = s.servico_id
LEFT JOIN ItemAtendimento i ON a.atendimento_id = i.atendimento_id
LEFT JOIN Peça p ON i.peca_id = p.peca_id
GROUP BY a.atendimento_id;

-- Recupere os atendimentos ordenados por data
SELECT * FROM Atendimento ORDER BY data_atendimento DESC;

-- Recupere os serviços mais caros
SELECT * FROM Servico ORDER BY preco DESC LIMIT 5;

-- Recupere os clientes que fizeram mais de 3 atendimentos
SELECT c.nome, COUNT(a.atendimento_id) AS num_atendimentos
FROM Cliente c
LEFT JOIN Veiculo v ON c.cliente_id = v.cliente_id
LEFT JOIN Atendimento a ON v.veiculo_id = a.veiculo_id
GROUP BY c.nome
HAVING COUNT(a.atendimento_id) > 3;

-- Recupere os veículos e os serviços realizados para cada atendimento
SELECT v.marca, v.modelo, s.descricao
FROM Veiculo v
INNER JOIN Atendimento a ON v.veiculo_id = a.veiculo_id
INNER JOIN Servico s ON a.servico_id = s.servico_id;
