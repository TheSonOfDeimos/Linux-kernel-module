MODULE_NAME = dm_zero


obj-m += $(MODULE_NAME).o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

test:
	sudo dmesg -C
	sudo insmod $(MODULE_NAME).ko
	sudo dmesg

	sudo dmsetup create zero1 --table "0 100 zero"
	ls -al /dev/mapper/*
	sudo dmesg

	sudo dmsetup create dmp1 --table "0 100 dm_zero /dev/mapper/zero1"
	ls -al /dev/mapper/*
	sudo dmesg

	sudo dmsetup remove zero1

	sudo lsmod | grep "$(MODULE_NAME)"
	sudo rmmod $(MODULE_NAME)

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean

	