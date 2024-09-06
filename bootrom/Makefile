bootrom_img = bootrom.img

GCC=riscv64-unknown-elf-gcc -march=rv64im -mabi=lp64
OBJCOPY=riscv64-unknown-elf-objcopy

all: $(bootrom_img) bootrom.dump

%.img: %.bin
	dd if=$< of=$@ bs=128 count=1

%.bin: %.elf
	$(OBJCOPY) -O binary $< $@

%.elf: %.S linker.ld
	$(GCC) -Tlinker.ld $< -nostdlib -static -Wl,--no-gc-sections -o $@

%.dump: %.elf
	riscv64-unknown-elf-objdump --disassemble-all --disassemble-zeroes --section=.text --section=.text.start --section=.text.hang --section=.data --section=.bss --section=.rodata.dtb $< > $@
