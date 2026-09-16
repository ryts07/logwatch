# docs/CARTE.md -- gabarit de départ, amendé à l'étape 4

# Carte LogWatch v0 - v1 du AAAA-MM-JJ (étape 1)

## Entrées et sorties

lit : ... (et qui décide du chemin : l'option, .env, ou la valeur par
défaut)
écrit : ...
supprime : ...

## Les fonctions, dans l'ordre du fichier

Les quatorze lignes se generent, depuis logwatch/ :
Select-String -Path logwatch.py -Pattern '^def ' |
ForEach-Object { "| " + $\_.Line.Substring(4).TrimEnd(':') + " | |" }
Coller le resultat sous l'en-tete, puis remplir la seule colonne rend.
| fonction | rend
|
|-----------------------------------|---------------------------------------
--------|
| charger_env(chemin=".env") | à préciser
|
| parser_ligne(ligne) | un dictionnaire à onze clés, ou None
si la ligne n'a pas la forme attendue |
| ... |
|

## Les détections annoncées par le README (question 7)

| détection | fonction | ce que le README lui demande (seuil, unité, « dès
que » / « au moins » / « au-delà ») |
|-----------|----------|----------------------------------------------------
--------------------------------|
| ## Les détections annoncées par le README (question 7)
| détection | fonction | ce que le README lui demande (seuil, unité, « dès que » / « au moins » / « au-delà ») |
|-----------|----------|--------------------------------------------------------------------------------|
| D1 | d1_somme_par_ip | Compte toutes les requêtes par IP (unité : nombre de requêtes), la somme de toutes les IP devant égaler `total_lines`. |
| D2 | d2_brute_force | Signale une IP dès que son nombre d'échecs (POST sur `url_login` avec 401/403) atteint `seuil_brute_force` (unité : nombre d'échecs). |
| D3 | d3_scan_port_ou_path | Signale une IP qui demande au moins `seuil_scan` URL distinctes typiques d'un scanner (unité : nombre d'URL distinctes). |
| D4 | d4_pic_trafic | Alerte dès qu'une fenêtre de `fenetre_minutes` minutes dépasse `seuil_pic` requêtes (unité : requêtes par fenêtre). |
| D5 | d5_erreurs_5xx | Alerte au-delà de `seuil_5xx` pour la part de réponses 5xx sur l'ensemble des requêtes (unité : pourcentage %). |
| D6 | purger_anciens_rapports | Supprime tout rapport plus vieux que `retention_jours` jours (unité : jours). |
|

## Points opaques (question 8)

- ligne 42 : que vaut `requete_parsee` quand la regex échoue et comment est géré l'élément `None` dans les boucles suivantes ?
- ligne 85 : que renvoie exactement `d4_pic_trafic` quand `fenetre_minutes` n'est pas un diviseur exact de 60 ?
- ligne 112 : que contient le dictionnaire de retour de `d5_erreurs_5xx` quand il n'y a aucune requête lue (division par zéro) ?
