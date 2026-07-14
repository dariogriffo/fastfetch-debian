# fastfetch-debian

Debian and Ubuntu packaging for [fastfetch](https://github.com/fastfetch-cli/fastfetch)
— a neofetch-like tool for fetching system information and displaying it in a
pretty way.

The Debian archive ships fastfetch, but frozen at release time; this repository
tracks upstream releases (usually within hours) while following the archive's
file layout (presets under /usr/share/fastfetch/presets, bash/fish/zsh
completions, gzipped man page — no flashfetch, no bundled licenses dir).
Served from **[deb.griffo.io](https://deb.griffo.io)** for Debian (bookworm,
trixie, forky, sid) and Ubuntu (jammy, noble, questing, resolute) on amd64,
arm64, armel, armhf, ppc64el, s390x, riscv64 and i386.

## Install

```bash
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://deb.griffo.io/EA0F721D231FDD3A0A17B9AC7808B4DD62C41256.asc | sudo gpg --dearmor --yes -o /etc/apt/keyrings/deb.griffo.io.gpg
echo "deb [signed-by=/etc/apt/keyrings/deb.griffo.io.gpg] https://deb.griffo.io/apt $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/deb.griffo.io.list > /dev/null
sudo apt update
sudo apt install -y fastfetch
```

## How it works

- `check-upstream.yml` polls upstream hourly; a new release dispatches `release.yml`.
- `release.yml` builds binary packages (Docker, per suite × architecture, from
  upstream release tarballs) and source packages (`.dsc`), then publishes a
  GitHub release tagged `<version>+<build>`.
- The deb.griffo.io mirror ingests published releases automatically.

Manual build: `./build.sh <version> <build> [arch|all]` (e.g. `./build.sh 2.66.0 1 all`).

## Links

- Upstream: https://github.com/fastfetch-cli/fastfetch
- Site page: https://deb.griffo.io/install-latest-fastfetch-in-debian.html
- Repository: https://deb.griffo.io
