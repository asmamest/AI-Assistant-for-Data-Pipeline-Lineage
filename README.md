# AI Assistant for Data Lineage Graph

Ce projet construit un **graphe de lignée de données** à partir du jeu de données public [DataAssetGraphData](https://github.com/csuvis/DataAssetGraphData) puis entraîne un **assistant conversationnel** (LLM) capable de répondre à des questions sur la structure et les relations du graphe.  
L’entraînement utilise les techniques **LoRA** et **QLoRA** via la bibliothèque `unsloth` pour une adaptation efficace en mémoire.

## 📊 Jeu de données

- Source : [DataAssetGraphData](https://github.com/csuvis/DataAssetGraphData) (fichiers `Node.rar` et `Edge.rar`)
- Contenu :
  - **18 fichiers JSON** de nœuds (ex: `DLG1-node.json`, …) contenant des assets de type `Data Field`, `Data Table` ou `Data Job`.
  - **18 fichiers JSON** d’arêtes (ex: `DLG1-edge.json`, …) décrivant les relations (`PARENT_CHILD` ou `DATA_FLOW`).
- Taille : environ **58 320 nœuds** et **60 222 arêtes** après fusion, formant un graphe cohérent de **39 508 nœuds** et **40 726 arêtes** après filtrage.

## 🎯 Objectifs

1. **Charger et fusionner** toutes les données dans un graphe unique avec `networkx`.
2. **Analyser** le graphe : distribution des types, degrés, détection d’anomalies, nœuds centraux.
3. **Générer automatiquement** un jeu de données de questions/réponses (Q/R) à partir du graphe (type, degré, voisins, informations).
4. **Fine‑tuner** un petit modèle de langage (Llama 3.2 3B) avec **QLoRA** pour qu’il réponde naturellement aux interrogations sur le graphe.
5. **Interroger** l’assistant sur le graphe de lignée.

## 🛠️ Méthodes utilisées

| Technique | Rôle |
|-----------|------|
| **LoRA** (Low‑Rank Adaptation) | Ajoute des matrices de faible rang aux couches d’attention, réduisant drastiquement le nombre de paramètres entraînables. |
| **QLoRA** | Combinaison de LoRA avec une quantification 4 bits du modèle de base, permettant de fine‑tuner des modèmes de plusieurs milliards de paramètres sur un seul GPU grand public. |
| **Unsloth** | Implémentation optimisée de LoRA/QLoRA, plus rapide et moins gourmande en mémoire. |
| **SFTTrainer** (TRL) | Entraînement supervisé sur des paires instruction/réponse. |

## 📁 Structure du projet
