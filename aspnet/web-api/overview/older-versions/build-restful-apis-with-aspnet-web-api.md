---
uid: web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
title: ASP.NET Web API 'SI ile yeniden takip eden API 'Ler oluşturun-ASP.NET 4. x
author: rick-anderson
description: "Uygulamalı laboratuvar: bir Contact Manager uygulaması için basit bir REST API derlemek için ASP.NET 4. x içindeki Web API 'sini kullanın."
ms.author: riande
ms.date: 02/18/2013
ms.custom: seoapril2019
ms.assetid: 87daa99f-3810-407e-b969-dd28a192959d
msc.legacyurl: /web-api/overview/older-versions/build-restful-apis-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 35b115d6b4f84084e78e429bbb4842670e57bba4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621816"
---
# <a name="build-restful-apis-with-aspnet-web-api"></a>ASP.NET Web API 'SI ile yeniden takip eden API 'Ler oluşturun

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

> Uygulamalı laboratuvar: bir Contact Manager uygulaması için basit bir REST API derlemek için ASP.NET 4. x içindeki Web API 'sini kullanın. Ayrıca API 'yi kullanmak için bir istemci oluşturacaksınız.

Son yıllarda, HTTP 'nin yalnızca HTML sayfaları sunmak için değil net ' in açık olması gerekir. Ayrıca, Web API 'Leri oluşturmaya yönelik güçlü bir platformdur, bir dizi fiil (GET, POST, vb.) ve *URI 'ler* ve *üstbilgiler*gibi birkaç basit kavram vardır. ASP.NET Web API 'SI, HTTP programlamasını basitleştiren bir bileşen kümesidir. ASP.NET MVC çalışma zamanının üzerine inşa edildiğinden, Web API 'SI, HTTP 'nin alt düzey aktarım ayrıntılarını otomatik olarak işler. Aynı zamanda, Web API 'SI HTTP programlama modelini doğal olarak kullanıma sunar. Aslında, Web API 'sinin bir hedefi HTTP 'nin gerçekliği dışında bir amaç *değildir* . Sonuç olarak, Web API 'sinin her ikisi de esnektir ve kolayca genişletilir.  REST mimari stili HTTP 'den yararlanmak için etkili bir yöntem olarak kendini kanıtlamış ve HTTP için geçerli tek yaklaşım olmasa da İlgili kişi Yöneticisi, diğer kişiler arasında kişileri listelemek, eklemek ve kaldırmak için bir daha sunacaktır. 

