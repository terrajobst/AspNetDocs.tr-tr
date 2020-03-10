---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: Kimlik doğrulama ve yetkilendirme kullanarak uygulamaları güvenli hale getirme | Microsoft Docs
author: microsoft
description: 9\. adımda, Nerdakşam yemeği uygulamamız için kimlik doğrulaması ve yetkilendirme ekleme ve kullanıcıların oluşturmak için siteye kaydolması ve sitede oturum açması gerekir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600984"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>Kimlik Doğrulama ve Yetkilendirme Kullanarak Uygulamaların Güvenliğini Sağlama

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 9 ' u.
> 
> 9\. adımda, Nerdakşam yemeği uygulamamıza güvenli hale getirmek üzere kimlik doğrulaması ve yetkilendirme ekleme işlemi, kullanıcıların yeni yemek 'ler oluşturmak için siteye kaydolmaları ve oturum açması ve yalnızca bir akşam yemeği 'yi barındıran Kullanıcı tarafından düzenlenebilir olması gerektiğini gösterir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-9-authentication-and-authorization"></a>Nerdakşam yemeği adım 9: kimlik doğrulama ve yetkilendirme

Şu anda Nerdakşam yemeği uygulamamız, siteyi ziyaret eden kişilerin herhangi bir akşam yemeği için ayrıntıları oluşturma ve düzenleme olanağı veriyor. Bunu, kullanıcıların yeni dinlayıcıları oluşturmak ve siteye oturum açması ve yalnızca bir akşam yemeği 'yi barındıran kullanıcının düzenleyebilmesini sağlayacak bir kısıtlama eklemesi için bunu değiştirelim.

Bunu etkinleştirmek için, uygulamamızı güvenli hale getirmek üzere kimlik doğrulaması ve yetkilendirme kullanacağız.

### <a name="understanding-authentication-and-authorization"></a>Kimlik doğrulama ve yetkilendirmeyi anlama

*Kimlik doğrulaması* , bir uygulamaya erişen istemcinin kimliğini belirleme ve doğrulama işlemidir. Daha fazlasını yapın, son kullanıcının bir Web sitesini ziyaret ettiğinde ne zaman olduğunu belirlemek. ASP.NET, tarayıcı kullanıcılarının kimlik doğrulamasının birden çok yolunu destekler. Internet Web uygulamaları için kullanılan en yaygın kimlik doğrulama yaklaşımına "form kimlik doğrulaması" adı verilir. Forms kimlik doğrulaması, bir geliştiricinin uygulama içinde HTML oturum açma formu yazarışını sağlar ve ardından bir veritabanı veya diğer parola kimlik bilgileri deposuna göre Son Kullanıcı gönderisin Kullanıcı adını/parolasını doğrular. Kullanıcı adı/parola birleşimi doğru ise, geliştirici daha sonra, ASP.NET sonraki isteklerde kullanıcıyı tanımlamak için şifrelenmiş bir HTTP tanımlama bilgisi vermesini isteyebilir. Form kimlik doğrulamasını Nerdakşam yemeği uygulamamız ile kullanacağız.

*Yetkilendirme* , kimliği doğrulanmış bir kullanıcının belırlı bir URL/kaynağa erişme izni olup olmadığını belirleme veya bazı eylemler gerçekleştirme işlemidir. Örneğin, Nerdakşam yemeği uygulamamız içinde yalnızca oturum açan kullanıcıların */Dinners/Create* URL 'sine erişip yeni dinetleri oluşturabileceksiniz. Ayrıca, yalnızca bir akşam yemeği barındıran kullanıcının düzenleyebilmesini ve diğer tüm kullanıcılara düzenleme erişimini reddetmesi için yetkilendirme mantığı eklemek isteyeceksiniz.

### <a name="forms-authentication-and-the-accountcontroller"></a>Forms kimlik doğrulaması ve AccountController

Yeni ASP.NET MVC uygulamaları oluşturulduğunda ASP.NET MVC için varsayılan Visual Studio proje şablonu otomatik olarak form kimlik doğrulaması etkinleştirilir. Ayrıca, projeye önceden oluşturulmuş bir hesap oturum açma sayfası uygulamasını otomatik olarak ekler. Bu, bir site içinde güvenliği tümleştirmeyi gerçekten kolaylaştırır.

