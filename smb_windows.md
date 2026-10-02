# **nmap -p445 --script smb-protocols demo.ine.local**

Bu komut, **`demo.ine.local`** adresindeki hedef sunucunun hangi **SMB (Server Message Block) protokol sürümlerini** (SMBv1, SMBv2, SMBv3 vb.) desteklediğini tespit eder.

Parçaların işlevleri:

* **`-p445`:** Yalnızca SMB dosya paylaşım servisinin çalıştığı **445 numaralı TCP portunu** tarar.
* **`--script smb-protocols`:** Nmap'in NSE (Nmap Scripting Engine) altyapısını kullanarak hedef sistemle el sıkışma gerçekleştirir ve etkin olan SMB lehçelerini (dialects) listeler.
* **`demo.ine.local`:** Taranacak hedef sunucunun alan adı veya ana makine adıdır.

Genellikle ağ güvenliği denetimlerinde, zafiyet barındıran eski ve güvensiz **SMBv1** protokolünün açık olup olmadığını hızlıca kontrol etmek için kullanılır.

# **use auxiliary/scanner/smb/smb_login**

Kullanım Alanı: Ağ üzerindeki SMB servislerinde geçerli kimlik bilgilerini, zayıf/varsayılan parolaları veya boş parola ile erişilebilen paylaşımları doğrulamak amacıyla güvenlik denetimlerinde kullanılır.

# **use exploit/windows/smb/psexec**

Bu komut, Metasploit Framework içerisinde yer alan ve Sysinternals PsExec aracının çalışma mantığını taklit eden exploit/windows/smb/psexec modülünü seçer.

Modülün Amacı ve Çalışma Mekanizması
Bu modül, geçerli yerel veya etki alanı (domain) yönetici kimlik bilgilerine sahip olunduğunda hedef Windows sistem üzerinde uzaktan komut çalıştırmak veya oturum (örneğin Meterpreter) açmak için kullanılır. Klasik bir yazılım açığı (exploit) sömürmek yerine, Windows'un meşru yönetim özelliklerini kötüye kullanır:

SMB Erişimi: Sağlanan kimlik bilgileriyle hedef sistemin SMB servisine (TCP 445) bağlanır.

Dosya Yükleme: Varsayılan olarak yönetimsel gizli paylaşıma (ADMIN$ veya C$) rastgele isimli bir çalıştırılabilir servis dosyası (payload) yükler.

Servis Oluşturma ve Başlatma: Windows Service Control Manager (SCM - RPC üzerinden) ile iletişim kurarak yüklenen bu dosyayı bir Windows servisi olarak kaydeder ve başlatır.

Temizlik: Servis çalışıp oturum sağlandıktan sonra genellikle oluşturulan servis ve yüklenen dosya sistemden silinir.
