# V-Server Setup

This project documents the setup of a Linux V-Server for secure SSH access, web hosting with NGINX, and GitHub-based development.

I administered the server from **Windows PowerShell** using OpenSSH. After connecting, the Linux commands were executed inside the SSH session in PowerShell.

The goal is to make the setup **reproducible and verifiable**. This README describes required steps; only checks that have actually been performed should be marked complete.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Quickstart](#quickstart)
- [Usage](#usage)
  - [1. SSH key authentication](#1-ssh-key-authentication)
  - [2. SSH key copy to server](#2-ssh-key-copy)
  - [3. Disable SSH password login](#3-disable-ssh-password-login)
  - [4. Install NGINX and serve a custom page](#4-install-nginx-and-serve-a-custom-page)
  - [5. Configure Git on the server](#5-configure-git-on-the-server)
  - [6. Connect the server to GitHub](#6-connect-the-server-to-github)
- [Troubleshooting and Security](#troubleshooting-and-security)
- [References](#references)

## Prerequisites

- A Linux V-Server (commands below assume Ubuntu/Debian) and an account with sudo privileges
- Working initial server access (SSH password login or hosting-provider console)
- Windows PowerShell with the OpenSSH client
- A GitHub account
- Network access to the server

Replace `USERNAME` with your username, `SERVER_IP` with the real IP address and `YOUR_GITHUB_EMAIL` with an email address associated with the GitHub account. Do not publish passwords or private SSH keys.

## Quickstart

**Local Windows PowerShell** — connect using the private key generated on the PC:

```powershell
ssh -i "$env:USERPROFILE\.ssh\da\demo_ed25519" -o IdentitiesOnly=yes USERNAME@SERVER_IP
```
Leave the server session using `logout`. If the key has not been installed yet, follow the setup steps below before attempting key-only login.

## Usage

### 1. SSH key authentication

Generate the **PC → V-Server** key pair **on Windows**, not on the server. Run in **local PowerShell**:

```powershell
ssh-keygen -t ed25519 
```

Enter file in which to save the key with name for Example:

```text
$env:USERPROFILE\.ssh\demo_ed25519
```

Enter passphrase, empty for no passphrase.

Do not overwrite an existing key pair. The file ending in `.pub` is the **public** key; the file without `.pub` is the **private** key and stays on Windows.

**Login with password**

```powershell
ssh USERNAME@SERVER_IP
```

### 2. SSH key copy to server

When password SSH login is available, copy the public key from **PowerShell** (Windows does not normally include `ssh-copy-id`):

```powershell
type ~\.ssh\demo_ed25519.pub | ssh USERNAME@SERVER_IP "cat >> .ssh/autorized_keys"
```

**Safety:** Never copy the private key.

You can control the authorized_keys on the server:

```bash
cat ~/.ssh/authorized_keys
```


In a **new Windows PowerShell session**, test **key-only** login while keeping the existing server session open:

```powershell
ssh -i ~/.ssh/da/demo_ed25519 USERNAME@SERVER_IP
```

Successful login must **not** require the server account password. A private-key passphrase prompt is normal.

### 3. Disable SSH password login

> **Safety:** Only do this *after* a separate, new key-only SSH login has succeeded. Keep the original working SSH session open until the new login succeeds again after reloading SSH.

On the **Linux server**, edit sshd_config:

```bash
sudo nano /etc/ssh/sshd_config
```

Lock for:
```text
#PasswordAuthentication yes
```
and switch it to:

```text
PasswordAuthentication no
```

Safe the document and restart ssh.service:

```bash
sudo systemctl restart ssh.service
```

Open **another new** key-only SSH connection from Windows. Do not close the original session until successful verification.

You can test password authentication while try to login with the following code:

```powershell
ssh -o PubkeyAuthentication=no USERNAME@SERVER_IP
```

When password is disabled it will give us the feedback:

```powershell
USERNAME@SERVER_IP: Permission denied (publickey).
```

### 4. Install NGINX and serve a custom page

On the **Linux server**:

```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl status nginx.service
```
You can see the example page:

```bash
sudo cat /var/www/html/index.nginx-debian.html
```

Create a custom page as followed:

```bash
sudo mkdir /var/www/atlernatives
sudo touch /var/www/atlernatives/alternate-index.html
```

Update `/etc/nginx/sites-available/default` (for the default HTTP site) to serve the custom directory instead of the standard welcome page. Example server block:

```nginx
server {
    listen 8081 ;
    listen [::]:8081;

    root /var/www/alternatives;
    index alternate-index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Addd HTML code to the alternate-index.html:

```bash
sudo nano /var/www/alternatives/alternate-index.html
```

Example custom HTML page:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>V-Server</title>
</head>
<body>
  <h1>Welcome to my V-Server!</h1>
  <p>This page is served by NGINX.</p>
</body>
</html>
```

Restart the service:

```bash
sudo service nginx restart
```

The HTTP response for YOUR-IP-ADRESS:8081 should contain `Welcome to my V-Server!`. A public website should use HTTPS before handling sensitive information.

### 5. Configure Git on the server

Configure the server's Git commit author identity:

```bash
git config --global user.name "YOUR_GITHUB_USERNAME"
git config --global user.email  "YOUR_GITHUB_EMAIL"
```

Verify:

```bash
git config --global --get user.name
git config --global --get user.email
```

These settings identify Git commits; they are separate from the SSH account used for GitHub authentication.

### 6. Connect the server to GitHub

Generate a **different** key pair **on the Linux V-Server** for **V-Server → GitHub**:

```bash
ssh-keygen -t ed25519 -C "YOUR_GITHUB_EMAIL" -f ~/.ssh/github_ed25519
cat ~/.ssh/github_ed25519.pub
```

Do not overwrite an existing key pair. Add **only** the `.pub` file contents at [GitHub → Settings → SSH and GPG keys](https://github.com/settings/keys) as an *Authentication Key*.

Configure the SSH client on the server by adding/updating the following entry in `~/.ssh/config`:

```sshconfig
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_ed25519
    IdentitiesOnly yes
```

```bash
chmod 600 ~/.ssh/config
ssh -T git@github.com
```

On first connection, check GitHub's published SSH host key fingerprint before accepting it. A successful result for this project was:

```text
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

GitHub does not provide an interactive shell; exit code `1` is normal for this test.

To test repository access, use:

```bash
git ls-remote git@github.com:Tofa93/my-dso-blog.git HEAD
```

## Troubleshooting and Security

- `ssh-copy-id` missing in PowerShell: use `Get-Content ... | ssh ...` or an existing SSH console session.
- `Permission denied (publickey,password)`: verify the actual server user, SSH port, public key in `authorized_keys`, file permissions and private-key path. Compare the settings of different SSH clients.
- Logged out after changing SSH settings: use the hosting provider console to restore the previous working configuration.
- NGINX still shows the default page: check the active site configuration, `root` path, `index.html`, and `sudo nginx -t`.
- Keep **private keys, passwords and server secrets** out of Git and public documentation. Prefer a passphrase for private keys.

## References

- [OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh-overview)
- [Ubuntu OpenSSH server documentation](https://documentation.ubuntu.com/server/how-to/security/openssh-server/)
- [NGINX beginner's guide](https://nginx.org/en/docs/beginners_guide.html)
- [Git configuration](https://git-scm.com/docs/git-config)
- [GitHub: SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [GitHub: SSH authentication test](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)
- [Docusaurus project page](../../docs/projects/vserver-setup.md)
