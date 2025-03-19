# App Smart Contract

## 1. App Smart Contract

A smart contract is essential for securely recording critical information, such as user data and on-chain configuration, when the application is initialized. This ensures transparency, trust, and verifiability for every interaction within the app.

**Implementing Your Smart Contract**

Developers must extend the Template contract, which serves as the foundational contract for Sparsity applications. The template contract can be found here: 👉 \[Template Contract]

**Required Functions**

To interact with Sparsity, developers must implement the following functions in the smart contract:

```solidity
interface APPInterface {
    // Called by the Outpost when a session is successfully created
    // sessionId: Unique session identifier
    // session: A struct containing endpoint, address, and session status
    function callbackSession(uint256 sessionId, CallbackSession memory session) external;

    // Called by the Outpost when a session ends
    // sessionId: Unique session identifier
    // isRevert: Indicates if the session was successful
    // data: Encoded final result from Sparsity Network
    function callbackSettlement(uint256 sessionId, bool isRevert, bytes memory data) external;

    // Called by the Outpost to check if the account join the specified session
    // sessionId: Unique session identifier
    // account: user wallet address
    function checkAuth(uint256 sessionId, address account) external view returns (bool);
}
```

These callback functions must be exposed in the smart contract to enable communication with the Sparsity contract.

Simultaneously, the Sparsity Outpost contract exposes the following interface:

```solidity
interface OutpostInterface {
    // sessionId: Unique session identifier
    // initialData: Encoded initial data to pass to Sparsity Network
    function newSession(uint256 sessionId, bytes memory initialData) external;
}
```

App developer can interact with these functions to manage sessions and authentication though the developer’s smart contract.

***

#### Key Concepts

🔹 **Session**\
A session represents the entire lifecycle of an app’s execution. It determines whether a user is within a session and helps manage authentication. The session ID must be unique for each session.\
&#xNAN;**`initialData`** is the encoded data that the user passes to the Sparsity network when initializing the session.

🔹 **Auth**\
Auth verifies whether an address has permission to use Sparsity within a session. This information is eventually relayed from the host chain to the Sparsity network, where the App ABCI Core can utilize it.

🔹 **Settle**\
When Sparsity completes its computation, the results are returned via a callback and recorded in the developer’s smart contract.

***

By following this approach, developers can ensure that their application's critical state and user data are securely stored and seamlessly integrated within the Sparsity ecosystem.
