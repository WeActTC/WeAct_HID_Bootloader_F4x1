CC=gcc
CFLAGS=-c -Wall
LDFLAGS=
SOURCES=WeAct_HID_Flash_CLI.c
INCLUDE_DIRS=-I .
DEL=
OBJPATH=OBJPATH

ifeq ($(OS),Windows_NT)
	SOURCES+=hid-win.c
	SOURCES+=rs232.c
	SOURCES+=hex2bin\readhex.c
	LIBS=-lsetupapi -lhid
	DEL=del
else
	DEL=rm -f
	UNAME_S := $(shell uname -s)
	ifeq ($(UNAME_S),Darwin)
		SOURCES+=hid-mac.c
		SOURCES+=rs232.c
		LIBS=-framework IOKit -framework CoreFoundation
	else
		SOURCES+=hid-libusb.c
		SOURCES+=rs232.c
		SOURCES+=hex2bin/readhex.c
		LIBS=`pkg-config libusb-1.0 --libs` -lrt -lpthread
		INCLUDE_DIRS+=`pkg-config libusb-1.0 --cflags`
		CFLAGS+=-std=gnu99
		LDFLAGS+=-no-pie
	endif
endif

OBJECTS=$(SOURCES:.c=.o)

EXECUTABLE = WeAct_HID_Flash-CLI

all: $(SOURCES) $(EXECUTABLE)

$(EXECUTABLE): $(OBJECTS)
	$(CC) $(LDFLAGS) $(OBJECTS) $(LIBS) -o $@

.c.o:
	$(CC) $(CFLAGS) $(INCLUDE_DIRS) $< -o $@ 

clean:
	$(DEL) $(OBJECTS) $(EXECUTABLE) $(EXECUTABLE).exe

