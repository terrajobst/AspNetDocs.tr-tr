---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework yapı Iskelesi ve geçişleri | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 denetleyici yöntemlerine alışkın değilseniz veya &quot;yardımcıları, formları ve doğrulama&quot; uygulamalı laboratuvarını tamamladıysanız, farkında olmanız gerekir...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598905"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework İskele Oluşturma ve Geçişler

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 denetleyici yöntemlerine alışkın değilseniz veya &quot;yardımcıları, formları ve doğrulama&quot; uygulamalı laboratuvarını tamamladıysanız, uygulama arasında tekrarlandığı herhangi bir veri varlığını oluşturma, güncelleştirme, listeleme ve kaldırma mantığının birçoğunun olduğunu bilmeniz gerekir. Bunun değil, modelinizde yapılacak birkaç sınıf varsa, her bir varlık işlemi için POST ve GET eylem yöntemlerini ve görünümlerin her birini yazmak için önemli bir zaman harcamanız gerekecektir.

Bu laboratuvarda, uygulamanızın CRUD (oluşturma, okuma, güncelleştirme ve silme) temelini otomatik olarak oluşturmak için ASP.NET MVC 4 scafkatını nasıl kullanacağınızı öğreneceksiniz. Basit bir model sınıfından başlayarak ve tek bir kod satırı yazmadan, tüm CRUD işlemlerini ve tüm gerekli görünümleri içerecek bir denetleyici oluşturacaksınız. Basit çözümü oluşturup çalıştırdıktan sonra, veri işleme için MVC mantığı ve görünümleri ile birlikte uygulama veritabanının oluşturulması gerekir.

Ayrıca, uygulamanın tamamında model güncelleştirmeleri gerçekleştirmek için Entity Framework geçişlerini kullanmanın ne kadar kolay olduğunu öğreneceksiniz. Entity Framework geçişleri, model basit adımlarla değiştirildikten sonra veritabanınızı değiştirmenize izin verir. Bunların hepsi göz önünde bulundurularak, ASP.NET MVC 4 ' ün en son özelliklerinden yararlanarak web uygulamalarını daha verimli bir şekilde oluşturup koruyabileceksiniz.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit yayımlarından](https://aka.ms/webcamps-training-kit)erişilebilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET MVC 4 ' te yapı iskelesi ve geçişleri Entity Framework](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)bulunabilir.

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Denetleyicilerde CRUD işlemleri için ASP.NET scafkatlarını kullanın.
- Entity Framework geçişleri kullanarak veritabanı modelini değiştirin.

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

Aşağıdaki alıştırma, bu uygulamalı Laboratuvarı yapar:

