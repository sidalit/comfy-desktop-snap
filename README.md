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

Launch Comfy Desktop from the application menu or use the command above. The `comfyui` server snap is installed as a dependency and starts automatically. The desktop connects to its configured address, defaulting to <http://127.0.0.1:8188>. Closing the desktop leaves the server running. Set `daemon=false` on the server snap to disable automatic startup; the desktop cannot start a stopped server.

Models are not included. In the desktop, open **Manager → Model Manager**, search for a model and select **Install**, then refresh the model list. The server downloads it into the correct subfolder under `/var/snap/comfyui/common/models` and makes it available to workflows. No folder or permission setup is needed.

Use Model Manager for server downloads; a workflow's ordinary **Download** link downloads a file through the browser without installing it on the server. On NVIDIA hosts the server adds its `torch-cuda` component automatically (snapd 2.68 or later) and uses a compatible GPU; otherwise it runs in CPU mode. The server's `accelerator` option (`auto`, `cpu` or `cuda`) overrides the choice.

```bash
sudo snap set comfyui accelerator=cpu   # optional: force CPU mode
sudo snap connect comfyui-desktop:password-manager-service   # optional: sign-in storage
sudo snap connect comfyui-desktop:removable-media            # optional: /media, /mnt
```

Desktop settings and downloaded outputs live under `~/snap/comfyui-desktop/common`. You can also add a remote ComfyUI connection in the desktop.

## Configuration

Choose a different server without opening the desktop:

```bash
sudo snap set comfyui-desktop server-url=http://192.168.1.20:8188
sudo snap unset comfyui-desktop server-url   # return to the local server
```

The **ComfyUI (snap)** connection follows this configuration on launch. Other connections added in the desktop are unchanged. Reopen the desktop after changing the server's address or port.

## Known limitations

- Model Manager installs models from its catalog. Downloads require the server's default loopback listener; other remote servers follow their own Manager security policy.
- Local environment installation is disabled. Upload inputs through the ComfyUI interface.
- Python and the GPU runtime are provided by the separate [comfyui snap](https://github.com/sidalit/comfyui-snap).
- The desktop and server update independently through snapd; the desktop's self-updater is disabled.

## Update to a new upstream release

Change `version` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). Comfy Desktop is AGPL-3.0-or-later-licensed; its dependencies carry their own licenses.
