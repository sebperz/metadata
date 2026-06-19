# Servidor web local + navegador como interfaz de escritorio

El proyecto requiere una aplicación GUI que funcione en Windows, macOS y Linux, con instalación cero para el usuario final (descargar un ejecutable, doble clic, funciona). Inicialmente consideramos Tauri, pero se descartó por dependencias de compilación (webkit2gtk-devel). Elegimos un servidor HTTP local (axum) que abre el navegador automáticamente.

## Considered options

**Tauri**: binario de 3-8 MB, UI web moderna con drag & drop nativo. Descartado porque requiere webkit2gtk-devel y otras dependencias de sistema para compilar, lo que complica el desarrollo y los builds cross-platform en CI.

**Electron**: maduro, ecosistema enorme. Descartado por el tamaño del binario (80+ MB) y consumo de RAM, inaceptables para una herramienta simple de metadata.

**Python + PyInstaller**: librerías PDF excelentes (pikepdf, pypdf), desarrollo rápido. Descartado por binarios de 40-80 MB y UI menos pulida.

**Servidor local + navegador**: binario Rust (~10 MB) con axum como servidor HTTP, frontend HTML/CSS/JS vanilla embebido, abre el navegador con `webbrowser` crate. Sin dependencias de sistema más allá de Rust. El usuario ve la misma experiencia que una app de escritorio pero en una pestaña del navegador.