1. [Entity Framework geçişleri ile ASP.NET MVC 4 Scafkatlaması kullanma](#Exercise1)

> [!NOTE]
> Bu alıştırma, Alıştırmayı tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alıştırmaya yönelik ek yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>Alıştırma 1: Entity Framework geçişleri ile ASP.NET MVC 4 Scafkatlama kullanma

ASP.NET MVC yapı iskelesi, CRUD işlemlerini standartlaştırılmış bir şekilde oluşturmanın hızlı bir yolunu sağlar. bu sayede uygulamanızın veritabanı katmanıyla etkileşime geçmesini sağlayan gerekli mantık oluşturulur.

Bu alıştırmada, CRUD yöntemlerini oluşturmak için önce kod ile ASP.NET MVC 4 scafkatlamayı nasıl kullanacağınızı öğreneceksiniz. Daha sonra, Entity Framework geçişlerini kullanarak modelinizin değişiklikleri uygulamayı nasıl güncelleştireceğinizi öğreneceksiniz.

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>Görev 1-yapı Iskelesi kullanarak yeni bir ASP.NET MVC 4 projesi oluşturma

1. Zaten açık değilse, **Visual Studio 2012**' u başlatın.
2. **Dosya Seç | Yeni proje**. Yeni proje iletişim kutusunda, **görsel C# altında | Web** bölümünde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi **MVC4andEFMigrations** olarak adlandırın ve bu laboratuvarın **Source\ex1-usingmvc4scaffoldıngefgeçişler** klasörüne ayarlayın. **Çözüm adını** **Başlangıç** olarak ayarlayın ve **çözüm için dizin oluşturma** onay işaretli olduğundan emin olun. **Tamam**’a tıklayın.

    ![Yeni ASP.NET MVC 4 projesi Iletişim kutusu](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "Yeni ASP.NET MVC 4 projesi Iletişim kutusu")

    *Yeni ASP.NET MVC 4 projesi Iletişim kutusu*
3. **Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** şablonunu seçin ve **Razor** 'nin seçili **Görünüm altyapısı**olduğundan emin olun. Projeyi oluşturmak için **Tamam**'a tıklayın.

    ![Yeni ASP.NET MVC 4 Internet uygulaması](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "Yeni ASP.NET MVC 4 Internet uygulaması")

    *Yeni ASP.NET MVC 4 Internet uygulaması*
4. Çözüm Gezgini **modeller** ' a sağ tıklayın ve Ekle | ' yi seçin.Basit bir sınıf kişisi (POCO) oluşturmak için sınıfı. **Kişiyi** adlandırın ve **Tamam**' a tıklayın.
5. Kişi sınıfını açın ve aşağıdaki özellikleri ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 ve Entity Framework geçişleri-Ex1 Person özellikleri*)

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. Oluştur 'a tıklayın **|** Değişiklikleri kaydetmek ve projeyi derlemek Için çözüm oluşturun.

    ![Uygulamayı oluşturma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Uygulamayı oluşturma")

    *Uygulamayı oluşturma*
7. Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Denetleyici**.
8. Denetleyiciyi *personcontroller* olarak adlandırın ve aşağıdaki değerlerle **Yapı iskelesi seçeneklerini** doldurun.

   1. **Şablon** açılan listesinde, **Entity Framework seçeneğini kullanarak okuma/yazma eylemleri ve görünümleri ile MVC denetleyicisi** ' ni seçin.
   2. **Model sınıfı** aşağı açılan listesinde **kişi** sınıfını seçin.
   3. **Veri bağlamı sınıfı** listesinde **yeni veri bağlamı&lt;...&gt;** öğesini seçin. Herhangi bir ad seçin ve **Tamam**' a tıklayın.
   4. **Görünümler** açılan listesinde, **Razor** 'nin seçili olduğundan emin olun.

      ![Yapı iskelesi ile kişi denetleyicisi ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Yapı iskelesi ile kişi denetleyicisi ekleme")

      *Yapı iskelesi ile kişi denetleyicisi ekleme*
9. Yeni denetleyiciyi yapı iskelesi içeren bir kişiye oluşturmak için **Ekle** ' ye tıklayın. Artık denetleyici eylemlerinin yanı sıra görünümleri de oluşturmuş oldunuz.

    ![Yapı iskelesi ile kişi denetleyicisi oluşturduktan sonra](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "Yapı iskelesi ile kişi denetleyicisi oluşturduktan sonra")

    *Yapı iskelesi ile kişi denetleyicisi oluşturduktan sonra*
10. **Personcontroller** sınıfını açın. Tam CRUD eylem yöntemlerinin otomatik olarak oluşturulduğuna dikkat edin.

   ![Kişi denetleyicisinin içinde](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Kişi denetleyicisinin içinde")

   *Kişi denetleyicisinin içinde*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>Görev 2-uygulamayı çalıştırma

Bu noktada, veritabanı henüz oluşturulmamış. Bu görevde, uygulamayı ilk kez çalıştıracak ve CRUD işlemlerini test edersiniz. Veritabanı, Code First ile anında oluşturulur.

1. Uygulamayı çalıştırmak için **F5**'e basın.
2. Tarayıcıda, kişi sayfasını açmak için URL 'ye **/Person** ekleyin.

    ![Uygulamanın ilk çalıştırması](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Uygulamanın ilk çalıştırması")

    *Uygulama: ilk çalıştırma*
3. Artık kişi sayfalarını araştırıp CRUD işlemlerini test edersiniz.

    1. Yeni bir kişi eklemek için **Yeni oluştur** ' a tıklayın. Ad ve soyadı girin ve **Oluştur**' a tıklayın.

        ![Yeni bir kişi ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Yeni bir kişi ekleme")

        *Yeni bir kişi ekleme*
    2. Kişinin listesinde, öğeleri silebilir, düzenleyebilir veya ekleyebilirsiniz.

        ![kişi listesi](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "kişi listesi")

        *Kişi listesi*
    3. Kişinin ayrıntılarını açmak için **Ayrıntılar** ' a tıklayın.

        ![Kişinin ayrıntıları](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Kişinin ayrıntıları")

        *Kişinin ayrıntıları*
4. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün. Tek bir kod satırı yazmak zorunda kalmadan, uygulamanız genelinde, modelden görünümler 'e kadar tüm CRUD 'yi oluşturduğunuza dikkat edin!

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>Görev 3-Entity Framework geçişleri kullanarak veritabanını güncelleştirme

Bu görevde veritabanını Entity Framework geçişleri kullanarak güncelleşolursunuz. Entity Framework geçişleri özelliğini kullanarak, modeli değiştirme ve veritabanlarınızdaki değişiklikleri yansıtan ne kadar kolay olduğunu fark edersiniz.

1. Paket Yöneticisi konsolunu açın. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.
2. Paket Yöneticisi konsolunda aşağıdaki komutu girin:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![Geçişleri etkinleştirme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Geçişleri etkinleştirme")

    *Geçişleri etkinleştirme*

    Enable-Migration komutu, veritabanını başlatmak için bir komut dosyası içeren **geçişler** klasörünü oluşturur.

    ![Geçişler klasörü](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Geçişler klasörü")

    *Geçişler klasörü*
3. **Configuration.cs** dosyasını geçişler klasöründe açın. Sınıf oluşturucusunu bulun ve **Automaticmigrationsenabled** değerini *true*olarak değiştirin.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. Kişi sınıfını açın ve kişinin ikinci adı için bir öznitelik ekleyin. Bu yeni öznitelikle, modeli değiştiriyorsunuz.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. **Derlemeyi Seç |** Uygulamayı oluşturmak için menüdeki çözümü oluşturun.

    ![Uygulamayı oluşturma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Uygulamayı oluşturma")

    *Uygulamayı oluşturma*
6. Paket Yöneticisi konsolunda aşağıdaki komutu girin:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    Bu komut, veri nesnelerinde değişikliklere bakar ve sonra veritabanına uygun şekilde değişiklik yapmak için gerekli komutları ekler.

    ![İkinci adı ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "İkinci adı ekleme")

    *İkinci adı ekleme*
7. Seçim Değişiklik güncelleştirmesiyle bir SQL betiği oluşturmak için aşağıdaki komutu çalıştırabilirsiniz. Bu, veritabanını el ile güncelleştirmenizi sağlar (Bu durumda gerekli değildir) veya değişiklikleri diğer veritabanlarına uygulamanız gerekir:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![SQL betiği oluşturma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL betiği oluşturma")

    *SQL betiği oluşturma*

    ![SQL betiği güncelleştirmesi](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL betiği güncelleştirmesi")

    *SQL betiği güncelleştirmesi*
8. Paket Yöneticisi konsolunda, veritabanını güncelleştirmek için aşağıdaki komutu girin:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![Veritabanı güncelleştiriliyor](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Veritabanını Güncelleştirme")

    *Veritabanı güncelleştiriliyor*

    Bu, **kişi** sınıfının geçerli tanımıyla eşleşecek şekilde **kişiler** tablosuna **MiddleName** sütununu ekler.
9. Veritabanı güncelleştirildikten sonra denetleyici klasörüne sağ tıklayın ve Ekle | ' yi seçin.Kişi denetleyicisini yeniden eklemek için denetleyici (aynı değerlerle tamamlanır). Bu işlem, yeni özniteliği ekleyen mevcut yöntemleri ve görünümleri güncelleştirir.

    ![Denetleyici güncelleştirmesi ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Denetleyici güncelleştirmesi ekleme")

    *Denetleyiciyi güncelleştirme*
10. **Ekle**'yi tıklatın. Sonra, **PersonController.cs üzerine yazma** değerlerini ve **Ilişkili görünümlerin üzerine yazın** ve **Tamam**' a tıklayın.

   ![Denetleyici üzerine yazma ekleme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *Denetleyiciyi güncelleştirme*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-uygulamayı çalıştırma

1. Uygulamayı çalıştırmak için **F5**'e basın.
2. **/Person**öğesini açın. Verilerin korunduğu, ortadaki Ad sütununun eklendiğine dikkat edin.

    ![İkinci ad eklendi](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "İkinci ad eklendi")

    *İkinci ad eklendi*
3. **Düzenle**' ye tıklarsanız, geçerli kişiye bir göbek adı ekleyebileceksiniz.

    ![Göbek adı sürümü](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Göbek adı sürümü")

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı laboratuvarda herhangi bir model sınıfı kullanarak ASP.NET MVC 4 yapı Iskelesi ile CRUD işlemleri oluşturmaya yönelik basit adımları öğrendiniz. Daha sonra, Entity Framework geçişleri kullanarak, uygulamanızda veritabanından görünümlere kadar uçtan uca güncelleştirme gerçekleştirmeyi öğrendiniz.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) kısmına gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *Web için VS Express kutucuğu*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Ek B: kod parçacıklarını kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
