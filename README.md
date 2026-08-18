<p align="center">
  <img width="1024" height="408" alt="image" src="https://comprafacil-bucket.s3.us-east-1.amazonaws.com/static/images/Gemini_Generated_Image_2q0b0h2q0b0h2q0b.jpeg" />
</p>

<p align="center">
  <strong>Revisión de código con IA, agnóstica de proveedor</strong><br>
  Usa Claude, Gemini, Codex, OpenCode, Cursor Agent, Kilo, Kiro, Ollama, LM Studio, GitHub Models, MiniMax o cualquier IA para hacer cumplir tus estándares de código.<br>
  Núcleo en Bash puro. Funciona en cualquier entorno.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/version-2.10.1-blue.svg" alt="Version">
  <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License">
  <img src="https://img.shields.io/badge/bash-5.0%2B-orange.svg" alt="Bash">
  <img src="https://img.shields.io/badge/platforms-macOS%20%7C%20Linux%20%7C%20Windows-lightgrey.svg" alt="Platforms">
  <img src="https://img.shields.io/badge/homebrew-tap-FBB040.svg" alt="Homebrew">
  <img src="https://img.shields.io/badge/tests-266%20passing-brightgreen.svg" alt="Tests">
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome">
</p>

<p align="center">
  <a href="#-instalación">Instalación</a> •
  <a href="#-inicio-rápido">Inicio Rápido</a> •
  <a href="#-proveedores">Proveedores</a> •
  <a href="#-comandos">Comandos</a> •
  <a href="#-documentación">Documentación</a>
</p>

---

## Ejemplo

<img width="962" height="941" alt="image" src="https://github.com/user-attachments/assets/c8963dff-6aa5-420c-b58b-1416e81af384" />

## 🎯 ¿Por qué?

Tienes estándares de código. Tu equipo los ignora. Las code reviews detectan los problemas demasiado tarde.

**GGA** se ejecuta en cada commit, validando los archivos staged contra tu `AGENTS.md`. Como tener un desarrollador senior revisando cada línea antes de que llegue al repo.

```
┌─────────────────┐     ┌──────────────┐     ┌─────────────────┐
│   git commit    │ ──▶ │  AI Review   │ ──▶ │  ✅ Pass/Fail   │
│  (staged files) │     │  (any LLM)   │     │  (with details) │
└─────────────────┘     └──────────────┘     └─────────────────┘
```

- 🔌 **Agnóstico de proveedor** — Claude, Gemini, Codex, OpenCode, Cursor Agent, Kilo, Kiro, Ollama, LM Studio, GitHub Models, MiniMax
- 📦 **Núcleo en Bash puro** — sin runtime ni frameworks; algunos proveedores pueden requerir su propio CLI o tooling de API
- 🪝 **Nativo de Git** — Hook estándar pre-commit
- ⚡ **Caché inteligente** — Omite archivos sin cambios
- 🔍 **Modo de revisión de PR** — Revisa PRs completos, no solo el último commit
- 🪟 **Multiplataforma** — macOS, Linux, Windows (Git Bash), WSL

---

## 📦 Instalación

### Homebrew 

```bash
brew install gentleman-programming/tap/gga
```

### Manual (recomendado)

```bash
git clone https://github.com/PauloCCBCompraFacil/comprafacil-guardian-angel.git
cd comprafacil-guardian-angel
./install.sh
```

### Windows (Git Bash, PowerShell, cmd.exe)

