---
name: proje-baslat
description: Yeni yazılım projesini "önce iskelet, sonra kod" yöntemiyle başlatır (CLAUDE.md, AGENTS.md, docs/, reports/, git init). Kullan - "/proje-baslat", "yeni proje başlat", "proje iskeleti kur", "start new project", "project skeleton".
---

# Proje başlat (iskelet önce, kod sonra)

Kod yazma; sadece iskelet kur. Mevcut dosyaların üzerine yazma.
Kapsam dışı: tek dosyalık/atılacak script'ler için bu skill'i kullanma. Framework scaffolder boş klasör istiyorsa onu önce çalıştır, iskeleti sonra ekle.

## Adımlar
1. Güvenlik: `git rev-parse --is-inside-work-tree` ve klasörün boş olup olmadığına bak. Mevcut repo içindeyse ya da klasör doluysa DUR, hedef klasörü kullanıcıyla teyit et. Proje adı/amacı belirsizse tek satırda sor.
2. Aşağıdaki dosyaları kısa şablonlarla oluştur (`<...>` yerini doldur).
3. `.git` yoksa `git init`. Yalnızca oluşturduğun dosyaları `git add <dosyalar>` ile ekle (asla `git add -A`), ilk commit "chore: proje iskeleti". Remote ekleme, push yapma; push'u yalnızca kullanıcı yapar.
4. Sonraki adımları öner (en altta).

## Dosyalar
- `AGENTS.md` ve `GEMINI.md`: CLAUDE.md'ye symlink (`@import` yalnız Claude'da çalışır):
```
ln -s CLAUDE.md AGENTS.md; ln -s CLAUDE.md GEMINI.md
```
  Symlink mümkün değilse ikisine de tek satır yaz: `Tüm kurallar CLAUDE.md'de; işe başlamadan oku, kuralı yalnız orada düzenle`
- `CLAUDE.md` (≤40 satır):
```
# <Proje adı>
## Amaç
<tek cümle>
## Stack
TBD (mimari kararından sonra yazılır)
## Komutlar
- test: TBD
- build: TBD
## Model rolleri
Claude = planlar, kod yazar, commit eder; Gem Neon = kod/plan review ve ikinci görüş; Hydrogen = araştırma özetleri (reports/). Ayrıntı: kullanıcının global ~/.claude/CLAUDE.md dosyası.
## Kurallar
- Kuralları yalnızca CLAUDE.md'de düzenle (AGENTS.md/GEMINI.md symlink).
- Mimari karar onaylanıp docs/ARCHITECTURE.md'ye yazılmadan uygulama kodu yazılmaz.
- Önce araştırma: docs/NOTES.md ve reports/ dolar, sonra mimari kullanıcıya onaylatılır.
- Test: yeni davranış ve hata düzeltmesinde testi uygulamadan önce çalıştır ve FAIL gör; yalnız-mock ya da totolojik test yazma.
- Her görevin bir "bitti ne zaman" satırı olur.
- Kritik iş başka bir ajan/model tarafından gözden geçirilir.
- CLAUDE.md kısa kalır (≤40 satır); ayrıntı docs/ altına gider.
- Push'u yalnızca kullanıcı yapar.
## Bitti tanımı
Görevin "bitti ne zaman" koşulu doğrulandı (kodda kabul testi geçer), kritik iş başka ajan/model tarafından gözden geçirildi, madde BACKLOG'dan CHANGELOG'a taşındı.
## Bağlantılar
- docs/NOTES.md (ürün kırılımı) | docs/ARCHITECTURE.md (mimari) | docs/BACKLOG.md (iş listesi) | docs/CHANGELOG.md (biten işler)
- docs/CONSTANTS.md (sabitler: endpoint, adres, sürüm) | reports/ (araştırma çıktıları)
```
- `docs/NOTES.md`: `# Notlar` + `## Ürün kırılımı`, `## Bileşenler / özellikler`, `## Açık sorular` (boş madde `- `).
- `docs/ARCHITECTURE.md`: `# Mimari` + `Durum: taslak` (taslak/onaylı) + `## Kararlar` (boş).
- `docs/BACKLOG.md` (biten madde silinip CHANGELOG'a taşınır):
```
# Backlog
## Yapılacak
- [ ] Araştırma ve mimari kararı — bitti ne zaman: reports/ dolu, NOTES açık soruları kapalı, docs/ARCHITECTURE.md kullanıcı onaylı
## Devam eden
```
- `docs/CHANGELOG.md`: `# Changelog` başlığı + tarihli satırlar.
- `docs/CONSTANTS.md`: `# Sabitler` + tablo (ad | değer | not).
- `reports/.gitkeep` (boş).
- `.gitignore`: en az `.env*`, `node_modules/`, `__pycache__/`, `.venv/`.

## Sonraki adımlar (kullanıcıya öner)
1. Araştırma görevlerini listele; çıktıları `reports/` altına yazdır (ucuz ajanlara).
2. NOTES.md'yi doldur, açık soruları kapat.
3. Mimari taslağı ARCHITECTURE.md'ye yaz, kullanıcıya onaylat (durum: onaylı); stack'i CLAUDE.md'ye yaz, BACKLOG'a özellikleri ekle.
