# When AI Sees Litter

An interactive Streamlit app that uses a YOLO model to identify common litter and turn a detection into practical disposal guidance for **Shibuya, Tokyo**.

The app currently recognises three categories:

- Clear plastic bottles
- Drink cans
- Styrofoam pieces

It is an educational sorting assistant, not an official waste-collection service. Always follow the instructions for your building and local ward.

## What it does

- Detects litter in an uploaded image or a photo taken with the device camera.
- Draws labelled bounding boxes and shows a count for each detected item.
- Gives Shibuya-specific disposal steps, recycling context, and links to official local guidance.
- Includes an experimental browser-based live-camera mode.
- Explains the relationship between better sorting, recycling, and the UN Sustainable Development Goals.

## Quick start

This project targets Python 3.11.

```bash
git clone <your-repository-url>
cd whenaiseeslitterstreamlit

python -m venv .venv
source .venv/bin/activate

python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m pip install streamlit-webrtc

streamlit run streamlit_app.py
```

Open the local address Streamlit displays, usually <http://localhost:8501>.

> `streamlit-webrtc` is required because the app imports it for the Live (beta) option. It is installed separately above because it is not yet listed in `requirements.txt`.

## Using the app

1. Choose **Upload image** or **Camera**.
2. Add or take a well-lit photo where the litter item is clearly visible.
3. Review the detected items and the disposal cards shown below the image.
4. Use **Advanced settings** only if you need to adjust confidence, overlap, image-size, or minimum-area filters.

For the most dependable experience, use image upload or camera capture. The **Live (beta)** option is experimental and should not yet be relied on for a production deployment.

## Model configuration

By default, the app downloads the model below when it first starts and caches it under `/tmp/models`:

```text
https://raw.githubusercontent.com/Bellzum/streamlit-main/main/new_taco1.pt
```

You can override the model source with environment variables.

### Use a remote model

```bash
export MODEL_URL="https://example.com/path/to/model.pt"
streamlit run streamlit_app.py
```

### Use a model stored in the project or local machine

Set `MODEL_URL` to an empty value so the app uses `LOCAL_MODEL` instead:

```bash
export MODEL_URL=""
export LOCAL_MODEL="new_taco1.pt"
streamlit run streamlit_app.py
```

The current interface maps class IDs in this order: `0 = Clear plastic bottle`, `1 = Drink can`, and `2 = Styrofoam piece`. Use a model trained with that same three-class ordering, otherwise the displayed labels will be inaccurate.

## Project structure

| Path | Purpose |
| --- | --- |
| `streamlit_app.py` | Application interface, model loading, detection, and Shibuya guidance. |
| `requirements.txt` | Python packages for the core application. |
| `packages.txt` | Operating-system packages used by hosted Linux deployments. |
| `.streamlit/config.toml` | Streamlit colour theme. |
| `logo.png` | Application logo. |
| `*.pt` | YOLO model-weight files. |
| `pages/` | Streamlit demonstration pages currently included in the navigation. |

## Deployment notes

- A hosted environment needs Python 3.11, the Python packages above, and the system packages in `packages.txt`.
- If the hosting environment cannot reach the default model URL, supply the weights locally and configure `MODEL_URL=""` plus `LOCAL_MODEL`.
- The live-camera feature requires browser camera permission and is generally most reliable over HTTPS.
- The SDG panel expects `sdg11.png`, `sdg12.png`, and `sdg13.png`; add these assets before a public deployment to avoid missing-image warnings.

## Troubleshooting

| Symptom | What to check |
| --- | --- |
| `ModuleNotFoundError: streamlit_webrtc` | Run `python -m pip install streamlit-webrtc`. |
| Model download fails | Check network access to `MODEL_URL`, or configure a local model as described above. |
| No detections | Use a clearer, closer image; then lower the confidence or minimum-area filters in **Advanced settings**. |
| Wrong item labels | Confirm that the model uses the three class IDs and ordering listed in the model-configuration section. |
| Camera does not open | Allow browser camera access and try serving the app over HTTPS. |

## Reference links

- [Shibuya City: Garbage and recycling](https://www.city.shibuya.tokyo.jp/contents/living-in-shibuya/en/daily/garbage.html)
- [Streamlit documentation](https://docs.streamlit.io/)
- [Ultralytics YOLO documentation](https://docs.ultralytics.com/)
