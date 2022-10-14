 # Docker Beispiel code
docker run -d -p 80:80 docker/getting-started

docker run -dp 3000:3000 \
    -w /app -v "$(pwd):/app" \
    node:12-alpine \
    sh -c "yarn install && yarn run dev"

# Flags
 - d # run in detached mode / background
 - p 80:80 # map to port 80 of the host to port 80 in the container
 docker/getting-started # the image to use
 - w /app # sets the container's present working directory where the command will run from
 - v "$(pwd):/app" - bind mount (link) the host's present getting-started/app directory to the container's /app directory
 - sh -c "yarn install && yarn run dev" - volume mapping

 # Build Container Image
 docker build -t getting-started .

 # Run the Container
 docker run -dp 3000:3000 getting-started

 # Run Container in Ubuntu
 docker run -it ubuntu ls /

 # Run Docker Compose
 docker-compose up -d

 # Exit program
 exit

 # Logs
 docker logs -f <container-id>
 docker-compose logs -f

 # ID of Container
 docker ps

 # Stop Container
 docker stop 49d81349f070 #Container ID

 # Remove Container
 docker rm 49d81349f070 #Container ID

 # Combined Command Stop and Remove
 docker rm -f <container-id>

 # Push repo on Docker
 docker push matthiasf1271/getting-started:tagname #tagname -> benennen

 # Login to Docker
 docker login -u name

 # Tag
 docker tag getting-started matthiasf1271/getting-started

 # Create a Filename in Ubuntu
 docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"

 # View the inheritance of data.txt
 docker exec <container-id> cat /data.txt

 # Create a named Volume
 docker volume create todo-db

# Create a Volume with volume mount
docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started

# Create a Network
docker network create todo-app # todo-app => name

# Defining MySQL service
docker run -d \
    --network todo-app --network-alias mysql --platform linux/amd64 \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:5.7

docker run -it --network todo-app nicolaka/netshoot

# Connect MySQL Database
docker exec -it 24cbf1d06e4b mysql -p # 24cbf1d06e4b => MYSQL Container

# Show Database
mysql> SHOW DATABASES;

# Show Items
mysql> select * from todo_items;

# Inside nicolaka find IP Adress
dig mysql

# -Running app with MySQL
docker run -dp 3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:12-alpine \
  sh -c "apk --no-cache --virtual build-dependencies add python2 make g++ && yarn install && yarn run dev"

  # Flags
  
    - MYSQL_HOST - the hostname for the running MySQL server
    - MYSQL_USER - the username to use for the connection
    - MYSQL_PASSWORD - the password to use for the connection
    - MYSQL_DB - the database to use once connected

  # Security Scanning
  docker scan getting-started # getting-started => image to scan

  # History
  docker image history getting-started # s.o.
