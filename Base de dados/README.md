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

