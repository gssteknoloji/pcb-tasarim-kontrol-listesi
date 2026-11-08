# PCB Tasarım Kontrol Listesi

**Üretime göndermeden önce son bakış.** Bu liste, [GSS Teknoloji](https://gss.com.tr) olarak kendi kartlarımızı üretime vermeden önce geçtiğimiz maddelerden derlendi. Her madde en az bir kez canımızı yakmış bir hatadan geliyor. Kopyalayın, kendi projenize uyarlayın; eksik gördüğünüz maddeyi *pull request* ile ekleyin.

*English summary at the end.*

Kullanım: her maddeyi `[ ]` → `[x]` yaparak işaretleyin. "Geçerli değil" olan maddeyi silmeyin, `[-]` yapın; böylece neyin bilinçli atlandığı sonradan anlaşılır.

---

## 1. Şema

- [ ] Her netin bir adı var; `Net-(R12-Pad1)` gibi otomatik adlar güç ve haberleşme hatlarında kalmadı.
- [ ] Bütün besleme sembolleri doğru nete bağlı (3V3 ile 3.3V, GND ile AGND karışmadı).
- [ ] Kullanılmayan girişler tanımlı: pull-up / pull-down ya da sürülüyor. Kullanılmayan op-amp katları kapatıldı.
- [ ] Her IC'nin besleme bacağının yanında dekuplaj kondansatörü var (tipik 100 nF, ayrıca 1–10 µF toplu).
- [ ] Reset, enable ve boot/strapping pinleri açılışta doğru seviyede; bu pinlere bağlı çevre birimleri açılış seviyesini bozmuyor.
- [ ] Polarite: diyot, elektrolitik kondansatör, LED ve konnektör pin 1 yönleri şemada ve kılıfta aynı.
- [ ] Sigorta, TVS ve ters polarite koruması giriş konnektörünün hemen arkasında.
- [ ] I²C hatlarında pull-up var ve değeri hat kapasitesine göre seçildi; adres çakışması yok.
- [ ] UART çaprazlaması doğru (TX → RX). RS485 için A/B ve sonlandırma direnci kararı verildi.
- [ ] Analog girişlerde RC filtre ve gerekiyorsa koruma diyotu var; ADC referansı temiz.
- [ ] Kristal yük kondansatörleri kristalin veri sayfasına göre hesaplandı.
- [ ] Test noktaları şemada tanımlı: besleme rayları, reset, UART, haberleşme hatları.
- [ ] Değerler ve tolerans/gerilim sınıfları girildi; "DNP" (takılmayacak) parçalar işaretli.
- [ ] Şema üzerinde revizyon numarası ve tarih var.

## 2. Kılıf (footprint) ve kütüphane

- [ ] Her yeni kılıf veri sayfasındaki önerilen pad deseniyle karşılaştırıldı; pad numaraları şema pinleriyle eşleşti.
- [ ] Konnektörlerin pin 1'i, polarite anahtarı ve mekanik delikleri kılıfta doğru; **1 ölçeğinde kâğıda basıp parçayı üstüne koydunuz mu?**
- [ ] Termal pad'li parçalarda (QFN, DPAK) termal pad ve via dizisi tanımlı; lehim pastası açıklığı parçalanmış.
- [ ] 3D modeller yüklü; kasa ve komşu parçalarla çakışma kontrolü yapıldı.
- [ ] Courtyard (yerleşim alanı) katmanı her kılıfta var; DRC bunu kullanıyor.

## 3. Yerleşim

- [ ] Konnektörler, LED'ler, butonlar ve montaj delikleri mekanik çizimdeki koordinatlarda; kasa ile son kontrol yapıldı.
- [ ] Dekuplaj kondansatörleri ilgili besleme bacağına en yakın yerde, via'dan önce.
- [ ] Kristal mikrodenetleyiciye bitişik, altında kesintisiz toprak, çevresinde sinyal yolu yok.
- [ ] Anahtarlamalı regülatörün sıcak döngüsü (giriş kondansatörü – anahtar – diyot/indüktör) en kısa; indüktör altında hassas sinyal yok.
- [ ] Analog ve dijital bölümler ayrıldı; ADC ve referans gürültülü hatlardan uzak.
- [ ] Isınan parçalar (regülatör, sürücü, güç direnci) birbirinden ve sıcaklık sensöründen uzak; soğutma yüzeyi düşünüldü.
- [ ] Anten / RF modül kenarda, altında ve çevresinde bakır yok (keep-out), modül üreticisinin önerdiği mesafe korundu.
- [ ] Yüksek gerilim ile düşük gerilim arasında yeterli yalıtım mesafesi; gerekiyorsa yarık (slot) açıldı.
- [ ] Programlama konnektörü ve UART erişilebilir; kart kasadayken de ulaşılıyor.
- [ ] Parça yönleri (polarite) olabildiğince aynı yöne bakıyor; dizgi ve kontrol kolaylaşır.

## 4. Yollama (routing)

- [ ] Güç yolları akıma göre genişletildi (dış katman 1 oz için yaklaşık 1 mm / 1 A başlangıç; hesap aracıyla doğrulayın).
- [ ] Her sinyal via'sının yakınında dönüş yolu (toprak via'sı) var; toprak düzlemi bölünmedi.
- [ ] Diferansiyel çiftler (USB, RS485, Ethernet) birlikte ve eşit uzunlukta; empedans hedefi üretici stackup'ına göre.
- [ ] Hassas hatlar (ADC, kristal, reset) uzun paralel dijital hatların yanından geçmiyor.
- [ ] 90° köşe yok; dar açılı pad girişleri (asit tuzağı) yok.
- [ ] Termal rahatlama (thermal relief) elle lehimlenecek ve THT pad'lerde açık; büyük bakırlara direkt bağlı pad'ler lehimlenirken soğuk lehim yapar.
- [ ] Via-in-pad kullanıldıysa doldurulmuş / kapatılmış via olarak sipariş edildi.
- [ ] Topraklama stratejisi yazıldı: tek nokta mı, düzlem mi, kasa toprağı nereden bağlanıyor.

