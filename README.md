# huggingface-word-game-lab
# AI 끝말잇기 게임 (AI Word Chain Game with Hugging Face & Gradio)

Hugging Face의 언어 모델(LLM)과 Gradio를 활용하여 만든 AI 기반 영어 끝말잇기 게임입니다. 이 프로젝트는 단순한 게임을 넘어, `transformers` 라이브러리 사용법, 모델 선정 과정, 그리고 인터랙티브 웹 UI 구축까지의 전 과정을 담은 실습 튜토리얼입니다.

<br>

## 데모 스크린샷
<img width="1120" alt="스크린샷 2025-06-22 오전 12 35 20" src="https://github.com/user-attachments/assets/57fa0def-41c3-4aac-b096-5affacd7f52a" />

<br>

## 주요 기능 (Features)

-   **AI 기반 단어 생성**: 사용자가 입력한 단어의 마지막 알파벳을 기반으로, AI(`google/flan-t5-large`)가 다음 단어를 생성합니다.
-   **실시간 단어 유효성 검증**:
    -   **규칙 준수**: 이전 단어의 마지막 글자로 시작하는지 확인합니다.
    -   **중복 방지**: 게임에서 이미 사용된 단어는 사용할 수 없습니다.
    -   **사전 기반 검증**: `NLTK` 영어 단어 사전을 통해 실제로 존재하는 유효한 단어인지 검증합니다.
-   **인터랙티브 웹 UI**: `Gradio`를 활용하여 사용자가 직관적으로 게임을 플레이할 수 있는 웹 인터페이스를 제공합니다.
-   **상태 관리**: 게임이 진행되는 동안 사용된 단어 목록을 지속적으로 관리하여 게임의 규칙을 유지합니다.

<br>

## 기술 스택 (Tech Stack)

| Category      | Technology / Library                                       |
| ------------- | ---------------------------------------------------------- |
| **AI/ML** | `PyTorch`, `Hugging Face Transformers`                     |
| **LLM** | `google/flan-t5-large`                                     |
| **Web UI** | `Gradio`                                                   |
| **NLP-Util** | `NLTK (Natural Language Toolkit)`                          |
| **Language** | `Python 3.11`                                               |

<br>

## 시스템 흐름 (System Flow)

이 프로젝트는 다음과 같은 순서로 작동합니다.

1.  **사용자 입력**: 유저가 Gradio 인터페이스에 단어를 입력하고 'Submit' 버튼을 클릭합니다.
2.  **입력 검증**: 시스템은 사용자가 입력한 단어가 게임 규칙(시작 글자, 중복 여부, NLTK 사전 존재 여부)에 맞는지 확인합니다.
3.  **프롬프트 생성**: 검증이 완료되면, AI에게 다음 단어를 요청하기 위한 프롬프트(지시어)를 생성합니다.
4.  **AI 추론 (Inference)**: 생성된 프롬프트를 `flan-t5-large` 모델에 전달하여 다음 단어를 추론합니다.
5.  **결과 후처리 및 검증**: AI가 생성한 단어 역시 게임 규칙에 맞는지 검증합니다. 유효한 단어가 나올 때까지 필요시 추론을 반복합니다.
6.  **상태 업데이트**: 유효한 AI의 단어를 '사용한 단어 목록'에 추가합니다.
7.  **결과 출력**: 사용자의 단어와 AI의 응답을 Gradio 인터페이스에 표시하여 턴을 넘깁니다.

<br>

## 설치 및 실행 방법 (Installation & How to Run)

### 1. 저장소 복제 (Clone Repository)

```bash
git clone [https://github.com/Hannalee-0622/huggingface-word-game-lab.git](https://github.com/Hannalee-0622/huggingface-word-game-lab.git)
cd huggingface-word-game-lab
```

### 2. 가상 환경 생성 및 활성화 (Recommended)

프로젝트별 독립적인 환경 구성을 위해 가상 환경 사용을 권장합니다.

```bash
# 가상 환경 생성
python -m venv venv

# 가상 환경 활성화 (Windows)
venv\Scripts\activate

# 가상 환경 활성화 (macOS/Linux)
source venv/bin/activate
```

### 3. 필요 라이브러리 설치 (Install Dependencies)

프로젝트에 필요한 라이브러리들을 설치합니다.

```bash
pip install transformers torch gradio nltk
```

### 4. NLTK 단어 사전 다운로드

최초 실행 시 1회에 한해, 영어 단어 사전을 다운로드해야 합니다. Python 환경에서 아래 코드를 실행해주세요.

```python
import nltk
nltk.download('words')
```

### 5. Jupyter Notebook 실행

모든 준비가 완료되었습니다. Jupyter Notebook을 실행하여 프로젝트를 열어주세요.

```bash
jupyter notebook
```

Jupyter Notebook이 실행되면 `Huggingface-Transformers_LAB.ipynb` 파일을 열고, 처음부터 끝까지 모든 셀을 실행합니다. 마지막 셀이 실행되면 Gradio 앱이 실행되며, 터미널에 출력되는 로컬 URL(예: `http://127.0.0.1:7860`)을 웹 브라우저에서 열어 게임을 플레이할 수 있습니다.
