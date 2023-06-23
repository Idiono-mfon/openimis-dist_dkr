doctl compute ssh openimis-vm --ssh-key-path ~/.ssh/id_rsa.pub (To Login to VM)
ssh -i ~/Documents/deployments/.ssh/id_rsa idysman@143.198.111.7 (login as idysman)

how to install docker compose in ubuntu 22.0

To install Docker Compose on Ubuntu 22.04, you can follow these steps:

1. **Update package lists**: First, update the package lists on your Ubuntu system by running the following command:

   ```
   sudo apt update
   ```

2. **Install dependencies**: Docker Compose requires some dependencies to be installed. Install them by running the following command:

   ```
   sudo apt install -y curl unzip
   ```

3. **Download Docker Compose**: Download the Docker Compose binary by using the `curl` command. The following command downloads the latest stable version:

   ```
   sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

   This command downloads the Docker Compose binary and saves it as `/usr/local/bin/docker-compose`.

4. **Set executable permissions**: Make the downloaded binary executable by running the following command:

   ```
   sudo chmod +x /usr/local/bin/docker-compose
   ```

5. **Verify installation**: Verify that Docker Compose is installed correctly by checking its version:

   ```
   docker-compose --version
   ```

   This command displays the version of Docker Compose installed on your system, confirming a successful installation.

That's it! Docker Compose should now be installed on your Ubuntu 22.04 system. You can now use it to manage your multi-container Docker applications.

##To update ocker permission
sudo chmod 666 /var/run/docker.sock

To specify the SSH path on OpenSSH, you can use the `ssh` command-line tool with the `-i` flag. The `-i` flag allows you to specify the path to the private key file to use for authentication. Here's how you can do it:

```
ssh -i /path/to/private_key_file user@host
```

Replace `/path/to/private_key_file` with the actual path to your private key file. For example, if your private key file is located in the home directory and named `id_rsa`, the command would be:

```
ssh -i ~/.ssh/id_rsa user@host
```

Here, `~/.ssh/id_rsa` represents the path to the private key file.

By specifying the SSH path using the `-i` flag, you can use a specific private key for authentication instead of the default key(s) in the default location (`~/.ssh/id_rsa` or `~/.ssh/id_dsa`). This is useful when you have multiple SSH key pairs and need to use a specific key for a particular host or user.

Note: Make sure the specified private key file has the appropriate permissions (`chmod 600 /path/to/private_key_file`) to ensure that only the owner can read and write to the file.

To add an SSH key for another user as the root user on a Linux VM, you can follow these steps:

1. **Connect to the Linux VM**: Use an SSH client, such as Terminal on macOS or PuTTY on Windows, to connect to your Linux VM. You'll need the IP address of the VM and the SSH credentials (username and password or SSH key) you used when setting up the VM.

   ```
   ssh root@vm_ip_address
   ```

   Replace `root` with the username for the root user, and `vm_ip_address` with the IP address of your Linux VM.

2. **Switch to the user account**: Once you have logged in as the root user, you need to switch to the user account for which you want to add the SSH key.

   ```
   su - target_username
   ```

   Replace `target_username` with the username of the user for whom you want to add the SSH key.

3. **Create the SSH directory**: If the user doesn't already have an SSH directory, you can create it using the following command:

   ```
   mkdir -p ~/.ssh
   ```

   This command creates a directory called `.ssh` in the user's home directory (`~`).

4. **Set the correct permissions**: Set the correct permissions for the SSH directory and the `authorized_keys` file within it. Incorrect permissions can prevent SSH key authentication from working.

   ```
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

   The first command sets the permissions for the `.ssh` directory, and the second command sets the permissions for the `authorized_keys` file.

5. **Add the SSH key**: Open the `authorized_keys` file in a text editor and paste the contents of the SSH public key that you want to add. You can use a command-line text editor like `nano` or `vi` to edit the file:

   ```
   nano ~/.ssh/authorized_keys
   ```

   Paste the SSH public key into the editor, then save and exit the file.

