# My-QCM – Multiple-Choice Exam Trainer

A lightweight single-page web app for practicing multiple-choice exams (French *résidanat* medical exams).
Built with plain **HTML, CSS and JavaScript** – no frameworks, no build step.

**Live demo:** https://oussama22-tech.github.io/My-QCM/

![Screenshot](screenshot.png)

## Features

- **Question bank in a separate JSON file** – content and application logic are fully decoupled
- **Custom practice sessions** – filter by exam, topic and answer reliability, choose the number of questions
- **Clinical cases stay together** – questions that share a case are kept in order, even when shuffling
- **Randomized order** using a Fisher–Yates shuffle
- **Strict scoring** – a question counts as correct only if exactly the right set of options is selected, plus a per-option breakdown
- **Immediate feedback** – correct and wrong options are highlighted, with an explanation and source reference
- **Progress tracking** – statistics are saved locally in the browser (`localStorage`)
- **"Redo my mistakes"** mode that replays only previously missed questions
- **Results by topic**, sorted from weakest to strongest
- **Flag and review** questions, then export the notes as JSON
- **Robust loading** – if `questions.json` cannot be fetched, the app offers to load the file manually

## Usability & accessibility

- Keyboard control: **A–E** to select options, **Enter** to validate and continue
- Automatic dark mode (`prefers-color-scheme`) and reduced-motion support (`prefers-reduced-motion`)
- Highly legible typeface (Atkinson Hyperlegible) and visible focus states
- Semantic ARIA attributes for screen readers (`role="group"`, `aria-pressed`)

## Project structure

```
My-QCM/
├── index.html       # Interface, styles and application logic
└── questions.json   # Question bank
```

## Question format

Each entry in `questions.json` looks like this:

```json
{
  "id": "FMT_2025_J1_Q92",
  "source": "FMT 2025 J1, Q92",
  "topic": 7,
  "case": null,
  "question": "…",
  "options": { "A": "…", "B": "…", "C": "…", "D": "…", "E": "…" },
  "answer": ["B"],
  "confidence": "haute",
  "explanation": "…",
  "reference": "…",
  "verified_by_human": false
}
```

New questions can be added without touching the code.

## Run locally

Browsers block loading local JSON files directly, so serve the folder with a small local web server:

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Possible improvements

- Encapsulate the global application state
- Render question content without `innerHTML` to safely handle untrusted data
- Split the code into separate HTML, CSS and JS files
- Add an optional exam timer
