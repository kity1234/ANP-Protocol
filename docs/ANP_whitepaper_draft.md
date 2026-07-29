# ANP — Artificial Network Protocol
### Un modèle en couches pour l'interopérabilité, le raisonnement distribué et la gouvernance de l'intelligence artificielle

**Statut du document :** Draft de travail (v0.1) — proposition ouverte à discussion et critique
**Auteur :** Serge Olivier KITT
**Date :** Juillet 2026
**Licence :** CC BY 4.0 — voir `LICENSE-DOCS`

---

## Résumé

L'écosystème actuel de l'intelligence artificielle se développe sans grammaire architecturale commune : chaque acteur (OpenAI, Google, Anthropic, communauté open source, laboratoires nationaux) construit ses propres protocoles d'interconnexion — MCP, A2A, formats propriétaires — sans cadre unificateur permettant de penser l'ensemble. Ce document propose **ANP (Artificial Network Protocol)**, un modèle conceptuel en couches inspiré du modèle OSI, mais fondamentalement adapté aux propriétés spécifiques de l'IA : la nature probabiliste des systèmes, le besoin de router par le *sens* plutôt que par l'adresse, et l'exigence d'une gouvernance éthique intégrée plutôt qu'ajoutée après coup.

ANP ne prétend pas résoudre tous les problèmes ouverts du domaine. Il propose une structure pour les nommer clairement, et identifie explicitement les zones qui relèvent encore de la recherche active plutôt que de l'ingénierie résolue.

---

## 1. Pourquoi un nouveau modèle ?

Le modèle OSI (1984) et TCP/IP ont permis l'interopérabilité d'internet en séparant les responsabilités en couches indépendantes, chacune ignorant le contenu des couches voisines. Ce principe — l'aveuglement au contenu — est ce qui a permis au réseau de transporter aussi bien un email qu'une vidéo sans jamais avoir à « comprendre » ce qu'il transportait.

L'IA rompt structurellement avec ce principe. Un système d'IA doit **comprendre le contenu** pour fonctionner : router une requête vers le bon modèle exige d'interpréter son sens, pas seulement de lire une adresse. ANP part de ce constat : ce n'est pas un modèle de *transport*, c'est un modèle de **cognition distribuée**. L'analogie avec OSI reste utile pédagogiquement, mais elle ne doit pas être forcée au-delà de sa pertinence réelle.

---

## 2. Architecture générale

ANP compte **six couches numérotées (0 à 5)** et **une couche transversale de gouvernance** qui les traverse toutes. Ce choix architectural — six couches plutôt qu'un nombre arbitrairement réduit — reflète la complexité réelle du problème plutôt qu'une simplification de façade.

| Couche | Nom | Rôle | Équivalent OSI le plus proche |
|---|---|---|---|
| 0 | Thermodynamique & Énergétique | Budget de calcul et sobriété | Absent d'OSI |
| 1 | Infrastructure & Calcul | Matériel, interconnexion | Physique + Liaison |
| 2 | Routage Cognitif | Router par compétence | Réseau |
| 3 | Interaction & Appels d'Outils | Agents ↔ monde extérieur | Transport |
| 4 | Sémantique & Contexte Partagé | Interopérabilité du sens | Absent d'OSI |
| 5 | Mémoire Persistante | Continuité de la conversation | Absent d'OSI |
| T | Gouvernance & Vérification | Éthique, alignement, confiance | Cryptographie transversale (TLS) |

---

## 3. Détail des couches

### Couche 0 — Thermodynamique & Énergétique

**Rôle.** Contraindre le coût physique du calcul. Chaque requête embarque un budget explicite (FLOPs, énergie, empreinte carbone). Le modèle adapte la profondeur de son raisonnement à ce budget : réponse rapide si le budget est faible, déploiement d'un raisonnement arborescent complet si le budget est élevé.

**Problème ouvert.** Rien n'empêche aujourd'hui un acteur de déclarer un budget mensonger. Une solution robuste nécessite soit une preuve cryptographique de calcul (voir §5), soit un tiers de confiance qui audite la consommation réelle.

### Couche 1 — Infrastructure & Calcul

**Rôle.** Standardiser l'interconnexion matérielle (GPU, TPU, accélérateurs), indépendamment du fabricant. Définit une latence maximale admissible et un format d'échange de tenseurs, dans la continuité de standards existants comme ONNX.

