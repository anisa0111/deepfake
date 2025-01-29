# Real-Time Face-Swapping Tool using Deepfake Algorithm

## Overview

This project implements a cloud-based real-time face-swapping tool that enables face swapping in a video using a deepfake-based model. The system is designed using a 3-tier architecture to ensure efficient deployment of machine learning-based real-time applications. The architecture includes:

1. **Client Application Server**: The entry point for the user to interact with the cloud infrastructure.
2. **WebSocket Server**: Handles real-time duplex communication between the client and the system.
3. **Autoscaling ML Inferencing Server**: Performs the heavy-lifting of running the deepfake model for face swapping.

This architecture allows the seamless deployment of various real-time applications that rely on complex machine learning models.

## Installation Instructions

### Prerequisites

Ensure you are using **Ubuntu 18.04** or a compatible version.

### Client Application Server

1. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```

2. To test the client application locally:
   ```bash
   python manage.py runserver
   ```

3. To deploy the client on the cloud, collect static files and deploy:
   ```bash
   python manage.py collectstatic
   gcloud app deploy
   ```

### WebSocket Server

1. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
   ```

2. To test the WebSocket server locally:
   ```bash
   gunicorn -b 127.0.0.1:8001 -k flask_sockets.worker main:app
   ```

3. To deploy the WebSocket server on the cloud:
   ```bash
   gcloud app deploy
   ```

### Deepfake Prediction Model

1. Deploy the deepfake model as a custom routine on the AI Platform:
   
   - Run `setup.py` to package the custom routine and dependencies.
   
   - Create a model on the AI Platform and deploy the created package as a version.

2. Ensure the `ModelPrediction` class is set as the main class to instruct the system to load and perform inference with the deepfake model.

## Functionalities of the Program

### Client Application Server

The Client Application Server consists of the following key files:

1. **app.yaml**: Configures the app's settings, URL routing, and static files.
2. **Static Files**: Contain HTML and CSS code for the web application, allowing users to access the face-swapping video stream.
3. **facedetect Folder**: Contains Django default files generated during the framework initialization. Key components:
   - `views.py`: Handles image requests.
   - `urls.py`: Manages application routing.
   - `settings.py`: Contains configuration values for the web app.

### WebSocket Server

The WebSocket Server has similar functionality to the Client Server but operates as a background task. Key components:

1. **app.yaml**: Contains the entrypoint for the application, which is directed to the `main.py` file.
2. **main.py**: Receives client frames, makes API calls to the deepfake model, and returns results to the client.

### Deepfake Prediction Model

The Deepfake Prediction Model is deployed on the AI Platform, which offers machine learning inferencing as a service. The WebSocket server sends API requests, and the AI Platform scales automatically based on request volume and resource availability.

Key components:

1. **Prediction.py**: Defines the `ModelPrediction` class, which handles the deepfake model loading and inferencing routines.

## Contributing

If you'd like to contribute to this project, please fork the repository and submit a pull request with your changes. Ensure that your contributions align with the project's goals and architecture.

---

This **Real-Time Face-Swapping Tool** offers a powerful, scalable solution for face swapping in videos using state-of-the-art deepfake algorithms. The modular design allows for easy expansion and deployment of other machine learning applications in real-time environments.
