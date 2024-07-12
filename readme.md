
# System Design

![System Design](SystemDesign.png)

# 🎉 CoDev Studio

Welcome to CoDev Studio! This application enables multiple users to collaboratively write and edit code in real-time using WebSockets. Users can sign up or log in with unique usernames, create or join rooms via unique room IDs, and interact with others through real-time chat and code editing. Each room supports multiple users who can collaboratively write code, choose programming languages, submit code for execution, and view results together. The backend uses the Judge0 API for code execution and Redis for task queuing and pub/sub functionality. 

## 🌟 Features
- **🔒 User Authentication**: Sign up and log in with unique usernames.
- **🛏️ Room Management**: Create or join rooms with unique IDs.
- **📝 Real-time Collaboration**: Code and chat in real-time with other users in the room.
- **🌐 Multi-language support**: Choose the programming language for your code, supports 4 languages (python,javascript,java,c++)
- **🚀 Code Submission and Execution**: Submit code and view results using the Judge0 API.
- **🔄 Real-time Updates**: Automatic updates for code changes, language selection, user activity, and chat messages.

## 🛠️ Tech Stack
- **Frontend**: Vite, React, TypeScript
- **Backend**: Express, HTTP for WebSockets, MongoDB
- **Queue and Pub/Sub System**: Redis

## 📦 Setup Guide

### Manual Setup
1. **Clone the repository**:
    ```sh
    git clone https://github.com/adityaChauhan2510/CoDev-Studio.git
    cd CoDev-Studio
    ```

2. **Install dependencies for each service**:
    ```sh
    # Server
    cd server
    npm install

    # Worker
    cd ../worker
    npm install

    # Client
    cd ../client
    npm install
    ```

3. **Create a `.env` file** in each folder and configure your environment variables: (Refer the .env.example file)
    ```env
    # Example Client .env file
	    VITE_REACT_APP_SERVER_URL =
    # Example Server .env file
	    MONGO_URL =
        REDIS_URL = 
	# Example Worker .env file
        REDIS_URL =
		X_RAPID_API_KEY = 
		//judge0 api key
 

4. **Start redis and mongoDB locally**
    ```sh
    # In separate terminal
    # Using Docker
    docker run -p 6379:6379 -d redis
    docker run -d -p 27017:27017 -v ~/mongo-data:/data/db mongo
    ```

5. **Start each service**:
    ```sh
    # Start Server
    cd server
    npm run start

    # Start Worker
    cd ../worker
    npm run start

    # Start Client
    cd ../client
    npm run dev
    ```


## 🚀 How It Works
1. **Sign Up / Log In**: Users sign up or log in with a unique username.
2. **Create / Join Room**: Users can create a new room with a unique room ID or join an existing room.
3. **WebSocket Connection**: Upon joining a room, a WebSocket connection is established.
4. **User Mapping**: On the server, the username is mapped to the WebSocket connection and added to the room's users array.
5. **Code Editor**: Users can write and edit code in a collaborative editor with a language selection option.
6. **Submit Code**: When a user submits code, it is pushed to a Redis queue.
7. **Worker Processing**: A worker listens to the queue, processes the code using the Judge0 API, and publishes the result to Redis.
8. **Result Broadcasting**: The main server subscribes to the result channel and broadcasts the result to all clients in the room.


## 🎨 Room Structure
- **Name**: The name of the room.
- **Room ID**: A unique identifier for the room.
- **Users**: An array of user objects `{username, wss}`.
- **Code**: The current code in the editor.
- **Chats**: An array of chat objects `{username, message}`.
- **Language**: The selected programming language.
- **Result**: The result of the last code execution.


## 📬 Contributing
Contributions to CoDev Studio are welcomed.





