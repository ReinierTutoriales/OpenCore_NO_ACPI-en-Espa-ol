# Cambio de OpenCore oficial a OpenCore_NO_ACPI_Build

## Acerca de
**OpenCore_NO_ACPI_Build** es una bifurcación *no oficial* de OpenCore desarrollada por [**btwise**](https://gitee.com/btwise/OpenCore_NO_ACPI), no respaldada por Acidanthera (el equipo detrás de OpenCore) ni por mí. Este documento solo pretende proporcionar información al respecto. La principal (y única) diferencia con la versión oficial de OpenCore es que permite ***evitar*** la inyección de ACPI (como parches, tablas y parámetros de arranque) en sistemas operativos distintos a macOS.

Esto puede ser útil en casos donde la inyección de tablas y configuraciones ACPI cause problemas en otros sistemas operativos, como Microsoft Windows, donde SSDTs no conformes con ACPI son la causa principal de la temida "Pantalla Azul de la Muerte" (BSOD). En esencia, está dirigido a usuarios novatos (y supuestos "veteranos" de Hackintosh) que no saben cómo agregar tres líneas de código a sus SSDTs para desactivar la inyección en Windows. Si tu EFI está bien configurado, no necesitas esta bifurcación de OpenCore.

**P**: ¿Cómo funciona?  
**R**: Incluye una nueva opción (*Quirk*) en las secciones `ACPI/Quirks` y `Booter/Quirks` llamada `EnableForAll`. Si se establece en `false`, no se inyectarán parches ACPI, SSDTs ni parámetros de arranque en sistemas distintos a macOS.

## Requisitos previos
1. Una carpeta EFI funcional y un archivo `config.plist` ya configurados.
2. :warning: ¡Asegúrate de que tu versión de OpenCore y la de OpenCore_NO_ACPI_Build sean la misma! De lo contrario, podrías enfrentar errores de validación. Por ejemplo: si usas OpenCore 0.8.7, OpenCore_NO_ACPI_Build también debe ser 0.8.7.

## Instrucciones
1. :warning: ¡Haz una copia de seguridad de tu carpeta EFI actual en una unidad USB formateada en FAT32!
2. Descarga la versión correcta de [**OpenCore_NO_ACPI_Build**](https://github.com/wjz304/OpenCore_NO_ACPI_Build/releases) que coincida con tu versión de OpenCore y descomprímela.
3. Reemplaza los siguientes archivos en tu carpeta `EFI`:
   - **BootX64.efi** (en EFI/Boot)
   - **OpenCore.efi** (en EFI/OC)
   - Los **Drivers** que uses (en EFI/OC/Drivers)
   - Las **Tools** que emplees (en EFI/OC/Tools)
4. Agrega las siguientes claves a tu `config.plist`:
   - En `ACPI/Quirks`, añade: `EnableForAll` (Tipo: Boolean) y configúralo como `NO`.
   - En `Booter/Quirks`, añade: `EnableForAll` (Tipo: Boolean) y configúralo como `NO`.
5. Guarda los cambios y reinicia.

## Verificación
- Inicia Windows desde el selector de arranque de OpenCore.
- Ejecuta [**HWiNFO**](https://sourceforge.net/projects/hwinfo/).
- En la ventana principal, verifica el "Nombre de la marca del equipo". Debería mostrar una combinación del fabricante y el modelo de la placa base (o portátil). Si aparece "Acidanthera" seguido del modelo de Mac configurado en SMBIOS, algo salió mal.

> [!NOTE]
> 
> Si solo deseas evitar la inyección de SMBIOS en Windows, puedes lograrlo con la versión oficial de OpenCore. Solo necesitas ajustar estas configuraciones en tu `config.plist`:
> 
> - `Kernel/Quirks/CustomSMBIOSGuid` = `YES`
> - `PlatformInfo/SMBIOS/UpdateSMBIOSMode` = `Custom`

## Recursos
- **OpenCore_NO_ACPI** – [Última versión](https://github.com/wjz304/OpenCore_NO_ACPI_Build/releases)
