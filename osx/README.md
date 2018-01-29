# Running on OSX
OSX does not work well with Docker's `network_mode=host` setting. To mimic this behaviour, follow these steps:

* make sure you run the latest version of docker-compose ([up --no-start](https://docs.docker.com/compose/reference/up/) should be supported)
* run `docker-compose up --no-start`
* run `docker network inspect osx_default | grep Gateway` and copy the IP address
* replace each `localhost` entry in the `docker-compose.yml` file with that IP address

Instead of running the steps manually, you can run this oneliner:

`sed -i '' "s/\"localhost:.*\"/\"localhost:$(docker network inspect osx_default | grep Gateway | awk '{gsub(/"/, ""); print $2}')\"/" docker-compose.yml`