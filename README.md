# Docker_

DEMO PROJECT: Developing with Containers

	1. JS and Nodejs application <backend>
	2. Connect to a Docker Container with a MongoDB database.
	
	> Frontend/Backend: HTML, JS, NodeJS -> localhost:3000/my-app
	> To integrate to a DB: MongoDB Container
	> To make interactions easier / not use the terminal: Deploy MongoExpress [UI-container]: from here we can see, DB structure and all the updates our container is making in the DB. -> localhost:8081/db/my-db
	
	DOCKER NETWORK
Docker creates an isolated docker network where containers run in.
Containers inside this network communicate with each other using names

1. create network for the mongo-DB/UI
	docker network create <name_of_a_network>
	
	for express to connect to the DB,we need a user name and password
2. Start MongoDB	
	docker run -d \ : start in dettached mode
> -p 27017:27017 \ : open host port
> -e MONGO_INITDB_ROOT_USERNAME=mongoadmin \ : username for mongodb
> -e MONGO_INITDB_ROOT_PASSWORD=secret \ : password for mongodb
> --name mongodb \ : overwrite the name of the container
> --net mongo-network \ : container runs in mongo network
> mongo : name of the image

3. Start Mongo_Express
-> should connect to the mongodb container on startup
	
	docker run -d \
> -p 8081:8081 \ : run on our local port 8081
> -e ME_CONFIG_MONGODB_ADMINUSERNAME=mongoadmin \
> -e ME_CONFIG_MONGODB_ADMINPASSWORD=secret \
> --net mongo-network \
> --name mongo-express \ : overwite name of the container
> -e ME_CONFIG_MONGODB_SERVER=mongodb \ : define the serverDB name its to run on
> mongo-express : name of the image

Create a mongo express DB from the UI: Mongo Express server listening at http://0.0.0.0:8081

4. Connect our NodeJS to the Database : Done by <see code>
