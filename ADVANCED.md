---

# Vim Cheat Sheet — Advanced

## Sommaire

1. Philosophie Vim (la clé de la vitesse)
2. Motions avancées
3. Text Objects (arme secrète)
4. Combinaisons puissantes
5. Navigation dans le code
6. Édition multi-lignes intelligente
7. Macros avancées
8. Registres (copy/paste avancé)
9. Marks et navigation dans les fichiers
10. Historique et jumps
11. Recherche avancée
12. Buffers / Tabs workflow
13. Tricks avancés

---

# 1. Philosophie Vim

Vim fonctionne comme une **phrase** :

```
[action] + [objet]
```

Exemples :

```
daw
```

→ delete a word

```
ci(
```

→ change inside parentheses

```
y}
```

→ yank jusqu'au prochain paragraphe

---

# 2. Motions avancées

### navigation par mots

| commande | effet                            |
| -------- | -------------------------------- |
| `w`      | mot suivant                      |
| `W`      | mot suivant (ignore ponctuation) |
| `b`      | mot précédent                    |
| `B`      | mot précédent large              |
| `e`      | fin du mot                       |

---

### navigation par phrases / paragraphes

| commande | effet                |
| -------- | -------------------- |
| `(`      | phrase précédente    |
| `)`      | phrase suivante      |
| `{`      | paragraphe précédent |
| `}`      | paragraphe suivant   |

---

### navigation ligne rapide

| commande | effet                |
| -------- | -------------------- |
| `fX`     | aller au prochain X  |
| `FX`     | aller au précédent X |
| `tX`     | avant X              |
| `;`      | répéter recherche    |
| `,`      | inverse              |

Exemple :

```
f(
```

aller au prochain `(`

---

# 3. Text Objects (le vrai super pouvoir)

C'est **LA fonctionnalité que les utilisateurs avancés utilisent tout le temps**.

Structure :

```
[action] + i/a + object
```

| objet | description |
| ----- | ----------- |
| `w`   | word        |
| `s`   | sentence    |
| `p`   | paragraph   |
| `"`   | quotes      |
| `'`   | quotes      |
| `(`   | parenthèses |
| `{`   | braces      |
| `<`   | balises     |

---

### exemples

```
ci"
```

changer texte **dans les guillemets**

```
da(
```

supprimer **( et contenu)**

```
yi{
```

copier contenu du bloc

---

### différence `i` vs `a`

| commande | effet                |
| -------- | -------------------- |
| `ci(`    | change **inside ()** |
| `ca(`    | change **(content)** |

---

# 4. Combinaisons puissantes

Quelques combos ultra utilisés :

```
ciw
```

change mot

```
di"
```

delete inside quotes

```
ci{
```

change bloc code

```
dap
```

delete paragraphe

```
gUw
```

mot en majuscule

```
guw
```

mot en minuscule

---

# 5. Navigation dans le code

### jump entre fonctions

| commande | effet               |
| -------- | ------------------- |
| `[[`     | fonction précédente |
| `]]`     | fonction suivante   |

---

### matching bracket

```
%
```

saute entre :

```
()
{}
[]
```

Très utile en dev.

---

# 6. Édition multi-lignes intelligente

### indent

```
>>
```

indent ligne

```
<<
```

désindent

---

### indent bloc

```
>ap
```

indent paragraphe

---

### join lignes

```
J
```

fusionne deux lignes

---

### split ligne

```
i<Enter>
```

---

# 7. Macros avancées

### enregistrer

```
qa
```

macro dans registre `a`

---

### arrêter

```
q
```

---

### jouer

```
@a
```

---

### répéter

```
10@a
```

exécute 10 fois

---

# 8. Registres (super puissant)

Vim a **plusieurs clipboard internes**.

### voir registres

```
:reg
```

---

### utiliser registre

```
"ap
```

coller registre `a`

---

### copier dans registre

```
"ayy
```

---

### clipboard système

```
"+y
```

copier vers OS

```
"+p
```

coller depuis OS

---

# 9. Marks (navigation bookmarks)

### créer mark

```
ma
```

mark `a`

---

### revenir

```
'a
```

ligne

```
`a
```

position exacte

---

Très utile dans gros fichiers.

---

# 10. Historique et jumps

### back / forward

```
Ctrl-o
```

retour

```
Ctrl-i
```

avant

---

### jump list

```
:jumps
```

---

# 11. Recherche avancée

### mot sous curseur

```
*
```

search forward

```
#
```

search backward

---

### remplacer interactif

```
:%s/foo/bar/gc
```

avec confirmation.

---

### remplacer dans sélection

```
:'<,'>s/foo/bar/g
```

---

# 12. Buffers / Tabs workflow

### buffers

```
:ls
```

liste

```
:b3
```

aller buffer

```
:bn
```

next

```
:bp
```

prev

---

### tabs

```
:tabnew
```

nouvel onglet

```
gt
```

tab suivant

```
gT
```

tab précédent

---

# 13. Tricks avancés

### répéter dernière commande

```
.
```

extrêmement puissant.

---

### modifier plusieurs lignes

```
Ctrl-v
```

visual block.

Exemple :

```
Ctrl-v
select
I//
Esc
```

commenter plusieurs lignes.

---

### dupliquer ligne

```
yyp
```

---

### déplacer ligne

```
ddp
```

---

### exécuter commande shell

```
:!ls
```

---

### formatter fichier

```
gg=G
```

---

# Raccourcis les plus utilisés:

Top 20 réel :

```
ciw
ci"
ci(
ci{
da(
di"
yy
dd
p
J
.
%
*
Ctrl-o
Ctrl-i
>> 
<<
@@
```

---
