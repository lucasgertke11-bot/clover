# Clover Bootloader

Clover é um bootloader UEFI focado em compatibilidade com macOS e Linux.

## Suporte

| Recurso | Suportado |
|---------|-----------|
| UEFI | ✅ Sim |
| BIOS | ✅ Sim (através de legacy) |
| Secure Boot | ⚠️ Parcial |
| macOS | ✅ Sim |

## Status: ✅ Binários Incluídos

Binários EFI versão 5172 incluídos para todas as distribuições:
- Ubuntu ✅
- Debian ✅
- Fedora ✅
- Arch Linux ✅
- Gentoo ✅

## Estrutura de Arquivos

```
/EFI/CLOVER/
└── BOOTX64.efi       # Bootloader principal UEFI 64-bit
```

## Instalação

### UEFI

```bash
# Copiar para EFI
sudo mkdir -p /boot/efi/EFI/CLOVER
sudo cp BOOTX64.efi /boot/efi/EFI/CLOVER/

# Configurar boot
sudo efibootmgr -c -d /dev/sda -p 1 -L "Clover" -l "\\EFI\\CLOVER\\BOOTX64.efi"
```

## Instalação por Distribuição

### Ubuntu/Debian
```bash
sudo cp -r ubuntu/EFI/CLOVER /boot/efi/EFI/
```

### Fedora
```bash
sudo cp -r fedora/EFI/CLOVER /boot/efi/EFI/
```

### Arch Linux
```bash
sudo cp -r arch/EFI/CLOVER /boot/EFI/
```

### Gentoo
```bash
sudo cp -r gentoo/EFI/CLOVER /boot/efi/EFI/
```

## Configuração

O arquivo `config.plist` controla todas as opções de boot.

### Exemplo de Entrada Linux

```xml
<key>KernelAndKextPatches</key>
<dict>
    <key>KernelCpu</key>
    <string>AppleCPU</string>
</dict>
```

## Vantagens

- Excelente compatibilidade com hardware Apple
- Suporte a DSDT patches
- Muitos drivers incluídos
- Temas visuais ricos

## Desvantagens

- Processo de compilação complexo
- Maior que outros bootloaders

---

**Versão**: 5172  
**Código Fonte**: https://github.com/CloverHackyColor/CloverBootloader  
**Licença**: BSD-2-Clause  
**Website**: https://cloverbootloader.github.io/
