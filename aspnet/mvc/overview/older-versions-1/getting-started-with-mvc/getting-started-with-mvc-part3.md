---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: Görünüm ekleme | Microsoft Docs
author: shanselman
description: Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturun.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581559"
---
# <a name="adding-a-view"></a>Görünüm Ekleme

[Scott Hanselman](https://github.com/shanselman) tarafından

> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

Bu bölümde, bir istemciye geri HTML yanıtları oluşturmayı düzgün bir şekilde saklamak için Merhaba Dünya denetleyicisi sınıfımız nasıl bir görünüm şablonu dosyası kullandığımıza bakacağız.

Dizin yönteminizin bulunduğu bir görünüm şablonu kullanarak başlayalım. Yöntemizin dizin olarak adlandırılır ve Merhaba Dünya denetleyicide yer alabilir. Şu anda dizinimiz () yöntemi, denetleyici sınıfı içinde sabit kodlanmış bir ileti içeren bir dize döndürür.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

Şimdi Dizin yöntemini şöyle değiştirelim:

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

Şimdi, projemizi dizin () yöntemi için kullanabilmemiz için bir görünüm şablonu ekleyelim. Bunu yapmak için, Dizin yönteminin ortasında bir yerde bulunan fareyle sağ tıklayın ve Görünüm Ekle... öğesine tıklayın.

![görüntü](getting-started-with-mvc-part3/_static/image1.png)

Bu işlem, Dizin yönteminiz tarafından kullanılabilecek bir görünüm şablonu oluşturmak istediğimizden ilgili bazı seçenekler sunan "Görünüm Ekle" iletişim kutusunu getirir. Şimdilik hiçbir şeyi değiştirmeyin ve Ekle düğmesine tıklamanız yeterlidir.

[![Görünüm Ekle Iletişim kutusu](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

Ekle ' ye tıkladıktan sonra, burada görüldüğü gibi yeni bir klasör ve çözüm klasöründe yeni bir dosya görüntülenir. Artık görünümler altında bir HelloWorld klasörü ve bu klasörün içindeki Index. aspx dosyası var.

[![solutionexplorerwithındex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

Yeni Dizin dosyası zaten açık ve düzenlenebilir hale gelmiştir. İlk &lt;H2&gt;Dizin&lt;/H2&gt; "Merhaba Dünya" gibi bir metin ekleyin.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

Uygulamanızı çalıştırın ve tarayıcınızda [`http://localhost:xx/HelloWorld`](http://localhostxx) yeniden ziyaret edin. Denetleyicimizin bu örnekteki Dizin yöntemi herhangi bir iş gerçekleştirmedi, ancak istemciye geri yanıt işlemek için bir görünüm şablonu dosyası kullanmak istediğimizi belirten "Return View ()" çağrısını gerçekleştirdik. Kullanılacak görünüm şablonu dosyasının adını açıkça belirttiğimiz için, ASP.NET MVC, \Views\HelloWorld klasörü içinde Index. aspx görünüm dosyasını kullanmaya göre varsayılan olarak belirttik. Şimdi görünümümüzde sabit olarak koddığımız dizeyi görebiliriz.

[![dizini-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

Oldukça iyi bir şekilde görünür. Ancak, tarayıcının başlığının "Dizin" olduğunu ve sayfadaki büyük başlığı "MVC Uygulamam" diyor olduğuna dikkat edin. Bunları değiştirelim.

### <a name="changing-views-and-master-pages"></a>Görünümleri ve ana sayfaları değiştirme

İlk olarak, "MVC Uygulamam" metnini değiştirelim. Bu metin paylaşılır ve her sayfada görünür. Bu, uygulamamızda her sayfada olsa da, kodumuza yalnızca bir yerde görünür. Çözüm Gezgini/Views/Shared klasörüne gidin ve site. Master dosyasını açın. Bu dosya, ana sayfa olarak adlandırılır ve tüm diğer sayfalarımızın kullandığı paylaşılan "Shell" dir.

Bu dosyada ContentPlaceholder "MainContent" yazılı bir metin görürsünüz.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

Bu yer tutucu, oluşturduğunuz tüm sayfaların ana sayfada "sarmalanmış" olacağı yerdir. Başlığı değiştirmeyi deneyin, sonra uygulamanızı çalıştırın ve birden çok sayfayı ziyaret edin. Tek bir değişikliğin birden çok sayfada göründüğünü fark edeceksiniz.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

Artık her sayfada birincil başlık-bu, "MVC film Uygulamam" dir. Bu, üstteki beyaz metni tüm sayfalarda paylaşıldığından işler.

Burada site. Master, değişen başlıkla tamamen verilmiştir:

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

Şimdi dizin sayfasının başlığını değiştirelim.

Open /HelloWorld/Index.aspx. Değişen iki yer vardır. İlk olarak, tarayıcının başlığında görünen başlık, sonra da ikincil üst bilgi-bu H2 ' dir. Her birini biraz farklı hale getireceğim ve bu sayede, uygulamanın bir kısmını hangi kod değişikliğini görebileceksiniz.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

Uygulamanızı çalıştırın ve/movies. ziyaret edin Tarayıcı başlığı, birincil başlık ve ikincil başlıkların değiştirildiğini unutmayın. Görünümünüzde küçük değişikliklerle uygulamanızda büyük değişiklikler yapmak kolaydır.

[![film listesi-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

"Data" (Bu durumda "Merhaba Dünya!") çok az. ileti), ancak sabit olarak kodlanmıştır. V (views) ve C (Controller) aldık, ancak henüz M (model) yoktu. Kısa süre içinde veritabanı oluşturma ve model verilerini alma işlemlerinin nasıl yapılacağını adım adım inceleyeceğiz.

## <a name="passing-a-viewmodel"></a>ViewModel geçirme

Bir veritabanına gittiğimiz ve modeller hakkında konuşmadan önce, önce "Viewmodeller" ile konuşalım. Bunlar, bir görünüm şablonunun bir istemciye geri HTML yanıtı işlemek için ne gerektirdiğini temsil eden nesnelerdir. Genellikle bir denetleyici sınıfı tarafından bir görünüm şablonuna oluşturulup geçirilir ve yalnızca görünüm şablonunun gerektirdiği ve daha fazla olmayan verileri içermelidir.

Daha önce HelloWorld örneğimizde, Welcome () eylemi yöntemi bir ad ve numTimes parametresi sürdü ve tarayıcıya çıktı. Denetleyicinin bu yanıtı doğrudan işlemeye devam etmesine izin vermek yerine, bu verileri tutmak için küçük bir sınıf oluşturun ve bunu kullanarak HTML yanıtını geri işlemek için bir görünüm şablonuna geçirin. Bu şekilde, denetleyici bir işlemle ve görünüm şablonuyla ilgilendirmekle birlikte, uygulamamız içinde "kaygıları ayrımı" konusunda devam etmemizi sağlar.

HelloWorldController.cs dosyasına dönün ve yeni bir "WelcomeViewModel" sınıfı ekleyin ve denetleyicinizin içindeki hoş geldiniz yöntemini değiştirin. Bu, yeni sınıf ile aynı dosyada bulunan tüm HelloWorldController.cs.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

Birden çok satırda olsa da, hoş geldiniz yönteminiz aslında yalnızca iki kod ifadesi olur. İlk ifade, iki parametremizi bir ViewModel nesnesine paketler ve ikincisi elde edilen nesneyi görünüme geçirir.

Şimdi bir hoş geldiniz görünüm şablonuna ihtiyacımız var! Hoş geldiniz yöntemine sağ tıklayın ve Görünüm Ekle ' yi seçin. Bu kez, "kesin türü belirtilmiş bir görünüm oluştur" seçeneğini denetliyoruz ve açılan listeden WelcomeViewModel sınıfınızı seçeceğiz. Bu yeni görünüm yalnızca Welcomeviewmodel ve diğer nesne türleri hakkında bilgi sahibi olur.

> *NOTE: için WelcomeViewModel ' i ekleyerek açılan listede göstermek üzere bir kez derlemenize gerek duyarsınız.*

Görünüm Ekle iletişim kutusu şöyle görünmelidir. Ekle düğmesine tıklayın. ![Görünümü daire içinde Ekle](getting-started-with-mvc-part3/_static/image10.png)

Bu kodu, yeni Welcome. aspx &lt;H2&gt; altına ekleyin. Bir döngü oluşturacağız ve kullanıcının söylediğimiz her zaman Merhaba!

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

Ayrıca, aşağıdaki ekran görüntüsünde görüldüğü gibi model nesnemiz her seferinde yararlı IntelliSense karşılaştiğimiz için, bu görünümü bir WelcomeViewModel hakkında söylediğimiz için (müşterilerimiz evlemidir.

[![NumTime kaynak kodu](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

Uygulamanızı çalıştırın ve `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` yeniden ziyaret edin. Artık URL 'den veri çekiyoruz, denetleyicimiz otomatik olarak denetleyicimize geçirilir, denetleyici verileri bir ViewModel halinde paketliyoruz ve bu nesneyi görünümümüze geçirir. Görünüm, verileri kullanıcıya HTML olarak görüntülüyor.

[![hoş geldiniz-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

Bu, model için bir "a" türüdür ancak veritabanı türü değildir. Öğrendiklerimizi ve bir film veritabanı oluşturmamızı görelim.

> [!div class="step-by-step"]
> [Önceki](getting-started-with-mvc-part2.md)
> [İleri](getting-started-with-mvc-part4.md)
