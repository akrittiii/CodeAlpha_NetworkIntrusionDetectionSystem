
# Network Intrusion Detection System (NIDS) using Snort  

This project demonstrates how to set up and configure a Network Intrusion Detection System (NIDS) using [Snort](https://www.snort.org/), a powerful open-source tool for monitoring network traffic and detecting potential threats.  

---

## Features  
- **Real-time Traffic Analysis**: Monitors network traffic for potential security breaches.  
- **Custom Rule Creation**: Add your own intrusion detection rules.  
- **Modular Configuration**: Easily configurable for different environments.  

---

## Prerequisites  
Before starting, ensure you have the following:  
- A Linux-based operating system (e.g., Ubuntu or CentOS).  
- Basic knowledge of networking and security.  
- A non-production network environment for testing.  

---

## Installation Steps  

1. **Install Dependencies**  
   ```bash
   sudo apt update
   sudo apt install -y build-essential libpcap-dev libpcre3-dev libdumbnet-dev bison flex zlib1g-dev
   ```  

2. **Download and Install Snort**  
   ```bash
   wget https://www.snort.org/downloads/snort/xxxxx.tar.gz
   tar -xzvf xxxxx.tar.gz
   cd snort-xxxx
   ./configure
   make
   sudo make install
   ```  

3. **Set Up Configuration Directories**  
   ```bash
   sudo mkdir -p /etc/snort/rules /var/log/snort /usr/local/lib/snort_dynamicrules
   sudo cp etc/*.conf /etc/snort/
   ```  

4. **Download Snort Rules**  
   Register on [Snort.org](https://www.snort.org/) and download the latest rules. Place them in `/etc/snort/rules`.  

5. **Edit Configuration File**  
   - Open `/etc/snort/snort.conf`:  
     ```bash
     sudo nano /etc/snort/snort.conf
     ```  
   - Configure `HOME_NET` and `EXTERNAL_NET`.  
   - Include rule files, e.g.:  
     ```bash
     include $RULE_PATH/local.rules
     ```  

6. **Create Custom Rules**  
   - Open `local.rules`:  
     ```bash
     sudo nano /etc/snort/rules/local.rules
     ```  
   - Add a sample rule:  
     ```bash
     alert icmp any any -> $HOME_NET any (msg:"ICMP Packet Detected"; sid:1000001;)
     ```  

7. **Run Snort**  
   - Test the configuration:  
     ```bash
     snort -T -c /etc/snort/snort.conf
     ```  
   - Run in NIDS mode:  
     ```bash
     sudo snort -A console -q -c /etc/snort/snort.conf -i <interface>
     ```  

---

## Logs and Alerts  
- Logs are stored in `/var/log/snort`.  
- Real-time alerts appear on the console if running in `-A console` mode.  

---

## Future Improvements  
- Automate the setup using scripts or Ansible.  
- Integrate with visualization tools (e.g., Kibana).  
- Add advanced rule sets for specific use cases.  

---

## License  
This project is licensed under the MIT License.  

---

## Contribution  
Contributions are welcome! Feel free to submit issues or pull requests.  

---

## Resources  
- [Snort Documentation](https://www.snort.org/documents)  
- [Snort Rules](https://www.snort.org/rules)  
