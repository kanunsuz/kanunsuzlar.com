---
image: resim/metakapak.jpg
---

Google,Facebook,Twitter gibi büyük sistemler üzerinde kendi sitemizden içerik yayınladığımız zamanlarda paylaşımlarda resimler gözükür mesela ben facebook üzerinde neşet ertaşın bir şarkısını paylaştığımda kapağında bir resim gözükür daha sonra alt kısımda açıklama olur işte bunları sayfada bulunan tagler sağlar 
[https://www.youtube.com/watch?v=x2C3sk8kNe4](https://www.youtube.com/watch?v=x2C3sk8kNe4)
url de CTRL+U ile kaynak koduna bakıp CTRL+F ile **og:** olarak aratırsanız OpenGraph tag'leri ile karşılaşacaksınız 
![jekyll meta tag](https://blog.kanunsuzlar.com/resim/tag1.png)
![jekyll meta tag](https://blog.kanunsuzlar.com/resim/metatag.png)

**site_name** => **Sitenin adı**

**url** => **Adı üzerinde URL**

**title** => **Başlığı**

**image** => **Gözükecek olan resmin adresi**


tabi daha fazla tag var fakat biz temelleri ele alacağız
{% highlight html %}
{% raw %}
<meta name="description" content="{% if page.excerpt %}{{ page.excerpt | strip_html | strip_newlines | truncate: 160 }}{% else %}{{ site.description }}{% endif %}">
<meta property="og:locale" content="tr_TR">
<meta property="og:type" content="article">
<meta property="og:title" content="{%if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}">
<meta property="og:url" content="{{ site.url }}{{ page.url }}">
<meta property="og:image" content="{% if page.image %}{{ site.url }}/{{ page.image }}{% else %}https://kanunsuzlar.com/m.jpg{% endif %}" />
<meta property="og:site_name" content="Kanunsuz Blog">
<meta property="article:published_time" content="{{ page.date }}" />
<meta property="og:description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
{% endraw %}
{% endhighlight %} 

Şimdi size belki karışık gözüken şu kodların açıklamasını yapalım
Örnek olarak
{% highlight html %}

{% raw %}
<meta property="og:title" content="{%if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}">
{% endraw %}
{% endhighlight %}


Bu kısımda görünen if eğer daha önceden programlama ile uğraşanlar olduysa bu alanda nasıl kullanıldığını biliyordur if ile eğer page.title yani yazıda başlık varsa onu og:title olarak kullandırtıyoruz eğer yoksa else ile sitenin normal başlığı kullanılıyor siz page.title,site.title bunları dert etmeyin bunlar tanımlanmış şeylerdir 

Bir örnek daha verdiğim zaman mantığı kavrayacağınıza inanıyorum 
{% highlight html %}

{% raw %}
<meta property="og:image" content="{% if page.image %}{{ site.url }}/{{ page.image }}{% else %}https://kanunsuzlar.com/m.jpg{% endif %}" />
{% endraw %}
{% endhighlight %}

Bu kısımda aynı şekilde az önce bahsettiğim gibi if ve else kullandık dedik ki eğer yazı içerisinde page.image varsa og:image olarak onu kullanıyoruz bu sayede paylaşım yaptığımız sırada yazımızla alakalı görsel ortaya çıkıyor eğer yoksa default bir görsel kullanarak onu gösteriyoruz 
fakat siz ben bunlara vakit ayıramam diyorsanız kısa zaman içinde jekyll ile bu işi otomatik halledebileceğiniz bir yazılım yapacağım.

Tagler sadece bu anlattıklarımdan ibaret değildir işte benim kullandığım taglerin bazıları
{% highlight html %}
{% raw %}
<meta name="description" content="{% if page.excerpt %}{{ page.excerpt | strip_html | strip_newlines | truncate: 160 }}{% else %}{{ site.description }}{% endif %}">
    <meta property="og:locale" content="tr_TR">
    <meta property="og:type" content="article">
    <meta property="og:title" content="{%if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}">
    <meta property="og:url" content="{{ site.url }}{{ page.url }}">
    <meta property="og:image" content="{% if page.image %}{{ site.url }}/{{ page.image }}{% else %}https://kanunsuzlar.com/m.jpg{% endif %}" />
    <meta property="og:site_name" content="Kanunsuz Blog">
    <meta property="article:published_time" content="{{ page.date }}" />
    <meta property="og:description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
      <meta name="twitter:card" content="summary_large_image"/>
    <meta name="twitter:title" content="{%if page.title %}{{ page.title }}{% else %}{{ site.title }}{% endif %}">
    <meta name="twitter:description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
    <meta name="twitter:site" content="@kanun_suz" />
    <meta name="twitter:creator" content="@kanun_suz">
    <meta name="twitter:card" content="summary">

{% endraw %}
{% endhighlight %}

Sağlıcakla kalın!


