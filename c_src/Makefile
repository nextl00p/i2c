#
# Make the i2c_drv
# usage: TARGET=arm-none-linux-gnueabi make -f Makefile.cross
# Beaglebone Black: arm-linux-gnueabihf make -f Makefile.cross

OSNAME := $(shell uname -s)
MACHINE := $(shell uname -m)
ERLDIR	:= $(shell erl -noshell -eval "io:format([126,115,126,110],[code:root_dir()])" -s erlang halt)
ERL_C_INCLUDE_DIR := $(ERLDIR)/usr/include
CC = gcc
LD = ld
PRIVDIR=../priv/
DTHREAD=../../dthread

OBJS = i2c_drv.o

LDFLAGS = -shared -fpic

all : $(PRIVDIR) $(PRIVDIR)/i2c_drv.so

override CFLAGS += -Wall -Wextra -Wswitch-default -Wswitch-enum -fPIC -I$(ERL_C_INCLUDE_DIR) -I $(DTHREAD)/include -DDLOG_DEFAULT=DLOG_NONE

$(PRIVDIR):
	@mkdir -p $(PRIVDIR)

$(PRIVDIR)/i2c_drv.so : $(OBJS)
	$(CC) $(LDFLAGS) -o $@ $^

clean:
	$(RM) -f $(PRIVDIR)/i2c_drv.so $(OBJS)
