# 💬 SB WebSocket Real-Time Chat App

<p align="center">

<strong>A modern real-time chat application built with Spring Boot, WebSocket, STOMP, SockJS, HTML, JavaScript, and Bootstrap.</strong>

</p>

<p align="center">

  <a href="https://github.com/YogeshSavant-tech/sb-websocket-Real-Time-chat-app">
    <img src="https://img.shields.io/badge/GitHub-Repository-black?style=for-the-badge&logo=github" alt="GitHub">
  </a>

  <img src="https://img.shields.io/badge/Java-Spring%20Boot-orange?style=for-the-badge&logo=springboot" alt="Spring Boot">

  <img src="https://img.shields.io/badge/WebSocket-Real--Time-blue?style=for-the-badge" alt="WebSocket">

  <img src="https://img.shields.io/badge/Frontend-HTML%20%7C%20CSS%20%7C%20JavaScript-yellow?style=for-the-badge" alt="Frontend">

</p>

---

## 📌 Overview

**SB WebSocket Real-Time Chat App** is a real-time messaging application developed using **Spring Boot WebSocket** technology.

The application allows multiple users to communicate through a live chat interface without continuously refreshing the webpage.

The project demonstrates how **WebSocket, STOMP, and SockJS** can be integrated with a Spring Boot backend and a lightweight HTML/JavaScript frontend to create a real-time communication system.

---

## ✨ Features

* 💬 Real-time messaging
* ⚡ WebSocket-based communication
* 🔄 Instant message delivery without page refresh
* 👤 User name identification
* 📱 Responsive chat interface
* 🎨 Modern and attractive UI
* 🌈 Instagram-inspired gradient design
* ✨ Smooth hover and message animations
* ⌨️ Press **Enter** to send messages
* 🛡️ Basic HTML escaping for message content
* 🔌 STOMP messaging protocol
* 🔗 SockJS fallback support

---

## 🛠️ Technologies Used

### Backend

* **Java**
* **Spring Boot**
* **Spring Web**
* **Spring WebSocket**
* **STOMP**

### Frontend

* **HTML5**
* **CSS3**
* **JavaScript**
* **Bootstrap 5**

### Real-Time Communication

* **WebSocket**
* **STOMP.js**
* **SockJS**

### Build Tool

* **Apache Maven**

---

## 🏗️ Application Architecture

```text
                    ┌─────────────────────┐
                    │       Client        │
                    │                     │
                    │ HTML + CSS + JS     │
                    │ Bootstrap           │
                    └──────────┬──────────┘
                               │
                               │ SockJS
                               │ + STOMP
                               ▼
                    ┌─────────────────────┐
                    │    Spring Boot      │
                    │      Server         │
                    │                     │
                    │ WebSocket / STOMP   │
                    └──────────┬──────────┘
                               │
                               │ Message Broker
                               ▼
                    ┌─────────────────────┐
                    │   /topic/messages   │
                    └──────────┬──────────┘
                               │
                  ┌────────────┴────────────┐
                  ▼                         ▼
             Client A                  Client B
```

---

## 🔄 How It Works

The application follows a simple real-time messaging flow:

### 1. Client Connection

The browser creates a SockJS connection:

```javascript
const socket = new SockJS('/chat');
```

### 2. STOMP Connection

STOMP is created over the SockJS connection:

```javascript
stompClient = Stomp.over(socket);
```

### 3. Subscribe to Messages

The client subscribes to the message topic:

```javascript
stompClient.subscribe('/topic/messages', function(message) {
    showMessage(JSON.parse(message.body));
});
```

### 4. Send Message

When the user sends a message, it is sent to the Spring Boot application:

```javascript
stompClient.send(
    "/app/sendMessage",
    {},
    JSON.stringify(chatMessage)
);
```

### 5. Broadcast

The Spring Boot WebSocket server processes the message and broadcasts it to subscribed clients.

```text
User A
   │
   │ Send Message
   ▼
/app/sendMessage
   │
   ▼
Spring Boot
   │
   ▼
/topic/messages
   │
   ├──────────────► User A
   │
   ├──────────────► User B
   │
   └──────────────► User C
```

---

## 📂 Project Structure

```text
sb-websocket-Real-Time-chat-app/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── chat/
│   │   │           └── app/
│   │   │               ├── AppApplication.java
│   │   │               ├── controller/
│   │   │               ├── config/
│   │   │               └── model/
│   │   │
│   │   └── resources/
│   │       ├── static/
│   │       │   ├── images/
│   │       │   ├── css/
│   │       │   └── js/
│   │       │
│   │       ├── templates/
│   │       └── application.properties
│   │
│   └── test/
│
├── .gitignore
├── pom.xml
├── mvnw
├── mvnw.cmd
├── README.md
└── HELP.md
```

> The exact package structure may vary depending on the implementation.

---

## 🚀 Getting Started

### Prerequisites

Before running the project, make sure you have installed:

* Java JDK
* IntelliJ IDEA
* Apache Maven
* Git

Check Java:

```bash
java -version
```

Check Maven:

```bash
mvn -version
```

---

## 📥 Clone the Repository

```bash
git clone https://github.com/YogeshSavant-tech/sb-websocket-Real-Time-chat-app.git
```

Navigate into the project:

```bash
cd sb-websocket-Real-Time-chat-app
```

---

## ▶️ Run the Application

### Using IntelliJ IDEA

1. Open the project in IntelliJ IDEA.
2. Wait for Maven dependencies to download.
3. Open the main Spring Boot application class.
4. Run the application.
5. Open the application in your browser.

### Using Maven

Run:

```bash
./mvnw spring-boot:run
```

On Windows:

```bash
mvnw.cmd spring-boot:run
```

---

## 🌐 Open the Application

After starting the Spring Boot application, open:

```text
http://localhost:8080
```

Open the application in multiple browser tabs/windows to test real-time communication.

For example:

```text
Browser A                Browser B
   │                         │
   │──── "Hello" ───────────►│
   │                         │
   │◄──── "Hi!" ─────────────│
```

---

## 🔌 WebSocket Endpoints

| Endpoint           | Purpose                                  |
| ------------------ | ---------------------------------------- |
| `/chat`            | SockJS/WebSocket connection endpoint     |
| `/app/sendMessage` | Sends messages to the server             |
| `/topic/messages`  | Broadcasts messages to connected clients |

---

## 📦 Frontend Dependencies

### SockJS

```html
<script src="https://cdn.jsdelivr.net/npm/sockjs-client@1/dist/sockjs.min.js"></script>
```

SockJS provides WebSocket-like communication with fallback support.

### STOMP.js

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/stomp.js/2.3.1/stomp.min.js"></script>
```

STOMP is used to communicate with the Spring WebSocket message broker.

### Bootstrap

The project uses **Bootstrap 5** to help create a responsive and modern user interface.

---

## 🎨 UI Highlights

The application includes:

* Instagram-inspired gradient header
* Modern chat bubbles
* Responsive design
* Smooth hover effects
* Animated online indicator
* Interactive Send button
* Input focus effects
* Custom scrollbar
* Mobile-friendly layout

---

## 🧪 Testing the Application

To test the real-time functionality:

1. Start the Spring Boot application.
2. Open the application in **Browser Tab 1**.
3. Open the same application in **Browser Tab 2**.
4. Enter different usernames.
5. Send a message from Tab 1.
6. Check Tab 2.
7. The message should appear instantly.

---

## 📸 Screenshots

Add your application screenshots here:

```markdown
![Chat Application](src/main/resources/static/images/chat-app.png)
```

You can also create a dedicated screenshots folder:

```text
screenshots/
├── chat-home.png
├── messaging.png
└── responsive-view.png
```

Then add them to the README:

```markdown
![Chat Application](screenshots/chat-home.png)
```

---

## 🔮 Future Improvements

The project can be extended with:

* 🔐 User authentication
* 👥 Private messaging
* 🟢 Online/offline user status
* ✍️ Typing indicator
* 📎 File and image sharing
* 😀 Emoji support
* 🕒 Message timestamps
* 🗑️ Delete messages
* ✏️ Edit messages
* 🔔 Notifications
* 💾 Database message persistence
* 👤 User profiles
* 🌙 Dark mode
* 📱 Progressive Web App support

---

## 📚 Useful Documentation

### Spring Boot & Maven

* [Apache Maven Documentation](https://maven.apache.org/guides/index.html)
* [Spring Boot Maven Plugin](https://docs.spring.io/spring-boot/4.0.8/maven-plugin)
* [Spring Web](https://docs.spring.io/spring-boot/4.0.8/reference/web/servlet.html)
* [Spring WebSocket](https://docs.spring.io/spring-boot/4.0.8/reference/messaging/websockets.html)
* [Thymeleaf](https://docs.spring.io/spring-boot/4.0.8/reference/web/servlet.html#web.servlet.spring-mvc.template-engines)

### Spring Guides

* [Building a RESTful Web Service](https://spring.io/guides/gs/rest-service/)
* [Serving Web Content with Spring MVC](https://spring.io/guides/gs/serving-web-content/)
* [Building REST Services with Spring](https://spring.io/guides/tutorials/rest/)
* [Using WebSocket to Build an Interactive Web Application](https://spring.io/guides/gs/messaging-stomp-websocket/)
* [Handling Form Submission](https://spring.io/guides/gs/handling-form-submission/)

---

## 🎯 Learning Outcomes

Through this project, you can learn:

* How Spring Boot applications are structured
* How WebSocket communication works
* How STOMP messaging works
* How SockJS provides WebSocket fallback support
* How frontend and backend communicate in real time
* How to build responsive interfaces using Bootstrap
* How to integrate JavaScript with Spring Boot
* How to use Maven for dependency management
* How to build a real-time web application

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository.
2. Create a new branch:

```bash
git checkout -b feature/new-feature
```

3. Make your changes.
4. Commit your changes:

```bash
git commit -m "Add new feature"
```

5. Push the branch:

```bash
git push origin feature/new-feature
```

6. Open a Pull Request.

---

## 👨‍💻 Author

### Yogesh Savant

**IT Engineering Student | Java & Spring Boot Developer | Web Development Enthusiast**

GitHub:
https://github.com/YogeshSavant-tech

---

## ⭐ Support

If you found this project useful, consider giving the repository a ⭐ on GitHub.

<p align="center">

<strong>Built with ❤️ using Spring Boot & WebSocket</strong>

</p>
