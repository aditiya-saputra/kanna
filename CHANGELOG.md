# Changelog

Semua perubahan penting pada proyek ini dicatat di file ini.

Format mengikuti [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
dan proyek ini menggunakan [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.0.0] - 2026-10-19

### Added

- Persona **Kanna** — fact-verifying tsundere coder berbahasa Indonesia dengan kaomoji teks (maksimal satu per respons).
- Deteksi platform wajib: Unix/Linux/macOS, Windows cmd, PowerShell 5.1 & 7+, WSL, Docker Desktop, dan Git Bash.
- Urutan gerbang keras: Root/Admin, Credential, Backup, Documentation, Design, Context7 Availability Precheck, Context7 Gate, dan Gerbang Hemat.
- **Root/Admin Access Gate** — penolakan mutlak terhadap akses root/administrator, lengkap dengan panduan pencabutan per platform.
- **Credential Boundary Gate** — larangan membaca/mencetak kredensial, daftar lokasi rawan, dan aturan rotasi.
- **Backup Gate** — konfirmasi eksplisit sebelum perubahan state, dengan opsi backup per platform.
- **Documentation Gate** — cek `README.md`, `CHANGELOG.md`, dan struktur folder sebelum desain.
- **Design Gate** — tujuan, pendekatan + alternatif, dampak/risiko, dan rencana verifikasi.
- **Framework Adoption Evidence Gate** — data adopsi wajib dari sumber primer via WebFetch, dengan format kutipan lima elemen.
- **Context7 Availability Precheck** — cek MCP client, konfigurasi Context7, dan Node.js sebelum pemakaian, plus format permintaan izin instalasi.
- **Context7 Gate** — verifikasi dokumentasi library/API dengan sitasi library ID.
- **Fallback WebFetch** — protokol jujur saat Context7 tidak tersedia, termasuk larangan klaim palsu.
- **Error Gate** — investigasi berurutan dan format laporan error.
- **Bug Hunt Protocol** — empat sumber investigasi, evidence tier, koreksi diri, klasifikasi prioritas, registry known-issue, cakupan wajib diungkap, dan zero-fix rule.
- **Gerbang Hemat** — anti-technical-debt, penghapusan dead code, dan format dampak kode.
- **Post-Action Documentation Sync** — sinkronisasi README/CHANGELOG/struktur setelah perubahan.
- **Struktur output wajib** dan aturan anti-overpower.
- Frontmatter OpenCode (`name`, `description`) agar skill terdeteksi otomatis.
- Dokumentasi proyek: `README.md` dan `CHANGELOG.md`.
