# RPi_Docker-Compose_SetUp
This is a repo guide to help get started with getting docker-compose up and running on a Raspberry Pi. This was tested out on a RPi 3B (1GB RAM, 32GB SD)


# Docker Compose Setup on Raspberry Pi

This guide will walk you through setting up Docker and Docker Compose on a Raspberry Pi. It's compatible with Raspberry Pi OS (32 or 64-bit) and most Debian-based distributions.

## 🧰 Requirements

- Raspberry Pi (any model that supports Docker, recommended: Pi 3 or newer)
- Raspberry Pi OS (or other Debian-based distro)
- Internet access
- Terminal access (via SSH or directly)

## 📦 Step 1: Update Your System

```bash
sudo apt update && sudo apt upgrade -y
```

## 🐳 Step 2: Install Docker

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

After installation, you need to add your user to the Docker group so you can run `docker` commands without needing `sudo`.

### 👤 Example: If your username is `tom`

Run the following command:

```bash
sudo usermod -aG docker tom
```

> 🔍 This command adds the user `tom` to the `docker` group.  
> This gives the user permission to run Docker commands without needing to prefix them with `sudo`.

### 💡 Generic Option

If you're writing a script or don't want to hardcode the username, use:

```bash
sudo usermod -aG docker $USER
```

> This version automatically uses the currently logged-in username (e.g., `tom`, if that's who is logged in).

⚠️ **Important**: You must log out and log back in (or reboot your Pi) for the group change to take effect.

## 🧱 Step 3: Install Docker Compose (v2 - plugin based)

As of Docker v20+, Compose is now included as a plugin.

```bash
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/latest/download/docker-compose-linux-aarch64 \
  -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
```

### Verify Docker Compose is working:

```bash
docker compose version
```

You should see output like:

```
Docker Compose version v2.x.x
```

## 🧪 Step 4: Test with a Sample Compose File

Create a sample project directory and Compose file:

```bash
mkdir my-pi-app && cd my-pi-app
```

Create `docker-compose.yml`:

```yaml
version: '3'
services:
  hello-world:
    image: hello-world
```

Run it:

```bash
docker compose up
```

## ✅ Done!

You now have Docker and Docker Compose running on your Raspberry Pi.

---

## 🛠 Troubleshooting

- If `docker compose` doesn't work, check your architecture using `uname -m` and make sure you're using the correct binary (`aarch64` for 64-bit OS).
- For 32-bit Raspberry Pi OS, use the `armv7` binary from the same Compose GitHub release page.

---

## 📚 References

- [Docker on ARM](https://docs.docker.com/engine/install/debian/)
- [Docker Compose GitHub](https://github.com/docker/compose)

---

## 📝 License

This guide is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to:
- Share — copy and redistribute the material in any medium or format
- Adapt — remix, transform, and build upon the material for any purpose, even commercially

**Under the following terms:**
- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made.

Created by [Your Name or GitHub Username].


