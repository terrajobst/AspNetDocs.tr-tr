---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2\. Bölüm: denetleyiciler | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 2\. Bölüm denetleyicileri içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559880"
---
# <a name="part-2-controllers"></a>2\. Bölüm: Denetleyiciler

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 2\. Bölüm denetleyicileri içerir.

Geleneksel Web çerçeveleri ile gelen URL 'Ler genellikle disk üzerindeki dosyalarla eşleştirilir. Örneğin: "/Products.aspx" veya "/Products.php" gibi bir URL isteği bir "Products. aspx" veya "Products. php" dosyası tarafından işlenebilir.

Web tabanlı MVC çerçeveleri, URL 'Leri sunucu koduna biraz farklı bir şekilde eşler. Gelen URL 'Leri dosyalara eşlemek yerine, URL 'Leri sınıfların yöntemlerine eşleyin. Bu sınıflar "denetleyiciler" olarak adlandırılır ve gelen HTTP isteklerini işlemekten, Kullanıcı girişi işleme, verileri alma ve kaydetme ve istemciye geri gönderme yanıtını belirleme (HTML görüntüleme, bir dosyayı indirme, farklı bir şekilde yeniden yönlendirme) URL, vb.).

## <a name="adding-a-homecontroller"></a>HomeController ekleme

Sitemizin ana sayfasında URL 'Leri işleyecek bir denetleyici sınıfı ekleyerek MVC müzik deposu uygulamamıza başlayacağız. ASP.NET MVC 'nin varsayılan adlandırma kurallarını takip edeceğiz ve HomeController ' a çağrı yapacağız.

Çözüm Gezgini içindeki "denetleyiciler" klasörüne sağ tıklayın ve "Ekle" yi ve ardından "denetleyici..." öğesini seçin. komutundaki

![](mvc-music-store-part-2/_static/image1.jpg)

Bu, "denetleyici Ekle" iletişim kutusunu getirir. Denetleyiciyi "HomeController" olarak adlandırın ve Ekle düğmesine basın.

![](mvc-music-store-part-2/_static/image1.png)

Bu, aşağıdaki kodla yeni bir HomeController.cs dosyası oluşturur:

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

Mümkün olduğunca basit bir şekilde başlamak için Dizin metodunu yalnızca bir dize döndüren basit bir yöntemle değiştirin. İki değişiklik yapacağız:

- Yöntemi eylem sonucu yerine bir dize döndürecek şekilde değiştirin
- Return ifadesini "from evden" döndürecek şekilde değiştirin

Yöntemi şu şekilde görünmelidir:

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Şimdi siteyi çalıştıralım. Web-Server ' i başlatabiliriz ve aşağıdakilerden birini kullanarak siteyi deneyebiliriz::

- Debug ⇨ start hata ayıklamayı Başlat menü öğesini seçin
- Araç çubuğundaki yeşil ok düğmesine tıklayın ![](mvc-music-store-part-2/_static/image2.jpg)
- F5 klavye kısayolunu kullanın.

Yukarıdaki adımlardan herhangi birini kullanmak, projemizi derler ve Visual Web Developer 'ın yerleşik ASP.NET geliştirme sunucusunun başlatılmasına neden olur. ASP.NET Development Server 'ın başlatıldığını göstermek için ekranın alt köşesinde bir bildirim görünür ve altında çalıştığı bağlantı noktası numarasını gösterir.

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer, URL 'SI Web-Server ' ı işaret eden bir tarayıcı penceresini otomatik olarak açar. Bu, Web uygulamamızı hızlıca denememize olanak sağlayacak:

![](mvc-music-store-part-2/_static/image3.png)

Neredeyse hızlı bir şekilde, yeni bir Web sitesi oluşturdunuz, üç satırlık bir işlev ekledik ve bir tarayıcıda metin aldık. Roket bilimi değil, ancak bir başlangıç.

*Note: Visual Web Developer, Web sitenizi rastgele boş bir "bağlantı noktası" numarası üzerinde çalıştıracak ASP.NET geliştirme sunucusunu içerir. Yukarıdaki ekran görüntüsünde, site `http://localhost:26641/`çalışıyor, bu nedenle 26641 numaralı bağlantı noktasını kullanıyor. Bağlantı noktası numaranız farklı olacaktır. Bu öğreticide, URL 'ler gibi/Store/gözatım gibi bir iletişim kurduğumuz zaman, bağlantı noktası numarasından sonra da devam edecektir. 26641 numaralı bağlantı noktası,/Store/gözatma 'ya göz atarak `http://localhost:26641/Store/Browse`göz atacaktır.*

## <a name="adding-a-storecontroller"></a>StoreController ekleme

Sitemizin ana sayfasını uygulayan basit bir HomeController ekledik. Şimdi, müzik mağazamız için göz atma işlevini uygulamak üzere kullanacağımız başka bir denetleyici ekleyelim. Mağaza denetleyicimiz üç senaryoyu destekleyecektir:

