Evet öğreniyom. Ne var yani… Bu benim ilk blog yazım o yüzden olumlu yorumlarınızı kendinize saklayın varsa olumsuz yorumlarınız dinlerim. Keyifli okumalar.



1-lab01–01.exe’yi Virustotal’e aktardığımızda 57 farklı antivirus tarafından tespit edildi ve kategori olarak trojan olduğunu görüyoruz


Lab01.01.dll dosyasının çıktısı da şu şekilde


Dosyaların compiled edildiği tarih için detect it easy toolunu kullandım.

exe file

dll.file
3-Bu soru için entropy değerine bakmak gene aynı tool üzerinden advanced tiki aktif edip çıkan “Entropy” sekmesine tıklıyorum. Aynı zamanda bunu kitapta da anlatıldığı üzere raw-size ve virtual size değerlerine de bakarak anlayabiliriz. Bu değerlerin birbirlerine yakın olması herhangi bir packed işleminin olmadığı anlamına gelir.


dll file

exe file
4-Exe ve dll dosyalarını ayrı ayrı incelediğimizde import edilen dll dosyalarının KERNEL32.dll,MSVCRT.dllve WS2_32.dll olduğunu görüyoruz. Peki bu dll dosyaları nedir ve ne işe yarar önce buna bakalım

Kernel32.dll

Amacı: Bu DLL, Windows işletim sisteminin çekirdek fonksiyonlarını içerir. Bellek yönetimi, dosya işlemleri, iş parçacığı yönetimi gibi düşük seviye işlevler için kullanılır.
Malware Kullanımı: Malware, dosya okuma/yazma, bellek manipülasyonu ve süreç yaratma gibi işlemler için kernel32.dll’yi kullanabilir.
Ws2_32.dll

Amacı: Bu DLL, Windows Sockets API’sini sağlar ve ağ bağlantıları ile ilgili işlevler içerir.

Malware Kullanımı: Malware, komuta ve kontrol sunucularıyla iletişim kurmak, ağ üzerinden veri sızdırmak veya zararlı trafiği yönlendirmek için Ws2_32.dll’yi kullanabilir.

MSVCRT.dll

Amacı: C programlama diline ait standart kütüphane işlevlerini sağlar. String işlemleri, bellek yönetimi, dosya giriş/çıkışı gibi temel fonksiyonları içerir.
Malware Kullanımı: Zararlı yazılım, string manipülasyonu, bellek yönetimi ve dosya işlemleri gibi işlemleri gerçekleştirmek için bu DLL’i kullanabilir, ayrıca zararlı aktiviteleri gizlemek için sistemdeki yaygın işlevlerden faydalanabilir.

exe file
CloseHandle

Amacı: Açılmış bir nesne tanıtıcısını (handle) kapatır ve işletim sisteminin bu nesneye tahsis ettiği kaynakları serbest bırakır.
Malware Kullanımı: Kötü amaçlı yazılımlar, kullandıkları dosya veya işlem tanıtıcılarını kapatarak izlerini silebilir ya da kaynakları serbest bırakabilir.
2. UnmapViewOfFile

Amacı: Belleğe eşlenmiş (mapped) bir dosya görünümünü sanal bellekten kaldırır.
Malware Kullanımı: Kötü amaçlı yazılımlar, zararlı bir dosya görüntüsünü bellekten kaldırdıktan sonra kendi işlemlerini gizleyebilir veya başka bir zararlı bileşeni devreye sokabilir. Ayrıca, zararlı işlemlerini tamamladığında sistem kaynaklarını serbest bırakmak için kullanılabilir.
3. IsBadReadPtr

Amacı: Belirtilen bellek bölgesinin geçerli bir okuma bölgesi olup olmadığını kontrol eder.
Malware Kullanımı: Bu fonksiyon, kötü amaçlı yazılımlar tarafından bellek bölgesini kontrol etmek ve herhangi bir hatadan kaçınarak zararlı işlemleri yürütmek için kullanılabilir. Kötü amaçlı yazılım, bellek manipülasyonu yapmadan önce hedef bellek bölgesinin geçerliliğini bu fonksiyonla doğrulayabilir.
4. MapViewOfFile

Amacı: Dosya içeriğini belleğe haritalar (mapped). Bu, dosyanın sanal bellekte yer almasını sağlar.
Malware Kullanımı: Kötü amaçlı yazılımlar, dosyaların bellekteki görüntüsünü almak ve bu belleği değiştirmek ya da kendi zararlı kodlarını belleğe yüklemek için bu fonksiyonu kullanabilir.
5. CreateFileMappingA

