---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 modeller ve veri erişimi | Microsoft Docs
author: rick-anderson
description: "Note: Bu uygulamalı laboratuvar, ASP.NET MVC 'nin temel bilgisine sahip olduğunuzu varsayar. Daha önce ASP.NET MVC kullandıysanız, ASP.NET MVC 4 ' ün üzerinde gitmeniz önerilir..."
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560202"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 Modelleri ve Veri Erişimi

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

Bu uygulamalı laboratuvar, **ASP.NET MVC**'nin temel bilgisine sahip olduğunuzu varsayar. Daha önce **ASP.NET MVC** kullandıysanız, **ASP.NET MVC 4 temel** uygulamalı laboratuvarına gitmeniz önerilir.

Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET MVC 4 modelleriyle ve veri erişiminde](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)bulunabilir.

**ASP.NET MVC temelleri** uygulamalı laboratuvarda, denetleyicilerden görünüm şablonlarına sabit kodlanmış veriler geçirdik. Ancak gerçek bir Web uygulaması oluşturmak için gerçek bir veritabanı kullanmak isteyebilirsiniz.

Bu uygulamalı laboratuvar, müzik mağazası uygulaması için gereken verileri depolamak ve almak üzere bir veritabanı altyapısını nasıl kullanacağınızı gösterir. Bunu gerçekleştirmek için, var olan bir veritabanıyla başlayıp Varlık Veri Modeli oluşturacaksınız. Bu laboratuvarda, **Database First** yaklaşımı ve **Code First** yaklaşımını karşılacaksınız.

Ancak, **model First** yaklaşımını de kullanabilir, araçları kullanarak aynı modeli oluşturabilir ve sonra veritabanını buradan oluşturabilirsiniz.

