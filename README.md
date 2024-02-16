# Taein-TTS
<p>
<img src="https://img.shields.io/badge/license-MIT-333333.svg?&style=for-the-badge"/>
<a href="https://icecream0910.github.io/taein-tts/demo" target="_blank"><img src="https://img.shields.io/badge/DEMO-333333.svg?&style=for-the-badge"/></a>
</p>

## Description

Taein-TTS is a project aimed at creating a text-to-speech (TTS) system that reads sentences in my own voice. This repository includes pre-trained models that have been trained using my voice.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Installation

This README focuses on guiding you through the process of synthesizing speech using pre-trained models, rather than detailing the model training process.

1. Clone the huggingface repository:
   [https://huggingface.co/icecream0910/taein-tts](https://huggingface.co/icecream0910/taein-tts)

2. Modify the `run-server.bat` batch file in the `/server` directory to match your actual file paths.

    For example, if your server folder is at `C:\myown-tts\server`, update the file as follows:

    ```bat
    @echo off
    setlocal
    cd /D "%~dp0"
    set MECAB_KO_DIC_PATH=.\mecab\mecab-ko-dic -r .\mecab\mecabrc
    set TTS_MODEL_FILE=C:\myown-tts\server\models\glowtts-v2\best_model.pth.tar
    set TTS_MODEL_CONFIG=C:\myown-tts\server\models\glowtts-v2\config.json
    set VOCODER_MODEL_FILE=C:\myown-tts\server\models\hifigan-v2\best_model.pth.tar
    set VOCODER_MODEL_CONFIG=C:\myown-tts\server\models\hifigan-v2\config.json
    server.exe
    endlocal
    ```

3. Update the `glowtts-v2/config.json` and `hifigan-v2/config.json` files in the `/server/models/` directory with your actual file paths.

    Ensure you double the backslash (`\\`) in the file paths, as shown below:

    - For `glowtts-v2/config.json`:
    ```json
    "stats_path": "C:\\mydata\\tts-server\\models\\glowtts-v2\\scale_stats.npy"
    ```

    - For `hifigan-v2/config.json`:
    ```json
    "stats_path": "C:\\mydata\\tts-server\\models\\hifigan-v2\\scale_stats.npy"
    ```

## Usage

To start the TTS server, execute `run-server.bat`. Once the server is running, you will see the message `INFO:werkzeug: * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)` in the command prompt, indicating that the speech synthesis feature is available through the TTS server. To stop the server, press CTRL+C in the command prompt.

### API

- Text preprocessing: `/tts-server/api/process-text`

    Splits sentences and removes special characters to automatically stitch together and playback multi-line sentences as you type.

- Text Inference: `/tts-server/api/infer-glowtts`

    Synthesizes text to speech. Send the text to be synthesized in the `text` parameter of the URL.
    
    Example:
    ```
    http://localhost:5000/tts-server/api/infer-glowtts?text=hello
    ```

### Text Inference Demo Page

Visit [http://localhost:5000/](http://localhost:5000/) for a demo.

## Contributing

1. Fork the repository (https://github.com/icecream0910/myown-tts/fork).
2. Create a new branch: `git checkout -b feature/<featureName>`.
3. Commit your changes: `git commit -am 'Add <featureName>'`.
4. Push to the branch: `git push origin feature/<featureName>`.
5. Submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

## References

This implementation draws inspiration from the following repositories:

- [SCE-TTS](https://github.com/sce-tts)
- [g2pK](https://github.com/Kyubyong/g2pK)
- [mimic-recording-studio](https://github.com/MycroftAI/mimic-recording-studio)
- [coqui TTS](https://github.com/coqui-ai/TTS)

The datasets below are distributed under the CC-BY 2.0 license, with the original text data provided by the Korea Information Society Development Institute's AI Hub, including Korean dialogue text data and Korean-English translation (parallel) corpus text data.

- [Korean Corpus for Voice Recording](https://github.com/sce-tts/mimic-recording-studio/blob/master/backend/prompts/korean_corpus.csv)
- [SleepingCE Speech Dataset](https://drive.google.com/file/d/1UpoBaZRTJXkTdsoemLBWV48QClm6hpTX/view?usp=sharing)
- [Pre-trained Models for SleepingCE Speech Dataset (Glow-TTS)](https://drive.google.com/file/d/1DMKLdfZ_gzc_z0qDod6_G8fEXj0zCHvC/view?usp=sharing)
- [Pre-trained Models for SleepingCE Speech Dataset (HiFi-GAN)](https://drive.google.com/file/d/1vRxp1RH-U7gSzWgyxnKY4h_7pB3tjPmU/view?usp=sharing)
    - These models were fine-tuned from the model provided by [coqui-ai/TTS](https://github.com/coqui-ai/TTS), trained on the [VCTK dataset](https://datashare.ed.ac.uk/handle/10283/3443), available [here](https://github.com/coqui-ai/TTS/releases/download/v0.0.12/vocoder_model--en--vctk--hifigan_v2.zip).

