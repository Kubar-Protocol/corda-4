
# Setting up Corda 4 Network

This project demonstrates a basic CorDapp running on Corda Community Edition 4.10. The sample network includes one notary and two nodes (PartyA and PartyB) that can issue and agree on simple IOU transactions.

## Prerequisites

- **Java 8** (Corda 4.10 requires Java 8)
- **IntelliJ IDEA** (Community Edition or higher)
- **Gradle** (use the provided Gradle wrapper)
- **Git**

## Quick Start

### 1. Download the Sample CorDapp

Clone the repository containing the sample CorDapp:


### 2. Open in IntelliJ IDEA

- Open IntelliJ and select **File > Open**.
- When prompted, import the project as a Gradle project.

### 3. Deploy the Nodes

From the project root, run the Gradle task to deploy nodes:
# On Unix/macOS:
./gradlew deployNodes

# On Windows:
gradlew.bat deployNodes

This creates a set of node directories (e.g., under `build/nodes`) with the sample CorDapp installed.

### 4. Launch the Network

Start the nodes by running the provided script:

# On Unix/macOS:
./build/nodes/runnodes

# On Windows:
.\build\nodes\runnodes.bat

Additionally, start the Spring Boot servers for PartyA and PartyB:

# For PartyA:
./gradlew runPartyAServer

# For PartyB:
./gradlew runPartyBServer


### 5. Interact with the CorDapp

You can interact with the running CorDapp in several ways:
- **HTTP Endpoints:**  
  Access the web endpoints (e.g., PartyA on `http://localhost:50005` and PartyB on `http://localhost:50006`) to view details or create IOUs.
- **Interactive Shell:**  
  Use the Corda shell (displayed in the terminal) to run flows (e.g., `flow start ExampleFlow$Initiator ...`).
- **H2 Web Console:**  
  Connect directly to a node’s database to inspect stored states and transactions.

### 6. Testing

Run the available integration, contract, and flow tests from IntelliJ or via Gradle to verify the CorDapp functionality.

Below is an example of a short README-style documentation you can share with others. It explains the prerequisites, how to build the container image (if needed), and how to run the containerized application.

---

# Cordapp Clients – Containerized Application

This document describes how to run the containerized Cordapp Clients application using Docker. The application is built with Gradle and packaged into an executable jar file. The Docker image uses Eclipse Temurin’s JDK 8 runtime.

## Prerequisites

- **Docker:** Ensure Docker is installed on your system.  
  [Get Docker](https://docs.docker.com/get-docker/)

- **Access to the Source or Pre-built Image:**  
  Either build the Docker image yourself (instructions below) or pull the image from a container registry if available.

## Building the Application

1. **Generate the Executable Jar:**  
   In the project root, run:
   ```shell
   ./gradlew clean jar
   ```
   This creates an executable jar in the `build/libs/` folder (e.g. `cordapp-example-0.1.jar`). Make sure your `build.gradle` includes a manifest with your main class:
   ```groovy
   jar {
       manifest {
           attributes(
               'Main-Class': 'com.example.Main'  // Replace with your main class
           )
       }
   }
   ```

2. **Build the Docker Image:**  
   From the project root (where the Dockerfile is located), run:
   ```shell
   docker build -t cordapp-clients .
   ```

## Running the Container

1. **Run the Docker Container:**  
   Use the following command to start the container and map port 50005 (adjust the port if your application uses a different one):
   ```shell
   docker run -p 50005:50005 cordapp-clients
   ```

2. **Access the Application:**  
   - Open a web browser and navigate to:  
     `http://localhost:50005`
   - Alternatively, if your application exposes specific endpoints (e.g., `/status`), navigate to those.

## Dockerfile Overview

The Dockerfile used in this project is:

```dockerfile
FROM eclipse-temurin:8-jre
WORKDIR /app
# Copy the executable jar (ensure the name matches the generated jar)
COPY build/libs/cordapp-example-0.1.jar app.jar
EXPOSE 50005
ENTRYPOINT ["java", "-jar", "app.jar"]
```

This image uses the Eclipse Temurin JDK 8 runtime to run the jar file.

## Troubleshooting

- **Jar Not Found:**  
  If Docker reports that the jar file cannot be found, verify that:
  - You ran `./gradlew clean jar` successfully.
  - The jar file exists in `build/libs` with the expected name.
  - The COPY path in the Dockerfile exactly matches the jar file name.

- **Port Mapping:**  
  Ensure no other application is using port 50005. If necessary, update the Dockerfile’s EXPOSE instruction and the `docker run` command to use a different port.

---

By following these steps, you (and others you share this with) will be able to build and run the containerized Cordapp Clients application using Docker.

Feel free to modify this documentation to suit any additional configuration details specific to your environment.
## Additional Information

For further details on the sample CorDapp’s project structure, node configuration, and testing strategies, refer to the official [Corda 4.10 Sample CorDapp Tutorial](https://docs.r3.com/en/platform/corda/4.10/community/tutorial-cordapp.html) 

---
