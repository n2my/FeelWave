# FeelWave

### 📥 Code Download

The FeelWave code package can be downloaded here: https://pan.ustc.edu.cn/share/index/8e1ee29b7d6e4a78ae25.

### 🎬 Demo Video

A demonstration of FeelWave is available at:
**YouTube Demo:** [https://youtu.be/j-PLP6Tuc9g](https://youtu.be/j-PLP6Tuc9g).

This repository contains the core implementation of the **cross-modal emotion distillation framework**, where an audio-based teacher model transfers emotion-relevant representations to a mmWave-based student model.

---

## 📦 Environment

The experiments were conducted under the following environment:

* Python 3.10.16
* TensorFlow 2.15.0
* Keras 2.15.0 (standalone Keras; `tf.keras` corresponds to TensorFlow 2.15.0)

---

## 📁 Repository Structure

```
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
```

---

# EmoDataset: Paired mmWave–Audio Emotional Speech Dataset

## 📘 Overview

### 📥 Download Link

The dataset includes:

* **Processed HDF5 files (~3.43 GB)**
* **Raw mmWave + audio data (~87 GB)**
  
The dataset can be downloaded here: https://pan.ustc.edu.cn/share/index/9fb5b7a0cc3247d0bb85.

**EmoDataset** is a paired **mmWave–audio emotional speech** dataset collected in an **IRB-approved** study. Over one month, **27 stage actors** (11 male, 16 female, aged 18–31) were recruited to perform emotional speech while synchronized **mmWave IF signals** and **audio waveforms** were recorded.

The dataset supports research on multimodal emotion sensing, vocal biomechanics, robust speech modeling, and mmWave–audio alignment.

---

## 🎭 Emotion Taxonomy

A six-category emotion set covering a broad valence–arousal range:

* **happy**
* **calm**
* **angry**
* **tense**
* **sad**
* **bored**

Each participant performed all six emotions.

---

## 🗣 Speech Sentences

Participants read 18 command-style sentences from *ok-google.io* (Google, 2021):

```
1. How old is Taylor
2. What is the definition of back end
3. Do I need an umbrella for tomorrow
4. Who invented the wheel
5. When will AA one two five land
6. Convert six millimeters to meters
7. Make a note: message my mom
8. Show me the appointments for tomorrow
9. Set an alarm in six minutes
10. Where were you born
11. What is the time at home
12. What is the weather like
13. What is the temperature outside
14. What is Apple trending at
15. What is six centimeters in meters
16. What is six plus three
17. Open gmail dot com
18. Decrease brightness
```

Each sentence appears multiple times across all emotions.

---

## 📡 Data Modalities

Two data formats are provided:

1. **Processed HDF5 data**
2. **Raw audio + mmWave IF data**

---

## 1. Processed HDF5 Format

Each sample is a group in an HDF5 file with the naming scheme:

```
emotion_sentenceID_subjectID_repeatIndex
```

**Example:**

```
angry_s10_3_2
```

Meaning:

* `angry` — emotion
* `s10` — sentence ("Where were you born")
* `3` — participant ID
* `2` — repetition index

### Keys in each group

* **time_mmwave** — mmWave vocal vibration sequence
* **time_audio** — synchronized audio waveform
* **word_timing_audio** — word-level timing annotations used **only** by the audio teacher model during **offline distillation**; they are **not** used in FeelWave’s online inference and therefore introduce **no latency**

All data are time-aligned.

---

## 2. Raw Data Format

Raw mmWave IF and audio signals are stored in a hierarchical directory structure.

Example path:

```
FeelWave_Data_Raw/mmwave/angry/s1/1/0
```

Meaning:

* `mmwave` — modality
* `angry` — emotion
* `s1` — sentence ID
* `1` — participant ID
* `0` — repetition index

Raw data maintain their native sampling rates and radar frame formats.

---

## 📝 Summary Table

| Component       | Description                                |
| --------------- | ------------------------------------------ |
| Participants    | 27 stage actors (aged 18–31)               |
| Emotions        | happy, calm, angry, tense, sad, bored      |
| Sentences       | 18 phrases from *ok-google.io*             |
| Modalities      | audio + mmWave IF signals                  |
| Formats         | HDF5 (processed), raw (audio & mmWave)     |
| Synchronization | Time-aligned within each sample            |

---

