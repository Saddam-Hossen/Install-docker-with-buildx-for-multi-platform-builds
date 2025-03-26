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

Let me know if you need further assistance! 🚀
