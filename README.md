<h2 align="center">
  <a href=#><img src="https://raw.githubusercontent.com/armbian/.github/master/profile/logosmall.png" alt="Armbian logo"></a>
  <br><br>
</h2>

# Armbian Linux Build Framework

## Purpose of This Repository

The **Armbian Linux build framework** creates customizable OS images based on **Debian** or **Ubuntu** for **single-board computers (SBCs)** and embedded devices. It builds a complete Linux system — kernel, bootloader, and root filesystem — with fine-grained control over versions, configuration, firmware, device trees, and system tweaks.

The framework supports **native**, **cross**, and **containerized** builds for multiple architectures (`x86_64`, `aarch64`, `armhf`, `riscv64`) and is suitable for development, testing, production, or automation.

> **Looking for prebuilt images?** Use [Armbian Imager](https://github.com/armbian/imager/releases) — the easiest way to download and flash Armbian to an SD card or USB drive. Available for Linux, macOS, and Windows.

## Quick Start

```bash
git clone https://github.com/armbian/build
cd build
./compile.sh
```

<a href="#quick-start"><img src=".github/README.gif" alt="Build demonstration" width="100%"></a>

## Build Host Requirements

### Hardware

- **RAM:** ≥ 8 GB (less with `KERNEL_BTF=no`)
- **Disk:** ~ 50 GB free space
- **Architecture:** `x86_64`, `aarch64`, or `riscv64`

### Operating System

- **Native builds:** Armbian / Debian 13 (Trixie)
- **Containerized:** any Docker-capable Linux
- **Windows:** WSL2 with Armbian / Debian 13 (Trixie)

### Software

- Superuser privileges (`sudo` or root)
- An up-to-date host system (outdated Docker or related tools can cause failures)

## What's in This Repository

The build framework is written primarily in **Bash** (`compile.sh`, `lib/`, `extensions/`), with helper tooling in **Python**. Board, kernel, u-boot and distribution definitions are plain configuration files consumed by the framework. Continuous integration is orchestrated via **GitHub Actions** workflows in `.github/workflows/`.

| Path | Contents |
| :--- | :--- |
| `compile.sh` | Main entrypoint — invokes the CLI defined under `lib/` |
| `lib/` | Bash framework code: CLI, build steps, artifact handling, tooling |
| `extensions/` | Optional build-time extensions that hook into the framework |
| `config/boards/` | Per-board configuration files (`.conf`, `.csc`, `.wip`, `.eos`, `.tvb`) |
| `config/bootenv/`, `config/bootscripts/` | Board/family boot environment and boot script templates |
| `config/sources/` | Source definitions for SoC families and related components |
| `config/cli/`, `config/distributions/` | Package sets and per-distribution/release configuration |
| `config/its/` | Image Tree Source (`.its`) files used to build image tree binaries |
| `packages/` | Armbian-specific packaging (kernel deb scripts, BSP, `bsp-cli`, `bsp-desktop`, etc.) |
| `patch/` | Kernel, u-boot, ATF, and misc patches, organized per target and version |
| `tools/` | Auxiliary tools (see [`tools/README.md`](tools/README.md)) |
| `action.yml` | Composite GitHub Action ("Rebuild Armbian") that drives image/kernel builds |

### Board configuration classes

Board configs live in `config/boards/` and their file extension indicates support status:

| Extension | Meaning |
| :--- | :--- |
| `.conf` | Supported — current package base |
| `.csc` | Community maintained / unstable |
| `.wip` | Work in progress |
| `.eos` | End of life |
| `.tvb` | TV box (community maintained, best effort) |

See [`config/boards/README.md`](config/boards/README.md) for the full list of board configuration variables (`BOARDFAMILY`, `BOOTCONFIG`, `KERNEL_TARGET`, `SERIALCON`, `MODULES`, `DEFAULT_OVERLAYS`, …).

## Using the GitHub Action

The repository also exposes itself as a reusable composite action (`action.yml`, "Rebuild Armbian") that wraps `./compile.sh` for CI. It checks out this framework alongside [`armbian/os`](https://github.com/armbian/os) and any custom repository, then runs a build with the requested board, kernel branch, release, UI flavor, extensions and compression settings. See `action.yml` for the full list of inputs.

## Continuous Integration

Automated builds, linting, security scans, label/maintainer syncs and other maintenance tasks are handled by GitHub Actions workflows under `.github/workflows/`. For a live overview of runs for this repository see:

👉 **[actions.armbian.com — build](https://actions.armbian.com/?repo=build)**

## Resources

- **[Documentation](https://docs.armbian.com/Developer-Guide_Overview/)** — comprehensive guides for building, configuring, and customizing
- **[Website](https://www.armbian.com)** — news, features, and board information
- **[Blog](https://blog.armbian.com)** — development updates and technical articles
- **[Forums](https://forum.armbian.com)** — community support and discussions

## Contributing

We welcome contributions. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting issues, submitting changes, and working with the framework (patch generation, PR labeling, commit message expectations, etc.).

## Support

### Community forums
Get help from users and contributors on troubleshooting, configuration, and development.
👉 [forum.armbian.com](https://forum.armbian.com)

### Real-time chat
Join discussions with developers and community members on IRC or Discord.
👉 [Community Chat](https://docs.armbian.com/Community_IRC/)

### Paid consultation
For commercial projects, guaranteed response times, or advanced needs, paid support is available from Armbian maintainers.
👉 [Contact us](https://www.armbian.com/contact)

## Contributors

Thank you to everyone who has contributed to Armbian!

<a href="https://github.com/armbian/build/graphs/contributors">
  <img alt="Contributors" src="https://contrib.rocks/image?repo=armbian/build" />
</a>

## Armbian Partners

Our [partnership program](https://forum.armbian.com/subscriptions) supports Armbian's development and community. Learn more about [our Partners](https://armbian.com/partners).

## License

This project is licensed under the **GNU General Public License v2.0**. See [LICENSE](LICENSE) for the full text.
