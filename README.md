# virtual-mouse-gesture-control
Developed a system using computer vision and Python to control cursor movement with hand gestures, enabling touch-free interaction.

# 🖱️ AI Virtual Mouse Using Gesture Recognition

**Status:** Completed Project (Archived)
**Tech Stack:** Python, OpenCV, NumPy, PyAutoGUI, MediaPipe

## 📖 Project Overview
Developed a touch-free human-computer interaction system that controls the mouse cursor using hand gestures. The system utilizes a standard webcam to detect hand landmarks in real-time, mapping finger movements to screen coordinates for cursor control and recognizing specific gesture patterns for clicking actions.

## 🏗️ System Architecture
The application follows a linear computer vision pipeline processing 30+ frames per second.

```mermaid
graph TD
    A[Webcam Input] -->|Capture Frame| B(Image Pre-Processing)
    B -->|Flip & Convert RGB| C{Hand Detection Model}
    C -->|No Hand| A
    C -->|Hand Detected| D[Extract 21 Landmarks]
    D --> E[Finger State Analysis]
    
    subgraph "Logic & Mapping"
    E -->|Index Up Only| F[Moving Mode]
    E -->|Index + Middle Up| G[Clicking Mode]
    F --> H[Convert Cam Coords to Screen Coords]
    H --> I[Smooth Movement / Interpolation]
    end
    
    I --> J[Move Cursor]
    G --> K[Calculate Distance < 30px]
    K -->|True| L[Trigger Left Click]

🧠 Key Technical Implementation
1. Hand Tracking & Landmark Extraction
Instead of training a model from scratch, I utilized MediaPipe's lightweight palm detection model. This provided 21 3D hand-knuckle coordinates in real-time.

Index Finger Tip (ID 8): Used as the primary tracking point for the cursor.

Middle Finger Tip (ID 12): Used as the trigger for clicking actions.

2. Coordinate Mapping & Smoothing
One of the biggest challenges was mapping the small camera frame (640x480) to a large screen resolution (1920x1080).

Linear Interpolation: Applied numpy.interp to map the X/Y ranges.

Jitter Reduction: Implemented a smoothing factor (k=5) where Current_X = Previous_X + (Target_X - Previous_X) / k. This eliminated the "shaking" effect common in raw webcam data.

3. Gesture Logic
Navigation: When only the Index finger is up, the system enters "Moving Mode."

Clicking: When both Index and Middle fingers are up and the distance between tips drops below a threshold (approx 30px), a click is simulated using autopy or pyautogui.

🚀 Impact
Achieved a functional prototype with <50ms latency.

Successfully operated in variable lighting conditions due to robust landmark detection rather than simple color masking.
