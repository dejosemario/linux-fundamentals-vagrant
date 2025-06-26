# linux-fundamentals-vagrant
This is a beginner-friendly project for learning Linux fundamentals using Vagrant. It includes tasks such as exploring the Linux file system, managing permissions, installing packages, and testing connectivity. 


## Technical Challenges Encountered

### Initial Setup Issue
I initially attempted to use Vagrant with VirtualBox as specified in the assignment. However, I encountered a compatibility conflict:

**Error encountered:**

**Root cause:**
- VirtualBox requires exclusive access to hardware virtualization
- Docker Desktop uses Hyper-V, which conflicts with VirtualBox
- WSL environment cannot access VirtualBox without special configuration

**Resolution:**
After researching the issue, I switched to using Docker as an alternative containerization solution. This provided the same learning environment (Ubuntu Linux) with identical system administration capabilities.

### Why Docker is a valid Alternative
- Provides isolated Ubuntu environment for learning
- Full root access for system administration tasks
- Same file system, permissions, and package management
- Industry-standard containerization technology
- No virtualization conflicts with existing Docker setup

## Assignment Completion

### 2. Set Up Ubuntu Server Environment

**Screenshot #1: Docker Container Initialization and Access**

![Docker Container Setup](screenshots/screenshot1.png)

**Description:**
This screenshot demonstrates setting up an Ubuntu Linux environment using Docker as an alternative to Vagrant. The process includes:

1. **Checking container status** with `docker ps -a` - showing the existing "linux-fundamentals" container
2. **Starting the container** with `docker start linux-fundamentals` 
3. **Accessing the environment** with `docker exec -it linux-fundamentals /bin/bash`
4. **Confirming access** as root user in the Ubuntu environment

**SSH Alternative:** Unlike Vagrant which requires SSH to access the virtual machine, Docker provides direct access to the container through the `docker exec` command. This eliminates the need for SSH configuration while providing the same isolated Linux environment for system administration practice.

### 3. Explore the Linux File System

**Screenshot #2: Custom Folder Structure Creation**

![Linux Directory Structure](screenshots/screenshot2.png)

**Description:**
This screenshot shows exploring the Linux file system and creating a custom directory structure. The commands demonstrate:

1. **Navigation** to `/home` directory
2. **Creating nested directories** with `mkdir -p vagrant/projects/devops`
3. **Listing directory contents** with `ls -la` to verify the folder structure
4. **The created structure**: `/home/vagrant/projects/devops`

The `-p` flag in `mkdir` creates parent directories as needed, which is essential for creating nested directory structures in a single command.

### 4. Manage File Permissions and Ownership

**Screenshot #3: File Permissions and Ownership Management**

![File Permissions and Ownership](screenshots/screenshot3.png)

**Description:**
This screenshot demonstrates Linux file permissions and ownership management using `chmod` and `chown` commands. The sequence shows:

1. **File Creation**: Created `test-file.txt` and `another-file.txt` with default permissions
2. **Initial Permissions**: Files created with `-rw-r--r--` (644) permissions - owner can read/write, group and others can only read
3. **Permission Changes with chmod**:
   - `chmod 740 test-file.txt` - Changed to `-rwxr-----` (owner: read/write/execute, group: read, others: no access)
   - `chmod 755 another-file.txt` - Changed to `-rwxr-xr-x` (owner: read/write/execute, group/others: read/execute)
4. **User Creation**: Added `testuser` using `useradd testuser`
5. **Ownership Changes with chown**:
   - `chown testuser test-file.txt` - Changed owner from `root` to `testuser`
   - `chown testuser:testuser another-file.txt` - Changed both owner and group to `testuser`

**Permission Values Explained:**
- **740**: Owner (7=rwx), Group (4=r--), Others (0=---)
- **755**: Owner (7=rwx), Group (5=r-x), Others (5=r-x)
- The first character indicates file type (- for regular file, d for directory)
- Following 9 characters represent permissions in groups of 3: owner, group, others
- Each group uses rwx notation: r=read(4), w=write(2), x=execute(1)


**Ownership Format**: `owner:group` - shows who owns the file and which group has group permissions.

