# Mac Pro Hackintosh — EFI

**Intel i5-12400F + AMD RX 5500 XT** | Triple boot: macOS + Windows + Ubuntu

| Branch | EFI | Localização |
|---|---|---|
| `master` | Produção | disk0s3 interno (`/Volumes/NO NAME`) |
| `develop` | Dev/Debug | pendrive MACOS 1 (`/Volumes/MACOS 1`) |

A pasta `EFI/` é um espelho exato da partição — restore é só copiar `EFI/*` para a partição.

Documentação: `system.md` | Contexto IA: `ai-context/README.md`
