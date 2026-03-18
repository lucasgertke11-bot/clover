# Clover Bootloader

Bootloader com suporte a BIOS e UEFI, originalmente desenvolvido parahackintosh, mas também funciona com Linux.

## Arquivos

### UEFI
| Arquivo | Uso |
|---------|-----|
| `CLOVERX64.efi` | Bootloader UEFI (copie para /EFI/CLOVER/) |
| `BOOTX64.efi` | Bootloader UEFI (copie para /EFI/BOOT/) |

### BIOS/Legacy
| Arquivo | Uso |
|---------|-----|
| `boot6` | Bootloader BIOS (para MBR - sem BiosBlockIO) |
| `boot7` | Bootloader BIOS (para MBR - com BiosBlockIO) |

---

## Instalação

### UEFI
```bash
# Copiar para partição ESP
mkdir -p /boot/EFI/CLOVER/
mkdir -p /boot/EFI/BOOT/
cp uefi/CLOVERX64.efi /boot/EFI/CLOVER/
cp uefi/BOOTX64.efi /boot/EFI/BOOT/
```

### BIOS/Legacy
```bash
# Instalar no MBR (escolha um)
dd if=bios/boot6 of=/dev/sda bs=440 count=1 conv=notrunc  # Sem BiosBlockIO
dd if=bios/boot7 of=/dev/sda bs=440 count=1 conv=notrunc  # Com BiosBlockIO (recomendado)
```

---

## Diferença entre boot6 e boot7

- **boot6**: Sem suporte a BiosBlockIO (mais compatível com VMs)
- **boot7**: Com suporte a BiosBlockIO (recomendado para hardware real)

---

## Integração com Calamares

```python
def install_clover(boot_type, target):
    if boot_type == "uefi":
        esp = target  # ex: /boot/efi
        os.makedirs(f"{esp}/EFI/CLOVER", exist_ok=True)
        os.makedirs(f"{esp}/EFI/BOOT", exist_ok=True)
        shutil.copy("uefi/CLOVERX64.efi", f"{esp}/EFI/CLOVER/")
        shutil.copy("uefi/BOOTX64.efi", f"{esp}/EFI/BOOT/")
    else:
        disk = target  # ex: /dev/sda
        with open(disk, "r+b") as f:
            with open("bios/boot7", "rb") as boot:
                f.seek(0)
                f.write(boot.read(440))
```

---

## Créditos

- Clover Bootloader: https://github.com/CloverHackyColor/CloverBootloader
