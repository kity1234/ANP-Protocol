# SANP — Semantic Artificial Network Protocol
### Un modèle en couches pour l'interopérabilité, le raisonnement distribué et la gouvernance de l'intelligence artificielle

![Statut : Draft v0.1](https://img.shields.io/badge/status-draft-orange)
![Licence : MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Contributions bienvenues](https://img.shields.io/badge/contributions-welcome-brightgreen)

---

## En une phrase

**SANP est un modèle conceptuel qui traite la communication entre systèmes d'IA comme un problème architectural à part entière** — un problème que les protocoles réseau classiques n'ont jamais eu à résoudre, parce qu'ils transportent des bits, pas du sens.

---

## Pourquoi ce projet existe

L'écosystème actuel de l'IA se développe sans grammaire architecturale commune. OpenAI, Google, Anthropic, la communauté open source et les laboratoires nationaux construisent chacun leurs propres protocoles d'interconnexion — MCP, A2A, formats propriétaires — sans cadre unificateur pour penser l'ensemble.

Les modèles réseau classiques comme OSI et TCP/IP ont résolu l'interopérabilité en restant délibérément aveugles au contenu : un routeur n'a pas besoin de comprendre un email pour le transmettre. L'IA rompt avec cette hypothèse. Router une requête vers le bon modèle, ou permettre à deux systèmes entraînés indépendamment d'échanger une intention, exige d'interpréter le sens — ce qu'OSI n'a jamais eu à faire.

> ANP n'est pas un protocole de transport. C'est une proposition de **cognition distribuée**.

Ce document est un draft de travail, pas un standard achevé. Il est publié pour être discuté et critiqué, pas pour revendiquer une autorité.

---

## Architecture générale : 6 couches + 1 couche transversale

| Couche | Nom | Rôle clé |
|---|---|---|
| **0** | Thermodynamique & Énergétique | Budget de calcul et sobriété par construction. Chaque requête embarque un quota FLOPs/énergie qui module la profondeur du raisonnement. |
| **1** | Infrastructure & Calcul | Standardisation du matériel (GPU, TPU) et des formats d'échange de tenseurs, dans la continuité de standards existants comme ONNX. |
| **2** | Routage Cognitif | Route par *compétence* (vecteur d'embedding), et non par adresse fixe. Chaque modèle publie un certificat de compétence. |
| **3** | Interaction & Appels d'Outils | Communication des agents avec le monde extérieur — API, autres modèles, systèmes physiques. C'est ici que des protocoles comme MCP trouvent naturellement leur place. |
| **4** | Sémantique & Contexte Partagé | Interopérabilité du sens via des ancres d'espace latent. Inclut un mécanisme de fallback : une incohérence sémantique déclenche un reroutage vers la couche 2. |
| **5** | Mémoire Persistante | Distingue la mémoire épisodique (ticket de contexte propre à une session) de la mémoire sémantique (un embedding du monde, persistant et mis à jour plus lentement). |
| **T** | Gouvernance & Vérification *(transversale)* | Éthique, alignement, traçabilité et confiance — incrustée dans chaque couche plutôt qu'ajoutée en périphérie. |

---

## Ce qui est réellement nouveau

Deux choix de conception se distinguent :

- **Couche 2 + Couche 0 ensemble** : les requêtes sont routées par le sens plutôt que par l'adresse, *et* contraintes par un budget énergétique explicite — un couplage entre routage sémantique et coût physique que nous n'avons pas vu formalisé ailleurs.
- **La couche 4 n'est pas passive** : si la réponse d'un modèle ne correspond pas au vecteur d'intention initial, la couche déclenche un reroutage automatique plutôt que de laisser passer silencieusement une mauvaise réponse. Le réseau est conçu pour s'auto-corriger.

---

## Le problème central identifié : déclaratif vs vérifiable

> Un système peut *déclarer* une propriété — budget, compétence, alignement — sans que cette déclaration soit vérifiable de façon indépendante.

ANP ne prétend pas résoudre ce problème. Il propose de combiner quatre mécanismes complémentaires, chacun insuffisant isolément :

1. **Attestation matérielle** (enclaves type TPM/SGX) — garantit l'intégrité d'exécution, pas la compétence.
2. **Certification tierce indépendante** — audits périodiques, dans l'esprit des évaluateurs de capacités dangereuses déjà actifs dans le domaine.
3. **Réputation continue** — s'auto-corrige dans le temps, mais laisse une fenêtre d'exploitation avant que la dérive soit détectée.
4. **Preuves à divulgation nulle de connaissance** — un champ de recherche actif, particulièrement pertinent pour vérifier le budget déclaré de la couche 0 sans exposer le calcul sous-jacent.

---

## Limites assumées

Un modèle qui prétendrait n'avoir aucune limite serait moins crédible, pas davantage.

- La **couche 4** repose sur une hypothèse de recherche — l'alignement d'espaces latents entre modèles — qui n'est pas résolue à l'échelle générale aujourd'hui.
- Le **mécanisme d'arbitrage** en cas de désaccord réel entre modèles délibérant en parallèle est esquissé, pas formalisé.
- La section **confiance et vérification** (ci-dessus) recense des pistes existantes plutôt qu'elle ne propose une solution originale et complète.

---

## Feuille de route

- [x] Formulation du modèle conceptuel (v0.1)
- [ ] Confrontation à la littérature académique existante (protocoles multi-agents, spécifications MCP/A2A, recherche sur l'alignement inter-modèles)
- [ ] Ouverture d'une discussion publique (issues, forum)
- [ ] Implémentation d'une preuve de concept limitée à la couche 3 (Interaction) — la plus mature

---

## Contribuer

Ce n'est pas une proposition fermée — c'est un point de départ pour la critique.

- **Architectes réseau** : dites-nous où ce modèle viole les principes de robustesse qui ont fait fonctionner internet.
- **Chercheurs en IA** : dites-nous si la couche 4 (Sémantique) est une impasse ou une piste viable.
- **Ingénieurs ML** : dites-nous par quelle couche vous commenceriez à prototyper demain.
- **Sceptiques** : dites-nous pourquoi tout ceci est inutile ou risqué.

Ouvrez une issue ou soumettez une pull request — le désaccord est bienvenu et attendu à ce stade.

---

## Soutenir ce projet

ANP est développé de façon indépendante, sans soutien institutionnel ou d'entreprise. Si tu veux aider à financer la prochaine étape — une implémentation de preuve de concept limitée à la Couche 3 (Interaction), qui nécessite des ressources de calcul — voici comment :

- **Bitcoin :** `1EDrde4DHf1p8Vm34Rmax1SRzXNZiooRf7`
- **USDT (réseau ERC-20 / Ethereum) :** `0x3661f7006a5fb87cf1a035319b8fc39e62243b1a`

Aucune pression, aucun palier, aucune contrepartie — juste un moyen de soutenir un travail indépendant si ça te semble utile.

---

## Licence & Auteur

- **Auteur :** Serge Olivier KITT
- **Draft initial :** Juillet 2026
- **Licence :** Code sous MIT (`LICENSE`) — Contenu écrit (whitepaper, README) sous CC BY 4.0 (`LICENSE-DOCS`)