Bu laboratuvar, HTTP, REST ve temel bir HTML, JavaScript ve jQuery hakkında temel bir bilginiz olduğunu varsaymaktadır.
> 
> > [!NOTE]
> > ASP.NET Web sitesi, [https://asp.net/web-api](https://asp.net/web-api)ADRESINDEKI Web API çerçevesine adanmış bir alana sahiptir. Bu site, Web API 'siyle ilgili en son bilgileri, örnekleri ve haberleri sağlamaya devam edecek, bu nedenle neredeyse tüm cihazlar veya geliştirme çerçevesiyle sunulan özel Web API 'Leri oluşturma sanatı hakkında daha ayrıntılı bilgi almak istiyorsanız, sık sık kontrol edin.
> > 
> > ASP.NET MVC 4 ' e benzer ASP.NET Web API 'SI, hizmet katmanını denetleyicilerden ayırmak açısından çok daha fazla esneklik sağlar. Bu, kullanılabilir bağımlılık ekleme çerçevelerinin birkaçını oldukça kolay kullanmanıza olanak tanır. MSDN 'de, [buradan](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)yükleyebileceğiniz bir ASP.NET Web API projesinde bağımlılık ekleme Için neklemesine nasıl kullanacağınızı gösteren iyi bir örnek vardır.
> 
> 
> Tüm örnek kod ve kod parçacıkları [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Yeniden takip eden bir Web API 'SI uygulama
- Bir HTML istemcisinden API çağırma

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek B](#AppendixB) 'yi okuyun).

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

**Kod parçacıklarını yükleme**

Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır. Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek istiyorsanız, [Ek A: Ek A: kod parçacıkları&quot;kullanarak](#AppendixA) bu &quot;belgedeki eke başvurabilirsiniz.

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki Alıştırmayı içerir:

1. [Alıştırma 1: salt okunurdur Web API 'SI oluşturma](#Exercise1)
2. [Alıştırma 2: okuma/yazma Web API 'SI oluşturma](#Exercise2)
3. [Alıştırma 3: bir HTML Istemcisinden Web API 'sini kullanma](#Exercise3)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Create_a_Read-Only_Web_API"></a>
### <a name="exercise-1-create-a-read-only-web-api"></a>Alıştırma 1: salt okunurdur Web API 'SI oluşturma

Bu alıştırmada, Contact Manager için salt okunurdur GET yöntemlerini uygulayacaksınız.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_API_Project"></a>
#### <a name="task-1---creating-the-api-project"></a>Görev 1-API projesi oluşturma

Bu görevde, yeni ASP.NET Web projesi şablonlarını kullanarak bir Web API web uygulaması oluşturacaksınız.

1. **Web Için Visual Studio 2012 Express**'i çalıştırın. bunu yapmak için **başlat** 'a gidip **Web için vs Express** yazın ve **ENTER**tuşuna basın.
2. **Dosya** menüsünden **Yeni proje**' yi seçin. **Görseli C# seçin |** Proje türü ağaç görünümünden Web projesi türü, sonra **ASP.NET MVC 4 Web uygulaması** proje türünü seçin. Projenin **adını** *ContactManager* , **çözüm adı** olarak ayarlayın ve ardından **Tamam**'a tıklayın.

    ![Yeni bir ASP.NET MVC 4,0 Web uygulaması projesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image1.png "Yeni bir ASP.NET MVC 4,0 Web uygulaması projesi oluşturma")

    *Yeni bir ASP.NET MVC 4,0 Web uygulaması projesi oluşturma*
3. ASP.NET MVC 4 proje türü iletişim kutusunda **Web API 'si** proje türünü seçin. **Tamam**’a tıklayın.

    ![Web API proje türünü belirtme](build-restful-apis-with-aspnet-web-api/_static/image2.png "Web API proje türünü belirtme")

    *Web API proje türünü belirtme*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_the_Contact_Manager_API_Controllers"></a>
#### <a name="task-2---creating-the-contact-manager-api-controllers"></a>Görev 2-Contact Manager API denetleyicileri oluşturma

Bu görevde API yöntemlerinin bulunacağı denetleyici sınıflarını oluşturacaksınız.

1. **ValuesController.cs** adlı dosyayı **denetleyiciler** klasöründe projeden silin.
2. Projedeki **denetleyiciler** klasörüne sağ tıklayın ve Ekle ' yi seçin **|** Bağlam menüsünden denetleyici.

    ![Projeye yeni bir denetleyici ekleniyor](build-restful-apis-with-aspnet-web-api/_static/image3.png "Projeye yeni bir denetleyici ekleniyor")

    *Projeye yeni bir denetleyici ekleniyor*
3. Görüntülenen **Denetleyici Ekle** iletişim kutusunda, şablon menüsünden **boş API denetleyicisi** ' ni seçin. Denetleyici sınıfına **contactcontroller**adını adlandırın. Ardından Ekle ' ye tıklayın **.**

    ![Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma](build-restful-apis-with-aspnet-web-api/_static/image4.png "Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma")

    *Yeni bir Web API denetleyicisi oluşturmak için denetleyici Ekle iletişim kutusunu kullanma*
4. **Contactcontroller**'a aşağıdaki kodu ekleyin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex01-Get API yöntemi*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample1.cs)]
5. Uygulamada hata ayıklamak için **F5**’e basın. Bir Web API projesi için varsayılan giriş sayfası görünmelidir.

    ![Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası](build-restful-apis-with-aspnet-web-api/_static/image5.png "Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası")

    *Bir ASP.NET Web API uygulamasının varsayılan giriş sayfası*
6. Internet Explorer penceresinde, **Geliştirici Araçları** penceresini açmak için **F12** tuşuna basın. **Ağ** sekmesine tıklayın ve ardından, pencereye ağ trafiği yakalamaya başlamak Için **Yakalamayı Başlat** düğmesine tıklayın.

    ![Ağ sekmesini açma ve ağ yakalamayı başlatma](build-restful-apis-with-aspnet-web-api/_static/image6.png "Ağ sekmesini açma ve ağ yakalamayı başlatma")

    *Ağ sekmesini açma ve ağ yakalamayı başlatma*
7. Tarayıcının adres çubuğuna URL 'YI **/api/Contact** ile ekleyin ve ENTER tuşuna basın. İletim ayrıntıları ağ yakalama penceresinde görünür. Yanıtın MIME türünün **Application/JSON**olduğunu unutmayın. Bu, varsayılan çıkış biçiminin JSON olduğunu gösterir.

    ![Web API isteğinin çıkışını ağ görünümünde görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image7.png "Web API isteğinin çıkışını ağ görünümünde görüntüleme")

    *Web API isteğinin çıkışını ağ görünümünde görüntüleme*

    > [!NOTE]
    > Internet Explorer 10 ' un bu noktada varsayılan davranışı, kullanıcının Web API çağrısından kaynaklanan akışı kaydetmek veya açmak isteyip istememesini ister. Çıktı, Web API URL çağrısının JSON sonucunu içeren bir metin dosyası olacaktır. Yanıt içeriğini geliştiriciler araç penceresi aracılığıyla izleyebilmek için iletişim kutusunu iptal etme.
8. Bu API çağrısının yanıtı hakkında daha fazla ayrıntı görmek için **ayrıntılı görünüme git** düğmesine tıklayın.

    ![Ayrıntılı görünüme geç](build-restful-apis-with-aspnet-web-api/_static/image8.png "Ayrıntılar görünümüne geç")

    *Ayrıntılı görünüme geç*
9. Gerçek JSON yanıt metnini görüntülemek için **yanıt gövdesi** sekmesine tıklayın.

    ![Ağ izleyicisinde JSON çıkış metnini görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image9.png "Ağ izleyicisinde JSON çıkış metnini görüntüleme")

    *Ağ izleyicisinde JSON çıkış metnini görüntüleme*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Creating_the_Contact_Models_and_Augment_the_Contact_Controller"></a>
#### <a name="task-3---creating-the-contact-models-and-augment-the-contact-controller"></a>Görev 3-Iletişim modellerini oluşturma ve Iletişim denetleyicisi 'ni artırmak

Bu görevde API yöntemlerinin bulunacağı denetleyici sınıflarını oluşturacaksınız.

1. **Modeller** klasörüne sağ tıklayın ve Ekle ' yi seçin **| Sınıf...** bağlam menüsünden.

    ![Web uygulamasına yeni model ekleme](build-restful-apis-with-aspnet-web-api/_static/image10.png "Web uygulamasına yeni model ekleme")

    *Web uygulamasına yeni model ekleme*
2. **Yeni öğe Ekle** iletişim kutusunda yeni dosyayı **Contact.cs** olarak adlandırın ve Ekle ' ye tıklayın **.**

    ![Yeni kişi sınıfı dosyası oluşturuluyor](build-restful-apis-with-aspnet-web-api/_static/image11.png "Yeni kişi sınıfı dosyası oluşturuluyor")

    *Yeni kişi sınıfı dosyası oluşturuluyor*
3. Aşağıdaki Vurgulanan kodu **kişi** sınıfına ekleyin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex01-Contact sınıfı*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample2.cs)]
4. **Contactcontroller** sınıfında, **Get** yönteminin yöntem tanımında Word **dizesini** seçin ve Word *kişisi*yazın. Sözcük içine yazıldıktan sonra, sözcük **kişisinin**başlangıcında bir gösterge görüntülenir. **CTRL** tuşunu basılı tutun ve nokta (.) tuşuna basın ya da farenizi kullanarak, modeller ad alanı için **using** yönergesini otomatik olarak doldurmanız için farenizi kullanarak simge simgesine tıklayın.

    ![Ad alanı bildirimleri için IntelliSense yardımını kullanma](build-restful-apis-with-aspnet-web-api/_static/image12.png)

    *Ad alanı bildirimleri için IntelliSense yardımını kullanma*
5. **Get** yöntemi için kodu değiştirin, böylece bir iletişim modeli örnekleri dizisi döndürür.

    (Kod parçacığı- *Web API Laboratuvarı-Ex01-kişiler listesi döndürülüyor*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample3.cs)]
6. Tarayıcıdaki Web uygulamasında hata ayıklamak için **F5** tuşuna basın. API 'nin yanıt çıkışında yapılan değişiklikleri görüntülemek için aşağıdaki adımları gerçekleştirin.

   1. Tarayıcı açıldıktan sonra geliştirici araçları henüz açık değilse **F12** tuşuna basın.
   2. **Ağ** sekmesine tıklayın.
   3. **Yakalamayı Başlat** düğmesine basın.
   4. **/Api/Contact** URL sonekini adres çubuğundaki URL 'ye ekleyin ve **ENTER** tuşuna basın.
   5. **Ayrıntılı görünüme git** düğmesine basın.
   6. **Yanıt gövdesi** sekmesini seçin. Bir kişi örnekleri dizisinin seri hale getirilmiş formunu temsil eden bir JSON dizesi görmeniz gerekir.

      ![Karmaşık bir Web API yöntemi çağrısının JSON seri hale getirilmiş çıkışı](build-restful-apis-with-aspnet-web-api/_static/image13.png "Karmaşık bir Web API yöntemi çağrısının JSON seri hale getirilmiş çıkışı")

      *Karmaşık bir Web API yöntemi çağrısının JSON seri hale getirilmiş çıkışı*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Extracting_Functionality_into_a_Service_Layer"></a>
#### <a name="task-4---extracting-functionality-into-a-service-layer"></a>Görev 4-bir hizmet katmanına Işlevsellik ayıklama

Bu görev, geliştiricilerin hizmet işlevlerini denetleyici katmanından ayırmasını kolaylaştırmak için işlevselliği bir hizmet katmanına nasıl çıkarabileceğinizi gösterir ve böylelikle işi gerçekten yapan hizmetlerin yeniden kullanılabilirliğini sağlar.

1. Çözüm kökünde yeni bir klasör oluşturun ve BT **Hizmetleri**olarak adlandırın. Bunu yapmak için **ContactManager** projesi ' ne sağ tıklayın, **Yeni | klasör** **Ekle** ' yi seçin, BT *Hizmetleri*olarak adlandırın.

    ![Hizmetler klasörü oluşturuluyor](build-restful-apis-with-aspnet-web-api/_static/image14.png "Hizmetler klasörü oluşturuluyor")

    *Hizmetler klasörü oluşturuluyor*
2. **Hizmetler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Sınıf...** bağlam menüsünden.

    ![Hizmetler klasörüne yeni bir sınıf ekleniyor](build-restful-apis-with-aspnet-web-api/_static/image15.png "Hizmetler klasörüne yeni bir sınıf ekleniyor")

    *Hizmetler klasörüne yeni bir sınıf ekleniyor*
3. **Yeni öğe Ekle** iletişim kutusu göründüğünde, yeni sınıf **contactrepository** adını adlandırın ve **Ekle**' ye tıklayın.

    ![Kişi deposu hizmet katmanının kodunu içeren bir sınıf dosyası oluşturma](build-restful-apis-with-aspnet-web-api/_static/image16.png "Kişi deposu hizmet katmanının kodunu içeren bir sınıf dosyası oluşturma")

    *Kişi deposu hizmet katmanının kodunu içeren bir sınıf dosyası oluşturma*
4. Modeller ad alanını dahil etmek için **ContactRepository.cs** dosyasına bir using yönergesi ekleyin.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample4.cs)]
5. GetAllContacts metodunu uygulamak için aşağıdaki vurgulanmış kodu **ContactRepository.cs** dosyasına ekleyin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex01-Ilgili kişi deposu*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample5.cs)]
6. Zaten açık değilse, **ContactController.cs** dosyasını açın.
7. Aşağıdaki using ifadesini dosyanın ad alanı bildirimi bölümüne ekleyin.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample6.cs)]
8. Deponun örneğini temsil eden bir özel alan eklemek için **ContactController.cs** sınıfına aşağıdaki vurgulanmış kodu ekleyin. böylece, sınıf üyelerinin geri kalanı hizmet uygulamasını kullanabilir.

    (Kod parçacığı- *Web API Laboratuvarı-Ex01-Ilgili kişi denetleyicisi*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample7.cs)]
