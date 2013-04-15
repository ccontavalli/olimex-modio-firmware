###############################################################################
# Makefile for the project firmware
###############################################################################

VPATH = ../src

## General Flags
PROJECT = firmware
MCU = atmega16
TARGET = firmware.elf
CC = avr-gcc

CPP = avr-g++

## Options common to compile, link and assembly rules
COMMON = -mmcu=$(MCU)

## Compile options common for all C compilation units.
CFLAGS = $(COMMON)
CFLAGS += -Wall -gdwarf-2 -std=gnu99 -Os -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums
CFLAGS += -MD -MP -MT $(*F).o -MF dep/$(@F).d 

## Assembly specific flags
ASMFLAGS = $(COMMON)
ASMFLAGS += $(CFLAGS)
ASMFLAGS += -x assembler-with-cpp -Wa,-gdwarf2

## Linker flags
LDFLAGS = $(COMMON)
LDFLAGS +=  -Wl,-Map=firmware.map


## Intel Hex file production flags
HEX_FLASH_FLAGS = -R .eeprom -R .fuse -R .lock -R .signature

HEX_EEPROM_FLAGS = -j .eeprom
HEX_EEPROM_FLAGS += --set-section-flags=.eeprom="alloc,load"
HEX_EEPROM_FLAGS += --change-section-lma .eeprom=0 --no-change-warnings


## Objects that must be built in order to link
OBJECTS = firmware.o AnalogINs.o DigitalINs.o DigitalOUTs.o I2C_FSM.o I2CAddress.o 

## Objects explicitly added by the user
LINKONLYOBJECTS = 

## Build
all: $(TARGET) firmware.hex firmware.eep firmware.lss size

## Compile
firmware.o: DemoSoft.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $< -o firmware.o

AnalogINs.o: AnalogINs.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

DigitalINs.o: DigitalINs.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

DigitalOUTs.o: DigitalOUTs.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

I2C_FSM.o: I2C_FSM.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

I2CAddress.o: I2CAddress.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

##Link
$(TARGET): $(OBJECTS)
	 $(CC) $(LDFLAGS) $(OBJECTS) $(LINKONLYOBJECTS) $(LIBDIRS) $(LIBS) -o $(TARGET)

%.hex: $(TARGET)
	avr-objcopy -O ihex $(HEX_FLASH_FLAGS)  $< $@

%.eep: $(TARGET)
	-avr-objcopy $(HEX_EEPROM_FLAGS) -O ihex $< $@ || exit 0

%.lss: $(TARGET)
	avr-objdump -h -S $< > $@

size: ${TARGET}
	@echo
	@avr-size -C --mcu=${MCU} ${TARGET}

## Clean target
.PHONY: clean
clean:
	-rm -rf $(OBJECTS) firmware.elf dep firmware.hex firmware.eep firmware.lss firmware.map

## Other dependencies
-include $(shell mkdir dep 2>/dev/null) $(wildcard dep/*)
