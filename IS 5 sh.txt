#!/bin/bash

# Step 1: Navigate to the Source Directory
cd /usr/src

# Step 2: Download Snort and DAQ Packages
wget https://www.snort.org/downloads/snort/daq-2.0.7.tar.gz
wget https://www.snort.org/downloads/snort/snort-2.9.16.1.tar.gz

# Step 3: Extract the Downloaded Packages
tar xvzf daq-2.0.7.tar.gz
tar xvzf snort-2.9.16.1.tar.gz

# Step 4: Install Required Dependencies
yum install libpcap* pcre* libdnet* -y

# Step 5: Compile and Install DAQ
cd daq-2.0.7
./configure
make
make install

# Step 6: Compile and Install Snort
cd ../snort-2.9.16.1
./configure
make
make install

# Step 7: Verify Snort Installation
snort --version

# Step 8: Set Up Snort Configuration
mkdir -p /etc/snort/rules
mkdir -p /var/log/snort

# Step 9: Configure Snort
echo 'include /etc/snort/rules/icmp.rules' >> /etc/snort/snort.conf

# Step 10: Create an ICMP Rule
echo 'alert icmp any any -> any any (msg:"ICMP Packet"; sid:477; rev:3;)' > /etc/snort/rules/icmp.rules

# Step 11: Start Snort in IDS Mode
snort -i enp3s0 -c /etc/snort/snort.conf -l /var/log/snort/

# Step 12: In Another Terminal, Test with Ping
# ping www.yahoo.com (to trigger Snort alert)

# Step 13: Check Snort Alerts
cat /var/log/snort/alert
