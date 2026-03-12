# Stable Fast 3D Setup Status

## Current Status

✅ **Completed:**
- Virtual environment created (`.venv` with Python 3.9.6)
- Stable Fast 3D repository cloned
- Most dependencies installed (PyTorch, transformers, trimesh, rembg, etc.)
- `texture_baker` and `uv_unwrapper` packages built and installed

⚠️ **Issue:**
- `uv_unwrapper` C extension has import issues (segfault on import)
- This appears to be an architecture/linking issue with the C++ extension
- The model requires HuggingFace login/access token

## Required HuggingFace Access

The model is gated and requires:
1. Request access at: https://huggingface.co/stabilityai/stable-fast-3d
2. Create an access token: https://huggingface.co/settings/tokens
3. Login: `huggingface-cli login`

## Next Steps

### Option 1: Fix uv_unwrapper Import

The C extension may need:
- OpenMP runtime installed (for macOS): https://mac.r-project.org/openmp/
- Architecture-specific build flags
- Running from within the `stable-fast-3d` directory

### Option 2: Try Running from Repository Directory

```bash
cd stable-fast-3d
source ../.venv/bin/activate
python run.py ../images/ME_NEW_26.PNG --output-dir ../output/ --device cpu
```

### Option 3: Use MPS Backend (Mac Silicon)

If you have an Apple Silicon Mac:
```bash
export PYTORCH_ENABLE_MPS_FALLBACK=1
python run.py images/ME_NEW_26.PNG --output-dir output/ --device mps
```

## Files Created

- `.venv/` - Virtual environment
- `stable-fast-3d/` - Repository
- `docs/stable_fast_3d_status.md` - This file
