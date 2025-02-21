# Create a new project

Sparsity is a decentralized platform that provides powerful computational capabilities while preserving the trustless nature of decentralization. It overcomes the inherent limitations of blockchain computing power, enabling developers to create scalable and efficient applications without compromising security or decentralization.

When building an application or service on Sparsity, developers must implement three core components:

1. **App Smart Contract** – Responsible for initializing the app, submitting requests, creating sessions, managing resources, collecting app results, and settling data on-chain.
2. **App ABCI Core** – The backbone of the application, responsible for performing computations based on functional requirements. It interacts with the App Client (if applicable) during the session, manages state transitions, and ensures consensus with the underlying blockchain through the Application Blockchain Interface (ABCI).
3. **App Client** – The front-end or user-facing component that communicates with both the ABCI Core and smart contracts, ensuring a seamless user experience.

By integrating these components, developers can tap into Sparsity's computational power and modular architecture to build next-generation decentralized applications.
