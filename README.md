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

# Features
User Features:
* Member Registration & Login
* Workout Routine Access
* Profile Management
* AI Exercise Monito
* Real-time Posture Feedback

# Admin Features:
* Member Management
* Attendance Tracking
* Rank Assignment (Beginner/Intermediate/Advanced)
* System Oversight

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

#  Core Components:
*Presentation Layer
*GUI built with Tkinter/PyQt
*User and Admin dashboards
*Application Layer
*Authentication & Authorization
*Business Logic Controllers
*AI Integration Module
*Data Layer
*File-based Storage System
*Local Data Persistence

#Data Flow:
*text
User Input → Authentication → Session Management → Business Logic → File Storage
Webcam Feed → AI Processing → Pose Analysis → Real-time Feedback → User Display

# Pages Overview
*Authentication Pages:

Login Page
User/Admin role selection
Username/password authentication
Session management
Registration Page
New member sign-up
Profile information collection
Automatic rank assignment

# User Dashboard
 *Main Dashboard
 *Welcome message & user stats
 *Quick access to workouts
 *Attendance summary
 *Workout Section
 *Exercise routines display
 *Progress tracking
 *AI trainer activation
 *Profile Management
 *Personal info update
 *Password change
 *Workout history

#Admin Dashboard:
*Member Management
*View all members
*Edit/delete members
*Assign ranks
*Reset passwords
*Attendance Module
*Daily attendance tracking
*Monthly reports
*Member activity overview
*System Analytics
*Gym statistics
*Member growth charts
*Usage patterns

#AI Trainer Interface:
*Exercise Selection
*Choose from available exercises
*Set repetition goals
*Difficulty levels
*Real-time Monitoring
*Live camera feed
*Pose landmarks overlay
*Repetition counter
*Form feedback display
*Session Summary
*Performance metrics
*Form accuracy score
*Progress Comparsion

## System Architecture

The application follows a simple, layered architecture:

1.  **Input Layer:** This layer is responsible for capturing video from a file or webcam using OpenCV.
2.  **Processing Layer:** This layer uses the MediaPipe library to perform pose estimation on each frame of the video. The results are then passed to the exercise-specific logic.
3.  **Application Logic Layer:** This layer contains the core logic of the application. It uses the pose estimation results to calculate body part angles and count exercise repetitions.
4.  **Output Layer:** This layer displays the video feed with the pose landmarks and real-time feedback on the screen using OpenCV.


# Technology Requirements
Core Technologies:
yaml
Programming Language: Python 3.8+
GUI Framework: Tkinter (built-in)
AI Framework: MediaPipe
Computer Vision: OpenCV
Data Processing: NumPy
Storage: File-based (TXT/JSON)
Detailed Dependencies:
txt

# requirements.txt
mediapipe==0.10.0
opencv-python==4.8.1.78
numpy==1.24.3
Pillow==10.0.0
datetime==4.7
os-sys==2.2.1
Hardware Requirements:
Processor: Intel Core i3 or equivalent
RAM: 4GB minimum, 8GB recommended
Storage: 500MB free space
Camera: 720p webcam or better
OS: Windows 10/11, Ubuntu 18.04+

# Code Implementation
Core Authentication Module
python

# modules/auth/authentication.py
import hashlib
from datetime import datetime

#class Authentication:
    def __init__(self):
        self.users_file = "data/members.txt"
        self.admin_file = "data/admin_credentials.txt"
    
    def hash_password(self, password):
        """Hash password for secure storage"""
        return hashlib.sha256(password.encode()).hexdigest()
    
    def register_user(self, username, password, email, full_name):
        """Register new member"""
        try:
            hashed_pw = self.hash_password(password)
            user_data = f"{username}:{hashed_pw}:{email}:{full_name}:Beginner:Active\n"
            
            with open(self.users_file, 'a') as file:
                file.write(user_data)
            return True
        except Exception as e:
            print(f"Registration error: {e}")
            return False
    
    def login_user(self, username, password, is_admin=False):
        """Authenticate user/login"""
        file_path = self.admin_file if is_admin else self.users_file
        hashed_pw = self.hash_password(password)
        
        try:
            with open(file_path, 'r') as file:
                for line in file:
                    data = line.strip().split(':')
                    if data[0] == username and data[1] == hashed_pw:
                        return True, data
            return False, None
        except FileNotFoundError:
            return False, None
