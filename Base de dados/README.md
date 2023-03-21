# Base de dados

## Obtenção dos dados

O site **fbref.com** disponibiliza, em detalhes, estatísticas de várias temporadas do **Campeonato Brasileiro de Futebol Série A**, do Brasil. 

Na página de estatísticas da competição, foi possível fazer o download, em formato **.csv** de 9 dos 12 conjuntos de dados (listados abaixo).

Para o objetivo deste projeto, os dados da posição de goleiro não foram extraídos, focando apenas nos jogadores de linha.

Standard Stats
Goalkeeping
Advanced Goalkeeping
Shooting
Passing 
Pass Types
Goal and Shot Creation
Defensive Actions
Possession
Playing Time
Miscellaneous Stats

Com os arquivos .csv prontos, o próximo passo foi criar uma conexão entre o **DBeaver** e o **PostgreSQL**, para manejo da base de dados.

![IMG](https://i.ibb.co/yQS5Ypj/Captura-de-Tela-47.png)

Já no **DBeaver**, com a conexão feita com o **PostgreSQL**, a criação do schema **fbRefStats** com as 9 tabelas em .csv. 

![IMG](https://i.ibb.co/VwC2StL/Captura-de-Tela-48.png)

Com as tabelas devidamente importadas, observando os tipos das colunas, o próximo passo foi a limpeza dos dados dessas tabelas, com três etapas principais.

Com o comando **[DROP COLUMN](https://github.com/rafaelvcarelli/fbrefanalysis/blob/main/DROPCOLUMNS.sql)**, retirar as colunas **"rk"**,**** que se referiam ao ranking feito pelo site, **"Matches"** e **"-9999",** referências a links para o **fbref.com**

A renomeação das colunas das tabelas, para melhor entendimento. Como exemplo, usando o comando **[RENAME COLUMN](https://github.com/rafaelvcarelli/fbrefanalysis/blob/main/RENAMECOLUMNS.sql)**, renomeei as colunas da tabela **fbrefPossession**, referente aos dados sobre posse de bola. As outras 8 tabelas também foram atualizadas.

Por fim, na coluna **"pos"**, referente a posição dos atletas em campo, uma pequena alteração de nome com comando **UPDATE** para melhor compreensão.


### A tabela que será usada como exemplo nas visualizações é a fbrefPassing, relacionada aos passes dos jogadores.

    SELECT * FROM FBREFPASSING F LIMIT 5
|Player▲|nation|pos|squad|age|born|90s|cmptotal|atttotal|Cmp%Total|totdisttotal|prgdisttotal|cmpshort|attshort|Cmp%Short|cmpmedium|attmedium|Cmp%Medium|cmplong|attlong|Cmp%Long|assists|xag|xa|A-xAG|keypasses|final3rdpasses|penaltyareapasses|penaltyareacrosses|progressivepasses|
|-------|------|---|-----|---|----|---|--------|--------|---------|------------|------------|--------|--------|---------|---------|---------|----------|-------|-------|--------|-------|---|--|-----|---------|--------------|-----------------|------------------|-----------------|
|Abner|br BRA|DF|Atl Paranaense|21|2000|234|986|1283|769|17089|6919|469|533|880|412|517|797|91|181|503|2|22|17|-2|31|105|16|6|139|
|Adryelson|br BRA|DF|Botafogo (RJ)|23|1998|161|540|662|816|10461|4038|184|208|885|285|327|872|56|93|602|0|3|1|-3|3|15|0|0|20|
|Alesson|br BRA|MF/FW|Cuiabá|22|1999|114|192|278|691|2793|855|115|147|782|64|85|753|7|17|412|0|13|7|-13|15|10|9|3|29|
|Ale|br BRA|MF|América (MG)|31|1990|214|939|1110|846|16696|5100|422|485|870|386|428|902|106|135|785|2|15|14|5|21|125|15|3|144|
|Alisson|br BRA|MF/FW|São Paulo|28|1993|105|372|451|825|5456|1570|214|231|926|121|150|807|21|32|656|1|9|17|1|12|39|19|10|55|



## A próxima etapa do projeto é analisar os dados usando SQL
## [ANÁLISES ---------------->](https://github.com/rafaelvcarelli/fbrefanalysis/tree/main/An%C3%A1lises%20-%20SQL)
