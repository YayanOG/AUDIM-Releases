<div align="center">

<img src="assets/logo.png" alt="AUDIM Logo" width="136" />

**[English](#-english) | [Español](#-español)**

# AUDIM

### Native Hi-Res Audio Player for Android & Windows · `FOLD v1.4.2` Engine

<p>
  <img src="https://img.shields.io/badge/Version-v1.2.2-00E676?style=for-the-badge" alt="AUDIM v1.2.2" />
  <img src="https://img.shields.io/badge/FOLD%20Engine-v1.4.2-00E5FF?style=for-the-badge" alt="FOLD Engine v1.4.2" />
  <img src="https://img.shields.io/badge/Android-ARM64%20NEON-18191C?style=for-the-badge&logo=android&logoColor=00E676" alt="Android ARM64 NEON" />
  <img src="https://img.shields.io/badge/Windows-x64%20WASAPI%20Exclusive-18191C?style=for-the-badge&logo=windows&logoColor=00E5FF" alt="Windows x64 WASAPI Exclusive" />
  <img src="https://img.shields.io/badge/License-Proprietary-FF1744?style=for-the-badge" alt="Proprietary License" />
</p>

> **Copyright © 2026 YayanOG. All Rights Reserved.**  
> This repository hosts **official binary releases** exclusively for download and personal use in accordance with [`LICENSE`](LICENSE).

</div>

---

## 🇬🇧 English

### What is AUDIM and How Does It Work?

**AUDIM** is a high-resolution (*Hi-Res*) audio player built from the ground up with a **Hi-Res OLED** aesthetic, smooth GPU-accelerated graphics, and a **native C++17 audio & DSP engine** shared between **Android** (smartphones and DAPs with zero Google Play Services dependency) and **Windows x64**.

Its **C++17** core (`ARM64 NEON` on Android and `AVX2 / FMA` on Windows x64) reads streams directly from the file descriptor through a *lock-free* circular *ring buffer* in RAM (zero temporary files), ensuring smooth, stable playback even with **large, heavy high-resolution files**. When no effects or equalization are enabled, the signal travels through a **Bit-Perfect direct path** (including **WASAPI Exclusive** on Windows x64 and direct output on Android) with no artificial synthesis or alteration; when DSP is active, all processing operates in double-precision floating point (`Float64`).

#### True Format Compatibility

- **Lossless / Hi-Res PCM & CD Quality:**
  - Full native support for **`FLAC`** (lossless compression with bit-exact decoding to its original PCM resolution), **`WAV`** (`RIFF` / `RF64`), **`ALAC`** (`.m4a`), and **`AIFF`** (as well as **DSD** `.dsf`, and `.dff` on Android), alongside the ecosystem's proprietary **FOLD (`v1.4.2`)** and **Flex (`.flex` / `FLX1`)** formats.
  - Smooth handling of large, heavy masters in **`16 / 24 / 32-bit`** (integer and `IEEE Float`) and high sample rates.
- **Standard Lossy Formats:**
  - Native support for **`MP3`**, **`AAC`**, **`Opus`**, and **`Ogg Vorbis`**.
  - Includes an **off-by-default** **AI Reconstruction** option (`>14 kHz`) on Android, **clearly labeled as artificial / non-audiophile**, which never intervenes on lossless tracks (`FLAC`, `WAV`, `ALAC`, `AIFF`, `DSD`), **`FOLD`**, **`.flex`**, Hi-Res audio, or **Bit-Perfect** mode.

#### Key Audiophile Features

- **Native C++17 Engine (`ARM64 NEON` on Android / `AVX2 & FMA` on Windows x64):**
  - Real-time in-memory decoding of *lossless*, Hi-Res, **FOLD (`v1.4.2`)**, and **Flex (`.flex`)** formats, featuring **WASAPI Exclusive (Bit-Perfect)** and low-latency **WASAPI Shared** on Windows x64, and direct high-resolution output on Android.
- **Precision Equalizer & Preamp (`Float64`):**
  - **10-band Graphic Equalizer** (`31 Hz – 16 kHz`, `±15.0 dB`) and **Parametric Equalizer** (`up to 32 bands`, *Peaking*, *Low/High Shelf*, *Low/High/Band Pass* filters, `L+R` / `L` / `R` channels, and configurable `Q` factor).
  - **Extended DSP Preamp from `-24.0 dB` to `+24.0 dB`** (`0.5 dB` steps) with **Live Spectrum Panorama**: the waveform and its bars stay centered on their horizontal axis and scale in amplitude proportionally to gain, with a visual clipping/saturation indicator.
  - Dedicated **Tone** controls (*Bass `90 Hz`* / *Treble `10 kHz`*), **phase-coherent M/S Stereo Expansion**, **Balance**, **Mono**, **Tempo (`0.50x–3.00x`)**, **Stereo Reverb**, **Soft Limiter**, **SW/SoX Resampler**, and **12 Dither / Noise Shaping algorithms**.
- **Bit-Perfect Transparency vs. Optional Synthesis:**
  - In **Bit-Perfect** mode or when playing *lossless* audio (`FLAC`, `WAV`, `ALAC`, `AIFF`, `DSD`), **`FOLD`**, **`.flex`**, or **Hi-Res (`>48 kHz` or `≥24-bit`)** streams, the chain remains `100%` free of artificial synthesis.
  - Exclusively for lossy tracks (`MP3`, `AAC`, `Opus`, `Ogg Vorbis`), the optional **AI Reconstruction** module (disabled by default on Android and explicitly labeled as **artificial / non-audiophile**) estimates high frequencies (`>14 kHz`) with an HD comparative GPU spectrogram.
- **OLED Interface, Library & GPU Visualization:**
  - Dynamic ambient backdrops synced to cover art, continuous **WaveSeekbar** centered beneath Play/Pause, 17+ library categories with smart disc/track-number sorting in **Albums**, synchronized lyrics (`.lrc`), and GPU-reactive visualizers.

---

### Ecosystem Technologies: FOLD and Flex (`.flex`)

#### What is FOLD?
**FOLD (`v1.4.2`)** is our proprietary high-resolution audio folding and transport technology built on **linear-phase QMF subband banks (`768-tap` Kaiser)**, designed to drastically reduce storage footprint while preserving maximum sonic fidelity. **It is already running natively and stably inside AUDIM**, allowing tracks to be compressed/folded and **unfolded in real time back to their original resolution** within today's supported active rates:

- **CD Quality (`FOLD-CD` / `FOLD-CD Ultra`):** **`44.1 kHz / 16-bit`** (and `48 kHz` base carrier), restoring the encoded dynamic range over standard containers.
- **High-Resolution PCM (`FOLD1` / `FOLD2` and `FHB1 Ultra`):** native unfolding up to **`192 kHz` at `24–32 bits`** (`44.1 / 48 / 88.2 / 96 / 176.4 / 192 kHz`, supporting `16`, `24`, and `32-bit` integer / `IEEE Float`).

> **Current status and operational ceiling:** **FOLD `v1.4.2` is already operational in AUDIM** for compressing/folding and unfolding audio during playback. If an original **`WAV`** master exceeds the format's current active maximum ceiling, unfolding operates up to today's supported limit (**`192 kHz`**). Only the **standalone third-party encoding/decoding tools** (*standalone CLI / external suite*) have not yet been released to the public, and the future expansion roadmap plans to bring active unfolding up to **`352.8 kHz`, `384 kHz`, `705.6 kHz`, and `768 kHz`**, fully covering both the **`44.1 kHz`** and **`48 kHz`** clock families.

#### What is Flex (`.flex`)?
**Flex (`.flex` / `FLX1`)** is the ecosystem's hybrid perceptual and parametric format (`96–512 kbps`, with an `O(1)` instant seek table, *gapless* playback, and embedded cover art/metadata), **and it already works natively inside AUDIM**. It allows compressing a song into a much lighter file and **unfolding/decoding it in real time during playback** into high resolution (`44.1 kHz` up to **`192 kHz` / `24-bit`** via an `MDCT/PVQ` base band + `QMF` subband stages).

> **Current status and technical honesty:** **`.flex` (`FLX1`) is already functional today inside AUDIM**. Unlike an uncompressed **`WAV`** file—which stores raw PCM samples with no codec ceiling or perceptual quantization—**`.flex`** unfolding has a **format-inherent maximum resolution and fidelity ceiling** (`up to 192 kHz / 24-bit` and `96–512 kbps` perceptual bitrate), so it does not always match bit-for-bit the exact original resolution of an extreme **`WAV`** master; in return, it delivers a very high **file-size-to-sound-quality** ratio ready to use in the app.

---

### Quick Installation (`v1.2.2`)

> **Recommendation:** If you want to experience **AUDIM** at its best, we strongly recommend trying **Android `v1.2.2`** over the Windows build first—it is the most complete, polished, and feature-rich version of the player.

Visit the **[Releases](https://github.com/YayanOG/AUDIM-Releases/releases/latest)** tab and download the package for your platform:

#### Android (`AUDIM-v1.2.2.apk`) — Recommended
1. Download **`AUDIM-v1.2.2.apk`** on your Android phone or DAP (`arm64-v8a`, 64-bit Android).
2. Open it from your device's file manager and allow installation from this source if prompted by the system.
3. Grant audio storage read permission and select your music folders under **Library → Folders**.

#### Windows x64 (`AUDIM-v1.2.2-Windows-x64-Setup.exe` / `.msi`)
1. Download **`AUDIM-v1.2.2-Windows-x64-Setup.exe`** (recommended installer) or **`AUDIM-v1.2.2-Windows-x64.msi`**.
2. Run the installer and follow the on-screen wizard.
3. Open **AUDIM**, add your music folders, and select **WASAPI Exclusive** in **Settings → Audio → Output** for bit-exact playback to your DAC.

---

### Donations / Support the Project

If you find **AUDIM** useful and want to support ongoing development, audiophile optimization, and new features on Android and Windows, you can contribute via cryptocurrency:

| Cryptocurrency | Network | Address |
| :--- | :--- | :--- |
| **Bitcoin (BTC)** | Bitcoin | `bc1qvczqecmg2mp004nhu7ama06l8sjfgh5rxckqwf` |
| **Ethereum (ETH)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |
| **Tether (USDT)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |
| **USD Coin (USDC)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |

---

### License and Copyright

**AUDIM** is proprietary software. Use of the official binaries is authorized exclusively for **non-commercial personal use**.  
Reverse engineering, decompilation, disassembly, circumvention of protections, unauthorized redistribution, or commercial use is prohibited. See the full terms in [`LICENSE`](LICENSE).

---

## 🇪🇸 Español

### ¿Qué es AUDIM y Cómo Funciona?

**AUDIM** es un reproductor de audio de alta resolución (*Hi-Res*) diseñado desde cero con estética **Hi-Res OLED**, aceleración gráfica fluida en GPU y un **motor de audio y DSP nativo en C++17** compartido entre **Android** (smartphones y DAPs sin dependencia de Google Play Services) y **Windows x64**.

Su núcleo **C++17** (`ARM64 NEON` en Android y `AVX2 / FMA` en Windows x64) lee los flujos directamente desde el descriptor de archivo mediante un *ring buffer* circular *lock-free* en RAM (cero archivos temporales), garantizando una reproducción fluida y estable incluso con **archivos grandes y pesados de alta resolución**. Cuando el usuario no activa efectos ni ecualización, la señal viaja por una **ruta directa Bit-Perfect** (incluyendo **WASAPI Exclusivo** en Windows x64 y salida directa en Android) sin síntesis ni alteraciones artificiales; cuando se activa el DSP, todo el procesamiento opera en coma flotante de doble precisión (`Float64`).

#### Compatibilidad Real de Formatos

- **Sin pérdidas / PCM Hi-Res y calidad CD:**
  - Soporte nativo completo para **`FLAC`** (compresión sin pérdidas con decodificación bit-exacta a su resolución PCM original), **`WAV`** (`RIFF` / `RF64`), **`ALAC`** (`.m4a`) y **`AIFF`** (además de **DSD** `.dsf`, y `.dff` en Android), junto con los formatos propios del ecosistema **FOLD (`v1.4.2`)** y **Flex (`.flex` / `FLX1`)**.
  - Manejo fluido de másteres pesados de gran tamaño en **`16 / 24 / 32 bits`** (entero e `IEEE Float`) y altas frecuencias de muestreo.
- **Formatos con pérdida estándar:**
  - Soporte nativo para **`MP3`**, **`AAC`**, **`Opus`** y **`Ogg Vorbis`**.
  - Incluye en Android una opción **desactivada por defecto** de **Reconstrucción IA** (`>14 kHz`), **claramente marcada como artificial / no audiófila**, que jamás interviene sobre pistas sin pérdidas (`FLAC`, `WAV`, `ALAC`, `AIFF`, `DSD`), **`FOLD`**, **`.flex`**, audio Hi-Res ni modo **Bit-Perfect**.

#### Características Audiófilas Principales

- **Motor Nativo C++17 (`ARM64 NEON` en Android / `AVX2 & FMA` en Windows x64):**
  - Decodificación en tiempo real de formatos *lossless*, Hi-Res, **FOLD (`v1.4.2`)** y **Flex (`.flex`)** directamente en memoria, con **WASAPI Exclusivo (Bit-Perfect)** y **WASAPI Compartido de baja latencia** en Windows x64, y salida directa de alta resolución en Android.
- **Ecualizador & Preamplificador de Precisión (`Float64`):**
  - **Ecualizador Gráfico de 10 bandas** (`31 Hz – 16 kHz`, `±15.0 dB`) y **Ecualizador Paramétrico** (`hasta 32 bandas`, filtros *Peaking*, *Low/High Shelf*, *Low/High/Band Pass*, canales `L+R` / `L` / `R` y factor `Q` configurable).
  - **Preamplificador DSP ampliado de `-24.0 dB` a `+24.0 dB`** (pasos de `0.5 dB`) con **Panorama de Espectro en Vivo**: la onda y sus barras permanecen centradas en su eje horizontal y escalan su amplitud de forma proporcional a la ganancia, con indicador visual de saturación/clipping.
  - Controles dedicados de **Tono** (*Graves `90 Hz`* / *Agudos `10 kHz`*), **Expansión Estéreo M/S coherente en fase**, **Balance**, **Mono**, **Tempo (`0.50x–3.00x`)**, **Reverberación estéreo**, **Limitador suave**, **Remuestreador SW/SoX** y **12 algoritmos de Dither / Noise Shaping**.
- **Transparencia Bit-Perfect vs. Síntesis Opcional:**
  - En modo **Bit-Perfect** o al reproducir audio *lossless* (`FLAC`, `WAV`, `ALAC`, `AIFF`, `DSD`), **`FOLD`**, **`.flex`** o flujos **Hi-Res (`>48 kHz` o `≥24-bit`)**, la cadena se mantiene `100 %` libre de síntesis artificial.
  - Exclusivamente para pistas con pérdida (`MP3`, `AAC`, `Opus`, `Ogg Vorbis`), el módulo opcional de **Reconstrucción IA** (apagado por defecto en Android y señalizado explícitamente como **artificial / no audiófilo**) permite estimar altas frecuencias (`>14 kHz`) con espectrograma comparativo HD en GPU.
- **Interfaz OLED, Biblioteca y Visualización GPU:**
  - Fondos ambientales dinámicos sincronizados con la carátula, barra continua **WaveSeekbar** centrada bajo Play/Pausa, 17+ categorías de biblioteca con orden inteligente por número de disco/pista en **Álbumes**, letras sincronizadas (`.lrc`) y visualizadores reactivos en GPU.

---

### Tecnologías del Ecosistema: FOLD y Flex (`.flex`)

#### ¿Qué es FOLD?
**FOLD (`v1.4.2`)** es nuestra tecnología propia de plegado y transporte de audio de alta resolución mediante bancos subbanda **QMF de fase lineal (`768 taps` Kaiser)**, diseñada para reducir drásticamente el peso de almacenamiento preservando la máxima fidelidad sonora. **Actualmente ya funciona de forma nativa y estable dentro de AUDIM**, permitiendo comprimir/plegar pistas y **desplegarlas (*unfold*) en tiempo real de vuelta a su resolución original** dentro de las tasas activas soportadas hoy:

- **Calidad CD (`FOLD-CD` / `FOLD-CD Ultra`):** **`44.1 kHz / 16-bit`** (y portadora base `48 kHz`), restaurando el rango dinámico codificado sobre contenedores estándar.
- **PCM de Alta Resolución (`FOLD1` / `FOLD2` y `FHB1 Ultra`):** despliegue nativo hasta **`192 kHz` en `24–32 bits`** (`44.1 / 48 / 88.2 / 96 / 176.4 / 192 kHz`, soportando `16`, `24` y `32 bits` entero / `IEEE Float`).

> **Estado actual y techo operativo:** **FOLD `v1.4.2` ya está operativo en AUDIM** para comprimir/plegar y desplegar audio en reproducción. Si un máster original en **`WAV`** supera el tope máximo activo actual del formato, el despliegue opera hasta el techo soportado hoy (**`192 kHz`**). Únicamente las **herramientas independientes de codificación/decodificación para terceros** (*standalone CLI / suite externa*) aún no han sido liberadas al público, y el plan de expansión futura contempla llevar el despliegue activo hasta **`352.8 kHz`, `384 kHz`, `705.6 kHz` y `768 kHz`**, cubriendo por completo las familias de reloj de **`44.1 kHz`** y **`48 kHz`**.

#### ¿Qué es Flex (`.flex`)?
**Flex (`.flex` / `FLX1`)** es el formato híbrido perceptual y paramétrico del ecosistema (`96–512 kbps`, con tabla de búsqueda instantánea `O(1)`, reproducción *gapless* y carátulas/metadatos embebidos), **y ya funciona de forma nativa dentro de AUDIM**. Permite comprimir una canción en un archivo muchísimo más ligero y **desplegarla/decodificarla en tiempo real durante la reproducción** hacia alta resolución (`44.1 kHz` hasta **`192 kHz` / `24-bit`** mediante banda base `MDCT/PVQ` + etapas subbanda `QMF`).

> **Estado actual y honestidad técnica:** **`.flex` (`FLX1`) ya es funcional hoy mismo dentro de AUDIM**. A diferencia de un archivo **`WAV`** sin comprimir —que almacena las muestras PCM crudas sin limitación de códec ni cuantización perceptual—, el despliegue de **`.flex`** posee un **techo máximo de resolución y fidelidad propio del formato** (`hasta 192 kHz / 24-bit` y tasa perceptual `96–512 kbps`), por lo que no siempre iguala bit a bit la resolución original exacta de un máster **`WAV`** extremo; a cambio, ofrece una relación **peso / calidad sonora** muy alta y lista para usar en la aplicación.

---

### Instalación Rápida (`v1.2.2`)

> **Recomendación:** Si quieres probar **AUDIM** en su mejor versión, te recomendamos encarecidamente probar **Android `v1.2.2`** por encima de la versión de Windows, ya que ofrece la experiencia más completa, pulida y avanzada del reproductor.

Visita la pestaña **[Releases](https://github.com/YayanOG/AUDIM-Releases/releases/latest)** y descarga el paquete correspondiente a tu plataforma:

#### Android (`AUDIM-v1.2.2.apk`) — Recomendado
1. Descarga **`AUDIM-v1.2.2.apk`** en tu teléfono o DAP Android (`arm64-v8a`, Android 64-bit).
2. Ábrelo desde el gestor de archivos del dispositivo y autoriza la instalación de aplicaciones de origen conocido si el sistema lo solicita.
3. Concede permiso de lectura de almacenamiento de audio y selecciona tus carpetas de música en **Biblioteca → Carpetas**.

#### Windows x64 (`AUDIM-v1.2.2-Windows-x64-Setup.exe` / `.msi`)
1. Descarga **`AUDIM-v1.2.2-Windows-x64-Setup.exe`** (instalador recomendado) o **`AUDIM-v1.2.2-Windows-x64.msi`**.
2. Ejecuta el instalador y sigue el asistente en pantalla.
3. Abre **AUDIM**, agrega tus carpetas de música y elige **WASAPI Exclusivo** en **Ajustes → Audio → Salida** para reproducción bit-exacta hacia tu DAC.

---

### Donaciones / Apoya el Proyecto

Si **AUDIM** te resulta útil y quieres apoyar el desarrollo continuo, la optimización audiófila y nuevas funciones en Android y Windows, puedes contribuir mediante criptomonedas:

| Criptomoneda | Red | Dirección |
| :--- | :--- | :--- |
| **Bitcoin (BTC)** | Bitcoin | `bc1qvczqecmg2mp004nhu7ama06l8sjfgh5rxckqwf` |
| **Ethereum (ETH)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |
| **Tether (USDT)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |
| **USD Coin (USDC)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |

---

### Licencia y Derechos de Autor

**AUDIM** es software propietario. El uso de los binarios oficiales está autorizado exclusivamente para **uso personal no comercial**.  
Queda prohibida la ingeniería inversa, descompilación, desensamblado, evasión de protecciones, redistribución no autorizada o uso comercial. Consulta los términos completos en [`LICENSE`](LICENSE).

---

<div align="center">

**AUDIM** · *Hi-Res Audio Player for Android & Windows*  
*Native C++17 Engine (`FOLD v1.4.2`) · Copyright © 2026 YayanOG*

</div>
