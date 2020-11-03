## Mounting a volume with containers file in docker-compose

`docker-compose.yml`

The issue was that whenever you specified a volume inside the containers it replaces the content of the folder inside the container (as it's supposed to do so). If you wish to avoid this you will need to create a docker volume and mount it to the container.

In this example we mount the */etc/nginx* to a local path (*/home/contre/ser/nginx*) 

```yml
version: "3.2" 
services:
  web:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - type: volume
        source: nginx
        target: /etc/nginx
        volume:
          nocopy: true

volumes:
  nginx:
    driver: local
    driver_opts:
        type: none
        o: bind
        device: /home/contre/ser/nginx
```

*Source: https://stackoverflow.com/questions/47664107/docker-mount-to-folder-overriding-content*

What you will get is on startup, the host folder will be empty and the files from the image will be "copied" onto the host folder. Editing files in *host path* will be relected inside the container and similarly files edited inside the container */container/path* will be reflected in *host path* on the host.