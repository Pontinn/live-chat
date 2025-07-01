# Live Chat with Spring Boot and WebSocket

![Badge](https://img.shields.io/badge/Java-21-blue)
![Badge](https://img.shields.io/badge/Spring_Boot-3.5.3-brightgreen)
![Badge](https://img.shields.io/badge/WebSocket-STOMP-purple)
![Badge](https://img.shields.io/badge/Frontend-HTML_&_JS-orange)

A simple yet powerful real-time chat application built with Java and Spring Boot on the backend, and plain HTML, CSS, and JavaScript on the frontend. This project demonstrates the use of **Spring WebSockets** with the **STOMP** protocol to enable full-duplex, real-time communication between the server and multiple clients.

## 📖 About The Project

This project was created to be a clear and functional example of how to build interactive web applications with the Spring ecosystem. The backend manages the WebSocket connection and message broadcasting, while the frontend client connects to send and receive messages instantly, without needing to reload the page.

### ✨ Features

* **Real-Time Communication:** Messages are sent and received instantly by all connected users.
* **Simple Connection:** Connect and disconnect from the chat with a single click.
* **Clean Interface:** A user-friendly interface built with HTML, CSS, and jQuery.
* **Robust Backend:** Utilizes Spring Boot for quick setup and a stable backend.
* **Basic Security:** Prevents XSS attacks by escaping HTML characters in messages.

## 🛠️ Tech Stack

This project is built with the following technologies:

**Backend:**
* **Java 21**
* **Spring Boot 3.5.3**
* **Spring Web**
* **Spring WebSocket:** For WebSocket-based communication.
* **Maven:** For dependency management.

**Frontend:**
* **HTML5**
* **CSS3** (with Bootstrap for base layout)
* **JavaScript**
* **jQuery:** For DOM manipulation.
* **StompJS:** A JavaScript client for the STOMP protocol over WebSocket.

## 🚀 Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

You will need to have Java (JDK 21 or higher) and Apache Maven installed on your machine.
* [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/downloads/)
* [Apache Maven](https://maven.apache.org/download.cgi)

### Installation & Running

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/Pontinn/live-chat.git
    ```
2.  **Navigate to the project directory:**
    ```sh
    cd live-chat
    ```
3.  **Run the application using Maven:**
    ```sh
    mvn spring-boot:run
    ```
    The server will start on port `8080`.

## 🎈 How to Use

1.  After starting the application, open your browser and navigate to:
    ```
    http://localhost:8080
    ```
2.  Enter a username in the "Username" field.
3.  Click the **Connect** button.
4.  Start sending messages! Open multiple browser tabs or windows to simulate a conversation with several users.

## ⚙️ How It Works

The architecture is divided between the backend and the frontend:

### Backend (Spring Boot)

* `WebSocketConfiguration.java`: Configures the WebSocket connection.
    * It registers a WebSocket endpoint at `/pontindev-livechat-websocket`.
    * It configures a simple message broker on the `/topic` prefix. Messages sent to this prefix are broadcast to all subscribed clients.
    * It sets `/app` as the application destination prefix for messages bound for `@MessageMapping` annotated methods.
* `LiveChatController.java`: Controls the message flow.
    * The `newMessage` method is mapped to the `/new-message` destination.
    * When a client sends a message to `/app/new-message`, this method is invoked.
    * The incoming message (`ChatInput`) is processed, its content is HTML-escaped for security, and it's then wrapped in a `ChatOutput` and sent to the `/topic/livechat` topic.

### Frontend (HTML/JS)

* `index.html`: The structure of the chat page.
* `script.js`: The client-side logic.
    * It uses the **StompJS** library to communicate with the backend over WebSocket.
    * On "Connect", the client establishes a connection to the WebSocket endpoint and subscribes to the `/topic/livechat` topic.
    * When a message is received on the topic, the `updateLiveChat` function appends it to the conversation table.
    * On "Send", a message is published to the `/app/new-message` destination, sending the username and message to the backend.

---

Feel free to contribute, fork, or use this project as a foundation for your own ideas!
