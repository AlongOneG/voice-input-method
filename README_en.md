太好了！以下是你提供的 README 的英文翻译版本，保留了原有结构，并尽量让语义自然、简洁，适合在 GitHub 等平台发布。
<!-- by韦泉宇-->

---

# Low-Latency Offline Speech Input Method Based on FunASR

![Demo webpage](demo/rtxim.png)

Long-press the hotkey to start speaking. The recognized text will be automatically copied to the clipboard, pasted at the current cursor position, and displayed in the text box.

Click the "Traditional/Simplified" conversion button to convert the content in the text box. The converted result will also be copied to the clipboard.

This project is developed with Python 3.10 and requires a desktop environment. KDE is recommended. It also works on Windows (tested with Python 3.10.6 only).

---

## Installation

First, navigate to the `RTXIME` directory:

```bash
cd RTXIME/
```

### Prerequisites

If you are using a Wayland environment, make sure `xdotool` is installed to simulate keyboard input.

For Arch Linux:

```bash
pacman -S xdotool
```

For Ubuntu/Debian:

```bash
sudo apt-get install xdotool
```

Create a virtual environment and install the required dependencies:

```bash
python3 -m venv venv

# For Linux/macOS
venv/bin/pip install -r requirements.txt

# For Windows
venv\Scripts\pip install -r win_requirements.txt
```

---

## Export the ONNX Model

Before running the application, you need to export the ONNX model:

```bash
python model_export.py
```

Then, modify the `model_dir` path in `Qt_ONNX_windows_style.py` to match the exported model directory.

---

## Running the Application

* **On X11 or Windows**:
  Run `Qt_ONNX_windows_style.py` from the virtual environment.
  The default global hotkey is **Scroll Lock** — long-press to speak.

* **On Wayland (KDE)**:
  Run `KDE_Wayland.py` instead.
  The default global hotkey is also **Scroll Lock** — long-press to speak.

---

## Integration with rime-ice Input Method

![Demo webpage](demo/rtxime.png)

For an enhanced input experience, RTXIME supports integration with the `rime-ice` input method. It can extract user word data from rime-ice to enable personalized hotword support.

* This version uses a different model. Export the model using `RTXIME/model_export.py`.

* *(Optional)* Install rime-ice input method. Quick setup guide:
  [https://github.com/Mark24Code/rime-auto-deploy](https://github.com/Mark24Code/rime-auto-deploy)

* Locate the `rime_ice.userdb.txt` file in the rime-ice user directory. Copy its path and set it as the `file_path` variable in `rime_ice2hotwords.py`.

* Run the script:

  ```bash
  python rime_ice2hotwords.py
  ```

  It will extract hotwords into `hotwords.txt` (by default, single Chinese characters are ignored. To include them, set `keep_single_char = False` in the script).

* Then run `Rtxime.py`. It will load `hotwords.txt` and automatically reload changes on-the-fly.

---

## Related Project

If you want to input text on your PC using your phone’s voice input:

**Linux voice input method (alternative approach):**
[https://github.com/pofice/linux-voice-input-method-2](https://github.com/pofice/linux-voice-input-method-2)

---

## FunASR Project Source

[https://github.com/alibaba-damo-academy/FunASR](https://github.com/alibaba-damo-academy/FunASR)

---

