# Contexto para IA — Mac Pro Hackintosh

Este repositório é o centro de verdade do projeto Hackintosh do Fagner.
Aqui estão as informações que o modelo de IA precisa para trabalhar com contexto completo.

## Estrutura do Repositório

```
/
├── BOOT/                    ← EFI boot files (produção/master)
├── OC/                      ← OpenCore config (produção/master)
│   ├── config.plist         ← Configuração principal
│   ├── Kexts/               ← Kernel extensions
│   ├── ACPI/                ← SSDT tables
│   └── Drivers/             ← UEFI drivers
├── hackintosh/
│   └── system.md            ← Hardware, versões, status atual
└── ai-context/
    └── README.md            ← Este arquivo (guia para a IA)
```

## Como Usar

- **Branch `master`** = EFI de produção (disco interno disk0s3)
- **Branch `develop`** = EFI de dev/debug (pendrive MACOS 1)
- Sempre verificar `hackintosh/system.md` para o estado atual do sistema

## Contexto Essencial

- Usuário: Fagner Gomes (fagner.egomes@gmail.com)
- Sistema: Hackintosh com OpenCore, triple boot (macOS + Windows + Ubuntu)
- macOS atual: 15.7.5 Sequoia → migrando para Tahoe 26.4.1
- EFI de produção: NÃO é o pendrive — é o disco interno (disk0s3)
- WiFi usa `itlwm.kext` + Heliport (não AirportItlwm) na produção
- GPU AMD requer `agdpmod=pikera` nos boot args sempre

## Decisões Importantes Já Tomadas

| Data | Decisão | Motivo |
|---|---|---|
| 2026-04-30 | itlwm na produção (não AirportItlwm) | Mais estável no Sequoia |
| 2026-04-30 | Triple boot configurado | Windows + macOS + Ubuntu |
| 2026-05-04 | Time Machine backup feito | Antes de atualizar para Tahoe |
| 2026-05-04 | /Users/fagner/www centralizado | Centro de verdade + git |
