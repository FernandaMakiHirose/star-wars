# Modelando um banco de dados na prática com SQL SERVER
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

Também crie a tabela Naves:
![tabela](https://user-images.githubusercontent.com/72028645/132556976-0c8ab6cd-1747-4532-9d2f-63461da035c8.png)
