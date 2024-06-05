 ## IP 2: Creating a Basic Micro-service (docker-compose)
 
This configuration sets up a basic micro-service architecture with MongoDB as the database, a backend service, and a client service, each running in its respective container.
The containers are connected using a custom network for communication between the different container
Custom volumes are used to ensure data persistence even when containers are deleted, the volume are linked to the db service and backend service

 ### How to Run

To run the micro-service, follow these steps:

1. **Build the Containers:**
   ```bash
   docker-compose build

2. **Start and Run the Containers**
   ```bash
   docker-compose up

### Summary of the configuration file (docker-compose.yml)

The `docker-compose.yml` file defines the configuration for orchestrating the deployment of the micro-service. 
It includes the specifications for running the necessary containers and configuring their interactions.

**Key Components:**

1. **db Service:**
   - MongoDB service defined with the latest MongoDB image being pulled from dockerhub.
   - It is exposed at port `27017`.
   - Container to be created will be named `mongodb_container`.
   - For data persistence, data volume is made and mounted at `yolo_volumes/data/mongodb`.
   
2. **backend Service:**
   - Container to be created will be named `backend_container`.
   - Image from my dockerhub account: `jmaisiba/yolo_backend_image:v1.0.4`.
   - It is exposed at port `5000`.
   - Depends on the `db` service hence the db container will run first.
   - Container has persistent volume mounted at `yolo_volumes/data/backend`.

3. **client Service:**
   - Container to be created will be named: `client_container`.
   - Image from my dockerhub account: `jmaisiba/yolo_client_image:v1.1.0`.
   - It is exposed port `80`.
   - Restarts on failure.
   - Depends on the `db` and `backend` services hence this container starts last.

**Networks:**
- A custom network called `yolo_network` is used with a bridge network driver.

**Volumes:**
- For persistence of data I create a volume called `yolo_volumes` to store data for db and backend volume is defined.

