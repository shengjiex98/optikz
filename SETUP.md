# Quick Setup Guide

## Prerequisites Check

Before starting, verify you have the required tools:

```bash
# Check Python version (must be 3.11+)
python3 --version

# Check for pdflatex
which pdflatex

# Check for Ghostscript
which gs
```

If missing:

**macOS:**
```bash
brew install --cask mactex
brew install ghostscript
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt-get install texlive-latex-base texlive-latex-extra texlive-pictures ghostscript
```

## Setup with uv (Recommended)

```bash
# 1. Navigate to project
cd /Users/jerry/Projects/optikz-backend

# 2. Create virtual environment
uv venv

# 3. Activate it
source .venv/bin/activate

# 4. Install dependencies
uv pip install -r requirements.txt

# 5. Set your OpenAI API key
export OPENAI_API_KEY="sk-your-key-here"

# 6. Test the installation
python -m cli.main --help
```

## Quick Test Run

```bash
# Add a test diagram image to examples/
# Then run:
python -m cli.main examples/your_diagram.png --iters 2 --open-report
```

## Expected Output

The tool will create a `runs/` directory with:
- `run_YYYYMMDD_HHMMSS/` - Timestamped run directory
  - `final_tikz.tex` - Generated TikZ code
  - `final_standalone.tex` - Compilable LaTeX document
  - `report.html` - Visual report (opens automatically with `--open-report`)
  - `iter_*/` - Rendered images for each iteration

## Next Steps

1. **Read the main [README.md](README.md)** for detailed usage
2. **Add your own diagrams** to `examples/`
3. **Experiment with parameters** (`--iters`, `--threshold`)
4. **Check [optikz_backend/core/llm.py](optikz_backend/core/llm.py)** to customize prompts
5. **Run tests**: `pytest tests/` (requires `uv pip install pytest`)

## Troubleshooting

**"pdflatex not found"**
- Install LaTeX distribution (see Prerequisites Check)

**"gs not found"**
- Install Ghostscript (see Prerequisites Check)

**"OPENAI_API_KEY not set"**
- Export your API key: `export OPENAI_API_KEY="sk-..."`

**LaTeX compilation errors**
- Check `runs/run_*/iter_*/diagram.tex` for malformed TikZ
- The LLM may generate invalid TikZ on first try; refinement usually fixes it

**Low similarity scores**
- Increase `--iters` to allow more refinement iterations
- Try with simpler diagrams first
- Check the HTML report to see visual differences
