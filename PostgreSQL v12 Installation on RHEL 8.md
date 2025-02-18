## PostgreSQL v12 Installation on RHEL 8 (Linux)

### Steps 1: 
Navigate to www.postgresql.org/downloads

### Step 2:  Select operating system as Linux.

### Step 3: Select appropriate Linux Distribution (In my case Red Hat).

### Step 4: Select Postgresql YUM Repositor link

### Step 5: Select Version 12 from available postgresql releases

### Step 6: Select “RHEL/Centos 8- x86_64” 

### Step 7 : Download “ pgdg-redhat-repo-42.0-11.noarch.rpm” from the list.

### Step 8: Install the downloaded rpm using the following syntax on the linux box:
      rpm -ivh pgdg-redhat-repo-42.0-11.noarch.rpm
    
### Step 9 :  Disable default postgresql on linux using the following syntax on the linux box:
      dnf -qy module disable postgresql 
### Step 10: Type the following command to list all available postgresql version.
       Yum list module postgresql
    
### Step 11: Look for postgresql v12 version.
    Yum list module postgresql12*
      

### Step 12: Install two packages from the postgresql12 list.
      Yum install postgresql12-server.x86_64 postgresql12-contrib.X86_64
      

### Step 13: Check the installation has completed successfully.
