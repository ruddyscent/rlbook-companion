# CLAUDE.md

이 저장소는 Sutton & Barto의 *Reinforcement Learning: An Introduction (2nd Edition)* 을 공부하며 작성한 한국어 학습 노트, 연습문제 풀이, 실험 노트북을 담고 있다.

## 디렉터리 구조

```
chXX/
├── notes.md        # 챕터 학습 노트 (한국어 산문)
├── solutions.md    # 연습문제 풀이 (한국어 산문, 코드 없는 챕터)
├── notes.ipynb     # notes.md + solutions.md를 합친 통합 노트북
├── solutions.ipynb # 코드가 필요한 연습문제 풀이 노트북
└── figures.ipynb   # 책의 그림을 재현하는 실험 노트북
```

챕터마다 구성이 다를 수 있다. 코드가 없는 챕터(ch01, ch03 등)는 `notes.md`와 `solutions.md`를 하나의 `notes.ipynb`로 합친다. 코드가 있는 챕터(ch02, ch04 등)는 `notes.ipynb`(노트 + 간단한 연습문제)와 `solutions.ipynb`(코드 연습문제), `figures.ipynb`(그림 재현)으로 분리할 수 있다.

## notes.ipynb 구성 규칙

`notes.md`와 `solutions.md`를 합쳐 `notes.ipynb`를 만들 때는 다음 순서를 따른다.

1. 챕터 제목 셀 (예: `# 1 소개 (Introduction)`)
2. 책의 절 순서에 따라 notes.md 내용을 마크다운 셀로 배치
3. 각 절과 연관된 연습문제를 해당 절 직후에 삽입 (연습문제 번호와 절 번호가 대응되는 경우)
4. 연습문제가 특정 절에 묶이지 않는 경우, 관련 절 다음에 모아서 배치
5. 요약(Summary)과 역사(History) 등 마무리 절은 연습문제 다음에 배치

셀 타입은 설명과 풀이는 `markdown`, 실행 코드는 `code`로 구분한다. 코드 없는 챕터는 모든 셀이 마크다운이다.

## 한국어 번역 스타일

- 원서의 **용어 원문을 괄호에 병기**한다. 예: `강화학습(reinforcement learning)`, `탐험(exploration)`
- 첫 등장 시에만 원문을 병기하고, 이후에는 한국어 용어만 사용한다.
- 인명은 한국어 발음으로 표기하고 원문을 괄호에 병기한다. 예: `벨만(Bellman)`, `손다이크(Thorndike)`
- 책의 예시와 설명을 한국어로 자연스럽게 풀어 쓰되, 원문의 의미를 충실히 반영한다. 직역보다는 의미 중심의 번역을 지향한다.
- 연습문제 풀이에서는 공식 정답이 아닌 학습 과정에서의 풀이 노트를 작성한다. 풀이 노트는 책의 연습문제 원문을 그대로 옮기지 않고, 번호와 제목만 표기한다. 풀이 내용은 한국어로 서술하되, 필요한 경우 원문의 핵심 문장을 인용할 수 있다.
- 책의 연습문제 원문은 저작권 보호를 위해 그대로 옮기지 않고, 번호와 제목만 표기한다. 풀이 노트에서는 문제의 핵심 아이디어와 풀이 과정을 한국어로 서술하되, 필요한 경우 원문의 핵심 문장을 인용할 수 있다.
- 한국어는 번역투, 지나친 수동형, AI 슬롭처럼 보이는 표현 등이 없는 자연스러운 학술 산문체로 작성한다. 문체는 해라체 종결어미(`~이다`, `~한다`, `~된다`)로 통일한다.
- 이 저장소의 모든 문서는 RLBook에 기반하고 있으므로, 꼭 필요한 경우가 아니라면 `이 책은`, `이 책에서는`, `저자는`과 같은 표현을 사용하지 않도록 한다.

### 주요 용어 통일

| 영어 | 한국어 |
|------|--------|
| reinforcement learning | 강화학습 |
| policy | 정책 |
| reward | 보상 |
| value function | 가치 함수 |
| state | 상태 |
| action | 행동 |
| episode | 에피소드 |
| agent | 에이전트 |
| environment | 환경 |
| exploration | 탐험 |
| exploitation | 활용 |
| greedy | 탐욕적 |
| step-size parameter | 단계 크기 매개변수 |
| temporal-difference | 시간 차분 |
| model-based / model-free | 모델 기반 / 모델을 사용하지 않는 |
| Markov decision process (MDP) | 마르코프 결정 과정 |
| dynamic programming | 동적 계획법 |
| Monte Carlo | 몬테카를로 |

## 개발 환경

- Python 가상환경: `.venv/` (uv로 관리)
- 노트북 실행: `docker compose up` (Jupyter Lab, 기본 포트 8888)
- pre-commit 훅: `nbdev_clean` (노트북 커밋 전 정리)

노트북을 편집할 때는 커밋 전에 pre-commit 훅이 설치되어 있어야 한다.

```bash
uv tool install nbdev pre-commit
nbdev_install_hooks
pre-commit install
```

## 콘텐츠 지침

- 내용은 원서를 충실히 반영하되, 직역보다는 의미 중심의 한국어로 풀어 쓴다.
- 연습문제 풀이는 공식 정답이 아닌 학습 과정의 노트이다.
- 책의 연습문제 원문은 저작권 보호를 위해 그대로 옮기지 않고, 번호와 제목만 표기한다.
- 코드는 Python으로 작성하며, NumPy, Matplotlib, Seaborn 등을 주로 사용한다. 타입 힌트를 포함하여 가독성을 높인다.
- 코드는 해당 코드 셀이 완결성을 갖도록 작성한다. 따라서, 필요한 라이브러리 임포트, 데이터 생성, 시각화 등이 모두 포함되어야 한다. 따라서, 다른 셀과 중복된 코드가 있을 수 있다.
- 수식과 그리스 문자는 LaTeX 표기를 사용한다.
- 강화학습 분야에서 꼭 필요한 용어가 아니라면, 가능한 한 일상적인 용어를 사용하여 쉽게 풀어서 설명한다.