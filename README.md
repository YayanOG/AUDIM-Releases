<div align="center">

<img src="assets/logo.png" alt="AUDIM Logo" width="136" />

# AUDIM

### Reproductor Hi-Res Nativo para Android y Windows · Motor `FOLD v1.4.2`

<p>
  <img src="https://img.shields.io/badge/Versi%C3%B3n-v1.2.2-00E676?style=for-the-badge" alt="AUDIM v1.2.2" />
  <img src="https://img.shields.io/badge/Motor%20FOLD-v1.4.2-00E5FF?style=for-the-badge" alt="Motor FOLD v1.4.2" />
  <img src="https://img.shields.io/badge/Android-ARM64%20NEON-18191C?style=for-the-badge&logo=android&logoColor=00E676" alt="Android ARM64 NEON" />
  <img src="https://img.shields.io/badge/Windows-x64%20WASAPI%20Exclusive-18191C?style=for-the-badge&logo=windows&logoColor=00E5FF" alt="Windows x64 WASAPI Exclusive" />
  <img src="https://img.shields.io/badge/Licencia-Propietaria-FF1744?style=for-the-badge" alt="Licencia Propietaria" />
</p>

> **Copyright © 2026 YayanOG. Todos los derechos reservados (*All Rights Reserved*).**  
> Este repositorio aloja exclusivamente **lanzamientos oficiales binarios** para descarga y uso personal conforme a [`LICENSE`](LICENSE).

</div>

---

## ¿Qué es AUDIM?

**AUDIM** es un reproductor de audio de alta resolución (*Hi-Res*) diseñado desde cero con estética **Hi-Res OLED**, aceleración gráfica fluida y un motor de procesamiento digital de señal (**DSP**) nativo en **C++17** compartido entre **Android** (smartphones y DAPs sin dependencia de Google Play Services) y **Windows x64**.

### Características Audiófilas Principales

- **Motor Nativo C++17 (ARM NEON en Android / AVX2 & FMA en Windows x64):**
  - Reproducción nativa de formatos sin pérdida y alta resolución: **FLAC, WAV/RF64, AIFF, ALAC (`.m4a`), DSD (`.dsf`, y `.dff` en Android), MP3, AAC, OGG y Opus**, junto con soporte preparado para el ecosistema **FOLD** y soporte experimental en desarrollo para **`.flex`**.
  - **ARM64 NEON** en Android (decodificación en tiempo real directa desde archivo sin archivos temporales) y **WASAPI Exclusivo (Bit-Perfect)** / **WASAPI Compartido de baja latencia** en Windows x64.
- **Ecualizador & Preamplificador de Precisión (`Float64`):**
  - **Ecualizador Gráfico de 10 bandas** (`31 Hz – 16 kHz`, `±15.0 dB`) y **Ecualizador Paramétrico** (`hasta 32 bandas`, filtros *Peaking*, *Low/High Shelf*, *Low/High/Band Pass*, canales `L+R` / `L` / `R` y factor `Q` configurable).
  - **Preamplificador DSP ampliado de `-24.0 dB` a `+24.0 dB`** (pasos de `0.5 dB`) con **Panorama de Espectro en Vivo**: la onda y sus barras permanecen centradas en su eje horizontal y escalan su amplitud de forma proporcional a la ganancia, con indicador visual de saturación/clipping.
  - Controles dedicados de **Tono** (*Graves `90 Hz`* / *Agudos `10 kHz`*), **Expansión Estéreo M/S coherente en fase**, **Balance**, **Mono**, **Tempo (`0.50x–3.00x`)**, **Reverberación estéreo**, **Limitador suave**, **Remuestreador SW/SoX** y **12 algoritmos de Dither / Noise Shaping**.
- **Transparencia Bit-Perfect y Reconstrucción IA Opcional (Android):**
  - En modo **Bit-Perfect** o con audio *lossless* / **FOLD** / **Hi-Res (`>48 kHz` o `≥24-bit`)**, la cadena se mantiene `100 %` libre de síntesis artificial.
  - Para pistas comprimidas con pérdida (`MP3`, `AAC`, `OGG`, `Opus`), incluye un módulo **opcional** (apagado por defecto) de reconstrucción espectral de altas frecuencias (`>14 kHz`) con espectrograma comparativo HD en GPU.
