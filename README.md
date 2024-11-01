## LinkSphere: Federated Learning with Proof of Stake

LinkSphere is a federated learning protocol that uses Proof of Stake (PoS) to incentivize honest participation and improve model accuracy. It addresses the issue of malicious clients who can sabotage the network and reduce model accuracy.

### Federated Learning and Challenges

Federated learning allows training deep learning models while keeping data private. Clients train models on their local data and share only the updated model parameters with a central aggregator. The aggregator combines these updates to create a new, improved model.

However, ensuring honest participation is crucial. Malicious clients can submit tampered updates, hindering the model's accuracy.

### LinkSphere Architecture

LinkSphere uses a PoS-based architecture with the following components:

* **Clients:** These devices or users have private data and train models.
* **Staking Registry:** Clients stake a certain amount to participate, which can be slashed for malicious behavior.
* **Slashing Manager:** This contract monitors for and penalizes dishonest clients.
* **Reward Manager:** This contract distributes fees paid by users among the network participants.
* **Aggregator:** This component combines the updated model parameters from clients.

**Micro-Rollup Architecture:**

LinkSphere utilizes a micro-rollup built on top of the client network. This rollup acts as a Model Parameter Sharing (MPS) Chain, maintaining a verifiable record of updated parameters for each training epoch.

The rollup allows for off-chain verifiable computation. The slashing conditions are implemented here. The State Transition function performs slashing checks and maintains the state of each client's model parameters and their slashing eligibility. After each epoch, the aggregator fetches the state. If a client is malicious, the Slashing Manager is called to slash their stake.

### Slashing Conditions

LinkSphere implements slashing conditions to identify and penalize malicious clients:

* **Krum Function:** This function checks for outliers by calculating the sum of squared distances between a client's model parameters and those of other clients. The assumption is that honest clients have similar parameters. A client with a high Krum score is likely malicious.
* **Correlation Checks:** LinkSphere checks the correlation between a client's model parameters from consecutive epochs. If the parameters are too similar, the client may not be training the model properly and could face a penalty.

This approach discourages malicious behavior and incentivizes honest participation, leading to more accurate models in the federated learning process.