**Statut.** C'est la couche la plus proche de l'état de l'art actuel — elle formalise plus qu'elle n'invente.

### Couche 2 — Routage Cognitif

**Rôle.** Diriger une requête vers le modèle le plus compétent, non vers une adresse fixe. Chaque modèle publie un **certificat de compétence** : un vecteur d'embedding résumant ses domaines d'expertise. Le réseau route par similarité sémantique entre la requête et les certificats disponibles.

**Précision technique.** Ce mécanisme repose sur des embeddings vectoriels continus, où la distance entre deux points reflète une proximité de sens — et non sur des fonctions de hachage cryptographique, dont la propriété recherchée (effet avalanche) serait contre-productive ici.

**Problème ouvert.** Un certificat de compétence auto-déclaré n'est pas une preuve de compétence réelle. Voir §5.

### Couche 3 — Interaction & Appels d'Outils

**Rôle.** Gérer comment un agent IA interagit avec le monde extérieur : API, bases de données, autres agents, systèmes physiques. C'est la couche où des protocoles déjà existants comme MCP (Model Context Protocol) trouvent naturellement leur place. Elle gère la négociation de connexion, les délais d'exécution, la gestion d'erreurs.

**Statut.** Couche la plus mature — elle s'appuie sur des standards en cours d'adoption réelle dans l'industrie.

### Couche 4 — Sémantique & Contexte Partagé

**Rôle.** Permettre à des modèles entraînés indépendamment — sur des données, des architectures et parfois des langues différentes — de communiquer une intention sans ambiguïté. Plutôt que d'échanger du texte brut, les systèmes échangeraient une **ancre d'espace latent** : une représentation vectorielle de l'intention, générée par un modèle traducteur intermédiaire.

**Problème ouvert — le plus critique du modèle.** Il n'existe aujourd'hui aucune garantie que deux modèles entraînés séparément partagent une géométrie d'espace latent compatible, même face à une même idée. Des techniques de recherche existent (alignement de Procuste, analyse canonique de corrélations, apprentissage contrastif cross-modèle) mais aucune ne constitue une solution générale éprouvée à ce jour. Cette couche formalise une intuition juste, pas un problème résolu.

**Procédure de fallback (auto-correction inter-couches).** La couche 4 agit aussi comme un contrôle de cohérence sur le travail de la couche 2 : si le vecteur d'intention initial ne correspond pas à la réponse effectivement produite par le modèle sélectionné, la couche 4 émet un signal explicite (« incohérence sémantique détectée ») et renvoie la requête à la couche 2 pour un reroutage vers un autre modèle. Ce mécanisme rend le protocole auto-correcteur plutôt que strictement séquentiel : une erreur de routage n'est pas silencieusement propagée jusqu'à l'utilisateur, elle déclenche une nouvelle tentative. Un nombre maximal de tentatives de reroutage devrait être défini pour éviter les boucles infinies en cas d'ambiguïté persistante.

### Couche 5 — Mémoire Persistante

**Rôle.** Assurer la continuité conversationnelle au-delà d'une session isolée. Cette couche distingue deux flux de mémoire, par analogie avec la distinction cognitive entre mémoire épisodique et mémoire sémantique :

- **Mémoire épisodique** — le « ticket de contexte » proprement dit : un résumé compressé et volatile de l'historique propre à une session ou un utilisateur donné, permettant à un système de ne jamais reposer une question déjà traitée.
- **Mémoire sémantique** — un « embedding du monde » persistant, mis à jour en arrière-plan, représentant les connaissances générales accumulées indépendamment d'une conversation particulière. Contrairement au ticket épisodique, ce flux n'est pas propre à une session et évolue à un rythme différent.

Cette distinction enrichit la couche sans en complexifier l'architecture : les deux flux partagent le même mécanisme de transport, mais obéissent à des règles de durée de vie, de granularité et de confidentialité différentes.

