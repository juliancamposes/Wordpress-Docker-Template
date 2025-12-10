# 🐳 Dockerized WordPress Development Environment

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white) ![WordPress](https://img.shields.io/badge/WordPress-117AC9?style=flat&logo=wordpress&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)

This repository provides a complete, persistent local development environment for **WordPress** using Docker Compose. It includes MySQL 8.0, WordPress, and phpMyAdmin.

## 🚀 Quick Start

1.  **Prerequisites:** Ensure [Docker Desktop](https://www.docker.com/products/docker-desktop) is installed and running.
2.  **Start the Environment:** Run the following command in your terminal:
    ```bash
    docker-compose up -d
    ```
3.  **Access the Services:**
    * 🏠 **WordPress Site:** [http://localhost:8000](http://localhost:8000)
    * ⚙️ **Database Manager (phpMyAdmin):** [http://localhost:8080](http://localhost:8080)

---

## 💾 Data Persistence (How it works)

**Your data is safe.** This configuration is designed so you do not lose your work when you close Docker or restart your computer.

* **WordPress Files (Code, Themes, Plugins):**
    The directory is mapped using a **Bind Mount** (`.:/var/www/html`).
    * Your source code lives on your host machine in the current folder.
    * Modifying files locally updates them in the container immediately.
    * If you stop the container, the files remain on your computer.

* **Database (Posts, Pages, Settings):**
    The database uses a **Named Volume** (`db_data`).
    * MySQL data is stored in a managed Docker volume, isolated from the container's lifecycle.
    * Running `docker-compose down` **will not** delete your database.

---

## 🔑 Configuration & Credentials

The environment comes pre-configured with the following settings:

| Service | Variable | Value |
| :--- | :--- | :--- |
| **WordPress** | DB Host | `database` |
| **WordPress** | DB User | `wordpress` |
| **WordPress** | DB Password | `wordpress` |
| **WordPress** | DB Name | `wordpress` |
| **MySQL** | Root Password | `password` |

> **Note:** When accessing via **phpMyAdmin**, use server: `database`, user: `wordpress`, password: `wordpress`.

---

## 🛠️ Essential Commands

### Start / Restart
Builds (if necessary) and starts the containers in the background.
```bash
docker-compose up -d
```

### Stop Containers (Safe)
Stops and removes the containers and networks, but **keeps the database volume**. Next time you start, your data will still be there.
```bash
docker-compose down
```

### View Logs
Follow the logs in real-time to debug issues.
```bash
docker-compose logs -f
```

### ⚠️ Full Reset (Destructive)
**WARNING:** Use this only if you want to delete everything and start from scratch. This command removes containers **AND** the database volume.
```bash
docker-compose down -v
```

---

## 📂 Project Structure

After the first run, your directory will be populated with WordPress core files:

```text
.
├── docker-compose.yml
├── README.md
├── wp-content/       <-- Develop your themes and plugins here
├── wp-config.php     <-- Generated WP configuration
└── ...               <-- Other WP core files
```

### 📝 Git Configuration Note
Since WordPress installs its core files in your root folder, if you initialize a Git repository, **ensure you use a `.gitignore` file**. You should likely ignore the WordPress core files and only track your custom `wp-content` themes and plugins.