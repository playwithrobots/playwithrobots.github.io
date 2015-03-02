# AVR-GCC Makefile
PROJECT=sample_project
SOURCES=main.c
CC=avr-gcc
OBJCOPY=avr-objcopy
MMCU=atmega8   # change the name as per your mcu

CFLAGS=-mmcu=$(MMCU) -Wall

$(PROJECT).hex: $(PROJECT).out
	$(OBJCOPY) -j .text -O ihex $(PROJECT).out $(PROJECT).hex

$(PROJECT).out: $(SOURCES)
	$(CC) $(CFLAGS) -I./ -o $(PROJECT).out $(SOURCES)

program: $(PROJECT).hex
	avrdude -p m8 -c avrusb500 -e -U flash:w:$(PROJECT).hex  # change it as per your mcu and programmer
clean:
	rm -f $(PROJECT).out
	rm -f $(PROJECT).hex
