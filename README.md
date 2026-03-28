# Clover Bootloader

Clover é um bootloader UEFI focado em compatibilidade com macOS e Linux.

## Suporte

| Recurso | Suportado |
|---------|-----------|
| UEFI | ✅ Sim |
| BIOS | ✅ Sim (através de legacy) |
| Secure Boot | ⚠️ Parcial |
| macOS | ✅ Sim |

## ⚠️ Status: Precisa Ser Compilado

Os binários EFI precisam ser compilados a partir do código fonte.

### Como Compilar

#### Ubuntu/Debian

```bash
# Instalar dependências
sudo apt-get install build-essential uuid-dev iasl git nasm python3 libfuse-dev

# Clonar código fonte
git clone https://github.com/CloverHackyColor/CloverBootloader.git

# Compilar
cd CloverBootloader
./ebuild.sh -gcc151 -x64
```

#### Fedora

```bash
sudo dnf install gcc uuid-devel iasl nasm python3 fuse-devel
./ebuild.sh -gcc151 -x64
```

#### Arch Linux

```bash
sudo pacman -S gcc uuid iasl nasm python3 fuse2
./ebuild.sh -gcc151 -x64
```

## Estrutura de Arquivos (Após Compilação)

```
/EFI/CLOVER/
├── CLOVERX64.efi       # Bootloader principal
├── CLOVERIA32.efi      # Bootloader 32-bit
├── drivers64/          # Drivers UEFI 64-bit
├── drivers32/          # Drivers UEFI 32-bit
├── tools/              # Ferramentas
├── themes/             # Temas visuais
├── config.plist        # Configuração principal
└── ACPI/patched/      # DSDT patches
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

## Instalação

### UEFI

```bash
# Copiar para EFI
sudo mkdir -p /boot/efi/EFI/CLOVER
sudo cp CLOVERX64.efi /boot/efi/EFI/CLOVER/
sudo cp -r drivers64 tools themes /boot/efi/EFI/CLOVER/

# Configurar boot
sudo efibootmgr -c -d /dev/sda -p 1 -L "Clover" -l "\\EFI\\CLOVER\\CLOVERX64.efi"
```

## Vantagens

- Excelente compatibilidade com hardware Apple
- Suporte a DSDT patches
- Muitos drivers incluídos
- Temas visuais ricos

## Desvantagens

- Processo de compilação complexo
- Maior que outros bootloaders
- Desenvolvimento mais lento

---

**Código Fonte**: https://github.com/CloverHackyColor/CloverBootloader  
**Licença**: GPLv3  
**Website**: https://clover bootloader.github.io/
