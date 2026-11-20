# Section briefs

Every section: `## NN. Title`, opening sentence with the point + number, then content below. Cite facts.md.

## 01 Proje tanımı ve kapsam
Problem, solution in 2 sentences, target user, scope and out-of-scope list. Table: Çıktı | Konum | İçerik (deliverables). Table: key numbers (LOC, modules, tests, commits).

## 02 Mimari
Layers and data flow end to end. Table: Bileşen | Dosya | Sorumluluk | Bağımlılık. Table: key design decisions | gerekçe | ödünleşim. Include one `diagram-spec` block (nodes, arrows, labels, groupings) for the architecture figure.

## 03 Teknolojiler
Table: Teknoloji | Sürüm (lockfile) | Rolü | Neden seçildi. Separate runtime, dev and test dependencies.

## 04 Geliştirme süreci
Phases in order with dates/commit counts from git. Table: Aşama | Dönem | Çıktı | Kilit karar. Include a `diagram-spec` timeline (phase, start, end, milestone).

## 05 Değerlendirme ve testler
Test suite: count, runner command, pass rate. One subsection per evaluation, each with a results table and file reference; note set size and what the numbers cannot show. Table: Test alanı | Test sayısı | Kapsam.

## 06 Çok yönlü kalite değerlendirmesi (puanlı)
Table: Boyut | Puan (/10) | Gerekçe (kanıt) | En büyük eksik. Dimensions: doğruluk/kalite, mimari, kod kalitesi, test/ölçüm, dokümantasyon, güvenlik/gizlilik, performans, kullanılabilirlik, bakım kolaylığı, teslime hazırlık. Weighted overall score with stated weights. Every score cites evidence; no score above 8 without measured support.

## 07 Sınırlamalar ve riskler
Table: Risk | Olasılık | Etki | Kanıt | Azaltma. Separate "bilinen sınırlar" (confirmed) from "olası riskler". Rank by impact.

## 08 Alternatif teknolojiler
For each major choice (3-6 choices): Table: Seçenek | Artı | Eksi | Ne zaman tercih edilir. Mark the chosen option and say whether switching is justified now, with a number or condition.

## 09 Yol haritası
Table: Öncelik | İş | Kazanım | Efor (S/M/L) | Önkoşul | Ölçüt. Group as Şimdi / Sonra / Belki. Include a `diagram-spec` roadmap (lanes, items, dependencies). Each item links to a section 06/07 finding.

## 10 CV ve portföy değeri (optional)
Table: Beceri | Kanıt (dosya/sayı) | CV cümlesi. 3 ready CV bullets with numbers, a 2-sentence portfolio blurb, interview talking points. Only claims backed by facts.md.

## 11 Ekler
Table: Dosya haritası (path | amaç). Komutlar (install, run, test, eval). Sözlük. Kaynak/olgu listesi pointing to facts.md items; "doğrulanmadı" list.
