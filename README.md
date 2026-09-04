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

## 한글

템플릿 기본 폰트에는 한글 글리프가 없어서 Windows의 **Malgun Gothic**을 얹었다. `ucharclasses`가 한글 문자를 만나면 자동으로 폰트를 바꿔주므로 **본문에서 한글을 따로 감쌀 필요가 없다.** 그냥 쓰면 된다.

```latex
정인성. ``정치적 양극화의 다차원성.'' 한국사회학회. 부산, 대한민국.
```

다른 컴퓨터에서 빌드하려면 Malgun Gothic이 있어야 한다. 없으면 `CV.tex`의 `\newfontfamily\KoreanFont{...}`를 `NanumGothic`이나 `Noto Sans KR`로 바꾼다.

## 자주 쓰는 문법

```latex
\Section{목차명}{제목}{PDF북마크}   % 좌측 섹션 라벨

\Entry                              % 항목 시작
\BulletItem   내용 \hfill \DatestampY{2025}        % 큰 항목 + 우측 날짜
\Gap                                % 항목 사이 간격
\begin{Detail}
\SubBulletItem 세부 내용            % 들여쓴 하위 항목
\end{Detail}

\DatestampY{2025}                   % 2025
\DatestampYM{2026}{08}              % Aug 2026
\DatestampY{2020} -- \DatestampY{2025}
```

인용부호는 LaTeX 방식으로 쓴다: ``` ``큰따옴표'' ```

## 메모

- 마침표 뒤 여분 공백을 없애려고 `\frenchspacing`을 켜 두었다. 껐다 켜면 줄바꿈이 달라져 우측 날짜가 다음 줄로 밀릴 수 있다.
- `template-baseline` 태그가 템플릿 원본을 가리킨다. `git diff template-baseline`이 곧 내가 채워 넣은 이력이다.
- 기존 `CV_Inseong_JUNG.docx`와 암호로 보호된 PDF는 `.gitignore`로 제외했다. 디스크에는 남아 있고 저장소에만 올라가지 않는다.

## 라이선스

템플릿: [simple-resume-cv](https://github.com/zachscrivena/simple-resume-cv) by Zach Scrivena — Unlicense (public domain).
폰트: Tinos (Apache License 2.0), GNU FreeFont (GPL).
이력 내용은 저작자 본인에게 있다.
