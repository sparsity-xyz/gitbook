# Test ABCI Client

## Integration and Communication with ABCI Core

1.  **Use Self-defined Data Type With Protobuf Encapsulation**\
    Ensure that you are using self-defined message and embed in the Sparsity Protobuf for messages encapsulating and communication between the client and the ABCI Core.

    ```javascript
    import { BatchState, Message, MessageType } from '@sparsity/abci';
    ```
2. **WebSocket Communication with ABCI Core**\
   Make sure to use WebSocket to communicate with the ABCI Core. Messages should be parsed correctly, and the App Client should receive proper responses from the ABCI Core.
3.  **Local Integration Testing with Relay Server**\
    To facilitate local integration testing, Sparsity provides a relay server (dispatcher) in a Docker image. This server bridges the gap between the ABCI Client and the ABCI Core.

    **Steps:**

    *   **Step 1: Download and Start the Dispatcher Server**

        ```bash
        docker pull sparsityxyz/fleet-er
        docker run -ti --rm -p 9981:9981 sparsityxyz/fleet-er --no-indexer
        ```
    * **Step 2: Run Your ABCI Core** (it will bind with above **Dispatcher** by default)
    * **Step 3: Enable Communication Between Client and Dispatcher on Port 9981**\
      The App Client should now communicate directly with the dispatcher via port 9981.
4. **Message Communication**\
   You should be able to observe message communication between the App Client and the App ABCI Core.
