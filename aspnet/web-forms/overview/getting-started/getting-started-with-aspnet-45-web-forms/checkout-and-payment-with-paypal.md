---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: PayPal ile kullanıma alma ve ödeme | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615141"
---
# <a name="checkout-and-payment-with-paypal"></a>PayPal ile Kasa İşlemleri ve Ödeme

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, Wingtip Toys örnek uygulamasının, PayPal kullanarak Kullanıcı Yetkilendirme, kayıt ve ödeme dahil olmak üzere nasıl değiştirileceği açıklanmaktadır. Yalnızca oturum açan kullanıcıların ürünleri satın alma yetkisi olur. ASP.NET 4,5 Web Forms proje şablonunun yerleşik kullanıcı kaydı işlevselliği, gerek duyduğunuz kadarını zaten içeriyor. PayPal Express kullanıma alma işlevselliği ekleyeceksiniz. Bu öğreticide, PayPal geliştirici sınama ortamını kullanıyorsunuz, bu nedenle hiçbir gerçek fon aktarılmaz. Öğreticinin sonunda, alışveriş sepetine eklenecek ürünleri seçerek, kullanıma al düğmesine tıklayarak ve verileri PayPal sınama Web sitesine aktararak uygulamayı test edersiniz. PayPal testi Web sitesinde, sevk etme ve ödeme bilgilerinizi onaylayıp, ardından satın almayı onaylamak ve tamamlayacak yerel Wingtip Toys örnek uygulamasına geri dönecektir.

Çevrimiçi alışverişle ilgili ölçeklenebilirlik ve güvenlik konusunda uzmanlaşan birkaç deneyimli üçüncü taraf ödeme işlemcisi vardır. ASP.NET geliştiricileri, bir alışveriş ve satın alma çözümünü uygulamadan önce üçüncü taraf ödeme çözümünün avantajlarından faydalanma avantajlarına göz önünde bulundurmalıdır.

> [!NOTE] 
> 
> Wingtip Toys örnek uygulaması, ASP.NET Web geliştiricileri için sunulan belirli ASP.NET kavramlarını ve özelliklerini göstermek üzere tasarlanmıştır. Bu örnek uygulama, ölçeklenebilirlik ve güvenlikle ilgili tüm olası durumlar için en iyi duruma getirilmemiştir.

## <a name="what-youll-learn"></a>Şunları öğreneceksiniz:

- Bir klasördeki belirli sayfalara erişimi kısıtlama.
- Anonim bir alışveriş sepetinden bilinen bir alışveriş sepeti oluşturma.
- Proje için SSL 'yi etkinleştirme.
- Projeye bir OAuth sağlayıcısı ekleme.
- PayPal test ortamını kullanarak ürünleri satın almak için PayPal kullanma.
- Bir **DetailsView** denetimindeki PayPal 'den ayrıntıları görüntüleme.
- Wingtip Toys uygulamasının veritabanını PayPal 'den elde edilen ayrıntılarla güncelleştirme.

## <a name="adding-order-tracking"></a>Sipariş Izleme ekleme

Bu öğreticide, bir kullanıcının oluşturduğu siparişten verileri izlemek için iki yeni sınıf oluşturacaksınız. Sınıflar Sevkiyat bilgileri, satın alma toplamı ve ödeme onayı hakkındaki verileri izler.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Order ve OrderDetail model sınıflarını ekleyin

Bu öğretici serisinde daha önce, *modeller* klasöründe `Category`, `Product`ve `CartItem` sınıfları oluşturarak Kategoriler, ürünler ve alışveriş sepeti öğelerinin şemasını tanımlamış olursunuz. Artık ürün siparişi için şemayı ve siparişin ayrıntılarını tanımlamak üzere iki yeni sınıf ekleyeceksiniz.

1. **Modeller** klasöründe, *Order.cs*adlı yeni bir sınıf ekleyin.   
   Yeni sınıf dosyası düzenleyicide görüntülenir.
2. Varsayılan kodu aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. *Modeller* klasörüne bir *OrderDetail.cs* sınıfı ekleyin.
4. Varsayılan kodu şu kodla değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

`Order` ve `OrderDetail` sınıfları, satın alma ve gönderme için kullanılan sipariş bilgilerini tanımlayan şemayı içerir.

Ayrıca, varlık sınıflarını yöneten ve veritabanına veri erişimi sağlayan veritabanı bağlamı sınıfını güncelleştirmeniz gerekir. Bunu yapmak için, yeni oluşturulan sipariş ve `OrderDetail` modeli sınıflarını `ProductContext` sınıfına eklersiniz.

1. **Çözüm Gezgini**, *ProductContext.cs* dosyasını bulun ve açın.
2. Vurgulanan kodu aşağıda gösterildiği gibi *ProductContext.cs* dosyasına ekleyin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

Bu öğretici serisinde daha önce bahsedildiği gibi, *ProductContext.cs* dosyasındaki kod `System.Data.Entity` ad alanını ekleyerek Entity Framework tüm çekirdek işlevlerine erişebilirsiniz. Bu işlevsellik, türü kesin belirlenmiş nesnelerle çalışarak verileri sorgulama, ekleme, güncelleştirme ve silme özelliğini içerir. `ProductContext` sınıfındaki Yukarıdaki kod, yeni eklenen `Order` ve `OrderDetail` sınıflarına Entity Framework erişim ekler.

## <a name="adding-checkout-access"></a>Kullanıma alma erişimi ekleme

Wingtip Toys örnek uygulaması, anonim kullanıcıların bir alışveriş sepetini gözden geçirmesine ve ürün eklemesine olanak tanır. Ancak, anonim kullanıcılar alışveriş sepetine ekledikleri ürünleri satın almayı tercih ettikleri zaman sitede oturum açması gerekir. Oturum açtıktan sonra, kullanıma alma ve satın alma sürecini işleyen Web uygulamasının kısıtlı sayfalarına erişebilirler. Bu kısıtlı sayfalar, uygulamanın *kullanıma alma* klasöründe bulunur.

### <a name="add-a-checkout-folder-and-pages"></a>Kullanıma alma klasörü ve sayfaları ekleme

