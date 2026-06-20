# Kapsamlı Git Komut Kılavuzu ve Terimler Sözlüğü

Bu kılavuz; Git ortamının yapılandırılmasından depo oluşturmaya, değişikliklerin takibinden uzak depo senkronizasyonuna kadar ihtiyaç duyacağınız tüm temel süreçleri ve Git terimlerini içerir.

---

## 1. Araç Yapılandırması (Configure Tooling)

Yerel bilgisayarınızdaki tüm Git depolarında geçerli olacak kullanıcı bilgilerini ve terminal arayüzünü özelleştirin:


# Commit işlemlerinde adınızın görünmesi için küresel isim tanımlar
git config --global user.name "[isim]"

# Commit işlemlerine eklenecek e-posta adresini tanımlar
git config --global user.email "[eposta_adresi]"

# Terminal çıktılarının daha okunaklı olması için otomatik renklendirmeyi açar
git config --global color.ui auto

2. Depo Oluşturma (Create Repositories)
Bir Git projesine sıfırdan yerelde başlayabilir veya GitHub üzerindeki mevcut bir projeyi bilgisayarınıza indirebilirsiniz:
# Bulunduğunuz dizini bir Git deposuna dönüştürür (.git klasörü oluşturur)
git init

# Yerel depoyu GitHub üzerindeki boş bir uzak depoya bağlar
git remote add origin [url]

3. Dallanma Yönetimi (Branches)
Git ile çalışırken yaptığınız her commit, o an aktif olan (üzerinde bulunduğunuz) dala işlenir. Hangi dalda olduğunuzu görmek için git status komutunu kullanabilirsiniz.
# Belirtilen isimde yeni bir dal oluşturur
git branch [dal-adi]

# Belirtilen dala geçiş yapar ve çalışma dizinini günceller
git checkout [dal-adi]

# Belirtilen dalın geçmişini, o an aktif olan mevcut dalınızla birleştirir
git merge [dal]

# Görevi biten yerel dalı siler
git branch -d [dal-adi]


4. Değişiklikleri İzleme ve Kaydetme (Make Changes)
Proje dosyalarınızın gelişimini ve sürümlerini incelemek, değişiklikleri kalıcı hale getirmek için:
# Aktif dalın tüm versiyon geçmişini listeler
git log

# Bir dosyanın (yeniden adlandırılmış olsa bile) tüm geçmişini listeler
git log --follow [dosya]

# İki dal arasındaki içerik farklarını gösterir
git diff [birinci-dal]...[ikinci-dal]

# Belirtilen commit'in metadata ve içerik değişikliklerini detaylıca gösterir
git show [commit-hash]

# Belirtilen dosyayı versiyonlanmaya hazır hale getirmek için hazırlar (Staging Area)
git add [dosya]

# Hazırlık alanındaki dosyaları kalıcı olarak versiyon geçmişine kaydeder (Snapshot)
git commit -m "[açıklayıcı_mesaj]"

5. Dosya Yoksayma (.gitignore)
Bazı dosyaların Git tarafından takip edilmesini engellemek en iyi pratiklerden biridir. Bu işlem proje kök dizininde oluşturulan .gitignore adlı özel bir dosya ile yapılır.

💡 İpucu: Projenizin teknolojisine uygun hazır şablonlara github.com/github/gitignore adresinden ulaşabilirsiniz.

6. Commit'leri Yeniden Düzenleme ve Geri Alma (Redo Commits)
Hataları silmek ve proje geçmişini temiz bir şekilde yeniden şekillendirmek için:

# [commit] sonrasındaki tüm commit'leri iptal eder, değişiklikleri yerelde korur
git reset [commit]

# Belirtilen commit noktasına kadar olan tüm geçmişi ve yerel değişiklikleri tamamen siler
git reset --hard [commit]

⚠️ DİKKAT: Versiyon geçmişini değiştirmek ciddi yan etkilere yol açabilir. Eğer GitHub (uzak depo) üzerinde halihazırda var olan commit'leri değiştirecekseniz çok dikkatli olmalısınız.

7. Değişiklikleri Senkronize Etme (Synchronize Changes)
Yerel deponuz ile GitHub üzerindeki uzak depoyu birbiriyle güncel tutmak için:

# Uzak depodaki tüm geçmişi ve dalları yerel takip listesine indirir (Dosyalarınızı değiştirmez)
git fetch

# Uzak depodan indirilen dal geçmişini aktif olan yerel dalınızla birleştirir
git merge

# Yerel daldaki tüm commit'leri GitHub'a yükler
git push

# Mevcut yerel dalınızı GitHub'daki en güncel commit'lerle günceller (fetch + merge kombinasyonudur)
git pull

8. Git Terimleri Sözlüğü (Glossary)
git: Açık kaynaklı, dağıtık bir versiyon kontrol sistemidir.

GitHub: Git depolarını barındıran ve ekiplerin birlikte çalışmasını sağlayan bir platformdur.

commit: Deponuzun belirli bir andaki durumunun SHA (hash) algoritmasıyla sıkıştırılmış anlık görüntüsüdür (snapshot).

branch (dal): Bir commit'i işaret eden, taşınabilir ve hafif bir göstergedir.

clone: Bir deponun tüm commit ve dallarıyla birlikte yerel bilgisayara indirilmiş kopyasıdır.

remote: Ekip üyelerinin değişiklikleri takas etmek için kullandığı, GitHub üzerinde barındırılan ortak depodur.

fork: Başka bir kullanıcıya ait GitHub deposunun, kendi hesabınıza kopyalanmış sürümüdür.

pull request (PR): Bir daldaki değişikliklerin ana kodla birleştirilmeden önce incelendiği, tartışıldığı ve test edildiği iş akışı alanıdır.

HEAD: Şu anda üzerinde çalıştığınız aktif dizini (mevcut dalı, commit'i veya etiketleri) gösteren işaretçidir.

# GitHub'da var olan bir depoyu (tüm dosya, dal ve geçmişiyle) bilgisayarınıza indirir
git clone [url]