- **Interfaz OLED, Biblioteca y Visualización GPU:**
  - Fondos ambientales dinámicos sincronizados con la carátula, barra continua **WaveSeekbar** centrada bajo Play/Pausa, 17+ categorías de biblioteca con orden inteligente por número de disco/pista en **Álbumes**, letras sincronizadas (`.lrc`) y visualizadores reactivos en GPU.

---

## Tecnologías del Ecosistema: FOLD y Flex (`.flex`)

### ¿Qué es FOLD?
**FOLD** es nuestra tecnología propia de audio sin pérdidas y alta resolución, diseñada con un enfoque en la eficiencia de almacenamiento y la máxima fidelidad sonora.

> **Estado actual:** El codificador y decodificador (*encoder/decoder*) independiente de **FOLD** aún no ha sido liberado al público. Sin embargo, **AUDIM** ya está preparado de forma nativa para su ecosistema, con planes futuros de expandir el soporte hacia frecuencias ultra altas de **352.8 kHz, 384 kHz, 705.6 kHz y 706.8 kHz**.

### ¿Qué es Flex (`.flex`)? *(Experimental / En desarrollo)*
**Flex (`.flex`)** es un concepto experimental de formato de audio perceptual enfocado en lograr una alta eficiencia de compresión manteniendo una experiencia auditiva limpia.

> **Estado actual:** Actualmente **Flex (`.flex`)** es una idea en fase experimental / de desarrollo y **todavía no funciona por completo dentro de la aplicación**.

---

## Instalación Rápida (`v1.2.2`)

Visita la pestaña **[Releases](https://github.com/YayanOG/AUDIM-Releases/releases/latest)** y descarga el paquete correspondiente a tu plataforma:

### Android (`AUDIM-v1.2.2.apk`)
1. Descarga **`AUDIM-v1.2.2.apk`** en tu teléfono o DAP Android (`arm64-v8a`, Android 64-bit).
2. Ábrelo desde el gestor de archivos del dispositivo y autoriza la instalación de aplicaciones de origen conocido si el sistema lo solicita.
3. Concede permiso de lectura de almacenamiento de audio y selecciona tus carpetas de música en **Biblioteca → Carpetas**.

### Windows x64 (`AUDIM-v1.2.2-Windows-x64-Setup.exe` / `.msi`)
1. Descarga **`AUDIM-v1.2.2-Windows-x64-Setup.exe`** (instalador recomendado) o **`AUDIM-v1.2.2-Windows-x64.msi`**.
2. Ejecuta el instalador y sigue el asistente en pantalla.
3. Abre **AUDIM**, agrega tus carpetas de música y elige **WASAPI Exclusivo** en **Ajustes → Audio → Salida** para reproducción bit-exacta hacia tu DAC.

---

## Donaciones / Apoya el Proyecto

Si **AUDIM** te resulta útil y quieres apoyar el desarrollo continuo, la optimización audiófila y nuevas funciones en Android y Windows, puedes contribuir mediante criptomonedas:

| Criptomoneda | Red | Dirección |
| :--- | :--- | :--- |
| **Bitcoin (BTC)** | Bitcoin | `bc1qvczqecmg2mp004nhu7ama06l8sjfgh5rxckqwf` |
| **Ethereum (ETH)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |
| **Tether (USDT)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |
| **USD Coin (USDC)** | ERC-20 | `0x516D53F67b52e2496BBE3fAAE27cc35CE67987E0` |

---

## Licencia y Derechos de Autor

**AUDIM** es software propietario. El uso de los binarios oficiales está autorizado exclusivamente para **uso personal no comercial**.  
Queda prohibida la ingeniería inversa, descompilación, desensamblado, evasión de protecciones, redistribución no autorizada o uso comercial. Consulta los términos completos en [`LICENSE`](LICENSE).

---

<div align="center">

**AUDIM** · *Hi-Res Audio Player for Android & Windows*  
*Native C++17 Engine (`FOLD v1.4.2`) · Copyright © 2026 YayanOG*

</div>
