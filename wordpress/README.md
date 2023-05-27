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
3. Change ownership of db_data to www-data and USER `sudo chown -R www-data:${USER} ./db_data`
4. Change ownership of webdata to www-data:www-data: `sudo chown -R www-data:${USER} ./webdata`
5. Change ownership of docker-compose.yml to current user: `sudo chown -R ${USER}:${USER} docker-compose.yml`
### Step 2: Access the database and change the config of `old_domain` to `new_domain`:
1. Access docker-compose.yml file: `nano docker-compose.yml`
2. Replace `{domain}` to your domain
3. Exit and save
### Step 3: Access and change the domain in docker-compose.yml:
1. Access the mysql_container: `docker exec -it db_{domain} bash`
2. Access the mysql server: `mysql -u your_mysql_username -p`
3. Switch to database: `USE wordpress;`
4. Update old domain in wp_posts: `UPDATE wp_posts SET post_content = REPLACE(post_content, 'old-domain.com', 'new-domain.com');`
5. Update old domain in wp_options: `UPDATE wp_options SET option_value = REPLACE(option_value, 'old-domain.com', 'new-domain.com');`
6. Update old domain in wp_postmeta: `UPDATE wp_postmeta SET meta_value = REPLACE(meta_value, 'old-domain.com', 'new-domain.com');`
8. Exit: `exit;`
### Step 4: Run the stack:
1. Access back to folder `{new_foler}/`
2. Run: `docker-compose up -d`
