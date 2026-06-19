# Git ile Dosya ve Klasörleri Yoksayma: `.gitignore` Kullanımı

Bu rehberde; Git tarafından takip edilmesini istemediğimiz özel dosyaların, hassas verilerin veya log klasörlerinin `.gitignore` dosyası kullanılarak nasıl dışarıda bırakılacağını ve bazı özel durumlar için istisnaların nasıl tanımlanacağını adım adım inceleyeceğiz.

---

## 1. `.gitignore` Nedir ve Neden Kullanılır?

Projelerimizde Git deposuna (repository) eklenmesini istemediğimiz bazı dosyalar bulunur. Bunlara örnek olarak; yerel yapılandırma dosyaları (`.env`), şifreler, büyük veri logları, `node_modules` klasörleri veya işletim sisteminin otomatik ürettiği (`.DS_Store`) dosyalar verilebilir. 

Bu tarz dosyaları kalıcı olarak Git takibinden çıkarmak için proje kök dizinine bir `.gitignore` dosyası ekleriz.

---

## 2. Temel Dosya Yoksayma Adımları

Öncelikle Git'in takip etmesini istemediğimiz gizli bir dosya oluşturalım ve çalışma alanımızın durumunu inceleyelim.


# Takip edilmesini istemediğimiz özel bir dosya oluşturalım
touch my_private_file.txt

# Deponun durumunu kontrol edelim
git status

Çıktı Analizi:
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        aftergithub.txt
        my_private_file.txt
Şimdi bu özel dosyayı yoksaymak için .gitignore dosyamızı oluşturalım ve içerisine dosya adını yazalım:
# .gitignore dosyasını oluşturun ve içine dosya adını ekleyin
echo "my_private_file.txt" > .gitignore

# Durumu tekrar kontrol edin
git status
Yeni Çıktı Analizi:
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        aftergithub.txt


Gördüğünüz gibi, my_private_file.txt dosyasını .gitignore içerisine eklediğimiz andan itibaren Git bu dosyayı tamamen görmezden gelmeye başladı. Artık sadece .gitignore dosyasının kendisi ve diğer takip edilmeyen dosyalar listeleniyor.

3. Klasör Düzeyinde Yoksayma ve İstisna Tanımlama (!)
Bazen bir klasörün içerisindeki neredeyse tüm dosyaları yoksaymak, ancak sadece belirli bir veya birkaç dosyayı takip etmek isteyebiliriz. Bunun için ünlem işareti (!) kullanarak kurallara istisna ekleyebiliriz.

Adım 3.1: Özel Bir Klasör ve Dosyalar Oluşturma

# Yeni bir klasör oluşturalım ve içine geçelim
mkdir my_private_folder
cd my_private_folder

# Biri gizli kalacak, diğeri ise herkese açık olacak iki dosya oluşturalım
touch private_file.txt
touch public_file.txt

# Ana dizine geri dönelim
cd ..
Adım 3.2: Gelişmiş Filtreleme Kurallarını Tanımlama
Klasörün içindeki her şeyi yoksayıp, yalnızca public_file.txt dosyasını takip edilir kılmak için .gitignore dosyamızı şu şekilde güncelliyoruz:
my_private_file.txt
my_private_folder/*
!my_private_folder/public_file.txt
Buradaki Mantık:

my_private_folder/* komutu, klasörün altındaki tüm içeriği Git takibinden çıkarır.

!my_private_folder/public_file.txt komutu ise ünlem (!) işareti sayesinde bir önceki yoksayma kuralına istisna getirir ve bu dosyanın Git tarafından takip edilmesini sağlar.

Adım 3.3: Durumu Doğrulama
git status
Çıktı Analizi:
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        aftergithub.txt
        my_private_folder/


Git artık klasörü tamamen yoksaymıyor; içerisindeki istisna olarak belirttiğimiz public_file.txt dosyasından dolayı klasörü takip listesine dahil ediyor.

4. Değişiklikleri Kaydetme ve Uzak Depoya Gönderme (Push)
Yapılandırdığımız kuralları yerel depomuza işleyip ardından GitHub üzerindeki uzak depomuza aktaralım.
# 1. Tüm değişiklikleri hazırlık alanına (Staging Area) ekleyin
git add .

# 2. Değişiklikleri anlamlı bir mesajla commit edin
git commit -m "Chore: Add my_private_folder filter configuration to .gitignore"

# 3. Ana dalın adını 'main' olarak yapılandırın (Eğer daha önce yapılmadıysa)
git branch -M main

# 4. Değişiklikleri uzak depoya (origin) gönderin
git push origin main

İşlem tamamlandıktan sonra tarayıcınızdan GitHub deponuzu ziyaret ettiğinizde, .gitignore kurallarına takılan gizli dosyalarınızın GitHub'a yüklenmediğini, yalnızca izin verdiğiniz dosyaların başarıyla gönderildiğini görebiliriz.