6. **Set the correct permissions (again)**: After adding the SSH key, ensure that the correct permissions are set for the `authorized_keys` file.

   ```
   chmod 600 ~/.ssh/authorized_keys
   ```

   This command ensures that only the user has read and write permissions for the `authorized_keys` file.

7. **Exit the user account**: Once you have added the SSH key, you can exit the user account and return to the root user.

   ```
   exit
   ```

   This command exits the current user account and returns to the root user account.

That's it! You have successfully added an SSH key for another user as the root user on a Linux VM. The user can now use the SSH key for authentication when connecting to the VM.

To create a user account on a DigitalOcean Droplet after its creation, you can follow these steps:

1. **Connect to the Droplet**: Use an SSH client, such as Terminal on macOS or PuTTY on Windows, to connect to your Droplet. You'll need the IP address of the Droplet and the SSH credentials (username and password or SSH key) you used when creating the Droplet.

   ```
   ssh username@droplet_ip_address
   ```

   Replace `username` with the username you want to create, and `droplet_ip_address` with the IP address of your Droplet.

2. **Switch to the root user**: Once you have logged in as the initial user (such as "root"), you need to switch to the root user account to perform administrative tasks.

   ```
   sudo su -
   ```

   Enter the password for the initial user (or the SSH key passphrase if applicable) when prompted.

3. **Create a new user**: Use the `adduser` command to create a new user account. You'll be prompted to enter a username and password for the new user.

   ```
   adduser new_username
   ```

   Follow the prompts to set the password and any additional information requested.

4. **Grant administrative privileges**: To allow the new user to run commands with administrative privileges (sudo), you need to add them to the `sudo` group.

   ```
   usermod -aG sudo new_username
   ```

   This command adds the user to the `sudo` group, which grants administrative privileges.

5. **(Optional) Set up SSH key authentication (recommended)**: If you prefer to use SSH key authentication instead of passwords, you can generate an SSH key pair on your local machine and add the public key to the new user's `authorized_keys` file. This allows you to log in to the Droplet using the private key associated with the public key you added.

   On your local machine, generate an SSH key pair if you haven't already:

   ```
   ssh-keygen -t rsa -b 4096
   ```

   Then, copy the public key to the new user's `.ssh/authorized_keys` file on the Droplet:

   ```
   ssh-copy-id new_username@droplet_ip_address
   ```

   Replace `new_username` with the username you created, and `droplet_ip_address` with the IP address of your Droplet.

That's it! You have successfully created a new user account on your DigitalOcean Droplet. You can now log out from the root user and log in with the newly created user account:

```
exit
ssh new_username@droplet_ip_address
```

Replace `new_username` with the username you created, and `droplet_ip_address` with the IP address of your Droplet.

To access your Node.js application deployed on a DigitalOcean Droplet from the internet, you need to follow these steps:

1. **Ensure your application is running**: Make sure your Node.js application is up and running on the Droplet. You can verify this by connecting to the Droplet using SSH and checking if the application process is active.

2. **Configure firewall**: By default, DigitalOcean Droplets have a firewall enabled. You need to allow incoming traffic on the port your Node.js application is listening on. Typically, Node.js applications use port 3000, but you may have configured it differently. To open the port, you can use the following command:

   ```
   sudo ufw allow <port_number>
   ```

   Replace `<port_number>` with the actual port your Node.js application is using.

3. **Configure DNS**: If you have a domain name, you need to configure the DNS settings to point to your Droplet's IP address. This step allows users to access your application using a domain name instead of the IP address. To do this, log in to your domain registrar's website (where you purchased the domain) and set the DNS A record to your Droplet's IP address.

4. **Access the application**: Once you have completed the above steps, you should be able to access your Node.js application using either the Droplet's IP address or the domain name. Open a web browser and enter the IP address or domain name followed by the port number (if it's not the default port 80). For example:

   ```
   http://<droplet_ip_address>:<port_number>
   ```

   or

   ```
   http://<your_domain_name>:<port_number>
   ```

   Replace `<droplet_ip_address>` with your Droplet's IP address, `<port_number>` with the port your application is listening on, and `<your_domain_name>` with your domain name (if you have one).

