# **enum4linux -a target.ine.local
İşlevi: Kapsamlı bir numaralandırma (enumeration) taraması başlatır (-a bayrağı "all" anlamına gelir).

Ne Yapar: İşletim sistemi tespiti, çalışma grubu/etki alanı bilgileri, kullanıcı hesapları, kullanıcı grupları, SMB paylaşımları, şifre politikaları ve SID dökümü gibi sistemin dışarıya sızdırdığı neredeyse tüm bilgileri tek seferde toplamaya çalışır.

# **enum4linux target.ine.local -N
İşlevi: N bayrağı ile hedefe yönelik NetBIOS ad çözümlemesi ve sorgulaması (nmblookup) yapar.

Ne Yapar: Hedef makinenin NetBIOS adını, ait olduğu çalışma grubunu (Workgroup) ve ağ üzerindeki rollerini sorgulayarak doğrular.

# **enum4linux -s /root/Desktop/wordlists/shares.txt target.ine.local
İşlevi: Paylaşım ismi kaba kuvveti (share brute-forcing) uygular (-s parametresi "share list" belirtir).

Ne Yapar: shares.txt dosyasındaki her bir kelimeyi olası bir paylaşım adı olarak dener. browseable = no ayarlandığı için normal paylaşım listesinde görünmeyen gizli paylaşımların (örneğin listeden tespit ettiğiniz pubfiles) var olup olmadığını ortaya çıkarır.

# **smbclient target.ine.local/pubfiles -u ""
İşlevi: Boş/anonim bir kullanıcı adı (-u "") ile pubfiles paylaşımına bağlanmaya çalışır.

Sözdizimi Durumu: Linux ortamında smbclient ile hedef belirtirken genellikle çift eğik çizgi (//target.ine.local/pubfiles) standardı kullanılır; ancak parametre olarak -u "" geçilmesi oturumu anonim kimlikle başlatma niyetini sunucuya bildirir.

# **smbclient //target.ine.local/pubfiles

İşlevi: Belirtilen pubfiles paylaşımına etkileşimli bir SMB oturumu başlatır.

Ne Yapar: UNC yol biçimini (//sunucu/paylasim) doğru şekilde kullanır. Kullanıcı adı veya parola bayrağı verilmediğinde istemci sizden bir parola girmenizi ister; sunucuda anonim/guest erişim açıksa Enter'a basıp geçerek doğrudan smb: \> komut satırına erişebilirsiniz.

