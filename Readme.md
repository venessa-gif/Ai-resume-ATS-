# 📄 AI Resume ATS Checker

Upload a resume (PDF, DOCX or TXT), optionally paste a job description, and get an estimated **ATS score**, a category breakdown, missing keywords, prioritised improvements and example bullet rewrites. Built with **Streamlit** and **Google Gemini Flash**.

> ATS scores are AI-generated estimates. Real ATS software has no universal score, so treat the result as guidance, not a guarantee.

## Features

- Reads PDF, DOCX and TXT resumes
- Estimated ATS score (0-100) with scores for keyword match, formatting, experience, skills, education and readability
- Tailored keyword matching when you paste a job description
- Prioritised improvements (High / Medium / Low) and before/after bullet rewrites
- Quick local checks: email, phone, LinkedIn, standard sections, word count
- Downloadable Markdown report

## Project structure

```
.
├── app.py             # Streamlit app
├── requirements.txt   # Python dependencies
└── README.md
```

## Run locally

1. Install Python 3.10 or newer.
2. Create a virtual environment and install dependencies:

   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Get a free API key at <https://aistudio.google.com/apikey>.
4. Give the app the key, using **one** of these:

   - Create `.streamlit/secrets.toml`:

     ```toml
     GEMINI_API_KEY = "your-key-here"
     ```

   - or set an environment variable: `export GEMINI_API_KEY="your-key-here"`
   - or just paste the key into the sidebar when the app opens.

5. Start the app:

   ```bash
   streamlit run app.py
   ```

## Configuration

| Setting | Where | Default |
| --- | --- | --- |
| `GEMINI_API_KEY` | Streamlit secrets or environment variable | none (can be typed in the sidebar) |
| `GEMINI_MODEL` | Streamlit secrets, environment variable, or the sidebar box | `gemini-3.5-flash` |

If Google releases a newer Flash model, change the model name in the sidebar or set `GEMINI_MODEL`. No code change is needed.

## Deploy on Streamlit Community Cloud

1. Push this repository to GitHub.
2. Go to <https://share.streamlit.io> and sign in with GitHub.
3. Click **Create app**, choose the repository, branch `main`, and main file `app.py`.
4. Open **Advanced settings → Secrets** and add:

   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```

5. Click **Deploy**.

**Never commit your API key.** Keep `.streamlit/secrets.toml` out of GitHub (add it to `.gitignore`).

## Privacy

The text of the uploaded resume (and job description, if provided) is sent to the Google Gemini API for analysis. The app does not store resumes. Avoid uploading documents you are not comfortable sending to a third-party AI service.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| "Almost no text could be extracted" | The PDF is probably a scan or image. Export a text-based PDF or DOCX. |
| "API key looks invalid" | Re-copy the key from AI Studio and check the secret name is exactly `GEMINI_API_KEY`. |
| "Model name was not found" | Change the model in the sidebar to a current Gemini Flash model. |
| "Rate limit or quota reached" | Wait a minute, or enable billing on your Google AI project. |
