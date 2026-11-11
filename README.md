# 2026년 전자공학실험 Term Project — Sound Equalizer

[한국어](#한국어) | [English](#english)

## 한국어

직접 설계한 필터 회로(lowpass / highpass / bandpass)의 출력을 녹음하여,
이상적인 필터를 통과한 신호와 비교·분석하는 스크립트입니다.

- 입력 신호, 이상적인 필터 출력, 녹음된 회로 출력의 waveform과 spectrogram을 그림으로 저장합니다.
- 이상적인 신호와 녹음된 신호의 유사도를 seg SI-SNR 점수(dB)로 출력합니다. 유사할수록 점수가 높습니다.

실험 절차와 녹음 방법은 `how to use.pdf`를 참고 바랍니다.

### 폴더 구성

| 경로 | 설명 |
|---|---|
| `samples/` | 회로에 입력으로 재생할 음원 `mixed_1.wav` ~ `mixed_5.wav` |
| `recorded/` | 회로 출력을 녹음한 wav 파일을 넣는 폴더 |
| `exps/` | 분석 결과 그림(png)이 저장되는 폴더 |
| `references/` | 이상적인 필터 출력(wav)이 저장되는 폴더 |
| `main.ipynb` | Colab용 분석 노트북 |
| `main.py` | 개인 PC용 분석 스크립트 (내용은 노트북과 동일) |

### 녹음 파일 준비

1. `samples/`의 음원 중 하나를 회로에 입력으로 재생하고, 회로 출력을 녹음합니다.
2. 녹음 파일을 wav로 변환합니다. (m4a 등으로 저장된 경우 온라인 변환기 사용)
3. 파일 이름을 `mixed_{샘플 번호}_{필터 종류}.wav`로 바꿔 `recorded/` 폴더에 넣습니다.
   - 필터 종류는 `lowpass`, `highpass`, `bandpass` 중 하나입니다.
   - 예) 1번 음원으로 lowpass를 실험한 경우: `recorded/mixed_1_lowpass.wav`

### 실행 방법 1: Colab (수업에서 사용)

Google 계정이 필요합니다.

1. 이 저장소에서 `Code` → `Download ZIP`으로 전체 파일을 받아 압축을 풉니다.
2. 압축을 푼 폴더를 본인의 Google Drive에 업로드합니다.
3. Google Drive에서 `main.ipynb`를 Colab으로 엽니다.
4. 노트북의 `colab_basedir`를 업로드한 폴더 경로로 수정합니다.
   - 예) 내 드라이브의 `Colab Notebooks` 폴더에 파일들을 바로 올린 경우:
     `/content/drive/My Drive/Colab Notebooks`
5. `sample_idx`(1~5)와 `filter_mode`(`lowpass` / `highpass` / `bandpass`)를 실험에 맞게 수정합니다.
6. 녹음 파일을 Google Drive의 `recorded/` 폴더에 올린 뒤, 셀을 위에서부터 차례로 실행합니다.

`sample_idx`와 `filter_mode`, `colab_basedir` 외의 코드는 수정하지 않습니다.

### 실행 방법 2: 개인 PC

Python이 설치된 환경(conda 등)에서 실행합니다.

```
pip install -r requirements.txt
python main.py
```

실행 전에 `main.py` 상단의 `sample_idx`와 `filter_mode`를 수정합니다.

### 결과 확인

- 점수: 실행하면 `seg SI-SNR score`가 출력됩니다.
- 그림: `exps/mixed_{샘플 번호}_{필터 종류}.png`
  - 위에서부터 입력 신호(source), 이상적인 필터 출력(ideal), 녹음된 회로 출력(recorded)입니다.
  - 왼쪽은 waveform, 오른쪽은 spectrogram(가로축 시간, 세로축 주파수)입니다.
- 이상적인 필터 출력 음원: `references/mixed_{샘플 번호}_{필터 종류}.wav`

`[Warn]` 메시지가 출력되면 재생한 음원의 앞 또는 뒷부분이 녹음에 다 담기지 않은 것이므로,
재생과 녹음의 시작·종료 시점을 맞춰 다시 녹음하는 것을 권장합니다.

---

## English

**2026 Electronics Engineering Lab Term Project — Sound Equalizer**

This script records the output of the filter circuit you designed (lowpass / highpass / bandpass)
and compares it with the signal produced by an ideal filter.

- It saves a figure with the waveform and spectrogram of the input signal, the ideal filter output, and the recorded circuit output.
- It prints a seg SI-SNR score (dB) that measures how similar the recorded signal is to the ideal one. A higher score means a closer match.

See `how to use.pdf` (written in Korean) for the experiment procedure and how to record.

### Folder structure

| Path | Description |
|---|---|
| `samples/` | Audio files to play into the circuit: `mixed_1.wav` to `mixed_5.wav` |
| `recorded/` | Put the wav files recorded from your circuit output here |
| `exps/` | Result figures (png) are saved here |
| `references/` | Ideal filter outputs (wav) are saved here |
| `main.ipynb` | Analysis notebook for Colab |
| `main.py` | Analysis script for a local PC (same content as the notebook) |

### Preparing the recording

1. Play one of the files in `samples/` into your circuit and record the circuit output.
2. Convert the recording to wav. (Use an online converter if it was saved as m4a or similar.)
3. Rename the file to `mixed_{sample number}_{filter type}.wav` and put it in the `recorded/` folder.
   - The filter type is one of `lowpass`, `highpass`, `bandpass`.
   - Example: lowpass experiment with sample 1 → `recorded/mixed_1_lowpass.wav`

### Option 1: Colab (used in class)

A Google account is required.

1. Download all files from this repository with `Code` → `Download ZIP` and unzip them.
2. Upload the unzipped folder to your Google Drive.
3. Open `main.ipynb` from Google Drive in Colab.
4. Change `colab_basedir` in the notebook to the path of the uploaded folder.
   - Example: if the files are placed directly in the `Colab Notebooks` folder of My Drive:
     `/content/drive/My Drive/Colab Notebooks`
5. Set `sample_idx` (1 to 5) and `filter_mode` (`lowpass` / `highpass` / `bandpass`) for your experiment.
6. Upload your recording to the `recorded/` folder in Google Drive, then run the cells in order from the top.

Do not modify any code other than `sample_idx`, `filter_mode`, and `colab_basedir`.

### Option 2: Local PC

Run in an environment with Python installed (conda, etc.).

```
pip install -r requirements.txt
python main.py
```

Set `sample_idx` and `filter_mode` at the top of `main.py` before running.

### Checking the results

- Score: the `seg SI-SNR score` is printed when you run the code.
- Figure: `exps/mixed_{sample number}_{filter type}.png`
  - From top to bottom: input signal (source), ideal filter output (ideal), recorded circuit output (recorded).
  - Left column: waveform. Right column: spectrogram (x-axis time, y-axis frequency).
- Ideal filter output audio: `references/mixed_{sample number}_{filter type}.wav`

If a `[Warn]` message is printed, the beginning or end of the played audio was not fully captured in the recording.
Re-recording with the start and stop of playback and recording aligned is recommended.
