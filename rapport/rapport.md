---
title: 'SE201 : Projet 1'
author: Florian Tarazona, Isaïe Muron, Lucie Molinié
...

\newpage

## RISC-V Tool Chain

### RISC-V Tools

Paragraphe sur les commandes executées à la compilation


- L'option `-nostdlib` retire les fichiers objets des librairies systèmes/des fichiers liés au démarrage lors de l'étape de link. Entre autres, les seuls 
fichiers considérés sont ceux spécifiés explicitement.
- L'option `-nostartfile` est similaire à l'option précédente, mais ne concerne que les fichiers liés au démarrage du programme (par exemple, 
les fichiers du type `crtX.o`).


Paragraphe sur le dump assembleur du tri 


Du code qualifié de _Position Independent_ est un morceau de code s'exécutant correctement indépendamment de son placement dans la mémoire. Le PIC est utile lors 
d'utilisation partagée d'un même extrait de code (par exemple des fonctions de librairies communes à deux programmes) puisqu'il permet de ne pas se soucier des 
emplacements des programmes respectifs. L'absence d'utilisation d'adresses absolues rend plus difficile la modification de la mémoire puisque l'attaquant ne connait 
pas l'adresse exacte où il doit réaliser l'injection de code / l'écriture mémoire.\
L'instruction `auipc` permet d'ajouter au `pc` un immédiat codé sur 20bits. En particulier, elle permet d'effectuer un saut sur n'importe quelle adresse de 32 bits 
lorsqu'elle est associée à l'instruction `jalr`. Cette combinaison permet, en pratique, d'accéder à toutes adresses écrites sur 32 bits à partir d'adresses relatives 
et non absolues.

### Ripes


\newpage

## Simple Pipelining


\newpage

## Branches and Multiple-Issue


\newpage

## Caches