Varsayılan site. Master ana sayfası, erişimi doğrulanmadığı zaman sitenin sağ üst kısmında "oturum aç" bağlantısını görüntüler:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

"Oturum aç" bağlantısına tıklanması bir kullanıcıyı */Account/Logon* URL 'sine götürür:

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

Kaydolmayan ziyaretçiler bunu, */Account/Register* URL 'sine alacak ve hesap ayrıntılarını girmesine izin veren "Register" bağlantısına tıklayarak yapabilir:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

"Kaydet" düğmesine tıklamak, ASP.NET üyelik sisteminde yeni bir kullanıcı oluşturur ve Forms kimlik doğrulamasını kullanarak kullanıcının site üzerinde kimliğini doğrular.

Bir Kullanıcı oturum açtığında, site. Master sayfanın sağ üst köşesindeki "hoş geldiniz [Kullanıcı adı]!" çıktısını almak için sayfayı değiştirir ileti ve bir "oturum aç" bağlantısı yerine "oturum kapatma" bağlantısını işler. "Oturumu Kapat" bağlantısına tıklanması Kullanıcı oturumunu günlüğe kaydeder:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

Yukarıdaki oturum açma, oturum kapatma ve kayıt işlevselliği, projeyi oluştururken Visual Studio tarafından projemizi eklenen AccountController sınıfı içinde uygulanır. AccountController için Kullanıcı arabirimi, \Views\Account dizinindeki Görünüm şablonları kullanılarak uygulanır:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController sınıfı, şifreli kimlik doğrulama tanımlama bilgileri vermek için ASP.NET Forms kimlik doğrulama sistemini ve Kullanıcı adlarını/parolaları depolamak ve doğrulamak için ASP.NET üyelik API 'sini kullanır. ASP.NET üyelik API 'SI genişletilebilir ve parola kimlik bilgisi deposunun kullanılmasını sağlar. ASP.NET, bir SQL veritabanı içinde veya Active Directory içinde Kullanıcı adı/parolaları depolayan yerleşik üyelik sağlayıcısı uygulamalarıyla birlikte gelir.

Nerdakşam yemeği uygulamamız, projenin kökündeki "Web. config" dosyasını açıp bunun içindeki &lt;üyelik&gt; bölümüne bakarak hangi üyelik sağlayıcısını kullanması gerektiğini yapılandırabiliriz. Proje oluşturulduğunda varsayılan Web. config eklenir ve SQL üyelik sağlayıcısını kaydeder ve veritabanı konumunu belirtmek için bunu "ApplicationServices" adlı bir bağlantı dizesi kullanacak şekilde yapılandırır.

Varsayılan "ApplicationServices" bağlantı dizesi (Web. config dosyasının &lt;connectionStrings&gt; bölümü içinde belirtilen) SQL Express kullanmak üzere yapılandırılmıştır. "ASPNETDB" adlı bir SQL Express veritabanına işaret eder. MDF "uygulamanın" uygulama\_verileri "dizini. Bu veritabanı, üyelik API 'SI uygulama içinde ilk kez kullanıldığında, ASP.NET otomatik olarak veritabanını oluşturur ve içinde uygun üyelik veritabanı şemasını sağlayacaktır:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

SQL Express kullanmak yerine tam bir SQL Server örneği kullanmak (veya uzak bir veritabanına bağlanmak) istiyoruz, tüm yapmanız gereken, Web. config dosyasındaki "ApplicationServices" bağlantı dizesini güncelleştirmek ve uygun üyelik şemasının olduğundan emin olmak için , işaret ettiği veritabanına eklenmiştir. Üyelik ve diğer ASP.NET uygulama hizmetleri için uygun şemayı bir veritabanına eklemek için \Windows\Microsoft.NET\Framework\v2.0.50727\ dizinindeki "ASPNET\_regsql. exe" yardımcı programını çalıştırabilirsiniz.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[Yetkilendir] filtresi kullanılarak/Dinners/Create URL 'sini yetkilendirme

