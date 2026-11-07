# Paquete precompilado para Arch Linux

Este paquete contiene el módulo `8192eu.ko.zst` ya compilado con:

- clnhub `ed48fb9`
- parche MAC en `os_dep/linux/os_intfs.c`
- `CONFIG_WIFI_MONITOR = y`

## Compatibilidad

Solo funciona en:

- Arquitectura `x86_64`.
- Kernel `linux 7.0.12.arch1-1` (`uname -r` = `7.0.12-arch1-1`).

No es portable a otras versiones de kernel. Si actualizas el kernel, el paquete dejará de cargar hasta que se recompile.

## Instalación

Descarga el asset `rtl8192eu-arch-prebuilt-1.0-1-x86_64.pkg.tar.zst` desde:

```text
https://github.com/SLAYER-CODE/rtl8192eu-linux-arch/releases/latest
```

Instala:

```bash
sudo pacman -U ./rtl8192eu-arch-prebuilt-1.0-1-x86_64.pkg.tar.zst
```

Luego reinicia o recarga el módulo (esto corta la WiFi):

```bash
sudo modprobe -r 8192eu
sudo modprobe 8192eu
```

## Conflicto con DKMS

Si ya tienes el módulo DKMS instalado, existirán dos archivos `8192eu.ko.zst`:

- `/usr/lib/modules/7.0.12-arch1-1/updates/8192eu.ko.zst` (este paquete)
- `/usr/lib/modules/7.0.12-arch1-1/updates/dkms/8192eu.ko.zst` (DKMS)

Usa solo uno. Para una instalación limpia, elimina el DKMS o evita instalar ambos.

## Recompilar el paquete

Copia el módulo actual a `packaging/`, actualiza `sha256sums` en el `PKGBUILD` y ejecuta:

```bash
cd packaging
sha256sum 8192eu.ko.zst
makepkg -f
```

El paquete resultante se puede subir como asset de release.

## Alternativa recomendada a largo plazo

Para sobrevivir a actualizaciones de kernel, usa la instalación DKMS desde la fuente del repositorio en lugar de este paquete precompilado.
