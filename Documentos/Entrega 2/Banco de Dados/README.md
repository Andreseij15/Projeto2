# Modelagem Física do Banco de Dados

Este diretório contém a modelagem física do sistema de gestão escolar e jogos.

## Tabelas Criadas

### 1. Escola
Armazena os dados institucionais das escolas parceiras.
- **Campos:** Nome, Email, CNPJ e ID (PK).

### 2. Estudante
Contém o registro dos alunos vinculados às escolas.
- **Campos:** RA (PK), Senha, Nome, Idade, Série e ID_Escola (FK).

### 3. Pacotes
Gerencia os tipos de assinatura e limites de acesso por escola.
- **Campos:** ID_Pacote (PK), Tipo, Limite, Jogos e ID_Escola (FK).

### 4. Jogos
Catálogo de jogos disponíveis na plataforma.
- **Campos:** ID_Jogo (PK), Nome, Descrição e Faixa Etária.

### 5. Acesso Jogos Aluno
Tabela de junção que registra quais alunos têm acesso a quais jogos.

## Script SQL
/* Modelo Físico Final Corrigido */

CREATE TABLE escola (
    Nome_escola VARCHAR(100),
    Email_Institucional VARCHAR(100),
    CNPJ NUMERIC,
    ID_Escola NUMERIC PRIMARY KEY
);

CREATE TABLE estudante (
    RA NUMERIC PRIMARY KEY,
    Senha NUMERIC,
    Periodo_escolar VARCHAR(50),
    Serie NUMERIC,
    Idadde NUMERIC,
    Nome VARCHAR(100),
    ID_Escola NUMERIC
);

CREATE TABLE pacotes (
    Tipo_Assinatura VARCHAR(50),
    Limite_Acessos NUMERIC,
    Jogos VARCHAR(100),
    IP_Valido NUMERIC,
    ID_pacote NUMERIC PRIMARY KEY,
    ID_Escola NUMERIC
);

CREATE TABLE jogos (
    Tipo_Jogo VARCHAR(50),
    Nome VARCHAR(100), -- Corrigido para VARCHAR
    Descricao VARCHAR(255),
    Faixa_Etaria NUMERIC,
    Modo_Offline VARCHAR(20),
    ID_Jogo NUMERIC PRIMARY KEY
);

CREATE TABLE acesso_jogos_aluno (
    ID_Escola NUMERIC,
    ID_Jogos NUMERIC,
    RA NUMERIC
);

/* Resolvendo os relacionamentos (FKs) */

-- Liga o estudante à escola
ALTER TABLE estudante ADD CONSTRAINT FK_estudante_escola
    FOREIGN KEY (ID_Escola)
    REFERENCES escola (ID_Escola);

-- Liga o pacote à escola
ALTER TABLE pacotes ADD CONSTRAINT FK_pacotes_escola
    FOREIGN KEY (ID_Escola)
    REFERENCES escola (ID_Escola);

-- Liga a tabela de acesso aos Jogos, Estudantes e Escola
ALTER TABLE acesso_jogos_aluno ADD CONSTRAINT FK_acesso_aluno
    FOREIGN KEY (RA) REFERENCES estudante (RA);

ALTER TABLE acesso_jogos_aluno ADD CONSTRAINT FK_acesso_jogo
    FOREIGN KEY (ID_Jogos) REFERENCES jogos (ID_Jogo);

ALTER TABLE acesso_jogos_aluno ADD CONSTRAINT FK_acesso_escola
    FOREIGN KEY (ID_Escola) REFERENCES escola (ID_Escola);