AI Pose Detection Module
python

# modules/ai_trainer/pose_detector.py
import cv2
import mediapipe as mp
import numpy as np

class PoseDetector:
    def __init__(self):
        self.mp_pose = mp.solutions.pose
        self.pose = self.mp_pose.Pose(
            static_image_mode=False,
            model_complexity=1,
            smooth_landmarks=True,
            enable_segmentation=False,
            min_detection_confidence=0.5,
            min_tracking_confidence=0.5
        )
        self.mp_drawing = mp.solutions.drawing_utils
    
    def detect_pose(self, image):
        """Detect human pose in image frame"""
        try:
            # Convert BGR to RGB
            image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
            results = self.pose.process(image_rgb)
            
            # Draw pose landmarks
            if results.pose_landmarks:
                self.mp_drawing.draw_landmarks(
                    image, results.pose_landmarks, self.mp_pose.POSE_CONNECTIONS
                )
            
            return image, results.pose_landmarks
        except Exception as e:
            print(f"Pose detection error: {e}")
            return image, None
    
    def calculate_angle(self, point1, point2, point3):
        """Calculate angle between three points for form analysis"""
        try:
            a = np.array([point1.x, point1.y])
            b = np.array([point2.x, point2.y])
            c = np.array([point3.x, point3.y])
            
            radians = np.arctan2(c[1]-b[1], c[0]-b[0]) - np.arctan2(a[1]-b[1], a[0]-b[0])
            angle = np.abs(radians * 180.0 / np.pi)
            
            if angle > 180.0:
                angle = 360 - angle
                
            return angle
        except:
            return 0
Workout Manager Module
python

# modules/user/workout_manager.py
class WorkoutManager:
    def __init__(self):
        self.workouts_file = "data/workouts.txt"
        self.workouts = self.load_workouts()
    
    def load_workouts(self):
        """Load workout routines from file"""
        workouts = {}
        try:
            with open(self.workouts_file, 'r') as file:
                for line in file:
                    if ':' in line:
                        level, exercises = line.strip().split(':', 1)
                        workouts[level] = exercises.split(';')
            return workouts
        except FileNotFoundError:
            # Default workouts if file doesn't exist
            return {
                'Beginner': ['Push-ups:10', 'Squats:15', 'Plank:30s'],
                'Intermediate': ['Push-ups:20', 'Squats:25', 'Plank:60s', 'Lunges:12'],
                'Advanced': ['Push-ups:30', 'Squats:35', 'Plank:90s', 'Lunges:20', 'Burpees:10']
            }
    
    def get_workout_plan(self, user_level):
        """Get workout plan based on user level"""
        return self.workouts.get(user_level, [])
    
    def update_user_progress(self, username, exercise, completed_reps):
        """Update user workout progress"""
        try:
            with open(f"data/progress_{username}.txt", 'a') as file:
                timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
                file.write(f"{timestamp}:{exercise}:{completed_reps}\n")
            return True
        except Exception as e:
            print(f"Progress update error: {e}")
            return False
File Storage Handler
python

# modules/storage/file_handler.py
import os
from datetime import datetime