## 5. Güç ve koruma

- [ ] Giriş: ters polarite koruması, sigorta (ya da PTC), TVS; gerilim sınıfları girişin en kötü durumuna göre.
- [ ] Regülatör giriş–çıkış farkı ve güç kaybı hesaplandı; LDO'da sıcaklık artışı kabul edilebilir.
- [ ] Açılış sırası (power sequencing) gerektiren parçalar için sıralama sağlandı.
- [ ] Brown-out eşiği ve besleme çökme davranışı düşünüldü; EEPROM/flash yazarken besleme kesilirse ne olacak?
- [ ] Dışarıya açık her port (USB, RS485, sensör girişi) ESD koruması ile donatıldı.
- [ ] Röle ve indüktif yüklerde serbest geçiş diyotu / snubber var.

## 6. Üretilebilirlik (DFM)

- [ ] Üreticinin kurallarıyla DRC çalıştırıldı: minimum yol / aralık, delik çapı, halka genişliği, lehim maskesi genişliği.
- [ ] Kart kenarından bakıra ve bileşene güvenli mesafe (tipik ≥ 0,3 mm bakır, ≥ 1 mm parça).
- [ ] Delik çapları standart; en küçük delik üreticinin ücretsiz sınırının üstünde (çoğu üreticide 0,3 mm).
- [ ] Lehim maskesi köprüsü ince adımlı parçalarda korunuyor; yoksa maske açıklığı "gang" yapıldı ve bilinçli karar verildi.
- [ ] Katman dizilimi ve kalınlık (ör. 1,6 mm, 1 oz) üreticinin standart seçeneğinde; özel istek varsa siparişte belirtildi.
- [ ] Yüzey kaplaması seçildi (HASL / kurşunsuz HASL / ENIG); ince adımlı BGA ve altın parmaklarda ENIG.
- [ ] Panelleme gerekiyorsa: V-cut ya da sekmeli (mouse-bite), kenar şeritleri, fiducial'lar ve araç delikleri eklendi.
- [ ] Kart dış hattı (Edge.Cuts / outline) kapalı tek bir çizgi; iç kesimler ayrı tanımlı.

## 7. Dizgi (DFA)