9. **Get** yöntemini, iletişim deposu hizmetini kullanacak şekilde değiştirin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex01-depo aracılığıyla kişiler listesi döndürülüyor*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample8.cs)]
10. **Contactcontroller**'ın **Get** yöntemi tanımına bir kesme noktası koyun.

   ![İletişim denetleyicisine kesme noktaları ekleme](build-restful-apis-with-aspnet-web-api/_static/image17.png "İletişim denetleyicisine kesme noktaları ekleme")

   *İletişim denetleyicisine kesme noktaları ekleme*
11. Uygulamayı çalıştırmak için **F5**'e basın.
12. Tarayıcı açıldığında, geliştirici araçlarını açmak için **F12** tuşuna basın.
13. **Ağ** sekmesine tıklayın.
14. **Yakalamayı Başlat** düğmesine tıklayın.
15. Adres çubuğuna URL 'YI **/api/Contact** sonekine ekleyin ve **ENTER** tuşuna basarak API denetleyicisini yükleyin.
16. **Get** yöntemi yürütülmeye başladıktan sonra Visual Studio 2012 ' i kesmeniz gerekir.

   ![Get yöntemi içinde kesme](build-restful-apis-with-aspnet-web-api/_static/image18.png "Get yöntemi içinde kesme")

   *Get yöntemi içinde kesme*
