CC = arm-none-eabi-gcc
MACH=cortex-m4
CFLAGS = -c  -mcpu=$(MACH) -mthumb -std=gnu11 -Wall -o0
#LDFLAGS= -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=nano.specs  -T stm32_ls.ld -Wl,-Map=final.map
LDFLAGS.SH= -mcpu=$(MACH) -mthumb -mfloat-abi=soft --specs=rdimon.specs  -T stm32_ls.ld -Wl,-Map=final.map



all:main.o led.o stm32_startup.o syscalls.o final.elf

semi:main.o led.o stm32_startup.o syscalls.o final_sh.elf

main.o:main.c 
	$(CC) $(CFLAGS) -o $@ $^

led.o:led.c
	$(CC) $(CFLAGS) -o $@ $^

stm32_startup.o:stm32_startup.c
	$(CC) $(CFLAGS) -o $@ $^

syscalls.o:syscalls.c
	$(CC) $(CFLAGS) -o $@ $^

final.elf:main.o led.o stm32_startup.o syscalls.o
	$(CC) $(LDFLAGS) -o $@ $^

final_sh.elf:main.o led.o stm32_startup.o  
	$(CC) $(LDFLAGS.SH) -o $@ $^



clean:
	rm -rf *.o *.elf

load:
	openocd -f /usr/share/openocd/scripts/board/stm32f4discovery.cfg
