# Using Docker Compose

### If you don't have Ollama yet, use Docker Compose for easy installation. Run this command:

```
docker compose up -d --build
```

### For Nvidia GPU Support: Use an additional Docker Compose file:

```
docker compose -f docker-compose.yaml -f docker-compose.gpu.yaml up -d --build
```

For AMD GPU Support: Some AMD GPUs require setting an environment variable for proper functionality:

```
HSA_OVERRIDE_GFX_VERSION=11.0.0 docker compose -f docker-compose.yaml -f docker-compose.amdgpu.yaml up -d --build
```

### AMD GPU Support with HSA_OVERRIDE_GFX_VERSION

For AMD GPU users encountering compatibility issues, setting the HSA_OVERRIDE_GFX_VERSION environment variable is crucial. This variable instructs the ROCm platform to emulate a specific GPU architecture, ensuring compatibility with various AMD GPUs not officially supported. Depending on your GPU model, adjust the HSA_OVERRIDE_GFX_VERSION as follows:

    For RDNA1 & RDNA2 GPUs (e.g., RX 6700, RX 680M): Use HSA_OVERRIDE_GFX_VERSION=10.3.0.
    For RDNA3 GPUs: Set HSA_OVERRIDE_GFX_VERSION=11.0.0.
    For older GCN (Graphics Core Next) GPUs: The version to use varies. GCN 4th gen and earlier might require different settings, such as ROC_ENABLE_PRE_VEGA=1 for GCN4, or HSA_OVERRIDE_GFX_VERSION=9.0.0 for Vega (GCN5.0) emulation.

Ensure to replace <version> with the appropriate version number based on your GPU model and the guidelines above. For a detailed list of compatible versions and more in-depth instructions, refer to the ROCm documentation and the openSUSE Wiki on AMD GPGPU.

Example command for RDNA1 & RDNA2 GPUs:

```
HSA_OVERRIDE_GFX_VERSION=10.3.0 docker compose -f docker-compose.yaml -f docker-compose.amdgpu.yaml up -d --build
```

### To Expose Ollama API: Use another Docker Compose file:

```
docker compose -f docker-compose.yaml -f docker-compose.api.yaml up -d --build
```
