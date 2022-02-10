---
title: 'SE201 : Projet 1'
author: Florian Tarazona, Isaïe Muron, Lucie Molinié
...

\newpage

## RISC-V Tool Chain

### RISC-V Tools

Lorsque l'on lance le Makefile (`$make`), on fait appel au compilateur gcc pour architecture RISC-V.

- L'option `-nostdlib` retire les fichiers objets des librairies systèmes/des fichiers liés au démarrage lors de l'étape de link. Entre autres, les seuls 
fichiers considérés sont ceux spécifiés explicitement.
- L'option `-nostartfile` est similaire à l'option précédente, mais ne concerne que les fichiers liés au démarrage du programme (par exemple, 
les fichiers du type `crtX.o`).


On peut désassembler le fichier `.elf` résultant en utilisant `objdump` (cf. Makefile, ajout d'une cible `assembly`), on obtient le code assembleur suivant :

```
Déassemblage de la section .text :

000100d8 <minIndex>:
   100d8:	00050813          	mv	a6,a0
   100dc:	04b05063          	blez	a1,1011c <minIndex+0x44>
   100e0:	00050693          	mv	a3,a0
   100e4:	00000513          	li	a0,0
   100e8:	00000713          	li	a4,0
   100ec:	0100006f          	j	100fc <minIndex+0x24>
   100f0:	00170713          	addi	a4,a4,1
   100f4:	00468693          	addi	a3,a3,4
   100f8:	02e58063          	beq	a1,a4,10118 <minIndex+0x40>
   100fc:	00251793          	slli	a5,a0,0x2
   10100:	00f807b3          	add	a5,a6,a5
   10104:	0006a603          	lw	a2,0(a3)
   10108:	0007a783          	lw	a5,0(a5)
   1010c:	fef652e3          	bge	a2,a5,100f0 <minIndex+0x18>
   10110:	00070513          	mv	a0,a4
   10114:	fddff06f          	j	100f0 <minIndex+0x18>
   10118:	00008067          	ret
   1011c:	00000513          	li	a0,0
   10120:	00008067          	ret

00010124 <main>:
   10124:	e5010113          	addi	sp,sp,-432
   10128:	1a112623          	sw	ra,428(sp)
   1012c:	1a812423          	sw	s0,424(sp)
   10130:	1a912223          	sw	s1,420(sp)
   10134:	1b212023          	sw	s2,416(sp)
   10138:	19312e23          	sw	s3,412(sp)
   1013c:	000117b7          	lui	a5,0x11
   10140:	1e878793          	addi	a5,a5,488 # 111e8 <input>
   10144:	00410413          	addi	s0,sp,4
   10148:	18c78613          	addi	a2,a5,396
   1014c:	00040713          	mv	a4,s0
   10150:	0007a683          	lw	a3,0(a5)
   10154:	00d72023          	sw	a3,0(a4)
   10158:	00478793          	addi	a5,a5,4
   1015c:	00470713          	addi	a4,a4,4
   10160:	fec798e3          	bne	a5,a2,10150 <main+0x2c>
   10164:	00000493          	li	s1,0
   10168:	06300993          	li	s3,99
   1016c:	06200913          	li	s2,98
   10170:	409985b3          	sub	a1,s3,s1
   10174:	00040513          	mv	a0,s0
   10178:	f61ff0ef          	jal	ra,100d8 <minIndex>
   1017c:	00950533          	add	a0,a0,s1
   10180:	00251513          	slli	a0,a0,0x2
   10184:	19010793          	addi	a5,sp,400
   10188:	00a78533          	add	a0,a5,a0
   1018c:	e7452783          	lw	a5,-396(a0)
   10190:	00042703          	lw	a4,0(s0)
   10194:	e6e52a23          	sw	a4,-396(a0)
   10198:	00f42023          	sw	a5,0(s0)
   1019c:	00148493          	addi	s1,s1,1
   101a0:	00440413          	addi	s0,s0,4
   101a4:	fd2496e3          	bne	s1,s2,10170 <main+0x4c>
   101a8:	00412503          	lw	a0,4(sp)
   101ac:	1ac12083          	lw	ra,428(sp)
   101b0:	1a812403          	lw	s0,424(sp)
   101b4:	1a412483          	lw	s1,420(sp)
   101b8:	1a012903          	lw	s2,416(sp)
   101bc:	19c12983          	lw	s3,412(sp)
   101c0:	1b010113          	addi	sp,sp,432
   101c4:	00008067          	ret

000101c8 <_start>:
   101c8:	ff010113          	addi	sp,sp,-16
   101cc:	00112623          	sw	ra,12(sp)
   101d0:	f55ff0ef          	jal	ra,10124 <main>
   101d4:	00a00893          	li	a7,10
   101d8:	00000073          	ecall
   101dc:	00c12083          	lw	ra,12(sp)
   101e0:	01010113          	addi	sp,sp,16
   101e4:	00008067          	ret

```

Le symbole `_start` correspond au code qui viendrait habituellement d'un fichier `crtX.s`. Le code de la première boucle du programme commence à l'adresse `0x1013c` et fini en `0x10154` :

```

   1013c:       000117b7                lui     a5,0x11
   10140:       1e878793                addi    a5,a5,488 # 111e8 <input>
   10144:       00410413                addi    s0,sp,4
   10148:       18c78613                addi    a2,a5,396
   1014c:       00040713                mv      a4,s0
   10150:       0007a683                lw      a3,0(a5)
   10154:       00d72023                sw      a3,0(a4)

```

Toujours à l'aide de `objdump`, on peut obtenir une liste des symboles générés:

```

insertion-sort.elf:     format de fichier elf32-littleriscv

SYMBOL TABLE:
000100d8 l    d  .text	00000000 .text
000111e8 l    d  .data	00000000 .data
00011378 g       .data	00000000 __SDATA_BEGIN__
000111e8 g     O .data	00000190 input
000101c8 g     F .text	00000020 _start
00011378 g       .data	00000000 __BSS_END__
00011378 g       .data	00000000 __bss_start
00010124 g     F .text	000000a4 main
000111e8 g       .data	00000000 __DATA_BEGIN__
00011378 g       .data	00000000 _edata
00011378 g       .data	00000000 _end
000100d8 g     F .text	0000004c minIndex

```

Le symbole `input` est à l'adresse `0x000111e8`. Il est utilisé par l'instruction d'adresse `0x10140`. 


Du code qualifié de _Position Independent_ est un morceau de code s'exécutant correctement indépendamment de son placement dans la mémoire. Le PIC est utile lors 
d'utilisation partagée d'un même extrait de code (par exemple des fonctions de librairies communes à deux programmes) puisqu'il permet de ne pas se soucier des 
emplacements des programmes respectifs. L'absence d'utilisation d'adresses absolues rend plus difficile la modification de la mémoire puisque l'attaquant ne connait 
pas l'adresse exacte où il doit réaliser l'injection de code / l'écriture mémoire.\
L'instruction `auipc` permet d'ajouter au `pc` un immédiat codé sur 20bits. En particulier, elle permet d'effectuer un saut sur n'importe quelle adresse de 32 bits 
lorsqu'elle est associée à l'instruction `jalr`. Cette combinaison permet, en pratique, d'accéder à toutes adresses écrites sur 32 bits à partir d'adresses relatives 
et non absolues.

Le code assembleur obtenu n'est pas _position independent_, il fait appel à des instructions utilisant des adresses absolues au lieu d'adresses relatives.
???? le dump indique des adresses absolues dans tous les cas, en particulier à la ligne `0x10178`, alors que les instructions utilisent des offsets. Traduction de objdump?
Dans le cas où c'est bien les adresses absolues qui sont utilisées, ce code n'est pas _position independent_.\
Dans tous les cas, l'utilisation de `ret` à la fin de la fonction `minIndex` se traduit par l'instruction `jalr x0, x1, 0` et l'adresse dans `x1` n'est aps une adresse relative à la position actuelle (c'est l'adresse de retour enregistrée par l'instruction d'adresse `0x10178`).



### Ripes


\newpage

## Simple Pipelining


\newpage

## Branches and Multiple-Issue


\newpage

## Caches