Şimdi, kullanıma alma işlemi sırasında müşterinin göreceği bir *kullanıma alma* klasörü ve içindeki sayfalar oluşturacaksınız. Bu sayfaları daha sonra bu öğreticide güncelleşceksiniz.

1. **Çözüm Gezgini** içinde proje adına (**Wingtip Toys**) sağ tıklayın ve **Yeni klasör ekle**' yi seçin. 

    ![PayPal ile kullanıma alma ve ödeme-yeni klasör](checkout-and-payment-with-paypal/_static/image1.png)
2. Yeni klasör *kullanıma almayı*adlandırın.
3. *Kullanıma alma* klasörüne sağ tıklayın ve ardından **yeni öğe**&gt;-**Ekle** ' yi seçin. 

    ![PayPal ile kullanıma alma ve ödeme-yeni öğe](checkout-and-payment-with-paypal/_static/image2.png)
4. **Yeni öğe Ekle** iletişim kutusu görüntülenir.
5. Sol taraftaki **Visual C#**  -&gt; **Web** şablonları grubunu seçin. Ardından orta bölmeden, **ana sayfayla Web formu**' nu seçin ve *Checkoutstart. aspx*olarak adlandırın. 

    ![PayPal ile kullanıma alma ve ödeme-yeni öğe ekleme Iletişim kutusu](checkout-and-payment-with-paypal/_static/image3.png)
6. Daha önce olduğu gibi, ana sayfa olarak *site. Master* dosyasını seçin.
7. Aşağıdaki ek sayfaları, yukarıdaki adımları kullanarak *kullanıma alma* klasörüne ekleyin:   

    - CheckoutReview. aspx
    - Checkouttamamlanmıştır. aspx
    - CheckoutCancel. aspx
    - CheckoutError. aspx

### <a name="add-a-webconfig-file"></a>Web. config dosyası Ekle

*Kullanıma alma* klasörüne yeni bir *Web. config* dosyası ekleyerek, klasörde bulunan tüm sayfalara erişimi kısıtlayabilirsiniz.

1. *Kullanıma alma* klasörüne sağ tıklayın ve **yeni öğe**&gt; -**Ekle** ' yi seçin.  
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Sol taraftaki **Visual C#**  -&gt; **Web** şablonları grubunu seçin. Ardından orta bölmeden **Web yapılandırma dosyası**' nı seçin, *Web. config*dosyasının varsayılan adını kabul edin ve **Ekle**' yi seçin.
3. *Web. config* DOSYASıNDAKI mevcut XML içeriğini aşağıdakiler ile değiştirin:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. *Web. config* dosyasını kaydedin.

*Web. config* dosyası, Web uygulamasının tüm bilinmeyen kullanıcılarının, *kullanıma alma* klasöründe yer alan sayfalara erişiminin reddedilmesi gerektiğini belirtir. Ancak, Kullanıcı bir hesabı kaydettirirse ve oturum açtıysa, bilinen bir Kullanıcı olur ve *kullanıma alma* klasöründeki sayfalara erişimi olur.

ASP.NET yapılandırmasının bir hiyerarşiyi izlediğine dikkat edin. Bu, her *Web. config* dosyasının yapılandırma ayarlarını, içinde bulunduğu klasöre ve altındaki tüm alt dizinlere uygular.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>Proje için SSL 'yi etkinleştir

 Güvenli Yuva Katmanı (SSL), Web sunucularının ve Web istemcilerinin şifreleme kullanımıyla daha güvenli iletişim kurmasına izin vermek için tanımlanan bir protokoldür. SSL kullanılmazsa, istemci ve sunucu arasında gönderilen veriler, ağa fiziksel erişimi olan herkes tarafından paket algılaması 'na açıktır. Ayrıca, bazı yaygın kimlik doğrulama şemaları düz HTTP üzerinden güvenli değildir. Özellikle, temel kimlik doğrulaması ve Forms kimlik doğrulaması şifrelenmemiş kimlik bilgileri gönderir. Güvenli olması için, bu kimlik doğrulama düzenlerinin SSL kullanması gerekir. 

1. **Çözüm Gezgini**' de **wingtiptoys** projesine tıklayın ve sonra **Özellikler** penceresini göstermek için **F4** tuşuna basın.
2. SSL 'yi `true`için **etkin** olarak değiştirin.
3. Daha sonra kullanabilmek için **SSL URL 'sini** kopyalayın.   
 Daha önce SSL Web siteleri oluşturmadığınız sürece SSL URL 'SI `https://localhost:44300/` olur (aşağıda gösterildiği gibi).   
    ![Proje Özellikleri](checkout-and-payment-with-paypal/_static/image4.png)
4. **Çözüm Gezgini**' de **wingtiptoys** projesine sağ tıklayın ve **Özellikler**' e tıklayın.
5. Sol sekmede **Web**' e tıklayın.
6. **Proje URL** 'sini daha önce kaydettiğiniz **SSL URL 'sini** kullanacak şekilde değiştirin.   
    ![Project Web Properties](checkout-and-payment-with-paypal/_static/image5.png)
7. **CTRL + S**tuşlarına basarak sayfayı kaydedin.
8. Uygulamayı çalıştırmak için **CTRL + F5** tuşlarına basın. Visual Studio, SSL uyarılarından kaçınmanıza izin veren bir seçenek görüntüler.
9. IIS Express SSL sertifikasına güvenmek ve devam etmek için **Evet** ' e tıklayın.   
    ![IIS Express SSL sertifikası ayrıntıları](checkout-and-payment-with-paypal/_static/image6.png)  
 Bir güvenlik uyarısı görüntülenir.
10. Sertifikayı localhost 'a yüklemek için **Evet** ' e tıklayın.   
    ![güvenlik uyarısı iletişim kutusu](checkout-and-payment-with-paypal/_static/image7.png)  
 Tarayıcı penceresi görüntülenecektir.

Artık SSL kullanarak Web uygulamanızı kolayca test edebilirsiniz.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>OAuth 2,0 sağlayıcısı ekleme

