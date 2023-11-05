# Mongo-Express-Docker
Learning the docker basics with hands-on. Creating mongo with networking and connecting mongo-express to mongo container in same network. 

First learned using cli & later this will be emulated in docker compose. 


Install Postgres with docker & specific version
docker run --name postgres-latest-version-138  -e POSTGRES_PASSWORD=mysecretpassword -d postgres:13.8

# Run Mongo container on a specific port
docker run --name my-mongo-one -p 5001:27017 -d mongo

# Run Mongo db in the specific network (db and app container needs to be on same network to communicate )
docker network create mongo-network 
docker run -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network -d mongo

# Run Mongo Express container in above mongo network, so they both can communicate
docker run -d  --network mongo-network -p 8081:8081 -e ME_CONFIG_MONGODB_SERVER=mongodb -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password   -e ME_CONFIG_BASICAUTH_USERNAME="user" -e ME_CONFIG_BASICAUTH_PASSWORD="fairly long password" --name mongo-express mongo-express

