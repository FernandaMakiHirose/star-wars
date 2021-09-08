# Modelando um banco de dados na prática com SQL SERVER
1) Criar tabelas

No `Microsoft SQL Server Management Studio` crie a tabela Planetas:
```
CREATE TABLE Planetas(
	IdPlaneta int NOT NULL,
	Nome VARCHAR(50) NOT NULL,
	Rotacao float NOT NULL,
	Orbita float NOT NULL,
	Diametro float NOT NULL,
	Clima VARCHAR(50) NOT NULL,
	Populacao int NOT NULL,
)
GO 
ALTER TABLE Planetas ADD CONSTRAINT Pk_Planetas PRIMARY KEY (IdPlaneta);
```
Cria uma tabela e adicione uma chave primária, o id que não pode se repetir.

Crie a tabela Naves (jeito 2 de criar uma tabela): 

![tabela](https://user-images.githubusercontent.com/72028645/132556976-0c8ab6cd-1747-4532-9d2f-63461da035c8.png)

Crie a tabela Pilotos:
```
CREATE TABLE Pilotos(
	IdPiloto int NOT NULL,
	 Nome varchar(200) NOT NULL,
	 AnoNascimento varchar(10) NOT NULL,
	 IdPlaneta int NOT NULL,
)
GO 
ALTER TABLE Pilotos ADD CONSTRAINT Pk_Pilotos PRIMARY KEY (IdPiloto);
GO
ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY (IdPlaneta)
REFERENCES Planetas (IdPlaneta)
```

Crie a tabela PilotosNaves:
```
CREATE TABLE PilotosNaves(
	IdPiloto int NOT NULL,
	IdNave int NOT NULL,
	FlagAutorizado bit NOT NULL,
)
GO 
ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave);
GO 
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY(IdPiloto)
REFERENCES Pilotos (IdPiloto)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY(IdNave)
REFERENCES Naves (IdNave)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado
```

E por fim crie a tabela HistoricoViagens:
```
CREATE TABLE HistoricoViagens(
	IdNave int NOT NULL,
	IdPiloto int NOT NULL,
	DtSaida datetime NOT NULL,
	DtChegada datetime NULL,
)
GO 

ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY(IdPiloto, IdNave)
REFERENCES PilotosNaves (IdPiloto, IdNave)
GO
ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves
```

2) Após clonar o projeto, no arquivo `DaoBase.cs` existe o código:
```
con = new SqlConnection(@"Data Source=MAKI\MSSQLSERVER02;Initial Catalog=EstrelaDaMorte;Integrated Security=True;Connect Timeout=30");
```
Substitua o `MAKI\MSSQLSERVER02` pelo path do seu banco de dados