17. Devam etmek için **F5** tuşuna basın.
18. Zaten odağa sahip değilse Internet Explorer 'a geri dönün. Ağ yakalama penceresini aklınızda edin.

    ![Web API çağrısının sonuçlarını gösteren Internet Explorer 'da ağ görünümü](build-restful-apis-with-aspnet-web-api/_static/image19.png "Web API çağrısının sonuçlarını gösteren Internet Explorer 'da ağ görünümü")

    *Web API çağrısının sonuçlarını gösteren Internet Explorer 'da ağ görünümü*
19. **Ayrıntılı görünüme git** düğmesine tıklayın.
20. **Yanıt gövdesi** sekmesine tıklayın. API çağrısının JSON çıkışını ve hizmet katmanının aldığı iki kişiyi nasıl temsil ettiğini aklınızda edin.

    ![Web API 'sindeki JSON çıkışını Geliştirici Araçları penceresinde görüntüleme](build-restful-apis-with-aspnet-web-api/_static/image20.png "Web API 'sindeki JSON çıkışını Geliştirici Araçları penceresinde görüntüleme")

    *Web API 'sindeki JSON çıkışını Geliştirici Araçları penceresinde görüntüleme*

<a id="Exercise2"></a>

<a id="Exercise_2_Create_a_ReadWrite_Web_API"></a>
### <a name="exercise-2-create-a-readwrite-web-api"></a>Alıştırma 2: okuma/yazma Web API 'SI oluşturma

Bu alıştırmada, veri düzenlemesi özellikleriyle etkinleştirmek üzere ilgili kişi Yöneticisi için POST ve PUT yöntemlerini uygulayacaksınız.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Opening_the_Web_API_Project"></a>
#### <a name="task-1---opening-the-web-api-project"></a>Görev 1-Web API projesi açılıyor

Bu görevde, alıştırma 1 ' de oluşturulan Web API projesini geliştirmeye hazırlanacaktır, böylece kullanıcı girişi kabul edebilir.

1. **Web Için Visual Studio 2012 Express**'i çalıştırın. bunu yapmak için **başlat** 'a gidip **Web için vs Express** yazın ve **ENTER**tuşuna basın.
2. **Kaynak/Ex02-ReadWriteWebAPI/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. **Hizmetler/ContactRepository. cs** dosyasını açın.

<a id="Ex2Task2"></a>

<a id="Task_2_-_Adding_Data-Persistence_Features_to_the_Contact_Repository_Implementation"></a>
#### <a name="task-2---adding-data-persistence-features-to-the-contact-repository-implementation"></a>Görev 2-Ilgili kişi deposu uygulamasına veri kalıcılığı özellikleri ekleme

Bu görevde, alıştırma 1 ' de oluşturulan Web API projesinin ContactRepository sınıfını, Kullanıcı girişini ve yeni Iletişim örneklerini kalıcı hale getirebilmesi için kullanacaksınız.

1. Bu alıştırmada daha sonra Web sunucusu önbellek öğesi anahtar adının adını temsil etmek için **Contactrepository** sınıfına aşağıdaki sabiti ekleyin.

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample9.cs)]
2. **Contactrepository** öğesine aşağıdaki kodu içeren bir Oluşturucu ekleyin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex02-kişi deposu Oluşturucusu*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample10.cs)]
3. **Getallcontacts** yönteminin kodunu aşağıda gösterildiği gibi değiştirin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex02-tüm kişileri al*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample11.cs)]

    > [!NOTE]
    > Bu örnek, tanıtım amaçlıdır ve Web sunucusunun önbelleğini bir depolama ortamı olarak kullanacaktır. böylece, değerler oturum depolama mekanizması veya Istek depolama ömrü kullanmak yerine birden fazla istemciye aynı anda kullanılabilir olacaktır. Bunlardan biri, Web sunucusu önbelleğinin Entity Framework, XML depolama alanını veya başka bir çeşitliliğini kullanabilir.
