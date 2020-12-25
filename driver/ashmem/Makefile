KERNELDIR ?= /lib/modules/$(shell uname -r)/build

PWD := $(shell pwd)

obj-m		:= ashmem_mod.o
ashmem_mod-y    := deps.o ashmem.o

all: deps.h modules

.PHONY: deps.h
deps.h:
	sudo bash $(PWD)/gen_deps.sh > $@

.PHONY: modules
modules:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules

.PHONY: clean
clean:
	rm -rf deps.h *.o *.ko *.mod.c *.symvers *.order .*.cmd .tmp_versions .cache.mk

