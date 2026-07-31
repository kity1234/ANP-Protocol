# Contribuer à SANP

SANP est un draft de travail, pas un standard achevé. Il est publié précisément pour être challengé, testé et amélioré par des personnes qui savent des choses que l'auteur ignore. Si tu lis ceci, tu n'arrives pas trop tôt et tu n'as pas besoin de permission pour ne pas être d'accord.

## Quel type de contribution est utile en ce moment

À ce stade (v0.1), les contributions les plus précieuses sont **critiques**, pas seulement additives :

- **Critique structurelle** — est-ce que ce modèle viole un principe de robustesse ou de sécurité qui a fait fonctionner internet ? Dis-le, et cite le précédent si tu peux.
- **Antériorité** — si un papier, un protocole (MCP, A2A, ou autre) ou une direction de recherche résout déjà ce qu'ANP traite comme un problème ouvert (en particulier l'alignement sémantique inter-modèles de la Couche 4), indique-le nous. Dupliquer un travail existant sous un autre nom n'aide personne.
- **Falsifiabilité** — si tu peux décrire un scénario concret où une couche casse, ça vaut plus qu'un paragraphe d'éloges.
- **Faisabilité d'implémentation** — la Couche 3 (Interaction) est la plus mature et la première candidate pour une preuve de concept. Si tu la prototyperais différemment, ouvre une issue.

## Comment contribuer

1. **Ouvre une issue d'abord** pour tout ce qui est structurel — un changement de rôle d'une couche, un nouveau mécanisme, un changement de nom. Ça garde la discussion visible et évite les efforts dupliqués.
2. **Les pull requests** sont bienvenues pour le whitepaper et le README (fautes, clarté, traductions) sans discussion préalable. Pour tout ce qui touche l'architecture elle-même, merci d'ouvrir une issue d'abord.
3. **Le désaccord n'a pas besoin d'être poli pour être technique.** La franchise est bienvenue. Les attaques personnelles ne le sont pas.

## Ce que ce projet n'est pas (encore)

Ce n'est pas un protocole implémenté, pas une entreprise, et pas une revendication d'autorité sur la façon dont les systèmes d'IA devraient communiquer. Traite-le comme une proposition pour une conversation que le domaine n'a pas encore pleinement eue.

## Gestion des versions

Les changements substantiels au modèle (nouvelles couches, mécanismes retirés, sémantique modifiée) doivent être consignés dans la section historique des versions du whitepaper, pas fusionnés silencieusement.