Nerdakşam yemeği uygulaması için güvenli kimlik doğrulama ve hesap yönetimi uygulamasını etkinleştirmek üzere kod yazmak zorunda yoktu. Kullanıcılar, uygulamamız ile yeni hesaplar kaydedebilir ve sitenin oturumunu açma/kapatma olabilir.

Artık uygulamaya yetkilendirme mantığı ekleyebiliriz ve sitede ne yapabileceklerini ve yapabileceklerini denetlemek için ziyaretçilerin kimlik doğrulama durumunu ve Kullanıcı adını kullanabilirsiniz. DinnersController sınıfımız "oluşturma" eylem yöntemlerine yetkilendirme mantığı ekleyerek başlayalım. Özellikle, */Dinners/Create* URL 'sine erişen kullanıcıların oturum açması gerekir. Oturum açmadıysa, oturum açabilmek için bunları oturum açma sayfasına yönlendirirsiniz.

Bu mantığı uygulamak oldukça kolaydır. Her şey için bir [Yetkilendir] filtre özniteliği eklememiz gerekir, örneğin:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC, eylem yöntemlerine bildirimli olarak uygulanabilen, yeniden kullanılabilir mantığı uygulamak için kullanılabilen "eylem filtreleri" oluşturma özelliğini destekler. [Yetkilendir] filtresi, ASP.NET MVC tarafından sunulan yerleşik eylem filtrelerinden biridir ve bir geliştiricinin eylem yöntemlerine ve denetleyici sınıflarına bildirimli olarak yetkilendirme kuralları uygulamasını sağlar.

Herhangi bir parametre olmadan uygulandığında (yukarıdaki gibi), [Yetkilendir] filtresi, eylem yöntemi isteğini yapan kullanıcının oturum açmış olması gerekir; Aksi takdirde tarayıcı, oturum açma URL 'sine otomatik olarak yönlendirilir. Bu yeniden yönlendirmeyi yaparken, ilk istenen URL bir QueryString bağımsız değişkeni olarak geçirilir (örneğin:/Account/LogOn? ReturnUrl =% 2Fınfıanlar% 2fCreate). AccountController daha sonra yeniden oturum açtıklarında kullanıcıyı istenen URL 'ye yeniden yönlendirir.

[Yetkilendir] filtresi, isteğe bağlı olarak, kullanıcının hem oturum açmasını hem de izin verilen bir güvenlik rolünün bir listesini içinde olmasını gerektirmek için kullanılabilecek bir "kullanıcılar" veya "Roller" özelliği belirtme özelliğini destekler. Örneğin, aşağıdaki kod,/Dinners/Create URL 'sine erişmek için yalnızca "ScottGu" ve "billg" olmak üzere iki özel kullanıcıya izin verir:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

Kod içinde belirli kullanıcı adlarının gömülmesi, oldukça mümkün değildir. Daha iyi bir yaklaşım, kodun tarafından kontrol edilen daha üst düzey "rolleri" tanımlamak ve ardından bir veritabanı ya da Active Directory sistemi kullanarak (gerçek Kullanıcı eşleme listesini koddan dışarıdan depolanmasını etkinleştirmek) Kullanıcı rolüne eşlemek için daha iyi bir yaklaşımdır. ASP.NET, yerleşik bir rol yönetim API 'SI ve bu kullanıcı/rol eşlemesini gerçekleştirmeye yardımcı olabilecek yerleşik bir rol sağlayıcıları kümesi (SQL ve Active Directory gibi) içerir. Daha sonra kodu yalnızca belirli bir "Yönetici" rolünde bulunan kullanıcıların/Dinners/Create URL 'sine erişmesine izin verecek şekilde güncelleştirebiliriz:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Dinlayıcıları oluştururken User.Identity.Name özelliğini kullanma

Bir isteğin oturum açmış olan kullanıcısının Kullanıcı adını, denetleyici temel sınıfında kullanıma sunulan User.Identity.Name özelliğini kullanarak alabiliriz.

