# Step 1: Update System Packages  
sudo apt update -y && sudo apt upgrade -y  

# Step 2: Install Lynis  
sudo apt install lynis -y  # For Debian-based systems  
sudo yum install lynis -y  # For RHEL-based systems  

# Step 3: Verify Lynis Installation  
lynis show version  

# Step 4: Run a System Audit  
sudo lynis audit system  

# Step 5: Understanding the Audit Results  
# Lynis outputs results with color codes:
# Green: Everything is working fine or disabled.
# Yellow: Warnings, skipped tests, or missing configurations.
# Red: Critical security issues that need immediate attention.

# Step 6: Perform a Specific Security Audit  
sudo lynis audit system --quick  

# Step 7: View and Analyze Lynis Report  
cat /var/log/lynis-report.dat  

# Step 8: Check System Hardening Suggestions  
lynis show hardening  

# Step 9: View all Installed Plugins  
lynis show plugins  

# Step 10: Run Lynis in a Custom Mode (For Compliance Testing)  
sudo lynis audit system --profile /etc/lynis/custom.prf  

# Step 11: Export Results to a File  
sudo lynis audit system | tee lynis_audit_results.txt  

# Step 12: Remove Lynis (If Needed)  
sudo apt remove lynis -y  # For Debian-based systems  
sudo yum remove lynis -y  # For RHEL-based systems  

# Interpreting the Audit Report:
	•	Green: No issues found.
	•	Yellow: Possible misconfigurations or missing security features.
	•	Red: Critical security vulnerabilities requiring immediate action.

# Show Linux Hardening Steps
lynis show hardening  
