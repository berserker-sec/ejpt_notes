# **nmap demo.ine.local**

Bu komut, demo.ine.local adresindeki hedef sunucunun veya cihazın ağ üzerindeki durumunu inceleyen temel bir port taraması (port scan) başlatır.

Ne Yapar?
DNS Çözümlemesi: demo.ine.local alan adını yerel ağda (veya /etc/hosts dosyasında) karşılık gelen IP adresine çevirir.

Erişilebilirlik Kontrolü (Host Discovery): Hedef makinenin açık ve hatta olup olmadığını kontrol etmek için ping (veya TCP SYN/ACK paketleri) gönderir.

Port Taraması: Varsayılan olarak en yaygın kullanılan en popüler 1000 TCP portunu sorgular.

Durum Raporu: Bu portların durumunu listeler:

# **nmap --script http-enum -sV -p 80 demo.ine.local**

Bu komut, demo.ine.local hedefinin 80 numaralı portundaki (HTTP) web servisini ve gizli içeriklerini hedefler.

Kısaca bileşenleri ve yaptığı iş:

-p 80: Taramayı yalnızca 80 numaralı portla sınırlar.

-sV: 80 portunda çalışan web sunucusunun adını ve tam sürümünü (örneğin Apache 2.4.41, nginx 1.18.0) tespit eder.

--script http-enum: Nmap'in NSE betiğini çalıştırarak web sunucusunda yaygın olarak bulunan gizli/önemli dizinleri, dosyaları ve yönetim panellerini (örneğin /admin, /login, /phpmyadmin, /uploads, CMS kurulumları) otomatik olarak tarar ve listeler.

# **davtest -url http://demo.ine.local/webdav**

Bu komut, hedef web sunucusundaki WebDAV (Web Distributed Authoring and Versioning) hizmetinin yapılandırmasını ve izinlerini test eden bir araç komutudur.

Kısaca bileşenleri ve yaptığı işlem:

davtest: WebDAV etkin sunucularda yazma, taşıma ve çalıştırma izinlerini otomatik olarak denetleyen bir güvenlik test aracıdır.

-url [http://demo.ine.local/webdav](http://demo.ine.local/webdav): Testin gerçekleştirileceği hedef WebDAV dizinini belirtir.

Ne Yapar?
Dizin ve Dosya Oluşturma: Belirtilen URL'de yeni bir test dizini oluşturmayı ve içine farklı uzantılara sahip (örneğin .txt, .html, .php, .asp, .cgi vb.) dosyalar yüklemeyi (PUT metodu ile) dener.

Çalıştırma İzinleri: Yüklediği dosyaların sunucu tarafında çalıştırılabilir (executable) olup olmadığını kontrol eder.

Temizleme: Test amacıyla yüklediği geçici dosyaları silmeyi (DELETE metodu) dener.

Sonuç Raporu: Hangi dosya uzantılarının başarıyla yüklenebildiğini ve hangilerinin çalıştırılabildiğini gösteren bir özet tablosu sunar.

# **davtest -auth bob:password_123321 -url http://demo.ine.local/webdav**

Bu komut, bir önceki adımdaki WebDAV testinin kimlik doğrulama (authentication) bilgileri kullanılarak gerçekleştirilmesini sağlar.

Kısaca bileşenleri ve yaptığı iş:

-auth bob:password_123321: Hedef WebDAV dizini parola korumalı (HTTP Basic Authentication vb.) olduğunda, sunucuya kullanıcı adı (bob) ve parola (password_123321) ile giriş yapılmasını sağlar.

-url [http://demo.ine.local/webdav](http://demo.ine.local/webdav): Testin yapılacağı hedef adresi belirtir.

Ne Yapar?
Hedeflenen WebDAV dizinine doğrudan (anonim) erişim kapalıysa veya yetki gerektiriyorsa, belirtilen kimlik bilgileriyle oturum açarak:

bob kullanıcısının dizin üzerinde dosya oluşturma (PUT), silme (DELETE) veya dizin açma (MKCOL) izinlerinin bulunup bulunmadığını test eder.

Farklı uzantılardaki (örneğin .txt, .php, .html) dosyaların bu kullanıcı yetkileriyle sunucuya yüklenip çalıştırılamadığını denetler.

Özetle: Parola korumalı WebDAV alanında, belirtilen kullanıcının dosya yükleme ve çalıştırma izinlerini test eder.

# **cadaver http://demo.ine.local/webdav**

cadaver [http://demo.ine.local/webdav](http://demo.ine.local/webdav) komutu, hedef adresteki WebDAV sunucusuna bağlanmak için kullanılan komut satırı tabanlı etkileşimli bir WebDAV istemcisini (client) başlatır.

Tıpkı klasik bir FTP istemcisi gibi çalışır; komutu çalıştırdığınızda (gerekirse kullanıcı adı/parola sorup) size özel bir kabuk (dav:!>) açar.

Ne Yapar ve İçeride Hangi Komutlar Kullanılır?
Bağlantı kurulduktan sonra tıpkı yerel terminalde veya FTP'de gezinir gibi şu işlemleri yapmanıza imkan tanır:

Dosya Yükleme: Sunucuya dosya yüklemek için put <dosya_adi> (örneğin bir webshell yüklemek için kullanılır).

Dosya İndirme: Sunucudan dosya çekmek için get <dosya_adi>.

Dizin ve Dosyaları Listeleme: Uzak sunucudaki içerikleri görmek için ls.

Klasör Oluşturma / Silme: mkdir <klasor> ile dizin açma, delete <dosya> ile silme.

Çıkış: Oturumu sonlandırmak için exit veya quit.
