# GUIDES

## **Setup new stack**
### Step 1: Access and change domain:
1. Access docker-compose.yml file: `nano docker-compose.yml`
2. Replace `{domain}` to your domain
3. Exit and save
### Step2: Config environment variables:
`nano docker-compose.yml`
### Step 3: Run docker-compose:
`docker-compose up -d`

## **Clone to new stack**
### Step 1: Copy and change ownership root
1. Copy: `sudo cp -r <old_folder> <new_folder>`
2. Access to new folder: `cd <new_folder>`
3. Change ownership of mysql_data to 999:www-data: `sudo chown -R 999:www-data ./mysql_data`
4. Change ownership of webdata to www-data:www-data: `sudo chown -R www-data:www-data ./webdata`
5. Change ownership of docker-compose.yml to current user: `sudo chown -R ${USER}:${USER} docker-compose.yml`
### Step 2: Access and change the domain in docker-compose.yml:
1. Access docker-compose.yml file: `nano docker-compose.yml`
2. Replace `{domain}` to your domain
3. Exit and save
### Step 3: Change domain in config.php and admin/config.php:
1. Access config.php file: `cd webdata && sudo nano config.php`
2. Replace `<old_domain>` to `<your domain>`
3. Exit and save
4. Continue with admin/config.php