- Müzik mağazamız içindeki müzik tarzlarımızın bir listeleme sayfası
- Belirli bir tarz tüm müzik albümlerini listeleyen bir tarayıcı sayfası
- Belirli bir müzik albümünden ilgili bilgileri gösteren Ayrıntılar sayfası

Yeni bir StoreController sınıfı ekleyerek başlayacağız. Henüz yapmadıysanız, tarayıcıyı kapatarak veya Debug ⇨ Stop Debugging menü öğesini seçerek uygulamayı çalıştırmayı durdurun.

Şimdi yeni bir StoreController ekleyin. HomeController ile yaptığımız gibi, bunu, Çözüm Gezgini içinde "denetleyiciler" klasörüne sağ tıklayıp, Add-&gt;Controller menü öğesini seçerek yapacağız.

![](mvc-music-store-part-2/_static/image4.png)

Yeni StoreController bir "Dizin" metoduna zaten sahip. Bu "Dizin" yöntemini, müzik Deponuzdaki tüm tarzları listeleyen listeleme sayfamızı uygulamak için kullanacağız. Ayrıca, StoreController 'ın işlemesini istediğimiz iki senaryoyu uygulamak için iki ek yöntem de ekleyeceğiz: tarama ve ayrıntılar.

Denetleyicimiz içindeki bu yöntemlere (Dizin, gözatmayı ve ayrıntıları) "denetleyici eylemleri" adı verilir ve HomeController. Index () eylem yöntemiyle zaten gördüğünüz gibi, işleri URL isteklerine yanıt verebiliyor ve (genel olarak konuşulur) hangi içeriğin olduğunu belirleme URL 'YI çağıran tarayıcıya veya kullanıcıya geri gönderilmelidir.

Dizin () yöntemini "Hello. Index ()" dizesini döndürecek şekilde değiştirerek StoreController uygulamamıza başlayacağız ve gözatıp () ve ayrıntılar () için benzer yöntemler ekleyeceğiz:

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

Projeyi yeniden çalıştırın ve aşağıdaki URL 'Lere gözatamazsınız:

- /Store
- /Store/zat
- /Store/Details

Bu URL 'Lere erişim, denetleyicimiz içindeki eylem yöntemlerini çağırır ve dize yanıtlarını döndürür:

![](mvc-music-store-part-2/_static/image5.png)

Bu harika, ancak bunlar yalnızca sabit dizelerdir. Böylece, URL 'den bilgi alıp sayfa çıktısında görüntülenecek şekilde dinamik hale olalım.

İlk olarak, URL 'den bir QueryString değeri almak için, gezinme eylemi yöntemini değiştireceksiniz. Bunu, eylem yönteimize bir "tarz" parametresi ekleyerek yapabiliriz. Bu ASP.NET MVC, çağrıldığında otomatik olarak herhangi bir QueryString veya "tarz" adlı form gönderme parametrelerini eylem yönteimize iletir.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*Note: Kullanıcı girişini silmek için HttpUtility. HtmlEncode yardımcı programı yöntemini kullanıyoruz. Bu, kullanıcıların JavaScript 'i/Store/gözatmaya benzer bir bağlantıyla ekleme değiştirmesini engeller. Tarz =&lt;betiği&gt;Window. Location = 'http://hackersite.com'&lt;/SCRIPT&gt;.*

Şimdi/Store/gözatmaya gözatmaya izin veriyor musunuz? Tarz = disco

![](mvc-music-store-part-2/_static/image6.png)

Daha sonra Ayrıntılar eylemini, ID adlı bir giriş parametresi okumak ve görüntülenecek şekilde değiştirelim. Önceki yönteminizin aksine ID değerini bir QueryString parametresi olarak gömeceğiz. Bunun yerine, bunu doğrudan URL 'nin içine ekleyeceğiz. Örneğin:/Store/Details/5.

ASP.NET MVC bunu, herhangi bir şeyi yapılandırmak zorunda kalmadan kolayca yapabilmenizi sağlar. ASP.NET MVC 'nin varsayılan yönlendirme kuralı, eylem yöntemi adından sonra bir URL 'nin segmentini "ID" adlı bir parametre olarak değerlendirmek için kullanılır. Eylem yönteminizin ID adlı bir parametresi varsa ASP.NET MVC, URL segmentini otomatik olarak bir parametre olarak size iletir.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

Uygulamayı çalıştırın ve/Store/Details/5 adresine gidin:

![](mvc-music-store-part-2/_static/image7.png)

Şimdiye kadar yaptığımız şeyleri de en üst sınıra bakalım:

- Visual Web Developer 'da yeni bir ASP.NET MVC projesi oluşturduk
- Bir ASP.NET MVC uygulamasının temel klasör yapısını tartıştık.
- ASP.NET geliştirme sunucusunu kullanarak Web sitemizi nasıl çalıştıracağınızı öğrendiniz
- İki denetleyici sınıfı oluşturduk: bir HomeController ve StoreController
- URL isteklerine yanıt veren ve tarayıcıya metin döndüren denetleyicilerimize eylem yöntemleri ekledik

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-1.md)
> [İleri](mvc-music-store-part-3.md)
