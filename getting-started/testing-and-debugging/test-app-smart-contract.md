# Test App Smart Contract

## App Smart Contract Checklist

Ensure that the following requirements are met when implementing your App Smart Contract:

1. **Implement Required Interfaces**\
   Verify that all required functions are properly implemented and that they handle data parsing and settlement correctly when triggered.

**`APPInterface`**

```solidity
interface APPInterface {
    // Called by the Outpost when a session is successfully created
    // sessionId: Unique session identifier
    // session: A struct containing the endpoint, address, and session status
    function callbackSession(uint256 sessionId, CallbackSession memory session) external;

    // Called by the Outpost when a session ends
    // sessionId: Unique session identifier
    // isRevert: Indicates whether the session was successful
    // data: Encoded final result from the Sparsity Network
    function callbackSettlement(uint256 sessionId, bool isRevert, bytes memory data) external;
}
```

Make sure these callback functions are properly exposed to communicate with the Sparsity contract.

2. **Proper Integration with Outpost Contract Interface**\
   Ensure the contract is properly hooked into the Outpost contract, including handling the relevant functions.

**`OutpostInterface`**

```solidity
interface OutpostInterface {
    // sessionId: Unique session identifier
    // initialData: Encoded initial data to pass to the Sparsity Network
    function newSession(uint256 sessionId, bytes memory initialData) external;

    // address: User's wallet address to add to the session, allowing them to interact with the Sparsity Network
    // sessionId: Unique session identifier
    function authIn(address account, uint256 sessionId) external;

    // address: User's wallet address to remove from the session
    // sessionId: Unique session identifier
    function authOut(address account, uint256 sessionId) external;
}
```

3. **Session Creation Validation**\
   When a new session is created, ensure that the `newSession` function is triggered correctly, and that `initialData` is passed in as expected.

By following this checklist, you can ensure that your App Smart Contract functions seamlessly within the Sparsity ecosystem.
