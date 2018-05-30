---
layout: post
title:  "Migrate Heroku Data to Docker Container"
categories: blog
---

I'm in the process of migrating a project from Heroku to Digital Ocean. In the process, I wanted to finally use Docker to containerize the project.

After getting the code setup, there is the issue of migrating the data from my Heroku Postgres database to my Postgres Container.

2 issues:

- copying the data dump into the container
- how to copy the data over


docker cp foo.txt mycontainer:/foo.txt

docker exec <container_name> pg_restore --verbose --clean --no-acl --no-owner -h postgres --dbname=postgresql://<user>:<password>@127.0.0.1:<port>/<db_name> latest.dump


Why is this the solution
- docker exec to run command within the container
- pg_restore to restore the data from the dump file
- --verbose --clean --no-acl --no-owner are all options
-h postgres is host

--dbname=postgresql://<user>:<password>@127.0.0.1:<port>/<db_name> is specifying the db

YOu can get around this with a .pgpass file and setting it to chmod 600.
 I was unable to get that to work so I found a solution to pass the password in the command.
