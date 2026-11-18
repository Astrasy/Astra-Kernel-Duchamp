# ⚡ Astra Kernel — Android 14 GKI 6.1 LTS (`duchamp` / Dimensity 8300-Ultra)

Kernel customizado de nível de engenharia compilado sobre a árvore oficial **Google AOSP `common-android14-6.1-lts`** com `Clang AOSP + ThinLTO`, projetado sob medida para o **Xiaomi Redmi K70E / POCO X6 Pro 5G (`duchamp` / MediaTek `MT6897`)**.

## Arquitetura & Melhorias Técnicas

- **Identidade:** `6.1.x-Astra` (`CONFIG_LOCALVERSION="-Astra"`)
- **Compatibilidade KMI Total (`android14-11`):** 100% compatível com todos os ~150 módulos `.ko` da MediaTek em `/vendor_dlkm` e `vendor_boot` (`HZ=250`, `NO_HZ_IDLE`, `PREEMPT`, `UCLAMP`).
- **Memória `MGLRU` Íntegra (`CONFIG_LRU_GEN_ENABLED=y`):** Utiliza a implementação oficial do Google no Linux 6.1 (sem o backport defeituoso em `mm/readahead.c` que causava *NULL pointer dereference* em `f2fs_file_fadvise` / `madvise`).
- **Rede de Baixa Latência & Economia de Rádio (`TCP BBR` + `FQ`):** Algoritmo `bbr` da Google compilado nativamente como padrão (`CONFIG_DEFAULT_TCP_CONG="bbr"`), reduzindo retransmissões de pacotes em Wi-Fi/5G e aquecimento do modem.
- **Root & Stealth (`ReSukiSU` + `SUSFS v2.0.0`):** Suporte nativo a `MULTI_MANAGER`, `SUS_PATH`, `SUS_MOUNT`, `OPEN_REDIRECT`, `SUS_MAP` e proteção Unicode VFS.
- **Empacotamento Duplo:**
  - `Astra-6.1.x-duchamp-boot-lz4.img` (`header_version 4`, `Image.lz4` frame `02214c18`, `64 MB` com footer AVB SHA256_RSA2048).
  - `Astra-6.1.x-duchamp-AnyKernel3.zip` (instalador universal GKI 2.0).
