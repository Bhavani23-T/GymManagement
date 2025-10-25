# AI Fitness Trainer

This project is an AI-powered fitness trainer that uses your webcam to track your exercises and count your repetitions. It leverages the MediaPipe library for real-time pose estimation.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

* Python 3.x
* OpenCV
* MediaPipe
* Pandas
* Numpy

### Installation

1. Clone the repo:
   ```sh
   git clone https://github.com/your_username_/Project-Name.git
   ```
2. Install the required packages:
   ```sh
   pip install -r requirements.txt
   ```

## Usage

You can run the application from the command line, specifying the exercise you want to perform. You can either use a pre-recorded video or your webcam.

### Using a pre-recorded video

To use a pre-recorded video, use the `-vs` or `--video_source` flag, followed by the path to your video file.

```sh
python main.py -t <exercise_type> -vs <path_to_video>
```

For example:

```sh
python main.py -t push-up -vs Exercise_videos/push-up.mp4
```

### Using your webcam

To use your webcam, simply omit the `-vs` flag.

```sh
python main.py -t <exercise_type>
```

For example:

```sh
python main.py -t squat
```

Press 'q' to quit the application.

## Exercises

The following exercises are currently supported:

*   **Push-ups:** Tracks the angle of your arms to count repetitions.
*   **Pull-ups:** Tracks the position of your nose relative to your shoulders.
*   **Sit-ups:** Tracks the angle of your abdomen.
*   **Squats:** Tracks the angle of your legs.
*   **Walk:** Tracks the alternating movement of your knees.

## How it Works

The application uses the MediaPipe library to detect the user's pose in real-time. For each exercise, a specific set of body landmarks and angles are monitored to determine if a repetition has been completed.

1.  **Pose Estimation:** MediaPipe's Pose solution is used to detect 33 pose landmarks on the body.
2.  **Angle Calculation:** The `body_part_angle.py` file contains functions to calculate the angles between different body parts.
3.  **Repetition Counting:** The `types_of_exercise.py` file contains the logic for counting repetitions for each exercise. It uses the calculated angles and landmark positions to determine if a valid repetition has been performed.
4.  **Real-time Feedback:** The application provides real-time feedback to the user, displaying the current exercise, the number of repetitions, and the status of the movement (e.g., "up" or "down").

## Advantages

*   **Cost-effective:** Provides a free alternative to personal trainers.
*   **Convenient:** Can be used anytime, anywhere with a webcam.
*   **Real-time feedback:** Helps users maintain proper form and track their progress.
*   **Beginner-friendly:** Simple to use and provides clear instructions.

## Disadvantages

*   **Limited exercise library:** Only supports a few exercises.
*   **Accuracy limitations:** The accuracy of the pose estimation can be affected by factors such as lighting, clothing, and camera angle.
*   **No personalized workout plans:** The application does not provide personalized workout plans based on the user's fitness level or goals.

## System Design

The system is designed as a modular application with the following components:

*   **`main.py`:** The main entry point of the application. It handles command-line arguments, video capture, and the main application loop.
*   **`utils.py`:** Contains utility functions for angle calculation, landmark detection, and displaying the score table.
*   **`body_part_angle.py`:** Defines a class for calculating the angles of different body parts.
*   **`types_of_exercise.py`:** Contains the logic for counting repetitions for each exercise.

## System Architecture

The application follows a simple, layered architecture:

1.  **Input Layer:** This layer is responsible for capturing video from a file or webcam using OpenCV.
2.  **Processing Layer:** This layer uses the MediaPipe library to perform pose estimation on each frame of the video. The results are then passed to the exercise-specific logic.
3.  **Application Logic Layer:** This layer contains the core logic of the application. It uses the pose estimation results to calculate body part angles and count exercise repetitions.
4.  **Output Layer:** This layer displays the video feed with the pose landmarks and real-time feedback on the screen using OpenCV.

## Technology Requirements

### Hardware

*   A computer with a webcam.

### Software

*   **Python 3.x**
*   **OpenCV:** For video capture and image processing.
*   **MediaPipe:** For pose estimation.
*   **NumPy:** For numerical operations.
*   **Pandas:** For data manipulation (used for storing landmark data).
