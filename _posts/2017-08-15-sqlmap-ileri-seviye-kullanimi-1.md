---
 layout: post
 title:  "SQLMap Üst Düzey Kullanımı 1"
 date:   2017-08-15 10:06:45 +0200
 categories: Hack
 image: /resim/sqlmap1.jpg	
---
SQLmap nedir diye soracak olursanız SQL Injection açığı barındıran sistemlerde açıkları test etmek için geliştirilmiş bir yazılım

[http://ferruh.mavituna.com/sql-injection-a-giris-ve-sql-injection-nedir-oku/](http://ferruh.mavituna.com/sql-injection-a-giris-ve-sql-injection-nedir-oku/)

[enter link description here](https://www.merdincz.com/Sqlmap-kullanimi/)
Şu iki bağlantıya bakarak daha iyi anlayabilirsiniz(ben alayını okumadım)

SQLMap kullanımında açık bulunan sayfanın bağlı olduğu kullanıcı,veritabanı izinlerine göre sınırları zorlamak mümkündür yani sqlmap ile root şifresi veya sistem dosyalarını okumak mümkün olur 

genel kullanımı çok basittir 

![SQLMap Kullanımı](https://blog.kanunsuzlar.com/resim/sqlmap1.jpg)

ilk olarak 
1) -u 

	Açık bulunan websitesini bu parametreden sonra koyuyoruz burada tırnak içine almamızın sebebi "&" tarzı işaretlerin araya kaçmaması
	
2) --random-agent
	
	Siteye bir tarayıcıymış gibi istek atarak olası bi engellemeyi aşmak burayı random getirir fakat random yazdığımız için rastgele bir tarayıcı kimliği kullanacaktır özel olarak bi tarayıcı kimliği kullanacaksanız --user-agent parametresini kullanmalısınız
 
 3) --dbs
	
	Veritabanlarını listelememize yarayan komut bize bu komuttan sonra veritabanı isimlerini çıkartacak ve bizde parametrelerle seçtiğimiz veritabanının tablolarını göreceğiz

![SQLMap Kullanımı 2](https://blog.kanunsuzlar.com/resim/sqlmap2.jpg)

![SQLMap Kullanımı 3](https://blog.kanunsuzlar.com/resim/sqlmap3.jpg)

4) -D
	
	Veritabanını seçmemize yarar 

5) --tables

	Seçtiğimiz veritabanın da bulunan tabloları listeleriz
	
![SQLMap Kullanımı 4](https://blog.kanunsuzlar.com/resim/sqlmap4.jpg)

![SQLMap Kullanımı 5](https://blog.kanunsuzlar.com/resim/sqlmap5.jpg)

6) -T 
	
	Seçtiğimiz veritabanı üzerinden tablo seçmemize yardımcı olan parametre

7) --columns
	
	Seçilen tablonun tüm kolonlarını görmemizi sağlar
	
![SQLMap Kullanımı 6](https://blog.kanunsuzlar.com/resim/sqlmap6.jpg)

![SQLMap Kullanımı 7](https://blog.kanunsuzlar.com/resim/sqlmap7.jpg)

8) -C 
	
	Çıkarttığımız kolonlar arasında hedef kolonları seçmemize yarar

9) --dump 
	
	Seçtiğimiz veritabanı,tablo,kolonu indirmemize yarıyor
	
Buraya kadar GET olan ile gittik bir de POST ile SQL Injection var onun için ise 

10) --data
	
	Post işlemleri için kullanılır kullanımı
	data="veri"
Basit kullanımı buraya kadardı şimdi biraz daha ileri seviye denemeler yapacağız 
ilk olarak hangi veritabanına bağlı olduğumuzu ve o veritabanına hangi kullanıcı ile bağlandığımızı öğrenmeliyiz bunun için kullanacağımız komutlar 

![SQLMap Current User, Current Db ](https://blog.kanunsuzlar.com/resim/sqlmap8.jpg)
	
	--current-user 
	--current-db
Sorgulamayı yaptığımız zaman bize bağlı olduğumuz veritabanını ve kullancıyı verecek 

![SQLMap Kullanıcı ve Veritabanı](https://blog.kanunsuzlar.com/resim/sqlmap9.jpg)

daha sonra kullanıcının yetkilerini sorgulamalıyız neleri görmeye neleri yazmaya izni var öğrendikten sonra işlemlerimize buna göre devam etmeliyiz 

![SQLMap Kullancı İzinleri Sorgulama](https://blog.kanunsuzlar.com/resim/sqlmap10.jpg)

![SQLMap Kullanıcı İzinleri](https://blog.kanunsuzlar.com/resim/sqlmap11.jpg)

Geçerli kullanıcının izinlerinde dosyaları okumamıza yarayacak olan yetkiyi görüyoruz şimdi direk /etc/passwd dosyasını çektirelim bundan önce ufak bir bilgi daha vereyim eğer yaptığınız testlerde sqlmap'in kullandığı payloadları anlık olarak görmek istiyorsanız veya istekleri takip etmek istiyorsanız 
-v3 
-v4
-v5
-v6
kullanabilirsiniz 

![SQLMap Kullanımı ](https://blog.kanunsuzlar.com/resim/sqlmap12.jpg)

Dosya okumak için kullanacığımız komut

	--file-read
	
![SQLMap Kullanımı](https://blog.kanunsuzlar.com/resim/sqlmap13.jpg)
Komutumuzu girdikten sonra çıkan sorulara default yanıtını vererek dosyamızı indiriyoruz daha sonra cat komutu ile dosyayı görüyoruz

![/etc/passwd görek birazda](https://blog.kanunsuzlar.com/resim/sqlmap14.jpg)

Ve /etc/passwd dosyasını çekmeyi başarabildik şimdi ise v5 parametresi ile çıkan payloadı decode edelim
	
	id=-6272%27%20UNION%20ALL%20SELECT%20CONCAT%280x71706b6b71%2CIFNULL%28CAST%28LENGTH%28LOAD_FILE%280x2f6574632f706173737764%29%29%20AS%20CHAR%29%2C0x20%29%2C0x716b6a6271%29--%20fsiM&type=dislike

![url decoder](https://i.hizliresim.com/Prbqd9.png)

LOAD_FILE kısmında /etc/passwd görmemeiz normal 
0x2f6574632f706173737764 -> /etc/passwd 
anlamına gelir

Bir sonra olacak olan yazıda eğer açığı bildirdiğim firmadan izinleri alırsam efsane bi yere sızma girişimimi sansürsüzcene anlatıcam
