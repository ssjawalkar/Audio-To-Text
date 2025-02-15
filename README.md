# Audio Transcribe Backend

## Overview
The Audio Transcribe backend is a Spring Boot application that provides an API for transcribing audio files into text using OpenAI's Whisper model.

## Features
- Accepts audio file uploads via REST API.
- Uses OpenAI's Whisper model for transcription.
- Returns transcribed text as a response.
- Configurable via `application.properties`.
- Supports CORS for frontend communication.

## Dependencies
- Spring Boot
- Spring Web
- OpenAI API

## Setup Instructions
### Prerequisites
- Java 17+
- Maven
- OpenAI API key

### Configuration
Update `application.properties` with your OpenAI API key:
```properties
spring.application.name=audio-transcribe
spring.ai.openai.api-key=your_openai_api_key
spring.ai.openai.audio.transcription.base-url=https://api.openai.com
spring.ai.openai.audio.transcription.options.model=whisper-1
spring.ai.openai.audio.transcription.options.response-format=json
```

### Running the Application
```sh
mvn spring-boot:run
```
The backend will start on `http://localhost:8080`.

## API Endpoint
### Transcribe Audio
**Endpoint:**
```
POST /api/transcribe
```
**Request:**
- `multipart/form-data` with an audio file.

**Response:**
```json
{
  "transcription": "Transcribed text from the audio."
}
```
![postman](https://github.com/user-attachments/assets/ac015d4f-e208-423d-9eb2-778a4b741047)

## CORS Configuration
The backend allows requests from the frontend running on `http://localhost:5173/`.
To modify CORS settings, update `WebConfig.java`:
```java
registry.addMapping("/**")
        .allowedOrigins("http://your-frontend-url")
        .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
        .allowedHeaders("*")
        .allowCredentials(true);
```


## Deployment
For production deployment:
1. Package the application:
   ```sh
   mvn clean package
   ```
2. Run the JAR file:
   ```sh
   java -jar target/audio-transcribe-0.0.1-SNAPSHOT.jar
   ```

---

# Audio Transcribe Frontend

## Overview
The frontend is a React application that allows users to upload audio files and receive transcriptions from the backend.

## Features
- Uploads audio files to the backend.
- Displays transcribed text.
- Uses Axios for API requests.

## Setup Instructions
### Prerequisites
- Node.js and npm

### Installation
```sh
npm install
```

### Running the Application
```sh
npm run dev
```

The frontend will start on `http://localhost:5173/`.

## Frontend Components
### `App.jsx`
- Main entry point that renders the `AudioUploader` component.

### `AudioUploader.jsx`
- Provides UI for uploading an audio file.
- Sends the file to the backend for transcription.
- Displays the transcribed text.

## API Integration
The frontend interacts with the backend via:
```js
axios.post('http://localhost:8080/api/transcribe', formData, {
    headers: { 'content-type': 'multipart/form-data' }
})
```
Ensure the backend is running before testing the frontend.

![React](https://github.com/user-attachments/assets/70f0011a-d563-4e32-9ab4-026edbe05d9b)

## Deployment
To build for production:
```sh
npm run build
```
Serve the built files using a web server or deploy to a hosting service.

---

