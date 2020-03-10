---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 yardımcıları, formları ve doğrulaması | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 modeller ve veri erişimi uygulamalı laboratuvarda, veritabanından verileri yüklüyor ve görüntülüyor olursunuz. Bu uygulamalı laboratuvarda,...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539580"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 Yardımcılar, Formlar ve Doğrulama

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

**ASP.NET MVC 4 modeller ve veri erişimi** uygulamalı laboratuvarda, veritabanından verileri yüklüyor ve görüntülüyor olursunuz. Bu uygulamalı laboratuvarda, **müzik deposu** uygulamasına verileri düzenleme özelliği ekleyebilirsiniz.

Bu amaç göz önünde bulundurularak öncelikle Albümler 'in oluşturma, okuma, güncelleştirme ve silme (CRUD) eylemlerini destekleyecek olan denetleyiciyi oluşturacaksınız. Bir HTML tablosunda Albümler özelliklerini görüntülemek için ASP.NET MVC 'nin yapı iskelesi özelliğinden yararlanarak bir dizin görünümü şablonu oluşturacaksınız. Bu görünümü geliştirmek için uzun açıklamaları kesecek özel bir HTML Yardımcısı ekleyeceksiniz.

Daha sonra, veritabanı içindeki albümleri değiştirmenize olanak sağlayacak olan düzenleme ve oluşturma görünümlerini, açılan öğeler gibi form öğelerinin yardımıyla de ekleyeceksiniz.

Son olarak, kullanıcıların bir albümü silmesine izin verirsiniz ve ayrıca bu kişilerin girişlerini doğrulayarak yanlış veri girmesini engelleyebilirsiniz.

Bu uygulamalı laboratuvar, **ASP.NET MVC**'nin temel bilgisine sahip olduğunuzu varsayar. Daha önce **ASP.NET MVC** kullandıysanız, **ASP.NET MVC temelleri** uygulamalı laboratuvarına gitmeniz önerilir.

Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET MVC 4 yardımcıları, formları ve doğrulamasında](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)bulunabilir.

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- CRUD işlemlerini desteklemek için bir denetleyici oluşturma
- Bir HTML tablosunda varlık özelliklerini görüntülemek için bir dizin görünümü oluşturma
- Özel HTML Yardımcısı ekleme
- Düzenleme görünümü oluşturma ve özelleştirme
- HTTP-GET veya HTTP-POST çağrılarına tepki veren eylem yöntemlerine göre ayrım yapın
- Oluşturma görünümü ekleme ve özelleştirme
- Bir varlığın silinmesini işleme
- Kullanıcı girişini doğrulama

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

**Kod parçacıklarını yükleme**

