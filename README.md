# stable-projectorz-comfyui-advanced-workflow
Advanced ComfyUI workflow for Stable Projectorz — One-click 4K game asset pipeline


# Stable Projectorz × ComfyUI — Advanced 4K Game Asset Pipeline

> I spent a long time trying to get Stable Projectorz working with ComfyUI — couldn't find working solutions anywhere. Finally got it working AND pushed it to the next level. Sharing the full workflow for free. Hope it helps the community!

![Preview](stable-projectorz-comfyui-advanced-workflow.jpg
)

## What's included

- ✅ Stable Projectorz bridge (Depth ControlNet)
- ✅ Tile ControlNet for upscale detail preservation
- ✅ SDXL + Refiner (two-stage sampling)
- ✅ LoRA Stack (4 simultaneous LoRAs)
- ✅ IP-Adapter for style/color transfer
- ✅ Ultimate SD Upscale (2-pass, up to 4K)
- ✅ IC-Light for post-process lighting control
- ✅ DSINE Normal Map generation
- ✅ VAE Decode Tiled
- ✅ ImageSharpen + ColorCorrect

## Required Custom Nodes

| Node | Link |
|------|------|
| ComfyUI-StableProjectorzBridge | github.com/tianlang0704/ComfyUI-StableProjectorzBridge |
| ComfyUI_UltimateSDUpscale | github.com/ssitu/ComfyUI_UltimateSDUpscale |
| ComfyUI-Impact-Pack | github.com/ltdrdata/ComfyUI-Impact-Pack |
| ComfyUI_IPAdapter_plus | github.com/cubiq/ComfyUI_IPAdapter_plus |
| comfyui-ic-light | github.com/kijai/ComfyUI-IC-Light |
| comfyui_controlnet_aux | github.com/Fannovel16/comfyui_controlnet_aux |
| ComfyUI-post-processing-nodes | github.com/EllangoK/ComfyUI-post-processing-nodes |
| rgthree-comfy | github.com/rgthree/rgthree-comfy |

## Required Models

- Any SDXL base model (tested with WildcardXL Lightning)
- `sd_xl_refiner_1.0.safetensors`
- `4x-ClearRealityV1.pth` → `models/upscale_models/`
- `controlnet-tile-sdxl` (TTPlanet V2 recommended)
- `control-lora-depth-rank256.safetensors`
- `ip-adapter-plus_sdxl_vit-h.safetensors` → `models/ipadapter/`
- `CLIP-ViT-H-14-laion2B-s32B-b79K.safetensors` → `models/clip_vision/`
- `iclight_sd15_fc.safetensors` → `models/IC-Light/`
- `dreamshaper_8.safetensors` (for IC-Light)

## Pipeline Flow
```
Stable Projectorz (3D Model)
    ↓ Depth ControlNet
SDXL KSampler (base, steps 0→10)
    ↓
SDXL Refiner KSampler (steps 10→14)
    ↓
VAE Decode (Tiled)
    ↓
Tile ControlNet + Ultimate SD Upscale (pass 1, x2)
    ↓
Ultimate SD Upscale (pass 2, x2)
    ↓
ImageSharpen → ColorCorrect
    ↓
Projectorz Output (back to Stable Projectorz)
    ↓ (optional)
IC-Light → DSINE Normal Map
```

## Tips

- Bypass Tile ControlNet for faster generation during testing
- Bypass IC-Light and Normal Map if not needed
- IP-Adapter weight 0.8+ for strong style transfer
- For characters: bypass Depth ControlNet, use OpenPose instead
- SDXL Lightning models: keep CFG at 2.0-3.0, steps 12-14

## Credits

Workflow developed with assistance from Claude (Anthropic).
Special thanks to Igor (Stable Projectorz developer https://stableprojectorz.com/ ) and the ComfyUI community.
