---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Windows Phone 8 uygulamasından Web API 'SI çağırma (C#)-ASP.NET 4. x
author: rmcmurray
description: 'Kod ile öğretici: ASP.NET 4. x içinde bir Windows Phone 8 uygulamasına kitapların kataloğunu sağlayan bir ASP.NET Web API uygulaması oluşturun.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614739"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a>Windows Phone 8 Uygulamasından Web API'sine Çağrı Yapma (C#)

[Robert McMurray](https://github.com/rmcmurray) tarafından

Bu öğreticide, Windows Phone 8 uygulamasına kitap kataloğu sağlayan bir ASP.NET Web API uygulamasından oluşan tam uçtan uca bir senaryo oluşturmayı öğreneceksiniz.

### <a name="overview"></a>Genel bakış

ASP.NET Web API gibi yeniden ESUIT Hizmetleri, sunucu tarafı ve istemci tarafı uygulamalar için mimari soyutlayarak geliştiriciler için HTTP tabanlı uygulamaların oluşturulmasını basitleştirir. Web API geliştiricilerin, iletişim için özel bir soket tabanlı protokol oluşturmak yerine yalnızca uygulama için önkoşul HTTP yöntemlerini yayımlaması gerekir (örneğin: GET, POST, PUT, DELETE) ve istemci uygulama geliştiricilerinin yalnızca kullanması gerekir uygulamaları için gerekli olan HTTP yöntemleri.

Bu uçtan uca öğreticide, Web API 'sini kullanarak aşağıdaki projeleri oluşturma hakkında bilgi edineceksiniz:

- [Bu öğreticinin ilk bölümünde](#STEP1), bir kitap kataloğunu yönetmek Için tüm oluşturma, okuma, güncelleştirme ve SILME (CRUD) işlemlerini destekleyen bir ASP.NET Web API uygulaması oluşturacaksınız. Bu uygulama, MSDN 'den [örnek xml dosyasını (Books. xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) kullanacaktır.
- [Bu öğreticinin ikinci bölümünde](#STEP2), Web API uygulamanızdan verileri alan etkileşimli bir Windows Phone 8 uygulaması oluşturacaksınız.

#### <a name="prerequisites"></a>Önkoşullar

- Windows Phone 8 SDK yüklü Visual Studio 2013
- Hyper-V yüklü 64 bitlik bir sistemde Windows 8 veya üzeri
- Ek gereksinimlerin listesi için [WINDOWS Phone SDK 8,0](https://www.microsoft.com/download/details.aspx?id=35471) Indirme sayfasındaki *sistem gereksinimleri* bölümüne bakın.

> [!NOTE]
> Yerel sisteminizdeki Web API 'SI ve Windows Phone 8 projeleri arasındaki bağlantıyı test etecekseniz, test ortamınızı ayarlamak için *[Windows Phone 8 öykünücüsünü yerel bir bilgisayarda Web API uygulamalarına bağlama](https://go.microsoft.com/fwlink/?LinkId=324014)* makalesindeki yönergeleri izlemeniz gerekir.

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>1\. Adım: Web API kitaplığı projesi oluşturma

Bu uçtan uca öğreticinin ilk adımı, tüm CRUD işlemlerini destekleyen bir Web API projesi oluşturmaktır; Bu öğreticinin [Adım 2](#STEP2) ' de bu çözüme Windows Phone uygulama projesini ekleneceğini unutmayın.

1. **Visual Studio 2013**açın.
2. **Dosya**ve ardından **Yeni**' ye ve ardından **Proje**' ye tıklayın.
3. **Yeni proje** iletişim kutusu görüntülendiğinde, **yüklü**' i, ardından **Şablonlar** **' C#ı ve** ardından **Web**' i genişletin.

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                Genişletmek için görüntü öğesine tıklayın                                                                |

4. **ASP.NET Web uygulamasını**vurgulayın, proje adı için **kitaplığı** girin ve ardından **Tamam**' a tıklayın.
5. **Yeni ASP.NET projesi** iletişim kutusu görüntülendiğinde, **Web API** şablonunu seçin ve ardından **Tamam**' a tıklayın.

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                Genişletmek için görüntü öğesine tıklayın                                                                |

6. Web API projesi açıldığında, projeden örnek denetleyiciyi kaldırın:

    1. Çözüm Gezgini ' nde **denetleyiciler** klasörünü genişletin.
    2. **ValuesController.cs** dosyasına sağ tıklayın ve ardından **Sil**' e tıklayın.
    3. Silmeyi onaylamanız istendiğinde **Tamam** ' a tıklayın.
7. Web API projesine bir XML veri dosyası ekleyin; Bu dosya, kitaplığı kataloğunun içeriğini içerir:

   1. Çözüm Gezgini ' nde **uygulama\_veri** klasörüne sağ tıklayın, ardından **Ekle**' ye ve ardından **Yeni öğe**' ye tıklayın.
   2. **Yeni öğe Ekle** iletişim kutusu görüntülendiğinde, **XML dosya** şablonunu vurgulayın.
   3. Dosyayı **Books. xml**olarak adlandırın ve **Ekle**' ye tıklayın.
   4. **Books. xml** dosyası AÇıLDıĞıNDA, MSDN 'deki örnek **kitaplar. xml** dosyasındaki dosyadaki kodu XML ile değiştirin: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. XML dosyasını kaydedin ve kapatın.

8. Kitaplığı modelini Web API projesine ekleyin; Bu model, kitaplığı uygulaması için oluşturma, okuma, güncelleştirme ve silme (CRUD) mantığını içerir:

   1. Çözüm Gezgini ' nde **modeller** klasörüne sağ tıklayın, ardından **Ekle**' ye ve ardından **sınıf**' a tıklayın.
   2. **Yeni öğe Ekle** iletişim kutusu görüntülendiğinde, sınıf dosyasını **BookDetails.cs**olarak adlandırın ve **Ekle**' ye tıklayın.
   3. **BookDetails.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. **BookDetails.cs** dosyasını kaydedin ve kapatın.

9. Kitaplığı denetleyicisi 'ni Web API projesine ekleyin:

   1. Çözüm Gezgini ' nde **denetleyiciler** klasörüne sağ tıklayın, ardından **Ekle**' ye tıklayın ve ardından **Denetleyici**' ye tıklayın.
   2. **Yapı Iskelesi Ekle** iletişim kutusu görüntülendiğinde, **Web API 2 denetleyici-boş**' ı vurgulayın ve **Ekle**' ye tıklayın.
   3. **Denetleyici Ekle** iletişim kutusu görüntülendiğinde, denetleyici **bookscontroller**adını adlandırın ve ardından **Ekle**' ye tıklayın.
   4. **BooksController.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. **BooksController.cs** dosyasını kaydedin ve kapatın.

10. Hataları denetlemek için Web API uygulaması oluşturun.

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>2\. Adım: Windows Phone 8 kitaplığı Katalog projesini ekleme

Bu uçtan uca senaryonun sonraki adımı, Windows Phone 8 için katalog uygulaması oluşturmaktır. Bu uygulama, varsayılan kullanıcı arabirimi için *Windows Phone veri bağlama uygulama* şablonunu kullanır ve veri kaynağı olarak Bu öğreticinin [1. ADıMıNDA](#STEP1) oluşturduğunuz Web API uygulamasını kullanır.

1. Çözüm Gezgini ' nde bulunan **kitaplığı** çözümüne sağ tıklayın, ardından **Ekle**' ye ve ardından **Yeni proje**' ye tıklayın.
2. **Yeni proje** iletişim kutusu görüntülendiğinde, **yüklü**' i ve ardından **görsel C#** ' i genişletin ve ardından **Windows Phone**.
3. **Windows Phone veriye bağlı uygulamayı**vurgulayın, ad Için **bookcatalog** girin ve ardından **Tamam**' a tıklayın.
4. Json.NET NuGet paketini **Bookcatalog** projesine ekleyin:

    1. Çözüm Gezgini ' nde **Bookcatalog** projesi için **Başvurular** ' a sağ tıklayın ve ardından **NuGet Paketlerini Yönet**' e tıklayın.
    2. **NuGet Paketlerini Yönet** iletişim kutusu görüntülendiğinde, **çevrimiçi** bölümünü genişletin ve **NuGet.org**vurgulayın.
    3. Arama alanına **JSON.net** girin ve arama simgesine tıklayın.
    4. Arama sonuçlarında **JSON.net** vurgulayın ve ardından **Install**' a tıklayın.
    5. Yükleme tamamlandığında **Kapat**' a tıklayın.
5. Bookdetails modelini **bookcatalog** projesine ekleyin; Bu, kitaplığı sınıfının genel bir modelini içerir:

   1. Çözüm Gezgini ' nde **Bookcatalog** projesine sağ tıklayın, ardından **Ekle**' ye ve ardından **Yeni klasör**' e tıklayın.
   2. Yeni klasör **modellerini**adlandırın.
   3. Çözüm Gezgini ' nde **modeller** klasörüne sağ tıklayın, ardından **Ekle**' ye ve ardından **sınıf**' a tıklayın.
   4. **Yeni öğe Ekle** iletişim kutusu görüntülendiğinde, sınıf dosyasını **BookDetails.cs**olarak adlandırın ve **Ekle**' ye tıklayın.
   5. **BookDetails.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. **BookDetails.cs** dosyasını kaydedin ve kapatın.

6. **MainViewModel.cs** sınıfını, KITAPLıĞı Web API uygulamasıyla iletişim kuracak işlevselliği içerecek şekilde güncelleştirin:

   1. Çözüm Gezgini ' nde **Viewmodeller** klasörünü genişletin ve ardından **MainViewModel.cs** dosyasına çift tıklayın.
   2. **MainViewModel.cs** dosyası açıldığında, dosyadaki kodu aşağıdaki kodla değiştirin; `apiUrl` sabitinin değerini, Web API 'nizin gerçek URL 'siyle güncelleştirmeniz gerektiğini unutmayın: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. **MainViewModel.cs** dosyasını kaydedin ve kapatın.

7. **MainPage. xaml** dosyasını, uygulama adını özelleştirmek için güncelleştirin:

   1. Çözüm Gezgini 'nde **MainPage. xaml** dosyasına çift tıklayın.
   2. **MainPage. xaml** dosyası açıldığında aşağıdaki kod satırlarını bulun: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. Bu satırları aşağıdakiler ile değiştirin: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. **MainPage. xaml** dosyasını kaydedin ve kapatın.

8. Görüntülenecek öğeleri özelleştirmek için **Ayrıntılar Page. xaml** dosyasını güncelleştirin:

   1. Çözüm Gezgini 'nde, **Ayrıntılar Page. xaml** dosyasına çift tıklayın.
   2. **Ayrıntılar Page. xaml** dosyası açıldığında aşağıdaki kod satırlarını bulun: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. Bu satırları aşağıdakiler ile değiştirin: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. **Ayrıntılar Page. xaml** dosyasını kaydedin ve kapatın.

9. Hataları denetlemek için Windows Phone uygulamayı derleyin.

### <a name="step-3-testing-the-end-to-end-solution"></a>3\. Adım: uçtan uca çözümü test etme

Bu öğreticinin *Önkoşullar* bölümünde belirtildiği gibi, yerel sisteminizdeki Web API 'si ve Windows Phone 8 projeleri arasındaki bağlantıyı sınarken, test ortamınızı ayarlamak için *[Windows Phone 8 öykünücüsünü yerel BIR bilgisayardaki Web API uygulamalarına bağlama](https://go.microsoft.com/fwlink/?LinkId=324014)* makalesindeki yönergeleri izlemeniz gerekir.

Test ortamı yapılandırıldıktan sonra, Windows Phone uygulamasını başlangıç projesi olarak ayarlamanız gerekecektir. Bunu yapmak için, Çözüm Gezgini ' nde **Bookcatalog** uygulamasını vurgulayın ve ardından **Başlangıç projesi olarak ayarla**' ya tıklayın:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| Genişletmek için görüntü öğesine tıklayın |

F5 tuşuna bastığınızda, Visual Studio her iki Windows Phone öykünücüyü başlatır ve &quot;bu, uygulama verileri Web API 'sinden alınırken&quot; ileti bekleyin:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| Genişletmek için görüntü öğesine tıklayın |

Her şey başarılı olursa kataloğun görüntülendiğini görmeniz gerekir:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| Genişletmek için görüntü öğesine tıklayın |

Herhangi bir kitap başlığına dokunduğunuzda, uygulama kitap açıklamasını görüntüler:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| Genişletmek için görüntü öğesine tıklayın |

Uygulama Web API 'niz ile iletişim kuramıyorsa, bir hata iletisi görüntülenir:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| Genişletmek için görüntü öğesine tıklayın |

Hata iletisine dokunduğunuzda, hatayla ilgili ek ayrıntılar görüntülenir:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 Genişletmek için görüntü öğesine tıklayın                                                                 |
