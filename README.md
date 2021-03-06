# Kathara_labs_test
KATHARA-LAB.CONF KATHARA MANUALKATHARA-LAB.CONF NAME kathara-lab.conf - Lab configuration file  DESCRIPTION The main lab configuration file. 


**KATHARA-LAB.CONF(5)KATHARA MANUALKATHARA-LAB.CONF(5)
NAME
kathara-lab.conf - Lab configuration file

DESCRIPTION
The main lab configuration file. In this file you can specify the names of devices to be started, any option that should be used when launching them, and the topology of the network that connects them. Optionally, you can also provide some descriptive information for the lab, which will be displayed upon its startup. This file is not explicitly required, but running a lab without a lab.conf file is kind of useless...

This file is a list of device[arg]=value assignments, where arg can be an integer value or the name of an option (described below).

If arg is an integer value, then value is the name of the collision domain to which interface etharg of device device must be connected (note that the name of the collision domain must not contain spaces (" "), commas (",") and dots ("."). For example, pc1[0]=CD1 means that interface eth0 of device pc1 will be connected to collision domain CD1.

If arg is an option name, then device will be launched with option arg set to value value.

In order to establish a uniform convention, comment lines should always start with a hash character (#).

DEVICE OPTIONS
image (string)
Docker image used for this device.
mem (string)
Set the amount of available RAM inside the device. If you set this option, the minimum allowed value is 4m (4 megabyte).
This option takes a positive integer, followed by a suffix of "b", "k", "m", "g", to indicate bytes, kilobytes, megabytes, or gigabytes.

cpus (float)
Limit the amount of CPU available for this device.
This option takes a positive float, ranging from 0 to max number of host logical CPUs. For instance, if the host device has two CPUs and you set device[cpus]=1.5, the container is guaranteed at most one and a half of the CPUs.

port (string)
Map localhost port HOST to the internal port GUEST of the device for the specified PROTOCOL.
If HOST port is not specified, default is 3000. If PROTOCOL is not specified, default is tcp. Supported PROTOCOL values are: tcp, udp, or sctp.

bridged (boolean)
Connect the device to the host network by adding an additional network interface. This interface will be connected to the host network through a NAT connection.
ipv6 (boolean)
Enable or disable IPv6 on this device.
exec (string)
Run a specific shell command inside the device during the startup phase.
sysctl (string)
Set a sysctl option for this device. Only the net. namespace is allowed to be set. Can be set multiple times per device, each will add a new entry (unless the same config item is used again).
env (string)
Set an environment variable for the device. Can be set multiple times per device, each will add a new entry (unless the same variable is used again). The format is: ENV_NAME=ENV_VALUE.
shell (string)
Use the specified shell to connect to the device, e.g., when kathara connect is called.
num_terms (integer)
Choose the number of terminals to open for this device.
LAB META INFORMATION
It is also possible to provide descriptive information about a lab by using one of the following special assignments:

LAB_NAME=string (a word as identifier for the lab)
LAB_DESCRIPTION=string (a brief description of the purpose of the lab)
LAB_VERSION=string (the version of the lab)
LAB_AUTHOR=string (people who have written the lab)
LAB_EMAIL=string (contacts of lab authors)
LAB_WEB=string (useful web resources related to the lab)
EXAMPLE
    LAB_NAME="Example"
	LAB_DESCRIPTION="A simple example of lab.conf"
	LAB_VERSION=1.0
	LAB_AUTHOR="Kathara Authors"
	LAB_EMAIL=contact@kathara.org
	LAB_WEB=http://www.kathara.org/

	r1[0]="A"
	r1[1]="B"
	r1[port]="32000"
	r1[image]="namespace/image_name"
	r1[sysctl]="net.ipv6.conf.all.forwarding=1"

	r2[0]="C"
	r2[1]="B"
	r2[port]="2000:500/udp"
	r2[exec]="echo Hi"

	pc1[0]="A"
	pc1[bridged]="true"

	pc2[0]="C"
	pc2[mem]="128m"
    pc2[shell]="/bin/sh"
Example of a lab.conf(5) file.

REPORTING BUGS
Report bugs opening an issue on the official GitHub repository where the development and maintenance is primarily done.
Issues which are security relevant should be disclosed privately to the Kathara mailing list. You do not have to be subscribed to the list to send a message there.
When reporting a bug, remember to write used commands, eventually attach your lab, and include the output of kathara-check(1) in order to make possible to reproduce the bug.

AUTHORS
Kathara was born from Netkit. Its first version was developed by Gaetano Bonofiglio and Veronica Iovinella. Currently it is mantained by Mariano Scazzariello, Tommaso Caiazzi and Lorenzo Ariemma.

People involved also include:

Giuseppe Di Battista
Gabriele Lospoto
Maurizio Patrignani
Maurizio Pizzonia
Massimo Rimondini
COPYRIGHT
Copyright ?? 2017-2021 License GPLv3+: GNU GPL version 3 or later http://gnu.org/licenses/gpl.html. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
kathara(1), kathara-lstart(1), Kathara official site

MAY 2022KATHARA-LAB.CONF(5)**