4. Kişi kaydetme işini yapmak için **Contactrepository** sınıfına **savecontact** adlı yeni bir yöntem uygulayın. **Savecontact** yöntemi tek bir **iletişim** parametresi almalıdır ve başarılı veya başarısız olduğunu belirten bir Boole değeri döndürmelidir.

    (Kod parçacığı- *Web API Laboratuvarı-Ex02-SaveContact metodunu uygulama*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample12.cs)]

<a id="Exercise3"></a>

<a id="Exercise_3_Consume_the_Web_API_from_an_HTML_Client"></a>
### <a name="exercise-3-consume-the-web-api-from-an-html-client"></a>Alıştırma 3: bir HTML Istemcisinden Web API 'sini kullanma

Bu alıştırmada, Web API 'sini çağırmak için bir HTML İstemcisi oluşturacaksınız. Bu istemci JavaScript kullanarak Web API 'SI ile veri değişimi kolaylaştırır ve sonuçları HTML biçimlendirmesi kullanarak bir Web tarayıcısında görüntüler.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Displaying_Contacts"></a>
#### <a name="task-1---modifying-the-index-view-to-provide-a-gui-for-displaying-contacts"></a>Görev 1-kişileri görüntülemek için bir GUI sağlamak üzere dizin görünümünü değiştirme

