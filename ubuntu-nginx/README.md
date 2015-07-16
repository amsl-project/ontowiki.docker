To use amsl within a the docker container you have to clone the repository to a path of your choice. Afterwards, you'll be able to run the downloaded amsl within docker. This allows for development on your PC's drive while amsl is running in the container. If you want to have access to e.g. the sparql endpoint make sure to expose the port 8890 for the web gui and 1111 for the isql connection.

create with

    $ docker build -t ontowiki .

run with (maps internal port 80 to your local port 8080, same for 8890 to 8891)

    $ docker run -t -i -p 8080:80 -p 8891:8890 -v /path/to/amsl/:/var/www/ --name ontowiki ontowiki

This also mounts your local amsl directory to the internal webserver directory.

If you want to read another log than ontowiki.log you'll have to connect into the docker container with 

	$ docker exec -it ontowiki bash

You'll then get a bash prompt where you can navigate to other logfiles like in /var/log/...

Run as a user, which is in the docker group or with `sudo`.
