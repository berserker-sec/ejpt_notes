# **nmap -p445 --script smb-protocols demo.ine.local**

Bu komut, **`demo.ine.local`** adresindeki hedef sunucunun hangi **SMB (Server Message Block) protokol sürümlerini** (SMBv1, SMBv2, SMBv3 vb.) desteklediğini tespit eder.

Parçaların işlevleri:

* **`-p445`:** Yalnızca SMB dosya paylaşım servisinin çalıştığı **445 numaralı TCP portunu** tarar.
* **`--script smb-protocols`:** Nmap'in NSE (Nmap Scripting Engine) altyapısını kullanarak hedef sistemle el sıkışma gerçekleştirir ve etkin olan SMB lehçelerini (dialects) listeler.
* **`demo.ine.local`:** Taranacak hedef sunucunun alan adı veya ana makine adıdır.

Genellikle ağ güvenliği denetimlerinde, zafiyet barındıran eski ve güvensiz **SMBv1** protokolünün açık olup olmadığını hızlıca kontrol etmek için kullanılır.

# **use auxiliary/scanner/smb/smb_login**

Kullanım Alanı: Ağ üzerindeki SMB servislerinde geçerli kimlik bilgilerini, zayıf/varsayılan parolaları veya boş parola ile erişilebilen paylaşımları doğrulamak amacıyla güvenlik denetimlerinde kullanılır.