Bu görevde, Web uygulamasının varsayılan dizin görünümünü, mevcut kişilerin listesini bir HTML tarayıcısında görüntüleme gereksinimini destekleyecek şekilde değiştirirsiniz.

1. Zaten açık değilse, **Web Için Visual Studio 2012 Express 'i** açın.
2. **Kaynak/Ex03-ConsumingWebAPI/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
3. **Görünümler/giriş** klasöründe bulunan **Index. cshtml** dosyasını açın.
4. Div öğesi içindeki HTML kodunu, aşağıdaki koda benzeymek üzere ID **gövdesi** ile değiştirin.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample13.html)]
5. Web API 'sine HTTP isteği gerçekleştirmek için, dosyanın alt kısmına aşağıdaki JavaScript kodunu ekleyin.

    [!code-cshtml[Main](build-restful-apis-with-aspnet-web-api/samples/sample14.cshtml)]
6. Zaten açık değilse, **ContactController.cs** dosyasını açın.
7. **Contactcontroller** sınıfının **Get** yöntemine bir kesme noktası koyun.

    ![API denetleyicisinin Get yöntemine bir kesme noktası yerleştirme](build-restful-apis-with-aspnet-web-api/_static/image21.png "API denetleyicisinin Get yöntemine bir kesme noktası yerleştirme")

    *API denetleyicisinin Get yöntemine bir kesme noktası yerleştirme*
8. Projeyi çalıştırmak için **F5** tuşuna basın. Tarayıcı, HTML belgesini yükler.

    > [!NOTE]
    > Uygulamanızın kök URL 'sine göz attığınızdan emin olun.
9. Sayfa yüklendiğinde ve JavaScript yürütüldükten sonra, kesme noktası isabet eder ve kod yürütmesi denetleyicide duraklatılır.

    ![Web için VS Express kullanarak Web API çağrılarında hata ayıklama](build-restful-apis-with-aspnet-web-api/_static/image22.png "Web için VS Express kullanarak Web API çağrılarında hata ayıklama")

    *Web için Visual Studio 2012 Express kullanarak Web API çağrısında hata ayıklama*
10. Görünümü tarayıcıda yüklemeye devam etmek için kesme noktasını kaldırın ve **F5** 'e veya hata ayıklama araç çubuğunun **devam** düğmesine basın. Web API çağrısı tamamlandıktan sonra, Web API çağrısından döndürülen kişileri tarayıcıda liste öğeleri olarak görürsünüz.

    ![Tarayıcıda liste öğeleri olarak görünen API çağrısının sonuçları](build-restful-apis-with-aspnet-web-api/_static/image23.png "Tarayıcıda liste öğeleri olarak görünen API çağrısının sonuçları")

    *Tarayıcıda liste öğeleri olarak görünen API çağrısının sonuçları*
11. Hata ayıklamayı durdurun.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Modifying_the_Index_View_to_Provide_a_GUI_for_Creating_Contacts"></a>
#### <a name="task-2---modifying-the-index-view-to-provide-a-gui-for-creating-contacts"></a>Görev 2-kişi oluşturmak için bir GUI sağlamak üzere dizin görünümünü değiştirme

Bu görevde, MVC uygulamasının dizin görünümünü değiştirmeye devam edersiniz. HTML sayfasına kullanıcı girişini yakalayan ve yeni bir kişi oluşturmak için Web API 'sine gönderecek bir form eklenir ve GUI 'den tarihi toplamak için yeni bir Web API denetleyicisi yöntemi oluşturulur.

1. **ContactController.cs** dosyasını açın.
2. Aşağıdaki kodda gösterildiği gibi, **Post** adlı denetleyici sınıfına yeni bir yöntem ekleyin.

    (Kod parçacığı- *Web API Laboratuvarı-Ex03-post yöntemi*)

    [!code-csharp[Main](build-restful-apis-with-aspnet-web-api/samples/sample15.cs)]
