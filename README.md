# Balochistan Smart Highway Watch

**Original application name and logo are retained.** This build refines the existing command-centre interface and voice playback while preserving the original Streamlit workflows and Python logic.

## What changed
- Refined responsive dark command-centre styling, cards, metrics, controls, sidebar navigation, and mobile layout.
- Preserved the supplied `logo.png` and the original product name.
- Preserved the existing six operational sections and their workflows: Admin Control Dashboard, Emergency SOS & Welfare, Driver Portal & Journey Risk, Highway Map & Safe Routes, Multilingual Alert & Voice, and Road Clearance & Logs.
- Tuned neural speech rate/pitch for a steadier delivery and improved browser voice selection to prefer the requested language instead of mixing Urdu, Pashto, and Hindi voices.
- Kept Microsoft Edge Neural TTS as the preferred speech engine, with existing gTTS/browser fallbacks.

## Run locally
```bash
python -m pip install -r requirements.txt
streamlit run app.py
```

## Deployment notes
This build deliberately keeps the existing Streamlit/Python runtime rather than replacing it with a new React API layer in one risky step. That is the safest way to preserve every existing feature, database operation, route map, and multilingual voice workflow. A full React migration should be done in staged modules with feature-by-feature acceptance tests before switching production traffic.

For Render, create a **Web Service** with:
- Build command: `pip install -r requirements.txt`
- Start command: `streamlit run app.py --server.port $PORT --server.address 0.0.0.0`

**Important:** SQLite and uploaded custom voice samples are local files. Configure persistent storage for them on Render, or migrate those records/files to a managed database/object store before relying on them in production. Also change any default credentials before public deployment.

## Voice language note
Urdu and English use dedicated neural voices where available; Pashto uses its configured Pashto neural voice where the provider supports it. Balochi currently uses a phonetic Urdu fallback because a reliable dedicated Balochi neural voice is not consistently available in the selected TTS engine. Voice quality can also vary by browser/device for the browser-speech fallback.
