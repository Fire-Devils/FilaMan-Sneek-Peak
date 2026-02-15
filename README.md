# How to Install FilaMan via Docker

This guide explains how to run the FilaMan application using a pre-built Docker image.

---

## English

### Recommended Method: Using the Install Script

This is the easiest way to get started. You only need to run one command.

**Prerequisites:**
-   **Linux/macOS:** `bash`, `curl`, `docker`, and `docker-compose` must be installed.
-   **Windows:** Use WSL (Windows Subsystem for Linux).

**Installation:**
Run the following command in your terminal. It will download the installer script and execute it.

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/fire-devils/FilaMan-System/main/install.sh)"
```

The script will guide you through the process by asking for the Docker image path. It will automatically create a directory (`filaman_data`), generate the necessary configuration files with secure keys, and start the application.

### Manual Installation

Follow these steps if you prefer to set up the application manually.

**Step 1: Create a Folder**  
Create a new, empty folder on your computer.

**Step 2: Create `docker-compose.yml`**  
Inside the folder, create a file named `docker-compose.yml` and paste the following content. You **must** replace the `image` value with the correct path.

```yaml
# Content of docker-compose.yml
version: '3.8'
services:
  filaman:
    image: ghcr.io/fire-devils/filaman-system:latest # IMPORTANT: Replace if you have a different image path
    container_name: filaman-system-app
    restart: unless-stopped
    ports:
      - "8000:8000"
    volumes:
      - ./filaman.db:/app/filaman.db
    env_file:
      - .env
networks:
  default:
    name: filaman-network
```

**Step 3: Create `.env` Configuration File**  
In the same folder, create another file named `.env`. Paste the content below.

```env
# Content of .env
SECRET_KEY=change-me-in-production
CSRF_SECRET_KEY=change-me-in-production
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=admin123
ADMIN_DISPLAY_NAME=Admin
ADMIN_LANGUAGE=en
ADMIN_SUPERADMIN=true
DEBUG=false
CORS_ORIGINS=*
DATABASE_URL=sqlite+aiosqlite:////app/filaman.db
```

**Step 4: Start the Application**  
Open a terminal, navigate into your folder, and run:  
`docker-compose up -d`

### Accessing the Application

- **URL:** http://localhost:8000
- **Username:** `admin@example.com`
- **Password:** `admin123`

---

## Deutsch

### Empfohlene Methode: Installation per Skript

Dies ist der einfachste Weg, um zu starten. Sie müssen nur einen Befehl ausführen.

**Voraussetzungen:**
-   **Linux/macOS:** `bash`, `curl`, `docker`, und `docker-compose` müssen installiert sein.
-   **Windows:** Verwenden Sie WSL (Windows Subsystem für Linux).

**Installation:**
Führen Sie den folgenden Befehl in Ihrem Terminal aus. Er lädt das Installationsskript herunter und führt es aus.

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/fire-devils/FilaMan-System/main/install.sh)"
```

Das Skript wird Sie durch den Prozess führen, indem es nach dem Docker-Image-Pfad fragt. Es erstellt automatisch ein Verzeichnis (`filaman_data`), generiert die notwendigen Konfigurationsdateien mit sicheren Schlüsseln und startet die Anwendung.

### Manuelle Installation

Folgen Sie diesen Schritten, wenn Sie die Anwendung lieber manuell einrichten möchten.

**Schritt 1: Ordner erstellen**  
Erstellen Sie einen neuen, leeren Ordner auf Ihrem Computer.

**Schritt 2: `docker-compose.yml` erstellen**  
Erstellen Sie im Ordner eine Datei namens `docker-compose.yml` und fügen Sie den Inhalt von unten ein. Sie **müssen** den Wert bei `image` durch den korrekten Pfad ersetzen.

```yaml
# Inhalt der docker-compose.yml
version: '3.8'
services:
  filaman:
    image: ghcr.io/fire-devils/filaman-system:latest # WICHTIG: Ersetzen, falls Sie einen anderen Image-Pfad haben
    container_name: filaman-system-app
    restart: unless-stopped
    ports:
      - "8000:8000"
    volumes:
      - ./filaman.db:/app/filaman.db
    env_file:
      - .env
networks:
  default:
    name: filaman-network
```

**Step 3: `.env`-Konfigurationsdatei erstellen**  
Erstellen Sie im selben Ordner eine Datei namens `.env` und fügen Sie den untenstehenden Inhalt ein.

```env
# Inhalt der .env
SECRET_KEY=change-me-in-production
CSRF_SECRET_KEY=change-me-in-production
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=admin123
ADMIN_DISPLAY_NAME=Admin
ADMIN_LANGUAGE=en
ADMIN_SUPERADMIN=true
DEBUG=false
CORS_ORIGINS=*
DATABASE_URL=sqlite+aiosqlite:////app/filaman.db
```

**Schritt 4: Anwendung starten**  
Öffnen Sie ein Terminal, navigieren Sie in Ihren Ordner und führen Sie aus:  
`docker-compose up -d`

### Zugriff auf die Anwendung

- **URL:** http://localhost:8000
- **Benutzername:** `admin@example.com`
- **Passwort:** `admin123`
