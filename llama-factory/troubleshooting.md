Please refer https://github.com/NVIDIA/dgx-spark-playbooks/blob/main/nvidia/llama-factory/README.md

Step 4. Install LLaMA Factory with dependencies
Remove the torchaudio dependency (not needed for LLM fine-tuning) to avoid conflicts with the container's optimized PyTorch, then install.

## Remove torchaudio dependency that conflicts with NVIDIA's PyTorch build
sed -i 's/"torchaudio[^"]*",\?//' pyproject.toml

## Install LLaMA Factory with metrics support
pip install -e ".[metrics]"
pip install --no-deps torchaudio

## Error
OSError: Could not load this library: /usr/local/lib/python3.12/dist-packages/torchaudio/lib/libtorchaudio.so


## Fix Applied
Modify the source file to prevent import failure:

File:
LLaMA-Factory/src/llamafactory/data/mm_plugin.py

Comment out:
import torchaudio

