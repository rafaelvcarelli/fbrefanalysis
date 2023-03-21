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

Por questões de visualização, criamos uma tabela temporária para visualizar os dados de forma mais concisa, apenas com as colunas de nome, posição, clube, total de tentativas e total de passes. Para fazer sentido com o jogo, os goleiros e defensores foram excluídos da visualização.

    CREATE VIEW aboveavgpa AS
    
    SELECT
    
    "Player▲" ,POS , squad, CMPTOTAL, ATTTOTAL
    
    FROM FBREFPASSING F

-----------------------------------------
    SELECT * FROM ABOVEAVGPAS
    
    WHERE ATTTOTAL > (SELECT AVG(ATTTOTAL) FROM ABOVEAVGPAS F3)
    
    AND CMPTOTAL > (SELECT AVG(CMPTOTAL) FROM ABOVEAVGPAS F2)
    
    AND NOT POS = 'GK'
    
    ORDER BY ATTTOTAL DESC
    
    LIMIT 25

|Player▲|pos|cmptotal|squad|atttotal|
|-------|---|--------|-----|--------|
|André|MF|2268|Fluminense|2458|
|Júnior Alonso|DF|1872|Atlético Mineiro|2141|
|Allan|MF|1772|Atlético Mineiro|2081|
|Ganso|MF/FW|1816|Fluminense|2076|
|Rafinha|DF|1819|São Paulo|2069|
|Marcos Rocha|DF|1645|Palmeiras|2045|
|Kevin|DF|1445|Avaí|1951|
|Samuel Xavier|DF|1642|Fluminense|1948|
|Jhon Arias|FW/MF|1535|Fluminense|1850|
|Marlon Freitas|MF|1563|Atl Goianiense|1848|
|Renê|DF|1481|Internacional|1795|
|Juninho Capixaba|DF|1254|Fortaleza|1774|
|Carlos de Pena|MF/FW|1272|Internacional|1735|
|Fabricio Bustos|DF|1340|Internacional|1708|
|Rodrigo Alves Soares|DF|1360|Juventude|1683|
|Manoel|DF|1508|Fluminense|1677|
|Luciano Castán|DF|1371|Coritiba|1631|
|Ayrton Lucas|DF|1322|Flamengo|1626|
|Murilo Cerqueira|DF|1463|Palmeiras|1624|
|Nino|DF|1442|Fluminense|1595|
|Léo Pelé|DF|1386|São Paulo|1591|
|Aderlan Silva|DF|1150|Bragantino|1583|
|Raul|MF|1323|Bragantino|1557|
|Raniele|MF/DF|1194|Avaí|1543|
|Eduardo Gabriel|DF|1329|Santos|1538|

Mais a frente, é preciso entender qual o tipo de passe os jogadores executam. Logo, criando outra visualização, vamos analisar os jogadores que mais tentam passes longos no campeonato.

   

    CREATE VIEW aboveavglong AS
    SELECT
      "Player▲",
      SQUAD ,
      POS ,
      ATTLONG
    FROM FBREFPASSING F

________

    SELECT * FROM ABOVEAVGLONG
    
    WHERE ATTLONG > (SELECT AVG(ATTLONG) FROM ABOVEAVGLONG F3)
    
    AND NOT POS = 'DF'
    
    AND NOT POS = 'GK'
    
    ORDER BY attlong DESC
    
    LIMIT 25

|Player▲|squad|pos|attlong|
|-------|-----|---|-------|
|Gustavo Scarpa|Palmeiras|MF/FW|455|
|Marlon Freitas|Atl Goianiense|MF|382|
|Allan|Atlético Mineiro|MF|331|
|Carlos de Pena|Internacional|MF/FW|288|
|Vinícius|Ceará|FW/MF|284|
|Raul|Bragantino|MF|272|
|Raniele|Avaí|MF/DF|265|
|Jadson|Juventude|MF|234|
|Chico|Juventude|MF/FW|231|
|Reinaldo|São Paulo|DF/FW|229|
|Wellington Rato|Atl Goianiense|FW/MF|228|
|Rafael Gava|Cuiabá|MF|226|
|Danilo|Palmeiras|MF|216|
|João Lucas|Cuiabá|DF/MF|212|
|João Pedro Pepê|Cuiabá|MF|207|
|Rodrigo Fernández|Santos|MF|194|
|Pablo Maia|São Paulo|MF|185|
|Ignacio Fernández|Atlético Mineiro|MF|184|
|André|Fluminense|MF|180|
|Dieguinho|Goiás|MF/DF|178|
|Giorgian De Arrascaeta|Flamengo|MF|172|
|Artur|Bragantino|FW/MF|168|
|David Terans|Atl Paranaense|MF|168|
|José Welison|Fortaleza|MF|164|
|Jesús Trindade|Coritiba|MF|159|