ASP.NET Web Forms üyelik ve kimlik doğrulama için gelişmiş seçenekler sağlar. Bu geliştirmeler OAuth içerir. OAuth, Web, mobil ve Masaüstü uygulamalarından basit ve standart bir yöntemde güvenli yetkilendirmeye izin veren bir açık protokoldür. ASP.NET Web Forms şablonu, Facebook, Twitter, Google ve Microsoft 'u kimlik doğrulama sağlayıcıları olarak göstermek için OAuth kullanır. Bu öğretici, kimlik doğrulama sağlayıcısı olarak yalnızca Google kullanıyor olsa da, sağlayıcıyı kullanmak için kodu kolayca değiştirebilirsiniz. Diğer sağlayıcıları uygulama adımları, bu öğreticide göreceğiniz adımlara çok benzer.

Kimlik doğrulamasına ek olarak öğreticide yetkilendirme uygulamak için de roller de kullanılır. Yalnızca `canEdit` rolüne eklediğiniz kullanıcılar verileri değiştirebilir (kişileri oluşturabilir, düzenleyebilir veya silebilir).

> [!NOTE] 
> 
> Windows Live uygulamaları, çalışan bir Web sitesi için yalnızca canlı URL 'yi kabul eder, bu nedenle oturum açma işlemleri için yerel bir Web sitesi URL 'SI kullanamazsınız.

Aşağıdaki adımlar, bir Google kimlik doğrulama sağlayıcısı eklemenize olanak sağlayacak.

