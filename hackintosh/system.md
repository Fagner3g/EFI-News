# Hackintosh — Estado do Sistema

## Hardware

| Componente | Modelo |
|---|---|
| CPU | Intel Core i5-12400F (12ª Gen, Alder Lake, 6 cores) |
| GPU | AMD Radeon RX 5500 XT 8 GB |
| RAM | 16 GB DDR4 2400 MHz |
| Ethernet | Realtek RTL8125 (2.5 GbE) |
| WiFi/BT | Intel WiFi (fw: 68.x — AC 9xxx/AX201) |
| SMBIOS | MacPro7,1 |
| Serial | F5KHDDZFP7QM |

## Software

| Item | Versão |
|---|---|
| macOS | 15.7.5 Sequoia (build 24G624, kernel 24.6.0) |
| OpenCore | EFI de Abr/2026 |
| Boot | Triple boot: macOS + Windows + Ubuntu |

## Estrutura EFI

| EFI | Localização física | Branch GitHub | Uso |
|---|---|---|---|
| Produção | disk0s3 (interno, 314 MB) | `master` | Boot diário |
| Dev/Debug | disk4s1 (pendrive MACOS 1, 30 GB) | `develop` | Testes |

### Estrutura do repositório (espelho da partição)

```
hackintosh/
├── EFI/                    ← cópia exata da partição EFI (disk0s3)
│   ├── APPLE/              ← firmware updater Apple
│   ├── BOOT/               ← bootloader genérico UEFI
│   ├── Microsoft/          ← boot entry Windows
│   ├── OC/                 ← OpenCore (macOS)
│   │   ├── ACPI/           ← SSDTs
│   │   ├── Drivers/        ← drivers UEFI
│   │   ├── Kexts/          ← kernel extensions
│   │   ├── Resources/      ← tema GoldenGate
│   │   └── config.plist    ← configuração principal
│   └── ubuntu/             ← boot entry Ubuntu
├── README.md
├── system.md               ← este arquivo
└── ai-context/
    └── README.md
```

### Restore completo

```bash
sudo diskutil mount disk0s3
cp -r /Users/fagner/www/hackintosh/EFI/* "/Volumes/NO NAME/EFI/"
```

## Kexts Instalados (Produção — branch master)

| Kext | Versão | Função |
|---|---|---|
| Lilu | 1.7.3 | Framework base |
| VirtualSMC + plugins | 1.3.8 | SMC emulation |
| AppleALC | 1.9.8 | Áudio |
| WhateverGreen | 1.7.0 | GPU patches |
| AMFIPass | 1.4.1 | AMFI bypass |
| RestrictEvents | 1.1.7 | Event patches |
| NVMeFix | 1.1.4 | NVMe compat |
| LucyRTL8125Ethernet | 1.2.3 | Ethernet 2.5G |
| itlwm | 2.3.0 | WiFi Intel |
| IntelBluetoothFirmware | 2.5.0 | Bluetooth |
| IntelBTPatcher | 2.5.0 | BT patcher |
| BlueToolFixup | 2.7.3 | BT stack fix |
| USBToolBox + UTBDefault | 1.2.0 / 1.0 | USB mapping |
| XHCI-unsupported | 0.9.2 | XHCI compat |

## Boot Args (Produção)

```
-v debug=0x100 keepsyms=1 -amfipassbeta agdpmod=pikera
```

> `agdpmod=pikera` obrigatório para AMD RX 5500 XT  
> `-amfipassbeta` necessário com AMFIPass.kext

## Status de Hardware (2026-05-04)

| Componente | Status |
|---|---|
| Áudio | ✅ Funcionando |
| Ethernet | ✅ Funcionando |
| GPU / Display | ✅ Funcionando |
| USB | ✅ Funcionando |
| Bluetooth | ✅ Funcionando |
| WiFi | ✅ Funcionando (itlwm via Heliport) |
| Sleep/Wake | ⚠️ Não testado |

## Atualização Planejada

- **De:** macOS 15.7.5 Sequoia (kernel 24.x)
- **Para:** macOS Tahoe 26.4.1 (build 25E253, kernel 25.x)
- **Tamanho:** ~17.8 GB
- **Status:** Aguardando atualização dos kexts para kernel 25.x
