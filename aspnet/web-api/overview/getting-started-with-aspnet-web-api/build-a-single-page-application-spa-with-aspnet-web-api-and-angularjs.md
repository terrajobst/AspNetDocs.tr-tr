---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: "Uygulamalı laboratuvar: ASP.NET Web API 'SI ile tek sayfalı uygulama (SPA), angular. js-ASP.NET 4. x oluşturun"
author: rick-anderson
description: "Adım adım kodu: ASP.NET 4. x için ASP.NET Web API 'SI ve angular. js ile tek sayfalı uygulama (SPA) oluşturun."
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557045"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>Uygulamalı Laboratuvar: ASP.NET Web API ve Angular.js ile Tek Sayfalı Uygulama (SPA) Oluşturma

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

Bu uygulamalı laboratuvar, ASP.NET 4. x için ASP.NET Web API 'SI ve angular. js ile tek sayfalı uygulama (SPA) oluşturmayı gösterir.

Bu yandan laboratuvarda, Spa kavramını temel alan bir bilgi web sitesi olan Geek sınavını uygulamak için bu teknolojilerden yararlanabilirsiniz. İlk olarak, test sorularını almak ve yanıtları depolamak üzere gerekli uç noktaları kullanıma sunmak için ASP.NET Web API 'SI ile hizmet katmanını uygulayacaksınız. Daha sonra, AngularJS ve CSS3 dönüştürme efektlerini kullanarak zengin ve duyarlı bir kullanıcı arabirimi oluşturacaksınız.

Geleneksel Web uygulamalarında, istemci (tarayıcı) bir sayfa isteyerek sunucu ile iletişimi başlatır. Sunucu daha sonra isteği işler ve sayfanın HTML 'sini istemciye gönderir. Sayfayla sonraki etkileşimlerde – örn. Kullanıcı bir bağlantıya gider veya veri içeren bir form gönderir. sunucuya yeni bir istek gönderilir ve akış yeniden başlatılır: sunucu isteği işler ve yeni eylem isteğine yanıt olarak tarayıcıya yeni bir sayfa gönderir istemci tarafından yapılır.
> 
> Tek sayfalı uygulamalarda (maça) ilk istekten sonra tüm sayfa tarayıcıya yüklenir, ancak sonraki etkileşimler Ajax istekleri aracılığıyla gerçekleştirilir. Bu, tarayıcının yalnızca sayfanın değiştiği kısmını güncelleştirmesi gerektiği anlamına gelir; sayfanın tamamını yeniden yüklemeniz gerekmez. SPA yaklaşımı, uygulamanın kullanıcı eylemlerine yanıt vermesi için geçen süreyi azaltır ve bu da daha akıcı bir deneyimle sonuçlanır.
> 
> SPA 'nın mimarisi geleneksel Web uygulamalarında mevcut olmayan bazı güçlükleri içerir. Ancak, ASP.NET Web API gibi gelişen teknolojiler, AngularJS gibi JavaScript çerçeveleri ve CSS3 tarafından sunulan yeni stil özellikleri, maça tasarımını ve derlemesini gerçekten kolaylaştırır.
> 
> 
> Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

## <a name="overview"></a>Genel bakış

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- JSON verilerini göndermek ve almak için bir ASP.NET Web API hizmeti oluşturun
- AngularJS kullanarak yanıt veren kullanıcı arabirimi oluşturma
- CSS3 dönüşümlerle Kullanıcı arabirimi deneyimini geliştirin

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:

