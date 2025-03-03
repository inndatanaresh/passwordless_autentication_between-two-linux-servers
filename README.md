# Passwordless Authentication in Linux

## **Configuration Steps**

### **Master Server Setup**
1. Set the hostname for the master server:
   ```bash
   sudo hostnamectl set-hostname master-server
   ```

### **Slave Server Setup**

#### **Step 1: Generate SSH Key**
Run the following command on the slave server to generate an SSH key:
   ```bash
   ssh-keygen -t rsa
   ```
Press **Enter** three times to accept the default settings.

#### **Step 2: Copy Public Key to Master Server**
Copy the generated SSH public key to the master server:
   ```bash
   ssh-copy-id -i /home/<username>/.ssh/id_rsa.pub <username>@master-server
   ```
Replace `<username>` with the actual username.

#### **Step 3: Test Passwordless Login**
Try logging into the master server without a password:
   ```bash
   ssh master-server
   ```

---

## **Additional User Access**

- If another user needs access to the master server, they must first log in to the slave server using the IP address:
  ```bash
  ssh <username>@<slave-ip>
  ```
  Example:
  ```bash
  ssh divya@172.16.0.218
  ```
  
- After logging into the slave, they can access the master using the DNS name:
  ```bash
  ssh master-server
  ```

## **Purpose**

The main goal of this setup is:
- To avoid sharing passwords with third-party users.
- To ensure secure authentication without exposing the master server's IP address.
- Users will only need to use the master DNS name for access.

This setup enhances security while simplifying user authentication management.
