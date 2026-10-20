# Evaluasi Pelatihan – Report Generator

Web app untuk membuat lembar **Evaluasi Pelatihan** (PDF 1 halaman) dari hasil ekspor kuesioner Excel.

## Struktur

```
index.html          ← seluruh aplikasi (upload Excel, form, editor rangkuman, ekspor PDF)
api/summarize.js    ← Vercel Function: meneruskan komentar ke GitHub Models (ringkasan AI)
package.json
```

## Environment Variables (Vercel)

| Nama | Wajib | Keterangan |
|---|---|---|
| `GITHUB_MODELS_TOKEN` | Ya, untuk fitur AI | Fine-grained personal access token GitHub dengan izin **Models: Read-only** |
| `GITHUB_MODELS_MODEL` | Tidak | Default `openai/gpt-4.1-mini` |

Tanpa token, app tetap berjalan penuh; tombol AI disembunyikan dan rangkuman memakai mode **Rapikan** (tanpa AI).

## Uji di lokal (opsional)

```bash
npm i -g vercel
echo "GITHUB_MODELS_TOKEN=github_pat_xxx" > .env.local
vercel dev
```

Buka http://localhost:3000. Cek status AI di http://localhost:3000/api/summarize → `{"configured":true}`.

## Deploy

Setiap `git push` ke branch utama otomatis di-deploy ulang oleh Vercel.
