# Installing IPTables  
sudo apt update -y && sudo apt install iptables -y  # Debian-based  
sudo yum install iptables -y  # RHEL-based  

# Checking IPTables Rules  
sudo iptables -L -v -n  # Displays detailed information  
sudo iptables -t nat -L -v -n  # Check NAT table rules  

# Flushing (Removing) All Rules  
sudo iptables --flush  # Flush all rules  
sudo iptables -t nat --flush  # Flush NAT table rules  
sudo iptables -t mangle --flush  # Flush mangle table rules  

# Default Policy (Allow/Deny All Traffic)  
sudo iptables -P INPUT DROP  # Block all incoming traffic by default  
sudo iptables -P FORWARD DROP  # Block forwarded traffic  
sudo iptables -P OUTPUT ACCEPT  # Allow outgoing traffic  

# Allow SSH (Port 22)  
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  

# Allow HTTP & HTTPS Traffic  
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT  # HTTP  
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT  # HTTPS  

# Allow Specific IP Address  
sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT  

# Block Specific IP Address  
sudo iptables -A INPUT -s 192.168.1.200 -j DROP  

# Allow ICMP (Ping) Requests  
sudo iptables -A INPUT -p icmp -j ACCEPT  

# Limit SSH Login Attempts (Prevent Brute Force)  
sudo iptables -A INPUT -p tcp --dport 22 -m limit --limit 3/min --limit-burst 5 -j ACCEPT  

# NAT - Forward Traffic to Internal Server  
sudo iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.50:80  

# Masquerade (Enable Internet Access for LAN)  
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE  

# Save & Restore IPTables Rules  
sudo iptables-save > /etc/iptables/rules.v4  # Save rules  
sudo iptables-restore < /etc/iptables/rules.v4  # Restore rules  
