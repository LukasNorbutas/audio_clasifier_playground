# Emotion classifier in speech audio

*The problem*<br>
Classify the emotion of a speaking person from a short (3 second) audio utterance.

*Datasets* <br>
RAVDESS and TESS datasets, consisting of mostly short (up to 7 seconds) audio files.

*Constraints* <br>
Only the first 3 seconds of every audio file used to avoid cases with extreme padding. Shorter audio clips are padded to 3 seconds.

*Model results* (are bad, but could be improved a lot): <br>
M1: ResNet50 (L2 reg + Dropout): accuracy: 0.5469<br>
M2: ResNet50 (More reg + More dropout) : 0.4500<br>
M3: Custom 3-layer CNN: accuracy: 0.4625<br>

*Lessons learned* <br>
- Audio files can be analyzed as sequences (e.g. with RNNs) or as spectrograms (with CNNs). I only touched upon the tip of the iceberg - analyzed spetrograms with CNNs.
- Audio files are notoriously slow to read. Difficult to come up with a method that is fast and does not require to load imported audio files to memory.
- Preprocessing audio files that are diverse in length, sound, etc. is painful too. 
- Audio from different datasets can vary quite a bit. This suggests that running an audio AI product that can run on audio from diverse, noisy sources requires even more preprocessing/normalization. What I did here was simply use tanh on all audio files during preprocessing. This way we lose some important information though (e.g. differences between clips).
- Neither model converged to any stable results. Validation loss seems to start overfitting right away despite regularization and jumps up and down a lot. Could be remedied by adjusting model complexity, adding augmentation and reviewing differences in datasets.
