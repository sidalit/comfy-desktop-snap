<div align="center">

<img src="snap/gui/comfy-desktop.png" alt="Comfy Desktop logo" width="128" />

# Comfy Desktop

**Create generative AI workflows from your Linux desktop.**

[![comfy-desktop](https://snapcraft.io/comfy-desktop/badge.svg)](https://snapcraft.io/comfy-desktop)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Comfy Desktop](https://github.com/Comfy-Org/Comfy-Desktop), with support for local and remote ComfyUI servers.

</div>

---

## Getting Started

<a href="https://snapcraft.io/comfy-desktop"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install comfy-desktop
comfy-desktop
```

Launch from the terminal or your application menu. The [`comfyui` server](https://github.com/sidalit/comfyui-snap) is installed and started automatically; closing the desktop leaves it running.

## Configure

| Option | Accepted values | Default |
| --- | --- | --- |
| `server-url` | An HTTP(S) URL without spaces or fragments; empty or unset for automatic selection. | The connected `comfyui` server's address, falling back to `http://127.0.0.1:8188` if unavailable. |

```bash
# Connect to another server
sudo snap set comfy-desktop server-url=http://192.168.1.20:8188

# Return to the local server
sudo snap unset comfy-desktop server-url
```

Reopen the desktop after changing the server address.

Optional permissions:

```bash
sudo snap connect comfy-desktop:password-manager-service   # sign-in storage
sudo snap connect comfy-desktop:removable-media            # /media, /mnt
```

Desktop settings are stored in `~/snap/comfy-desktop/common`. See the [server configuration](https://github.com/sidalit/comfyui-snap#configure) for GPU and service settings.

## Limitations

- Models are downloaded separately. Open **Manager → Model Manager**, choose a model and select **Install**; ordinary browser downloads do not install models on the server.
- Model Manager downloads use the local server's default loopback address. Remote servers apply their own security policy.
- Creating local Python environments from the desktop is disabled; the server snap provides the runtime.
- The desktop cannot start a stopped server. Application updates are managed by snapd.

## Build

```bash
git clone https://github.com/sidalit/comfy-desktop-snap.git
cd comfy-desktop-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/comfy-desktop-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/Comfy-Org/Comfy-Desktop/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/comfy-desktop-snap/blob/main/LICENSE).
