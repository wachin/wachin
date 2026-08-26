# Guía Completa: Paquetes para que un Agente IA Trabaje en Linux (Debian 13)

> Guía definitiva para preparar un entorno Linux donde un agente de código pueda investigar, analizar, compilar y documentar proyectos de software.

---

## 1. Actualiza los índices

```bash
sudo apt update
```

---

## 2. Herramientas Principales del Sistema

Estas son las herramientas base que todo agente necesita:

```bash
sudo apt install -y \
  git \
  git-lfs \
  gh \
  python3 \
  python3-pip \
  python3-venv \
  python3-dev \
  build-essential \
  curl \
  wget \
  less
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `git` | `git` | Control de versiones, esencial para trabajar con repositorios |
| `git-lfs` | `git lfs` | Git Large File Storage, para repositorios con archivos grandes |
| `gh` | `gh` | GitHub CLI, para interactuar con GitHub directamente desde terminal |
| `python3` | `python3` | Intérprete de Python, base para muchas herramientas |
| `python3-pip` | `pip3` | Gestor de paquetes Python |
| `python3-venv` | `python3 -m venv` | Entornos virtuales de Python |
| `python3-dev` | - | Archivos de desarrollo de Python (headers) |
| `build-essential` | `gcc`, `make`, etc. | Compiladores y herramientas de build esenciales |
| `curl` | `curl` | Cliente HTTP para APIs y descargas |
| `wget` | `wget` | Descarga de archivos |
| `less` | `less` | Visualizador de archivos |

---

## 3. Búsqueda y Análisis de Código

Herramientas para que el agente pueda buscar, analizar y entender código rápidamente:

```bash
sudo apt install -y \
  ripgrep \
  fd-find \
  jq \
  tree \
  bat \
  silversearcher-ag \
  ctags \
  universal-ctags
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `ripgrep` | `rg` | Búsqueda recursiva ultra-rápida, respeta `.gitignore` |
| `fd-find` | `fdfind` | Búsqueda de archivos por nombre (más rápido que `find`) |
| `jq` | `jq` | Procesador de JSON en línea de comandos |
| `tree` | `tree` | Visualización de estructura de directorios |
| `bat` | `bat` | `cat` mejorado con resaltado de sintaxis |
| `silversearcher-ag` | `ag` | Búsqueda rápida de código fuente |
| `ctags` / `universal-ctags` | `ctags` | Generación de índices de código |

### Configurar `fd` en Debian

En Debian, `fd-find` se instala como `fdfind`. Para usar `fd`:

```bash
mkdir -p ~/.local/bin
ln -sf "$(command -v fdfind)" ~/.local/bin/fd
```

---

## 4. Herramientas GNU Esenciales

El conjunto básico de herramientas Unix que todo agente debe conocer:

```bash
sudo apt install -y \
  findutils \
  coreutils \
  grep \
  sed \
  gawk \
  diffutils \
  xargs \
  parallel
```

| Paquete | Comando principal | Descripción |
|---------|-------------------|-------------|
| `findutils` | `find`, `xargs` | Búsqueda de archivos y procesamiento |
| `coreutils` | `ls`, `cp`, `mv`, `cat`, `sort`, `uniq`, `wc`, etc. | Herramientas básicas del sistema |
| `grep` | `grep` | Búsqueda de patrones en texto |
| `sed` | `sed` | Edición de texto en línea de comandos |
| `gawk` | `awk` | Procesamiento de texto y columnas |
| `diffutils` | `diff`, `comm` | Comparación de archivos |
| `parallel` | `parallel` | Ejecución paralela de comandos |

---

## 5. Compresión y Archivos

Para trabajar con cualquier formato de archivo:

```bash
sudo apt install -y \
  unzip \
  zip \
  tar \
  xz-utils \
  zstd \
  p7zip-full \
  rsync \
  file
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `unzip` / `zip` | `unzip`, `zip` | Formato ZIP |
| `tar` | `tar` | Archivos tar/gz/bz2/xz |
| `xz-utils` | `xz`, `unxz` | Compresión XZ |
| `zstd` | `zstd`, `unzstd` | Compresión Zstandard (muy rápido) |
| `p7zip-full` | `7z` | Soporte para 7z y muchos formatos |
| `rsync` | `rsync` | Sincronización eficiente de archivos |
| `file` | `file` | Identificación de tipo de archivo |

---

## 6. Herramientas de Inspección de Ejecutables

Para analizar binarios, bibliotecas y paquetes:

```bash
sudo apt install -y \
  binutils \
  elfutils \
  strace \
  ltrace \
  patchelf \
  objdump
