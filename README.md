# **🐳 Docker Network Audit & Automation Tool**

A Bash-based Docker networking audit and reporting tool that inspects container networks, port mappings, IP addresses, and network modes — and automatically generates JSON audit reports every 6 hours using cron.  
This project simulates real-world DevOps / Cloud infrastructure auditing, where systems are continuously inspected instead of manually checked.  

## **🚀 Project Overview**
This tool provides both:  
- An interactive CLI menu for on-demand Docker network inspection
- An automated audit system that periodically generates structured JSON reports
- It helps answer critical questions like:
  - Which Docker networks exist?
  - Which containers are running?
  - How are containers connected to networks?
  - Which ports are exposed?
  - What IP addresses do containers have?
  - How many containers are attached to each network?
  - What Docker network drivers are in use?

## **⭐ Features**
✔ Docker Network Inspection  
- Lists all Docker networks available on the host.

✔ Container Visibility  
- Shows running containers or all containers (running + stopped).  

✔ Container Network Details  
- Inspects how containers are attached to Docker networks.  

✔ Port Mapping Audit  
- Displays host ↔ container port mappings to identify exposed services.  

✔ Container IP Address Extraction   
- Extracts private IP addresses assigned to containers.  

✔ Containers per Network  
- Counts how many containers are attached to each Docker network.  

✔ Network Mode Identification  
- Shows Docker network drivers (bridge, host, none, etc.).  

✔ JSON Export  
- Exports the complete audit into a structured JSON file.  

✔ Automated Audits (Cron)  
- Runs automatically every 6 hours, generating a fresh JSON snapshot without manual intervention.  

## **🖥️ Project Structure**
docker-network-audit/  
│  
├── docker_network_audit.sh  
└── audit.json        # Auto-generated JSON report  

## **▶️ Usage**
1. Make the script executable
- chmod +x docker_network_audit.sh

2. Run interactively
- ./docker_network_audit.sh
  - Use the menu to inspect networks, containers, ports, and export JSON manually.

3. ⏱️ Automated Execution (Cron)
- The script is scheduled using cron to run automatically every 6 hours.
-Cron Entry
  - 0 */6 * * * /usr/bin/bash /home/safi/Desktop/network/docker_audit/docker_network_audit.sh

4. Result
- A new JSON audit report is generated every 6 hours
- Always have an up-to-date snapshot of Docker networking state
- Simulates real infrastructure monitoring workflows

## **📄 JSON Output**

Audit reports are saved to:  
- /home/safi/Desktop/network/docker_audit/audit.json

Sample Output  
{  
  "networks": ["bridge", "host", "none"],  
  "containers": ["web1", "db1"],  
  "port_mappings": ["web1 0.0.0.0:8080->80/tcp"],  
  "container_ips": ["web1 172.17.0.2"],  
  "containers_per_network": ["bridge 2"],  
  "network_modes": ["bridge bridge", "host host"]  
}  

## **📦 Dependencies**

Required:  
- Docker
- Bash
- Optional (recommended):
  - jq (for clean JSON formatting)
    - Install jq:  
      sudo apt install jq  

## **🧠 How It Works**

- Uses Docker CLI commands (docker ps, docker network, docker inspect)
- Processes output using awk, sed, and Bash functions
- Converts audit data into structured JSON using jq
- Cron ensures regular, unattended execution
- This design supports both manual troubleshooting and continuous auditing.

## **🎯 Learning Outcomes**

This project helped me practice:  
- Docker networking fundamentals
- Container IP allocation and port exposure
- Bash scripting for infrastructure tooling
- JSON report generation
- Cron-based automation
- DevOps-style auditing and monitoring workflows
