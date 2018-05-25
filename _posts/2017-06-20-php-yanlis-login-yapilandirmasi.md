---
 layout: post
 title:  "PHP Yanlış Login Yapılandırılması"
 date:   2017-06-20 01:00:45 +0200
 categories: PHP
 image: /resim/cms_admin2.png	
---

PHP dilinde kod yazarken en çok yapılan hatalardan bir tanesidir fakat bununla ilgili internet üzerinde pek döküman bulamazsınız ben bu güvenlik açığının hangi durumlarda ortaya çıktığını ve önlemini anlatacağım.

------
PHP 'de yönetim panelleri girişinde temelde 3 sayfa kullanılır 

 - ayar.php 
 - login.php 
 - index.php

Bu üç sayfa olur
ayar.php içerisinde veritabanı ile bağlantı ve gerekli ayarlar bulunur
login.php içerisinde giriş bilgilerinin alındığı form bulunur
index.php içerisinde yönetim paneli kontrol edilen bilgiler bulunur
Her zaman bu dizilimde olmaz ama bu açığa denk geldiğim tüm sistemlerde dizilim aynı dosya adları farklı olsada okumaya devam ettikçe daha iyi anlayacaksınız
Örnek olarak
![CMS Bug](/resim/cms_admin.png)

URL Kısmına dikkat ederseniz 
**admin/sifre.php** olduğunu göreceksiniz bundan gelin siteyi açarken HTTP Header e bakalım
![CMS Redirect Header](/resim/cms_admin_header.png)

Göründüğü üzere "Location:sifre.php" olarak atanmış bizden bizi sifre.php'ye yönlendiriyor buradan sonra PHP tecrübesi olanlar "hee lan adam şurda şunu kullanmış galiba" demeye başlıyor bizde adamı yazdığı koda yakın sayılacak bir kod yazıyoruz
{% highlight php %}
{% raw %}
if(isset($_SESSION['giriyorum'])){
}
else{
	header("location:sifre.php ");
}

echo "lan ben burda ne arıyorum?";
{% endraw %}
{% endhighlight %} 


yaptığımızda adrese gidersek bizi sifre.php'ye yönlendirir fakat yönlendirmeden kaçarsak 
![CMS Bug](/resim/cms_admin2.png)

Gördüğünüz üzere 
"lan ben burda ne arıyorum" acaba sorusuna cevabı elde ettik ve sistemi kodlayan kişinin hangi mantıkla ilerlediğini anlamaya çalıştık sistemi kodlayan kişi farklı şekilde de bu açığı bırakabilir bu yüzden yapılması gereken tek şey

   
{% highlight php %}
if(isset($_SESSION['giriyorum'])){
}
else{
	header("location:sifre.php ");
	die();
}

echo "lan ben burda ne arıyorum?";
{% endhighlight %} 

{% highlight php %}
die(); 
{% endhighlight %} 

koyarak geri kalan işlemleri sonlandırmak 

![CMS Sonlara doğru](/resim/cms_sonlar.png)

Ve gördüğünüz gibi sorun kalmadı 

Yönlendirme engellemeyi Firefox NoRedirect eklentisi ile yapabilirsiniz 
![NoRedirect](/resim/cms_sonlar2.png)

Siteyi listeye ekledikten sonra artık eklediğimiz sitede hiç bir türlü yönlendirilmeyecek eğer yönlendirilirse bizim inisiyatifimizle olacak 
![CMS Final](/resim/cms.png) 

artık içeriye sızdık artık sitenin kontrol sistemine erişimimiz var!

