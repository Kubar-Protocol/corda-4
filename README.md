
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

## Additional Information

For further details on the sample CorDapp’s project structure, node configuration, and testing strategies, refer to the official [Corda 4.10 Sample CorDapp Tutorial](https://docs.r3.com/en/platform/corda/4.10/community/tutorial-cordapp.html) 

---
