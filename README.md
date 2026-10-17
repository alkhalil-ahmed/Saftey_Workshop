# PPE Safety Monitor

Production-oriented Streamlit dashboard for PPE compliance inspections with the bundled `best (4).pt` YOLO model.

## Run locally

```powershell
cd C:\Users\KALIL\Desktop\ppe-safety-monitor
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
streamlit run app.py
```

The application loads the bundled `best (4).pt` model directly. Its five classes are `Hardhat`, `NO-Hardhat`, `NO-Safety-Vest`, `Person`, and `Safety-Vest`.

## Detection and alert rules

- The renderer uses thin corner-only HUD brackets with only the class label or safety status.
- Person boxes are bright green and labeled `Person [SAFE]` when both hardhat and safety
  vest detections are associated; otherwise they become bright red and labeled
  `Person [NOT SAFE]` after the one-second confirmation delay.
- All five classes emitted by the custom model are rendered with class labels.
- `NO-Hardhat` and `NO-Safety-Vest` trigger alerts only when their box is spatially associated with a `Person` box.
- Associated workers receive a red `Person` box, a high-priority alert banner, and a violation-log entry.
- Video output is encoded to a temporary MP4 and displayed after frame-by-frame processing.

For production deployment, use HTTPS for live camera access and configure the Streamlit server's CORS/XSRF settings according to the deployment environment.
