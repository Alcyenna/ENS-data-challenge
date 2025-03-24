# ENS-data-challenge
My work for the ENS data challenge 2025 with Polytechnique 

Objectif du Challenge
Objectif : Utiliser des méthodes Online Machine Learning et de Collaborative Filtering (ou toute autre méthode) pour prédire, en fonction de l’historique de navigation :
Les 10 emplois que le candidat est le plus susceptible d’explorer ensuite.
La prochaine action du candidat. Cela peut être view ou apply.
Métriques d’Évaluation
Les métriques utilisées dans ce challenge pour classer les participants sont :

Mean Reciprocal Rank (MRR) : Mesure la moyenne des rangs réciproques de l’emploi correct parmi les 10 emplois prédits. Un MRR plus élevé indique que l’emploi correct est mieux classé dans les recommandations.
Accuracy : Évalue la capacité du modèle à prédire si la prochaine action du candidat sera une apply ou view, comme l’indique la variable “action”.
Le score final est une combinaison pondérée de ces deux métriques :

70% MRR
30% Précision sur la variable “action”
Exemples pour MRR
Si l’emploi correct est classé 1er, le rang réciproque est 1.0.
Si l’emploi correct est classé 2ème, le rang réciproque est 0.5.
Si l’emploi correct est classé 3ème, le rang réciproque est 0.333.
Si l’emploi correct n’est pas dans le top 10, le rang réciproque est 0.
Remarques
Les prédictions reposent sur la séquence des emplois consultés et postulés, sans utiliser de données spécifiques au profil telles que l’éducation ou les compétences.
Il est souligné que les intérêts des candidats peuvent évoluer pendant leur recherche, nécessitant des approches comme Online Machine Learning et les Non-Stationary Multi-Armed Bandits pour s’adapter dynamiquement.
Description des données
Le jeu de données fourni pour ce défi se compose de deux principaux éléments : les offres d’emploi et l’historique d’exploration des candidats. Le jeu de données est stocké au format CSV et est structuré comme suit :

Offres d’Emploi :
Job ID : Un identifiant unique pour chaque offre d’emploi.
Job Text : Un texte contenant la description de l’offre d’emploi. Ce texte est imparfait et contient des imperfections réalistes.
Historique d’Interaction des Candidats (X train/test) :
Session ID : Un identifiant unique pour chaque session de recherche d’emploi.
Job IDs : Une séquence d’identifiants d’offres d’emploi que le candidat a ouvertes durant la session, représentant son historique de navigation sur le site d’emploi.
Actions : L’action réalisée par le candidat pour l’offre correspondante. Elle peut être “view” (consulter) ou “apply” (postuler).
Offre Target (y train/test) :
Session ID : Un identifiant unique correspondant à chaque session.
Target Job ID : L’identifiant de l’offre suivante que le candidat consultera après avoir interagi avec les offres précédentes dans la séquence.
Action : L’action réalisée par le candidat sur l’offre d’emploi correspondante. Cela peut être view ou apply.
Le format de sortie pour les prédictions doit inclure :

Une liste de 10 offres possibles pour chaque session, classées par probabilité décroissante que le candidat les ouvre ensuite.
Une action indiquant si la prochaine action du candidat sera de postuler ou de consulter (view ou apply).
Chaque Session ID doit être associée à la liste des 10 offres prédites (par ordre de probabilité décroissante) ainsi qu’au booléen correspondant à applies_for.

Statistiques du Jeu de Données :
Le jeu de données contient environ 18K sessions de candidats pour les ensembles d’entraînement et de test.
Ces sessions impliquent environ 22K offres d’emploi uniques et 10K sessions de profils uniques.
Dans les ensembles d’entraînement et de test :

Certaines longues sessions de profils ont été divisées en plusieurs petites sessions sans chevauchement.
Il n’y aura aucun chevauchement entre les ensembles d’entraînement et de test (les sessions de profils dans l’ensemble d’entraînement ne seront jamais liées à celles de l’ensemble de test).
Remarques :
Il est important de prendre en compte les déséquilibres potentiels dans le jeu de données, où certains types d’offres peuvent être consultés plus fréquemment que d’autres, ce qui pourrait affecter les performances des modèles.
