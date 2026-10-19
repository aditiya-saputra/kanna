# Kanna

**Fact-Verifying Tsundere Coder** — skill agent untuk coding, refactor, bug hunt, dan verifikasi fakta lapangan.

[![Version](https://img.shields.io/badge/version-2.5.0-blue.svg)](CHANGELOG.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> "Aku bukan asisten yang bilang 'siap, kak!' ke setiap permintaan. Aku partner yang bikin kamu nggak nyesel minggu depan."

Kanna adalah persona coding agent berbahasa Indonesia yang menolak menyentuh kode sebelum gerbang keamanan dan desain terpenuhi. Dia mendeteksi program AI agent yang dipakai, memverifikasi kapabilitasnya lewat dokumentasi resmi, memverifikasi klaim sebelum dipakai, hemat baris kode, mencatat technical debt secara eksplisit, dan aktif mencari bug sebelum menyatakan pekerjaan selesai.

## Fitur

- **Gerbang berurutan yang tidak bisa dibalik** — Root/Admin, Program Identity, Credential, Backup, Documentation, Design, Context7, dan Gerbang Hemat.
- **Program Identity Gate** — mendeteksi program AI agent lewat parent PID, env var (nama saja), config marker, dan versi. Hanya agent + parent chain yang diperiksa; command line di-redact.
- **Compatibility Registry Lookup** — kapabilitas program (sub-agent, background shell, model routing, MCP) diverifikasi ke dokumentasi resmi, bukan dari ingatan. Status `❓` tidak pernah dijanjikan sebagai `✅`.
- **Verifikasi dokumentasi library** lewat Context7, dengan precheck MCP/Node.js dan fallback WebFetch yang jujur.
- **Framework Adoption Evidence** — data adopsi wajib dari sumber primer (Stack Overflow Survey, State of JS, JetBrains, dsb.), bukan dari ingatan model.
- **Error Gate** — Context7 → WebFetch → reproduksi → perbaikan → verifikasi pasca.
- **Background Shell Protocol** — log path, PID, timeout, kill switch, maksimal 3 task per gelombang, dan cleanup 0 orphan. Background shell tidak diklaim menghemat token.
- **Bug Hunt Protocol** — label bukti (✅ direproduksi, 📖 terbukti dari sumber, 🧠 penalaran, ⚠️ known issue), klasifikasi prioritas, zero-fix rule, dan reproduksi terisolasi.
- **Line Count Protocol & Sub-Agent Spawn Gate** — ukur pekerjaan dulu, klasifikasi zona, lalu baca dukungan model routing dari Compatibility Registry sebelum spawn. Spawn membeli waktu dengan token; menolak spawn menghemat token.
- **Zero Placeholder Rule** — larangan `// ...`, TODO tanpa rencana, stub diam-diam, fungsi kosong, silent catch, dan placeholder string di kode produksi.
- **Destructive Command Guard** — `rm -rf`, `git reset --hard`, `git clean -fd`, force push, dan migrasi destruktif wajib izin eksplisit.
- **Definition of Done** — kriteria selesai eksplisit; jika ada yang belum terpenuhi, statusnya debt, bukan “selesai”. Background task yang masih running berarti status belum selesai.
- **Sinkronisasi dokumentasi pasca-aksi** — README, CHANGELOG, struktur folder, dan nomor versi.
- **Persona tsundere fungsional** — sindiran selalu disertai perbaikan konkret; maksimal satu kaomoji teks per respons.
- **Cross-platform** — Unix/Linux/macOS, Windows (cmd, PowerShell 5.1 & 7+), WSL, Docker Desktop, dan Git Bash.

## Prasyarat

- Git
- Salah satu agent/IDE yang mendukung Agent Skills (`SKILL.md`), atau yang mendukung file instruksi (`AGENTS.md` / rules)
- Koneksi SSH ke GitHub jika memakai clone via SSH (opsional; HTTPS juga bisa)

## Instalasi

Kanna mengikuti standar [Agent Skills](https://agentskills.io): satu folder berisi `SKILL.md`. Karena itu, instalasinya cukup menaruh folder ini di direktori skill milik agent yang kamu pakai.

### Ringkasan lokasi

| Agent | Global (user) | Project | Invokasi |
|---|---|---|---|
| Claude Code | `~/.claude/skills/kanna/` | `.claude/skills/kanna/` | `/kanna` |
| OpenAI Codex | `~/.agents/skills/kanna/` | `.agents/skills/kanna/` | `$kanna` atau `/skills` |
| Cursor | `~/.cursor/skills/kanna/` atau `~/.agents/skills/kanna/` | `.cursor/skills/kanna/` atau `.agents/skills/kanna/` | `/kanna` |
| GitHub Copilot (VS Code/CLI) | `~/.copilot/skills/kanna/` atau `~/.agents/skills/kanna/` | `.github/skills/kanna/` | `/kanna` |
| Gemini CLI | `~/.gemini/skills/kanna/` atau `~/.agents/skills/kanna/` | `.gemini/skills/kanna/` atau `.agents/skills/kanna/` | `/skills` lalu pilih `kanna` |
| OpenCode | `~/.config/opencode/skills/kanna/` | `.opencode/skills/kanna/` | `@kanna` |

Windows: ganti `~` dengan `%USERPROFILE%`, dan `/` dengan `\` saat menulis path.

### Claude Code

Clone langsung ke direktori skill personal:

```bash
git clone git@github.com:aditiya-saputra/kanna.git ~/.claude/skills/kanna
```

Atau clone di lokasi lain lalu symlink (lebih mudah di-update):

```bash
git clone git@github.com:aditiya-saputra/kanna.git ~/src/kanna
mkdir -p ~/.claude/skills
ln -s ~/src/kanna ~/.claude/skills/kanna
```

Untuk satu proyek saja:

```bash
mkdir -p .claude/skills
git clone git@github.com:aditiya-saputra/kanna.git .claude/skills/kanna
```

Mulai sesi `claude`, lalu jalankan `/kanna` atau `/skills` untuk melihat daftar skill.

### OpenAI Codex

Codex membaca skill user dari `~/.agents/skills`:

```bash
mkdir -p ~/.agents/skills
git clone git@github.com:aditiya-saputra/kanna.git ~/.agents/skills/kanna
```

Untuk scope repo, letakkan di `.agents/skills/kanna/` dan commit agar tim ikut memakainya:

```bash
mkdir -p .agents/skills
git clone git@github.com:aditiya-saputra/kanna.git .agents/skills/kanna
```

Di Codex CLI/IDE, jalankan `/skills` untuk melihat daftar, atau panggil langsung dengan `$kanna`. Codex mendeteksi perubahan skill otomatis; restart jika belum muncul.

### Cursor

Cursor memuat skill dari `~/.cursor/skills` atau `~/.agents/skills`:

```bash
mkdir -p ~/.cursor/skills
git clone git@github.com:aditiya-saputra/kanna.git ~/.cursor/skills/kanna
```

Project-level:

```bash
mkdir -p .cursor/skills
git clone git@github.com:aditiya-saputra/kanna.git .cursor/skills/kanna
```

Buka **Customize → Skills** untuk memastikan skill terdeteksi, lalu panggil `/kanna` di Agent chat. Frontmatter `name` harus sama dengan nama folder (`kanna`), jadi jangan ganti nama foldernya.

### GitHub Copilot (VS Code, Copilot CLI, Copilot app)

Personal skill:

```bash
mkdir -p ~/.copilot/skills
git clone git@github.com:aditiya-saputra/kanna.git ~/.copilot/skills/kanna
```

Alternatif yang kompatibel lintas agent: `~/.agents/skills/kanna/`.

Project skill:

```bash
mkdir -p .github/skills
git clone git@github.com:aditiya-saputra/kanna.git .github/skills/kanna
```

Di VS Code, buka Chat lalu ketik `/skills` (mode Local) atau **Chat: Open Customizations → Skills**. Panggil dengan `/kanna`. Frontmatter `name` wajib lowercase dan sama dengan nama folder.

### Gemini CLI

Cara paling singkat, langsung dari repo:

```bash
gemini skills install https://github.com/aditiya-saputra/kanna.git --consent
gemini skills list --all
```

Atau clone manual ke direktori user:

```bash
mkdir -p ~/.gemini/skills
git clone git@github.com:aditiya-saputra/kanna.git ~/.gemini/skills/kanna
```

Di sesi Gemini CLI, jalankan `/skills list`, lalu minta task yang relevan; Gemini akan mengaktifkan `kanna` setelah konfirmasi. Untuk scope workspace, gunakan `.gemini/skills/kanna/` atau `.agents/skills/kanna/`.

### OpenCode

Global:

```bash
mkdir -p ~/.config/opencode/skills
git clone git@github.com:aditiya-saputra/kanna.git ~/.config/opencode/skills/kanna
```

Project-local:

```bash
mkdir -p .opencode/skills
git clone git@github.com:aditiya-saputra/kanna.git .opencode/skills/kanna
```

Panggil dengan `@kanna`, atau minta agent memuat skill ID `kanna`.

### IDE / agent lain

Jika agent mendukung Agent Skills, letakkan folder ini di direktori skill-nya (biasanya `~/.<agent>/skills/` atau `.agents/skills/`). Jika agent hanya mendukung file instruksi, gunakan pola pointer berikut.

Clone ke lokasi stabil:

```bash
git clone git@github.com:aditiya-saputra/kanna.git ~/src/kanna
```

Lalu tambahkan ke file instruksi agent — `AGENTS.md`, `.cursor/rules/`, `.windsurf/rules/`, `.clinerules/`, `.continue/rules/`, atau `CONVENTIONS.md` — sesuaikan dengan tool yang dipakai:

```markdown
## Kanna skill

Untuk semua task coding non-trivial, baca dan ikuti:
`~/src/kanna/SKILL.md`

Gerbang wajib: root/admin, kredensial, backup, dokumentasi, desain,
verifikasi Context7/WebFetch, lalu bug hunt sebelum menyatakan selesai.
```

Contoh agent yang umum memakai file instruksi: Windsurf, Cline, Zed, Continue, Aider, dan agent berbasis `AGENTS.md` lainnya. Selalu cek dokumentasi tool masing-masing untuk nama file dan lokasi yang tepat.

## Update

Jika di-clone langsung:

```bash
git -C ~/.claude/skills/kanna pull
```

Sesuaikan path dengan lokasi instalasimu. Jika memakai symlink ke `~/src/kanna`, cukup:

```bash
git -C ~/src/kanna pull
```

## Struktur

```text
kanna/
├── SKILL.md      # Definisi lengkap persona, gerbang, dan protokol
├── README.md     # Dokumen ini
├── CHANGELOG.md  # Riwayat perubahan
└── LICENSE       # MIT
```

## Kompatibilitas

- Format `SKILL.md` + frontmatter YAML mengikuti Agent Skills open standard.
- `name` sengaja dibuat lowercase (`kanna`) dan sama dengan nama folder agar lolos validasi Cursor, Copilot, dan Codex.
- Progressive disclosure: agent hanya membaca `name` + `description` sampai skill benar-benar dipakai.
- Perintah shell di dalam skill menyediakan varian Unix dan Windows; asumsi platform selalu disebutkan.
- Beberapa agent (mis. Cursor dan Copilot) juga membaca direktori skill milik Claude/Codex untuk kompatibilitas, jadi satu instalasi bisa dipakai bersama.
- Kanna memverifikasi kapabilitas program ke docs resmi (Claude Code, OpenCode, Cursor, Codex, Windsurf/Devin Desktop, Aider) sebelum menjanjikan sub-agent, background shell, atau model routing.

## Lisensi

Dirilis di bawah [MIT License](LICENSE).

```text
Copyright (c) 2026 aditiya-saputra
```

## Referensi

- Agent Skills standard — <https://agentskills.io> (diakses 2026-10-19)
- Claude Code skills — <https://code.claude.com/docs/en/skills> (diakses 2026-10-19)
- OpenAI Codex skills — <https://learn.chatgpt.com/docs/build-skills> (diakses 2026-10-19)
- Cursor Agent Skills — <https://cursor.com/docs/skills> (diakses 2026-10-19)
- VS Code / GitHub Copilot Agent Skills — <https://code.visualstudio.com/docs/agent-customization/agent-skills> (diakses 2026-10-19)
- Gemini CLI Agent Skills — <https://geminicli.com/docs/cli/skills/> (diakses 2026-10-19)
- Claude Code subagents — <https://code.claude.com/docs/en/sub-agents> (diakses 2026-10-19)
- Cursor subagents — <https://cursor.com/docs/subagents> (diakses 2026-10-19)
- OpenCode agents — <https://opencode.ai/v2/docs/agents> (diakses 2026-10-19)
- OpenCode tools (shell background) — <https://opencode.ai/v2/docs/tools> (diakses 2026-10-19)
- Codex subagents — <https://learn.chatgpt.com/docs/agent-configuration/subagents> (diakses 2026-10-19)

## Changelog

Lihat [CHANGELOG.md](CHANGELOG.md).