1. *Uygulama\_Start\Startup.auth.cs* dosyasını açın.
2. Yöntemin aşağıdaki gibi görünmesi için `app.UseGoogleAuthentication()` yönteminden açıklama karakterlerini kaldırın: 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. [Google geliştiricileri konsoluna](https://console.developers.google.com/)gidin. Ayrıca, Google Developer e-posta hesabınızla (gmail.com) oturum açmanız gerekir. Bir Google hesabınız yoksa **Hesap oluştur** bağlantısını seçin.   
   Ardından, **Google geliştiricileri konsolunu**görürsünüz.   
    ![Google geliştiricileri konsolu](checkout-and-payment-with-paypal/_static/image8.png)
4. **Proje oluştur** düğmesine tıklayın ve bir proje adı ve kimliği girin (varsayılan değerleri kullanabilirsiniz). Sonra **anlaşma onay kutusuna** ve **Oluştur** düğmesine tıklayın.  

    ![Google-yeni proje](checkout-and-payment-with-paypal/_static/image9.png)

   Birkaç saniye içinde yeni proje oluşturulur ve tarayıcınızda yeni projeler sayfası görüntülenir.
5. Sol sekmede, kimlik **doğrulaması &amp; API 'ler**' e ve ardından **kimlik bilgileri**' ne tıklayın.
6. **OAuth**altında **yeni istemci kimliği oluştur** ' a tıklayın.   
   **ISTEMCI kimliği oluştur** iletişim kutusu görüntülenir.   
    ![Google-Istemci KIMLIĞI oluşturma](checkout-and-payment-with-paypal/_static/image10.png)
7. **ISTEMCI kimliği oluştur** iletişim kutusunda, uygulama türü Için varsayılan **Web uygulamasını** saklayın.
8. **Yetkili JavaScript kaynakları** 'nı Bu öğreticide daha önce KULLANDıĞıNıZ SSL URL 'sine ayarlayın (başka bir SSL projesi oluşturmadığınız müddetçe`https://localhost:44300/`).   
   Bu URL, uygulamanızın başlangıtıdır. Bu örnek için yalnızca localhost sınama URL 'sini girersiniz. Ancak, localhost ve üretim için hesaba birden çok URL girebilirsiniz.
9. **Yetkilendirilmiş yeniden YÖNLENDIRME URI** 'sini şu şekilde ayarlayın: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   Bu değer, ASP.NET OAuth kullanıcılarının Google OAuth sunucusuyla iletişim kurmasını sağlayan URI 'dir. Yukarıda kullandığınız SSL URL 'sini (başka bir SSL projesi oluşturmadığınız müddetçe `https://localhost:44300/`) unutmayın.
10. **ISTEMCI kimliği oluştur** düğmesine tıklayın.
11. Google Developers konsolunun sol menüsünde **onay ekranı** menü öğesine tıklayın, ardından e-posta adresinizi ve ürün adınızı ayarlayın. Formu tamamladığınızda **Kaydet**' e tıklayın.
12. **API 'ler** menü öğesine tıklayın, aşağı kaydırın ve **Google + API**' nin yanındaki **kapalı** düğmesine tıklayın.   
    Bu seçenek kabul edilirse, Google + API etkinleştirilir.
13. Ayrıca, **Microsoft. Owin** NuGet paketini 3.0.0 sürümüne güncelleştirmeniz gerekir.   
    **Araçlar** menüsünde **NuGet Paket Yöneticisi** ' ni seçin ve ardından **çözüm için NuGet Paketlerini Yönet**' i seçin.  
    **NuGet Paketlerini Yönet** penceresinde **Microsoft. Owin** paketini bulun ve 3.0.0 sürümüne güncelleştirin.
14. Visual Studio 'da, *Startup.auth.cs* sayfasının `UseGoogleAuthentication` yöntemini, **Istemci kimliği** ve **istemci gizliliğini** kopyalayıp yöntemine yapıştırarak güncelleştirin. Aşağıda gösterilen **ISTEMCI kimliği** ve **istemci gizli** değerleri örneklerdir ve çalışmayacak. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. Uygulamayı derlemek ve çalıştırmak için **CTRL + F5** tuşlarına basın. **Oturum aç** bağlantısına tıklayın.
16. **Oturum açmak için başka bir hizmet kullan**' ın altında **Google**' a tıklayın.  
    ](checkout-and-payment-with-paypal/_static/image11.png) ![oturum açma
17. Kimlik bilgilerinizi girmeniz gerekiyorsa, kimlik bilgilerinizi gireceğiniz Google sitesine yönlendirilirsiniz.  
    ![Google-oturum açma](checkout-and-payment-with-paypal/_static/image12.png)
18. Kimlik bilgilerinizi girdikten sonra, yeni oluşturduğunuz Web uygulamasına izin vermeniz istenir.  
    ![Proje varsayılan hizmet hesabı](checkout-and-payment-with-paypal/_static/image13.png)
19. **Kabul et**' e tıklayın. Şimdi, Google hesabınızı kaydedebileceğiniz **wingtiptoys** uygulamasının **kayıt** sayfasına yeniden yönlendirilirsiniz.  
    ![Google hesabınızla kaydedin](checkout-and-payment-with-paypal/_static/image14.png)
20. Gmail hesabınız için kullanılan yerel e-posta kayıt adını değiştirme seçeneğiniz vardır, ancak genellikle varsayılan e-posta diğer adını (yani, kimlik doğrulaması için kullandığınız hesap) korumak istersiniz. Yukarıda gösterildiği gibi **oturum aç** ' a tıklayın.

### <a name="modifying-login-functionality"></a>Oturum açma Işlevini değiştirme

Bu öğretici serisinde daha önce belirtildiği gibi, varsayılan olarak ASP.NET Web Forms şablonuna Kullanıcı kayıt işlevselliğinin büyük bölümü eklenmiştir. Şimdi, `MigrateCart` yöntemini çağırmak için Default *login. aspx* ve *register. aspx* sayfalarını değiştirirsiniz. `MigrateCart` yöntemi, yeni oturum açmış kullanıcıyı anonim bir alışveriş sepetine ilişkilendirir. Kullanıcı ve alışveriş sepetini ilişkilendirerek, Wingtip Toys örnek uygulaması ziyaretler arasında kullanıcının alışveriş sepetini sürdürebilecektir.

1. **Çözüm Gezgini**, *Hesap* klasörünü bulun ve açın.
2. *Login.aspx.cs* adlı arka plan kod sayfasını, sarı renkle vurgulanmış kodu içerecek şekilde değiştirin, böylece şöyle görünür:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. *Login.aspx.cs* dosyasını kaydedin.

Şimdilik `MigrateCart` yöntemi için bir tanım olmadığı uyarısını yoksayabilirsiniz. Bu öğreticide daha sonra bir bit eklersiniz.

*Login.aspx.cs* arka plan kod dosyası bir oturum açma yöntemini destekler. Login. aspx sayfasını inceleyerek, bu sayfada bir "oturum aç" düğmesi, tıklama tıklayadaki kod `LogIn` işleyicisini tetikler.

*Login.aspx.cs* üzerinde `Login` yöntemi çağrıldığında, `usersShoppingCart` adlı alışveriş sepetinin yeni bir örneği oluşturulur. Alışveriş sepetinin (bir GUID) KIMLIĞI alınır ve `cartId` değişkenine ayarlanır. Ardından `MigrateCart` yöntemi çağrılır, hem `cartId` hem de oturum açan kullanıcının adı bu yönteme geçer. Alışveriş sepeti geçirildiğinde, anonim alışveriş sepetini tanımlamak için kullanılan GUID, Kullanıcı adıyla değiştirilmiştir.

Kullanıcı oturum açtığında alışveriş sepetini geçirmek için *login.aspx.cs* arka plan kodu dosyasını değiştirmenin yanı sıra, Kullanıcı yeni bir hesap ve oturum açtığında, alışveriş sepetini geçirmek için *register.aspx.cs arka plan kodu dosyasını* da değiştirmelisiniz.

1. *Hesap* klasöründe, *register.aspx.cs*adlı arka plan kod dosyasını açın.
2. Kodu sarı olarak ekleyerek arka plan kod dosyasını aşağıdaki gibi görünecek şekilde değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. *Register.aspx.cs* dosyasını kaydedin. Bir kez daha `MigrateCart` yöntemiyle ilgili uyarıyı yoksayın.

`CreateUser_Click` olay işleyicisinde kullandığınız kodun, `LogIn` yönteminde kullandığınız koda çok benzediğine dikkat edin. Kullanıcı siteye kaydolduğunda veya sitede oturum açtığında, `MigrateCart` yöntemine bir çağrı yapılır.

## <a name="migrating-the-shopping-cart"></a>Alışveriş sepetini geçirme

Oturum açma ve kayıt işlemini güncelleştirmiş olduğunuza göre, `MigrateCart` yöntemini kullanarak alışveriş sepetini geçirmek için kodu ekleyebilirsiniz.

1. **Çözüm Gezgini**, *Logic* klasörünü bulun ve *ShoppingCartActions.cs* sınıf dosyasını açın.
2. *ShoppingCartActions.cs* dosyasında vurgulanan kodu, *ShoppingCartActions.cs* dosyasındaki kodun aşağıdaki gibi görünmesini sağlamak için, sarı renkle birlikte ekleyin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

`MigrateCart` yöntemi, kullanıcının alışveriş sepetini bulmak için mevcut CartId 'yi kullanır. Daha sonra kod, tüm alışveriş sepeti öğelerinin üzerinden geçer ve `CartId` özelliğini (`CartItem` şeması tarafından belirtilen şekilde) oturum açan kullanıcı adıyla değiştirir.

### <a name="updating-the-database-connection"></a>Veritabanı bağlantısı güncelleştiriliyor

**Önceden oluşturulmuş** Wingtip Toys örnek uygulamasını kullanarak bu öğreticiyi takip ediyorsanız, varsayılan üyelik veritabanını yeniden oluşturmanız gerekir. Varsayılan bağlantı dizesini değiştirerek, uygulama bir sonraki sefer çalıştırıldığında üyelik veritabanı oluşturulur.

1. Projenin kökündeki *Web. config* dosyasını açın.
2. Varsayılan bağlantı dizesini aşağıdaki gibi görünecek şekilde güncelleştirin:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>PayPal 'i tümleştirme

PayPal, çevrimiçi tüccarların göre ödemeleri kabul eden Web tabanlı bir faturalandırma platformudur. Bu öğreticide, PayPal 'in hızlı kullanıma alma işlevselliğinin uygulamanıza nasıl tümleştirileceği açıklanmaktadır. Hızlı kullanıma alma, müşterilerinizin kendi alışveriş sepetine ekledikleri öğeler için PayPal kullanmasını sağlar.

### <a name="create-paypal-test-accounts"></a>PayPal test hesapları oluşturma

PayPal test ortamını kullanmak için bir geliştirici testi hesabı oluşturmanız ve doğrulamanız gerekir. Bir Satınalmacı test hesabı ve bir satıcı test hesabı oluşturmak için geliştirici sınama hesabını kullanacaksınız. Geliştirici sınama hesabı kimlik bilgileri ayrıca, Wingtip Toys örnek uygulamasının PayPal sınama ortamına erişmesine izin verir.

1. Bir tarayıcıda, PayPal geliştirici testi sitesine gidin:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. PayPal geliştirici hesabınız yoksa **, Kaydol ' a tıklayarak ve kaydolma**adımlarını izleyerek yeni bir hesap oluşturun. Var olan bir PayPal geliştirici hesabınız varsa **oturum**aç ' a tıklayarak oturum açın. Bu öğreticide daha sonra Wingtip Toys örnek uygulamasını test etmek için PayPal geliştirici hesabınızın olması gerekir.
3. PayPal geliştirici hesabınıza yeni kaydolduysanız PayPal geliştirici hesabınızı PayPal ile doğrulamanız gerekebilir. E-posta hesabınıza PayPal tarafından gönderilen adımları izleyerek hesabınızı doğrulayabilirsiniz. PayPal geliştirici Hesabınızı doğruladıktan sonra PayPal geliştirici testi sitesine tekrar oturum açın.
4. PayPal geliştirici hesabınızla PayPal geliştirici sitesinde oturum açtıktan sonra, henüz yoksa bir PayPal alıcı test hesabı oluşturmanız gerekir. Bir alıcı testi hesabı oluşturmak için, PayPal sitesinde **uygulamalar** sekmesine tıklayın ve ardından **Sandbox hesapları**' na tıklayın.   
 **Korumalı alan test hesapları** sayfası gösterilir.   

    > [!NOTE] 
    > 
    > PayPal geliştirici sitesi zaten bir ticari test hesabı sağlar.

    ![PayPal-Sandbox test hesaplarıyla kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image15.png)
5. Korumalı alan test hesapları sayfasında **Hesap oluştur**' a tıklayın.
6. **Test hesabı oluştur** sayfasında, seçtiğiniz bir alıcı testi hesabı e-postası ve parolası seçin.   

    > [!NOTE] 
    > 
    > Bu öğreticinin sonunda Wingtip Toys örnek uygulamasını test etmek için alıcı e-posta adresleri ve parolasına ihtiyacınız olacak.

    ![PayPal-Sandbox test hesaplarıyla kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image16.png)
7. **Hesap oluştur** düğmesine tıklayarak Satınalmacı testi hesabını oluşturun.  
 **Korumalı alan test hesapları** sayfası görüntülenir. 

    ![PayPal-PayPal hesaplarıyla kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image17.png)
8. **Sandbox test hesapları** sayfasında, **kolaylaştırıcısı** e-posta hesabına tıklayın.  
    **Profil** ve **bildirim** seçenekleri görüntülenir.
9. **Profil** seçeneğini belirleyin, ardından, ticari test HESABıNA yönelik API kimlik bilgilerinizi görüntülemek için **API kimlik bilgileri** ' ne tıklayın.
10. TEST API kimlik bilgilerini Not defteri 'ne kopyalayın.

Wingtip Toys örnek uygulamasından PayPal sınama ortamına API çağrıları yapmak için, görüntülenmiş, klasik TEST API kimlik bilgileriniz (Kullanıcı adı, parola ve Imza) gerekir. Bir sonraki adımda kimlik bilgilerini ekleyeceksiniz.

### <a name="add-paypal-class-and-api-credentials"></a>PayPal sınıfı ve API kimlik bilgileri ekleme

PayPal kodunun çoğunluğunu tek bir sınıfa yerleştirebilirsiniz. Bu sınıf, PayPal ile iletişim kurmak için kullanılan yöntemleri içerir. Ayrıca, bu sınıfa PayPal kimlik bilgilerinizi eklersiniz.

1. Visual Studio içindeki Wingtip Toys örnek uygulamasında, **Logic** Folder öğesine sağ tıklayın ve ardından **yeni öğe**&gt; -**Ekle** ' yi seçin.   
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Soldaki **yüklü** bölmeden **görsel C#**  ' ün altında **kod**' u seçin.
3. Orta bölmeden **sınıf**' ı seçin. Bu yeni sınıfı **PayPalFunctions.cs**olarak adlandırın.
4. **Ekle**'yi tıklatın.  
   Yeni sınıf dosyası düzenleyicide görüntülenir.
5. Varsayılan kodu şu kodla değiştirin:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. Bu öğreticide daha önce görüntülenen ticari API kimlik bilgilerini (Kullanıcı adı, parola ve Imza) ekleyerek PayPal sınama ortamına işlev çağrıları yapabilirsiniz.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> Bu örnek uygulamada, bir C# dosyaya (. cs) kimlik bilgilerini eklemeniz yeterlidir. Ancak, uygulanan bir çözümde, kimlik bilgilerinizi bir yapılandırma dosyasında şifrelemeyi göz önünde bulundurmanız gerekir.

NVPAPICaller sınıfı, PayPal işlevselliğinin çoğunu içerir. Sınıftaki kod, PayPal test ortamından bir test satın alımı yapmak için gereken yöntemleri sağlar. Aşağıdaki üç PayPal işlevi satın alma işlemleri yapmak için kullanılır:

- `SetExpressCheckout` işlevi
- `GetExpressCheckoutDetails` işlevi
- `DoExpressCheckoutPayment` işlevi

`ShortcutExpressCheckout` yöntemi, alışveriş sepetinden test satın alma bilgilerini ve ürün ayrıntılarını toplar ve `SetExpressCheckout` PayPal işlevini çağırır. `GetCheckoutDetails` yöntemi, satın alma ayrıntılarını onaylar ve test satın almadan önce `GetExpressCheckoutDetails` PayPal işlevini çağırır. `DoCheckoutPayment` yöntemi, sınama ortamından `DoExpressCheckoutPayment` PayPal işlevini çağırarak test satın alma işlemini tamamlar. Geri kalan kod, kodlama dizeleri, kod çözme, dizileri işleme ve kimlik bilgilerini belirleme gibi PayPal yöntemlerini ve sürecini destekler.

> [!NOTE] 
> 
> PayPal, [PayPal 'ın API belirtimine](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout)göre isteğe bağlı satın alma ayrıntıları eklemenizi sağlar. Wingtip Toys örnek uygulamasındaki kodu genişleterek, yerelleştirme ayrıntılarını, ürün açıklamalarını, vergiyi, müşteri hizmetleri numarasını ve diğer birçok isteğe bağlı alanı ekleyebilirsiniz.

**Shortcutexpresscheckout** yönteminde belirtilen return ve Cancel URL 'lerinin bir bağlantı noktası numarası kullandığına dikkat edin.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Visual Web Developer, SSL kullanarak bir Web projesi çalıştırdığında, genellikle 44300 numaralı bağlantı noktası Web sunucusu için kullanılır. Yukarıda gösterildiği gibi, bağlantı noktası numarası 44300 ' dir. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görebilirsiniz. Bu öğreticinin sonunda Wingtip Toys örnek uygulamasını çalıştırabilmeniz için bağlantı noktası numaranız kodda doğru şekilde ayarlanmalıdır. Bu öğreticinin sonraki bölümünde, yerel ana bilgisayar bağlantı noktası numarasını alma ve PayPal sınıfını güncelleştirme işlemleri açıklanmaktadır.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>PayPal sınıfındaki LocalHost bağlantı noktası numarasını güncelleştirme

Wingtip Toys örnek uygulaması, PayPal test sitesine giderek ve Wingtip Toys örnek uygulamasının yerel örneğine dönerek ürünleri satın alır. PayPal 'in doğru URL 'ye dönmesi için yukarıda bahsedilen PayPal kodunda yerel olarak çalışan örnek uygulamanın bağlantı noktası numarasını belirtmeniz gerekir.

1. **Çözüm Gezgini** içindeki proje adına (**wingtiptoys**) sağ tıklayın ve **Özellikler**' i seçin.
2. Sol sütunda **Web** sekmesini seçin.
3. **Proje URL 'si** kutusundan bağlantı noktası numarasını alın.
4. Gerekirse, Web uygulamanızın bağlantı noktası numarasını kullanmak için *PayPalFunctions.cs* dosyasındaki PayPal sınıfındaki (`NVPAPICaller`) `returnURL` ve `cancelURL` güncelleştirin:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

Artık eklediğiniz kod, yerel Web uygulamanız için beklenen bağlantı noktasıyla eşleşmeyecektir. PayPal, yerel makinenizde doğru URL 'ye geri dönebilecektir.

### <a name="add-the-paypal-checkout-button"></a>PayPal kullanıma alma düğmesini ekleme

Artık birincil PayPal işlevleri örnek uygulamaya eklendiğine göre, bu işlevleri çağırmak için gereken biçimlendirme ve kodu eklemeye başlayabilirsiniz. İlk olarak, kullanıcının alışveriş sepeti sayfasında göreceği kullanıma al düğmesini eklemeniz gerekir.

1. *ShoppingCart. aspx* dosyasını açın.
2. Dosyanın en altına gidin ve `<!--Checkout Placeholder -->` yorumu bulun.
3. `ImageButton` bir denetim ile değiştirin, böylece işaret aşağıdaki şekilde değiştirilir:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. *ShoppingCart.aspx.cs* dosyasında, dosyanın sonuna yakın `UpdateBtn_Click` olay işleyicisinden sonra, `CheckOutBtn_Click` olay işleyicisini ekleyin:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. Ayrıca, *ShoppingCart.aspx.cs* dosyasında, yeni görüntü düğmesine aşağıdaki gibi başvurulması için `CheckoutBtn`bir başvuru ekleyin:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. Değişikliklerinizi hem *ShoppingCart. aspx* dosyasına hem de *ShoppingCart.aspx.cs* dosyasına kaydedin.
7. Menüden **Debug**-&gt;**Build wingtiptoys**' u seçin.  
   Proje, yeni eklenen **ImageButton** denetimi ile yeniden oluşturulacak.

### <a name="send-purchase-details-to-paypal"></a>PayPal 'e satın alma ayrıntılarını gönder

Kullanıcı alışveriş sepeti sayfasındaki (*ShoppingCart. aspx*) **kullanıma al** düğmesine tıkladığında, satın alma işlemini başlatır. Aşağıdaki kod, ürünleri satın almak için gereken ilk PayPal işlevini çağırır.

1. *Kullanıma alma* klasöründen, *CheckoutStart.aspx.cs*adlı arka plan kod dosyasını açın.   
   Arka plan kod dosyasını açmayı unutmayın.
2. Mevcut kodu şu kodla değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

Uygulamanın kullanıcısı alışveriş sepeti sayfasındaki **kullanıma al** düğmesine tıkladığında tarayıcı *Checkoutstart. aspx* sayfasına gider. *Checkoutstart. aspx* sayfası yüklendiğinde `ShortcutExpressCheckout` yöntemi çağrılır. Bu noktada, Kullanıcı PayPal testi Web sitesine aktarılır. PayPal sitesinde, Kullanıcı PayPal kimlik bilgilerini girer, satın alma ayrıntılarını inceler, PayPal anlaşmasını kabul eder ve `ShortcutExpressCheckout` yönteminin tamamlandığı Wingtip Toys örnek uygulamasına geri döner. `ShortcutExpressCheckout` yöntemi tamamlandığında, kullanıcıyı `ShortcutExpressCheckout` yönteminde belirtilen *Checkoutreview. aspx* sayfasına yönlendirir. Bu, kullanıcının, Wingtip Toys örnek uygulaması içinden sipariş ayrıntılarını incelemesine olanak sağlar.

### <a name="review-order-details"></a>Sipariş ayrıntılarını gözden geçirme

PayPal 'den döndükten sonra, Wingtip Toys örnek uygulamasının *Checkoutreview. aspx* sayfası, sipariş ayrıntılarını görüntüler. Bu sayfa, kullanıcının ürünleri satın almadan önce sipariş ayrıntılarını incelemesine olanak sağlar. *Checkoutreview. aspx* sayfası şu şekilde oluşturulmalıdır:

1. *Kullanıma al* klasöründe, *Checkoutreview. aspx*adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. *CheckoutReview.aspx.cs* adlı arka plan kod sayfasını açın ve mevcut kodu şu kodla değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

**DetailsView** denetimi, PayPal 'den döndürülen sıra ayrıntılarını göstermek için kullanılır. Ayrıca, yukarıdaki kod, düzen ayrıntılarını Wingtip Toys veritabanına `OrderDetail` nesnesi olarak kaydeder. Kullanıcı, **Tüm siparişi** düğmesine tıkladığında, *Checkouttamamlanmıştır. aspx* sayfasına yönlendirilir.

> [!NOTE] 
> 
> **İpucuyla**
> 
> *Checkoutreview. aspx* sayfasının biçimlendirmesinde, sayfanın alt kısmındaki **DetailsView** denetimindeki öğelerin stilini değiştirmek için `<ItemStyle>` etiketinin kullanıldığına dikkat edin. Sayfayı **Tasarım görünümünde** görüntüleyerek (Visual Studio 'nun sol alt köşesinde bulunan **Tasarım** ' ı seçerek), sonra **DetailsView** denetimini seçip **akıllı etiketi** (denetimin sağ üst köşesindeki ok simgesi) seçerek **DetailsView görevlerini**görebilirsiniz.
> 
> ![PayPal-düzenleme alanları ile kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image18.png)
> 
> **Alanları Düzenle**' yi seçerek **alanlar** iletişim kutusu görüntülenir. Bu iletişim kutusunda, **DetailsView** denetiminin **ItemStyle**gibi görsel özelliklerini kolayca kontrol edebilirsiniz.
> 
> ![PayPal alanları Iletişim kutusuyla kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>Satın alma tamamlamayı doldurun

*Checkouttamamlanmıştır. aspx* sayfası, satın almayı PayPal 'den yapar. Yukarıda bahsedildiği gibi, uygulamanın *Checkouttamamlanmıştır. aspx* sayfasına gidebilmesi Için kullanıcının **tüm sırayla** tıklamalıdır.

1. *Kullanıma al* klasöründe, *Checkouttamamlanmıştır. aspx*adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. *CheckoutComplete.aspx.cs* adlı arka plan kod sayfasını açın ve mevcut kodu şu kodla değiştirin:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

*Checkouttamamlanmıştır. aspx* sayfası yüklendiğinde `DoCheckoutPayment` yöntemi çağrılır. Daha önce belirtildiği gibi, `DoCheckoutPayment` yöntemi PayPal test ortamından satın almayı tamamlar. PayPal siparişi satın almayı tamamladıktan sonra, *Checkoutcompleted. aspx* sayfasında, satınalmacının bir ödeme işlemi `ID` görüntülenir.

### <a name="handle-cancel-purchase"></a>Satın almayı Iptal et

Kullanıcı satın alma işlemini iptal etmeye karar verirse, bunların sırası iptal edildiğini göreceği *Checkoutcancel. aspx* sayfasına yönlendirilir.

1. *Kullanıma alma* klasöründe *Checkoutcancel. aspx* adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>Satın alma hatalarını işleme

Satın alma işlemi sırasında oluşan hatalar *Checkouterror. aspx* sayfası tarafından işlenir. *Checkoutstart. aspx* sayfası, *Checkoutreview.* aspx sayfası ve *checkouttamamlamayı.* aspx sayfası her biri bir hata oluşursa *checkouterror. aspx* sayfasına yönlendirilir.

1. *Kullanıma alma* klasöründe *Checkouterror. aspx* adlı sayfayı açın.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

Kullanıma alma işlemi sırasında bir hata oluştuğunda *Checkouterror. aspx* sayfası hata ayrıntılarıyla görüntülenir.

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Ürünlerin nasıl satın alınacağını görmek için uygulamayı çalıştırın. PayPal test ortamında çalıştırmayacağınızı unutmayın. Gerçek para alışverişi yapılmaz.

1. Tüm dosyalarınızın Visual Studio 'Ya kaydedildiğinden emin olun.
2. Bir Web tarayıcısı açın ve [https://developer.paypal.com](https://developer.paypal.com/)gidin.
3. Bu öğreticide daha önce oluşturduğunuz PayPal geliştirici hesabınızla oturum açın.  
   PayPal 'in geliştirici korumalı alanı için, hızlı kullanıma almayı test etmek üzere [https://developer.paypal.com](https://developer.paypal.com/) adresinden oturum açmanız gerekir. Bu yalnızca PayPal 'in canlı ortamına değil, PayPal 'in korumalı alan testi için geçerlidir.
4. Visual Studio 'da, Wingtip Toys örnek uygulamasını çalıştırmak için **F5** tuşuna basın.  
   Veritabanı yeniden oluşturulduktan sonra tarayıcı açılır ve *varsayılan. aspx* sayfasını gösterir.
5. "Otomobiller" gibi ürün kategorisini seçerek ve ardından her ürünün yanındaki **Sepete Ekle** ' ye tıklayarak alışveriş sepetine üç farklı ürün ekleyin.  
   Alışveriş sepeti seçtiğiniz ürünü görüntüler.
6. Kullanıma almak için **PayPal** düğmesine tıklayın. 

    ![PayPal-sepet ile kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image20.png)

   Kullanıma alma, Wingtip Toys örnek uygulaması için bir kullanıcı hesabına sahip olmanızı gerektirir.
7. Mevcut bir gmail.com e-posta hesabıyla oturum açmak için sayfanın sağ tarafındaki **Google** bağlantısına tıklayın.  
   Bir gmail.com hesabınız yoksa, [www.gmail.com](https://www.gmail.com/)adresinde test amaçları için bir tane oluşturabilirsiniz. "Kaydet" i tıklayarak standart bir yerel hesap da kullanabilirsiniz. 

    ![PayPal-log ile kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image21.png)
8. Gmail hesabınızla ve parolanızla oturum açın. 

    ![PayPal-Gmail oturum açma ile kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image22.png)
9. Gmail hesabınızı Wingtip Toys örnek uygulaması kullanıcı adınızla kaydetmek için **oturum aç** düğmesine tıklayın. 

    ![PayPal-yazmaç hesabı ile kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image23.png)
10. PayPal sınama sitesinde, bu öğreticide daha önce oluşturduğunuz **alıcı** e-posta adresinizi ve parolanızı ekleyin ve **oturum aç** düğmesine tıklayın. 

    ![PayPal-PayPal oturum açma ile kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image24.png)
11. PayPal ilkesini kabul edin ve **kabul et ve devam et** düğmesine tıklayın.  
    Bu sayfanın yalnızca bu PayPal hesabını ilk kez kullandığınızda görüntülendiğini unutmayın. Bu, bir test hesabı olduğunu ve gerçek para değişimi olmadığını unutmayın. 

    ![PayPal-PayPal Ilkesiyle kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image25.png)
12. PayPal test ortamı incelemesi sayfasındaki sipariş bilgilerini gözden geçirin ve **devam**' a tıklayın. 

    ![PayPal Inceleme bilgileriyle kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image26.png)
13. *Checkoutreview. aspx* sayfasında, sipariş tutarını doğrulayın ve üretilen sevkiyat adresini görüntüleyin. Ardından, **siparişi Tamam** düğmesine tıklayın. 

    ![PayPal siparişi Incelemesinin kullanıma alınması ve ödemesi](checkout-and-payment-with-paypal/_static/image27.png)
14. **Checkouttamamlanmıştır. aspx** sayfası bir ödeme işlem kimliğiyle görüntülenir. 

    ![PayPal ile kullanıma alma ve ödeme-kullanıma alma Tamam](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>Veritabanını gözden geçirme

Uygulamayı çalıştırdıktan sonra Wingtip Toys örnek uygulama veritabanındaki güncelleştirilmiş verileri inceleyerek, uygulamanın ürün satın alma işleminden başarıyla kaydedildiğini görebilirsiniz.

Bu öğretici serisinde daha önce yaptığınız gibi, **veritabanı Gezgini** penceresini (Visual Studio 'da**Sunucu Gezgini** Window) kullanarak *wingtiptoys. mdf* veritabanı dosyasında yer alan verileri inceleyebilirsiniz.

1. Hala açıksa tarayıcı penceresini kapatın.
2. Visual Studio 'da, **uygulama\_veri** klasörünü genişletmenizi sağlamak için **Çözüm Gezgini** üstündeki **tüm dosyaları göster** simgesini seçin.
3. **Uygulama\_veri** klasörünü genişletin.  
 Klasör için **tüm dosyaları göster** simgesini seçmeniz gerekebilir.
4. *Wingtiptoys. mdf* veritabanı dosyasına sağ tıklayın ve **Aç**' ı seçin.  
    **Sunucu Gezgini** görüntülenir.
5. **Tablolar** klasörünü genişletin.
6. **Siparişler**tablosuna sağ tıklayıp **tablo verilerini göster**' i seçin.  
 **Orders** tablosu görüntülenir.
7. Başarılı işlemleri onaylamak için **Paymenttransactionıd** sütununu gözden geçirin. 

    ![PayPal-Inceleme veritabanıyla kullanıma alma ve ödeme](checkout-and-payment-with-paypal/_static/image29.png)
8. **Siparişler** Tablosu penceresini kapatın.
9. Sunucu Gezgini, **OrderDetails** tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.
10. **OrderDetails** tablosundaki `OrderId` ve `Username` değerlerini gözden geçirin. Bu değerlerin **Orders** tablosuna dahil olan `OrderId` ve `Username` değerleriyle eşleştiğini unutmayın.
11. **OrderDetails** Tablosu penceresini kapatın.
12. Wingtip Toys veritabanı dosyasına (*wingtiptoys. mdf*) sağ tıklayın ve **Bağlantıyı kapat**' ı seçin.
13. **Çözüm Gezgini** penceresini görmüyorsanız, **Çözüm Gezgini** yeniden göstermek için **Sunucu Gezgini** penceresinin altındaki **Çözüm Gezgini** ' e tıklayın.

## <a name="summary"></a>Özet

Bu öğreticide ürünlerin satın alınmasını izlemek için sipariş ve sipariş ayrıntısı şemaları eklediniz. Ayrıca, PayPal işlevlerini Wingtip Toys örnek uygulamasına de tümleştirmiş olursunuz.

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET yapılandırmasına genel bakış](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Üyelik, OAuth ve SQL veritabanı ile güvenli bir ASP.NET Web Forms uygulamasını dağıtın Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure Ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>Sorumluluk reddi

Bu öğretici örnek kod içerir. Bu tür örnek kod, her türlü garanti verilmeden "olduğu gibi" sağlanır. Buna uygun olarak, Microsoft örnek kodun doğruluğunu, bütünlüğünü veya kalitesini garanti etmez. Örnek kodu kendi sorumluluğunuzdadır kullanmayı kabul etmiş olursunuz. Hiçbir koşulda, Microsoft herhangi bir örnek kod, içerik ya da bunlarla sınırlı olmamak kaydıyla, herhangi bir örnek kodda, içerikte veya herhangi bir kayıp ya da herhangi bir örnek kodun kullanılması sonucunda oluşan herhangi bir kayıp veya hasar bozulması dahil herhangi bir şekilde size tabi olmaz. İşbu olarak size bildirimde bulunulduğundan, Microsoft zararlarından herhangi birini ve tüm kayıpları, kaybı, yaralanma veya zarardan herhangi bir türden doğan, kayıp, yok etme ya da zarar verme içinde ifade edilen görünümleri iletme, kullanma veya bunlarla sınırlı olmamak için kullanın.

> [!div class="step-by-step"]
> [Önceki](shopping-cart.md)
> [İleri](membership-and-administration.md)
