# Peer-to-Peer Chat Application

This project implements a peer-to-peer chat application using `libp2p`. The application sets up two nodes, Earth and Moon, which communicate with each other using a custom protocol (`/chat/1.0.0`).

## Tech Used

- Node.js
- `libp2p`
- `pull-stream`
- `chalk`
- `node-emoji`
- `async`
- `peer-id`
- `peer-info`
- `pull-pushable`

## Installation

1. **Clone the Repository:**

   ```
   git clone https://github.com/tinniaru3005/p2p-chat-app.git
   cd p2p-chat-app
   ```

2. **Install Dependencies:**

    ```
    npm install
    ```

3. **Create Peer Identities:**

    You need to create two Peer IDs for the Earth and Moon nodes. You can use the `peer-id` module to generate these IDs.

    ```
    npx peer-id --count 2 --format json > ids.json
    ```

    Split the generated `ids.json` into two separate files: `earthId.json` and moonId.json, and place them in the `ids` directory.

4. **Run the Nodes:**

    Open two terminal windows.

    Terminal 1 (Earth Node):

    ```
    node earth.js
    ```

    Terminal 2 (Moon Node):

    ```
    node moon.js
    ```


## Usage

1. Start the Earth Node:

    In Terminal 1, run:

    ```
    node earth.js
    ```

    You should see output indicating that the Earth node is ready and listening.

2. Start the Moon Node:

    In Terminal 2, run:

    ```
    node moon.js
    ```

    You should see output indicating that the Moon node is ready and listening. The Moon node will try to connect with the Earth node.

3. Send Messages:

    In either terminal, type a message and press Enter. The message will be sent to the other node and displayed.

## Code Overview

1. **Earth Node (`earth.js`)**

    The Earth node creates a `libp2p` instance with its peer information and starts the node. It then dials the Moon node using the `/chat/1.0.0` protocol and sets up a `pull-stream` pipeline to handle incoming and outgoing messages.

2. **Moon Node (`moon.js`)**

    The Moon node creates a `libp2p` instance with its peer information and starts the node. It listens for connections on the `/chat/1.0.0` protocol and sets up a `pull-stream` pipeline to handle incoming and outgoing messages.

3. **`libp2p_bundle.js`**

    This file defines the `P2PNode` class, which extends the `libp2p` class and configures the node with the necessary modules for transport, connection encryption, and stream multiplexing.

