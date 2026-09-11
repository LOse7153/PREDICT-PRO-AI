# PREDICT PRO AI — Android + IA TIPSTER (mode réel)

Cette version mobile est conçue pour travailler avec des **données de football réellement récupérées** auprès de football-data.org v4.

## Ce qui est réel
- Les matchs sont récupérés depuis l'API 1xbet 
- Les scores et statuts LIVE viennent de l'API lorsqu'ils sont disponibles.
- Les historiques des équipes sont récupérés depuis l'API.
- Les probabilités sont recalculées pour chaque match.
- Aucun score d'exemple n'est utilisé comme prédiction réelle.
- Le moteur combine Poisson/Dixon-Coles, forme, Elo, Monte-Carlo et github 
- TIPSTER transforme les probabilités en 1X, X2, 1, 2, score exact ou PASS.
- Si la clé OpenAI est configurée, IA TIPSTER effectue une seconde lecture des candidats à partir des données calculées.

## Limite importante
Le mot « réel » signifie que l'application ne fabrique pas les matchs et travaille sur les données reçues du fournisseur. La couverture dépend du plan football-data.org : l'application ne peut pas afficher les compétitions que le fournisseur ne donne pas à ton compte. L'API est aussi limitée en nombre de requêtes selon le plan.

## Connexion aux données
Au premier lancement, entre ton token `football-data.org` dans l'application. Il est stocké dans le stockage sécurisé Android.

## Activer IA TIPSTER
Dans l'application, appuie sur l'icône ✨ et entre une clé API OpenAI. La clé est stockée localement pour cette version personnelle.

IA TIPSTER reçoit uniquement les candidats et les statistiques calculées par PREDICT PRO AI. Elle doit répondre avec une sélection parmi `1`, `X2`, `1X`, `2`, `score exact` ou `PASS` et une courte justification. Elle n'est pas autorisée à inventer des cotes, blessures ou actualités.

Pour une application publique, ne distribue pas une clé OpenAI dans l'APK : mets l'appel OpenAI derrière un backend sécurisé.

## Préparer avec Flutter

```bash
flutter create .
flutter pub get
```

## Tester

```bash
flutter run
```

## Construire l'APK

```bash
flutter build apk --release
```

APK : `build/app/outputs/flutter-apk/app-release.apk`

## Google Play
Pour une publication Google Play, utilise plutôt :

```bash
flutter build appbundle --release
```

Une vraie version publique doit aussi être signée correctement.

## GitHub Actions
Le projet contient `.github/workflows/android.yml` afin de compiler l'APK automatiquement sur GitHub Actions. Le téléphone peut donc servir à gérer le projet et récupérer l'APK sans installer Android Studio.

## Avertissement TIPSTER
Les probabilités et sélections sont statistiques. Elles ne garantissent jamais un résultat ni un gain.


## Branche d’analyse par mi-temps
- **Match** : analyse globale 1X2, buts attendus et scores probables.
- **1ère mi-temps** : probabilités 1/X/2 et scores de mi-temps à partir des scores `halfTime` de l’historique.
- **2ème mi-temps** : estimation séparée des buts de seconde période ; en LIVE, le calcul tient compte du score déjà acquis et du temps restant lorsque les données sont disponibles.
- Les analyses restent probabilistes et ne garantissent aucun résultat.

## Nouvelles branches d'analyse
- 🟨 Cartons jaunes : moyenne historique et estimation LIVE.
- 🚩 Corners : moyenne historique et estimation LIVE.
- 🎯 Tirs cadrés : moyenne historique et estimation LIVE.
- Les statistiques sont alimentées par les statistiques disponibles dans football-data.org; la couverture dépend du match et du plan API.
