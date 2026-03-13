# Vim Cheat Sheet

## Sommaire

1. Modes Vim
2. Navigation
3. Édition
4. Copier / Coller / Supprimer
5. Recherche et remplacement
6. Fichiers et buffers
7. Splits et fenêtres
8. Macros
9. Annulation
10. Astuces utiles

---

# 1. Modes Vim

| Commande | Description |
|---|---|
| `Esc` | Mode normal |
| `i` | Insérer avant le curseur |
| `a` | Insérer après le curseur |
| `o` | Nouvelle ligne dessous |
| `O` | Nouvelle ligne dessus |
| `v` | Mode visuel |
| `V` | Mode visuel ligne |
| `Ctrl-v` | Mode visuel bloc |

---

# 2. Navigation

## Basique

| Commande | Action |
|---|---|
| `h` | gauche |
| `j` | bas |
| `k` | haut |
| `l` | droite |

## Mots

| Commande | Action |
|---|---|
| `w` | mot suivant |
| `e` | fin du mot |
| `b` | mot précédent |

## Ligne

| Commande | Action |
|---|---|
| `0` | début ligne |
| `^` | premier caractère |
| `$` | fin ligne |

## Fichier

| Commande | Action |
|---|---|
| `gg` | début fichier |
| `G` | fin fichier |
| `Ctrl-d` | demi-page bas |
| `Ctrl-u` | demi-page haut |

---

# 3. Édition

| Commande | Action |
|---|---|
| `i` | insert |
| `a` | append |
| `o` | nouvelle ligne |
| `O` | ligne au-dessus |
| `r` | remplacer un caractère |
| `R` | remplacer plusieurs |

---

# 4. Copier / Coller / Supprimer

| Commande | Action |
|---|---|
| `x` | supprimer caractère |
| `dd` | supprimer ligne |
| `yy` | copier ligne |
| `p` | coller après |
| `P` | coller avant |
| `ctrl + shift + v  | coller depuis le clipboard |

## Combinaisons puissantes

| Commande | Action |
|---|---|
| `dw` | supprimer mot |
| `d$` | supprimer fin ligne |
| `daw` | supprimer mot entier |
| `cw` | changer mot |
| `c$` | changer fin ligne |
| `y}` | copier paragraphe |

---

# 5. Recherche

| Commande | Action |
|---|---|
| `/mot` | recherche |
| `?mot` | recherche arrière |
| `n` | résultat suivant |
| `N` | résultat précédent |

Remplacement :
| :%s/ancien/nouveau/g |

---

# 6. Fichiers

| Commande | Action |
|---|---|
| `:e fichier` | ouvrir fichier |
| `:w` | sauvegarder |
| `:q` | quitter |
| `:wq` | sauvegarder + quitter |

---

# 7. Buffers

| Commande | Action |
|---|---|
| `:ls` | liste buffers |
| `:b1` | aller buffer 1 |
| `:bn` | buffer suivant |
| `:bp` | buffer précédent |

---

# 8. Splits

Créer splits :

| Commande | Action |
|---|---|
| `:sp fichier` | split horizontal |
| `:vsp fichier` | split vertical |
| `Ctrl-w s` | split horizontal |
| `Ctrl-w v` | split vertical |

Navigation :

| Commande | Action |
|---|---|
| `Ctrl-w h` | gauche |
| `Ctrl-w j` | bas |
| `Ctrl-w k` | haut |
| `Ctrl-w l` | droite |
| `Ctrl-w w` | fenêtre suivante |

Gestion :

| Commande | Action |
|---|---|
| `Ctrl-w q` | fermer |
| `Ctrl-w =` | équilibrer |
| `Ctrl-w _` | maximiser hauteur |
| `Ctrl-w |` | maximiser largeur |

---

# 9. Macros

| Commande | Action |
|---|---|
| `qa` | start macro a |
| `q` | stop macro |
| `@a` | rejouer |
| `@@` | rejouer dernière |

---

# 10. Annulation

| Commande | Action |
|---|---|
| `u` | undo |
| `Ctrl-r` | redo |

---

# 11. Astuces utiles

| Commande | Action |
|---|---|
| `.` | répéter dernière action |
| `:set number` | numéros ligne |
| `:set relativenumber` | numéros relatifs |
| `:syntax on` | coloration |
| `:set hlsearch` | surligner recherche |
