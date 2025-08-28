# Requirements Document

## Introduction

This feature implements a complete YOLO-based tooth numbering system for dental panoramic images using the FDI (Fédération Dentaire Internationale) numbering system. The system will train a YOLO model to detect and classify teeth in dental panoramic images, providing accurate tooth identification with bounding boxes and FDI numbers. The dataset consists of approximately 500 dental panoramic images with YOLO-format annotations containing 32 FDI tooth classes.

## Requirements

### Requirement 1: Dataset Management and Preparation

**User Story:** As a data scientist, I want to properly organize and split the dental dataset, so that I can train and evaluate the YOLO model effectively.

#### Acceptance Criteria

1. WHEN the dataset is processed THEN the system SHALL split images into 80% training, 10% validation, and 10% test sets
2. WHEN organizing the dataset THEN the system SHALL ensure images and labels are paired correctly
3. WHEN preparing data THEN the system SHALL verify all 32 FDI tooth classes are represented in the dataset
4. IF an image exists THEN the system SHALL ensure its corresponding YOLO label file exists
5. WHEN splitting data THEN the system SHALL maintain class distribution across train/validation/test sets

### Requirement 2: YOLO Configuration Setup

**User Story:** As a machine learning engineer, I want to configure YOLO training parameters and data paths, so that the model can be trained with optimal settings.

#### Acceptance Criteria

1. WHEN creating configuration THEN the system SHALL generate a data.yaml file with correct train/val/test paths
2. WHEN configuring classes THEN the system SHALL include all 32 FDI tooth classes with proper mapping
3. WHEN setting up training THEN the system SHALL configure input size as 640x640 pixels
4. WHEN initializing model THEN the system SHALL use pretrained YOLO weights (e.g., yolov8s.pt)
5. IF configuration is created THEN the system SHALL validate all paths and class definitions

### Requirement 3: Model Training Implementation

**User Story:** As a researcher, I want to train a YOLO model on the tooth dataset, so that it can accurately detect and classify teeth using FDI numbering.

#### Acceptance Criteria

1. WHEN training starts THEN the system SHALL use any YOLO variant (YOLOv5/YOLOv8/YOLOv11)
2. WHEN training THEN the system SHALL use recommended input size of 640x640 pixels
3. WHEN initializing THEN the system SHALL load pretrained weights for transfer learning
4. WHEN training progresses THEN the system SHALL save training logs, weights, and metrics
5. WHEN training completes THEN the system SHALL save the best model weights
6. IF training fails THEN the system SHALL provide clear error messages and recovery options

### Requirement 4: Model Evaluation and Metrics

**User Story:** As a researcher, I want comprehensive evaluation metrics for the trained model, so that I can assess its performance and submit results.

#### Acceptance Criteria

1. WHEN evaluating THEN the system SHALL test on validation and test sets
2. WHEN calculating metrics THEN the system SHALL generate confusion matrix per class
3. WHEN measuring performance THEN the system SHALL calculate Precision, Recall, mAP@50, and mAP@50-95
4. WHEN creating outputs THEN the system SHALL generate sample prediction images with bounding boxes and FDI IDs
5. WHEN documenting results THEN the system SHALL include training curves (loss/accuracy plots)
6. IF evaluation completes THEN the system SHALL format results for submission requirements

### Requirement 5: Post-Processing and Anatomical Logic

**User Story:** As a dental professional, I want the system to apply anatomical correctness logic, so that tooth predictions follow proper dental anatomy rules.

#### Acceptance Criteria

1. WHEN post-processing THEN the system SHALL separate upper vs lower arch using Y-axis clustering
2. WHEN organizing teeth THEN the system SHALL divide left vs right quadrants using X-midline
3. WHEN sequencing THEN the system SHALL sort teeth horizontally within quadrants and assign FDI sequentially
4. WHEN handling gaps THEN the system SHALL skip numbers where spacing indicates missing teeth
5. IF anatomical rules conflict THEN the system SHALL prioritize spatial relationships over raw predictions

### Requirement 6: FDI Numbering System Compliance

**User Story:** As a dental practitioner, I want accurate FDI tooth numbering, so that tooth identification follows international dental standards.

#### Acceptance Criteria

1. WHEN numbering teeth THEN the system SHALL use two-digit FDI system correctly
2. WHEN assigning quadrants THEN the system SHALL use 1=upper right, 2=upper left, 3=lower left, 4=lower right
3. WHEN numbering positions THEN the system SHALL use 1=central incisor through 8=third molar
4. WHEN validating classes THEN the system SHALL support all 32 tooth classes (11-18, 21-28, 31-38, 41-48)
5. IF class mapping exists THEN the system SHALL maintain consistent class_id to FDI number conversion

### Requirement 7: Output Generation and Visualization

**User Story:** As a researcher, I want comprehensive output files and visualizations, so that I can analyze results and prepare submissions.

#### Acceptance Criteria

1. WHEN generating outputs THEN the system SHALL create prediction images with bounding boxes
2. WHEN labeling predictions THEN the system SHALL display FDI numbers on detected teeth
3. WHEN saving results THEN the system SHALL export confusion matrices and performance metrics
4. WHEN documenting training THEN the system SHALL save loss and accuracy curves
5. WHEN completing evaluation THEN the system SHALL generate summary report with all required metrics