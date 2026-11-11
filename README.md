# 2026년 전자공학실험 Term Project — Sound Equalizer

직접 설계한 필터 회로(lowpass / highpass / bandpass)의 출력을 녹음하여,
이상적인 필터를 통과한 신호와 비교·분석하는 스크립트입니다.

- 입력 신호, 이상적인 필터 출력, 녹음된 회로 출력의 waveform과 spectrogram을 그림으로 저장합니다.
- 이상적인 신호와 녹음된 신호의 유사도를 seg SI-SNR 점수(dB)로 출력합니다. 유사할수록 점수가 높습니다.

실험 절차와 녹음 방법은 `how to use.pdf`를 참고 바랍니다.

## 폴더 구성

| 경로 | 설명 |
|---|---|
| `samples/` | 회로에 입력으로 재생할 음원 `mixed_1.wav` ~ `mixed_5.wav` |
| `recorded/` | 회로 출력을 녹음한 wav 파일을 넣는 폴더 |
| `exps/` | 분석 결과 그림(png)이 저장되는 폴더 |
| `references/` | 이상적인 필터 출력(wav)이 저장되는 폴더 |
| `main.ipynb` | Colab용 분석 노트북 |
| `main.py` | 개인 PC용 분석 스크립트 (내용은 노트북과 동일) |

## 녹음 파일 준비

1. `samples/`의 음원 중 하나를 회로에 입력으로 재생하고, 회로 출력을 녹음합니다.
2. 녹음 파일을 wav로 변환합니다. (m4a 등으로 저장된 경우 온라인 변환기 사용)
3. 파일 이름을 `mixed_{샘플 번호}_{필터 종류}.wav`로 바꿔 `recorded/` 폴더에 넣습니다.
   - 필터 종류는 `lowpass`, `highpass`, `bandpass` 중 하나입니다.
   - 예) 1번 음원으로 lowpass를 실험한 경우: `recorded/mixed_1_lowpass.wav`

## 실행 방법 1: Colab (수업에서 사용)

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

## 실행 방법 2: 개인 PC

Python이 설치된 환경(conda 등)에서 실행합니다.

```
pip install -r requirements.txt
python main.py
```

실행 전에 `main.py` 상단의 `sample_idx`와 `filter_mode`를 수정합니다.

## 결과 확인

- 점수: 실행하면 `seg SI-SNR score`가 출력됩니다.
- 그림: `exps/mixed_{샘플 번호}_{필터 종류}.png`
  - 위에서부터 입력 신호(source), 이상적인 필터 출력(ideal), 녹음된 회로 출력(recorded)입니다.
  - 왼쪽은 waveform, 오른쪽은 spectrogram(가로축 시간, 세로축 주파수)입니다.
- 이상적인 필터 출력 음원: `references/mixed_{샘플 번호}_{필터 종류}.wav`

`[Warn]` 메시지가 출력되면 재생한 음원의 앞 또는 뒷부분이 녹음에 다 담기지 않은 것이므로,
재생과 녹음의 시작·종료 시점을 맞춰 다시 녹음하는 것을 권장합니다.
