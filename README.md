# Scripts de criação de tabelas
Scripts das tabelas criadas no desafio " Criando um gerenciador de espaçonaves do star wars com SQL Server + .NET"

## Comando para indicar a tabela a ser utilizada:

USE EstrelaDaMorte

## Comando para criação da tabela Planetas:

CREATE TABLE Planetas(

	IdPlaneta int NOT NULL,
	Nome varchar(50) NOT NULL,
	Rotacao float NOT NULL,
	Orbita float NOT NULL,
	Diametro float NOT NULL,
	Clima varchar(50) NOT NULL,
	Populacao int NOT NULL
)

GO

### Comando para alterar a tabela Planetas adicionando uma chave primária:

ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta);

GO

## Comando para criar tabela de naves:

CREATE TABLE Naves(

	IdNave int NOT NULL,
	Nome varchar(100) NOT NULL,
	Modelo varchar(150) NOT NULL,
	Passageiros int NOT NULL,
	Carga float NOT NULL,
	Classe varchar(100) NOT NULL,
)

GO

### Comando para alterar a tabela Naves adicionando uma chave primária:

ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave);

GO

## Comando para criação da tabela Pilotos 

CREATE TABLE Pilotos(

	IdPiloto int NOT NULL,
	Nome varchar(200) NOT NULL,
	AnoNascimento varchar(10) NOT NULL,
	IdPlaneta int NOT NULL,
)

GO

### Comandos para criação de chave primária e de chave estrangeira


ALTER TABLE Pilotos ADD CONSTRAINT PK_Pilotos PRIMARY KEY (IdPiloto);

GO

ALTER TABLE Pilotos  ADD  CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY(IdPlaneta) 
REFERENCES Planetas (IdPlaneta)

GO

ALTER TABLE Pilotos CHECK CONSTRAINT FK_Pilotos_Planetas

GO

## Comando para criação da tabela PilotosNaves

CREATE TABLE PilotosNaves(

	IdPiloto int NOT NULL,
	IdNave int NOT NULL,
	FlagAutorizado bit NOT NULL,)
	
	GO

### Comandos para criação de chave primária e de chave estrangeira

ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave);

GO

ALTER TABLE PilotosNaves  ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY(IdPiloto)
REFERENCES Pilotos (IdPiloto)

GO

ALTER TABLE PilotosNaves  ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY(IdNave)
REFERENCES Naves (IdNave)

GO

ALTER TABLE PilotosNaves  ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado  DEFAULT (1) FOR FlagAutorizado

GO

## Comando para criação da tabela HistoricoViagens

CREATE TABLE HistoricoViagens(

	IdNave int NOT NULL,
	IdPiloto int NOT NULL,
	DtSaida datetime NOT NULL,
	DtChegada datetime NULL
)

GO


### Comando para criação de chave estrangeira

ALTER TABLE HistoricoViagens  ADD  CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY(IdPiloto, IdNave)
REFERENCES PilotosNaves (IdPiloto, IdNave)

GO

ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves

GO

## Comandos para a seleção do conteúdo integral das tabelas criadas, respectivamente:

select * from Planetas

select * from Naves

select * from Pilotos

Select * from PilotosNaves

select * from HistoricoViagens