![Database First ve Model First karşılaştırması](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First ve Model First karşılaştırması")

*Database First ve Model First karşılaştırması*

Modeli oluşturduktan sonra, depolama görünümlerinde, sabit kodlanmış veriler yerine veritabanından alınan verileri sağlamak için StoreController 'da uygun ayarlamaları yaparsınız. StoreController görünüm şablonlarına aynı ViewModel döndürmesini sağladığından, veriler veritabanından geldiği halde görünüm şablonlarına herhangi bir değişiklik yapmanız gerekmez.

**Code First yaklaşımı**

Code First yaklaşım, genellikle Framework ile bağlanmış sınıfları oluşturmadan kodu koddan tanımlamanızı sağlar.

Önce kod içinde, model nesneleri POCOs ile tanımlanır, &quot;düz eski CLR nesneleri&quot;. POCOs, devralma gerektirmeyen ve arabirimleri uygulamayan basit düz sınıflardır. Veritabanından otomatik olarak veritabanı oluşturabilir veya var olan bir veritabanını kullanabilir ve koddan sınıf eşlemesi oluşturabilirsiniz.

Bu yaklaşımı kullanmanın avantajları,, POCOs sınıfları eşleme çerçevesiyle ilişkili olmadığından, modelin Kalıcılık çerçevesinden (Bu durumda Entity Framework) bağımsız kaldığı bir avantajdır.

> [!NOTE]
> Bu laboratuvar, ASP.NET MVC 4 ' ü ve bu uygulamalı laboratuvarda gösterilen özelliklere uyacak şekilde özelleştirilmiş ve küçültülmüş bir müzik deposu örnek uygulaması sürümünü temel alır.
> 
> Tüm **müzik deposu** öğreticisi uygulamasını araştırmak isterseniz, bunu [MVC-müzik-mağaza](https://github.com/evilDave/MVC-Music-Store)' da bulabilirsiniz.

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

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek isterseniz, [Ek C: kod parçacıkları&quot;kullanarak](#AppendixC) bu belgedeki eke başvurabilirsiniz &quot;.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alýþtýrmalardan oluşur:

1. [Alıştırma 1: veritabanı ekleme](#Exercise1)
2. [Alıştırma 2: Code First kullanarak veritabanı oluşturma](#Exercise2)
3. [Alıştırma 3: veritabanını parametrelerle sorgulama](#Exercise3)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **35 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>Alıştırma 1: veritabanı ekleme

Bu alıştırmada, verileri tüketmek için MusicStore uygulamasının tablolarıyla bir veritabanını nasıl ekleyeceğinizi öğreneceksiniz. Veritabanı modeliyle oluşturulduktan ve çözüme eklendikten sonra, sabit kodlanmış değerler kullanmak yerine, veritabanından alınan verileri görüntüleme şablonuna sağlamak için StoreController sınıfını değiştirirsiniz.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>Görev 1-veritabanı ekleme

Bu görevde, bir daha önceden oluşturulmuş bir veritabanını MusicStore uygulamasının ana tablolarıyla çözüme ekleyeceksiniz.

1. **Kaynak/Ex1-AddingADatabaseDBFirst/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Mvcmusicstore** veritabanı dosyası ekleyin. Bu uygulamalı laboratuvarda, **Mvcmusicstore. mdf**adlı önceden oluşturulmuş bir veritabanını kullanacaksınız. Bunu yapmak için, **uygulama\_veri** klasörüne sağ tıklayın, **Ekle** ' nin üzerine gelin ve **var olan öğe**' ye tıklayın. **\Source\varlıklar** ' a göz atın ve **Mvcmusicstore. mdf** dosyasını seçin.

    ![Varolan bir öğe ekleniyor](aspnet-mvc-4-models-and-data-access/_static/image2.png "Varolan bir öğe ekleniyor")

    *Varolan bir öğe ekleniyor*

    ![MvcMusicStore. mdf veritabanı dosyası](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore. mdf veritabanı dosyası")

    *MvcMusicStore. mdf veritabanı dosyası*

    Veritabanı projeye eklendi. Veritabanı çözüm içinde bulunduğunda bile, farklı bir veritabanı sunucusunda barındırıldığından bu dosyayı sorgulayabilir ve güncelleştirebilirsiniz.

    ![MvcMusicStore veritabanı Çözüm Gezgini](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore veritabanı Çözüm Gezgini")

    *MvcMusicStore veritabanı Çözüm Gezgini*
3. Veritabanıyla olan bağlantıyı doğrulayın. Bunu yapmak için, bir bağlantı kurmak üzere **Mvcmusicstore. mdf** öğesine çift tıklayın.

    ![MvcMusicStore. mdf 'e bağlanılıyor](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore. mdf 'e bağlanılıyor")

    *MvcMusicStore. mdf 'e bağlanılıyor*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>Görev 2-veri modeli oluşturma

Bu görevde, önceki görevde eklenen veritabanıyla etkileşim kurmak için bir veri modeli oluşturacaksınız.

1. Veritabanını temsil edecek bir veri modeli oluşturun. Bunu yapmak için, Çözüm Gezgini **modeller** klasörüne sağ tıklayın, **Ekle** ' nin üzerine gelin ve ardından **Yeni öğe**' ye tıklayın. **Yeni öğe Ekle** Iletişim kutusunda **veri** şablonu ' nu ve ardından **ADO.net varlık veri modeli** öğesini seçin. Veri modeli adını **StoreDB. edmx** olarak değiştirin ve **Ekle**' ye tıklayın.

    ![StoreDB ADO.NET Varlık Veri Modeli ekleme](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET Varlık Veri Modeli ekleme")

    *StoreDB ADO.NET Varlık Veri Modeli ekleme*
2. **Varlık veri modeli Sihirbazı** görüntülenir. Bu sihirbaz, model katmanının oluşturulmasında size kılavuzluk eder. Modelin yakın zamanda eklenen mevcut veritabanına göre oluşturulması gerektiğinden, **veritabanından oluştur** ' u seçin ve **İleri**' ye tıklayın.

    ![Model içeriğini seçme](aspnet-mvc-4-models-and-data-access/_static/image7.png "Model içeriğini seçme")

    *Model içeriğini seçme*
3. Bir veritabanından model oluştururken, kullanılacak bağlantıyı belirtmeniz gerekecektir. **Yeni bağlantı**' ya tıklayın.
4. **Microsoft SQL Server veritabanı dosyası** ' nı seçin ve **devam**' a tıklayın.

    ![Veri kaynağını seçin](aspnet-mvc-4-models-and-data-access/_static/image8.png "Veri kaynağını seçin")

    *Veri kaynağı seç iletişim kutusu*
5. **Araştır** ' a tıklayın ve **App\_Data** klasöründe bulduğunuz **mvcmusicstore. mdf** veritabanını seçip **Tamam**' a tıklayın.

    ![Bağlantı özellikleri](aspnet-mvc-4-models-and-data-access/_static/image9.png "Bağlantı özellikleri")

    *Bağlantı özellikleri*
6. Oluşturulan sınıf, varlık bağlantı dizesiyle aynı ada sahip olmalıdır, bu nedenle adını **Musicstoreentities** olarak değiştirin ve **İleri**' ye tıklayın.

    ![Veri bağlantısı seçiliyor](aspnet-mvc-4-models-and-data-access/_static/image10.png "Veri bağlantısı seçiliyor")

    *Veri bağlantısı seçiliyor*
7. Kullanılacak veritabanı nesnelerini seçin. Varlık modeli yalnızca veritabanının tablolarını kullanacak şekilde, **Tablolar** seçeneğini belirleyip **modeldeki yabancı anahtar sütunlarını dahil et ' in** ve ayrıca **üretilen nesne adları** seçeneklerinin de seçili olduğundan emin olun. Model ad alanını **Mvcmusicstore. model** olarak değiştirip **son**' a tıklayın.

    ![Veritabanı nesnelerini seçme](aspnet-mvc-4-models-and-data-access/_static/image11.png "Veritabanı nesnelerini seçme")

    *Veritabanı nesnelerini seçme*

    > [!NOTE]
    > Bir güvenlik uyarısı iletişim kutusu gösteriliyorsa, şablonu çalıştırmak ve model varlıkları için sınıflar oluşturmak üzere **Tamam** ' a tıklayın.
8. Veritabanına yönelik bir varlık diyagramı görüntülenir, ancak her bir tabloyu veritabanına eşleyen ayrı bir sınıf oluşturulur. Örneğin, **Albümler** tablosu, tablodaki her sütunun bir sınıf özelliği ile eşleşmeyeceği bir **Albüm** sınıfı tarafından temsil edilir. Bu, veritabanındaki satırları temsil eden nesneleri sorgulamanızı ve bunlarla çalışmanızı sağlar.

    ![Varlık diyagramı](aspnet-mvc-4-models-and-data-access/_static/image12.png "Varlık diyagramı")

    *Varlık diyagramı*

    > [!NOTE]
    > T4 şablonları (. tt), varlık sınıfları oluşturmak için kodu çalıştırır ve aynı ada sahip mevcut sınıfların üzerine yazar. Bu örnekte, sınıfların &quot;albüm&quot;, &quot;tarz&quot; ve &quot;sanatçı&quot; oluşturulan kodla üzerine yazıldı.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>Görev 3-uygulamayı oluşturma

Bu görevde, model oluşturma, **Albüm**, **tarz** ve **sanatçı** model sınıflarını kaldırmakla birlikte, projenin yeni veri modeli sınıflarını kullanarak başarılı bir şekilde yapıdığına yönelik olarak kontrol edersiniz.

1. **Build** menü öğesini seçerek projeyi derleyin ve ardından **MvcMusicStore**' u oluşturun.

    ![Projeyi oluşturma](aspnet-mvc-4-models-and-data-access/_static/image13.png "Projeyi oluşturma")

    *Projeyi oluşturma*
2. Proje başarıyla oluşturulur. Neden hala çalışıyor? Veritabanı tablolarında, kaldırılan sınıflar **albümü** ve **tarzında**kullanmakta olduğunuz özellikleri içeren alanlar bulunduğundan, bu BT işe yarar.

    ![Derlemeler başarılı oldu](aspnet-mvc-4-models-and-data-access/_static/image14.png "Derlemeler başarılı oldu")

    *Derlemeler başarılı oldu*
3. Tasarımcı varlıkları diyagram biçiminde görüntülüyor olsa da gerçekte C# sınıflardır. Çözüm Gezgini **StoreDB. edmx** düğümünü genişletin ve ardından **StoreDB.tt**yeni oluşturulan varlıkları görürsünüz.

    ![Oluşturulan dosyalar](aspnet-mvc-4-models-and-data-access/_static/image15.png "Oluşturulan dosyalar")

    *Oluşturulan dosyalar*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>Görev 4-veritabanını sorgulama

Bu görevde, sabit kodlanmış veriler kullanmak yerine, bilgileri almak için veritabanını sorgulayan için StoreController sınıfını güncelleşolursunuz.

1. **Controllers\storecontroller.cs** dosyasını açın ve aşağıdaki alanı sınıfına, **StoreDB**adlı bir **musicstoreentities** sınıfının örneğini tutacak şekilde ekleyin:

    (Kod parçacığı- *modeller ve veri erişimi-Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **Musicstoreentities** sınıfı, veritabanındaki her tablo için bir koleksiyon özelliği sunar. Tüm **albümlerle**bir tarzın alınması için **gözatmayı** eylem yöntemini güncelleştirin.

    (Kod parçacığı- *modeller ve veri erişimi-Ex1 Store tarama*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > Bu koleksiyonlara karşı kesin türü belirtilmiş sorgu ifadeleri yazmak için **LINQ** (dil ile tümleşik sorgu) adlı bir .NET özelliği kullanıyorsunuz. Bu, veritabanına karşı kod yürütecek ve programlayabileceğiniz nesneleri döndürmeyecektir.
    > 
    > LINQ hakkında daha fazla bilgi için lütfen [MSDN sitesini](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)ziyaret edin.
3. Tüm tarzları almak için **Dizin** eylemi yöntemini güncelleştirin.

    (Kod parçacığı- *modeller ve veri erişimi-Ex1 Store dizini*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. Tüm tarzları almak ve koleksiyonu bir listeye dönüştürmek için **Dizin** eylemi yöntemini güncelleştirin.

    (Kod parçacığı- *modeller ve veri erişimi-Ex1 Store GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5\. Görev-uygulamayı çalıştırma

Bu görevde, depolama dizini sayfasında artık sabit kodlanmış olanlar yerine veritabanında depolanan tarzların görüntüleneceğini kontrol edersiniz. **Storecontroller** daha önce olduğu gibi aynı varlıkları döndürdüğü için, bu kez verilerin veritabanından geldiği halde görünüm şablonunu değiştirme gereksinimi yoktur.

1. Çözümü yeniden derleyin ve uygulamayı çalıştırmak için **F5** 'e basın.
2. Proje giriş sayfasında başlar. **Tarzın** menüsünün artık sabit kodlanmış bir liste olmadığını ve verilerin doğrudan veritabanından alındığını doğrulayın.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *Veritabanından Tarzya göz atma*
3. Şimdi herhangi bir tarzya gidin ve albümlerin veritabanından doldurulduğunu doğrulayın.

    ![Veritabanından Albümler 'e göz atma](aspnet-mvc-4-models-and-data-access/_static/image17.png "Veritabanından Albümler 'e göz atma")

    *Veritabanından Albümler 'e göz atma*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>Alıştırma 2: Code First kullanarak veritabanı oluşturma

Bu alıştırmada, MusicStore uygulamasının tablolarıyla bir veritabanı oluşturmak ve verilere erişmek için Code First yaklaşımını nasıl kullanacağınızı öğreneceksiniz.

Model oluşturulduktan sonra, tek kodlanmış değerler kullanmak yerine, veritabanından alınan verileri görünüm şablonuna sağlamak için StoreController 'ı değiştirirsiniz.

> [!NOTE]
> 1\. Alıştırmayı tamamladıysanız ve Database First yaklaşımıyla zaten çalıştıysanız, artık farklı bir işlemle aynı sonuçların nasıl alınacağını öğreneceksiniz. Alıştırma 1 ile ortak olan görevler, okumanız daha kolay hale getirmek için işaretlendi. Alıştırma 1 ' i tamamlamadıysanız, ancak Code First yaklaşımı öğrenmek istiyorsanız, bu alıştırmaya başlayabilir ve konunun tam kapsamına ulaşabilirsiniz.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>Görev 1-örnek verileri doldurma

Bu görevde, Ilk önce kod kullanılarak oluşturulduğu zaman veritabanını örnek verilerle dolduracaksınız.

1. **Kaynak/EX2-Creatingadatabasecodefırst/BEGIN/** Folder konumunda bulunan **BEGIN** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Modeller** klasörüne **sampleData.cs** dosyasını ekleyin. Bunu yapmak için **modeller** klasörüne sağ tıklayın, **Ekle** ' nin üzerine gelin ve **var olan öğe**' ye tıklayın. **\Source\varlıklar** ' a göz atın ve **sampleData.cs** dosyasını seçin.

    ![Örnek veri doldurma kodu](aspnet-mvc-4-models-and-data-access/_static/image18.png "Örnek veri doldurma kodu")

    *Örnek veri doldurma kodu*
3. **Global.asax.cs** dosyasını açın ve aşağıdaki *using* deyimlerini ekleyin.

    (Kod parçacığı- *modeller ve veri erişimi-EX2 Global asax kullanımlar*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. **Uygulama\_Start ()** yönteminde, veritabanı başlatıcısı 'nı ayarlamak için aşağıdaki satırı ekleyin.

    (Kod parçacığı- *modeller ve veri erişimi-EX2 Global asax Setbaşlatıcısı*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>Görev 2-veritabanı bağlantısını yapılandırma

Projemizde zaten bir veritabanı eklediğine göre, **Web. config** dosyasına bağlantı dizesini yazmanız gerekir.

1. **Web. config dosyasına**bir bağlantı dizesi ekleyin. Bunu yapmak için, proje kökünde **Web. config** dosyasını açın ve DefaultConnection adlı bağlantı dizesini **&lt;connectionStrings&gt;** bölümünde yer alan bu satırla değiştirin:

    ![Web. config dosyası konumu](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web. config dosyası konumu")

    *Web. config dosyası konumu*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>Görev 3-modelle çalışma

Veritabanı bağlantısını zaten yapılandırdığınıza göre, modeli veritabanı tabloları ile bağlayacaksınız. Bu görevde, Code First veritabanıyla bağlantılı olacak bir sınıf oluşturacaksınız. Değiştirilmesi gereken var olan bir POCO model sınıfı olduğunu unutmayın.

> [!NOTE]
> Alıştırma 1 ' i tamamladıysanız, bu adımın bir sihirbaz tarafından gerçekleştirildiğini aklınızda görürsünüz. Code First yaparak, veri varlıklarına bağlanacak sınıfları el ile oluşturursunuz.

1. **Model** proje klasöründen poco model sınıfı **tarzını** açın ve bir ID ekleyin. **Genreıd**adlı bir int özelliği kullanın.

    (Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First tarz*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > Code First kuralları ile çalışmak için, sınıf tarzında otomatik olarak algılanacak bir birincil anahtar özelliği olmalıdır.
    > 
    > Bu [MSDN makalesinde](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)Code First kuralları hakkında daha fazla bilgi edinebilirsiniz.
2. Şimdi, **model** proje klasöründen poco model sınıfı **albümünü** açın ve yabancı anahtarları ekleyin, **genreıd** ve **ArtistId**adlarıyla Özellikler oluşturun. Bu sınıf zaten birincil anahtar için **Genreıd** 'ye sahip.

    (Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First albüm*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. POCO modeli sınıf **sanatçısını** açın ve **ArtistId** özelliğini ekleyin.

    (Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First sanatçı*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. **Modeller** proje klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Sınıf**. Dosyayı **MusicStoreEntities.cs**olarak adlandırın. Ardından Ekle ' ye tıklayın **.**

    ![Sınıf ekleme](aspnet-mvc-4-models-and-data-access/_static/image20.png "Sınıf ekleme")

    *Yeni öğe ekleme*

    ![Class2 ekleme](aspnet-mvc-4-models-and-data-access/_static/image21.png "Class2 ekleme")

    *Sınıf ekleme*
5. Az önce oluşturduğunuz, **MusicStoreEntities.cs**ve **System. Data. Entity** ve **System. Data. Entity. Infrastructure**ad alanlarını içeren sınıfını açın.

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. Sınıf bildirimini **DbContext** sınıfını genişletmek için değiştirin: bir public **dbset** bildirin ve **onmodeloluþturma** metodunu geçersiz kılın. Bu adımdan sonra modelinize Entity Framework ile bağlantı oluşturacak bir etki alanı sınıfı alacaksınız. Bunu yapmak için, sınıf kodunu aşağıdaki kodla değiştirin:

    (Kod parçacığı- *modeller ve veri erişimi-Ex2 Code First MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> Entity Framework **DbContext** ve **DBSET** Ile poco sınıf tarzında sorgulama yapabileceksiniz. **Onmodeloluþturma** yöntemini genişleterek, tarzın bir veritabanı tablosuna nasıl eşleneceğini **kodda** belirtirsiniz. Bu MSDN makalesinde DBContext ve DBSet hakkında daha fazla bilgi edinebilirsiniz: [bağlantı](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>Görev 4-veritabanını sorgulama

Bu görevde, sabit kodlanmış veriler kullanmak yerine, bunu veritabanından alacak şekilde StoreController sınıfını güncelleşolursunuz.

> [!NOTE]
> Bu görev, alıştırma 1 ile yaygındır.
> 
> Alıştırma 1 ' i tamamladıysanız, bu adımların her iki yaklaşıma (önce veritabanı veya önce kod) aynı olduğunu aklınızda olursunuz. Bunlar, verilerin modelle bağlantılı olduğu şekilde farklılık gösteren, ancak veri varlıklarına erişim, denetleyiciden henüz saydamdır.

1. **Controllers\storecontroller.cs** dosyasını açın ve aşağıdaki alanı sınıfına, **StoreDB**adlı bir **musicstoreentities** sınıfının örneğini tutacak şekilde ekleyin:

    (Kod parçacığı- *modeller ve veri erişimi-Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **Musicstoreentities** sınıfı, veritabanındaki her tablo için bir koleksiyon özelliği sunar. Tüm **albümlerle**bir tarzın alınması için **gözatmayı** eylem yöntemini güncelleştirin.

    (Kod parçacığı- *modeller ve veri erişimi-EX2 Store tarama*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > Bu koleksiyonlara karşı kesin türü belirtilmiş sorgu ifadeleri yazmak için **LINQ** (dil ile tümleşik sorgu) adlı bir .NET özelliği kullanıyorsunuz. Bu, veritabanına karşı kod yürütecek ve programlayabileceğiniz nesneleri döndürmeyecektir.
    > 
    > LINQ hakkında daha fazla bilgi için lütfen [MSDN sitesini](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)ziyaret edin.
3. Tüm tarzları almak için **Dizin** eylemi yöntemini güncelleştirin.

    (Kod parçacığı- *modeller ve veri erişimi-EX2 Store dizini*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. Tüm tarzları almak ve koleksiyonu bir listeye dönüştürmek için **Dizin** eylemi yöntemini güncelleştirin.

    (Kod parçacığı- *modeller ve veri erişimi-EX2 Store GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>5\. Görev-uygulamayı çalıştırma

Bu görevde, depolama dizini sayfasında artık sabit kodlanmış olanlar yerine veritabanında depolanan tarzların görüntüleneceğini kontrol edersiniz. **Storecontroller** daha önce olduğu gibi aynı **Storeındexviewmodel** döndürdüğü için görünüm şablonunu değiştirmeniz gerekmez, ancak bu kez veriler veritabanından gelir.

1. Çözümü yeniden derleyin ve uygulamayı çalıştırmak için **F5** 'e basın.
2. Proje giriş sayfasında başlar. **Tarzın** menüsünün artık sabit kodlanmış bir liste olmadığını ve verilerin doğrudan veritabanından alındığını doğrulayın.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *Veritabanından Tarzya göz atma*
3. Şimdi herhangi bir tarzya gidin ve albümlerin veritabanından doldurulduğunu doğrulayın.

    ![Veritabanından Albümler 'e göz atma](aspnet-mvc-4-models-and-data-access/_static/image23.png "Veritabanından Albümler 'e göz atma")

    *Veritabanından Albümler 'e göz atma*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>Alıştırma 3: veritabanını parametrelerle sorgulama

Bu alıştırmada, parametreleri kullanarak veritabanını sorgulamayı ve sorgu sonucu şekillendirmenin nasıl kullanıldığını, verileri daha verimli bir şekilde alan bir özellik olan veritabanı erişimlerini azaltan bir özelliği öğreneceksiniz.

> [!NOTE]
> Sorgu sonucu şekillendirme hakkında daha fazla bilgi için aşağıdaki [MSDN makalesini](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)ziyaret edin.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>Görev 1-veritabanından albümleri almak için StoreController değiştiriliyor

Bu görevde, belirli bir tarz albümleri almak için **Storecontroller** sınıfını veritabanına erişecek şekilde değiştirirsiniz.

1. Database-First yaklaşımını kullanmak istiyorsanız, Code-First yaklaşımını veya **Source\ex3-queryingthedatabasewithparametersdbfirst\begin** klasörünü kullanmak istiyorsanız **Source\ex3-queryingthedatabasewithparameterscodefırst\begin** klasöründe bulunan **BEGIN** Solution ' i açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Tarayıcı** eylemi yöntemini değiştirmek Için **storecontroller** sınıfını açın. Bunu yapmak için, **Çözüm Gezgini**, **denetleyiciler** klasörünü genişletin ve **StoreController.cs**öğesine çift tıklayın.
3. Belirli bir tarz için Albümler almak üzere, **tarama** eylemi yöntemini değiştirin. Bunu yapmak için aşağıdaki kodu değiştirin:

    (Kod parçacığı- *modeller ve veri erişimi-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> Varlığın bir koleksiyonunu doldurmak için, **dahil etme** yöntemini kullanarak albümleri de almak istediğinizi belirtmeniz gerekir. Kullanabilirsiniz. LINQ içinde **Single ()** uzantısı bu durumda, bir albüm için yalnızca bir tarz beklenmektedir. **Single ()** yöntemi bir lambda ifadesini parametre olarak alır. Bu durumda, adı tanımlı değerle eşleşen tek bir tarz nesneyi belirtir.
> 
> Ayrıca, bir tarz nesne alındığında, yüklemek istediğiniz diğer ilgili varlıkların yanı sıra, yüklenmesini istediğinizi belirtmenize olanak tanıyan bir özellikten faydalanabilirsiniz. Bu özelliğe **sorgu sonucu şekillendirme**adı verilir ve bilgileri almak için veritabanına erişmek için gereken sürelerin sayısını azaltmanızı sağlar. Bu senaryoda, aldığınız tarz için albümleri önceden getirmek isteyeceksiniz.
> 
> Sorgu, ilgili Albümler de istediğinizi belirtmek için **tarzlar. Include (&quot;albümler&quot;)** içerir. Tek bir veritabanı isteğinde hem tarz hem de albüm verilerini alacak olduğundan, bu daha verimli bir uygulamayla sonuçlanır.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Görev 2-uygulamayı çalıştırma

Bu görevde, uygulamayı çalıştıracaksınız ve veritabanından belirli bir tarz Albümler elde edersiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. Sonuçların veritabanından alındığını doğrulamak için, URL 'YI **/Store/zat? tarzı = pop** olarak değiştirin.

    ![Tarza göre gözatma](aspnet-mvc-4-models-and-data-access/_static/image24.png "Tarza göre gözatma")

    */Store/gözatmaya? tarz = pop 'a göz atma*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>Görev 3-bir kimliğe göre Albümler 'e erişme

Bu görevde, bir önceki prosedürü kendi kimliğine göre albümleri alacak şekilde tekrarlamalısınız.

1. Gerekirse, Visual Studio 'ya dönmek için tarayıcıyı kapatın. **Ayrıntılar** eylem yöntemini değiştirmek Için **storecontroller** sınıfını açın. Bunu yapmak için, **Çözüm Gezgini**, **denetleyiciler** klasörünü genişletin ve **StoreController.cs**öğesine çift tıklayın.
2. **Kimlik**bilgilerini temel alarak Albümler ayrıntılarını almak için **Ayrıntılar** eylem yöntemini değiştirin. Bunu yapmak için aşağıdaki kodu değiştirin:

    (Kod parçacığı- *modeller ve veri erişimi-Ex3 StoreController ayrıntıları yöntemi*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Görev 4-uygulamayı çalıştırma

Bu görevde, uygulamayı bir Web tarayıcısında çalıştıracaksınız ve kendi kimliğine göre albüm ayrıntılarını edinirsiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.
2. Proje giriş sayfasında başlar. URL 'YI **/Store/details/51** olarak değiştirin veya sonuçların veritabanından alındığını doğrulamak için bir albüm seçin.

    ![Gözatma ayrıntıları](aspnet-mvc-4-models-and-data-access/_static/image25.png "Gözatma ayrıntıları")

    */Store/Details/51 öğesine göz atma*

> [!NOTE]
> Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak, **Database First** yaklaşımını ve **Code First** YAKLAŞıMıNı kullanarak, ASP.NET MVC modellerinin ve veri erişiminin temellerini öğrendiniz:

- Verileri kullanmak için çözüme bir veritabanı ekleme
- Denetimleri, sabit kodlanmış bir yerine veritabanından alınan verilerle görüntüleme şablonları sağlamak üzere güncelleştirme
- Parametreleri kullanarak veritabanını sorgulama
- Veritabanı erişimleri sayısını azaltan, verileri daha verimli bir şekilde alan bir özellik olan sorgu sonucu şekillendirme 'yı kullanma
- Veritabanını modeliyle bağlamak için Microsoft Entity Framework 'de hem Database First hem de Code First yaklaşımları kullanma

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    *Web için VS Express kutucuğu*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama

Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma

1. [Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.

    > [!NOTE]
    > Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz. [Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.

    ![Windows Azure portal oturum açın](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure portal oturum açın")

    *Windows Azure 'da oturum açma Yönetim Portalı*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](aspnet-mvc-4-models-and-data-access/_static/image32.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](aspnet-mvc-4-models-and-data-access/_static/image33.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](aspnet-mvc-4-models-and-data-access/_static/image34.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](aspnet-mvc-4-models-and-data-access/_static/image36.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.

    ![Web sitesi yayımlama profili indiriliyor](aspnet-mvc-4-models-and-data-access/_static/image37.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](aspnet-mvc-4-models-and-data-access/_static/image38.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](aspnet-mvc-4-models-and-data-access/_static/image40.png) düğmesine tıklayın.

    ![Istemci IP adresi ekleniyor](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *Değişiklikleri Onayla*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](aspnet-mvc-4-models-and-data-access/_static/image43.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](aspnet-mvc-4-models-and-data-access/_static/image44.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](aspnet-mvc-4-models-and-data-access/_static/image45.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın.

     ![Hedef bağlantı dizesi yapılandırılıyor](aspnet-mvc-4-models-and-data-access/_static/image47.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Daha sonra, **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](aspnet-mvc-4-models-and-data-access/_static/image48.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Ardından **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](aspnet-mvc-4-models-and-data-access/_static/image50.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Ek C: kod parçacıkları kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](aspnet-mvc-4-models-and-data-access/_static/image51.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](aspnet-mvc-4-models-and-data-access/_static/image52.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](aspnet-mvc-4-models-and-data-access/_static/image53.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](aspnet-mvc-4-models-and-data-access/_static/image54.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, Visual Basic ve XML)*** 1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.

1. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
2. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](aspnet-mvc-4-models-and-data-access/_static/image55.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](aspnet-mvc-4-models-and-data-access/_static/image56.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*
