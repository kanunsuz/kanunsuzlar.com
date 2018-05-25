---
layout: post
title: PHP Fonksiyon Şifreleme
author: Yusuf GENÇ
---
# Php Fonksiyon ismini şifrelemek
Şifreleme nedir? Yaptığımız işlerde veya  hayatımızda nasıl bir önemi vardır?
Hep görürüz televizyonda suçlular dinlemelere takılmamak için Elmaya armut der. Aslında verdiğim örnekten yola çıkar isek ifade edeceğimiz şeyi hem biz hemde karşı tarafın anlaması lazım. Bu yol ile amacımızı gizlemiş ve gizlilik alanımızı başarıyla oluşturmuş oluyoruz. Fakat bu gizlilik deşifre olabilir. Konumuza gelelim şimdi PHP'deki genelde ~~yasaklı~~ bazı fonksiyonları biliriz. Eğer bilmiyor isek söyle size şöyle örnek vereyim `exec` komutu tam bir baş belası haline gelebiliyor eğer ki sunucunuza bir takım iyi veya kötü kişiler erişim sağladıysa.
 
Genelde bu fonksiyonu içeren kısımları engelleyen yazılımlar var. Bir php dosyasına bir ekleme yapacağız  fakat bunu karşı tarafa hissettirmeden yapmamız gerekiyor. Öyle ise şu yolları deneyebiliriz.Bir Array oluşturup buna fonksiyonumuzun her harfini ekleyelim.

    $a = array('x','e','c');

 Peki biz ne yaptık aslında ne yapacağız. PHP'de fonksiyonu bir değişkene atayabiliyoruz .Örnek `exec('whoami')` bunu komutu ben değişkenle vermek istiyor isem bunu bana mümkün kılıyor PHP , yukarıda oluşturduğumuz Array'ı kullanalım.
 

    $str=$a[1].$a[0].$a[1].$a[2];
Yav sen oralaya bir şeyler yazdın ama biz bunu anlamadık der gibisiniz.
İş size başta bahsettiğim gibi  şifrelemede olay hem bizim hemde karşı tarafın anlaması burada olayı PHP'ye bırakıyoruz.Değişkenimize şunları atamış olduk bu işlemi yaparak. `$a[1]->e , $a[2]->x , $a[1]-> e , $a[2]-> c'` şimdi kaba kodu bir silelim bakalım değişkenimize ne atanmış.`exec` değerini değişkenimize başarılı bir şekilde atamış olduk. Şimdi ise onu kullanma vakti geldi.
`echo $str('whoami');`
Çıktı :
`testpc\testuser`
Aslında farklı teknikler ile bu yapıyı genişleyebilirsiniz.Örnek vereyim `str_replace` kullanarakda aynı sonuç alabiliriz.

    $cmd=str_replace("u", "", "ueuxueucu");
    echo $cmd('whoami');
çıktısı yine aynı olacaktır. 

Bir seferki konuda görüşmek üzere sağlıcakla Kalın!
 

