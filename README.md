# FeelWave
This repository contains the core implementation of the **cross-modal emotion distillation framework**, where an audio-based teacher model transfers emotion-relevant representations to a mmWave-based student model.

## Environment

The experiments were conducted under the following environment:

- Python 3.10.16
- TensorFlow 2.15.0
- Keras 2.15.0  (standalone Keras; tf.keras corresponds to TensorFlow 2.15.0)

## Repository Structure
```text
FeelWave_Code
├── Backbone/                     # Model architectures
│   ├── autopool.py               # AutoPool operator
│   ├── mobilenetv3_variant.py    # MobileNetV3-Small variant (mmWave student)
│   ├── models.py                 # Audio teacher model (TRILL + word timing)
│   └── saved_model_trill/        # Pretrained TRILL checkpoint
│       ├── saved_model.pb
│       └── variables/
│           ├── variables.data-00000-of-00001
│           └── variables.index
│
├── cross_model_transfer.py       # Distillation pipeline (WCL + CE)
│
├── result/                       # Training outputs
│   ├── saved_teacher_model/
│   ├── saved_student_model/
│   ├── fold.json
│   ├── teacher_fold.txt
│   └── distill_fold.txt