```

| Paquete | Comandos | Descripción |
|---------|----------|-------------|
| `binutils` | `readelf`, `objdump`, `strings`, `nm`, `strip`, `ar` | Herramientas de análisis de binarios ELF |
| `elfutils` | `eu-readelf`, `eu-objdump` | Utilidades ELF alternativas |
| `strace` | `strace` | Seguimiento de llamadas al sistema |
| `ltrace` | `ltrace` | Seguimiento de llamadas a bibliotecas |
| `patchelf` | `patchelf` | Modificación de ELF (rpath, interpreter) |

### Ejemplos de uso para el agente:

```bash
# Identificar un archivo
file programa

# Analizar dependencias ELF
readelf -d programa

# Ver secciones del binario
objdump -p programa

# Extraer strings legibles
strings programa

# Ver símbolos
nm programa

# Modificar rpath
patchelf --set-rpath /mi/ruta programa
```

---

## 7. Herramientas para Paquetes Debian (.deb)

Para investigar y crear paquetes Debian:

```bash
sudo apt install -y \
  dpkg-dev \
  debhelper \
  devscripts \
  fakeroot \
  lintian \
  desktop-file-utils \
  dpkg-repack
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `dpkg-dev` | `dpkg-deb`, `dpkg-buildpackage`, `dpkg-source` | Herramientas de desarrollo de paquetes |
| `debhelper` | `dh` | Macros y helpers para empaquetado Debian |
| `devscripts` | `debuild`, `dch`, `debchange` | Scripts para mantenedores Debian |
| `fakeroot` | `fakeroot` | Simular usuario root para empaquetado |
| `lintian` | `lintian` | Verificador de calidad de paquetes .deb |
| `desktop-file-utils` | `desktop-file-validate` | Validación de archivos .desktop |
| `dpkg-repack` | `dpkg-repack` | Reconstruir un .deb desde un paquete instalado |

---

## 8. Herramientas para AppImage

Para trabajar con formato AppImage:

```bash
sudo apt install -y \
  squashfs-tools \
  squashfuse \
  fuse3 \
  fuse
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `squashfs-tools` | `unsquashfs`, `mksquashfs` | Extraer/crear sistemas de archivos squashfs |
| `squashfuse` | - | Montar squashfs sin root |
| `fuse3` / `fuse` | - | Filesystem in Userspace |

> **Nota:** No instalar `appimagetool` ni `linuxdeploy` todavía. Primero hay que investigar qué usa cada proyecto.

---

## 9. Herramientas de Red y Debugging

Para debugging de red y peticiones HTTP:

```bash
sudo apt install -y \
  net-tools \
  iproute2 \
  socat \
  ncat \
  httpie \
  tmux \
  screen
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `net-tools` | `netstat`, `ifconfig` | Herramientas de red clásicas |
| `iproute2` | `ip`, `ss` | Herramientas de red modernas |
| `socat` | `socat` | Multiplexor de sockets bidireccional |
| `ncat` | `ncat` | Cliente/servidor TCP/UDP |
| `httpie` | `http` | Cliente HTTP más amigable que curl |
| `tmux` | `tmux` | Multiplexor de terminal |
| `screen` | `screen` | Sesioness de terminal |

---

## 10. Herramientas de Texto y Documentación

Para generar y documentar:

```bash
sudo apt install -y \
  pandoc \
  texlive-base \
  groff \
  vim \
  nano \
  htop \
  btop
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `pandoc` | `pandoc` | Conversor universal de documentos |
| `texlive-base` | `pdflatex` | LaTeX para generación de PDF |
| `groff` | `groff` | Sistema de formateado de texto |
| `vim` / `nano` | `vim`, `nano` | Editores de texto |
| `htop` / `btop` | `htop`, `btop` | Monitoreo de procesos |

---

## 11. Herramientas Git Avanzadas

Para un mejor control de versiones:

```bash
sudo apt install -y \
  git \
  git-lfs \
  git-flow \
  gitk \
  tig
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `git-flow` | `git flow` | Flujo de trabajo Git (feature, release, hotfix) |
| `gitk` | `gitk` | Visualizador gráfico del historial |
| `tig` | `tig` | Visualizador del historial de git en terminal |

---

## 12. Herramientas de Análisis de Código

Para análisis estático y detección de patrones:

```bash
sudo apt install -y \
  cppcheck \
  splint \
  nmcli
```

| Paquete | Comando | Descripción |
|---------|---------|-------------|
| `cppcheck` | `cppcheck` | Análisis estático de C/C++ |
| `splint` | `splint` | Verificador estático de C |

