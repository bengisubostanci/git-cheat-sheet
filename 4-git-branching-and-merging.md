# Git Dallanma (Branching) ve Birleştirme (Merging) Yönetimi

Bu rehberde; Git'in en güçlü özelliklerinden biri olan dallanma (branching) mekanizmasını, yeni özellikler geliştirirken ana kodu nasıl koruyacağımızı, dalları yerelde ve uzak depoda (GitHub) nasıl birleştireceğimizi veya sileceğimizi adım adım inceleyeceğiz.

---

## 1. Git'te Dal (Branch) Mantığı Nedir?

Dallar (Branches), ana kod tabanınızı bozmadan yeni özellikler eklemenize, hataları düzeltmenize veya deneyler yapmanıza olanak tanıyan izole çalışma alanlarıdır. 

* **`main` (veya `master`):** Projenizin canlıya çıkan, kararlı sürümünü barındıran varsayılan (default) daldır.
* Yeni bir özellik geliştirileceği zaman `main` dalından yeni bir dal (örneğin `dev` veya `feature-x`) türetilir.

---

## 2. Dalları Listeleme ve Yeni Dal Oluşturma

Mevcut dallarınızı görmek ve yeni bir çalışma alanı açmak için aşağıdaki komut dizilimini kullanabilirsiniz:


# Mevcut yerel dalları listeleme
git branch

Örnek Çıktı:
* main
*  Not: Dal adının başındaki * (yıldız) işareti, şu anda aktif olarak üzerinde çalıştığınız ve bulunduğunuz dalı gösterir.

Yeni Bir Dal Oluşturma ve Seçme
# 'dev' adında yeni bir yerel dal oluşturma
git branch dev

# Oluşturulan dala geçiş yapma
git checkout dev
Kısa Yol (Pro İpucu): Yeni bir dal oluşturup aynı anda o dala geçiş yapmak için tek bir komut kullanabilirsiniz:
git checkout -b dev

3. Dal İçinde Çalışma ve Değişiklikleri İzleme
Şimdi dev dalındayken yeni bir dosya oluşturalım ve bu dalın main dalından nasıl izole olduğunu doğrulamak için farkları (diff) inceleyelim.
# Yeni bir dosya oluşturalım
touch after_dev
Durumu ve Dalların Farkını Kontrol Etme
# Dosyayı hazırlık alanına ekleyip commit edelim
git add .
git commit -m "Feat: Add after_dev file within dev branch"

# İki dal arasındaki farkı karşılaştırma (dev ile main arasındaki farklar)
git diff dev main
Değişiklikleri doğruladıktan sonra, bu yeni dalı yerelinizden GitHub'daki uzak depoya (remote) gönderebilirsiniz:
# Yeni dalı uzak depoya gönderme
git push origin dev

GitHub arayüzüne girdiğinizde, sağ üstteki dal seçim menüsünde artık dev dalının da listelendiğini görebilirsiniz.

4. Dalları Birleştirme (Merging)
dev dalında geliştirdiğiniz özellik tamamlandığında ve test edildiğinde, bu değişiklikleri ana dal olan main ile birleştirmeniz gerekir.

# 1. Öncelikle ana dala (main) geri dönün
git checkout main

# 2. 'dev' dalındaki değişiklikleri 'main' dalına enjekte edin
git merge dev
Örnek Çıktı:
Merge made by the 'recursive' strategy.
 after_dev | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 after_dev

 Birleştirme yerelde tamamlandıktan sonra, main dalının güncel halini GitHub'a göndermeyi unutmayın:
 git push origin main
 
 5. Dalları Silme (Clean Up)
Görevi biten ve başarıyla main dalına aktarılan dalları temizlemek, deponun düzenli kalmasını sağlar.

Yerel (Local) Dalı Silme
# Görevi biten yerel dalı siler (-D zorlayarak silmeyi ifade eder)
git branch -D dev
Uzak Depodaki (Remote / GitHub) Dalı Silme
# GitHub üzerindeki 'dev' dalını siler
git push origin --delete dev

⚠️ Kritik Uyarı: GitHub üzerinde silmek istediğiniz dal, deponun varsayılan (default) dalı olmamalıdır. Eğer varsayılan dalı silmek veya değiştirmek istiyorsanız öncelikle tarayıcıdan GitHub projenize girmeli; Settings -> Branches -> Default branch adımlarını takip ederek başka bir dalı varsayılan olarak atamalısınız.


 
