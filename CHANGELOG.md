# Changelog

Semua perubahan penting pada proyek ini dicatat di file ini.

Format mengikuti [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
dan proyek ini menggunakan [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [2.5.0] - 2026-10-19

### Added

- **Program Identity Gate** (§4A) — deteksi program AI agent lewat parent PID chain (maksimal 5 level), env var nama saja, config marker, versi, lalu tanya user. Cache per sesi; invalidasi saat program/versi berubah.
- **Compatibility Registry Lookup** (§4A.7) — verifikasi kapabilitas program (sub-agent foreground/background, background shell, model routing, MCP) ke dokumentasi resmi, dengan format status + kutipan/ringkas + URL + tanggal akses.
- **Background Shell Protocol** (§13A) — log path, PID, timeout, kill switch, maksimal 3 task per gelombang, monitoring, cleanup 0 orphan, dan fallback foreground yang jujur.
- **Batas privasi deteksi program** — hanya agent + parent chain; command line di-redact; dilarang dump environ penuh atau membaca isi config.
- **Gate order baru** — Program Identity (0A) setelah Root/Admin, sebelum Credential; Background Shell sebagai modifier di fase aksi.
- **DoD baru** — Program Identity, Compatibility Lookup, dan Background Cleanup masuk kriteria selesai.
- README: fitur Program Identity, Compatibility Registry, dan Background Shell; referensi docs resmi per program.

### Changed

- **Capability matrix §4A.5 sekarang eksplisit sebagai hipotesis**; §4A.7.4 menjadi titik awal terverifikasi per 2026-10-19. Status `❓` berarti “tidak ditemukan di docs”, bukan bukti fitur tidak ada.
- **§8.5.1 membaca capability dari §4A.7**, bukan dari tabel hipotesis. Jika sub-agent foreground `❌/❓`, spawn tidak boleh dijanjikan.
- **§9.2 membaca MCP client dari §4A.7**, bukan asumsi per program.
- **Struktur output §17** mencakup Program/Compatibility, Background Shell Status, dan Background Cleanup.
- **Cheat sheet §19 dan catatan implementasi §20** diperbarui dengan matriks, sumber docs, dan referensi background shell.
- **Matriks Aider** — MCP ditandai `❓` karena tidak ditemukan MCP native di docs, bukan `❌`.
- **Windsurf/Devin Desktop** — “Simultaneous Cascades” dibedakan dari subagent dispatch; model routing per sub-agent tidak diklaim.

### Fixed

- **Cursor** — klaim “background shell ✅ (built-in Bash subagent)” dihapus. Docs Cursor hanya mendokumentasikan subagent Explore dan Browser; background shell tetap `❓`.
- **Windsurf** — klaim sub-agent background `❌` dan kutipan “no documented user-facing background sub-agent dispatch” dihapus karena bukan kutipan resmi; status menjadi `❓`.
- **OpenCode** — sub-agent background `✅` sesuai docs V2 (child session foreground/background); background shell `✅` sesuai docs tool shell (parameter `background`).
- **Codex** — model routing `✅` (custom agent TOML), background shell `❓`; background subagent dibedakan dari proses detached.
- **Claude Code** — background shell `✅` (`run_in_background: true`), dengan catatan batas 30 menit default / 2 jam maksimum.
- **Deteksi env portabel** — mengganti `${!v}` (bash-only) dengan `printenv "$v"` yang bekerja di bash/zsh; value tetap tidak dicetak.
- **macOS** — menambahkan fallback `ps -p ... -o comm=,ppid=` karena `/proc` tidak tersedia.
- **Background capability test** — tes `sleep` dihapus sebagai bukti; capability wajib dari docs/schema tool, jika tidak jelas → foreground.
- **Konsistensi routing Windsurf** — tabel §8.5.1 disamakan dengan §4A.7.4 (`❌`, bukan `⚠️`).
- **Semua perbaikan v2.2.1 dipertahankan** — Destructive Command Guard, definisi non-trivial, kontrak output sub-agent, placeholder check yang aman untuk staged/untracked, dan Definition of Done.

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