---

## 13. Comando de Instalación Completa (Copia y Pega)

Para instalar **todas** las herramientas de una sola vez:

```bash
sudo apt update && sudo apt install -y \
  git \
  git-lfs \
  git-flow \
  gitk \
  tig \
  gh \
  python3 \
  python3-pip \
  python3-venv \
  python3-dev \
  build-essential \
  ripgrep \
  fd-find \
  jq \
  tree \
  bat \
  silversearcher-ag \
  universal-ctags \
  findutils \
  coreutils \
  grep \
  sed \
  gawk \
  diffutils \
  parallel \
  unzip \
  zip \
  tar \
  xz-utils \
  zstd \
  p7zip-full \
  rsync \
  file \
  binutils \
  elfutils \
  strace \
  ltrace \
  patchelf \
  dpkg-dev \
  debhelper \
  devscripts \
  fakeroot \
  lintian \
  desktop-file-utils \
  dpkg-repack \
  squashfs-tools \
  squashfuse \
  fuse3 \
  fuse \
  curl \
  wget \
  httpie \
  socat \
  ncat \
  net-tools \
  iproute2 \
  less \
  vim \
  nano \
  htop \
  btop \
  tmux \
  screen \
  pandoc \
  cppcheck
```

---

## 14. Configuración Post-Instalación

### Configurar `fd` en Debian

```bash
mkdir -p ~/.local/bin
ln -sf "$(command -v fdfind)" ~/.local/bin/fd
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Configurar GitHub CLI

```bash
gh auth status
# Si no has iniciado sesión:
gh auth login
```

### Configurar Git con tu correo de Proton

```bash
git config --global user.email "linuxfrontier@proton.me"
git config --global user.name "Tu Nombre"
```

### Verificar todo con un solo bloque

```bash
echo "=== Git ===" && git --version
echo "=== Git LFS ===" && git lfs version
echo "=== GitHub CLI ===" && gh --version | head -1
echo "=== Python ===" && python3 --version
echo "=== Pip ===" && pip3 --version
echo "=== Ripgrep ===" && rg --version | head -1
echo "=== fd ===" && fd --version
echo "=== jq ===" && jq --version
echo "=== Tree ===" && tree --version
echo "=== file ===" && file --version | head -1
echo "=== readelf ===" && readelf --version | head -1
echo "=== patchelf ===" && patchelf --version
echo "=== lintian ===" && lintian --version
echo "=== bat ===" && bat --version
echo "=== parallel ===" && parallel --version | head -1
echo "=== GitHub auth ===" && gh auth status 2>&1
```

---

## 15. ¿Qué NO instalar todavía?

Para un agente que investiga código, **NO** instales:

- PyQt6, PyInstaller, Nuitka (dependencias de proyectos)
- napari, Pyzo, CARA (aplicaciones específicas)
- `pip install -r requirements.txt` (dependencias de proyectos)
- appimagetool, linuxdeploy (binarios externos)

Primero investiga qué usa cada proyecto antes de instalar sus dependencias.

---

## Resumen de Categorías

| Categoría | Paquetes | Propósito |
|-----------|----------|-----------|
| **Git y GitHub** | `git`, `git-lfs`, `git-flow`, `gh`, `tig` | Control de versiones y GitHub |
| **Python** | `python3`, `pip3`, `python3-venv`, `python3-dev` | Entorno Python |
| **Búsqueda de código** | `ripgrep`, `fd-find`, `bat`, `ag` | Encontrar código rápido |
| **Compilación** | `build-essential`, `gcc`, `make`, `pkg-config` | Compilar software |
| **Análisis de binarios** | `binutils`, `elfutils`, `strace`, `patchelf` | Analizar ejecutables |
| **Paquetes Debian** | `dpkg-dev`, `debhelper`, `lintian`, `fakeroot` | Crear/verificar .deb |
| **AppImage** | `squashfs-tools`, `squashfuse`, `fuse3` | Trabajar con AppImage |
| **Compresión** | `tar`, `zip`, `7z`, `zstd`, `xz` | Cualquier formato |
| **Texto y docs** | `pandoc`, `vim`, `nano` | Editar y documentar |
| **Sistema** | `htop`, `tmux`, `curl`, `wget` | Monitoreo y red |

---

> **Nota:** Esta guía está diseñada para que un agente de código pueda trabajar de forma autónoma en Linux, investigando repositorios, analizando código, inspeccionando binarios y documentando hallazgos sin necesidad de instalar dependencias de proyectos específicos.
