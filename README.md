# Modelando um banco de dados na prática com SQL SERVER
Gerenciador de espaço naves do Star Wars modelando um banco de dados em SQL Server. A missão foi entregar os scripts de criação das tabelas que compõem a estrutura desse banco de dados. 

## Requisitos
- Microsoft SQL Server Management Studio
- Visual Studio

## Licença
Distribuido sob a licença MIT License. Veja `LICENSE` para mais informações.

## Guia
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

3) Abra o projeto no Visual Studio clicando duas vezes no arquivo `ControleAcessoEstrelaDaMorte.sln`. Para executar o projeto clique no botão de executar o arquivo `Program.cs`.

## Quiz
### Qual desses é o comando utilizado para a consulta da base da API?
select * from Tabela

### Para filtrar o conteúdo selecionado de uma API utilizamos o comando:
where

### São consideradas boas práticas para a criação de tabelas:
Criação de tabelas no plural, nomes claros e objetivos

### O tipo de dado 'bit' representa:
um valor booleano

### Sobre chaves estrangeiras, é correto afirmar:
É uma referência em uma tabela a uma chave primária de outra tabela

### Um banco de dados relacional pressupõe:
Que as tabelas se relacionam para gerar o controle dos dados

### Qual o objetivo de obter um diagrama de banco de dados?
Identificar mais facilmente como funciona o sistema, assim como a tabela principal (core) do sistema

### Sobre a sintaxe do comando DELETE, qual alternativa está correta?
DELETE [tabela.*] FROM tabela WHERE critério

### Sobre chaves primárias, é correto afirmar:
Ela não pode ser duplicada
