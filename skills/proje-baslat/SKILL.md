---
name: proje-baslat
description: Yeni yazılım projesini "önce iskelet, sonra kod" yöntemiyle başlatır (CLAUDE.md, AGENTS.md, docs/, reports/, git init). Kullan - "/proje-baslat", "yeni proje başlat", "proje iskeleti kur", "start new project", "project skeleton".
---

# Proje başlat (iskelet önce, kod sonra)

Boş/yeni klasörde çalışır. Kod yazma; sadece iskelet kur. Mevcut dosyaların üzerine yazma.

## Adımlar
1. Proje adı/amacı belirsizse tek satırda sor ya da teyit et.
2. Aşağıdaki dosyaları kısa şablonlarla oluştur (`<...>` yerini doldur).
3. `git init`, `git add -A`, ilk commit ("chore: proje iskeleti"). Remote ekleme, push yapma; push'u yalnızca kullanıcı yapar.
4. Sonraki adımları öner (en altta).

## Dosyalar
- `AGENTS.md` (tek kaynak CLAUDE.md, sapma olmasın):
```
See CLAUDE.md
@CLAUDE.md
```
- `CLAUDE.md` (≤40 satır):
```
# <Proje adı>
## Amaç
<tek cümle>
## Stack
TBD (mimari kararından sonra yazılır)
## Kurallar
- Kuralları yalnızca CLAUDE.md'de düzenle (AGENTS.md sadece işaret eder).
- Testler kabul koşulunu yazar ve yanlış davranışta FAIL etmeli; içi boş test yok.
- Her görevin bir "bitti ne zaman" satırı olur.
- Önce araştırma ve mimari: önce docs/NOTES.md ve reports/ dolar; kodlamadan önce kısa mimari kararı kullanıcıya onaylatılır.
- Kritik iş başka bir ajan/model tarafından gözden geçirilir.
- CLAUDE.md kısa kalır (≤40 satır); ayrıntı docs/ altına gider.
- Push'u yalnızca kullanıcı yapar.
## Bitti tanımı
Kabul testleri geçer, BACKLOG'da Bitti'ye taşındı, CHANGELOG'a işlendi, gözden geçirildi.
## Bağlantılar
- docs/NOTES.md (ürün kırılımı) | docs/BACKLOG.md (iş listesi) | docs/CHANGELOG.md (biten işler)
- docs/CONSTANTS.md (sabit bilgiler: endpoint, adres, sürüm) | reports/ (araştırma çıktıları)
```
- `docs/NOTES.md`:
```
# Notlar
## Ürün kırılımı
## Bileşenler / özellikler
- 
## Açık sorular
- 
```
- `docs/BACKLOG.md` (biten madde silinip CHANGELOG'a taşınır; her madde "bitti ne zaman" içerir):
```
# Backlog
## Yapılacak
- [ ] <görev> — bitti ne zaman: <koşul>
## Devam eden
## Bitti
(CHANGELOG.md'ye taşı)
```
- `docs/CHANGELOG.md`: `# Changelog` başlığı + tarihli satırlar.
- `docs/CONSTANTS.md`: `# Sabitler` + tablo (ad | değer | not): endpoint, adres, sürüm.
- `reports/.gitkeep` (boş).
- `.gitignore`: en az `.env*`, `node_modules/`, `__pycache__/`, `.venv/`.

## Sonraki adımlar (kullanıcıya öner)
1. Araştırma görevlerini listele; çıktıları `reports/` altına yazdır (ucuz ajanlara).
2. NOTES.md'yi doldur, açık soruları kapat.
3. Kısa mimari taslağı çıkar, kullanıcıya onaylat; sonra stack'i CLAUDE.md'ye yaz ve BACKLOG'a özellikleri ekle.
