[**English**](https://github.com/jmbayu/mini-nanoGPT) | [Français](README.fr.md)

# Mini NanoGPT 🚀

#### Training a GPT can really be this simple?

> Make GPT training fun and approachable! A visual training platform based on [karpathy/nanoGPT](https://github.com/karpathy/nanoGPT).

## 📖 What is this?

Mini-NanoGPT is a tool that helps you get started with training GPT models effortlessly. Whether you're:

* 🎓 A beginner in deep learning
* 👨‍🔬 A researcher
* 🛠️ A developer

Or simply curious about large language models and want to experience their magic,

You can train a model through an intuitive graphical interface!

## ✨ Key Features

### 1. Easy to Use

* 📱 **Visual Interface**: Say goodbye to command line; point-and-click to start training
* 🌍 **Bilingual UI**: Full support for both English and Chinese interfaces
* 🎯 **One-click Operations**: Data preprocessing, training, and text generation — all in one click

### 2. Powerful Features

* 🔤 **Flexible Tokenization**: Supports character-level and GPT-2/Qwen tokenizers, with multilingual support
* 🚄 **Efficient Training**: Supports multi-process acceleration and distributed training
* 📊 **Real-time Feedback**: Live display of training progress and performance
* ⚙️ **Parameter Visualization**: All training parameters can be adjusted directly in the UI
* 🧩 **Model Database**: Easily manage models and reuse training settings anytime

## 🚀 Getting Started

### Option 1: Docker Deployment (Recommended) 🐳

The easiest way to get started!

```bash
# Clone the repository
git clone --depth 1 https://github.com/jmbayu/mini-nanoGPT.git
cd mini-nanogpt

# Start with Docker Compose (recommended)
docker-compose up --build

# Or build and run manually
docker build -t mini-nanogpt .
docker run --gpus all -p 7860:7860 -v $(pwd)/data:/app/data mini-nanogpt
```

This will automatically build the Docker image and run the container. The container will automatically detect your system environment (CPU/GPU). Meanwhile, the `data`, `models`, and `assets` directories in the current working directory will be mounted into the container, allowing you to store data directly in these directories.

Once started, visit http://localhost:7860 to access the application.

### Option 2: Local Installation

First, create a virtual environment with a Python version up to 3.12. This is necessary due to `torch` 2.0 compatibility.

**Using bash:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Using PowerShell:**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Once the virtual environment is activated, install the dependencies:
```bash
# Clone the repository
git clone --depth 1 https://github.com/jmbayu/mini-nanoGPT.git
cd mini-nanogpt

# Install dependencies
pip install -r requirements.txt
```

### 2. Launch the App

```bash
python app.py
```

Open the displayed link in your browser (usually [http://localhost:7860](http://localhost:7860)) to see the training interface!

## 🎮 User Guide

### Step 1: Prepare Data

* Open the "Data Processing" page, paste your training text, and choose a tokenization method. For better results, check the option to use a tokenizer — it will automatically build a vocabulary based on your text.
* If you don't want to use a validation set, check the "Skip validation set" option.
* Click "Start Processing" when you're done.

Here's a small example for demonstration:

![Data Processing](https://github.com/jmbayu/mini-nanoGPT/blob/master/assets/imgs/en_data_process.png?raw=true)

### Step 2: Train the Model

* Switch to the "Training" page, and adjust the parameters as needed (or leave them as default for a quick try).
* The training and validation loss curves are displayed in real time. If you generated a validation set in Step 1, you should see two curves: blue for training loss, orange for validation loss.
* If only one curve is shown, check the terminal output. If you see an error like:

  ```
  Error while evaluating val loss: Dataset too small: minimum dataset(val) size is 147, but block size is 512. Either reduce block size or add more data.
  ```

  it means your `block size` is too large for the validation set. Try reducing it, for example to 128.
* You should now see both loss curves updating dynamically.
* Click "Start Training" and wait for training to complete.

![Training](https://github.com/jmbayu/mini-nanoGPT/blob/master/assets/imgs/en_train.png?raw=true)

#### Evaluation Mode Only?

* This mode lets you evaluate the model's loss on the validation set. Set the `Number of Evaluation Seeds` to any value >0 to activate evaluation-only mode. You'll see how the model performs with different random seeds.

### Step 3: Generate Text

1. Go to the "Inference" page
2. Enter a prompt
3. Click "Generate" and see what the model comes up with!

![Inference](https://github.com/jmbayu/mini-nanoGPT/blob/master/assets/imgs/en_inference.png?raw=true)

### Step 4: Model Comparison

1. Go to the "Comparison" page
2. Select two models to compare — they can even be the same model with different settings
3. Their configurations will be displayed automatically
4. You can input the same prompt and see how both models generate text
5. Or, apply different inference settings (temperature, top\_k, etc.) to compare outputs

![Comparison](https://github.com/jmbayu/mini-nanoGPT/blob/master/assets/imgs/en_comparison.png?raw=true)

## 📁 Project Structure

```
mini-nanogpt/
├── app.py           # App entry point
├── src/             # Configuration and core modules
├── data/            # Data storage
├── out/             # Model checkpoints
└── assets/          # Tokenizer files and other resources
```

## ❓ FAQ

### It's running too slowly?

* 💡 Try reducing batch size or model size
* 💡 Use a GPU to greatly improve speed
* 💡 Increase the evaluation interval

### The generated text isn’t good?

* 💡 Try increasing the training data
* 💡 Tune the model hyperparameters
* 💡 Adjust the temperature during generation

### Want to resume previous training?

* 💡 On the "Training" page, select "resume" under Initialization
* 💡 Point to the previous output directory

## 🤝 Contributing

Suggestions and improvements are welcome! You can:

* Submit an Issue
* Open a Pull Request
* Share your experience using the tool

## 📝 License

This project is open-sourced under the [MIT License](LICENSE).

---

🎉 **Start your GPT journey now!**
