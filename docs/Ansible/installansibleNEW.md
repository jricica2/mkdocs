# 🛠️ Installing Ansible on Windows, Linux, and macOS

## 📦 Prerequisites

- Python 3.9 or later (except on Windows where WSL is recommended)
- Administrator or sudo privileges
- Internet connection

---

## 🪟 Windows (via WSL)

Ansible is not natively supported on Windows. Use **Windows Subsystem for Linux (WSL)**.

1. **Enable WSL**

    ```powershell
    wsl --install
    ```
    !!! note
        Restart your computer if prompted.

2. **Install a Linux distribution**
    - Open Microsoft Store and install **Ubuntu** (or another preferred distro).

3. **Launch Ubuntu from Start Menu**

4. **Update packages**

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

5. **Install Ansible**

    ```bash
    sudo apt install software-properties-common -y
    sudo add-apt-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible -y
    ```

6. **Verify installation**

    ```bash
    ansible --version
    ```

---

## 🐧 Linux (Ubuntu/Debian)

1. **Update system**

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

2. **Install Ansible**

    ```bash
    sudo apt install software-properties-common -y
    sudo add-apt-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible -y
    ```

3. **Verify installation**

    ```bash
    ansible --version
    ```

---

## 🍎 macOS

1. **Install Homebrew** (if not already installed)

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

2. **Install Ansible**

    ```bash
    brew install ansible
    ```

3. **Verify installation**

    ```bash
    ansible --version
    ```

---

## ✅ Post-Installation Tips

- Create an inventory file: `/etc/ansible/hosts` or a custom one.
- Test with:

    ```bash
    ansible all -m ping -i your_inventory_file
    ```
