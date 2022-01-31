CC:=riscv64-linux-gnu-gcc
OBJDUMP:=riscv64-linux-gnu-objdump

CFLAGS:=-O -g -fno-pic -fno-inline -mcmodel=medlow -mabi=ilp32 -march=rv32im -Wall -static -nostdinc -nostartfiles -nodefaultlibs -nostdlib

.PHONY: all clean info

all: insertion-sort.elf

insertion-sort.elf: insertion-sort.c
	$(CC) $(CFLAGS) -o $@ $<

assembly: insertion-sort.elf
	echo | riscv64-linux-gnu-objdump -d insertion-sort.elf >> dump-d.txt

symbols: insertion-sort.elf
	echo | riscv64-linux-gnu-objdump -t -j.data -j.text insertion-sort.elf >> symbols.txt

info:
	@echo "Les commandes possibles sont:"
	@echo "make all        : compilation du code du tri insertion"
	@echo "make assembly   : écrit le dump assembleur du fichier compilé dans un fichier dump-*.txt"
	@echo "                  !!! les options -d/-S sont à modifier à la main"
	@echo "make symbols    : écrit le dump des symboles du fichier compilé dans un fichier symbols.txt"
	@echo "make info       : ce message"
	@echo "make clean      : nettoyage des fichiers inutiles"

clean:
	rm -f insertion-sort.elf
	rm -f *.txt
