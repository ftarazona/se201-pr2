CC:=riscv64-linux-gnu-gcc
OBJDUMP:=riscv64-linux-gnu-objdump

CFLAGS:=-O -g -fno-pic -fno-inline -mcmodel=medlow -mabi=ilp32 -march=rv32im -Wall -static -nostdinc -nostartfiles -nodefaultlibs -nostdlib

.PHONY: all clean

all: insertion-sort.elf

insertion-sort.elf: insertion-sort.c
	$(CC) $(CFLAGS) -o $@ $<

assembly: insertion-sort.elf
	echo | riscv64-linux-gnu-objdump -d insertion-sort.elf >> dump-d.txt

symbols: insertion-sort.elf
	echo | riscv64-linux-gnu-objdump -t -j.data -j.text insertion-sort.elf >> symbols.txt

clean:
	rm -f insertion-sort.elf
	rm -f *.txt