Kolaylık olması için, bu laboratuvar boyunca yönettiğiniz kodun çoğu Visual Studio kod parçacıkları olarak sunulmaktadır. Kod parçacıklarını yüklemek için **.\Source\Setup\CodeSnippets.vsi** dosyasını çalıştırın.

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek B: kod parçacıkları&quot;kullanarak](#AppendixB) bu belgedeki eke başvurabilirsiniz &quot;.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Aşağıdaki alıştırmalarda bu uygulamalı laboratuvar yapılır:

1. [Mağaza Yöneticisi denetleyicisi ve onun dizin görünümü oluşturuluyor](#Exercise1)
2. [HTML Yardımcısı ekleme](#Exercise2)
3. [Düzenleme görünümü oluşturuluyor](#Exercise3)
4. [Oluşturma görünümü ekleme](#Exercise4)
5. [Silme Işlemi işleniyor](#Exercise5)
6. [Doğrulama Ekleme](#Exercise6)
7. [Istemci tarafında unobtrusive jQuery kullanma](#Exercise7)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>Alıştırma 1: mağaza yöneticisi denetleyicisi ve onun dizin görünümü oluşturuluyor

Bu alıştırmada, CRUD işlemlerini desteklemek için yeni bir denetleyici oluşturmayı ve son olarak ASP.NET MVC 'nin yapı iskelesi avantajlarından yararlanarak bir dizin görünümü şablonu oluşturmayı öğreneceksiniz. bir HTML tablosunda Albümler özelliklerini görüntüleme özelliği.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>Görev 1-StoreManagerController oluşturma

Bu görevde, CRUD işlemlerini desteklemek için **Storemanagercontroller** adlı yeni bir denetleyici oluşturacaksınız.

1. **Kaynak/Ex1-Creatingdepotoremanagercontroller/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. Yeni bir denetleyici ekleyin. Bunu yapmak için Çözüm Gezgini içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ve sonra **Denetleyici** komutunu seçin. **Denetleyici** **adını** **storemanagercontroller** olarak değiştirin ve **MVC Controller seçeneğinin boş okuma/yazma eylemleri** seçildiğinden emin olun. **Ekle**'yi tıklatın.

    ![Denetleyici Ekle iletişim kutusu](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Denetleyici Ekle iletişim kutusu")

    *Denetleyici Ekle Iletişim kutusu*

    Yeni bir denetleyici sınıfı oluşturulur. Okuma/yazma eylemleri eklemek için belirttiğiniz için, genel CRUD eylemleri, TODO açıklamaları doldurulmuş olarak oluşturulur ve uygulamaya özel mantık dahil etmek isteyip istemediğini sorar.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>Görev 2-StoreManager dizinini özelleştirme

Bu görevde, veritabanından Albümler listesini içeren bir görünüm döndürmek için StoreManager Dizin eylemi yöntemini özelleştirecek olursunuz.

1. StoreManagerController sınıfında, aşağıdaki *using* yönergelerini ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve formları ve doğrulama-Ex1, MvcMusicStore kullanarak*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. Bir **Musicstoreentities** örneği tutmak Için **storemanagercontroller** öğesine bir alan ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex1 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. Albümler listesini içeren bir görünüm döndürmek için StoreManagerController Dizin eylemini uygulayın.

    Denetleyici eylemi mantığı, daha önce yazılan StoreController 'ın Dizin eylemine çok benzer olacaktır. Görüntülenecek tarz ve sanatçı bilgileri de dahil olmak üzere tüm albümlerini almak için LINQ kullanın.

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex1 StoreManagerController dizini*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>Görev 3-dizin görünümü oluşturma

Bu görevde, **Storemanager** denetleyicisi tarafından döndürülen albüm listesini görüntülemek Için dizin görünümü şablonu oluşturacaksınız.

1. Yeni görünüm şablonunu oluşturmadan önce, **görünümü Ekle Iletişim kutusunun** kullanılacak **Albüm** sınıfını bilmesi için projeyi derlemeniz gerekir. **Derlemeyi Seç | Projeyi derlemek için MvcMusicStore oluşturun** .
2. **Dizin** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin. Bu işlem, **Görünüm Ekle** iletişim kutusunu getirir.

    ![Görünüm Ekle](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Görünüm Ekle")

    *Dizin yönteminin içinden bir görünüm ekleme*
3. Görünüm Ekle iletişim kutusunda görünüm adının **Dizin**olduğunu doğrulayın. Kesin olarak **belirlenmiş görünüm oluştur** seçeneğini belirleyin ve **model sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** seçeneğini belirleyin. **Yapı iskelesi şablonu** açılır **listesinden liste** ' yi seçin. **Görünüm altyapısını** **Razor** 'e ve diğer alanlara varsayılan değerlerini kullanarak bırakın ve **Ekle**' ye tıklayın.

    ![Dizin görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Dizin görünümü ekleme")

    *Dizin görünümü ekleme*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>Görev 4-dizin görünümünün scafkatlama 'ını özelleştirme

Bu görevde, istediğiniz alanları görüntülemesi için ASP.NET MVC scafkatlama özelliğiyle oluşturulan basit görünüm şablonunu ayarlayacaksınız.

> [!NOTE]
> ASP.NET MVC içindeki **scafkatlama** desteği, albüm modelindeki tüm alanları listeleyen basit bir görünüm şablonu oluşturur. **Yapı iskelesi** , türü kesin belirlenmiş bir görünüme başlamak için hızlı bir yol sağlar: görünüm şablonunu el ile yazmak yerine, scafkatlama hızlı bir şekilde varsayılan şablon oluşturur ve oluşturulan kodu değiştirebilirsiniz.

1. Oluşturulan kodu gözden geçirin. Oluşturulan alanların listesi, **Yapı** verilerini görüntülemek için kullanılan aşağıdaki HTML tablosunun bir parçası olacaktır.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. Yalnızca **tarz**, **sanatçı**, **albüm başlığı**ve **Fiyat** alanlarını göstermek için **&lt;tablo&gt;** kodu aşağıdaki kodla değiştirin. Bu, **Albümkimliği** ve **Albüm sanatı URL 'si** sütunlarını siler. Ayrıca, Genreıd ve ArtistId sütunlarını, **artist.Name** ve **genre.Name**'nin bağlı sınıf özelliklerini görüntüleyecek şekilde değiştirir ve **Ayrıntılar** bağlantısını kaldırır.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. Aşağıdaki açıklamaları değiştirin.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5\. Görev-uygulamayı çalıştırma

Bu görevde, **Storemanager** **Dizin** görünümü şablonunun önceki adımların tasarımına göre Albümler listesini görüntülediğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. Bir albüm listesinin **başlık**, **sanatçı** ve **tarzlarını**göstererek görüntülendiğini doğrulamak için URL 'yi **/storemanager** olarak değiştirin.

    ![Albümler listesine göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Albümler listesine göz atma")

    *Albümler listesine göz atma*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>Alıştırma 2: HTML Yardımcısı ekleme

StoreManager Dizin sayfasında bir olası sorun vardır: başlık ve sanatçı adı özelliklerinin ikisi de tablo biçimlendirmesini oluşturmak için yeterince uzun olabilir. Bu alıştırmada, bu metni kesmek için özel bir HTML Yardımcısı eklemeyi öğreneceksiniz.

Aşağıdaki şekilde, küçük bir tarayıcı boyutu kullanırken metnin uzunluğu nedeniyle biçimin nasıl değiştirildiğini görebilirsiniz.

![Kesilmedi metin içeren albümler listesine göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Kesilmedi metin içeren albümler listesine göz atma")

*Kesilmedi metin içeren albümler listesine göz atma*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>Görev 1-HTML yardımcısını genişletme

Bu görevde, ASP.NET MVC görünümleri içinde kullanıma sunulan **HTML** nesnesine **Truncate** 'e yeni bir yöntem ekleyeceksiniz. Bunu yapmak için, ASP.NET MVC tarafından sunulan yerleşik **System. Web. Mvc. HtmlHelper** sınıfına bir **genişletme yöntemi** uygulayacaksınız.

> [!NOTE]
> **Uzantı yöntemleri**hakkında daha fazla bilgi için lütfen bu MSDN makalesini ziyaret edin. [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).

1. **Kaynak/EX2-AddingAnHTMLHelper/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. StoreManager 'ın Dizin görünümünü açın. Bunu yapmak için, Çözüm Gezgini **views** klasörünü ve ardından **storemanager** ' ı genişletin ve **Index. cshtml** dosyasını açın.
3. <strong>Truncate</strong> Helper metodunu tanımlamak için <strong>@model</strong> yönergesinin altına aşağıdaki kodu ekleyin.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>Görev 2-sayfada metin kesiliyor

Bu görevde, görünüm şablonundaki metni kesmek için **Truncate** metodunu kullanacaksınız.

1. StoreManager 'ın Dizin görünümünü açın. Bunu yapmak için, Çözüm Gezgini **views** klasörünü ve ardından **storemanager** ' ı genişletin ve **Index. cshtml** dosyasını açın.
2. **Sanatçı adını** ve albümün **başlığını**gösteren satırları değiştirin. Bunu yapmak için aşağıdaki satırları değiştirin.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Görev 3-uygulamayı çalıştırma

Bu görevde, **Storemanager** **Dizin** görünümü şablonunun albümün başlığını ve sanatçı adını kesen test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. **Başlık** ve **sanatçı** sütunundaki uzun metinlerin KESILDIĞINI doğrulamak için URL 'yi **/storemanager** olarak değiştirin.

    ![Kesilen başlıklar ve sanatçı adları](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Kesilen başlıklar ve sanatçı adları")

    *Kesilen başlıklar ve sanatçı adları*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>Alıştırma 3: düzenleme görünümü oluşturma

Bu alıştırmada, Mağaza yöneticilerinin bir albümü düzenlemesine izin vermek için form oluşturmayı öğreneceksiniz. **/Storemanager/Edit/ID** URL 'ye gözatacağız (**kimliği** düzenlenecek albümün benzersiz kimliği olan kimlik), bu nedenle sunucuya http-get çağrısı yapılıyor.

Denetleyici düzenleme eylemi yöntemi, veritabanından uygun albümü alır, kapsüllemek için bir **Storemanagerviewmodel** nesnesi oluşturur (sanatçı ve tarzların listesi ile birlikte) ve ardından HTML sayfasını kullanıcıya geri işlemek Için bir görünüm şablonuna geçirin. Bu sayfada, albüm özelliklerini düzenlemede metin kutuları ve açılan öğeler içeren bir **&lt;form&gt;** öğesi bulunur.

Kullanıcı, albüm formu değerlerini güncelleştirdikten ve **Kaydet** düğmesine tıkladığında, DEĞIŞIKLIKLER bir http-post çağrısıyla **/Storemanager/Edit/ID**öğesine geri gönderilir. URL son çağrıdaki ile aynı kalsa da, ASP.NET MVC bu zamanın bir HTTP-POST olduğunu belirler ve bu nedenle farklı bir düzenleme eylemi yöntemi yürütür (bir tane **[HttpPost]** ile donatılmış).

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>Görev 1-HTTP-GET düzenleme eylemi yöntemini uygulama

Bu görevde, veritabanından uygun albümü ve tüm tarzların ve sanatçıların listesini almak için düzenleme eylemi yönteminin HTTP-GET sürümünü uygulayacaksınız. Bu verileri, yanıtı işlemek için bir görünüm şablonuna geçirilecek son adımda tanımlanan **Storemanagerviewmodel** nesnesine göre paketleyebilir.

1. **Kaynak/Ex3-CreatingTheEditView/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Storemanagercontroller** sınıfını açın. Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.
3. Uygun **albümün** yanı sıra **tarzların** ve **sanatçıların** listesini almak için **http-get düzenleme** eylemi yöntemini aşağıdaki kodla değiştirin.

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex3 StoreManagerController http-düzenleme EYLEMINI al*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > **System. Collections. Generic** listesi yerine sanatçı ve tarzlar için **System. Web. Mvc** **SelectList** öğesini kullanıyorsunuz.
    > 
    > **SelectList** , HTML açılan listelerini doldurmak ve geçerli seçim gibi şeyleri yönetmek için temizleyici bir yoldur. Denetleyici eyleminde bu ViewModel nesnelerinin örneklendirime ve daha sonra ayarlanması, düzenleme formu senaryosunu temizleyici hale getirir.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>Görev 2-düzenleme görünümü oluşturma

Bu görevde, daha sonra albüm özelliklerini görüntüleyecek olan bir düzenleme görünümü şablonu oluşturacaksınız.

1. Düzenleme görünümünü oluşturun. Bunu yapmak için, eylemi **Düzenle** yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin.
2. Görünüm Ekle iletişim kutusunda görünüm adının **düzenlendiğini**doğrulayın. **Türü kesin belirlenmiş görünüm oluştur** onay kutusunu işaretleyin ve **veri sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** seçeneğini belirleyin. **Yapı iskelesi şablonu** açılır listesinden **Düzenle** ' yi seçin. Diğer alanları varsayılan değerlerine bırakın ve ardından **Ekle**' ye tıklayın.

    ![Düzenleme görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Düzenleme görünümü ekleme")

    *Düzenleme görünümü ekleme*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Görev 3-uygulamayı çalıştırma

Bu görevde, **Storemanager** **düzenleme** görünümü sayfasının, albüm olarak geçirilmiş parametre değerlerini görüntülemesini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. Geçirilen albümün özelliklerinin görüntülendiğini doğrulamak için **/Storemanager/Edit/1** URL 'sini değiştirin.

    ![Albümün düzenleme görünümüne göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Albümün düzenleme görünümüne göz atma")

    *Albümün düzenleme görünümüne göz atma*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>Görev 4-albüm Düzenleyicisi şablonunda açılan listeleri uygulama

Bu görevde, kullanıcının sanatçı ve tarzların listesinden seçim yapabilmesi için son görevde oluşturulan görünüm şablonuna açılan listeleri ekleyeceksiniz.

1. Tüm **Albüm** alan kümesi kodunu aşağıdaki kodla değiştirin:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > Sanatçı ve tarzların seçilmesi için işleme açılan listeleri için bir **HTML. DropDownList** Yardımcısı eklenmiştir. **HTML. DropDownList** 'e geçirilen parametreler şunlardır:
    > 
    > 1. Form alanının adı ( **&quot;ArtistId&quot;** ).
    > 2. Açılan **listenin selectvalues listesi** .

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5\. Görev-uygulamayı çalıştırma

Bu görevde, **Storemanager** **düzenleme** görünümü SAYFASıNıN sanatçı ve tarz kimliği metin alanları yerine açılan listeleri görüntülediğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. Sanatçı ve tarz KIMLIĞI metin alanları yerine açılan listeleri görüntülediğini doğrulamak için URL 'YI **/Storemanager/Edit/1** olarak değiştirin.

    ![Açılır liste ile albümün düzenleme görünümüne göz atma](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Açılır liste ile albümün düzenleme görünümüne göz atma")

    *Albümün düzenleme görünümüne göz atma, bu sefer açılan listeleri*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>Görev 6-HTTP-POST düzenleme eylem yöntemini uygulama

Artık düzenleme görünümü beklendiği gibi görüntülediğine göre, albüme yapılan değişiklikleri kaydetmek için HTTP-POST düzenleme eylemi yöntemini uygulamanız gerekir.

1. Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın. **Storemanagercontroller** ' i **denetleyiciler** klasöründen açın.
2. **Http-post düzenleme** eylemi yöntemi kodunu aşağıdaki kodla değiştirin (yerine geçecek yöntemin iki parametre alan aşırı yüklenmiş sürümü olduğunu unutmayın):

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex3 StoreManagerController http-düzenleme sonrası eylemi*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > Bu yöntem, Kullanıcı görünümün **Kaydet** düğmesine tıkladığında ve veritabanında kalıcı hale getirmek için form değerlerini sunucuya geri gönderirse yürütülür. Dekoratör **[HttpPost]** , YÖNTEMIN bu http-post senaryolarında kullanılması gerektiğini belirtir. Yöntemi bir **Albüm** nesnesi alır. ASP.NET MVC, albüm nesnesini, postalanan &lt;form&gt; değerlerinden otomatik olarak oluşturur.
    > 
    > Yöntemi şu adımları gerçekleştirir:
    > 
    > 1. Model geçerliyse:
    > 
    >     1. Bağlam içindeki albüm girişini, değiştirilen bir nesne olarak işaretlemek için güncelleştirin.
    >     2. Değişiklikleri kaydedin ve dizin görünümüne yeniden yönlendirin.
    > 2. Model geçerli değilse, ViewBag 'i **Genreıd** ve **ArtistId**ile doldurur ve bu durumda kullanıcının gerekli bir güncelleştirmeyi gerçekleştirmesini sağlamak için alınan albüm nesnesiyle birlikte görünümü döndürür.

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>Görev 7-uygulamayı çalıştırma

Bu görevde, **Storemanager düzenleme** görünümü sayfasının güncelleştirilmiş albüm verilerini veritabanına kaydettiğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Storemanager/Edit/1**olarak değiştirin. Albüm başlığını **yüklenecek** şekilde değiştirin ve **Kaydet**' e tıklayın. Albümün başlığının, Albümler listesinde gerçekten değiştirildiğini doğrulayın.

    ![Bir albümü güncelleştirme](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Bir albümü güncelleştirme")

    *Bir albümü güncelleştirme*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>Alıştırma 4: oluşturma görünümü ekleme

Artık **Storemanagercontroller** **düzenleme** özelliğini desteklediğine göre, Bu alıştırmada, Mağaza yöneticilerinin uygulamaya yeni albümler eklemesine Izin vermek için create VIEW şablonu ekleme hakkında bilgi edineceksiniz.

Düzenleme işlevselliğiyle yaptığınız gibi, **Storemanagercontroller** sınıfı içinde iki ayrı yöntem kullanarak oluşturma senaryosunu uygulayacaksınız:

1. Mağaza yöneticileri ilk olarak **/Storemanager/Create** URL 'yi ziyaret ettiğinde bir eylem yöntemi boş bir form görüntüler.
2. İkinci bir eylem yöntemi, mağaza yöneticisinin form içindeki **Kaydet** düğmesine tıkladığı ve DEĞERLERI bir http-post olarak **/Storemanager/Create** URL 'sine geri gönderdiği senaryoyu işleymeyecektir.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>Görev 1-HTTP-GET Create action metodunu uygulama

Bu görevde, tüm tarzların ve sanatçıların bir listesini almak için Create ACTION yönteminin HTTP-GET sürümünü uygulayacaksınız, bu verileri bir **Storemanagerviewmodel** nesnesine paketleyip, daha sonra bir görünüm şablonuna geçirilecek.

1. **Kaynak/EX4-AddingACreateView/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Storemanagercontroller** sınıfını açın. Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.
3. **Oluşturma** eylemi Yöntem kodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-EX4 StoreManagerController http-oluşturma EYLEMINI al*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>Görev 2-oluştur görünümü ekleme

Bu görevde, yeni (boş) bir albüm formu görüntüleyen oluştur görünüm şablonunu ekleyeceksiniz.

1. **Oluşturma** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin. Bu işlem, Görünüm Ekle iletişim kutusunu getirir.
2. Görünüm Ekle iletişim kutusunda görünüm adının **Oluştur**' u doğrulayın. **Türü kesin belirlenmiş görünüm oluştur** seçeneğini belirleyin ve **model sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** öğesini seçin ve **Yapı iskelesi şablonu** açılır listesinden **Oluştur** ' u seçin. Diğer alanları varsayılan değerlerine bırakın ve ardından **Ekle**' ye tıklayın.

    ![Oluşturma görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-Create-View. png")

    *Oluşturma görünümü ekleme*
3. **Genreıd** ve **ArtistId** alanlarını aşağıda gösterildiği gibi bir açılan liste kullanacak şekilde güncelleştirin:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Görev 3-uygulamayı çalıştırma

Bu görevde, **Storemanager** **oluşturma** görünümü sayfasının boş bir albüm formu görüntülediğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Storemanager/Create**olarak değiştirin. Yeni albüm özelliklerini doldurmak için boş bir form görüntülendiğini doğrulayın.

    ![Boş bir formla görünüm oluştur](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Boş bir formla görünüm oluştur")

    *Boş bir formla görünüm oluştur*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>Görev 4-HTTP-POST oluşturma eylemi yöntemi uygulama

Bu görevde, Kullanıcı **Kaydet** düğmesine tıkladığında çağrılacak olan Create ACTıON yönteminin http-post sürümünü uygulayacaksınız. Yöntemi, yeni albümü veritabanına kaydetmeniz gerekir.

1. Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın. **Storemanagercontroller** sınıfını açın. Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.
2. **Http-post oluşturma** eylemi yöntemi kodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-EX4 StoreManagerController http-oluşturma sonrası eylem*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > Oluşturma eylemi, önceki düzenleme eylemi yöntemine oldukça benzer, ancak nesneyi değiştirilmiş olarak ayarlamak yerine bağlamına ekleniyor.

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5\. Görev-uygulamayı çalıştırma

Bu görevde, **Storemanager oluşturma** görünümü sayfasının yeni bir albüm oluşturup ardından Storemanager dizin görünümüne yönlendirmenizi sağlayan bir test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Storemanager/Create**olarak değiştirin. Tüm form alanlarını, aşağıdaki şekilde olduğu gibi yeni bir albüm için verilerle birlikte doldurabilirsiniz:

    ![Albüm oluşturma](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Albüm oluşturma")

    *Albüm oluşturma*
3. Yeni oluşturduğunuz albümü içeren StoreManager dizin görünümüne yönlendirildiğinizi doğrulayın.

    ![Yeni albüm oluşturuldu](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "Yeni albüm oluşturuldu")

    *Yeni albüm oluşturuldu*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>Alıştırma 5: Işlemeyi silme

Albümleri silme özelliği henüz uygulanmadı. Bu alıştırmada ilgili olacak. Daha önce olduğu gibi, **Storemanagercontroller** sınıfı içinde iki ayrı yöntem kullanarak silme senaryosunu uygulayacaksınız:

1. Bir eylem yönteminde bir onay formu görüntülenir
2. İkinci bir eylem yöntemi, form gönderimini işleyecek

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>Görev 1-HTTP-GET silme eylemini uygulama yöntemi

Bu görevde, albümün bilgilerini almak için silme eylemi yönteminin HTTP-Al sürümünü uygulayacaksınız.

1. **Kaynak/eX5-el Lingsilme/başlangıç/** klasör konumunda bulunan **Başlangıç** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Storemanagercontroller** sınıfını açın. Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.
3. Denetleyiciyi Sil eylemi, önceki depo ayrıntıları denetleyicisi eylemiyle tamamen aynıdır: URL 'de belirtilen **kimliği** kullanarak **Albüm** nesnesini veritabanından sorgular ve uygun **görünümü**döndürür. Bunu yapmak için, HTTP-GET **Delete** ACTION yöntemi kodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-eX5 Işleme SILME http-silme EYLEMINI al*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. **Silme** eylemi yönteminin içine sağ tıklayın ve **Görünüm Ekle**' yi seçin. Bu işlem, Görünüm Ekle iletişim kutusunu getirir.
5. Görünüm Ekle iletişim kutusunda görünüm adının **silme**olduğunu doğrulayın. Kesin olarak **belirlenmiş görünüm oluştur** seçeneğini belirleyin ve **model sınıfı** açılır listesinden **Albüm (Mvcmusicstore. modeller)** seçeneğini belirleyin. **Yapı iskelesi şablonu** açılır listesinden **Sil** ' i seçin. Diğer alanları varsayılan değerlerine bırakın ve ardından **Ekle**' ye tıklayın.

    ![Silme görünümü ekleme](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Silme görünümü ekleme")

    *Silme görünümü ekleme*
6. Şablonu Sil, modeldeki tüm alanları gösterir. Yalnızca albümün başlığını gösterebilirsiniz. Bunu yapmak için, görünümün içeriğini aşağıdaki kodla değiştirin:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Görev 2-uygulamayı çalıştırma

Bu görevde, **Storemanager** **silme** görünümü sayfasının bir onay silme formu görüntülediğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Storemanager**olarak değiştirin. **Sil ' e** tıklayarak silinecek bir albüm seçin ve yeni görünümün karşıya yüklendiğini doğrulayın.

    ![Bir albümü silme](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Bir albümü silme")

    *Bir albümü silme*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>Görev 3-HTTP-Delete silme eyleminin uygulanması yöntemi

Bu görevde, Kullanıcı **Sil** düğmesine tıkladığında çağrılacak silme EYLEMI yönteminin http-post sürümünü uygulayacaksınız. Yöntemi, veritabanındaki albümü silmelidir.

1. Gerekirse, Visual Studio penceresine dönmek için tarayıcıyı kapatın. **Storemanagercontroller** sınıfını açın. Bunu yapmak için, **denetleyiciler** klasörünü genişletin ve **StoreManagerController.cs**öğesine çift tıklayın.
2. **Http-post Delete** ACTION yöntemi kodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-eX5 Işleme SILME http-SILME sonrası eylemi*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Görev 4-uygulamayı çalıştırma

Bu görevde, **Storemanager silme** görünümü sayfasının bir albümü silmesine ve sonra Storemanager dizin görünümüne yönlendirmenize olanak tanıyan test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Storemanager**olarak değiştirin. Sil ' e tıklayarak silinecek bir albümü seçin **.** **Sil** düğmesine tıklayarak silmeyi onaylayın:

    ![Bir albümü silme](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Bir albümü silme")

    *Bir albümü silme*
3. **Dizin** sayfasında görünmediğinden albümün silindiğini doğrulayın.

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>Alıştırma 6: doğrulama ekleme

Şu anda, yerinde oluşturduğunuz oluşturma ve düzenleme formları herhangi bir tür doğrulama gerçekleştirmez. Kullanıcı gerekli bir alanı boş bırakır veya fiyat alanında harfler yazarsanız, alacağınız ilk hata veritabanından alınır.

Model sınıfınıza veri ek açıklamaları ekleyerek uygulamaya doğrulama ekleyebilirsiniz. Veri ek açıklamaları, model özelliklerine uygulanmasını istediğiniz kuralların açıklanarak ASP.NET MVC, kullanıcılara uygun iletileri zorlamaya ve görüntülemeye yönelik bir işlem gerçekleştirir.

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>Görev 1-veri ek açıklamaları ekleme

Bu görevde, uygun olduğunda oluşturma ve düzenleme sayfasının doğrulama iletilerini görüntülemesi için, albüm modeline veri ek açıklamaları ekleyeceksiniz.

Basit bir model sınıfı için, bir veri ek açıklaması eklemek, **System. ComponentModel. DataAnnotation**için bir **using** açıklaması eklenerek ve ardından uygun özelliklere bir **[Required]** özniteliği yerleştirerek işlenir. Aşağıdaki örnek, **ad** özelliğini görünümünde gerekli bir alan haline getirir.

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

Bu, Varlık Veri Modeli oluşturulduğu bu uygulama gibi durumlarda biraz daha karmaşıktır. Doğrudan model sınıflarına veri ek açıklamaları eklediyseniz, modeli veritabanından güncelleştirirseniz bunların üzerine yazılır. Bunun yerine, ek açıklamaları tutmak için var olan ve **[Metadatatype]** özniteliğini kullanan model sınıflarıyla ilişkili olan meta veri kısmi sınıflarının kullanımını sağlayabilirsiniz.

1. **Kaynak/Ex6-AddingValidation/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Modeller** klasöründen **Album.cs** öğesini açın.
3. **Album.cs** içeriğini vurgulanan kodla değiştirin, böylece aşağıdakine benzer şekilde görünür:

    > [!NOTE]
    > Satır **[DisplayFormat (ConvertEmptyStringToNull = false)]** , veri alanı veri kaynağında güncellendiğinde, modeldeki boş dizelerin null olarak dönüştürülmeyeceğini gösterir. Bu ayar, Entity Framework veri ek açıklaması alanları doğrulamaktan önce modele null değerler atarken bir özel durumu ortadan kaldırır.

    (Kod parçacığı- *ASP.NET MVC 4 yardımcıları ve Forms ve doğrulama-Ex6 albüm meta verileri kısmi sınıfı*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > Bu **albümün** kısmi sınıfı, veri ek açıklamaları Için **albümümetadata** sınıfına Işaret eden bir **metadatatype** özniteliğine sahiptir. Bunlar, albüm modeline ek açıklama eklemek için kullandığınız bazı veri ek açıklama öznitelikleri şunlardır:
    > 
    > - Gerekli-özelliğin gerekli bir alan olduğunu belirtir
    > - DisplayName-form alanlarında ve doğrulama iletilerinde kullanılacak metni tanımlar
    > - DisplayFormat-veri alanlarının nasıl görüntülendiğini ve biçimlendirildiğini belirtir.
    > - StringLength-dize alanı için maksimum uzunluğu tanımlar
    > - Range-sayısal bir alan için en yüksek ve en küçük değeri verir
    > - ScaffoldColumn-düzenleyici formlarından alanları gizlemeye Izin verir

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Görev 2-uygulamayı çalıştırma

Bu görevde, son görevde seçilen görünen adları kullanarak sayfaların oluşturulması ve düzenlenmesi alanlarını doğruladığını test edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Storemanager/Create**olarak değiştirin. Görünen adların, kısmi sınıftaki **(albümle Ilgili** **Albüm sanatı URL 'si** gibi) eşleşen olanlarla eşleştiğini doğrulayın
3. Formu doldurmadan **Oluştur**' a tıklayın. Karşılık gelen doğrulama iletilerini almanızı doğrulayın.

    ![Oluştur sayfasındaki doğrulanan alanlar](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Oluştur sayfasındaki doğrulanan alanlar")

    *Oluştur sayfasındaki doğrulanan alanlar*
4. Aynı olduğunu, **düzenleme** sayfasıyla aynı olduğunu doğrulayabilirsiniz. URL 'YI **/Storemanager/Edit/1** olarak değiştirin ve görünen adların kısmi sınıftaki ( **albüm için albümünüz yerine albüm sanatı URL 'si** **gibi) eşleşip**eşleştiğini doğrulayın. **Başlığı** ve **fiyat** alanlarını boşaltın ve **Kaydet**' e tıklayın. Karşılık gelen doğrulama iletilerini almanızı doğrulayın.

    ![Düzenleme sayfasında doğrulanan alanlar](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *Düzenleme sayfasında doğrulanan alanlar*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>Alıştırma 7: Istemci tarafında unobtrusive jQuery kullanma

Bu alıştırmada, istemci tarafında MVC 4 unobtrusive doğrulamasını nasıl etkinleştireceğinizi öğreneceksiniz.

> [!NOTE]
> Unobtrusive jQuery, satır içi istemci betikleri dahil etmek yerine sunucuda eylem yöntemlerini çağırmak için Data-Ajax ön eki JavaScript 'ı kullanır.

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>Görev 1-Obtrusive jQuery 'ı etkinleştirmeden önce uygulamayı çalıştırma

Bu görevde, her iki doğrulama modelini de karşılaştırmak için jQuery 'i eklemeden önce uygulamayı çalıştıracaksınız.

1. **Kaynak/Ex7-UnobtrusivejQueryValidation/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. Uygulamayı çalıştırmak için **F5**'e basın.
3. Proje giriş sayfasında başlar. Doğrulama iletilerini aldığını doğrulamak için **/Storemanager/Create** ' e gözatıp Formu doldurmadan **Oluştur** ' a tıklayın:

    ![İstemci doğrulaması devre dışı](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "İstemci doğrulaması devre dışı")

    *İstemci doğrulaması devre dışı*
4. Tarayıcıda, HTML kaynak kodunu açın:

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>Görev 2-Obtrusive Istemci doğrulamasını etkinleştirme

Bu görevde, varsayılan olarak tüm New ASP.NET MVC 4 projelerinde false olarak ayarlanmış olan **Web. config** dosyasından jQuery **unobtrusive istemci doğrulamasını** etkinleştirecektir. Bunlara ek olarak, jQuery 'in Istemci doğrulaması işini sorunsuz hale getirmek için gerekli betiklerin başvurularını eklersiniz.

1. Proje kökünde **Web. config** dosyasını açın ve **ClientValidationEnabled** ve **Unobtrusivejavascriptenabled** anahtarları değerlerinin **true**olarak ayarlandığından emin olun.

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > Aynı sonuçları almak için Global.asax.cs adresindeki kodla istemci doğrulamasını da etkinleştirebilirsiniz:
    > 
    > **HtmlHelper. ClientValidationEnabled = true;**
    > 
    > Ek olarak, özel bir davranışa sahip olmak için herhangi bir denetleyiciye ClientValidationEnabled özniteliğini de atayabilirsiniz.
2. **Views\storemanager**'da **Create. cshtml** dosyasını açın.
3. Aşağıdaki betik dosyalarının **jQuery. Validate** ve **jQuery. Validate. unobtrusive**' &quot; **~/paketles/jqueryval**&quot; demeti aracılığıyla görünümde başvurulduğundan emin olun.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > Tüm bu jQuery kitaplıkları MVC 4 yeni projelere dahil edilmiştir. Projenin **/Scripts** klasöründe daha fazla kitaplık bulabilirsiniz.
    > 
    > Bu doğrulama kitaplıklarının çalışmasını sağlamak için jQuery Framework kitaplığına bir başvuru eklemeniz gerekir. Bu başvuru **\_Layout. cshtml** dosyasına zaten eklendiğinden, bu görünümü bu görünüme eklemeniz gerekmez.

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>Görev 3-uygulamayı unobtrusive doğrulamasını kullanarak çalıştırma

Bu görevde, Kullanıcı yeni bir albüm oluşturduğunda **Storemanager** oluşturma görünüm şablonu jQuery kitaplıklarını kullanarak istemci tarafı doğrulaması gerçekleştireceğini test edersiniz.

1. Uygulamayı çalıştırmak için **F5**'e basın.
2. Proje giriş sayfasında başlar. Doğrulama iletilerini aldığını doğrulamak için **/Storemanager/Create** ' e gözatıp Formu doldurmadan **Oluştur** ' a tıklayın:

    ![JQuery özellikli istemci doğrulaması](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "JQuery özellikli istemci doğrulaması")

    *JQuery özellikli istemci doğrulaması*
3. Tarayıcıda, oluştur görünümü için kaynak kodunu açın:

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > Her istemci doğrulama kuralı için unobtrusive jQuery, Data-Val-*RuleName*=&quot;*Message*&quot;olan bir öznitelik ekliyor. Aşağıda, istemci doğrulaması gerçekleştirmek için, bir Untastrusjquery 'ın HTML giriş alanına eklediği etiketlerin listesi verilmiştir:
   > 
   > - Veri-Val
   > - Veri-değer-sayı
   > - Veri Val aralığı
   > - Veri-değer-aralığı-min/Data-Val-Range-Max
   > - Veri-Val-gerekli
   > - Veri-değer uzunluğu
   > - Veri-değer-Uzunluk-Max/Data-Val-length-min
   > 
   > Tüm veri değerleri model **veri ek açıklaması**ile doldurulur. Daha sonra, sunucu tarafında çalışan tüm mantık istemci tarafında çalıştırılabilir. Örneğin, Price özniteliği modelde aşağıdaki veri ek açıklamasına sahiptir:
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > Unobtrusive jQuery kullandıktan sonra, oluşturulan kod:
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak, kullanıcıların veritabanında depolanan verileri aşağıdakilerin kullanımıyla nasıl değiştirdiklerini öğrendiniz:

- Dizin, oluşturma, düzenleme, silme gibi denetleyici eylemleri
- ASP.NET MVC 'nin bir HTML tablosunda özellikleri görüntülemek için yapı iskelesi özelliği
- Kullanıcı deneyimini geliştirmek için özel HTML Yardımcıları
- HTTP-GET veya HTTP-POST çağrılarına tepki veren eylem yöntemleri
- Oluşturma ve düzenleme gibi benzer görünüm şablonlarına yönelik paylaşılan bir düzenleyici şablonu
- Açılan öğeler gibi form öğeleri
- Model doğrulaması için veri ek açıklamaları
- JQuery unobtrusive kitaplığı kullanarak istemci tarafı doğrulaması

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *Web için VS Express kutucuğu*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Ek B: kod parçacıklarını kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
