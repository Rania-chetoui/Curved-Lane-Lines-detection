# Advanced Curved Lane Detection

Computer vision module for real-time curved lane detection, developed as the first component of an Intelligent Autonomous Quad project (in progress).

The module detects lane lines, computes road curvature and vehicle lateral offset, providing the visual foundation for autonomous navigation.

---

## Project context

This module is part of a larger project: an Intelligent Autonomous Quad currently under development. It will later be integrated into:

- Autonomous navigation systems
- Lane following and real-time tracking
- Obstacle detection and avoidance
- Decision-making modules

The current repository is a standalone, functional module. It is not the full system.

---

## What this module does

- White lane detection using HLS color space filtering and thresholding
- Bird's-eye view transformation (perspective warp) to get a top-down road view
- Sliding window search to locate left and right lane pixels
- Polynomial fitting (2nd order) on both lanes to model lane curvature
- Radius of curvature estimation in meters
- Curve direction detection (Left / Right / Straight)
- Vehicle lateral offset relative to lane center, in meters
- Real-time overlay on the original video with all computed metrics

---

## Pipeline

1. Load video frame
2. Perspective warp to bird's-eye view
3. Color filtering (HLS), threshold, Gaussian blur, Canny edges
4. Histogram of white pixels to locate lane bases
5. Sliding window search to extract lane pixels
6. Polynomial fit for each lane
7. Compute curvature radius and lateral offset
8. Project result back onto original frame with overlay

---

## Demo

![Demo](output/demo.gif)

Short GIF showing the result on project_video.mp4.

---

## Folder structure

    advanced-curved-lane-detection/
    ├── input_video/          # Raw input videos
    ├── output/               # Output videos or images with detected lanes
    ├── lane_detection.py     # Main detection script
    ├── requirements.txt      # Python dependencies
    ├── README.md
    └── LICENSE

---

## How to run

Install dependencies:

    pip install -r requirements.txt

Run the lane detection script:

    python lane_detection.py

Make sure project_video.mp4 is in the working directory, or update the path in lane_detection.py.

---

## Requirements

- Python 3.7+
- OpenCV
- NumPy
- Matplotlib

---

## Limitations

- Designed for white lane markings on asphalt. Does not handle dashed, colored, or poorly lit markings.
- Calibration constants (ym_per_pix, xm_per_pix) are specific to the test video resolution and camera setup.
- Single-video pipeline, not yet optimized for live camera streaming.
- No tracking between frames. Each frame is processed independently.

---

## Roadmap

This module will be integrated into the full Intelligent Quad system. Planned extensions:

- Live camera input
- Temporal smoothing between frames
- Integration with obstacle detection
- Coupling with the navigation and decision modules

---

## Note

This is a standalone module. It will later be integrated into a larger Intelligent Quad system currently in progress.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
