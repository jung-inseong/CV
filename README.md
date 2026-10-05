# CV — Inseong Jung

Curriculum vitae in LaTeX.

**최신 PDF:** [`CV_classic.pdf`](CV_classic.pdf)

## 빌드

```bash
latexmk -pdf CV_classic.tex      # pdflatex
latexmk -xelatex CV_classic.tex  # xelatex 도 된다
latexmk -c                       # 중간 산출물 정리
```

**두 번 이상 돌려야 한다.** 하단의 `Page 1 of N`은 문서 전체 페이지 수를 참조하는데, 이 값은 1회차 컴파일에서 알 수 없어 `??`로 나오고 2회차에 확정된다. `latexmk`는 필요한 횟수만큼 알아서 반복한다.

VS Code(LaTeX Workshop)용 레시피를 `.vscode/settings.json`에 넣어 두었다. 기본값은 `latexmk (xelatex)`이다.

## 구성

| 파일 | 역할 |
|---|---|
| `CV_classic.tex` | 이력 본문 — **여기만 고치면 된다** |
| `resume.cls` | 문서 클래스. `.tex`와 같은 폴더에 있어야 한다 |
| `CV_classic.pdf` | 빌드 결과. 공유용이라 저장소에 함께 둔다 |

클래스 파일은 건드리지 않고 필요한 설정(이름-소속 간격, 페이지 번호 등)은 `CV_classic.tex` 상단에서 덮어쓴다.

## 자주 쓰는 문법

```latex
\begin{rSection}{Section Name}

{\bf Title}{, Institution} \hfill {2024 -- 2025}
\begin{itemize}
  \item 세부 내용
\end{itemize}
\smallskip
{\bf Next Title}{, Institution} \hfill {2026}
...

\end{rSection}
```

## 라이선스

클래스 파일: `resume.cls` — Trey Hunner, modified by LaTeXTemplates.com (파일 상단 고지 참조).

이력 내용의 권리는 저작자 본인에게 있다.
