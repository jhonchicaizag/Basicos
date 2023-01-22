# docker-compose para instalar una base de datos en MONGO DB
# mongodb://root:admin@localhost:27017/    ==>   se usa para conectar con gestores (studio 3t, TablePlus) locales   
version: '3.1'

services:
  mongo:
    image: mongo
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: admin
    volumes:
      - ./mongodb:/data/db
    ports:
      - 27017:27017

  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: admin
      ME_CONFIG_MONGODB_SERVER: mongo
      ME_CONFIG_MONGODB_ENABLE_ADMIN: true

networks:
  default:
    name: mongodb_network