- [ ] Fiducial: kartta en az 2, tercihen 3; ince adımlı parçaların yanında yerel fiducial.
- [ ] Parça aralıkları dizgi makinesinin nozulunu ve yeniden işlemeyi (rework) düşünerek bırakıldı.
- [ ] Çift yüz dizgi varsa ağır parçalar üst yüzde; alt yüzde yeniden akış sırasında düşme riski olan parça yok.
- [ ] BOM tam: üretici adı, üretici parça numarası, referanslar, adet, DNP işaretleri, alternatif parçalar.
- [ ] Pick & place (CPL) dosyası: referans, X, Y, yüz, dönüş; dönüş açıları üreticinin konvansiyonuna göre kontrol edildi.
- [ ] Kritik parçaların stoğu sipariş vermeden önce kontrol edildi; stokta olmayan parça için alternatif belirlendi.

## 8. Serigrafi ve işaretleme

- [ ] Her parçanın referansı okunur ve pad üstüne gelmiyor; yön/polarite işaretleri parça takıldıktan sonra da görünüyor.
- [ ] Konnektör pin 1 ve sinyal adları (VCC, GND, A, B, TX, RX) serigrafide yazılı.
- [ ] Kart adı, revizyon, tarih ve firma / proje kodu yazılı; gerekiyorsa seri numarası alanı boş bırakıldı.
- [ ] Yazı yüksekliği en az 1 mm, çizgi kalınlığı en az 0,15 mm.
- [ ] Yüksek gerilim, sıcak yüzey gibi uyarı sembolleri gerekli yerlerde.

## 9. Test ve devreye alma

- [ ] Test noktaları en az 1 mm çapında ve tek yüzde toplanmış; iğne yatağı (bed of nails) planı varsa koordinatlar paylaşıldı.
- [ ] İlk güç verme planı yazıldı: akım sınırlı kaynak, beklenen boşta akım, hangi rayın hangi sırayla ölçüleceği.
- [ ] Programlama ve ilk yazılım yükleme yöntemi belli (UART/JTAG/USB); üretim test yazılımı var mı?
- [ ] Kart üstünde "canlı" göstergesi: güç LED'i ve bir durum LED'i.

## 10. Çıktılar ve sipariş

- [ ] Gerber: tüm bakır katmanlar, lehim maskesi (üst/alt), serigrafi (üst/alt), lehim pastası (dizgi için), kart dış hattı; **RS-274X** formatında.
- [ ] Delik dosyası: kaplamalı ve kaplamasız delikler ayrı (ya da üretici birleşik istiyorsa birleşik), Excellon formatında, birim ve orijin belirtilmiş.
- [ ] Gerber'ler **bağımsız bir görüntüleyicide** açılıp kontrol edildi (tasarım programında değil). Yansıma, eksik katman ve kaymış delik en çok burada yakalanır.
- [ ] Üretim notları yazıldı: katman sayısı, kalınlık, bakır ağırlığı, kaplama, maske ve serigrafi rengi, kontrollü empedans, özel istekler.
- [ ] Dosya adlarında proje adı ve revizyon var; ZIP tek klasörde, içinde eski revizyon kalıntısı yok.
- [ ] BOM, CPL ve montaj çizimi revizyonla eşleşiyor.
- [ ] Sipariş adedi, üretim süresi ve teslim adresi onaylandı; prototip için küçük adet, seri üretim öncesi **mutlaka bir prototip turu**.

---

## English summary

A pre-production PCB checklist distilled from our own board reviews at GSS Teknoloji. Sections: **schematic** (net names, decoupling, strapping pins, protection), **footprints** (datasheet land patterns, pin 1, 3D clash check, 1:1 paper print), **placement** (connectors to mechanical drawing, decoupling next to pins, crystal and switcher hot loops, RF keep-out, isolation), **routing** (trace widths, return paths, differential pairs, no acid traps, thermal reliefs), **power and protection** (reverse polarity, fuse, TVS, brown-out, ESD on every external port), **DFM** (fab rules DRC, edge clearance, standard drills, stackup, finish, panelization), **DFA** (fiducials, BOM with MPNs, pick-and-place rotations, stock check), **silkscreen** (polarity marks, pin 1, revision), **test** (test points, first power-up plan), and **outputs** (RS-274X Gerbers, Excellon drills, check in an independent viewer, fab notes, versioned ZIP, prototype run before volume).

Contributions welcome. Maintained by [GSS Teknoloji](https://gss.com.tr), Ankara.
