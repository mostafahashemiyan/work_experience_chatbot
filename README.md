# Personal Website Chatbot (Gradio + OpenAI + PDF Profile)

A lightweight chatbot you can embed/run for a personal website. It
answers questions as "you" using a system prompt built from:

-   a short summary text file (`me/summary.txt`)
-   your PDF profile (`me/Profile.pdf`) parsed via `pypdf`

It also supports two simple tools: - record_user_details: stores
interested visitors' email/name/notes (via Pushover notification) -
record_unknown_question: logs any question the bot couldn't answer (via
Pushover notification)

The UI is provided by Gradio ChatInterface.

------------------------------------------------------------------------

## Features

-   Persona-based assistant ("act as {name}")
-   Context loaded from local files (PDF + summary text)
-   Tool calls for:
    -   capturing leads (email/name/notes)
    -   recording unknown questions for follow-up
-   Simple Gradio web UI
-   Environment-based secrets using python-dotenv

------------------------------------------------------------------------

## Project Structure

. ├── app.py ├── me/ │ ├── Profile.pdf │ └── summary.txt ├── .env ├──
requirements.txt └── README.md

------------------------------------------------------------------------

## Requirements

-   Python 3.9+ recommended
-   OpenAI API key
-   Pushover account (optional for logging)

Python packages: - openai - gradio - python-dotenv - requests - pypdf

------------------------------------------------------------------------

## Setup

### 1) Clone & create environment

git clone `<YOUR_REPO_URL>`{=html} cd `<YOUR_REPO_FOLDER>`{=html}

python -m venv .venv source .venv/bin/activate \# macOS/Linux \#
.venv`\Scripts`{=tex}`\activate  `{=tex}\# Windows

### 2) Install dependencies

pip install -r requirements.txt

If you don't have a requirements.txt:

pip install openai gradio python-dotenv requests pypdf

### 3) Create .env

OPENAI_API_KEY=your_openai_key_here
PUSHOVER_TOKEN=your_pushover_app_token
PUSHOVER_USER=your_pushover_user_key

### 4) Add your profile files

Put these in the me/ folder: - me/Profile.pdf - me/summary.txt

------------------------------------------------------------------------

## Run the App

python app.py

Gradio will print a local URL (usually http://127.0.0.1:7860).

------------------------------------------------------------------------

## How It Works

1.  Loads environment variables
2.  Extracts text from Profile.pdf
3.  Reads summary.txt
4.  Builds a system prompt combining your persona and background
5.  Uses OpenAI Chat Completions with function tools
6.  Executes tool calls when triggered by the model

------------------------------------------------------------------------

## Example requirements.txt

openai\>=1.0.0 gradio\>=4.0.0 python-dotenv\>=1.0.0 requests\>=2.0.0
pypdf\>=4.0.0

------------------------------------------------------------------------

## License

MIT (recommended)