class FileHandler:
    def __init__(self):
        self.data_dir = "data/"
        self.ensure_data_directory()
    
    def ensure_data_directory(self):
        """Create data directory if it doesn't exist"""
        if not os.path.exists(self.data_dir):
            os.makedirs(self.data_dir)
    
    def read_file(self, filename):
        """Read data from file"""
        try:
            with open(os.path.join(self.data_dir, filename), 'r') as file:
                return file.readlines()
        except FileNotFoundError:
            return []
    
    def write_file(self, filename, data, mode='a'):
        """Write data to file"""
        try:
            with open(os.path.join(self.data_dir, filename), mode) as file:
                file.write(data + '\n')
            return True
        except Exception as e:
            print(f"File write error: {e}")
            return False
    
    def record_attendance(self, username):
        """Record user attendance"""
        timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        return self.write_file('attendance.txt', f"{username}:{timestamp}")
Main Application Entry Point
python

# main.py
import tkinter as tk
from modules.auth.authentication import Authentication
from modules.user.user_panel import UserPanel
from modules.admin.admin_panel import AdminPanel

class GymManagementSystem:
    def __init__(self, root):
        self.root = root
        self.root.title("Gym Management System")
        self.root.geometry("800x600")
        self.auth = Authentication()
        
        self.show_login_screen()
    
    def show_login_screen(self):
        """Display login interface"""
        # Clear existing widgets
        for widget in self.root.winfo_children():
            widget.destroy()
        
        # Login frame
        login_frame = tk.Frame(self.root)
        login_frame.pack(expand=True)
        
        # Login widgets
        tk.Label(login_frame, text="Gym Management System", font=("Arial", 20)).pack(pady=20)
        
        # Username
        tk.Label(login_frame, text="Username:").pack()
        username_entry = tk.Entry(login_frame)
        username_entry.pack(pady=5)
        
        # Password
        tk.Label(login_frame, text="Password:").pack()
        password_entry = tk.Entry(login_frame, show="*")
        password_entry.pack(pady=5)
        
        # Role selection
        role_var = tk.StringVar(value="user")
        tk.Radiobutton(login_frame, text="Member", variable=role_var, value="user").pack()
        tk.Radiobutton(login_frame, text="Admin", variable=role_var, value="admin").pack()
        
        # Login button
        tk.Button(login_frame, text="Login", 
                 command=lambda: self.handle_login(username_entry.get(), 
                                                 password_entry.get(), 
                                                 role_var.get())).pack(pady=10)
        
        # Register button
        tk.Button(login_frame, text="Register New Member", 
                 command=self.show_registration).pack()
    
    def handle_login(self, username, password, role):
        """Handle user login"""
        is_admin = (role == "admin")
        success, user_data = self.auth.login_user(username, password, is_admin)
        
        if success:
            if is_admin:
                AdminPanel(self.root, user_data)
            else:
                UserPanel(self.root, user_data)
        else:
            tk.messagebox.showerror("Error", "Invalid credentials!")
    
    def show_registration(self):
        """Display registration form"""
        # Implementation for registration screen
        pass

if __name__ == "__main__":
    root = tk.Tk()
    app = GymManagementSystem(root)
    root.mainloop()
    
# Installation & Setup
Step-by-Step Installation:
Clone and Setup

bash
# Clone repository
git clone https://github.com/your-username/gym-management-system.git
cd gym-management-system

# Create virtual environment
python -m venv gym_env
source gym_env/bin/activate  # On Windows: gym_env\Scripts\activate

# Install dependencies
pip install -r requirements.txt
Initialize Data Files

bash
# Create necessary data files
mkdir data
touch data/members.txt
touch data/workouts.txt
touch data/attendance.txt

# Add default admin credentials
echo "admin:5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8:admin@gym.com:System Administrator" > data/admin_credentials.txt
# Default admin password: "password"
Run Application

bash
python main.py

#outputs:
#Homepage:
<img width="1079" height="605" alt="image" src="https://github.com/user-attachments/assets/b6649838-2ca5-44fd-9b5d-9c639d9ed75d" />


#Author:
Tammisetti Bhavani. 

#Contact details:
*Email:tammisettibhavani23@gmail.com

