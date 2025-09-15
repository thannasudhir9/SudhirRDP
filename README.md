# SudhirRDP

> **Easily run a Windows 10 virtual machine using Docker and KVM.**

---

## 🚀 Project Overview

This project provides a simple way to deploy a Windows 10 VM using Docker and KVM virtualization. It uses the [dockurr/windows](https://github.com/dockurr/windows) image and is managed via Docker Compose.

---

## 📋 Prerequisites

- Ubuntu or compatible Linux OS
- Docker & Docker Compose installed
- KVM support enabled on your system
- Sufficient resources (at least 4 CPU cores, 4GB RAM, 400GB+ disk space)

---

## 🛠️ Setup Instructions

1. **Switch to root (optional):**
   ```bash
   sudo su
   ```
2. **Update your system and install Docker:**
   ```bash
   sudo apt update
   sudo apt install docker.io docker-compose
   ```
3. **Create a project directory and configuration file:**
   ```bash
   mkdir docker
   cd docker
   vim windows10.yml
   ```
4. **Paste the following Docker Compose configuration:**
   ```yaml
   services:
     windows:
       image: dockurr/windows
       container_name: windows
       environment:
         VERSION: "10"
         USERNAME: "MASTER"
         PASSWORD: "admin@123"
         RAM_SIZE: "8G"
         CPU_CORES: "4"
         DISK_SIZE: "400G"
         DISK2_SIZE: "100G"
       devices:
         - /dev/kvm
         - /dev/net/tun
       cap_add:
         - NET_ADMIN
       ports:
         - "8006:8006"
         - "3389:3389/tcp"
         - "3389:3389/udp"
       stop_grace_period: 2m
   ```
5. **Save the file and start the VM:**
   ```bash
   sudo docker-compose -f windows10.yml up
   ```

---

## 🖥️ Accessing Windows 10
- Open your browser and go to `http://localhost:8006` for the web interface.
- Use any RDP client to connect to `localhost:3389` with the credentials:
  - **Username:** MASTER
  - **Password:** admin@123

---

## 📝 Notes
- Make sure your system supports virtualization (KVM).
- Adjust RAM, CPU, and disk sizes in the YAML as needed.
- Change the default password for security.

---

## 📚 References
- [dockurr/windows GitHub](https://github.com/dockurr/windows)
- [Docker Documentation](https://docs.docker.com/)
- [KVM Documentation](https://www.linux-kvm.org/page/Main_Page)
- [YouTube Setup Guide](https://www.youtube.com/watch?v=sbwGtNUtIWQ&ab_channel=GHTechHub)