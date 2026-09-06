# rvp-releases

Artefacts de distribution de **Rondienza Visual Production**.

Ce dépôt ne contient **aucun code source**. Le code vit dans un dépôt privé
séparé ; seul le produit signé est publié ici, pour une raison précise :
l'updater de l'application doit pouvoir télécharger ses mises à jour **sans
qu'aucun jeton d'authentification ne soit embarqué dans le binaire**.

## Contenu

| Chemin               | Rôle                                                   |
| -------------------- | ------------------------------------------------------ |
| `latest-beta.json`   | manifeste du canal **beta** — l'endpoint que l'app lit  |
| `latest-stable.json` | manifeste du canal **stable** (pas encore ouvert)       |
| Releases GitHub      | les archives `.app.tar.gz` et leurs signatures `.sig`   |

L'application interroge une URL stable :

```
https://raw.githubusercontent.com/romuhica73/rvp-releases/main/latest-beta.json
```

Le manifeste y pointe vers l'archive d'une release versionnée. Les deux
coexistent volontairement : le manifeste doit vivre à une adresse fixe, l'archive
doit rester immuable et datée.

## Signature

Chaque archive est signée avec **minisign**. L'application vérifie la signature
contre une clé publique compilée dans son binaire, **avant** d'écrire quoi que ce
soit sur disque. Une archive non signée, altérée, ou signée par une autre clé ne
peut pas s'installer.

Clé publique en vigueur — keyID `0E50DFDB660E1E07`.

Un artefact publié ici est donc téléchargeable par tout le monde, mais ne peut
être **installé** que s'il porte une signature valide de la clé privée
correspondante — laquelle n'est ni dans ce dépôt, ni dans l'application.
