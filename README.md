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
