## 1. Çalışma Alanları Arasındaki Geçişler (Workflow)

Git'in temel iş akışı üç ana alandan oluşur: **Çalışma Dizini (Working Directory)**, **Hazırlık Alanı (Staging Area)** ve **Yerel Depo (Local Repository)**.



### 📥 Hazırlık Alanına Ekleme (Working Directory $\rightarrow$ Staging Area)
Değişikliklerinizi kaydetmeden önce hazırlık alanına göndermek için şu yöntemleri kullanabilirsiniz:

* **Yöntem 1 (Belirli bir dosya):** `git add dosya_adi.txt`
* **Yöntem 2 (Yeni ve değiştirilmiş tüm dosyalar):** `git add .`
* **Yöntem 3 (Silinenler dahil tüm proje):** `git add --all`

### 📤 Hazırlık Alanından Geri Alma (Staging Area $\rightarrow$ Working Directory)
Hazırlık alanına yanlışlıkla eklediğiniz dosyaları geri çekmek (unstage) için:

* **Yöntem 1 (Sadece belirli bir dosya):** `git rm --cached dosya_adi.txt` *(Dosyayı diskten silmez, sadece Git hazırlık alanından çıkarır)*
* **Yöntem 2 (Tüm hazırlık alanını sıfırlama):** `git reset`

---

## 2. Kalıcı Kayıt ve Değişiklikleri Geri Alma (Commit & Rollback)

### 💾 Değişiklikleri Kaydetme (Staging Area $\rightarrow$ Local Repository)
Hazırlık alanındaki dosyaları yerel depoya kalıcı bir versiyon olarak işlemek için:
```bash
git commit -m "Mesaj: Dosya ekleme ve iyileştirmeler yapıldı"

🔄 En Son Commit Sonrası Yapılan Değişiklikleri İptal Etme
Henüz commit edilmemiş yerel değişiklikleri çöpe atıp dosyayı son commit haline döndürmek için:
git checkout -- dosya_adi.txt

⏳ Geçmişteki Bir Commit Sürümüne Geri Dönme
Belirli bir dosyanın veya tüm projenin geçmişteki bir commit anındaki halini geri yüklemek için (git log ile commit hash değerini alabilirsiniz):

Yöntem 1 (Sadece belirli bir dosya için): git checkout <commit-hash> -- dosya_adi.txt

Yöntem 2 (Tüm proje dizini için): git checkout <commit-hash> -- .

Örnek Kullanım:
git checkout dbc5c8de11c -- myfile.txt
cat myfile.txt
# Çıktı: Merhaba ben ilk satırım (Geçmiş versiyondaki hali)
3. Dal (Branch) Yönetimi ve Silme İşlemleri
🌿 Yerel Dal Komutları
# Mevcut dalları listeleme (* işaretli olan aktif daldır)
git branch

# 'testing' adında yeni bir dal oluşturma
git branch testing

# Oluşturulan dala geçiş yapma
git checkout testing

# Görevi biten yerel bir dalı silme
git branch -d <branch-adi>

☁️ Uzak Depo (GitHub) Üzerinden Dal SilmeEğer GitHub üzerindeki bir dalı silmek istiyorsanız ve bu dal varsayılan (default) dal ise öncelikle değiştirmeniz gerekir:
GitHub tarayıcınızdan projeye gidin.Settings
Default branch adımlarını takip ederek başka bir dalı (örn: main) varsayılan yapın.Ardından terminalden şu komutla hedef dalı silin:
git push origin --delete <branch-adi>

4. Karşılaştırma ve İnceleme (git diff)
İki farklı commit arasındaki satır bazlı değişiklikleri incelemek için commit hash kodlarını ve dosya adını kullanabilirsiniz:
git diff <commit-hash-1> <commit-hash-2> dosya_adi
Örnek Terminal Çıktısı:
$ git diff dbc5c8de11 322740671 myfile
diff --git a/myfile b/myfile
index 9765325..4886f4a 100644
--- a/myfile
+++ b/myfile
@@ -1 +1,3 @@
 Merhaba ben ilk satırım
+
+Bu ikinci satırım

💡 Not: + işaretiyle başlayan yeşil satırlar eklenen kodları, - işaretiyle başlayan kırmızı satırlar ise silinenleri temsil eder.

5. Uzak Depo (GitHub) Entegrasyonu
Yerel projenizi buluttaki bir GitHub deposuna bağlamak ve kodlarınızı göndermek için:

# Yerel depoya uzak GitHub adresini 'origin' takma adıyla tanıtma
git remote add origin [https://github.com/kullanici_adi/repo-adi.git](https://github.com/kullanici_adi/repo-adi.git)

# Eklenmiş olan uzak depoyu doğrulama
git remote -v

# Kodları uzak depodaki ana dala gönderme (Push)
git push origin main
⌨️ Bonus: Git Bash Kısayolları (Kopyala - Yapıştır)
Git Bash (Terminal) üzerinde alışılagelmiş Windows kısayolları çalışmaz. Aşağıdaki pratik kombinasyonları kullanabilirsiniz:

Kopyalama: Terminalde farenizle (mouse) bir metni seçtiğiniz an otomatik olarak kopyalanır. Alternatif olarak Ctrl + Insert tuşlarını kullanabilirsiniz.

Yapıştırma: Shift + Insert veya Ctrl + Shift + V kombinasyonları ile terminale metin yapıştırabilirsiniz.
