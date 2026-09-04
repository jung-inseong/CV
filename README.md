# CV — Inseong Jung

Curriculum vitae in XeLaTeX.

**최신 PDF:** [`CV.pdf`](CV.pdf)

## 빌드

**XeLaTeX 전용이다.** `pdflatex`로는 컴파일되지 않는다.

```bash
latexmk -xelatex CV.tex        # CV.pdf 생성
latexmk -xelatex -pvc CV.tex   # 저장할 때마다 자동 재컴파일
latexmk -c                     # 중간 산출물 정리
```

## 구성

| 파일 | 역할 |
|---|---|
| `CV.tex` | 이력 본문 — **여기만 고치면 된다** |
| `simpleresumecv.cls` | 문서 클래스 (템플릿 원본) |
| `Fonts/` | Tinos, GNU FreeFont — **상대경로로 참조하므로 옮기면 안 된다** |
| `CV.pdf` | 빌드 결과. 공유용이라 저장소에 함께 둔다 |

## 폰트 바꾸기

`CV.tex` 상단 설정 블록에서 두 폰트를 갈아끼울 수 있다. 쓰려는 쪽의 `%`를 떼고, 안 쓰는 쪽 4줄에 `%`를 붙이면 된다.

| | 성격 | 분량 |
|---|---|---|
| **Pretendard** (현재) | 산세리프, 현대적 | 좁아서 한 줄에 많이 들어감 |
| **KoPubWorld Batang** | 명조, 학술 문서 느낌 | 넓어서 분량이 다소 늘어남 |

```latex
%% [A] Pretendard
\setmainfont{Pretendard-Regular.otf}
[Path=./Fonts/Pretendard/, BoldFont=Pretendard-Bold.otf, AutoFakeSlant=0.2]

%% [B] KoPubWorld Batang
% \setmainfont{KoPubWorld Batang Medium.ttf}
% [Path=./Fonts/KoPubWorldBatang/, BoldFont=KoPubWorld Batang Bold.ttf, AutoFakeSlant=0.2]
```

**한글은 그냥 쓰면 된다.** 두 폰트 모두 한글 글리프를 가지고 있어서 영문·한글·불릿기호가 한 폰트로 나온다. 예전처럼 한글용 폰트를 따로 얹거나 본문에서 감쌀 필요가 없다.

```latex
정인성. ``정치적 양극화의 다차원성.'' 한국사회학회. 부산, 대한민국.
```

> `Fonts/Tinos/`와 `Fonts/GNUFreeFont/`는 지우면 안 된다. 클래스 파일이 로드 시점에 이 둘을 먼저 읽고, 그 뒤에 `CV.tex`가 덮어쓰는 구조다.

## 크기와 줄간격 바꾸기

같은 설정 블록에 있다. `\fontsize{글자크기}{줄간격}` 형식이고, 두 번째 값이 줄간격이다.

```latex
%% 본문 — 현재 10pt / 13pt (1.3배)
\renewcommand{\normalsize}{\fontsize{10pt}{13pt}\selectfont}

%% 부분별
\renewcommand{\UseTitleFont}{...\fontsize{26pt}{31pt}...}      % 이름
\renewcommand{\UseSubTitleFont}{...\fontsize{9pt}{11pt}...}    % 소속·이메일
\renewcommand{\UseSectionFont}{...\fontsize{9pt}{11pt}...}     % 좌측 섹션 라벨
\renewcommand{\UseDetailFont}{...\fontsize{8.8pt}{10.6pt}...}  % 하위 항목
```

줄간격은 보통 글자크기의 1.2배가 기본이다. 분량을 1페이지로 줄이고 싶으면 본문을 `{9.5pt}{11.4pt}` 정도로 낮춘다.

클래스 파일(`simpleresumecv.cls`)은 건드리지 않고 `CV.tex`에서 덮어쓰는 방식이라, 템플릿 원본은 그대로 남는다.

## 자주 쓰는 문법

