# Tooth Numbering YOLO System

A complete YOLO-based tooth detection and FDI numbering system for dental panoramic images, implementing the OralVis AI Research Intern Task specifications.

## Overview

This system implements a comprehensive YOLO-based computer vision pipeline that processes dental panoramic images to detect and classify teeth according to the FDI (Fédération Dentaire Internationale) numbering system. The system handles approximately 500 dental panoramic images with YOLO-format annotations containing 32 FDI tooth classes.

## Key Features

- **Complete FDI System Implementation**: Exact class mapping with immutable order preservation
- **Multi-YOLO Support**: Compatible with YOLOv5, YOLOv8, and YOLOv11
- **Anatomical Post-Processing**: Optional logic for improved anatomical correctness
- **Comprehensive Evaluation**: Full metrics including confusion matrix, precision, recall, mAP@50, mAP@50-95
- **Submission Ready**: Generates all required deliverables for research submission

## Project Structure

```
tooth_numbering_yolo/
├── __init__.py              # Package initialization
├── fdi_system.py           # FDI numbering system implementation
├── config.py               # Configuration settings
├── utils.py                # Utility functions
├── data_manager.py         # Dataset management (Task 2)
├── trainer.py              # YOLO model training (Task 4)
├── evaluator.py            # Model evaluation (Task 5)
└── post_processor.py       # Anatomical post-processing (Task 6)

outputs/
├── dataset/                # Organized train/val/test splits
├── models/                 # Trained model weights
├── results/                # Evaluation results
├── plots/                  # Training curves and visualizations
└── predictions/            # Sample prediction images
```

## FDI Numbering System

The system implements the complete FDI tooth numbering system with **exact class order preservation**:

### Class ID ↔ FDI Reference Table

| Class ID | Tooth (FDI) | Class ID | Tooth (FDI) |
|----------|-------------|----------|-------------|
| 0 | Canine (13) | 16 | Lateral Incisor (22) |
| 1 | Canine (23) | 17 | Lateral Incisor (32) |
| 2 | Canine (33) | 18 | Lateral Incisor (42) |
| 3 | Canine (43) | 19 | Lateral Incisor (12) |
| 4 | Central Incisor (21) | 20 | Second Molar (17) |
| 5 | Central Incisor (41) | 21 | Second Molar (27) |
| 6 | Central Incisor (31) | 22 | Second Molar (37) |
| 7 | Central Incisor (11) | 23 | Second Molar (47) |
| 8 | First Molar (16) | 24 | Second Premolar (15) |
| 9 | First Molar (26) | 25 | Second Premolar (25) |
| 10 | First Molar (36) | 26 | Second Premolar (35) |
| 11 | First Molar (46) | 27 | Second Premolar (45) |
| 12 | First Premolar (14) | 28 | Third Molar (18) |
| 13 | First Premolar (34) | 29 | Third Molar (28) |
| 14 | First Premolar (44) | 30 | Third Molar (38) |
| 15 | First Premolar (24) | 31 | Third Molar (48) |

**CRITICAL**: Class order must not be changed throughout the entire system.

### FDI System Rules

- **First digit** = Quadrant (1=upper right, 2=upper left, 3=lower left, 4=lower right)
- **Second digit** = Tooth position (1=central incisor → 8=third molar)

## Quick Start

### 1. Validate FDI System Implementation

```bash
python validate_fdi_system.py
```

This validates:
- Complete FDI numbering system with exact class mapping
- Immutable class order preservation (CRITICAL requirement)
- Bidirectional class to FDI conversion
- FDI system validation (quadrants 1-4, positions 1-8)
- YOLO data.yaml generation with 32 FDI classes

### 2. Dataset Requirements

Place your dataset in the following structure:
```
ToothNumber_TaskDataset/
├── images/          # ~500 dental panoramic images
└── labels/          # Corresponding YOLO-format .txt files
```

**YOLO Label Format**: `class_id center_x center_y width height` (all normalized 0-1)

## Implementation Status

### Task 1: Project Setup and FDI System Implementation (COMPLETED)

- Complete FDI numbering system with exact class mapping
- FDI system validation (quadrants 1-4, positions 1-8)
- Immutable class order preservation
- Project directory structure
- Configuration and utility modules

### Completed Tasks

- **Task 2**: Dataset Preparation (80/10/10 split)
- **Task 3**: Data Configuration (data.yaml)
- **Task 4**: Model Training (YOLO variants support)
- **Task 5**: Model Evaluation (submission metrics)
- **Task 6**: Post-Processing (anatomical logic)
- **Task 7**: Output Generation (visualizations)
- **Task 8**: System Integration

## Configuration

Key configuration parameters in `config.py`:

```python
# Dataset split ratios
TRAIN_RATIO = 0.8
VAL_RATIO = 0.1
TEST_RATIO = 0.1

# YOLO training configuration
YOLO_CONFIG = {
    "input_size": 640,  # Recommended 640x640
    "batch_size": 16,
    "epochs": 100,
    "pretrained_weights": "yolov8s.pt"
}

# Supported YOLO variants
SUPPORTED_YOLO_VARIANTS = ["yolov5", "yolov8", "yolov11"]
```

## Submission Requirements

The system generates all required submission materials:

1. **Confusion Matrix** (32x32 for all tooth classes)
2. **Performance Metrics**: Precision, Recall, mAP@50, mAP@50-95
3. **Sample Prediction Images** with bounding boxes + FDI IDs
4. **Training Curves** (loss/accuracy plots)

## Anatomical Post-Processing (Optional)

Implements logic to improve anatomical correctness:

- Separate upper vs lower arch using Y-axis clustering
- Divide left vs right quadrants using X-midline detection
- Sort teeth horizontally within quadrants and assign FDI sequentially
- Handle missing teeth by skipping numbers where spacing is wide

## Validation and Testing

The system includes comprehensive validation:

- FDI system compliance checking
- Class order preservation verification
- YOLO label format validation
- Dataset structure validation
- Bidirectional conversion testing

## Logging

All operations are logged to `outputs/tooth_numbering.log` with detailed information about:

- Dataset processing steps
- Training progress and metrics
- Evaluation results
- Error handling and warnings

## Contributing

This implementation follows the exact specifications from the OralVis AI Research Intern Task. The class order and FDI mapping are immutable and must not be modified.

## GitHub Repository

**Repository URL**: https://github.com/SAISriram19/OralVis

## License

Research and educational use only. Part of the OralVis AI Research Intern Task implementation.