- Web veya daha büyük [için Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.

1. Windows Gezgini 'ni açın ve laboratuvarın **kaynak** klasörüne gidin.
2. Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.
3. Kullanıcı hesabı denetimi iletişim kutusu gösterilirse, devam etmek için eylemi onaylayın.

> [!NOTE]
> Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Kod parçacıklarını kullanma

Laboratuvar belgesi boyunca kod blokları eklemeniz istenir. Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.

> [!NOTE]
> Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür. Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun. Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız. Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.

---

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [Web API 'SI oluşturma](#Exercise1)
2. [SPA arabirimi oluşturma](#Exercise2)

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**

> [!NOTE]
> Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir. Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler. Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır. Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>Alıştırma 1: Web API 'SI oluşturma

SPA 'nın önemli parçalarından biri hizmet katmanıdır. Kullanıcı arabirimi tarafından gönderilen Ajax çağrılarını işlemeden ve bu çağrıya yanıt olarak veri döndürmekten sorumludur. Alınan veriler, istemci tarafından ayrıştırılıp tüketilmesi için makine tarafından okunabilen bir biçimde sunulmalıdır.

Web API çerçevesi, ASP.NET yığınının bir parçasıdır ve HTTP hizmetlerinin uygulanmasını kolaylaştırmak için tasarlanmıştır. Bu, genel bir API aracılığıyla JSON veya XML biçimli veriler gönderip alabilir. Bu alıştırmada, Geek test uygulamasını barındıracak Web sitesini oluşturacak ve ardından ASP.NET Web API 'sini kullanarak test verilerini kullanıma sunmak ve kalıcı hale getirmek için arka uç hizmetini uygulamanız gerekir.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>Görev 1 – Geek sınavından Ilk projeyi oluşturma

Bu görevde, Visual Studio ile birlikte gelen **bir ASP.net** proje türüne göre ASP.NET Web API 'si desteğiyle yeni BIR ASP.NET MVC projesi oluşturmaya başlayacaksınız. **Bir ASP.net** tüm ASP.NET teknolojilerini birleştirir ve bunları istediğiniz gibi karıştırma ve eşleştirme seçeneği sunar. Ardından, test sorularını eklemek için Entity Framework model sınıflarını ve veritabanı başlatıcısı 'nı ekleyeceksiniz.

1. **Web için Visual Studio Express 2013** ' i açın ve dosya ' yı seçin **| Yeni proje...** Yeni bir çözüm başlatmak için.

    ![Yeni bir proje oluşturma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Yeni proje oluşturma")

    *Yeni bir proje oluşturma*
2. **Yeni proje** iletişim kutusunda, görsel  **C# altında ASP.NET Web uygulaması ' nı seçin | Web** sekmesi. **.NET Framework 4,5** ' nin seçildiğinden emin olun, *geektest*olarak adlandırın, bir **konum** seçin ve **Tamam**' a tıklayın.

    ![Yeni bir ASP.NET Web uygulaması projesi oluşturma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Yeni bir ASP.NET Web uygulaması projesi oluşturma")

    *Yeni bir ASP.NET Web uygulaması projesi oluşturma*
3. **Yeni ASP.NET projesi** Iletişim kutusunda **MVC** ŞABLONUNU seçin ve **Web API** seçeneğini belirleyin. Ayrıca, **kimlik doğrulama** seçeneğinin **bireysel kullanıcı hesapları**olarak ayarlandığından emin olun. Devam etmek için **Tamam** 'a tıklayın.

    ![Web API bileşenleri dahil olmak üzere MVC şablonuyla yeni bir proje oluşturma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *Web API bileşenleri dahil olmak üzere MVC şablonuyla yeni bir proje oluşturma*
4. **Çözüm Gezgini**' de, **geektest** projesinin **modeller** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Mevcut öğe...** .

    ![Varolan bir öğe ekleniyor](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Varolan bir öğe ekleniyor")

    *Varolan bir öğe ekleniyor*
5. **Varolan öğe Ekle** Iletişim kutusunda **kaynak/varlıklar/modeller** klasörüne gidin ve tüm dosyalar ' ı seçin. **Ekle**'yi tıklatın.

    ![Model varlıklarını ekleme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Model varlıklarını ekleme")

    *Model varlıklarını ekleme*

    > [!NOTE]
    > Bu dosyaları ekleyerek, veri modeli, Entity Framework veritabanı bağlamı ve Geek test uygulaması için veritabanı başlatıcısı ekleniyor.
    > 
    > **Entity Framework (EF)** , ilişkisel bir depolama şemasını kullanarak doğrudan programlama yerine kavramsal bir uygulama modeliyle programlama yoluyla veri erişimi uygulamaları oluşturmanıza olanak sağlayan bir nesne ilişkisel Eşleyici 'DIR (ORM). [Buradan](../../../entity-framework.md)Entity Framework hakkında daha fazla bilgi edinebilirsiniz.
    > 
    > Aşağıda, az önce eklediğiniz sınıfların bir açıklaması verilmiştir:
    > 
    > - **Triviaoption:** bir test sorusu ile ilişkili tek bir seçeneği temsil eder
    > - **Üçlü soru:** bir test sorusunu temsil eder ve **Options** özelliği aracılığıyla ilişkili seçenekleri kullanıma sunar
    > - **Triviaanswer:** bir test sorusuna yanıt olarak Kullanıcı tarafından seçilen seçeneği temsil eder
    > - **Triviacontext:** Entity Framework, Geek test uygulamasının veritabanı bağlamını temsil eder. Bu sınıf **Dcontext** 'ten türetilir ve yukarıda açıklanan varlıkların koleksiyonlarını temsil eden **dbset** özelliklerini gösterir.
    > - **Triviadatabasebaşlatıcısı:** **Createdatabaseifnotexists**öğesinden devralan **triviacontext** sınıfı için Entity Framework başlatıcısı 'nın uygulanması. Bu sınıfın varsayılan davranışı, yalnızca yoksa, **çekirdek** yönteminde belirtilen varlıkları ekleyerek veritabanını oluşturmaktır.
6. **Global.asax.cs** dosyasını açın ve aşağıdaki using ifadesini ekleyin.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. Aşağıdaki kodu, **uygulama\_start** yönteminin başına ekleyerek, veritabanı başlatıcısı olarak **Triviadatabasebaşlatıcısı** 'nı ayarlayın.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. Kimliği doğrulanmış kullanıcılara erişimi kısıtlamak için **ana** denetleyiciyi değiştirin. Bunu yapmak için, **HomeController.cs** dosyasını **denetleyiciler** klasörünün içinde açın ve **Yetkilendir** özniteliğini **HomeController** sınıf tanımına ekleyin.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **Yetkilendirme** filtresi, kullanıcının kimliğinin doğrulandığını denetler. Kullanıcının kimliği doğrulanmıyorsa, eylemi çağırmadan HTTP durum kodu 401 (yetkisiz) döndürür. Filtreyi denetleyici düzeyinde küresel olarak veya tek tek eylemler düzeyinde uygulayabilirsiniz.
9. Artık Web sayfalarının ve markasının yerleşimini özelleştirecektir. Bunu yapmak için, görünümler içinde **\_Layout. cshtml** dosyasını açın **|**  *ASP.net uygulamamı* *Geek sınavından*değiştirerek, paylaşılan klasör ve **&lt;title&gt;** öğesi içeriğini güncelleştirin.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. Aynı dosyada, *hakkında* ve *iletişim kurulacak* bağlantıları kaldırarak ve *ana* bağlantı bağlantısını *çalmak*üzere yeniden adlandırarak gezinti çubuğunu güncelleştirin. Ayrıca, *uygulama adı* bağlantısını *Geek test*olarak yeniden adlandırın. Gezinti çubuğu için HTML aşağıdaki kod gibi görünmelidir.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. *ASP.net uygulamamı* *Geek sınavıyla*değiştirerek düzen sayfasının altbilgisini güncelleştirin. Bunu yapmak için **&lt;footer&gt;** öğesinin içeriğini aşağıdaki vurgulanmış kodla değiştirin.

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>Görev 2 – TriviaController Web API 'sini oluşturma

Önceki görevde, Geek test Web uygulamasının ilk yapısını oluşturdunuz. Şimdi, test veri modeliyle etkileşen ve aşağıdaki eylemleri sunan basit bir Web API hizmeti oluşturacaksınız:

- **/Api/trivia al**: kimliği doğrulanmış kullanıcı tarafından yanıtlanabilmesi için, test listesinden sonraki soruyu alır.
- **Post/api/trivia**: kimliği doğrulanmış kullanıcı tarafından belirtilen test yanıtını depolar.

Web API denetleyici sınıfının temelini oluşturmak için Visual Studio tarafından sunulan ASP.NET Scafkatlama Araçları ' nı kullanacaksınız.

1. **WebApiConfig.cs** dosyasını **uygulama\_başlangıç** klasörü içinde açın. Bu dosya, yolların Web API denetleyici eylemlerine nasıl eşlendiğine benzer şekilde Web API hizmetinin yapılandırmasını tanımlar.
2. Aşağıdaki using ifadesini dosyanın başına ekleyin.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. Web API 'SI eylem yöntemleri tarafından alınan JSON verileri için biçimlendiricisi küresel olarak yapılandırmak üzere aşağıdaki vurgulanmış kodu **register** yöntemine ekleyin.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **Camelcasepropertynamescontractresolver** , özellik adlarını JavaScript 'teki Özellik adları için genel kural olan *ortası* örneğine otomatik olarak dönüştürür.
4. **Çözüm Gezgini**' de, **geektest** projesinin **denetleyiciler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni yapı Iskelesi öğesi...** .

    ![Yeni bir yapı iskelesi öğesi oluşturma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Yeni bir yapı iskelesi öğesi oluşturma")

    *Yeni bir yapı iskelesi öğesi oluşturma*
5. **Yapı Iskelesi Ekle** iletişim kutusunda, sol bölmede **ortak** düğümün seçili olduğundan emin olun. Ardından, orta bölmedeki **Web API 2 denetleyici-boş** şablonunu seçin ve **Ekle**' ye tıklayın.

    ![Web API 2 denetleyici boş şablonu seçme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Web API 2 denetleyici boş şablonu seçme")

    *Web API 2 denetleyici boş şablonu seçme*

    > [!NOTE]
    > **ASP.net Scafkatlama** , ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir. Visual Studio 2013, MVC ve Web API projeleri için önceden yüklenmiş kod oluşturucuları içerir. Standart veri işlemlerini geliştirmek için gereken süreyi azaltmak üzere veri modelleriyle etkileşime geçen kodu hızlıca eklemek istediğinizde, projenizde scafkatlamayı kullanmanız gerekir.
    > 
    > Yapı iskelesi işlemi, gerekli tüm bağımlılıkların projeye yüklenmesini de sağlar. Örneğin, boş bir ASP.NET projesi ile başlayıp bir Web API denetleyicisi eklemek için scafkatlamayı kullanırsanız, gerekli Web API NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.
6. **Denetleyici Ekle** iletişim kutusunda, **Denetleyici adı** metin kutusuna *Triviacontroller* yazın ve **Ekle**' ye tıklayın.

    ![Trivia denetleyiciyi ekleme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Trivia denetleyiciyi ekleme")

    *Trivia denetleyiciyi ekleme*
7. **TriviaController.cs** dosyası daha sonra, boş bir **triviacontroller** sınıfı içeren **geektest** projesinin **Controllers** klasörüne eklenir. Aşağıdaki using deyimlerini dosyanın başına ekleyin.

    (Kod parçacığı- *AspNetWebApiSpa-Ex1-Triviacontrollerusler*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. Denetleyici içindeki **Triviacontext** örneğini tanımlamak, başlatmak ve atmak Için **triviacontroller** sınıfının başına aşağıdaki kodu ekleyin.

    (Kod parçacığı- *AspNetWebApiSpa-Ex1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **Triviacontroller** 'ın **Dispose** yöntemi **, triviacontext örneğinin** **Dispose** yöntemini çağırır, bu da bağlam nesnesi tarafından kullanılan tüm kaynakların **triviacontext** örneği atıldığında veya atık olarak toplandığında serbest bırakılacağını sağlar. Bu, Entity Framework tarafından açılan tüm veritabanı bağlantılarını kapatmayı içerir.
9. **Triviacontroller** sınıfının sonuna aşağıdaki yardımcı yöntemi ekleyin. Bu yöntem, belirtilen kullanıcı tarafından yanıtlanabilmesi için aşağıdaki test sorularını veritabanından alır.

    (Kod parçacığı- *AspNetWebApiSpa-Ex1-Triviacontrollernextsoru*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. Aşağıdaki **Get** ACTION yöntemini **triviacontroller** sınıfına ekleyin. Bu eylem yöntemi, kimliği doğrulanmış kullanıcı için bir sonraki soruyu almak üzere önceki adımda tanımlanan **NextQuestionAsync** Helper yöntemini çağırır.

    (Kod parçacığı- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. **Triviacontroller** sınıfının sonuna aşağıdaki yardımcı yöntemi ekleyin. Bu yöntem, belirtilen yanıtı veritabanında depolar ve yanıtın doğru olup olmadığını gösteren bir Boole değeri döndürür.

    (Kod parçacığı- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. Aşağıdaki **Post** eylemi yöntemini **triviacontroller** sınıfına ekleyin. Bu eylem yöntemi, yanıtı kimliği doğrulanmış kullanıcıyla ilişkilendirir ve **Storeasync** yardımcı yöntemini çağırır. Ardından, yardımcı yöntem tarafından döndürülen Boole değeriyle bir yanıt gönderir.

    (Kod parçacığı- *AspNetWebApiSpa-Ex1-Triviacontrollerpostaeylemi*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. **Triviacontroller** sınıf tanımına **Yetkilendir** özniteliğini ekleyerek kimliği doğrulanmış kullanıcılara ERIŞIMI kısıtlamak için Web API denetleyicisi ' ni değiştirin.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>Görev 3 – çözümü çalıştırma

Bu görevde, önceki görevde oluşturduğunuz Web API hizmetinin beklendiği gibi çalıştığını doğrulayacaksınız. Ağ trafiğini yakalamak ve Web API hizmetinden tam yanıtı incelemek için Internet Explorer **F12 geliştirici araçları** kullanacaksınız.

> [!NOTE]
> Visual Studio araç çubuğunda bulunan **Başlat** düğmesinde **Internet Explorer** 'ın seçili olduğundan emin olun.
> 
> ![Internet Explorer seçeneği](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. Çözümü çalıştırmak için **F5** tuşuna basın. **Oturum açma** sayfası tarayıcıda görünmelidir.

    > [!NOTE]
    > Uygulama başlatıldığında varsayılan MVC yolu tetiklenir. Bu, varsayılan olarak **HomeController** sınıfının **Dizin** eylemine eşlenir. **HomeController** , kimliği doğrulanmış kullanıcılarla kısıtlandığı için (Bu sınıfı alıştırma 1 ' deki **Yetkilendir** özniteliğiyle süslediğinizden ve henüz kimlik doğrulamasının olmadığı unutulmamalıdır), uygulama ilk isteği bir oturum açma sayfasına yönlendirir.

    ![Çözümü çalıştırma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Çözümü çalıştırma")

    *Çözümü çalıştırma*
2. Yeni bir kullanıcı oluşturmak için **Kaydet** ' e tıklayın.

    ![Yeni Kullanıcı kaydetme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Yeni Kullanıcı kaydetme")

    *Yeni Kullanıcı kaydetme*
3. **Kaydet** sayfasında, bir **Kullanıcı adı** ve **parola**girin ve ardından **Kaydet**' e tıklayın.

    ![Kayıt sayfası](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Kayıt sayfası")

    *Kayıt sayfası*
4. Uygulama yeni hesabı kaydeder ve kullanıcının kimliği doğrulanır ve giriş sayfasına yeniden yönlendirilir.

    ![Kullanıcının kimliği doğrulandı](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "Kullanıcının kimliği doğrulandı")

    *Kullanıcının kimliği doğrulandı*
5. Tarayıcıda, **Geliştirici Araçları** panelini açmak için **F12** tuşuna basın. **Ctrl + 4** tuşlarına basın veya **ağ** simgesine tıklayın ve ardından, ağ trafiğini yakalamaya başlamak için yeşil ok düğmesine tıklayın.

    ![Web API ağı yakalama başlatılıyor](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Web API ağı yakalama başlatılıyor")

    *Web API ağı yakalama başlatılıyor*
6. Tarayıcının adres çubuğundaki URL 'ye yönelik **API/trivia** ekleyin. Şimdi, **Triviacontroller**'daki **Get** ACTION yönteminden Yanıtın ayrıntılarını inceleyebilirsiniz.

    ![Web API aracılığıyla sonraki soru verilerini alma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Web API aracılığıyla sonraki soru verilerini alma")

    *Web API aracılığıyla sonraki soru verilerini alma*

    > [!NOTE]
    > İndirme işlemi tamamlandıktan sonra indirilen dosyayla bir eylem yapmanız istenir. Geliştirici araç penceresi aracılığıyla yanıt içeriğini izleyebilmek için iletişim kutusunu açık bırakın.
7. Şimdi yanıtın gövdesini inceleyeceksiniz. Bunu yapmak için **Ayrıntılar** sekmesine tıklayın ve ardından **yanıt gövdesi**' ne tıklayın. İndirilen verilerin Özellikler **seçeneklerine** sahip bir nesne olup olmadığını kontrol edebilirsiniz ( **triviaoption** nesnelerinin bir listesi), **kimlik** ve **başlık** **triviasoru** sınıfına karşılık gelir.

    ![Web API yanıt gövdesini görüntüleme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Web API yanıt gövdesini görüntüleme")

    *Web API yanıt gövdesini görüntüleme*
8. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>Alıştırma 2: SPA arabirimini oluşturma

Bu alıştırmada, ilk olarak, **AngularJS**kullanarak tek sayfalı uygulama etkileşimine odaklanarak Geek sınavından oluşan Web ön uç bölümünü derleyebilirsiniz. Daha sonra, CSS3 ile Kullanıcı deneyimini geliştirerek zengin animasyonlar gerçekleştirir ve bir sorudan sonrakine geçerken bağlam geçişinin görsel bir etkisini sağlayabilirsiniz.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>Görev 1 – AngularJS kullanarak SPA arabirimi oluşturma

Bu görevde, Geek test uygulamasının istemci tarafını uygulamak için **AngularJS** kullanacaksınız. **AngularJS** , tarayıcı tabanlı uygulamaları *Model-View-Controller* (MVC) özelliğiyle genişleterek hem geliştirme hem de sınamayı kolaylaştıran açık kaynaklı bir JavaScript çerçevesidir.

Visual Studio 'nun paket yöneticisi konsolundan AngularJS yükleyerek başlayacaksınız. Daha sonra, AngularJS şablon altyapısını kullanarak test sorularını ve yanıtlarını işlemek için Geek test uygulamasının davranışını ve görünümünü sağlamak üzere denetleyiciyi oluşturacaksınız.

> [!NOTE]
> AngularJS hakkında daha fazla bilgi için [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)bakın.

1. **Web için Visual Studio Express 2013** ' i açın ve **kaynak/EX2-Creatingaspaınterface/Begin** klasöründe bulunan **geektest. sln** çözümünü açın. Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.
2. **NuGet paket yöneticisi** > **Araçlar** ' dan **Paket Yöneticisi konsolunu** açın. **AngularJS. Core** NuGet paketini yüklemek için aşağıdaki komutu yazın.

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. **Çözüm Gezgini**' de, **geektest** projesinin **betikler** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni klasör**. Klasör **uygulamasını** adlandırın ve **ENTER**'a basın.
4. Yeni oluşturduğunuz **uygulama** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **JavaScript dosyası**.

    ![Yeni bir JavaScript dosyası oluşturma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *Yeni bir JavaScript dosyası oluşturma*
5. **Öğe Için ad belirtin** iletişim kutusunda, **öğe adı** metin kutusuna *Test-Controller* yazın ve **Tamam**' ı tıklatın.

    ![Yeni JavaScript dosyasını adlandırma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *Yeni JavaScript dosyasını adlandırma*
6. **Quiz-Controller. js** dosyasında, AngularJS **QuizCtrl** denetleyiciyi bildirmek ve başlatmak için aşağıdaki kodu ekleyin.

    (Kod parçacığı- *AspNetWebApiSpa-EX2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > **QuizCtrl** denetleyicisinin Oluşturucu işlevi, **$scope**adlı bir Injectable parametresi bekliyor. **$Scope** nesnesine Özellikler iliştirerek, kapsamın başlangıç durumu Oluşturucu işlevinde ayarlanmalıdır. Özellikler **Görünüm modelini**içerir ve denetleyici kaydedildiğinde şablon tarafından erişilebilecektir.
    > 
    > **QuizCtrl** denetleyicisi, **QuizApp**adlı bir modül içinde tanımlanır. Modüller, uygulamanızı ayrı bileşenlere ayırmanıza olanak sağlayan iş birimleridir. Modül kullanmanın başlıca avantajları, kodun anlaşılması daha kolay ve birim testi, yeniden kullanılabilirlik ve bakım yapma işlemlerini kolaylaştırır.
7. Artık, görünümden tetiklenen olaylara tepki vermek için kapsama davranış ekleyeceksiniz. **$Scope** nesnesinde **nextsoru** işlevini tanımlamak için **QuizCtrl** denetleyicisinin sonuna aşağıdaki kodu ekleyin.

    (Kod parçacığı- *AspNetWebApiSpa-EX2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > Bu işlev, önceki alıştırmada oluşturulan **trivia** Web API 'sindeki bir sonraki soruyu alır ve soru verilerini **$scope** nesnesine iliştirir.
8. **$Scope** nesnesinde **sendanswer** işlevini tanımlamak için **QuizCtrl** denetleyicisinin sonuna aşağıdaki kodu ekleyin.

    (Kod parçacığı- *AspNetWebApiSpa-EX2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > Bu işlev, Kullanıcı tarafından seçilen **yanıtı Web API** 'sine gönderir ve sonucu depolar; Örneğin, yanıt doğruysa veya değilse, **$scope** nesnesinde.
    > 
    > Yukarıdaki **Nextsoru** ve **Sendanswer** işlevleri, AngularJS **$http** nesnesini kullanarak Web API 'Si ile iletişimi tarayıcıdan XMLHttpRequest JavaScript nesnesi üzerinden soyutlar. AngularJS, diğer API 'Ler aracılığıyla bir kaynağa yönelik CRUD işlemleri gerçekleştirmeye yönelik daha yüksek bir soyutlama düzeyi getiren başka bir hizmeti destekler. AngularJS **$Resource** nesnesi, **$http** nesnesiyle etkileşim kurma gereksinimi olmadan üst düzey davranışları sağlayan eylem yöntemlerine sahiptir. CRUD modeli gerektiren senaryolarda **$Resource** nesnesini kullanmayı düşünün (ön bilgi, [$Resource belgelerine](https://docs.angularjs.org/api/ngResource/service/$resource)bakın).
9. Sonraki adım, test için görünümü tanımlayan AngularJS şablonunu oluşturmaktır. Bunu yapmak için, görünümler içindeki **Index. cshtml** dosyasını açın **| Giriş** klasörü ve içeriği aşağıdaki kodla değiştirin.

    (Kod parçacığı- *AspNetWebApiSpa-EX2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS şablonu, modelden ve kullanıcının tarayıcıda gördüğü dinamik görünüme statik biçimlendirme dönüştürmek için, modelden ve denetleyicideki bilgileri kullanan bildirime dayalı bir belirtimdir. Aşağıda, bir şablonda kullanılabilecek AngularJS öğelerinin ve öğe özniteliklerinin örnekleri verilmiştir:
    > 
    > - **Ng-App** yönergesi, uygulamanın kök öğesini temsıl eden Dom öğesini AngularJS söyler.
    > - **Ng-Controller** yönergesi, bir denetleyiciyi, yönergenin BILDIRILDIĞI noktada Dom 'a iliştirir.
    > - **{{}}** Küme ayracı gösterimi, denetleyicide tanımlanan kapsam özelliklerine yönelik bağlamaları gösterir.
    > - **Ng-Click** yönergesi, Kullanıcı tıklamasına yanıt olarak kapsamda tanımlanan işlevleri çağırmak için kullanılır.
10. **İçerik** klasörünün içindeki **site. css** dosyasını açın ve test görünümü için bir görünüm sağlamak üzere dosyanın sonuna aşağıdaki vurgulanmış stilleri ekleyin.

    (Kod parçacığı- *AspNetWebApiSpa-EX2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>Görev 2 – çözümü çalıştırma

Bu görevde, test sorularından bazılarını yanıtlamak için AngularJS ile oluşturduğunuz yeni kullanıcı arabirimini kullanarak çözümü yürütecaksınız.

1. Çözümü çalıştırmak için **F5** tuşuna basın.
2. Yeni bir kullanıcı hesabı kaydedin. Bunu yapmak için alıştırma 1, görev 3 ' te açıklanan kayıt adımlarını izleyin.

    > [!NOTE]
    > Çözümü önceki alıştırmada kullanıyorsanız, daha önce oluşturduğunuz kullanıcı hesabıyla oturum açabilirsiniz.
3. **Giriş** sayfası, test ilk sorusunun gösterildiği gibi görünmelidir. Seçeneklerden birine tıklayarak soruyu yanıtlayın. Bu, daha önce tanımlanan **Sendanswer** işlevini tetikler, bu da seçili seçeneği, **TRIVIA** Web API 'sine gönderir.

    ![Soru yanıt verme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Soru yanıt verme")

    *Soru yanıt verme*
4. Düğmelerden birine tıkladıktan sonra yanıt görüntülenmelidir. Aşağıdaki soruyu göstermek için **sonraki soru** ' ya tıklayın. Bu, denetleyicide tanımlanan **Nextsoru** işlevini tetikler.

    ![Sonraki soruyu isteme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Sonraki soruyu isteme")

    *Sonraki soruyu isteme*
5. Sonraki soru görünmelidir. İstediğiniz kadar çok kez soruları cevaplayın. Tüm soruları tamamladıktan sonra ilk soruya dönmeniz gerekir.

    ![Başka bir soru](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Başka bir soru")

    *Sonraki soru*
6. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>Görev 3 – CSS3 kullanarak bir ters animasyon oluşturma

Bu görevde, bir soru yanıtlanarak bir sonraki soru alındığında bir çevir efekti ekleyerek zengin animasyonlar gerçekleştirmek için CSS3 özelliklerini kullanacaksınız.

1. **Çözüm Gezgini**, **geektest** projesinin **Içerik** klasörüne sağ tıklayın ve Ekle ' yi seçin **| Mevcut öğe...** .

    ![Içerik klasörüne varolan bir öğe ekleniyor](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Içerik klasörüne varolan bir öğe ekleniyor")

    *Içerik klasörüne varolan bir öğe ekleniyor*
2. **Varolan öğe Ekle** Iletişim kutusunda **kaynak/varlıklar** klasörüne gidin ve **. css 'yi çevir**' i seçin. **Ekle**'yi tıklatın.

    ![Varlıklardan. css dosyasını ekleme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Varlıklardan. css dosyasını ekleme")

    *Varlıklardan. css dosyasını ekleme*
3. Yeni eklediğiniz **çevir. css** dosyasını açın ve içeriğini inceleyin.
4. **Çevirme dönüşümü** açıklamasını bulun. Bu açıklamanın altındaki stiller, bir &quot;kartı oluşturmak için CSS **perspektifini** ve **rotatey** dönüşümlerini kullanır&quot; efekti çevir.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. Yorumu **ters çevir sırasında bölmenin geri gizlemeyi** bulun. Bu açıklamanın altındaki stil, **arka yüz görünürlüğü** CSS özelliği *gizli*olarak ayarlanarak, yüzlerin arka tarafını gizleyerek görüntüleyicisinden gizler.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. **BundleConfig.cs** dosyasını **uygulama\_başlangıç** klasörü içinde açın ve başvuruyu **&quot;~/Content/CSS&quot;** Style demeti içindeki **Flip. css** dosyasına ekleyin

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. **F5** tuşuna basarak çözümü çalıştırın ve kimlik bilgilerinizle oturum açın.
8. Seçeneklerden birine tıklayarak bir soruyu yanıtlayın. Görünümler arasında geçiş yaparken çevirme efektinin olduğuna dikkat edin.

    ![Çevirme efektiyle soru yanıt verme](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Çevirme efektiyle soru yanıt verme")

    *Çevirme efektiyle soru yanıt verme*
9. Aşağıdaki soruyu almak için **sonraki soru** ' ya tıklayın. Çevirme efekti yeniden görünmelidir.

    ![Aşağıdaki soruyu çevirme efektiyle alma](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Aşağıdaki soruyu çevirme efektiyle alma")

    *Aşağıdaki soruyu çevirme efektiyle alma*

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak şu şekilde nasıl yapılacağını öğrendiniz:

- ASP.NET Scafkatlaması kullanarak bir ASP.NET Web API denetleyicisi oluşturma
- Sonraki test sorusunu almak için bir Web API alma eylemi uygulayın
- Test yanıtlarını depolamak için bir Web API 'SI gönderme eylemi uygulayın
- Visual Studio paket yöneticisi konsolundan AngularJS 'i yükler
- AngularJS şablonlarını ve denetleyicilerini uygulama
- Animasyon efektlerini gerçekleştirmek için CSS3 geçişlerini kullanma