Amacı: Dosya verilerini paylaşmak için bir dosya haritalama (file mapping) nesnesi oluşturur.
Malware Kullanımı: Kötü amaçlı yazılımlar, bir dosya haritalama nesnesi oluşturarak bu dosyanın bellekteki görüntüsüne erişim sağlayabilir ve dosya içeriğini manipüle edebilir.
6. CreateFileA

Amacı: Bir dosya veya cihazı açar veya oluşturur.
Malware Kullanımı: Kötü amaçlı yazılımlar, dosyalar üzerinde değişiklik yapmak, zararlı dosyalar oluşturmak veya sistem dosyalarına erişim sağlamak için bu fonksiyonu kullanabilir.
7. FindClose

Amacı: Bir dizin arama tanıtıcısını kapatır (örneğin, FindFirstFile ve FindNextFile ile kullanılan).
Malware Kullanımı: Zararlı yazılımlar, bir dizin taramasını bitirdikten sonra bu tanıtıcıyı kapatarak dosya taramalarını bitirebilir. İlgili dizin tarama sürecini tamamlayarak kaynakları serbest bırakabilir.
8. FindNextFileA

Amacı: Daha önce FindFirstFile tarafından başlatılan dizin arama işleminin bir sonraki dosyasını bulur.
Malware Kullanımı: Kötü amaçlı yazılımlar, belirli dosya türlerini veya zararlı bileşenlerini bulmak için bu fonksiyonu kullanarak dosya sistemini tarayabilir.
9. FindFirstFileA

Amacı: Bir dizin içindeki ilk dosyayı bulur.
Malware Kullanımı: Kötü amaçlı yazılımlar, dosya sistemini taramak ve belirli dosya türlerini (örneğin, sistem dosyaları, güvenlik yazılımları) bulmak için bu fonksiyonu kullanabilir.
10. CopyFileA

Amacı: Bir dosyayı belirtilen konuma kopyalar.
Malware Kullanımı: Kötü amaçlı yazılımlar, zararlı dosyalarını başka yerlere yaymak veya sistemdeki önemli dosyaları yedekleyerek değiştirmek için bu fonksiyonu kullanabilir.

dll file
1.Sleep

Amacı: Programın çalışmasını belirli bir süre (milisaniye cinsinden) duraklatır.
Zararlı Yazılım Kullanımı: Zararlı yazılımlar bu fonksiyonu, analiz araçlarından kaçınmak için çalışmasını geciktirmek veya işlemler arasında zaman boşlukları oluşturarak izlenmesini zorlaştırmak amacıyla kullanabilir.
2. CreateProcessA

Amacı: Yeni bir süreç veya program başlatır.
Zararlı Yazılım Kullanımı: Zararlı yazılımlar, yeni zararlı süreçler başlatmak veya dış programları çalıştırmak için bu fonksiyonu kullanabilir. Bu genellikle çok aşamalı saldırıların bir parçası olabilir ya da zararlı yükleri (payload) çalıştırmak için kullanılabilir.
3. CreateMutexA

Amacı: Programın birden fazla örneğinin aynı anda çalışmasını engellemek için bir mutex (karşılıklı dışlama nesnesi) oluşturur.
Zararlı Yazılım Kullanımı: Zararlı yazılımlar genellikle yalnızca bir örneğinin çalıştığından emin olmak için mutex kullanır. Eğer mutex zaten varsa, zararlı yazılım fazladan çalışmayı önlemek için kendini sonlandırabilir.
4. OpenMutexA

Amacı: Mevcut bir mutex nesnesini açar, böylece program mutex’in zaten var olup olmadığını kontrol edebilir.
Zararlı Yazılım Kullanımı: Zararlı yazılım, sistemde aynı zararlı yazılımın başka bir örneği çalışıyorsa, mutex’i açarak kontrol edebilir. Eğer mutex bulunursa, zararlı yazılımın zaten aktif olduğunu anlar ve kendini sonlandırarak fazladan işlem yapmaktan kaçınır.
5. Soru için exe dosyasının string ifadelerine bakıyoruz. Gözümüze kernel132.dll takılıyor.


exe file
6. Soru için dll dosyasını inceliyorum çünkü ws2_32.dll’i kullandığını o yüzden bir IP veya bir domain bulmayı umuyorum. Strings içerisinde 127[.]26[.]152[.]13 IP adresini buluyoruz.


7. soru bir yorumlama sorusu aslında burda benim yorumum exe dosyasının çalışmasıyla lab01–01.dll dosyasını bulduktan sonra windows/system32 dosyasının içine kerne123.dll olarak yerleştiriyor. Dll dosyası ise bir backdoor olarak işe yaramakta.
