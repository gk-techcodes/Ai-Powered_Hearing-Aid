🔊 AI-Powered Hearing Aid – Real-Time Noise Suppression with DTLN
This project uses a Dual-Path LSTM Network (DTLN) for real-time audio noise suppression. It’s designed for Raspberry Pi (or any edge device) and supports both training and real-time inference using .tflite models.

📁 Project Structure
graphql
Copy
Edit
hearing_aid_DTLN/
├── dataset_16k/           # Clean and noisy audio datasets (16kHz)
├── input_audio/           # Input test files for real-time enhancement
├── output_audio/          # Output files after enhancement
├── plots/                 # Spectrograms and waveform plots
├── pretrained_model/      # Contains model_1.tflite and model_2.tflite
├── scripts/               # All Python code files
│   ├── conv_16k.py        # Converts WAV files to 16kHz mono
│   ├── mix.py             # Mixes clean + noise at fixed SNR (e.g. 5dB)
│   ├── training.py        # Trains DTLN model using TensorFlow
│   ├── de_bug.py          # test script (for 21 sec .wav)
│   ├── test_dtln.py       # Inference test for 10-sec audio
│   ├── DTLN_model.py      # DTLN model architecture and training loop
│   ├── real_time_dtln_audio1.py    # real-time script
│   ├── info_u.py          # (Unknown purpose, probably utilities)
│   ├── test.py, te.py     # (Use-case testing or audio inspection)
│   ├── modef.py           # (Probably model export/tflite helper)

🧪 How to Use

✅ 1. Convert to 16kHz
Convert clean and noise files to mono 16kHz WAVs.

python scripts/conv_16k.py

✅ 2. Mix Clean + Noise
Mix datasets at a fixed SNR to generate training data.


python scripts/mix.py

This will populate:

dataset_16k/processed/clean/
dataset_16k/processed/noisy/

✅ 3. Train the Model
Train the DTLN model on processed data.

python scripts/training.py


🧠 Real-Time Inference
To run real-time inference using pretrained .tflite models:

python scripts/real_time_dtln_audio1.py
🧪 Testing
For a 21-second debug audio test:


python scripts/de_bug.py
For 10-second .wav enhancement:

python scripts/test_dtln.py
Outputs are saved in the output_audio/ folder.

🖼️ Visual Output
Spectrograms and waveform comparisons are saved in the plots/ folder:

<img width="1482" height="942" alt="Screenshot 2025-07-24 142700" src="https://github.com/user-attachments/assets/2dddf4c0-2cd0-4720-b990-04eb7b847467" />


📦 Dependencies
Install Python dependencies:

pip install numpy librosa soundfile tensorflow

For Raspberry Pi, install only:


pip uninstall tensorflow
pip install tflite-runtime

📊 Model Info
Parameter	Value
Sample Rate	16 kHz
Block Length	512 samples
Block Shift	128 samples
Framework	TensorFlow 2
Model Format	.tflite
