# Neural Cassette Modelling 

Neural modeling of cassette tape recorders, specifically trained on the **Tascam Portastudio 424 MkII**.

This project builds upon the work of Otto Mikkonen's [neural-tape-modeling](https://github.com/01tot10/neural-tape-modeling) research, adapting it for cassette tape characteristics rather than reel-to-reel machines.

<p align="center">
<img width="280" height="350" alt="Screenshot 2025-09-04 at 15 24 18" src="https://github.com/user-attachments/assets/6089ad93-e732-49ea-849b-d2bb6602048b" />

## Project Structure

```
neural-cassette-modelling/
├── reference/                    # original research reference
│   └── neural-tape-modeling/     # otto mikkonen's repo as submodule
├── src/                          # cassette-specific implementation
│   ├── models/                   # neural network architectures
│   ├── data/                     # data processing/loading
│   ├── training/                 # training scripts
│   ├── evaluation/               # testing & metrics
│   └── plugin/                   # future real-time plugin code
├── experiments/                  # tascam recordings & configurations
│   ├── recordings/               # raw audio I/O pairs
│   └── configs/                  # training configurations
├── weights/                      # trained model checkpoints
└── vendor/                       # selected dependencies
    ├── micro-tcn/                # tcn architecture
    ├── auraloss/                 # audio loss functions
    └── chow-tape-utils/          # utility functions
```

## Key Differences: Cassette vs Reel-to-Reel

  <p align="center">
      <img width="300" height="170" alt="Screenshot 2025-09-04 at 15 24 38" src="https://github.com/user-attachments/assets/c63dd852-88d7-4af3-b7f1-6b22c80e5267" />


The Tascam Portastudio 424 MkII presents unique modeling challenges:

- **Frequency Response**: More limited bandwidth (typically 40Hz-15kHz)
- **4-Track System**: Built-in mixing and routing capabilities
- **DBX Noise Reduction**: Optional compression/expansion system
- **Tape Speed**: Fixed 1⅞ IPS (vs variable speeds on reel-to-reel)
- **Saturation Characteristics**: Different magnetic particle formulations
- **Wow & Flutter**: Distinct patterns from cassette transport mechanism
- **Crosstalk**: Between adjacent tracks on narrow tape width


## Setup

### Prerequisites
- Python 3.9+
- CUDA-capable GPU (recommended)
- Audio interface for recording training data
- Tascam Portastudio 424 MkII (or similar cassette recorder)

### Installation

1. Clone with submodules:
```bash
git clone --recurse-submodules https://github.com/yourusername/neural-cassette-modelling.git
cd neural-cassette-modelling
```

2. Create Python environment:
```bash
conda env create -f environment.yaml
conda activate neural-cassette
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Data Collection

Recording high-quality training data from your cassette deck:

1. **Test Signals**: Generate sweep tones, impulses, and musical content
2. **Recording Chain**: 
   - Input → Tascam 424 MkII → Output
   - Sample rate: 48kHz or higher
   - Bit depth: 24-bit minimum
3. **Variations**: Record at different input levels to capture saturation curve

## Training

```bash
python src/training/train.py --config experiments/configs/tascam_424.yaml
```

## Future Goals

- [ ] Real-time VST/AU plugin implementation
- [ ] Model different cassette tape types (Type I/II/IV)
- [ ] Emulate specific vintage cassette formulations
- [ ] Add tape age/degradation modeling

## Acknowledgments

- Otto Mikkonen and Eloi Moliner Juanpere for the [neural-tape-modeling](https://github.com/01tot10/neural-tape-modeling) foundation and personal encouragement
- Jatin Chowdhury for [AnalogTapeModel](https://github.com/jatinchowdhury18/AnalogTapeModel) and real-time DSP advise 

