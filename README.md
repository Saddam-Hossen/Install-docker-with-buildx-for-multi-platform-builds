# Install-docker-with-buildx-for-multi-platform-builds

It looks like you're manually adding the Docker repository to your **Ubuntu 24.04.2 LTS** system. If you're setting up Docker, follow these steps to ensure everything is configured correctly:

### **Step 1: Install Required Dependencies**
Before proceeding, install necessary dependencies:
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg
```

### **Step 2: Add Docker’s Official GPG Key**
You've already run this command, but to confirm:
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### **Step 3: Add the Docker Repository**
You've correctly set up the repository:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### **Step 4: Update Package List**
```bash
sudo apt update
```

### **Step 5: Install Docker and Buildx**
Now, install Docker, including **Buildx** and **Compose**:
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### **Step 6: Start and Enable Docker**
```bash
sudo systemctl enable --now docker
```

### **Step 7: Verify Installation**
Check if Docker and Buildx are installed:
```bash
docker --version
docker buildx version
```




saddamnvn@DESKTOP-PTTGD06:~$ docker ps -a
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.49/containers/json?all=1": dial unix /var/run/docker.sock: connect: permission denied

```
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock
```

means your current user (`saddamnvn`) doesn't have permission to access the Docker daemon.

---

### ✅ Fix: Add your user to the `docker` group

Run the following command:

```bash
sudo usermod -aG docker $USER
```

Then **log out and log back in** (or reboot) to apply the group changes.

> 💡 Alternatively, you can run `newgrp docker` in the same session to apply it immediately without rebooting.

---

### 🔁 Then try again:
```bash
docker info
```

It should now show the full Docker server info without any permission errors.

---

Let me know if you're planning to use this with **VS Code Remote - SSH** or directly from Linux VS Code, and I’ll help configure that next.