**Point de vigilance.** La question du chiffrement et de la détention des clés de ces deux flux recoupe directement les enjeux de souveraineté des données traités par la couche transversale — les deux ne devraient pas être conçues indépendamment (voir §4, « Droit à l'oubli local »).

---

## 4. La couche transversale — Gouvernance & Vérification

Contrairement à un pare-feu périphérique qui inspecterait les requêtes en bordure du réseau, la couche de gouvernance est conçue comme **intrinsèque** : incrustée dans les en-têtes de chaque paquet, à toutes les couches, plutôt qu'ajoutée en une seule barrière contournable. Ce choix répond à une faiblesse connue des systèmes de filtrage périphérique en sécurité IA : un filtre placé uniquement en bordure peut être contourné par reformulation, précisément parce qu'il n'a pas la même profondeur de compréhension que le système qu'il est censé protéger. L'alignement doit donc être porté à la fois par l'entraînement des modèles eux-mêmes (couche 2 et au-delà) et par ce filet transversal — non par ce dernier seul.

**Droit à l'oubli local (piste optionnelle, orientée conformité réglementaire).** Dans une déclinaison future du standard, la couche de gouvernance pourrait imposer que le ticket de contexte de la mémoire épisodique (couche 5) soit chiffrable avec une clé détenue exclusivement par l'utilisateur final, et non par le fournisseur du modèle. Ce principe, distinct de la mémoire sémantique persistante qui reste sous la responsabilité du fournisseur, offrirait une garantie de suppression effective des données conversationnelles — un argument de conformité particulièrement pertinent au regard de cadres réglementaires comme le RGPD européen.

### 5. Le problème central : déclaratif vs vérifiable

La faiblesse structurelle commune aux couches 0, 2 et T est la suivante : **un système peut déclarer une propriété (budget, compétence, alignement) sans que cette déclaration soit vérifiable par construction.** C'est le même défi que la sécurité des communications a résolu partiellement avec TLS et les autorités de certification. ANP propose de traiter cette question comme un axe à part entière plutôt que comme un détail d'implémentation, en combinant quatre mécanismes complémentaires — aucun n'étant suffisant isolément :

1. **Attestation matérielle cryptographique** (inspirée des enclaves sécurisées type TPM, SGX, SEV) — garantit l'intégrité d'exécution d'un modèle, sans garantir sa compétence ou son alignement.
2. **Certification tierce indépendante**, périodique, par un organisme non affilié aux grands acteurs — sur le modèle des évaluateurs de capacités dangereuses déjà actifs dans le domaine (par exemple METR). Faiblesse : la certification est ponctuelle, un modèle peut dériver après coup.
3. **Réputation continue par observation**, s'auto-corrigeant dans le temps à mesure que les performances réelles s'écartent des déclarations. Faiblesse : laisse une fenêtre d'exploitation avant détection.
4. **Preuves à divulgation nulle de connaissance** (zero-knowledge proofs), un champ de recherche actif permettant de prouver qu'un calcul a respecté une contrainte sans exposer le calcul lui-même — particulièrement pertinent pour la vérification du budget de la couche 0.

Aucun de ces quatre mécanismes ne résout seul le problème de la confiance distribuée en IA. Leur combinaison, et la reconnaissance explicite de leurs limites respectives, est proposée ici comme direction de travail plutôt que comme solution arrêtée.

---

## 6. Limites assumées de ce document

Ce whitepaper est une proposition de structure, pas un protocole finalisé et implémentable en l'état. Trois limites méritent d'être nommées sans détour :

- La couche 4 (sémantique) repose sur une hypothèse de recherche non validée à l'échelle générale.
- Le mécanisme d'arbitrage en cas de désaccord entre modèles délibérant en parallèle (pertinent notamment en extension de la couche 2) reste à formaliser.
- La gouvernance de la confiance (§5) identifie des pistes existantes plutôt qu'une solution originale et complète.

Un modèle qui prétendrait n'avoir aucune de ces limites serait moins crédible, pas davantage.

---

## 7. Prochaines étapes proposées

- Confronter ce modèle à la littérature existante (papers sur les protocoles multi-agents, spécifications MCP et A2A, travaux sur l'alignement inter-modèles) pour affiner le vocabulaire et éviter les redites sous un autre nom.
- Ouvrir une discussion publique (issue tracker, forum dédié) pour recueillir la critique technique de la communauté avant toute revendication de standard.
- Explorer une implémentation de preuve de concept limitée à la couche 3 (interaction), la plus mature, comme démonstration tangible du modèle complet.

---

## Annexe — Historique des versions

- **v0.1** — Formulation initiale des six couches et de la couche transversale, développée en dialogue itératif ; intégration de la reformulation embedding (couche 2), de la clarification du nombre réel de couches, et de la section vérification/confiance (§5).
