# Test ABCI Core

## ABCI Core Checklist

1.  **Verify Proper Data Injection and Parsing**\
    Ensure that the encoded data passed as `initial_data` is correctly injected into the system. It should be parsed and consumed properly for further processing.

    ```typescript
    __init(initial_data: string): void;
    ```
2.  **Ensure Communication with App Client**\
    The ABCI Core should be able to communicate with the App Client via WebSocket. It should process incoming messages from client (of user defined data type) and respond \[StepEvent] to the client through the `step` function.

    ```typescript
    step(messages: Array<any>): Array<StepEvent>;
    ```
3.  **Proper Termination and Encoded Output Generation**\
    Ensure that the ABCI Core properly terminates the session when needed and generates the correct encoded output.

    ```typescript
    status(): [isEnd: boolean, data: string];
    ```

By following this checklist, you ensure that the ABCI Core integrates properly with the App Client and handles data flow correctly within the Sparsity ecosystem.
