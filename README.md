
# Overview

A Docker (PHP + Nginx + MySQL) development environment tailored to my personal needs.

# License

This project is licensed under the MIT License.

# Author

**Leo B (dcomp7)**  
[Github profile](https://github.com/dcomp7)


# Installation Guide

1. Clone the repository using the command:
   ```bash
   git clone https://github.com/dcomp7/docker-php-box.git
   ```

2. Edit the `.env` file:

    - In the `APPLICATION` variable, replace the value `/home/box` with the absolute path to the `wwwroot` on your machine.
    - In the `APPLICATION_DATA` variable, replace the value `/home/box-data` with the absolute path to the directory where media content (images, server side cache, etc.) will be stored.

3. Start the container:
   ```bash
   docker-compose up -d
   ```

4. Once the container is running, execute Composer:
   ```bash
   docker exec -it php-fpm composer update
   ```

5. Add the domain `box.local` to your hosts file:

   Open the file with administrator privileges in your text editor:

    - On Linux: `/etc/hosts`
    - On macOS: `/private/etc/hosts`
    - On Windows: `C:\Windows\System32\drivers\etc\hosts`

   Then, add the following line:
   ```bash
   127.0.0.1 box.local
   ```

6. You're all set! Open the project in your browser at:
   ```
   http://box.local
   ```

# Usage Instructions

1. To start or stop the container:

    - Use `docker-compose up` to start the container.
    - Use `docker-compose down` to stop it.

2. To access the container’s shell:

    - On Linux/Mac:
      ```bash
      docker exec -it nginx bash
      docker exec -it php-fpm bash
      docker exec -it mysql bash
      ```

    - On Windows:
      ```bash
      winpty docker exec -it nginx bash
      winpty docker exec -it php-fpm bash
      winpty docker exec -it mysql bash
      ```

3. To access the MySQL database within the container:
   ```bash
   mysql -u root -p
   ```

# Additional Information

1. **Database Dumps:**

   Place the desired SQL dump file in the `./mysql/dumps` directory.

2. **Useful Docker Commands:**

    - `docker ps` → Lists all running containers.
    - `docker kill <id>` → Terminates a running container.

# Technical Specifications

1. **Stack:**

    - Nginx
    - MySQL
    - PHP-FPM

2. **Port Exposure:**

    - Nginx: 80 and 443
    - PHP-FPM: 9000
    - MySQL: 3306

3. **Directories and Paths:**

    - Logs: `./nginx/logs` (mapped to `/var/log/nginx`)
    - Virtual Hosts: `./nginx/sites` (mapped to `/etc/nginx/conf.d`)
    - MySQL Binary Tables: `./mysql/data`

