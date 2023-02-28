# ExamBlancBDD

> Ajouter un nouveau joueur dans la base de données

```sql
INSERT INTO player (lastname, firstname, elo) VALUES ('NIVEAU', 'Mathis', 1500); 
```

> Inscrire un joueur à un tournois

```sql
INSERT INTO tj_player_tournament (playerid, tournamentid) VALUES (20, 1);
```

> Générer les rondes pour le tournois 1

```sql

```

> Entrer le score d'une partie

```sql
UPDATE game SET blackscore = 0 WHERE id = 1;
```

> Obtenir le podium du tournoi 23 (les 3 premiers joueurs) 

```sql

```

> Lister tous les maîtres internationaux

```sql
SELECT player.lastname, player.firstname, player.elo
From player
WHERE player.elo > 2400;
```


> Connaître le nombre de points marqués par un joueur par année.
 On commence par créer une colonne whitescore dans la table game
```sql
ALTER TABLE game
ADD whitescore numeric(2,1)
```

```sql
UPDATE game
SET whitescore = 1- blackscore;
```
Puis on peut faire la requête

```sql
SELECT player.lastname, player.firstname, EXTRACT(YEAR FROM game.date) AS year, SUM(game.blackscore = 1 OR game.blackscore = 0 OR game.blackscore = 0.5) AS points
FROM player
INNER JOIN game ON game.blackplayerid = player.playerid OR game.whiteplayerid = player.playerid
WHERE player.playerid = 1
GROUP BY player.playerid, year
ORDER BY year;
```

> Obtenir le nombre de coups moyen nécessaire pour gagner
```sql

```

> Lister les parties où le joueur a commencé par jouer un cavalier

```sql
SELECT game.gameid, count(move.move)(*) as nb_move, game.playerid
FROM game
INNER JOIN move ON move.gameid = game.gameid
WHERE move.index = 1 AND move.move = 'Nf3';
```
