# Sélection des capteurs : résumé pour l'équipe modélisation

## Capteurs à exclure (7) : aucune information utile
S_1, S_5, S_6, S_10, S_16, S_18, S_19

Confirmé par deux méthodes indépendantes : ratio pente/bruit ≈ 0, et test de Mann-Kendall ("no trend", p-value = 1.0).

## Capteurs à garder (14)
S_2, S_3, S_4, S_7, S_8, S_9, S_11, S_12, S_13, S_14, S_15, S_17, S_20, S_21

Tous montrent une tendance significative (Mann-Kendall, p-value ≈ 0), avec une force de signal homogène (ratio pente/bruit entre 0.011 et 0.014), aucun capteur ne domine nettement les autres.

## Direction de la tendance (utile pour le feature engineering)

**Augmentent avec la dégradation** : S_2, S_3, S_4, S_8, S_11, S_13, S_15, S_17
**Diminuent avec la dégradation** : S_7, S_9, S_12, S_14, S_20, S_21

## Détails complets
Voir `notebooks/01_eda.ipynb` pour le détail des calculs et graphiques.