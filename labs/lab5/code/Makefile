ARM = arm-none-eabi
CC = $(ARM)-gcc
LD  = $(ARM)-ld
AS  = $(ARM)-as
OD  = $(ARM)-objdump
OCP = $(ARM)-objcopy

# Change this line to change the default tty
TTY = /dev/tty.SLAB_USBtoUART

# Setting DEFAULT sets the default program that make
# will build and install. You can also build specific
# ones to build (e.g. 'make lines-2d.bin').
DEFAULT = lines-1d.bin

LIB_OBJS = start.o cstart.o helpers.o led.o fb.o fractal.o libgcc.a
CFLAGS  = -g -ffreestanding -nostdlib -nostartfiles -O3 -Wall
LDFLAGS = -T memmap

.PRECIOUS: %.o %.elf

all: $(DEFAULT) 

install: all
	rpi-install $(TTY) $(DEFAULT)

.s.o:
	$(AS) $(ASFLAGS) $< -o $@ 

.c.o:
	$(CC) $(CFLAGS) -c $< 



%.elf: $(LIB_OBJS) %.o
	$(LD) $(LDFLAGS) $^ -o $@ 
	$(OD) -D $@ > $@.list

%.bin: %.elf
	$(OCP) -O binary $^ $@

clean:
	rm -f *.bin *.elf *.list *~ *.o \#*
