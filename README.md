# Kanna

**Fact-Verifying Tsundere Coder** — skill agent untuk coding, refactor, bug hunt, dan verifikasi fakta lapangan.

> "Aku bukan asisten yang bilang 'siap, kak!' ke setiap permintaan. Aku partner yang bikin kamu nggak nyesel minggu depan."

Kanna adalah persona coding agent berbahasa Indonesia yang menolak menyentuh kode sebelum gerbang keamanan dan desain terpenuhi. Dia memverifikasi klaim sebelum dipakai, hemat baris kode, mencatat technical debt secara eksplisit, dan aktif mencari bug sebelum menyatakan pekerjaan selesai.

## Fitur

- **Gerbang berurutan yang tidak bisa dibalik** — Root/Admin, Credential, Backup, Documentation, Design, Context7, dan Gerbang Hemat.
- **Verifikasi dokumentasi library** lewat Context7, dengan precheck MCP/Node.js dan fallback WebFetch yang jujur.
- **Framework Adoption Evidence** — data adopsi wajib dari sumber primer (Stack Overflow Survey, State of JS, JetBrains, dsb.), bukan dari ingatan model.
- **Error Gate** — Context7 → WebFetch → reproduksi → perbaikan → verifikasi pasca.
- **Bug Hunt Protocol** — label bukti (✅ direproduksi, 📖 terbukti dari sumber, 🧠 penalaran, ⚠️ known issue), klasifikasi prioritas, zero-fix rule, dan reproduksi terisolasi.
- **Sinkronisasi dokumentasi pasca-aksi** — README, CHANGELOG, dan struktur folder.
- **Persona tsundere fungsional** — sindiran selalu disertai perbaikan konkret; maksimal satu kaomoji teks per respons.
- **Cross-platform** — Unix/Linux/macOS, Windows (cmd, PowerShell 5.1 & 7+), WSL, Docker Desktop, dan Git Bash.

## Instalasi

### OpenCode (global)

```bash
git clone git@github.com:aditiya-saputra/kanna.git ~/.config/opencode/skills/kanna
```

Jika folder tujuan sudah ada, clone di tempat lain lalu salin `SKILL.md`:

```bash
git clone git@github.com:aditiya-saputra/kanna.git /tmp/kanna
cp /tmp/kanna/SKILL.md ~/.config/opencode/skills/kanna/SKILL.md
```

### OpenCode (project-local)

```bash
mkdir -p .opencode/skills/kanna
cp SKILL.md .opencode/skills/kanna/SKILL.md
```

OpenCode menemukan skill dari frontmatter `name` dan `description` di `SKILL.md`. Tidak perlu registrasi tambahan.

## Pemakaian

- Ketik `@kanna` di prompt untuk memuat skill secara eksplisit.
- Atau minta agent memuat skill dengan ID `kanna`.
- Skill juga diiklankan otomatis ketika deskripsinya relevan dengan permintaan.

Contoh:

```text
@kanna refactor modul auth ini, tapi verifikasi dulu API library-nya
```

## Struktur

```text
kanna/
├── SKILL.md      # Definisi lengkap persona, gerbang, dan protokol
├── README.md     # Dokumen ini
└── CHANGELOG.md  # Riwayat perubahan
```

## Kompatibilitas

- Format `SKILL.md` + frontmatter YAML.
- Dapat ditempatkan di source skill mana pun yang mendukung `SKILL.md`, termasuk `~/.config/opencode/skills`, `~/.claude/skills`, atau `~/.agents/skills`.
- Perintah shell di dalam skill menyediakan varian Unix dan Windows; asumsi platform selalu disebutkan.

## Lisensi

Belum ditetapkan. Tambahkan file `LICENSE` sebelum mendistribusikan ulang.

## Changelog

Lihat [CHANGELOG.md](CHANGELOG.md).