```bash
git clone https://github.com/PauloCCBCompraFacil/comprafacil-guardian-angel.git
cd comprafacil-guardian-angel
bash install.sh
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

On Windows, el instalador también crea `~/bin/gga.bat` para que `gga` pueda invocarse desde `cmd.exe` y PowerShell. Añade `%USERPROFILE%\bin` al `PATH` de tu usuario de Windows para esas shells; `.bashrc` solo afecta a Git Bash.

> **WSL** también está completamente soportado — no requiere configuración especial.

### Usuarios de Oh My Zsh

Si usas [Oh My Zsh](https://ohmyz.sh/) con el plugin `git` habilitado (el valor por defecto), el alias `gga` entrará en conflicto con este CLI. Verás:

```
git: 'gui' is not a git command. See 'git --help'.
```

**Solución:** Añade esta línea a tu `~/.zshrc` después de la línea `source` de Oh My Zsh:

```bash
unalias gga 2>/dev/null
```

Después ejecuta `source ~/.zshrc` o abre una nueva terminal.

---

## 🚀 Inicio Rápido

```bash
cd ~/your-project
gga init                # Crea el archivo .gga de config
gga install             # Instala el git hook
# Edita .gga para definir tu PROVIDER
# Crea AGENTS.md con tus estándares de código
# Listo — cada commit se revisará 🎉
```

---

## 🔌 Proveedores

| Proveedor | Valor de config | Instalación |
|----------|-------------|-------------|
| **Claude** | `claude` | [claude.ai/code](https://claude.ai/code) |
| **Gemini** | `gemini` | [gemini-cli](https://github.com/google-gemini/gemini-cli) |
| **Codex** | `codex` | `npm i -g @openai/codex` |
| **OpenCode** | `opencode` | [opencode.ai](https://opencode.ai) |
| **Cursor Agent** | `cursor[:model]` | [cursor.com](https://cursor.com) |
| **Kilo** | `kilo[:model]` | `npm install -g @kilocode/cli` |
| **Kiro** | `kiro` | [kiro.dev/downloads](https://kiro.dev/downloads/) |
| **Ollama** | `ollama:<model>` | [ollama.ai](https://ollama.ai) |
| **LM Studio** | `lmstudio[:model]` | [lmstudio.ai](https://lmstudio.ai) |
| **GitHub Models** | `github:<model>` | [marketplace/models](https://github.com/marketplace/models) |
| **MiniMax** | `minimax[:model]` | [platform.minimax.io](https://platform.minimax.io) |

> 📖 Consulta [docs/providers.md](docs/providers.md) para ver ejemplos detallados y configuración.

---

## 📋 Comandos

| Comando | Descripción |
|---------|------------|
| `gga init` | Crea un archivo `.gga` de configuración de muestra |
| `gga install` | Instala el hook pre-commit |
| `gga install --commit-msg` | Instala el hook commit-msg |
| `gga uninstall` | Elimina los hooks instalados |
| `gga run` | Revisa los archivos staged |
| `gga run --ci` | Revisa el último commit (CI/CD) |
| `gga run --pr-mode` | Revisa los cambios completos del PR |
| `gga run --no-cache` | Revisa ignorando la caché |
| `gga config` | Muestra la configuración actual |
| `gga cache status` | Muestra información de la caché |
| `gga version` | Muestra la versión |

> 📖 Consulta [docs/commands.md](docs/commands.md) para ver el uso detallado.

---

## 📚 Documentación

| Tema | Descripción |
|-------|------------|
| [Configuration](docs/configuration.md) | Archivo de config `.gga`, opciones, jerarquía y overrides por variables de entorno |
| [Rules File](docs/rules-file.md) | Cómo escribir un `AGENTS.md` efectivo, buenas prácticas y enfoque basado en skills |
| [Providers](docs/providers.md) | Configuración detallada de cada proveedor de IA |
| [Commands](docs/commands.md) | Referencia completa de comandos con ejemplos |
| [Caching](docs/caching.md) | Cómo funciona la caché inteligente, invalidación y comandos asociados |
| [Integrations](docs/integrations.md) | Husky, pre-commit, Lefthook, VS Code, CI/CD |
| [Examples](docs/examples.md) | Walkthrough real y configs de proyecto |
| [Troubleshooting](docs/troubleshooting.md) | Problemas comunes y soluciones |
| [Changelog](docs/changelog.md) | Historial de versiones |
| [Contributing](CONTRIBUTING.md) | Cómo contribuir (flujo issue-first) |

---

