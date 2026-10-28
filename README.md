# Projet convertisseur de devises - Vue.js

Application de conversion de devises développée dans le cadre d'un Travaux Pratiques (TP) avec Vue 3 (Composition API) et Vite.

## Instructions d'installation et d'exécution
1. Installer les dépendances du projet :
   npm install

2 . Lancer le serveur local :
   npm run dev

3. Ouvrir le projet :
   Cliquer sur le lien http://localhost:5173 dans le terminal pour voir le projet dans le navigateur.

# Scripts
- `npm run dev` : serveur de développement
- `npm run build` : version de production 

## Fonctionnalités

- Saisie par clavier numérique virtuel
- Sélection des devises : Deux listes déroulantes (`<select>`) avec `v-model` et `v-for`.
- Conversion en temps réel & manuelle :
  - Utilisation d'un taux pivot (Euro EUR).
  - Conversion automatique dès la modification de la saisie ou des devises.
- Bouton **CONVERTIR** pour relancer ou vérifier le calcul.
- Inversion des devises : Bouton ⇄ pour échanger rapidement la devise source et la devise cible.
- Gestion des erreurs : Message d'avertissement si le montant est égal à 0 ou vide.

## Captures d'écran
   Les captures d'écran des 4 cas de test sont disponibles dans le dossier screenshots du dépôt.
## Auteur
Salem Nour Elhouda _ L2 DSI2 / G2 

