Below is a solid GitHub-ready `README.md` for your project. Copy/paste it into a file named `README.md` at the repo root and adjust the placeholders (like the demo screenshot, repo name, etc.) if you want.

````md
# Personal Website Chatbot (Gradio + OpenAI + PDF Profile)

A lightweight chatbot you can embed/run for a personal website. It answers questions as “you” using a **system prompt** built from:

- a short **summary** text file (`me/summary.txt`)
- your **PDF profile** (`me/Profile.pdf`) parsed via `pypdf`

It also supports two simple “tools”:
- **record_user_details**: stores interested visitors’ email/name/notes (via Pushover notification)
- **record_unknown_question**: logs any question the bot couldn’t answer (via Pushover notification)

The UI is provided by **Gradio ChatInterface**.

---

## Features

- ✅ Persona-based assistant (“act as {name}”)
- ✅ Context loaded from local files (PDF + summary text)
- ✅ Tool calls for:
  - capturing leads (email/name/notes)
  - recording unknown questions for follow-up
- ✅ Simple Gradio web UI
- ✅ Environment-based secrets using `python-dotenv`

---

## Project Structure

```txt
.
├── app.py                 # (your main script)
├── me/
│   ├── Profile.pdf        # PDF used as additional context
│   └── summary.txt        # Short summary used in system prompt
├── .env                   # environment variables (not committed)
├── requirements.txt       # optional, recommended
└── README.md
````

> Your current code reads `me/Profile.pdf` and `me/summary.txt`. Make sure those exist.

---

## Requirements

* Python 3.9+ recommended
* An OpenAI API key
* A Pushover account (optional but recommended if you want lead logging)

Python packages used:

* `openai`
* `gradio`
* `python-dotenv`
* `requests`
* `pypdf`

---

## Setup

### 1) Clone & create environment

```bash
git clone <YOUR_REPO_URL>
cd <YOUR_REPO_FOLDER>

python -m venv .venv
source .venv/bin/activate   # macOS/Linux
# .venv\Scripts\activate    # Windows
```

### 2) Install dependencies

```bash
pip install -r requirements.txt
```

If you don’t have a `requirements.txt` yet, you can install directly:

```bash
pip install openai gradio python-dotenv requests pypdf
```

### 3) Create your `.env`

Create a file named `.env` in the repo root:

```env
OPENAI_API_KEY=your_openai_key_here

# Optional (for Pushover lead logging / unknown question logging)
PUSHOVER_TOKEN=your_pushover_app_token
PUSHOVER_USER=your_pushover_user_key
```

> If you don’t want Pushover, you can remove/disable the `push()` calls and tool functions.

### 4) Add your profile files

Put these files in the `me/` folder:

* `me/Profile.pdf` (your CV / LinkedIn export / profile PDF)
* `me/summary.txt` (a short “about me” summary)

---

## Run the App

```bash
python app.py
```

Gradio will print a local URL (usually `http://127.0.0.1:7860`)—open it in your browser.

---

## How It Works

1. On startup, the app:

   * loads environment variables (`load_dotenv`)
   * reads text from `me/Profile.pdf`
   * reads text from `me/summary.txt`

2. A system prompt is built combining:

   * your name
   * summary text
   * extracted PDF text

3. The assistant uses OpenAI Chat Completions with **function tools**:

   * `record_unknown_question(question)`
   * `record_user_details(email, name, notes)`

4. When the model triggers a tool call, the program executes it and returns tool output back to the model.

---

## Notes & Tips

### Switching model

You currently use:

```py
model="gpt-4o-mini"
```

You can swap to another model available in your account.

### PDF extraction quality

`pypdf` text extraction quality depends on the PDF. If your PDF is image-based (scanned), it may extract poorly. In that case, convert it to text or use an OCR step before feeding it in.

### Privacy / Security

* Do **not** commit `.env`
* If you store emails, consider writing to a database instead of notifications
* If deploying publicly, add rate limiting and abuse protection

---

## Example `requirements.txt`

If you want one, create `requirements.txt` like this:

```txt
openai>=1.0.0
gradio>=4.0.0
python-dotenv>=1.0.0
requests>=2.0.0
pypdf>=4.0.0
```

---

## License

Choose a license (MIT is common) and add a `LICENSE` file.
If you’re unsure, MIT is a good default for small projects.

---

## Contact

If you’re using this as a personal website assistant, consider adding a line here with your preferred contact method.

```

If you want, I can also generate:
- a `requirements.txt` pinned to exact versions (from your environment)
- a `.gitignore` tailored for Python/Gradio
- a short “Deploy on Render / Hugging Face Spaces” section (with recommended security tweaks)
```
