# Comfy Desktop snap

[![comfyui-desktop](https://snapcraft.io/comfyui-desktop/badge.svg)](https://snapcraft.io/comfyui-desktop)

Snap packaging for [Comfy Desktop](https://github.com/Comfy-Org/Comfy-Desktop), a desktop application for ComfyUI generative AI workflows.

Unofficial build, not affiliated with or endorsed by the ComfyUI project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/comfyui-desktop"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install comfyui-desktop
comfyui-desktop
```

Launch Comfy Desktop from the application menu or use the command above. The `comfyui` server snap is installed as a dependency; its service starts automatically and the desktop connects to <http://127.0.0.1:8188>. Closing the desktop leaves the server running.

Models are not included. The server selects a compatible NVIDIA GPU or falls back to CPU mode:

```bash
sudo cp model.safetensors /var/snap/comfyui/common/models/checkpoints/
sudo snap set comfyui cpu=true   # optional: force CPU mode
sudo snap connect comfyui-desktop:password-manager-service   # optional: sign-in storage
sudo snap connect comfyui-desktop:removable-media            # optional: /media, /mnt
```

Desktop settings and downloaded outputs live under `~/snap/comfyui-desktop/common`. You can also add a remote ComfyUI connection in the desktop.

## Known limitations

- The server manages models and its own files; desktop model downloads and local environment installation are not supported. Upload inputs through the ComfyUI interface.
- Python and the GPU runtime are provided by the separate [comfyui snap](https://github.com/sidalit/comfyui-snap).
- The desktop and server update independently through snapd; the desktop's self-updater is disabled.
- Ubuntu Frame kiosk mode is not configured.

## Update to a new upstream release

Change `version` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). Comfy Desktop is AGPL-3.0-or-later-licensed; its dependencies carry their own licenses.
