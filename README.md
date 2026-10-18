<div align="center">

<img src="https://github.com/AbyssWM.png?size=200" width="140" alt="Abyss logo">

# 🍥 Abyss for Debian

**Debian packaging for the complete Abyss Wayland ecosystem.**

[![Debian](https://img.shields.io/badge/debian-forky-a80030?style=flat-square&logo=debian&logoColor=white)](https://www.debian.org/releases/testing/) [![Packages](https://img.shields.io/badge/packages-17-7c3aed?style=flat-square)](#-packages) [![Packaging license](https://img.shields.io/badge/packaging-0BSD-blue?style=flat-square)](LICENSE)

[🌐 Website](https://abysswm.github.io/) · [📖 Install guide](https://abysswm.github.io/wiki/getting-started) · [🌊 Abyss on GitHub](https://github.com/AbyssWM)

</div>

---

> [!WARNING]
> **First release.** Abyss is usable now, but this is the first version: expect bugs and please report them.

## 🚀 Install

Prebuilt `.deb` packages for **Debian forky (testing)** are attached to the GitHub release of every Abyss repository. This downloads the compositor and all libraries it needs, then installs them in one go:

```sh
mkdir abyss-debs && cd abyss-debs
for r in Abyssutils Abyss-scanner Abyssland-protocols Abyssparse Abysswire Abyssgraphics Abyssal Abysstoolkit Abysscursor Abyssland; do
  curl -s https://api.github.com/repos/AbyssWM/$r/releases/latest \
    | grep browser_download_url | grep -o 'https://[^"]*\.deb' | grep -v ubuntu1 | xargs -n1 curl -sLO
done
sudo apt install ./*.deb
```

Want the extra tools too? Add `Abyss-guiutils Xdg-desktop-portal-abyss AbyssPicker AbyssDusk AbyssPaper AbyssLock AbyssPolkit` to the list.

Then pick **Abyssland** in your display manager, or run `start-abyssland` from a TTY.

> [!NOTE]
> Ubuntu users: grab the Ubuntu files instead — see [ubuntu-builds](https://github.com/AbyssWM/ubuntu-builds).

## 🧪 Release support

| Release | Status |
|---|---|
| **Debian forky (testing)** | ✅ 17 / 17 build and install |
| Debian 13 trixie | ⚠️ 16 / 17 — `abyssland` needs newer xkbcommon (≥ 1.11), wayland-protocols (≥ 1.49), libinput (≥ 1.29) |
| LMDE | follows its Debian base — LMDE 7 (trixie) has the same limits |

## 🔨 Build it yourself

Each `packages/<name>/debian/` directory is a normal Debian packaging tree. The helper downloads the pinned source archive, verifies it against `sources.json` and lays out the source tree with a deterministic orig tarball:

```sh
tree=$(python3 tools/prepare-source.py abyssutils --out out/abyssutils | head -1)
cd "$tree" && dpkg-buildpackage -b -us -uc
```

Build in the order of the table below and install each result before building the next one. Changelog series: `forky`.

<details>
<summary>How the packages were verified</summary>

- Built with `dpkg-buildpackage -b` inside official Debian rootfs images (checksums verified), in a rootless user namespace, `-j2`.
- All 17 packages were installed in dependency order inside that root.
- `abyssland` needed two extra build dependencies found this way: `glslang-tools` and `libeis-dev`.
- Not yet done: lintian, test suites (`nocheck`), runtime / session tests.

</details>

## 📋 Packages

Listed in build order — every package only depends on the ones above it.

| # | Package | Source |
|---|---|---|
| 1 | [`abyssutils`](packages/abyssutils/debian) | [Abyssutils](https://github.com/AbyssWM/Abyssutils) |
| 2 | [`abyss-scanner`](packages/abyss-scanner/debian) | [Abyss-scanner](https://github.com/AbyssWM/Abyss-scanner) |
| 3 | [`abyssland-protocols`](packages/abyssland-protocols/debian) | [Abyssland-protocols](https://github.com/AbyssWM/Abyssland-protocols) |
| 4 | [`abyssparse`](packages/abyssparse/debian) | [Abyssparse](https://github.com/AbyssWM/Abyssparse) |
| 5 | [`abysswire`](packages/abysswire/debian) | [Abysswire](https://github.com/AbyssWM/Abysswire) |
| 6 | [`abyssgraphics`](packages/abyssgraphics/debian) | [Abyssgraphics](https://github.com/AbyssWM/Abyssgraphics) |
| 7 | [`abyssal`](packages/abyssal/debian) | [Abyssal](https://github.com/AbyssWM/Abyssal) |
| 8 | [`abysstoolkit`](packages/abysstoolkit/debian) | [Abysstoolkit](https://github.com/AbyssWM/Abysstoolkit) |
| 9 | [`abysscursor`](packages/abysscursor/debian) | [Abysscursor](https://github.com/AbyssWM/Abysscursor) |
| 10 | [`abyssland`](packages/abyssland/debian) | [Abyssland](https://github.com/AbyssWM/Abyssland) |
| 11 | [`abyss-guiutils`](packages/abyss-guiutils/debian) | [Abyss-guiutils](https://github.com/AbyssWM/Abyss-guiutils) |
| 12 | [`xdg-desktop-portal-abyss`](packages/xdg-desktop-portal-abyss/debian) | [Xdg-desktop-portal-abyss](https://github.com/AbyssWM/Xdg-desktop-portal-abyss) |
| 13 | [`abysspicker`](packages/abysspicker/debian) | [AbyssPicker](https://github.com/AbyssWM/AbyssPicker) |
| 14 | [`abyssdusk`](packages/abyssdusk/debian) | [AbyssDusk](https://github.com/AbyssWM/AbyssDusk) |
| 15 | [`abysspaper`](packages/abysspaper/debian) | [AbyssPaper](https://github.com/AbyssWM/AbyssPaper) |
| 16 | [`abysslock`](packages/abysslock/debian) | [AbyssLock](https://github.com/AbyssWM/AbyssLock) |
| 17 | [`abysspolkit`](packages/abysspolkit/debian) | [AbyssPolkit](https://github.com/AbyssWM/AbyssPolkit) |

## ⚖️ License

The packaging in this repository is **0BSD** ([LICENSE](LICENSE)). The packaged software keeps its own licenses — see [LICENSES.md](LICENSES.md).

Maintainer: bb8TheRobot &lt;bb8therobot85@gmail.com&gt;
