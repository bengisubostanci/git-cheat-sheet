# Git Temelleri: Adım Adım Uygulamalı Rehber

Bu kılavuz; Git Versiyon Kontrol Sistemi'nin (VCS) temel mantığını, yapılandırma adımlarını, temel iş akışlarını, değişiklik takibini ve geçmiş sürümlere geri dönme (rollback) işlemlerini kapsamaktadır.

---

## 1. Git Nedir?
Git, yazılım geliştirme sürecinde kaynak kodlardaki değişiklikleri takip etmek için tasarlanmış dağıtık bir **Versiyon Kontrol Sistemi'dir (VCS)**. Birden fazla yazılımcının aynı anda çalışmasını sağlar, değişikliklerin eksiksiz bir geçmişini tutar, dallanma (branching) ve birleştirme (merging) işlemlerini kolaylaştırır.

---

## 2. İlk Git Yapılandırmaları

Bir depoyu (repository) başlatmadan önce, küresel kullanıcı kimliğinizi, terminal çıktılarını ve satır sonu davranışlarını yapılandırmanız gerekir.

bash
# Küresel kullanıcı kimliğini ayarlama
git config --global user.name "Adınız Soyadınız"
git config --global user.email "eposta@adresiniz.com"

# Yapılandırmaları doğrulama
git config --global user.name
git config --global user.email

# Terminal çıktılarında renkli gösterimi aktif etme
git config --global color.ui auto


3. Git Projesi Oluşturma
Bir projeyi takip etmeye başlamak için önce bir dizin oluşturmalı ve ardından bir Git deposu başlatmalısınız. Bu işlem, Git'in tüm proje geçmişini sakladığı gizli bir .git klasörü oluşturur.
# Proje dizinini oluşturma ve içine geçiş yapma
mkdir git_projesi
cd git_projesi

# Yeni bir yerel Git deposu başlatma
git init
Başlatma işlemini gizli dosyaları listeleyerek doğrulayabilirsiniz:
ls -al
Örnek Çıktı:
drwxr-xr-x 1 user staff   0 Jun 19 17:00 .
drwxr-xr-x 1 user staff   0 Jun 19 17:00 ..
drwxr-xr-x 1 user staff   0 Jun 19 17:00 .git

4. Temel Git İş Akışı: Commit ve LogTemel Git yaşam döngüsü şu şekilde ilerler: Çalışma Dizini (Working Directory) $\rightarrow$ Hazırlık Alanı (Staging Area) $\rightarrow$ Yerel Depo (Local Repository).Adım 4.1: Bir Betik Dosyası Oluşturma
touch hello.sh
chmod +x hello.sh
hello.sh dosyasının içine aşağıdaki kodları ekleyin:
#!/bin/bash
echo "Merhaba Git"
Adım 4.2: Değişiklikleri İzleme ve Commit Etme
# Çalışma alanınızın durumunu kontrol edin
git status

# Dosyayı Hazırlık Alanına (Staging Area) ekleyin
git add hello.sh

# Değişiklikleri açıklayıcı bir mesajla Yerel Depoya kaydedin (Commit)
git commit -m "Feat: hello.sh betiği eklendi ve test edildi"
Adım 4.3: Versiyon Geçmişini Görüntüleme
git log
Örnek Çıktı:
commit 725c485ba552c26b73c78322adb5bfaa6105dfb0
Author: Adınız <eposta@adresiniz.com>
Date:   Fri Jun 19 17:15:00 2026 +0300

    Feat: hello.sh betiği eklendi ve test edildi

5. Takip Edilmeyen Dosyalarla Çalışmak
Şimdi yeni bir dosya ekleyelim ve Git'in takip edilmeyen (untracked) ile değiştirilmiş (modified) durumları nasıl algıladığını inceleyelim.
# Yeni bir dosya oluşturma
touch listhere.sh
chmod +x listhere.sh
Depo Durumunu Kontrol Etme
git status
Örnek Çıktı:
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	listhere.sh

nothing added to commit but untracked files present (use "git add" to track)
Yeni Dosyayı Hazırlama ve Commit Etme
git add listhere.sh
git commit -m "Feat: Dizin listeleme betiği (listhere.sh) eklendi"


6. Değişiklikleri İncelemek (git diff)
Takip edilen bir dosya çalışma dizininde değiştirildiğinde, bu değişiklikleri hazırlık alanına göndermeden önce tam olarak hangi satırların değiştiğini inceleyebilirsiniz.
#!/bin/bash
echo "Merhaba Git"
echo "Bir değişiklik yaptım"
Değişiklikleri Görüntüleme
git diff hello.sh
Örnek Çıktı:
diff --git a/hello.sh b/hello.sh
index 482acd7..dc72ce5 100644
--- a/hello.sh
+++ b/hello.sh
@@ -1,3 +1,5 @@
 #!/bin/bash
 
 echo "Merhaba Git"
+
+echo "Bir değişiklik yaptım"
Not: + ile başlayan satırlar eklemeleri, - ile başlayan satırlar ise silinenleri gösterir.

Hazırlık alanına (Staging Area) alınmış dosyaların farklarını görmek için ise şu komut kullanılır:
git diff --staged hello.sh
Değişikliği hazırlayıp commit edin:
git add hello.sh
git commit -m "Chore: hello.sh dosyasına yeni bir ek mesaj eklendi"
7. Değişiklikleri Geri Almak ve Rollback İşlemleri
Git, geliştirme sürecinin farklı aşamalarında yapılan hataları geri almak için güçlü araçlar sunar.

Senaryo A: Çalışma Dizinindeki Değişiklikleri İptal Etme
Eğer takip edilen bir dosyada (readme.md) yanlışlıkla bir değişiklik yaptıysanız ve dosyayı son commit durumuna döndürmek istiyorsanız:
# Çalışma dizinindeki yerel değişiklikleri çöpe atar
git checkout -- readme.md
Senaryo B: Hazırlık Alanındaki Değişiklikleri Geri Çekme (git reset)
Eğer bir silme veya değiştirme işlemini yanlışlıkla hazırlık alanına eklediyseniz (örneğin git rm hello.sh veya git add . komutunu hatalı çalıştırdıysanız):
# Değişikliği Hazırlık Alanından çıkarıp Çalışma Dizinine geri taşır
git reset HEAD hello.sh

# Çalışma dizinindeki bu değişikliği de tamamen iptal etmek için:
git checkout -- hello.sh

8. Belirli Bir Geçmiş Sürüme Dönmek
Her commit, zamanda benzersiz bir anlık görüntüdür (snapshot). Bir dosyayı veya tüm dizini geçmişteki herhangi bir commit ID'sine (hash değerine) geri döndürebilirsiniz.

git log --oneline komutunu kullanarak hedef commit ID'sini bulun.

İlgili dosyanın o commit anındaki durumunu geri yükleyin:

# Belirli bir commit noktasındaki dosya sürümünü geri getirir
git checkout <commit-hash> -- readme.md
hello.sh dosyasını güncelleyin:
