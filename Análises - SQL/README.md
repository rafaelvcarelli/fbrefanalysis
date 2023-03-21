## Queries para gerar análises - SQL

### A tabela utilizada para as análises será a fbrefPassing, referente aos passes dos jogadores.

Uma das primeiras perguntas que podemos fazer para os dados dessa tabela é sobre a média de passes dos jogadores.

    SELECT AVG(atttotal) FROM FBREFPASSING F; (para a quantidade de passes tentados)

|avg|
|---|
|462.5213333333333333|

    SELECT AVG(cmptotal) FROM FBREFPASSING F; (para a quantidade de passes completos)

|avg|
|---|
|366.0133333333333333|

Utilizando subqueries, filtramos os jogadores que estão acima da média, tanto na quantidade de tentativas de passe quanto de passes completos.

Por questões de visualização, criamos uma tabela temporária para visualizar os dados de forma mais concisa, apenas com as colunas de nome, posição, total de tentativas e total de passes.

    CREATE VIEW aboveavgpassing AS 
    SELECT
        "Player▲" ,POS , CMPTOTAL, ATTTOTAL
    FROM FBREFPASSING F
------------------------------------

    SELECT * FROM ABOVEAVGPASSING
             WHERE ATTTOTAL > (SELECT AVG(ATTTOTAL) FROM ABOVEAVGPASSING F3)
             AND CMPTOTAL > (SELECT AVG(CMPTOTAL) FROM ABOVEAVGPASSING F2)
    ORDER BY ATTTOTAL DESC

|Player▲|pos|cmptotal|atttotal|
|-------|---|--------|--------|
|André|MF|2268|2458|
|Júnior Alonso|DF|1872|2141|
|Allan|MF|1772|2081|
|Ganso|MF/FW|1816|2076|
|Rafinha|DF|1819|2069|
|Marcos Rocha|DF|1645|2045|
|Kevin|DF|1445|1951|
|Samuel Xavier|DF|1642|1948|
|Jhon Arias|FW/MF|1535|1850|
|Marlon Freitas|MF|1563|1848|
|Renê|DF|1481|1795|
|Juninho Capixaba|DF|1254|1774|
|Carlos de Pena|MF/FW|1272|1735|
|Fabricio Bustos|DF|1340|1708|
|Rodrigo Alves Soares|DF|1360|1683|
|Manoel|DF|1508|1677|
|Luciano Castán|DF|1371|1631|
|Ayrton Lucas|DF|1322|1626|
|Murilo Cerqueira|DF|1463|1624|
|Nino|DF|1442|1595|
|Léo Pelé|DF|1386|1591|
|Aderlan Silva|DF|1150|1583|
|Raul|MF|1323|1557|
|Raniele|MF/DF|1194|1543|
|Eduardo Gabriel|DF|1329|1538|

