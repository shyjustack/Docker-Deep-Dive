To install Docker on a server, you can follow these step-by-step instructions:

1. Update the system:
   ```
   sudo apt update
   sudo apt upgrade
   ```

2. Install dependencies to allow `apt` to use packages over HTTPS:
   ```
   sudo apt install apt-transport-https ca-certificates curl software-properties-common
   ```

3. Add the official Docker GPG key:
   ```
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

4. Add the Docker repository:
   - For x86_64/AMD64 architecture:
     ```
     echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
     ```

     For ARM64 architecture, you would use:
     ```
     echo "deb [arch=arm64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
     ```

5. Update the apt package index again:
   ```
   sudo apt update
   ```

6. Install Docker:
   ```
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```

7. Verify that Docker is installed correctly:
   ```
   sudo docker run hello-world
   ```

   If Docker is properly installed, you will see a "Hello from Docker!" message.

