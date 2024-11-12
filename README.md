# C++ Chat Application

## Project Overview

This project involves the design and implementation of a chat application built in C++ that can support high write throughput, intended to be used by thousands of users. The application will use an append-only database (such as Red Panda or Kafka) to handle the large amounts of chat data. The chat application is web-based, where the server needs to communicate with the client in real-time as new data (text messages) is sent.

## Key Features

- **High Write Throughput:** The system is designed to handle thousands of concurrent users, ensuring that messages can be sent and received in real-time with minimal delay.
- **Real-Time Communication:** The server uses WebSockets to communicate with the client as soon as new data (chat messages) is received.
- **Data Storage:** An append-only database (Red Panda or Kafka) is used to store chat messages and interactions.
- **Scalable Architecture:** The application is designed to scale efficiently, handling a growing user base without sacrificing performance.
- **Web-Based Interface:** A simple web interface is provided for users to send and receive chat messages in real-time.

## Technologies Used

- **C++20**: Modern C++ features such as generics, multithreading, and RAII will be used for clean, efficient, and predictable code.
- **WebSockets**: For real-time bi-directional communication between the server and client.
- **Red Panda/Kafka**: Append-only databases for storing chat messages and ensuring scalability.
- **SQL/NoSQL Database**: A SQL or NoSQL database will be used to aggregate the data and allow for querying of chat history.
- **CMake**: For managing the build process and dependencies.
- **Conan**: For handling external libraries and dependencies efficiently.

## Architecture

### 1. Server

The server is responsible for handling incoming messages from clients and broadcasting them to the appropriate recipients. It also stores the messages in the append-only database (Kafka/Red Panda). The server is implemented to support high write throughput and scalable communication with many clients.

### 2. Client

The client communicates with the server using WebSockets and displays the chat messages in real-time. Users can send messages that are then broadcasted to all other clients subscribed to the same chat room.

### 3. Database

An append-only database (Kafka/Red Panda) is used to store chat messages efficiently. This ensures that the data can be aggregated and consumed later without losing any information.

### 4. Data Flow

- Messages are sent by clients to the server.
- The server forwards the messages to Kafka/Red Panda for persistent storage.
- Kafka/Red Panda acts as a buffer for incoming messages and can be consumed by other services for further processing or storage.
- Clients receive real-time updates as new messages are broadcasted by the server.

## Design Considerations

- **Scalability**: The system is designed to handle a high volume of messages, especially when there are thousands of concurrent users. Kafka/Red Panda are chosen as they are highly scalable and designed to handle high write throughput.
- **Reliability**: Data persistence is ensured through the use of Kafka/Red Panda, ensuring that messages are not lost even if the system experiences failures.
- **Real-Time Communication**: WebSockets provide low-latency communication, ensuring that users receive messages as soon as they are sent.

## Installation

### Prerequisites

- C++20-compatible compiler (e.g., GCC, Clang)
- CMake 3.10 or higher
- Conan package manager
- Kafka/Red Panda server
- WebSocket server library (e.g., `libwebsocket`)

### Steps to Build

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/cpp-chat-app.git
   cd cpp-chat-app
   ```

2. Install dependencies via Conan:

   ```bash
   conan install . --build=missing
   ```

3. Create a build directory and compile the project:

   ```bash
   mkdir build && cd build
   cmake ..
   cmake --build .
   ```

4. Run the application:

   ```bash
   ./chat_server
   ```

### Running the Client

The client can be run in a web browser. Simply open the `index.html` file in the browser to start interacting with the server.

## Testing

Unit tests can be added to ensure the robustness of the application. The following testing libraries are recommended:
- Google Test (gtest) for unit tests.
- CTest for running tests within the CMake build process.

To run tests:

```bash
ctest
```

## Future Improvements

- Add authentication and user management to the chat application.
- Implement message encryption for secure communication.
- Enhance performance for handling larger user bases by optimizing message queueing and distribution.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
