---
 layout: post
 title:  "PHP Yanlış Login Yapılandırılması"
 date:   2017-06-20 01:00:45 +0200
 categories: PHP
 image: /resim/cms_admin2.png	
---

<h1 id="php-fonksiyon-ismini-şifrelemek">Php Fonksiyon ismini şifrelemek</h1>
<p>Şifreleme nedir? Yaptığımız işlerde veya hayatımızda nasıl bir önemi vardır? Hep görürüz televizyonda suçlular dinlemelere takılmamak için elmaya armut der. Aslında verdiğim örnekten yola çıkarsak  ifade edeceğimiz şeyi hem biz hemde karşı tarafın anlaması lazım. Bu yol ile amacımızı gizlemiş ve gizlilik alanımızı başarıyla oluşturmuş oluyoruz. Fakat bu gizlilik deşifre olabilir. Konumuza gelelim şimdi PHP’deki genelde <s>yasaklı</s> bazı fonksiyonları biliriz. Eğer bilmiyorsak size şöyle örnek vereyim <code>exec</code> komutu tam bir baş belası haline gelebiliyor eğer ki sunucunuza bir takım iyi veya kötü kişiler erişim sağladıysa.</p>
<p>Genelde bu fonksiyonu içeren kısımları engelleyen yazılımlar var. Bir php dosyasına bir ekleme yapacağız fakat bunu karşı tarafa hissettirmeden yapmamız gerekiyor. Öyle ise şu yolları deneyebiliriz;<br>
Bir Array oluşturup buna fonksiyonumuzun her harfini ekleyelim.</p>
<pre><code>$a = array('x','e','c');
</code></pre>
<p>Peki biz ne yaptık aslında ne yapacağız. PHP’de fonksiyonu bir değişkene atayabiliyoruz,örnek;<br>
<code>exec('whoami')</code> bunu komutu ben değişkenle vermek istiyorsam bunu bana mümkün kılıyor PHP , yukarıda oluşturduğumuz Array’ı kullanalım.</p>
<pre><code> $str=$a[1].$a[0].$a[1].$a[2];
</code></pre>
<p>Yav sen oralaya bir şeyler yazdın ama biz bunu anlamadık der gibisiniz. İş size başta bahsettiğim gibi şifrelemede olay hem bizim hemde karşı tarafın anlaması burada olayı PHP’ye bırakıyoruz.Değişkenimize şunları atamış olduk bu işlemi yaparak. <code>$a[1]-&gt;e , $a[2]-&gt;x , $a[1]-&gt; e , $a[2]-&gt; c</code> şimdi kaba kodu bir silelim bakalım değişkenimize ne atanmış.<code>exec</code> değerini değişkenimize başarılı bir şekilde atamış olduk. Şimdi ise onu kullanma vakti geldi.<br>
<code>echo $str('whoami');</code><br>
Çıktı :<br>
<code>testpc\testuser</code><br>
Aslında farklı teknikler ile bu yapıyı genişleyebilirsiniz.Örnek vereyim <code>str_replace</code> kullanarak da aynı sonuç alabiliriz.</p>
<pre><code> $cmd=str_replace("u", "", "ueuxueucu");
 echo $cmd('whoami')
</code></pre>
<p>çıktısı yine aynı olacaktır.<br>
Bir seferki konuda görüşmek üzere sağlıcakla Kalın!</p>