Daha önce, Create () eylem yönteminizin HTTP-POST sürümünü uyguladığımızda, akşam yemeği 'nin "HostedBy" özelliğini statik bir dizeye kodlıyoruz. Artık bu kodu, User.Identity.Name özelliğini kullanacak şekilde güncelleştirebilir, ayrıca akşam yemeği 'yi oluşturan ana bilgisayar için otomatik olarak bir RSVP ekleyebilirsiniz:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Create () yöntemine bir [Yetkilendir] özniteliği eklediğimiz için, ASP.NET MVC eylem yönteminin yalnızca/Dinners/Create URL 'sini ziyaret eden kullanıcı sitede oturum açtıysa yürütülür olmasını sağlar. Bu nedenle, User.Identity.Name Özellik değeri her zaman geçerli bir Kullanıcı adı içerecektir.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>User.Identity.Name özelliğini, Dinlayıcıları düzenlenirken kullanma

Şimdi, kullanıcıları sınırlayan bazı yetkilendirme mantığını ekleyelim, böylece kullanıcılar kendilerini barındırdığı dinyilerin özelliklerini düzenleyebilirler.

Bu konuda yardım almak için önce akşam yemeği nesnemiz için bir "ıhostedby (Kullanıcı adı)" yardımcı yöntemi ekleyeceğiz (daha önce oluşturduğumuz Dinner.cs kısmi sınıfı içinde). Bu yardımcı yöntem, girilen bir kullanıcı adının akşam yemeği HostedBy özelliği ile eşleşip eşleşmediğini ve bir büyük küçük harfe duyarsız dize karşılaştırması gerçekleştirmek için gereken mantığı Kapsüller doğru veya yanlış döndürür:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

Daha sonra DinnersController sınıfımızın içindeki Edit () eylem yöntemlerine bir [Yetkilendir] özniteliği ekleyeceğiz. Bu, */Dinners/Edit/[ID]* URL 'si istemek için kullanıcıların oturum açmasını sağlar.

Daha sonra, oturum açmış kullanıcının akşam yemeği ana bilgisayarıyla eşleştiğini doğrulamak üzere akşam yemeği. ıshostedby (Kullanıcı adı) yardımcı yöntemini kullanan düzenleme yöntemlerimize kod ekleyebiliriz. Kullanıcı ana bilgisayar değilse, "ınvalidowner" görünümü görüntülenir ve isteği sonlandırır. Bunu yapmak için kod aşağıdaki gibi görünür:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

Daha sonra \Views\dıntik dizinine sağ tıklayıp yeni bir "InvalidOwner" görünümü oluşturmak için Ekle-&gt;görünümü menü komutunu seçebilirsiniz. Aşağıdaki hata iletisiyle dolduracağız:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

Artık bir kullanıcı sahip olmadıkları bir akşam yemeği düzenlemeyi denediğinde bir hata mesajı alırlar:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Denetleyicimiz içindeki Delete () eylem yöntemleri için aynı adımları yineleyebiliriz ve ayrıca bir akşam yemeği 'nın yalnızca bir akşam yemeği 'nin silmesine izin vermek için.

### <a name="showinghiding-edit-and-delete-links"></a>Düzenle ve Sil bağlantılarını gösterme/gizleme

Ayrıntılar URL 'imizde DinnersController sınıfımızın düzenleme ve silme eylemine bağlantı veriyoruz:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

Şu anda, Ayrıntılar URL 'SI için ziyaretçinin akşam yemeği 'nin ana bilgisayarı olup olmamasına bakılmaksızın düzenleme ve silme eylemi bağlantılarını gösteriyoruz. Şimdi bağlantıları, ziyaret eden Kullanıcı akşam yemeği 'nin sahibi ise görüntülenmesini sağlayacak şekilde değiştirelim.

DinnersController içindeki details () eylem yöntemi bir akşam yemeği nesnesi alır ve ardından bunu model nesnesi olarak görünüm şablonumuza geçirir:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

Aşağıdaki gibi akşam yemeği. ıshostedby () yardımcı yöntemini kullanarak Düzenle ve Sil bağlantılarını koşullu olarak göstermek/gizlemek için görünüm şablonumuzu güncelleştirebiliriz:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>Sonraki Adımlar

Artık, kimlik doğrulamalı kullanıcıları AJAX kullanarak dinetleri için RSVP 'e nasıl etkinleştirelim bölümüne bakalım.

> [!div class="step-by-step"]
> [Önceki](implement-efficient-data-paging.md)
> [İleri](use-ajax-to-deliver-dynamic-updates.md)
