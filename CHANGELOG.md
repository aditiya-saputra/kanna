# Changelog

Semua perubahan penting pada proyek ini dicatat di file ini.

Format mengikuti [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
dan proyek ini menggunakan [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.2.1] - 2026-10-19

### Added

- **Definisi pekerjaan non-trivial** di §3.1, sehingga cakupan Backup, Design, Bug Hunt, dan Docs Sync tidak lagi ambigu.
- **Precedence & Stop Conditions** di §3.5: keamanan mengalahkan permintaan user; diam bukan persetujuan.
- **Destructive Command Guard** di §6.4 untuk `rm -rf`, `git reset --hard`, `git clean -fd`, force push, `DROP TABLE`, dan migrasi destruktif.
- **Kontrak output sub-agent** di §8.5.5: tugas, file, perubahan, verifikasi, sisa pekerjaan, dan risiko.
- **Definition of Done** di §21 sebagai kriteria selesai yang eksplisit.
- Pemeriksaan konsistensi nomor versi di §15.3.
- Catatan bahwa `grep` pada §12.7.4 hanya menandai kandidat; silent catch dan body kosong wajib diverifikasi manual.

### Changed

- **Tabel model routing dikoreksi** setelah verifikasi dokumentasi resmi: Codex CLI/IDE dan Cursor mendukung model per sub-agent; path OpenCode adalah `.opencode/agents/` (plural), bukan `.opencode/agent/`.
- **Zero Placeholder Rule diperjelas**: placeholder string hanya boleh di `.env.example`, `config.example`, dokumentasi, atau test fixture; dilarang di kode produksi.
- **Stub berlabel** sekarang wajib menyertakan persetujuan user, alasan, target, dan catatan debt.
- **Perintah Placeholder Check** diganti agar aman untuk path berspasi, perubahan staged, file untracked, dan file yang sudah dihapus.
- **Line Count Protocol** memakai `git diff HEAD --numstat` agar perubahan staged ikut terukur; wajib untuk klasifikasi zona sub-agent, bukan untuk semua perubahan dokumentasi.
- **Bug Hunt** dibatasi pada perubahan non-trivial; perubahan satu baris boleh diringkas tetapi tetap melalui Placeholder Check.
- **Status Bug Hunt** dipisahkan dari status pekerjaan: “bug hunt selesai” bukan “pekerjaan selesai”.
- **Docs Sync** sekarang mencatat perubahan versi.

### Fixed

- Menghapus backtick nyasar pada bank kaomoji malu-malu.
- Menambahkan `build` dan `coverage` ke pengecualian arsip backup.
- Memperbaiki hitungan baris file kosong di PowerShell dengan `@(Get-Content file).Count`.
- Menghapus ambiguitas “sama” pada tabel perintah terlarang §5.4.
- Merapikan penomoran dan referensi silang antar-gerbang.

## [2.2.0] - 2026-10-19

### Added

- **Line Count Protocol** (§8.5.0) — wajib mengukur atau menandai estimasi sebelum mengklasifikasi zona pekerjaan, dengan perintah Unix dan Windows.
- **Sub-Agent Spawn Gate** (§8.5) — deteksi dukungan model routing, tiga zona (🟢/🟡/🔴), format permintaan izin, aturan pembagian kerja, dan protokol merge.
- **Zero Placeholder Rule** (§12.7) — larangan penanda pemotongan, TODO tanpa rencana, stub diam-diam, fungsi kosong, silent catch, dan placeholder string di produksi.
- Lisensi MIT (`LICENSE`) dengan copyright 2026 aditiya-saputra.
- Panduan instalasi multi-agent di README: Claude Code, OpenAI Codex, Cursor, GitHub Copilot, Gemini CLI, OpenCode, serta pola fallback untuk IDE/agent berbasis file instruksi.
- Tabel ringkasan lokasi skill global/project dan cara invokasi per agent.
- Bagian prasyarat, update, kompatibilitas, dan referensi dokumentasi resmi dengan tanggal akses.

### Changed

- Frontmatter `name` diubah dari `Kanna` menjadi `kanna` agar memenuhi validasi Cursor, Copilot, dan Codex (lowercase dan sama dengan nama folder).
- README diperluas dari dokumentasi dasar menjadi panduan instalasi dan pemakaian lintas agent.
- Ringkasan cepat (§19) diperbarui dengan gerbang line count, sub-agent, placeholder check, dan larangan perintah destruktif.

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