That's it! You should now be able to access your Node.js application deployed on the DigitalOcean Droplet from the internet.

To remove all Docker images with a single command, you can use the `docker rmi` command along with the `$(docker images -q)` command substitution. Here's the command you can use:

```shell
$ docker rmi $(docker images -q)
```

Explanation of the command:

1. `docker images -q` lists all the Docker image IDs in the system.

2. `$(docker images -q)` is a command substitution that substitutes the output of `docker images -q` as arguments to the `docker rmi` command.

3. `docker rmi` removes the specified Docker images.

By running the above command, all Docker images present on your system will be removed. Please note that this action is irreversible, so ensure you want to delete all images before executing this command. Additionally, be cautious as it will remove all images, including the ones required for other containers or applications to function correctly.

To remove all stopped containers on your system, you can use the Docker command-line interface (CLI). Here's how you can do it:

1. Open your preferred terminal or command prompt.

2. Run the following command to list all containers on your system, including the stopped ones:

   ```
   docker ps -a
   ```

   This will display a list of all containers along with their statuses (running or stopped).

3. If you want to remove all the stopped containers, you can use the following command:

   ```
   docker container prune
   ```

   This command will remove all stopped containers from your system. Docker will prompt for confirmation before deleting the containers.

   Alternatively, if you want to remove both stopped containers and unused images, you can use the following command:

   ```
   docker system prune
   ```

   Docker will ask for confirmation before removing the stopped containers, unused images, and any other unused resources.

4. Confirm the action by typing "y" or "yes" when prompted.

   Docker will proceed to remove the stopped containers, freeing up disk space on your system.

Please note that removing containers will permanently delete them, and any data stored inside them will be lost. Make sure to back up any important data before removing containers.

To delete all Docker volumes, you can follow these steps:

1. Stop and remove all Docker containers:

   ```
   docker stop $(docker ps -a -q)
   docker rm $(docker ps -a -q)
   ```

2. Remove all Docker volumes:

   ```
   docker volume rm $(docker volume ls -q)
   ```

   This command uses `docker volume ls` to list all volumes and `docker volume rm` to remove them.

3. Verify that all volumes have been deleted:

   ```
   docker volume ls
   ```

   After running this command, you should see an empty list of volumes, indicating that they have been successfully deleted.

Please note that deleting Docker volumes will permanently remove all data stored in those volumes. Make sure you have a backup of any important data before proceeding with these steps.

Delete the Docker cache directory:

bash
Copy code
sudo rm -rf /var/lib/docker/
This command removes the entire Docker cache directory and its contents. Please note that using sudo is necessary to ensure proper permissions for deleting system files.

Restart Docker:

Copy code
sudo service docker restart

yeah @Mobolaji Fayomade basically, the recommended docker image for the database is throwing errors when the backend triggers a connection request. Therefore, a 502 gateway error is return as a response to the client upon making request to the backend. I am working on resolving this using the local deployment setup as a guide today

Goal:

Deploy openIMIS service

Milestones:
Application deployed but accessing it throws a 502 gateway error

Description:

After deploying the required docker images for OpenIMIS on a VM, the service throws a 502 gateway error when accessing it from the frontend. Debbuging the issue shows that the backend is unable to connect with the database container, therefore returns a 502 error to the client. Moreover, subsequent checks on the repository shows that the current version of the openIMIS has been updated and varies from the copy that previously deployed succesfully on the local environment. Though further debugging is stil ongoing, we can conclude to a reasonable extent that the erorr is from the latest docker images provided by the development team of OpenIMIS.

Current solution steps:

Redploy the services again and try tracing the issues related to the database connection
Redployed the previous version of the service (currently trying this)
Escalate to OpenIMIS support team

docker-compose -f docker-compose-mssql.yml up