```latex
\SectionGap                         % 섹션 사이 여백 (필요한 곳에만)
\Section{목차명}{제목}{PDF북마크}   % 좌측 섹션 라벨

\Entry                              % 항목 시작
\BulletItem   내용 \hfill \DatestampY{2025}        % 불릿 항목 + 우측 날짜
\Gap                                % 항목 사이 간격
\begin{Detail}
\SubBulletItem 세부 내용            % 들여쓴 하위 항목
\end{Detail}

\DatestampY{2025}                   % 2025
\DatestampYM{2026}{08}              % Aug 2026
\DatestampY{2020} -- \DatestampY{2025}
```

**번호 항목** — Conference Presentations 처럼 번호를 매기는 목록에는 `\NumItem`을 쓴다. 번호는 자동으로 올라가므로 항목을 중간에 넣거나 빼도 손댈 필요가 없다.

```latex
\Entry
\ResetNumbering        % 번호를 1부터 다시 시작
\NumItem
Jung, Inseong. (2026, Aug.) ``제목.'' 학회명. 장소.

\Gap
\NumItem
...
```

이 목록은 날짜를 우측 정렬하지 않고 저자 뒤 괄호 안에 넣는다(`(2026, Aug.)`). 원본 docx 형식을 따른 것이다.

번호 자리 너비는 설정 블록의 `\MaxNumberedItem`이 정한다. 지금은 두 자리(`88.`)로 잡혀 있어 항목이 10개를 넘어도 들여쓰기가 흔들리지 않는다.

**들여쓰기 정렬** — 표식(불릿 ■, 번호 1.)과 머리글 텍스트가 **모두 같은 선에서 시작**하도록 맞춰 두었다.

```
Korea University, Seoul, South Korea          <- \Entry
■   Master of Arts in Sociology               <- \BulletItem
Sociology of Culture, Political ...           <- \Entry
1.  Jung, Inseong. (2026, Aug.) ...           <- \NumItem
↑ 같은 선          ↑ 본문도 같은 열
```

표식을 고정폭 상자(`\CVItemCol`)에 **좌측 정렬**로 넣고 본문을 그 뒤에서 시작시키는 방식이다. 상자 너비는 두 자리 번호(`\MaxNumberedItem` = `88.`) 기준이라 항목이 10개를 넘어도 본문 위치가 흔들리지 않고, 폰트를 바꾸면 다시 재므로 정렬이 유지된다.

| 명령 | 쓰임 |
|---|---|
| `\Entry` | 표식 없이 선에서 바로 시작 (기관명, Research Interests) |
| `\BulletItem` | 불릿(■) 항목 |
| `\NumItem` | 번호 항목 (자동 증가) |
| `\Item` | 표식 없이 **본문 열**에서 시작 (표식 있는 항목과 본문만 맞출 때) |
| `\SubBulletItem` | 하위(●) 항목. 본문 열에서 한 단계 안쪽 |

정렬 관련 재정의는 모두 `CV.tex` 안에 있다. 클래스 파일은 건드리지 않았다.

인용부호는 LaTeX 방식으로 쓴다: ``` ``큰따옴표'' ```

## 메모

- 마침표 뒤 여분 공백을 없애려고 `\frenchspacing`을 켜 두었다. 껐다 켜면 줄바꿈이 달라져 우측 날짜가 다음 줄로 밀릴 수 있다.
- `template-baseline` 태그가 템플릿 원본을 가리킨다. `git diff template-baseline`이 곧 내가 채워 넣은 이력이다.
- 기존 `CV_Inseong_JUNG.docx`와 암호로 보호된 PDF는 `.gitignore`로 제외했다. 디스크에는 남아 있고 저장소에만 올라가지 않는다.

## 라이선스

템플릿: [simple-resume-cv](https://github.com/zachscrivena/simple-resume-cv) by Zach Scrivena — Unlicense (public domain).

폰트: Tinos (Apache License 2.0), GNU FreeFont (GPL), Pretendard (SIL Open Font License 1.1), KoPubWorld Batang (한국출판인회의 KoPub 서체).

이력 내용의 권리는 저작자 본인에게 있다.
