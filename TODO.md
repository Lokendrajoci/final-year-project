# TODO: Implantable Device Identification in X-rays

## Project Summary
A computer vision framework that localizes and identifies cardiac devices within chest scans to automatically flag manufacturer data, model parameters, and strict MRI safety restrictions.

## Problem Statement
Missing documentation and records require manual X-ray checks for cardiac devices. Accidental or unverified exposure to MRI fields can lead to catastrophic failures and severe patient risks.

## Key Goals
- **Automated Localization:** Bounding box localization of cardiac devices on standard chest radiographs.
- **Fine-Grained Classification:** Models to identify exact manufacturers and device models.
- **Multi-Task Analysis:** Instantly generate specific MRI safety and compatibility profiles.

---

## 📋 Task List

### 1. Project Initialization & Proposal Documentation
- [ ] **Proposal Refactoring:** Update LaTeX proposal files (`Abstract.tex`, `Introduction.tex`, `Methodology.tex`, `ExpectedResults.tex`) to match the Cardiac Implantable Electronic Device (CIED) project scope.
- [ ] **Environment Setup:** Configure Python environment with PyTorch/TensorFlow, OpenCV, Torchvision, Ultralytics, DICOM utilities (`pydicom`), and CUDA support.
- [ ] **Project Structure:** Establish directory structure for raw data, processed annotations, model weights, API services, and web UI.

### 2. Dataset Acquisition & Curation
- [ ] **Data Sourcing:** Collect and aggregate chest radiograph datasets containing cardiac devices (e.g., MIMIC-CXR, NIH ChestX-ray14, public pacemaker/ICD benchmarks).
- [ ] **Bounding Box Annotation:** Create and verify bounding box annotations (YOLO/COCO format) around cardiac devices (Pacemakers, ICDs, CRTs, loop recorders).
- [ ] **Class Labeling:** Assign fine-grained manufacturer labels (Medtronic, Boston Scientific, Abbott/St. Jude, Biotronik, Sorin/LivaNova) and model family series.
- [ ] **MRI Safety Data Integration:** Build a lookup database mapping device manufacturers and model lines to their specific MRI safety profiles (MR Safe, MR Conditional, MR Unsafe, max B0 field strength, SAR limits).
- [ ] **Data Preprocessing & Augmentation:** Implement CLAHE contrast enhancement, normalization, image resizing, and domain-specific augmentations (rotation, subtle noise, brightness adjustments).

### 3. Bounding Box Localization Module
- [ ] **Model Selection:** Benchmark target detection architectures (YOLOv8/v10/v11, Faster R-CNN, DETR) for CIED localization.
- [ ] **Training Pipeline:** Train localization model on annotated chest X-rays.
- [ ] **Evaluation:** Measure performance using mAP@0.5, mAP@0.5:0.95, Precision, Recall, and Intersection over Union (IoU).
- [ ] **ROI Cropping:** Build automated pipeline to extract cropped device region of interest (ROI) for downstream classification.

### 4. Fine-Grained Classification Module
- [ ] **Architecture Design:** Implement fine-grained classification models (e.g., EfficientNet, Swin Transformer, ResNet-50) tailored to distinguish subtle device contours, header shapes, and lead configurations.
- [ ] **Imbalance Handling:** Apply class weighting, focal loss, or oversampling for rare device models.
- [ ] **Model Training & Hyperparameter Tuning:** Train manufacturer and model-level classifiers on cropped device ROIs.
- [ ] **Evaluation Metrics:** Compute Top-1 / Top-3 Accuracy, Macro-F1 score, confusion matrices, and ROC-AUC curves.

### 5. Multi-Task MRI Safety & Compatibility Profiler
- [ ] **Safety Rule Engine:** Develop multi-task inference module to map predicted device identity to precise MRI safety parameters.
- [ ] **Safety Profile Generator:** Output MRI safety categorization (MR Safe, MR Conditional, MR Unsafe), required scan protocols, B0 field strength limits (1.5T / 3.0T), and lead condition flags.
- [ ] **Risk Alert System:** Design immediate high-risk warning flags for unverified or high-risk device exposures.

### 6. System Framework & UI Integration
- [ ] **API Development:** Build lightweight REST API (FastAPI / Flask) accepting chest radiograph uploads (PNG/JPEG/DICOM) and returning detection coordinates, classification results, and safety profiles.
- [ ] **Web Application Interface:** Create an intuitive dashboard UI for radiologists and emergency clinicians displaying:
  - Input radiograph with highlighted bounding box.
  - Detected device manufacturer, model, and confidence score.
  - Prominent color-coded MRI safety status badge.
- [ ] **DICOM Parser:** Add native DICOM tag reading and metadata extraction.

### 7. Validation, Testing & Documentation
- [ ] **End-to-End Testing:** Validate full pipeline execution latency and end-to-end reliability on test X-ray sets.
- [ ] **Safety Audit:** Verify safety profile mapping accuracy against standard manufacturer IFUs (Instructions for Use).
- [ ] **Finalizing Documentation:** Complete final project report, user manual, and code documentation.

---

## 🎯 Application Areas
- **Radiology & Imaging:** Automated pre-MRI screening workflow.
- **Emergency Medicine:** Instant identification of unknown cardiac devices in non-communicative or emergency patients.
- **Clinical Decision Support Systems (CDSS):** Integrated risk alerts in hospital EHR/PACS systems.
- **Hospital Administration:** Audit trail and digital documentation verification.
