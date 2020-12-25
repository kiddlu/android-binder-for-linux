# To build modules outside of the kernel tree, we run "make"
# in the kernel source tree; the Makefile these then includes this
# Makefile once again.
# This conditional selects whether we are being included from the
# kernel Makefile or not.

# called from kernel build system: just declare what our modules are
ccflags-y += -I$(src)			# needed for trace events
obj-m := binder_linux.o
binder_linux-y := binder.o binder_alloc.o deps.o

CROSS_COMPILE = 

CC = gcc


# Assume the source tree is where the running kernel was built
# You should set KERNELDIR in the environment if it's elsewhere
KERNELDIR ?= /lib/modules/$(shell uname -r)/build

# The current directory is passed to sub-makes as argument
PWD := $(shell pwd)

all: deps.h modules

.PHONY: deps.h
deps.h:
	sudo bash $(PWD)/gen_deps.sh > $@

.PHONY: modules
modules:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules

.PHONY: clean
clean:
	rm -rf deps.h *.o *.ko *.mod.c *.symvers *.order .*.cmd .tmp_versions .cache.mk *.ur-safe

