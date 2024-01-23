include $(abs_top_srcdir)/Makefrag

src_dir := .
include $(src_dir)/tests.d

RISCV_PREFIX	?= riscv$(XLEN)-unknown-elf-
RISCV_GCC			?= $(RISCV_PREFIX)gcc

tests_p = $(addprefix riscv_epi-p-, $(tests))
tests_v = $(addprefix riscv_epi-v-, $(tests))

CFLAGS ?= \
	-static \
	-mcmodel=medany \
	-fvisibility=hidden \
	-nostdlib \
	-nostartfiles \
	-I$(abs_top_srcdir) \
	-I$(RISCVTOOLS)

.PHONY: default all clean

default: all

all: $(tests_p) $(tests_v)

vpath %.S $(src_dir)

riscv_epi-p-%: %\#DD_5\#BS_100\#DI_random.S
	$(RISCV_GCC) $(CFLAGS) -I$(ENV_P) -T$(ENV_P)/link.ld -o $@ $<

riscv_epi-v-%: %\#DD_5\#BS_100\#DI_random.S
	$(RISCV_GCC) $(CFLAGS) -I$(ENV_V) -T$(ENV_V)/link.ld -o $@ $<

junk += $(tests_p) $(tests_v)

clean:
	rm -rf $(junk)
