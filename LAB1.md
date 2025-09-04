# Laboratorio 1 — Creación de Unidades Booteables (Paso a paso)

**Curso:** Sistemas Digitales 3 — Universidad Santo Tomás  
**Integrantes:**  
- Miguel Angel Montaña Sánchez  
- Jeferson Jair Hernández Garzón  
- Yossed Mauricio Riaño Páez

---

## Requisitos previos
- PC con Windows (para Rufus) o Linux (para Ventoy o GParted).  
- Dos memorias USB separadas (mínimo 8 GB, recomendado 16 GB o más).  
- ISOs descargadas:  
  - `ubuntu-22.04.4-desktop-amd64.iso` (última versión estable LTS de Ubuntu al momento del laboratorio).  
  - `Win11_24H2_Spanish_Mexico_x64.iso` (última versión publicada de Windows 11).  
- Programas: **Rufus** (Windows), **Ventoy** (Windows / Linux), **GParted** (opcional).  
- Acceso a la BIOS/UEFI del equipo para configurar el arranque.  
- Carpeta del repositorio:


---

## Preparación (descarga y verificación de ISOs)
1. Descargar las imágenes desde las páginas oficiales:  
 - [Ubuntu](https://ubuntu.com/download) → versión LTS.  
 - [Windows 11](https://www.microsoft.com/software-download).  
2. Verificar la integridad de los archivos ISO (opcional):  
 - En Linux:  
   ```bash
   sha256sum ubuntu-22.04.4-desktop-amd64.iso
   ```
 - En PowerShell (Windows):  
   ```powershell
   Get-FileHash -Algorithm SHA256 .\Win11_24H2_Spanish_Mexico_x64.iso
   ```

---

## Creación de memoria booteable con Rufus (Memoria A)

### Objetivo
Crear una memoria USB booteable para instalar **Ubuntu** o **Windows** utilizando Rufus.

### Paso a paso
1. Conectar la memoria USB al equipo.  
2. Abrir **Rufus**.  
3. En **Dispositivo** seleccionar la memoria USB.  
4. En **Selección de arranque**, cargar la ISO (`Win11_24H2_Spanish_Mexico_x64.iso`).  
5. En **Esquema de partición**, se configuró **GPT**.  
6. En **Sistema de destino**, Rufus ajustó automáticamente `UEFI (no CSM)`.  
7. En **Sistema de archivos**, se eligió **NTFS**, ya que la ISO de Windows supera los 4 GB.  
8. Verificar que el estado muestre *PREPARADO*.  
9. Hacer clic en **EMPEZAR** y esperar la creación del medio booteable.  

**Detalles del proceso con Rufus:**  
- Nombre exacto del ISO usado: `Win11_24H2_Spanish_Mexico_x64.iso`  
- Esquema de partición: GPT  
- Sistema de archivos: NTFS  
- Observaciones: se eligió GPT porque el equipo utiliza firmware UEFI moderno; NTFS fue necesario por el tamaño de la ISO de Windows.  

---

## Creación de memoria multipropósito con Ventoy (Memoria B)

### Objetivo
Preparar un USB con múltiples ISOs (Ubuntu + Windows) utilizando Ventoy.

### Paso a paso
1. Descargar Ventoy desde [GitHub oficial](https://github.com/ventoy/Ventoy).  
2. Ejecutar el instalador (`Ventoy2Disk.exe`) y seleccionar la memoria USB.  
3. Presionar **Install** (primera vez) — Ventoy crea dos particiones:  
 - Una pequeña con el bootloader.  
 - Una grande para almacenar ISOs.  
4. Copiar directamente los archivos ISO:  
 - `ubuntu-22.04.4-desktop-amd64.iso`  
 - `Win11_24H2_Spanish_Mexico_x64.iso`  
5. Reiniciar el equipo y arrancar desde el USB.  
6. Ventoy mostrará un menú con todas las ISOs disponibles para seleccionar.  

**Detalles del proceso con Ventoy:**  
- Versión de Ventoy usada: 1.0.99 (última estable al momento).  
- ISOs incluidas:  
- Ubuntu 22.04.4 LTS Desktop (amd64).  
- Windows 11 24H2 Spanish (México) x64.  
- Observaciones de compatibilidad:  
- Windows 11 inició correctamente en modo UEFI.  
- Ubuntu arrancó sin problemas con Secure Boot deshabilitado.  

Además, se mantuvo un archivo `ventoy-manifest.txt` en la raíz del USB con la lista de ISOs y su fecha de copia.  

---

## Instalación de Ubuntu (particionado paso a paso)

### Preparación del disco
- Desde Windows: reducir volumen con *Administración de discos* para liberar al menos 25 GB.  
- Alternativa en Linux: usar *GParted* para redimensionar.  

### Configuración de BIOS/UEFI
1. Ingresar al BIOS con F2/F12/Supr.  
2. Configurar el USB como primer dispositivo de arranque.  
3. Seleccionar el modo UEFI.  
4. Desactivar *Secure Boot* si genera errores.  

### Instalación y particionado manual
1. Arrancar desde la memoria USB (Rufus o Ventoy).  
2. Seleccionar **Instalar Ubuntu**.  
3. En tipo de instalación elegir **Algo más (particionado manual)**.  
4. Crear las siguientes particiones:  
 - `/ (root)` → 20 GB, EXT4.  
 - `swap` → 4 GB.  
 - `/home` → resto del espacio.  
5. Instalar GRUB en `/dev/sda`.  
6. Finalizar la instalación y reiniciar el sistema.  

---

## Comprobaciones post-instalación
- Verificar sistema con:
```bash
df -h
swapon --show

