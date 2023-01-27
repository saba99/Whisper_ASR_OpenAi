<h1 align="center">WhisperX</h1>

<p align="left">Whisper-Based Automatic Speech Recognition (ASR) with improved timestamp accuracy using forced alignment.

</p>


This repository refines the timestamps of openAI's Whisper model via forced aligment with phoneme-based ASR models (e.g. wav2vec2.0), multilingual use-case.

<h2 align="left" id="setup">Setup ⚙️</h2>
Install this package using

`pip install git+https://github.com/m-bain/whisperx.git`

If already installed, update package to most recent commit

`pip install git+https://github.com/m-bain/whisperx.git --upgrade`

If wishing to modify this package, clone and install in editable mode:
```
$ git clone https://github.com/m-bain/whisperX.git
$ cd whisperX
$ pip install -e .
```


You may also need to install ffmpeg, rust etc. Follow openAI instructions here https://github.com/openai/whisper#setup.

<h2 align="left" id="example">Usage 💬 (command line)</h2>

### English

Run whisper on example segment (using default params)

    whisperx examples/sample01.wav


For increased timestamp accuracy, at the cost of higher gpu mem, use bigger models and VAD filtering e.g.

    whisperx examples/sample01.wav --model large.en --vad_filter --align_model WAV2VEC2_ASR_LARGE_LV60K_960H

Result using *WhisperX* with forced alignment to wav2vec2.0 large:

https://user-images.githubusercontent.com/36994049/208253969-7e35fe2a-7541-434a-ae91-8e919540555d.mp4

Compare this to original whisper out the box, where many transcriptions are out of sync:

https://user-images.githubusercontent.com/36994049/207743923-b4f0d537-29ae-4be2-b404-bb941db73652.mov

### Other languages

The phoneme ASR alignment model is *language-specific*, for tested languages these models are [automatically picked from torchaudio pipelines or huggingface](https://github.com/m-bain/whisperX/blob/e909f2f766b23b2000f2d95df41f9b844ac53e49/whisperx/transcribe.py#L22).
Just pass in the `--language` code, and use the whisper `--model large`.

Currently default models provided for `{en, fr, de, es, it, ja, zh, nl, uk, pt}`. If the detected language is not in this list, you need to find a phoneme-based ASR model from [huggingface model hub](https://huggingface.co/models) and test it on your data.


#### E.g. German
    whisperx --model large --language de examples/sample_de_01.wav

https://user-images.githubusercontent.com/36994049/208298811-e36002ba-3698-4731-97d4-0aebd07e0eb3.mov


