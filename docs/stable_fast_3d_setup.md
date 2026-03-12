# Stable Fast 3D Setup Guide

## Status: ✅ Ready (Requires HuggingFace Access)

The environment is set up and ready to use. The only remaining step is to obtain HuggingFace access.

## Quick Start

### 1. Get HuggingFace Access

The model is gated and requires access:

1. **Request Access**: Visit https://huggingface.co/stabilityai/stable-fast-3d and click "Request access"
2. **Create Access Token**: 
   - Go to https://huggingface.co/settings/tokens
   - Create a new token with **read** permissions
   - Copy the token
3. **Login**:
   ```bash
   source .venv/bin/activate
   huggingface-cli login
   # Paste your token when prompted
   ```

### 2. Run the Model

Once logged in:

```bash
cd stable-fast-3d
source ../.venv/bin/activate
python run.py ../images/ME_NEW_26.PNG --output-dir ../output/ --device cpu
```

Or from the project root:

```bash
source .venv/bin/activate
cd stable-fast-3d
python run.py ../images/ME_NEW_26.PNG --output-dir ../output/ --device cpu
```

## Output

The model will generate:
- `output/ME_NEW_26.glb` - 3D mesh file (GLB format, ready for web use)

## Device Options

- `--device cpu` - CPU backend (slower but works everywhere)
- `--device mps` - Apple Silicon GPU (faster, requires `PYTORCH_ENABLE_MPS_FALLBACK=1`)
- `--device cuda:0` - NVIDIA GPU (fastest, if available)

## Additional Options

```bash
python run.py images/ME_NEW_26.PNG \
    --output-dir output/ \
    --device cpu \
    --texture-resolution 1024 \
    --remesh_option triangle
```

## Troubleshooting

### Import Error: uv_unwrapper not found

This has been fixed by adding the path in `run.py`. If you still see this error, ensure you're running from the `stable-fast-3d` directory or that the PYTHONPATH includes it.

### 403 Forbidden Error

You need to:
1. Request access to the model on HuggingFace
2. Login with `huggingface-cli login`

### OpenMP Issues

OpenMP is installed at `/opt/homebrew/opt/libomp/lib/libomp.dylib`. If you see linking errors, ensure this path exists.

## Files Modified

- `stable-fast-3d/run.py` - Added path fix for uv_unwrapper import
