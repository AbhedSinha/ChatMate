### Full Stack Social Media App (in-progress)
Trying to develop full-stack flutter application with `dart_frog` as backend

- client/
    - it's the flutter app
- server/
    - it's the `dart` server
    - packages/db
        - it's the package talking to the `postgres`
    - packages/shared
        - it's the shared code base among server and client, the purpose of using dart as backend and flutter on front-end is justified here.

### 🎨 Design
Inspiration --> https://dribbble.com/shots/18340567-Sosmad-Social-Media-App

### Under Development Project


### 🧰 Developer Setup
This project is running on local environment because I'm just learning and playing with it. Hence, you might need to setup some stuff other than flutter/dart to get it up and running.

### 🐟 Docker Setup
Don't delete the file `server/docket-compose.yaml` ;p and don't worry about it if you don't know about what is docker and how it works. I didn't knew it either, so cheer up! 😁

Step 1: Install docker

Step 2: Fire up the docker app once its installed

Step 3: Run the comment in `server/`
```
docker-compose up -d
```
You should see the following outputs that shows your database has been created and ready to use!

```
hamza@M1-Max server % docker-compose up -d
[+] Running 15/1
 ✔ postgres 14 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                                                                                                                   76.5s 
[+] Running 1/3
 ⠦ Network server_default        Created                                                                                                                                         0.5s 
 ⠴ Volume "server_postgres"      Created                                                                                                                                         0.5s 
 ✔ Container postgres_container  Started  
```

Just to verify, try:
```
docker container ls

CONTAINER ID   IMAGE      COMMAND                  CREATED              STATUS              PORTS                    NAMES
f7dce227ee38   postgres   "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:5432->5432/tcp   postgres_container
```
### 🐘 Postico/Postgres Admin setup
Now we need a client for our DB management, postgres admin and postico are pretty famous for this purpose So,

Step 1: Simply install Postico or Postgres Admin to manage your DB

NOTE: Postico is available only for mac

Step 2: Create a server and make sure `username` and `password` are same as in `server/routes/_middleware.dart`

NOTE: Don't do this for production server, I've added a comment to pull these creds. from cloud or .env something. This is just for learning purposes

Step 3: Click on `Test` once you have setup the creds to make sure you've everything working

Step 4: `Connect` and we have our backend setup locally to play with `dart_frog` 🚀

### 👨🏼‍💻 ORM (Stormberry)
You can use any ORM as per your preference, I'm just using `stormberry` because I was following flutter observeable series. So, its a dart package and it has pretty detailed documentation for everything you need.

Step 1: Now we need connect our ORM to our DB and for that run the following and make sure you are in `db/` this time:
```
DB_SSL=false DB_SOCKET=false DB_PASSWORD=changeme dart run stormberry migrate
```
Now, enter the name of db which is "postgres" and keep pressing "enter" for default values and lastly, just press "yes" and onwards to create your tables in postgres SQL

```
Building package executable... (1.0s)
Built stormberry:stormberry.
Select a database to update: postgres
Enter the database host address: 
Enter the database port: 
Enter the database username: 
Getting schema changes of postgres
=========================
++ TABLE posts
++ TABLE comments
++ TABLE users
++ TABLE stories
=========================
Do you want to apply these changes? (yes/no): yes
Database schema changed, applying updates now:
---
CREATE TABLE IF NOT EXISTS "posts" (
"id" serial NOT NULL,"uid" int8 NOT NULL,"caption" text NOT NULL,"has_image" boolean NULL,"image_url" text NULL,"has_video" boolean NULL,"video_url" text NULL,"likes" _int8 NOT NULL,"comments" _int8 NOT NULL,"created_at" timestamp NOT NULL
)
---
CREATE TABLE IF NOT EXISTS "comments" (
"id" serial NOT NULL,"uid" int8 NOT NULL,"content" text NOT NULL,"created_at" timestamp NOT NULL
)
---
CREATE TABLE IF NOT EXISTS "users" (
"id" serial NOT NULL,"first_name" text NOT NULL,"followers" _int8 NOT NULL,"following" _int8 NOT NULL,"posts" _int8 NOT NULL,"stories" _int8 NOT NULL,"last_name" text NOT NULL,"username" text NOT NULL,"email" text NOT NULL,"password" text NOT NULL,"bio" text NULL,"birthday" timestamp NULL,"image_url" text NOT NULL,"cover_url" text NOT NULL
)
---
CREATE TABLE IF NOT EXISTS "stories" (
"id" serial NOT NULL,"uid" int8 NOT NULL,"has_image" boolean NULL,"image_url" text NULL,"has_video" boolean NULL,"video_url" text NULL,"created_at" timestamp NOT NULL
)
---
ALTER TABLE "posts"
ADD PRIMARY KEY ( "id" )
---
ALTER TABLE "comments"
ADD PRIMARY KEY ( "id" )
---
ALTER TABLE "users"
ADD PRIMARY KEY ( "id" )
---
ALTER TABLE "stories"
ADD PRIMARY KEY ( "id" )
========================
---
DATABASE UPDATE SUCCESSFUL
```
And on refreshing postico/postgres admin.... 🥁🥁🥁🥁

Congrats! The setup is completed and you are good to go. Keep playing, fix my bugs, open PRs and enjoy!

## 🔑 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE.md) file for details

## 🧑 Author

#### Abhed Sinha

If you liked the repo then kindly support it by giving it a star ⭐!
