# App Client

## 3. App Client

If the application is interactive—requiring user operations throughout the process—developers must build a custom App Client tailored to their specific use case. This client must efficiently interact with both the ABCI Core and the App Smart Contract to ensure smooth communication and state management.

**3.1 Interacting with ABCI Core & Smart Contracts**

When developing the App Client, consider the following key interactions:

* **Registering and triggering the app** via the custom-developed App Smart Contract.
* **Indirectly interacting with the Outpost**:
  * Hook into the `[newSession]` function via the user-developed smart contract to initialize the computing session and allocate resources.
  * Get session status filled by the callback function \[callbackSession]
  * Use the `authIn/authOut` functions in the Outpost contract for address authentication registration.
* **Querying and verifying on-chain results** settled through the App Smart Contract:
  * Retrieve data settled in the user-developed contract, passed from the Outpost contract via the `[callbackSettlement]` interface.

**3.2 Interacting with ABCI Core**

When developing the App Client, consider the following key interactions:

* The **target URL/IP/endpoints** can be obtained via the `callbackSession` function in the App Smart Contract.
* **Sending and receiving messages** from the ABCI Core during the processing cycle:
  * The App Client should use **WebSocket** to communicate with the Sparsity network.

**Using Protobuf Types for Data Transmission**

To facilitate structured data exchange, developers should use the provided Protobuf types:

```typescript
import { BatchState, Message, MessageType } from '@sparsity/abci';
```

* **MessageType**: Defines the source of the message:
  * `MessageType.RESPONSE`: The request comes from the server.
  * `MessageType.REQUEST`: The request comes from the client.

**Sending Data to the Sparsity Network**

Example of sending data using the `Message`:

```typescript
import { Message } from '@sparsity/abci';

// Define your own content
const content = {
  // Custom application data
};

const data = new TextEncoder().encode(JSON.stringify(content));

const message = {
  type: MessageType.REQUEST,  // Client request type
  address: address,  
  timestamp: Date.now(),  
  data: data,  
  signature: new Uint8Array(),  
};

const wsMsg = Message.encode(message).finish();
socket.send(wsMsg);
```

* The server can parse the content from the message in the `step` function (mentioned in the previous section).

**Receiving Data from the Sparsity Network**

The server broadcasts settlement status data after each block is mined.

Example of receiving data:

```typescript
socket.onmessage = (event) => {
  event.data.arrayBuffer().then((buffer) => {
    const message = Message.decode(new Uint8Array(buffer));

    if (message.type === MessageType.RESPONSE) {
      const responseArr = BatchState.decode(message.data);
      responseArr.states.forEach((x) => {
        const processedData = JSON.parse(x.attributes[0].value);
        // processedData corresponds to the output "data" of the status function
      });
    }
  });
};
```

By properly integrating these components, developers can create a responsive and efficient client that fully leverages the Sparsity ecosystem. This ensures seamless interaction between the App Client, ABCI Core, and Smart Contracts, leading to a smooth and performant decentralized application.
