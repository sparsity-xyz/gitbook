# App ABCI Core

## 2. App ABCI Server

The ABCI server serves as the core logic of the backend service, providing computational resources, facilitating consensus, and generating results that will be settled on-chain. Follow the steps below to set up and implement your application.

### Installation

To get started, install the required package using either npm or yarn:

```sh
npm install @sparsity/abci
# or
yarn add @sparsity/abci
```

🔗 \[View package on npm]

### Implementing Your Application

To create a custom application, extend the `BaseApplication` class:

```typescript
import { BaseApplication, StepEvent } from '@sparsity/abci';

class MyApplication extends BaseApplication {
    // Implement your application logic here
    
    // Initializes the application with data from the smart contract
    __init__(initial_data: string): void;
    
    // Processes client-defined messages and returns events to be broadcast
    __step__(messages: Array<any>): Array<StepEvent>;
    
    // Determines session termination and provides final computation results
    __status__(): [isEnd: boolean, data: string];
}
```

### Core Functions to Implement

#### `__init__(initial_data: string): void`

This function is invoked during the initialization of the Sparsity network session.

* `initial_data`: Encoded data passed from the smart contract’s \[`newSession`] function (refer to the \[App Smart Contract] section).

In the Fibonacci demo application, this function receives `initial_data` from the smart contract, decodes it, and starts the computation:

```typescript
__init__(initial_data: string) {
    // Decode initial data from the contract
    if (initial_data !== "") {
        const decoded = ethers.AbiCoder.defaultAbiCoder().decode(['uint256'], initial_data);
        this.result = this.fibonacci(Number(decoded[0]));
        console.log("Computed Fibonacci result:", this.result);
        console.log("Encoded result:", this.resultData());
    } else {
        // Default behavior if no initial data is provided
        this.result = 1;
        console.log("No initial data received");
    }
}
```

#### `__status__(): [isEnd: boolean, data: string]`

* `isEnd`: Indicates whether the Sparsity network should terminate the session. If `true`, the session ends.
* `data`: The computed output, which is written back to the user’s smart contract as settlement data. This data is passed to the Outpost contract via the \[`callbackSettlement`] function.

In the Fibonacci demo application, once a valid result is computed, the function signals the session termination and returns the encoded result:

```typescript
__status__(): [isEnd: boolean, data: string] {
    // Continue session if computation is not yet complete
    if (this.result === 0) {
        return [false, ""];
    }
    // Encode the final result and terminate the session
    return [true, this.resultData()];
}
```

#### `__step__(messages: Array<any>): Array<StepEvent>`

For interactive applications, this function processes real-time or scheduled messages sent from the app client. The Sparsity network aggregates and includes these messages in each mined block.

Developers can define custom message formats, parse them, and process interactions within the Sparsity network. Each execution cycle generates a `StepEvent`, which is broadcast to all associated clients.

***

### Additional Features

* **Accessing Block Height:** The `blockHeight` property allows developers to retrieve the latest block number for custom logic implementation.
* **State Management & Smart Contract Integration:** By implementing these core functions, developers can define application behavior, manage state transitions, and seamlessly integrate with the Sparsity network and smart contracts on the host chain.
