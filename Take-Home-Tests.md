# DataSintesa DevOps Technical Test

## Take Home Tests



### 1. Generate VM CentOS

mengenerate VM CentOS melalui microsoft azure

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/fffe8b66-1a9c-4888-89c5-351312504859)

seteleh mengenerate kita masuk kedalam vm dengan perintah 
```
ssh -i oss.pem irwan@52.233.86.183
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/38911dbf-f907-48c9-add1-916a472002cc)

saya menggunkan VM versi CentOS Stream release 9

### 2. Menginstall Docker

saya menginstall docker untuk kebutuhan aplikasi seperti membuild aplikasi dan beberpa applikasi di jalankan on top docker

berikut prtintah untuk install docker:

1.Perbarui paket yang ada di sistem Anda:
```
sudo yum update -y
```
2.Instal beberapa paket yang diperlukan sebelum menginstal Docker
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
3.Tambahkan repository Docker ke sistem
```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```
4. Instal Docker menggunakan perintah berikut:
```
sudo yum install -y docker-ce docker-ce-cli containerd.io
```
5. Mulai layanan Docker dan aktifkan agar otomatis berjalan saat sistem dinyalakan:
```
sudo systemctl start docker
sudo systemctl enable docker
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/00b2b42e-1939-4530-afec-b8c41b65069e)


### 3. Build Aplikasi

1. membuat direktori oss dengan perintah

```
sudo mkdir /opt/oss
cd /opt/oss
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/074946d0-dc5e-4403-84ce-0ecb4805392a)

2. membuat index.js

```
sudo nano index.js
```
```
// Simple Express web server
// @see http://howtonode.org/getting-started-with-express
// Load the express module
var express = require('express');
var app = express();

// Respond to requests for / with 'Hello World'
app.get('/', function(req, res){
  res.send('Hello world!');
});

// Listen on port 80
app.listen(80, () => console.log('Express server started successfully.'));
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/cb598646-3551-4f54-8a9c-213485029c8d)

3. membuat file package.json

```
sudo nano package.json
```
```
{
  "name": "examplenodeapp",
  "description": "Example Express Node.js app.",
  "author": "dtndevopscandidate <devopscandidate@datasintesa.id>",
  "dependencies": {
    "express": "4.x"
  },
  "engine": "node >= 0.10.6"
}
```
![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/830544ff-ec6e-48ea-82dd-584389b650e3)

4. membuat Dockerfile

```
sudo nano Dockerfile
```
```
# Use the official Node.js image
FROM node:20.14.0-alpine

# Create and change to the app directory
WORKDIR /usr/src/app

# Copy package.json and install dependencies
COPY package.json ./
RUN npm install

# Copy the app source code
COPY . .

# Expose the port the app runs on
EXPOSE 80

# Run the app
CMD ["node", "index.js"]
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/2f0a659d-2892-4121-9714-865a91a36543)

5. membuat docker-compose.yml

```
services:
  web:
    build: .
    ports:
      - "80:80"
    depends_on:
      - db
    networks:
      - oss-net

  nginx:
    image: nginx:latest
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    ports:
      - "8080:80"
    depends_on:
      - web
    networks:
      - oss-net

  db:
    image: postgres:13
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - oss-net

networks:
  oss-net:

volumes:
  db_data:
```

6. membuat nginx.conf

```
events {
  worker_connections 1024;
}

http {
  server {
    listen 80;
    server_name oss-app.studentdumbways.my.id;

    location / {
      proxy_pass http://52.233.86.183:80;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
    }
  }
}
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/84820e5d-3094-4fef-907c-085a50216f23)

7. buat direktori baru bernama ```bin``` dan tambahkan script berikut

bin/start
```
#!/bin/bash

# Start the Express server, nginx, and postgresql

/usr/libexec/docker/cli-plugins/docker-compose up -d
```

bin/stop
```
#!/bin/bash

# Stop the Express server, nginx, and postgresql

/usr/libexec/docker/cli-plugins/docker-compose down
```

bin backup
```
TIMESTAMP=$(date +"%F")
BACKUP_DIR="/opt/oss/data/backups"
BACKUP_FILE="$BACKUP_DIR/backup_$TIMESTAMP.sql"

docker exec -t $(/usr/libexec/docker/cli-plugins/docker-compose ps -q db) pg_dumpall -c -U user > $BACKUP_FILE

echo "Backup saved to $BACKUP_FILE"
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/66d8665a-249b-4bed-bf31-bca1b798f6ec)

8. tambahkan perizinan agar dapat dieksekusi

```
chmod +x /bin/stop /bin/start /bin backup
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/d8ce7188-1228-4833-b84c-90e24575a5de)


9. Pastikan struktur direktori terlihat seperti ini
```
oss/
├── Dockerfile
├── index.js
├── docker-compose.yml
├── package.json
├── nginx.conf
└── bin/
    ├── start
    ├── stop
    └── backup
```

### 4. Mengeksekusi Aplikasi

1. menjalankan aplikasi dengan perintah

```
./bin/start
```
![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/d21b0f93-8079-44a0-9ce2-f59205b75fec)

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/9a2eef6b-5f59-40ce-8273-22f88000ef73)

2. menghentikan aplikasi dengan perintah

```
./bin/stop
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/4e2d5d5f-7ee6-448d-b595-22f11923b65e)

3. membackup data aplikasi dengan perintah

```
./bin/backup
```

![image](https://github.com/irwanpanai/DataSintesa-DevOps-Technical-Test/assets/89429810/6886431b-bbc7-4f5a-9d1a-6d6322753f16)