3. Zaten açık değilse, **Index. cshtml** dosyasını Visual Studio 'da açın.
4. Önceki göreve eklediğiniz sıralanmamış listeden hemen sonra, aşağıdaki HTML kodunu dosyaya ekleyin.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample16.html)]
5. Belgenin alt kısmındaki komut dosyası öğesi içinde, bir HTTP POST çağrısı kullanarak verileri Web API 'sine gönderecek olan düğme tıklama olaylarını işlemek için aşağıdaki vurgulanmış kodu ekleyin.

    [!code-html[Main](build-restful-apis-with-aspnet-web-api/samples/sample17.html)]
6. **ContactController.cs**içinde **Post** yöntemine bir kesme noktası koyun.
7. Uygulamayı tarayıcıda çalıştırmak için **F5** tuşuna basın.
8. Sayfa tarayıcıya yüklendikten sonra, yeni bir kişi adı ve kimliği yazın ve **Kaydet** düğmesine tıklayın.

    ![Tarayıcıda yüklenen istemci HTML belgesi](build-restful-apis-with-aspnet-web-api/_static/image24.png "Tarayıcıda yüklenen istemci HTML belgesi")

    *Tarayıcıda yüklenen istemci HTML belgesi*
9. **Post** yönteminde hata ayıklayıcı penceresi kesildiğinde, **iletişim** parametresinin özelliklerine göz atın. Değerler, forma girdiğiniz verilerle eşleşmelidir.

    ![İstemciden Web API 'sine gönderilen kişi nesnesi](build-restful-apis-with-aspnet-web-api/_static/image25.png "İstemciden Web API 'sine gönderilen kişi nesnesi")

    *İstemciden Web API 'sine gönderilen kişi nesnesi*
10. **Yanıt** değişkeni oluşturuluncaya kadar hata ayıklayıcıdaki yöntemi adım adım yapın. Hata ayıklayıcıda **Yereller** penceresinde İnceleme yapıldığında tüm özelliklerin ayarlandığını görürsünüz.

   ![Hata ayıklayıcıda oluşturma sonrasında yanıt](build-restful-apis-with-aspnet-web-api/_static/image26.png "Hata ayıklayıcıda oluşturma sonrasında yanıt")

   *Hata ayıklayıcıda oluşturma sonrasında yanıt*
11. **F5** tuşuna basarsanız veya hata ayıklayıcıda **devam et** ' e tıkladığınızda istek tamamlanır. Tarayıcıya geri döndüğünüzde, yeni kişi **Contactrepository** uygulamasıyla depolanan kişiler listesine eklenir.

   ![Tarayıcı, yeni kişi örneğinin başarıyla oluşturulmasını yansıtır](build-restful-apis-with-aspnet-web-api/_static/image27.png "Tarayıcı, yeni kişi örneğinin başarıyla oluşturulmasını yansıtır")

   *Tarayıcı, yeni kişi örneğinin başarıyla oluşturulmasını yansıtır*

> [!NOTE]
> Ayrıca, bu uygulamayı Azure 'a dağıtmak için [Ek C: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama](#AppendixC).

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu laboratuvar, sizi yeni ASP.NET Web API çerçevesine ve Framework kullanan yeniden Web API 'Lerinin uygulamasına sunmaktadır. Buradan, bu laboratuvara bir örnek olarak sağlanmaktansa, hizmetin herhangi bir sayıda mekanizmayı ve bir düzeyini kullanarak veri kalıcılığını kolaylaştıran yeni bir depo oluşturabilirsiniz. Web API 'SI, HTTP ve JSON veya XML 'yi destekleyen herhangi bir dilde yazılmış HTML olmayan istemcilerden gelen iletişimi etkinleştirme gibi birçok ek özelliği destekler. Bir Web API 'sini tipik bir Web uygulaması dışında barındırma özelliği de mümkündür ve bunun yanı sıra kendi serileştirme biçimlerinizi oluşturabilir.

ASP.NET Web sitesi, [[https://asp.net/web-api](https://asp.net/web-api)](https://asp.net/web-api)ADRESINDEKI Web API çerçevesine adanmış bir alana sahiptir. Bu site, Web API 'siyle ilgili en son bilgileri, örnekleri ve haberleri sağlamaya devam edecek, bu nedenle neredeyse tüm cihazlar veya geliştirme çerçevesiyle sunulan özel Web API 'Leri oluşturma sanatı hakkında daha ayrıntılı bilgi almak istiyorsanız, sık sık kontrol edin.

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>Ek A: kod parçacıkları kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](build-restful-apis-with-aspnet-web-api/_static/image28.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

<a id="CodeSnippetUsingKeyBoard"></a>

<a id="To_add_a_code_snippet_using_the_keyboard_C_only"></a>
### <a name="to-add-a-code-snippet-using-the-keyboard-c-only"></a>Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

    ![Kod parçacığı adını yazmaya başlayın](build-restful-apis-with-aspnet-web-api/_static/image29.png "Kod parçacığı adını yazmaya başlayın")

    *Kod parçacığı adını yazmaya başlayın*

    ![Vurgulanan parçacığı seçmek için Tab tuşuna basın](build-restful-apis-with-aspnet-web-api/_static/image30.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

    *Vurgulanan parçacığı seçmek için Tab tuşuna basın*

    ![Sekmeye tekrar basın ve kod parçacığı genişletilir](build-restful-apis-with-aspnet-web-api/_static/image31.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

    *Sekmeye tekrar basın ve kod parçacığı genişletilir*

<a id="CodeSnippetUsingMouse"></a>

<a id="To_add_a_code_snippet_using_the_mouse_C_Visual_Basic_and_XML"></a>
### <a name="to-add-a-code-snippet-using-the-mouse-c-visual-basic-and-xml"></a>Fareyi kullanarak bir kod parçacığı eklemek için (C#, VISUAL BASIC ve XML)

1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.
2. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
3. Listeden tıklatarak ilgili kod parçacığını seçin.

    ![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](build-restful-apis-with-aspnet-web-api/_static/image32.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

    *Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

    ![Listeden tıklatarak ilgili kod parçacığını seçin](build-restful-apis-with-aspnet-web-api/_static/image33.png "Listeden tıklatarak ilgili kod parçacığını seçin")

    *Listeden tıklatarak ilgili kod parçacığını seçin*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>Ek B: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürün için arama yapabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](build-restful-apis-with-aspnet-web-api/_static/image34.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](build-restful-apis-with-aspnet-web-api/_static/image35.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](build-restful-apis-with-aspnet-web-api/_static/image36.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](build-restful-apis-with-aspnet-web-api/_static/image37.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](build-restful-apis-with-aspnet-web-api/_static/image38.png)

    *Web için VS Express kutucuğu*

<a id="AppendixC"></a>

<a id="Appendix_C_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-c-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Ek C: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama

Bu ek, Azure portalından yeni bir Web sitesi oluşturmayı ve Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı gösterir.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>Görev 1-Azure portalından yeni bir Web sitesi oluşturma

1. [Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.

    > [!NOTE]
    > Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz. [Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.

    ![Windows Azure portal oturum açın](build-restful-apis-with-aspnet-web-api/_static/image39.png "Windows Azure portal oturum açın")

    *Portalda oturum açın*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image40.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Azure, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Azure 'a Portal dışından dağıtmanıza izin verir. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](build-restful-apis-with-aspnet-web-api/_static/image41.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](build-restful-apis-with-aspnet-web-api/_static/image42.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](build-restful-apis-with-aspnet-web-api/_static/image43.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](build-restful-apis-with-aspnet-web-api/_static/image44.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , her etkin yayımlama yöntemi için bir Web uygulamasını Azure 'da yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Azure 'da yayımlamaya yönelik bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerini okumayı destekler.

    ![Web sitesi yayımlama profili indiriliyor](build-restful-apis-with-aspnet-web-api/_static/image45.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, Visual Studio 'dan Azure 'da bir Web uygulaması yayınlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](build-restful-apis-with-aspnet-web-api/_static/image46.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="ApxCTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](build-restful-apis-with-aspnet-web-api/_static/image47.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](build-restful-apis-with-aspnet-web-api/_static/image48.png) düğmesine tıklayın.

    ![Istemci IP adresi ekleniyor](build-restful-apis-with-aspnet-web-api/_static/image49.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](build-restful-apis-with-aspnet-web-api/_static/image50.png)

    *Değişiklikleri Onayla*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](build-restful-apis-with-aspnet-web-api/_static/image51.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](build-restful-apis-with-aspnet-web-api/_static/image52.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](build-restful-apis-with-aspnet-web-api/_static/image53.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](build-restful-apis-with-aspnet-web-api/_static/image54.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.

     ![Hedef bağlantı dizesi yapılandırılıyor](build-restful-apis-with-aspnet-web-api/_static/image55.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Daha sonra, **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](build-restful-apis-with-aspnet-web-api/_static/image56.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Ardından **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](build-restful-apis-with-aspnet-web-api/_static/image57.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](build-restful-apis-with-aspnet-web-api/_static/image58.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

    ![Windows Azure 'da yayımlanan uygulama](build-restful-apis-with-aspnet-web-api/_static/image59.png "Windows Azure 'da yayımlanan uygulama")

    *Azure 'da yayımlanan uygulama*
