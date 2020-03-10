---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: 'Yineleme #1 – uygulamayı oluşturma (C#) | Microsoft Docs'
author: microsoft
description: 'İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve D...'
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: d3a940308f21a4f87bf80249bd465e8812794f68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582133"
---
# <a name="iteration-1--create-the-application-c"></a>Yineleme #1 – uygulamayı oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve silme (CRUD).

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Kişi yönetimi ASP.NET MVC uygulaması oluşturma (VB)

Bu öğretici dizisinde, başlangıçtan sonuna kadar bir Iletişim yönetimi uygulaması oluşturacaksınız. Ilgili kişi Yöneticisi uygulaması, kişi listesi için kişi bilgilerini, telefon numaralarını ve e-posta adreslerini depolamanıza olanak sağlar.

Uygulamayı birden çok yineleme üzerinde oluşturacağız. Her yinelemede, uygulamayı kademeli olarak geliştirdik. Bu birden çok yineleme yaklaşımının hedefi, her bir değişikliğin nedenini anlamanıza olanak sağlamaktır.

- Yineleme #1-uygulamayı oluşturun. İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve silme (CRUD).

- Yineleme #2-uygulamanın iyi görünmesini sağlayın. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.

- Yineleme #3-form doğrulaması ekleme. Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğruladık.

- Yineleme #4-uygulamayı gevşek olarak bağlanmış hale getirin. Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. Örneğin, uygulamamız depo deseninin ve bağımlılık ekleme düzeninin kullanılması için yeniden düzenliyoruz.

- Yineleme #5-birim testleri oluşturun. Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. Denetleyicilerimizin ve doğrulama mantığımız için veri modeli Sınıflarımızı ve derleme birimi testlerini modelliyoruz.

- Yineleme #6-test odaklı geliştirme kullanın. Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede kişi grupları ekleyeceğiz.

- Yineleme #7-Ajax işlevselliği ekleme. Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.

## <a name="this-iteration"></a>Bu yineleme

Bu ilk yinelemede, temel uygulamayı oluşturacağız. Amaç, mümkün olan en hızlı ve en kolay şekilde Iletişim Yöneticisi oluşturmak için kullanılır. Sonraki yinelemelerde, uygulamanın tasarımını geliştirdik.

Contact Manager uygulaması, temel bir veritabanı temelli uygulamadır. Uygulamayı kullanarak yeni kişiler oluşturabilir, var olan kişileri düzenleyebilir ve kişileri silebilirsiniz.

Bu yinelemede aşağıdaki adımları tamamlayacağız:

1. ASP.NET MVC uygulaması
2. Kişilerimi depolamak için bir veritabanı oluşturun
3. Microsoft Entity Framework veritabanı için bir model sınıfı oluşturun
4. Veritabanındaki tüm kişileri listemizi sağlayan bir denetleyici eylemi ve görünümü oluşturun
5. Veritabanında yeni bir kişi oluşturmamızı sağlayan denetleyici eylemleri ve bir görünüm oluşturun
6. Veritabanında var olan bir kişiyi düzenlemenizi sağlayan denetleyici eylemleri ve bir görünüm oluşturun
7. Veritabanında var olan bir kişiyi silmemizi sağlayan denetleyici eylemleri ve bir görünüm oluşturun

## <a name="software-prerequisites"></a>Yazılım önkoşulları

ASP.NET MVC uygulamalarında, bilgisayarınızda Visual Studio 2008 veya Visual Web Developer 2008 yüklü olmalıdır (Visual Web Developer, Visual Studio 'nun tüm gelişmiş özelliklerini içermeyen, Visual Studio 'nun ücretsiz bir sürümüdür). Visual Studio 2008 ya da Visual Web Developer 'ın deneme sürümünü aşağıdaki adresten indirebilirsiniz:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Visual Web Developer ile ASP.NET MVC uygulamaları için, Visual Web Developer Service Pack 1 ' ın yüklü olması gerekir. Service Pack 1 olmadan, Web uygulaması projeleri oluşturamazsınız.

ASP.NET MVC çerçevesi. ASP.NET MVC çerçevesini şu adresten indirebilirsiniz:

[https://www.asp.net/mvc](../../../index.md)

Bu öğreticide, bir veritabanına erişmek için Microsoft Entity Framework kullanırız. Entity Framework, .NET Framework 3,5 hizmet paketi 1 ' de bulunur. Bu hizmet paketini aşağıdaki konumdan indirebilirsiniz:

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

Bu indirmelerin her birini tek tek yerine getirmek yerine Web Platformu Yükleyicisinden (Web PI) yararlanabilirsiniz. Web PI aşağıdaki adresten indirebilirsiniz:

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC projesi

ASP.NET MVC web uygulaması projesi. Visual Studio 'Yu başlatın ve menü seçeneği **dosyasını, yeni proje ' yi**seçin. **Yeni proje** iletişim kutusu görüntülenir (bkz. Şekil 1). **Web** projesi türünü ve **ASP.NET MVC web uygulaması** şablonunu seçin. Yeni projenize *ContactManager* adını yazıp Tamam düğmesine tıklayın.

**Yeni proje** iletişim kutusunun sağ üst köşesindeki aşağı açılan listeden .NET Framework 3,5 ' ın seçili olduğundan emin olun. Aksi halde, ASP.NET MVC web uygulaması şablonu görünmez.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**Şekil 01**: yeni proje iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image2.png))

ASP.NET MVC uygulaması, **birim test projesi oluştur** iletişim kutusu görüntülenir. Bu iletişim kutusunu, ASP.NET MVC uygulamanızı oluştururken çözümünüze bir birim testi projesi oluşturmak ve eklemek istediğinizi belirtmek için kullanabilirsiniz. Bu yinelemede birim testleri oluşturmayacağız olsa da, daha sonraki bir yinelemede birim testleri eklemeyi planlıyoruz **, Evet seçeneğini belirleyip bir birim testi projesi oluşturmanız** gerekir. Yeni bir ASP.NET MVC projesi oluşturduğunuzda bir test projesi eklemek, ASP.NET MVC projesi oluşturulduktan sonra test projesi eklemekten çok daha kolaydır.

> [!NOTE] 
> 
> Visual Web Developer test projelerini desteklemediğinden, Visual Web Developer 'ı kullanırken birim testi projesi oluştur iletişim kutusunu edinmeyin.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**Şekil 02**: birim testi projesi oluştur iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image4.png))

ASP.NET MVC uygulaması, Visual Studio Çözüm Gezgini penceresinde görünür (bkz. Şekil 3). Çözüm Gezgini pencereyi görmüyorsanız, bu pencereyi açmak için menü seçenek **görünümü ' ne Çözüm Gezgini**. Çözümün iki proje içerdiğine dikkat edin: ASP.NET MVC projesi ve test projesi. ASP.NET MVC projesi ContactManager olarak adlandırılır ve test projesi ContactManager. Tests olarak adlandırılır.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**Şekil 03**: Çözüm Gezgini penceresi ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>Proje örnek dosyalarını silme

ASP.NET MVC proje şablonu, denetleyiciler ve görünümler için örnek dosyaları içerir. Yeni bir ASP.NET MVC uygulaması oluşturmadan önce bu dosyaları silmelisiniz. Çözüm Gezgini penceresindeki dosyaları ve klasörleri, bir dosya veya klasöre sağ tıklayıp **Sil**menü seçeneğini belirleyerek silebilirsiniz.

Aşağıdaki dosyaları ASP.NET MVC projesinden silmeniz gerekir:

- \Controllers\HomeController.cs

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

Ve, aşağıdaki dosyayı test projesinden silmeniz gerekir:

\Controllers\HomeControllerTest.cs

## <a name="creating-the-database"></a>Veritabanı oluşturma

Contact Manager uygulaması, veritabanı odaklı bir Web uygulamasıdır. İletişim bilgilerini depolamak için bir veritabanı kullanıyoruz.

Microsoft SQL Server, Oracle, MySQL ve IBM DB2 veritabanları dahil olmak üzere herhangi bir modern veritabanıyla ASP.NET MVC çerçevesi. Bu öğreticide, bir Microsoft SQL Server veritabanı kullanıyoruz. Visual Studio 'Yu yüklediğinizde, Microsoft SQL Server veritabanının ücretsiz bir sürümü olan Microsoft SQL Server Express yükleme seçeneği sunulur.

Çözüm Gezgini penceresinde uygulama\_veri klasörüne sağ tıklayıp yeni bir veritabanı oluşturun ve menü seçeneğini **Ekle, yeni öğe ' yi**seçin. **Yeni öğe Ekle** Iletişim kutusunda **veri** kategorisini ve **SQL Server veritabanı** şablonunu seçin (bkz. Şekil 4). Yeni veritabanını ContactManagerDB. mdf olarak adlandırın ve Tamam düğmesine tıklayın.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**Şekil 04**: yeni bir Microsoft SQL Server Express veritabanı oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image8.png))

Yeni veritabanını oluşturduktan sonra veritabanı, Çözüm Gezgini penceresindeki App\_Data klasöründe görüntülenir. Sunucu Gezgini penceresini açmak ve veritabanına bağlanmak için ContactManager. mdf dosyasına çift tıklayın.

> [!NOTE] 
> 
> Sunucu Gezgini penceresine Microsoft Visual Web Developer durumunda Veritabanı Gezgini penceresi denir.

Veritabanı tabloları, görünümler, Tetikleyiciler ve saklı yordamlar gibi yeni veritabanı nesneleri oluşturmak için Sunucu Gezgini penceresini kullanabilirsiniz. Tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**menü seçeneğini belirleyin. Veritabanı Tablo Tasarımcısı görüntülenir (bkz. Şekil 5).

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**Şekil 05**: veritabanı Tablo Tasarımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image10.png))

Aşağıdaki sütunları içeren bir tablo oluşturuyoruz:

<a id="0.1_table01"></a>

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Kimlik | int | false |
| FirstName | nvarchar (50) | false |
| LastName | nvarchar (50) | false |
| Telefon | nvarchar (50) | false |
| E-posta | nvarchar (255) | false |

İlk sütun, ID sütunu özeldir. Kimlik sütununu kimlik sütunu olarak işaretlemeniz ve birincil anahtar sütunu belirlemeniz gerekir. Sütun özelliklerini genişleterek (Şekil 6 ' nın alt kısmına bakarak) ve kimlik belirtimi özelliğine giderek bir sütunun bir kimlik sütunu olduğunu belirtirsiniz. **(Identity)** özelliğini **Yes**değerine ayarlayın.

Sütunu seçip bir anahtarın simgesiyle düğmesine tıklayarak bir sütunu birincil anahtar sütunu olarak işaretleyebilirsiniz. Bir sütun birincil anahtar sütunu olarak işaretlendikten sonra, sütunun yanında bir anahtarın simgesi görünür (bkz. Şekil 6).

Tablo oluşturmayı tamamladıktan sonra, yeni tabloyu kaydetmek için Kaydet düğmesine (disketin simgesiyle birlikte düğme) tıklayın. Yeni tablonuza ad *kişileri*verin.

Kişiler veritabanı tablosunu oluşturduktan sonra, tabloya bazı kayıtlar eklemeniz gerekir. Sunucu Gezgini penceresinde kişiler tablosuna sağ tıklayın ve **tablo verilerini göster**menü seçeneğini belirleyin. Görüntülenen kılavuza bir veya daha fazla kişi girin.

## <a name="creating-the-data-model"></a>Veri modeli oluşturma

ASP.NET MVC uygulaması modeller, görünümler ve denetleyicilerden oluşur. Önceki bölümde oluşturduğumuz kişiler tablosunu temsil eden bir model sınıfı oluşturarak başlayacağız.

Bu öğreticide, veritabanından otomatik olarak bir model sınıfı oluşturmak için Microsoft Entity Framework kullanırız.

> [!NOTE] 
> 
> ASP.NET MVC Framework, Microsoft Entity Framework herhangi bir şekilde bağlı değildir. ASP.NET MVC 'yi Nhazırda beklet, LINQ to SQL veya ADO.NET dahil alternatif veritabanı erişim teknolojileriyle kullanabilirsiniz.

Veri modeli sınıflarını oluşturmak için aşağıdaki adımları izleyin:

1. Çözüm Gezgini penceresinde modeller klasörüne sağ tıklayın ve **Ekle, yeni öğe**' yi seçin. **Yeni öğe Ekle** iletişim kutusu görünür (bkz. Şekil 6).
2. **Veri** kategorisini ve **ADO.net varlık veri modeli** şablonunu seçin. Veri modelinizi *Contactmanagermodel. edmx* olarak adlandırın ve **Ekle** düğmesine tıklayın. Varlık Veri Modeli Sihirbazı görüntülenir (bkz. Şekil 7).
3. **Model Içeriğini seçin** adımında, **veritabanından oluştur** ' u seçin (bkz. Şekil 7).
4. **Veri bağlantınızı seçin** adımında, ContactManagerDB. mdf veritabanını seçin ve varlık bağlantısı ayarları Için *Contactmanagerdbentities* adını girin (bkz. Şekil 8).
5. **Veritabanı nesnelerinizi seçin** adımında, tablolar etiketli onay kutusunu seçin (bkz. Şekil 9). Veri modeli, veritabanınızda bulunan tüm tabloları (yalnızca bir tane, kişiler tablosu) içerir. Ad alanı *modellerini*girin. Sihirbazı gerçekleştirmek için son düğmesine tıklayın.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**Şekil 06**: yeni öğe Ekle iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image12.png))

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**Şekil 07**: model içeriğini seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image14.png))

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**Şekil 08**: veri bağlantınızı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image16.png))

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**Şekil 09**: veritabanı nesnelerinizi seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image18.png))

Varlık Veri Modeli Sihirbazı 'nı tamamladıktan sonra, Varlık Veri Modeli Tasarımcısı görüntülenir. Tasarımcı, modellenen her tabloya karşılık gelen bir sınıfı görüntüler. Kişiler adlı bir sınıf görmeniz gerekir.

Varlık Veri Modeli Sihirbazı, veritabanı tablosu adlarını temel alan sınıf adları oluşturur. Neredeyse her zaman sihirbaz tarafından oluşturulan sınıfın adını değiştirmeniz gerekir. Tasarımcıda kişiler sınıfına sağ tıklayın ve **Yeniden Adlandır**seçeneğini belirleyin. Sınıf adını kişiler (plural) iken Iletişim (tekil) olarak değiştirin. Sınıf adını değiştirdikten sonra sınıf Şekil 10 gibi görünmelidir.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**Şekil 10**: kişi sınıfı ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image20.png))

Bu noktada veritabanı modelimizi oluşturduk. Veritabanımızda belirli bir kişi kaydını temsil etmek için Iletişim sınıfını kullanabiliriz.

## <a name="creating-the-home-controller"></a>Ana denetleyici oluşturma

Sonraki adım, ana denetleyicimizi oluşturmaktır. Ana denetleyici, bir ASP.NET MVC uygulamasında çağrılan varsayılan denetleyicisidir.

Çözüm Gezgini penceresinde denetleyiciler klasörüne sağ tıklayıp **, denetleyici Ekle, denetleyici** (bkz. Şekil 11) menü seçeneğini belirleyerek giriş denetleyicisi sınıfını oluşturun. **Oluşturma, güncelleştirme ve ayrıntı senaryoları için eylem ekleme yöntemleri**etiketli onay kutusuna dikkat edin. **Ekle** düğmesine tıklamadan önce bu onay kutusunun işaretli olduğundan emin olun.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**Şekil 11**: giriş denetleyicisini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image22.png))

Ana denetleyiciyi oluştururken, kod 1 ' de sınıfı alırsınız.

**Listeleme 1-Controllers\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>Kişileri listeleme

Kayıtları kişiler veritabanı tablosunda görüntülemek için bir dizin () eylemi ve bir dizin görünümü oluşturuyoruz.

Giriş denetleyicisi zaten bir dizin () eylemi içeriyor. Bu yöntemi, liste 2 gibi görünmesi için değiştirmemiz gerekiyor.

**Listeleme 2-Controllers\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

Liste 2 ' deki giriş denetleyicisi sınıfının \_varlıkları adlı bir özel alan içerdiğini unutmayın. \_varlıkları alanı, veri modelindeki varlıkları temsil eder. Veritabanıyla iletişim kurmak için \_varlıkları alanını kullanıyoruz.

Index () yöntemi, kişiler veritabanı tablosundan tüm kişileri temsil eden bir görünüm döndürür. İfade \_varlıklar. ContactSet. ToList (), kişiler listesini genel liste olarak döndürür.

Artık Dizin denetleyicisini oluşturduğumuz için, bir sonraki adımda dizin görünümü oluşturulması gerekir. Dizin görünümünü oluşturmadan önce **Build, Build Solution**seçeneklerini belirleyerek uygulamanızı derleyin. **Görünüm Ekle** iletişim kutusunda görüntülenecek model sınıflarının listesi için bir görünüm eklemeden önce projenizi her zaman derlemeniz gerekir.

Dizin () yöntemine sağ tıklayıp **Görünüm Ekle** menü seçeneğini belirleyerek Dizin görünümünü oluşturursunuz (bkz. Şekil 12). Bu menü seçeneği belirlendiğinde **Görünüm Ekle** iletişim kutusu açılır (bkz. Şekil 13).

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**Şekil 12**: Dizin görünümü ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image24.png))

**Görünüm Ekle** iletişim kutusunda, **türü kesin belirlenmiş görünüm oluştur**onay kutusunu işaretleyin. View Data sınıfını ContactManager. modeller. Contact ve içeriği görüntüle listesini seçin. Bu seçeneklerin belirlenmesi, kişi kayıtlarının listesini görüntüleyen bir görünüm oluşturur.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**Şekil 13**: Görünüm Ekle iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image26.png))

**Ekle** düğmesine tıkladığınızda, liste 3 ' teki dizin görünümü oluşturulur. Dosyanın üst kısmında görüntülenen &lt;% @ Page%&gt; yönergesine dikkat edin. Dizin görünümü ViewPage&lt;IEnumerable&lt;ContactManager. modeller. Contact&gt;&gt; sınıfına devralır. Diğer bir deyişle, görünümdeki model sınıfı, Iletişim varlıklarının bir listesini temsil eder.

Dizin görünümü gövdesi, model sınıfı tarafından temsil edilen kişilerin her biri boyunca yinelenen bir foreach döngüsü içerir. Kişi sınıfının her özelliğinin değeri bir HTML tablosu içinde görüntülenir.

**Listeleme 3-Views\home\ındex.aspx (değiştirilmemiş)**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

Dizin görünümünde bir değişiklik yapmanız gerekiyor. Ayrıntı görünümü oluşturmadığımızda, Ayrıntılar bağlantısını kaldırabiliriz. Aşağıdaki kodu Dizin görünümünden bulun ve kaldırın:

{id = öğe. Kimlik})%&gt;

Dizin görünümünü değiştirdikten sonra, Contact Manager uygulamasını çalıştırabilirsiniz. Hata Ayıkla, hata ayıklamayı Başlat menü seçeneğini belirleyin veya F5 tuşuna basın. Uygulamayı ilk kez çalıştırdığınızda Şekil 14 ' te iletişim kutusu alırsınız. **Hata ayıklamayı etkinleştirmek Için Web. config dosyasını Değiştir** seçeneğini belirleyin ve Tamam düğmesine tıklayın.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**Şekil 14**: hata ayıklamayı etkinleştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image28.png))

Dizin görünümü varsayılan olarak döndürülür. Bu görünüm, kişiler veritabanı tablosundaki tüm verileri listeler (bkz. Şekil 15).

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**Şekil 15**: Dizin görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image30.png))

Dizin görünümünün, görünümün alt kısmında yeni oluştur etiketli bir bağlantı içerdiğine dikkat edin. Sonraki bölümde, yeni kişiler oluşturmayı öğreneceksiniz.

## <a name="creating-new-contacts"></a>Yeni kişiler oluşturma

Kullanıcıların yeni kişiler oluşturmalarına olanak tanımak için, ana denetleyiciye iki Create () eylemi eklememiz gerekiyor. Yeni bir kişi oluşturmak için bir HTML formu döndüren bir Create () eylemi oluşturmamız gerekir. Yeni kişinin gerçek veritabanı eklemesini gerçekleştiren ikinci bir Create () eylemi oluşturuyoruz.

Ana denetleyiciye eklemesi gereken yeni Create () yöntemleri, liste 4 ' te yer alır.

**Listeleme 4-Controllers\HomeController.cs (oluşturma yöntemleriyle)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

İlk Create () yöntemi bir HTTP GET ile çağrılabilir, ancak ikinci Create () yöntemi yalnızca bir HTTP POST tarafından çağrılabilir. Diğer bir deyişle, ikinci Create () yöntemi yalnızca bir HTML formu postalamak için çağrılabilir. İlk Create () yöntemi yalnızca yeni bir kişi oluşturmak için HTML formunu içeren bir görünüm döndürür. İkinci Create () yöntemi çok daha ilginç: veritabanına yeni kişiyi ekler.

İkinci Create () yönteminin, kişi sınıfının bir örneğini kabul edecek şekilde değiştirildiğini unutmayın. HTML formundan gönderilen form değerleri, ASP.NET MVC çerçevesi tarafından otomatik olarak bu Iletişim sınıfına bağlanır. HTML oluştur formundaki her form alanı, Iletişim parametresinin bir özelliğine atanır.

Iletişim parametresinin bir [bind] özniteliğiyle donatılmış olduğuna dikkat edin. [Bind] özniteliği, kişi kimliği özelliğinin bağlamadan hariç tutulması için kullanılır. ID özelliği bir kimlik özelliğini temsil ettiğinden, ID özelliğini ayarlamak istemiyorum.

Create () yönteminin gövdesinde, Entity Framework yeni kişiyi veritabanına eklemek için kullanılır. Yeni kişi var olan kişiler kümesine eklenir ve bu değişiklikleri arka plandaki veritabanına geri göndermek için SaveChanges () yöntemi çağırılır.

İki Create () yönteminden birini sağ tıklayarak ve **Görünüm Ekle** menü seçeneğini belirleyerek yeni kişiler oluşturmak IÇIN bir HTML formu oluşturabilirsiniz (bkz. Şekil 16).

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**Şekil 16**: oluştur görünümü ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image32.png))

**Görünüm Ekle** iletişim kutusunda, içerik görüntüle Için **ContactManager. modeller. Contact** sınıfını ve **Oluştur** seçeneğini belirleyin (bkz. Şekil 17). **Ekle** düğmesine tıkladığınızda otomatik olarak bir oluştur görünümü oluşturulur.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**Şekil 17**: sayfa açılımı görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image34.png))

Oluştur görünümü, kişi sınıfının her bir özelliği için form alanları içerir. Oluşturma görünümü kodu, 5. listeye dahil edilir.

**Listeleme 5-Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

Create () yöntemlerini değiştirdikten ve oluşturma görünümünü ekledikten sonra, Ilgili kişi Yöneticisi uygulamasını çalıştırabilir ve yeni kişiler oluşturabilirsiniz. Oluştur görünümüne gitmek için dizin görünümünde görüntülenen **Yeni oluştur** bağlantısına tıklayın. Görünümü Şekil 18 ' de görmeniz gerekir.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**Şekil 18**: oluştur görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image36.png))

## <a name="editing-contacts"></a>Kişileri Düzenle

Bir kişi kaydını düzenlemenin işlevlerini eklemek, yeni kişi kayıtları oluşturmaya yönelik işlevselliği eklemeye çok benzer. İlk olarak, giriş denetleyicisi sınıfına iki yeni düzenleme yöntemi eklememiz gerekiyor. Bu yeni düzenleme () yöntemleri, liste 6 ' da bulunur.

**6-Controllers\HomeController.cs (düzenleme yöntemleriyle) listeleniyor**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

İlk Edit () yöntemi bir HTTP GET işlemi tarafından çağırılır. Düzenlenmekte olan kişi kaydının kimliğini temsil eden bu yönteme bir ID parametresi geçirilir. Entity Framework, kimlik ile eşleşen bir kişiyi almak için kullanılır. Bir kaydın düzenlenmesiyle ilgili HTML formu içeren bir görünüm döndürülür.

İkinci düzenleme () yöntemi, veritabanının gerçek güncelleştirmesini gerçekleştirir. Bu yöntem, bir parametre olarak kişi sınıfının bir örneğini kabul eder. ASP.NET MVC Framework form alanlarını düzenleme formundan bu sınıfa otomatik olarak bağlar. Bir kişiyi (kimlik özelliğinin değerine ihtiyacımız olması gerekir) düzenlediğinizde [bind] özniteliğini dahil ettiğine dikkat edin.

Entity Framework, değiştirilen kişiyi veritabanına kaydetmek için kullanılır. Özgün kişi önce veritabanından alınmalıdır. Sonra, kişide yapılan değişiklikleri kaydetmek için Entity Framework ApplyPropertyChanges () yöntemi çağırılır. Son olarak, Entity Framework SaveChanges () yöntemi, temel veritabanında yapılan değişiklikleri kalıcı hale getirmek için çağrılır.

Düzenle () yöntemine sağ tıklayıp Görünüm Ekle menü seçeneğini belirleyerek düzenleme formunu içeren görünümü oluşturabilirsiniz. Görünüm Ekle iletişim kutusunda **ContactManager. modeller. Contact** sınıfını ve **düzenleme** görünümü içeriğini seçin (bkz. Şekil 19).

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**Şekil 19**: düzenleme görünümü ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image38.png))

Ekle düğmesine tıkladığınızda, yeni bir düzenleme görünümü otomatik olarak oluşturulur. Oluşturulan HTML formu, kişi sınıfının özelliklerinin her birine karşılık gelen alanları içerir (bkz. Listeleme 7).

**Liste 7-Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>Kişiler siliniyor

Kişileri silmek isterseniz, ana denetleyici sınıfına iki Delete () eylemi eklemeniz gerekir. İlk Delete () eylemi bir silme onayı formunu görüntüler. İkinci Delete () eylemi, gerçek silme işlemini gerçekleştirir.

> [!NOTE] 
> 
> Daha sonra, yineleme #7 içinde, bir adım Ajax silmeyi desteklemesi için Ilgili kişi Yöneticisi ' ni değiştirirsiniz.

İki yeni Delete () yöntemi, listeleme 8 ' de yer alır.

**8-Controllers\HomeController.cs (silme yöntemleri) listesi**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

İlk Delete () yöntemi veritabanından bir kişi kaydını silmek için bir onay formu döndürür (bkz. Figure20). İkinci Delete () yöntemi, gerçek silme işlemini veritabanına göre gerçekleştirir. Özgün kişi veritabanından alındıktan sonra, veritabanı silme işlemini gerçekleştirmek için Entity Framework DeleteObject () ve SaveChanges () yöntemleri çağırılır.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**Şekil 20**: silme onayı görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image40.png))

Dizin görünümünü, kişi kayıtlarını silmeye yönelik bir bağlantı içerecek şekilde değiştirmemiz gerekiyor (bkz. Şekil 21). Aşağıdaki kodu düzenleme bağlantısını içeren tablo hücresine eklemeniz gerekir:

HTML. ActionLink ({ID = öğesi). Kimlik})%&gt;

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**Şekil 21**: düzenleme bağlantısıyla dizin görünümü ([tam boyutlu görüntüyü görüntülemek için tıklatın](iteration-1-create-the-application-cs/_static/image42.png))

Ardından, silme onayı görünümünü oluşturuyoruz. Giriş denetleyicisi sınıfında Delete () yöntemine sağ tıklayın ve Görünüm Ekle menü seçeneğini belirleyin. Görünüm Ekle iletişim kutusu görünür (bkz. Şekil 22).

Liste, oluşturma ve düzenleme görünümlerinin aksine, Görünüm Ekle iletişim kutusu silme görünümü oluşturma seçeneği içermez. Bunun yerine **ContactManager. modeller. Contact** veri sınıfını ve **boş** görünüm içeriğini seçin. Boş görünüm içeriği seçeneğinin belirlenmesi, kendimize görünümü oluşturmamızı gerektirir.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**Şekil 22**: silme onayı görünümü ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image44.png))

Silme görünümünün içeriği, liste 9 ' da bulunur. Bu görünüm belirli bir kişinin silinip silinmeyeceğini doğrulayan bir form içerir (bkz. Şekil 21).

**9-Views\Home\Delete.aspx listeleme**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>Varsayılan denetleyicinin adını değiştirme

Bu, kişilerle çalışma için denetleyici sınıfımız adının HomeController sınıfı olarak adlandırıldığını gösterebilir. Denetleyici ContactController olarak adlandırılmamalıdır mi?

Bu sorun, düzeltilmesi için yeterince kolay. İlk olarak, ana denetleyicinin adını yeniden düzenlemeniz gerekir. Visual Studio Code düzenleyicisinde HomeController sınıfını açın, sınıfın adına sağ tıklayın ve **yeniden Düzenle ' yi seçerek yeniden adlandır**' ı seçin. Bu menü seçeneğinin belirlenmesi yeniden adlandır iletişim kutusunu açar.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**Şekil 23**: bir denetleyici adını yeniden düzenleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image46.png))

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**Şekil 24**: Yeniden Adlandır iletişim kutusunu kullanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image48.png))

Denetleyici sınıfınızı yeniden adlandırırsanız, Visual Studio, görünümler klasöründeki klasörün adını da güncelleştirir. Visual Studio \Views\Home klasörünü \Views\Contact klasörüne yeniden adlandıracak.

Bu değişikliği yaptıktan sonra, uygulamanız artık bir giriş denetleyicisine sahip olmayacaktır. Uygulamanızı çalıştırdığınızda, Şekil 25 ' te hata sayfasını alırsınız.

[Yeni proje iletişim kutusunu ![](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**Şekil 25**: Varsayılan denetleyici yok ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-1-create-the-application-cs/_static/image50.png))

Global. asax dosyasındaki varsayılan yolu, ana denetleyici yerine Ilgili kişi denetleyicisini kullanacak şekilde güncelleştirmemiz gerekir. Global. asax dosyasını açın ve varsayılan yol tarafından kullanılan varsayılan denetleyiciyi değiştirin (bkz. listeleme 10).

**Listeleme 10-Global.asax.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

Bu değişiklikleri yaptıktan sonra, Ilgili kişi Yöneticisi doğru şekilde çalışır. Şimdi, varsayılan denetleyici olarak Iletişim denetleyicisi sınıfını kullanacaktır.

## <a name="summary"></a>Özet

Bu ilk yinelemede, mümkün olan en hızlı şekilde temel bir Contact Manager uygulaması oluşturduk. Denetleyicilerimizin ve görünümlerimize ait ilk kodu otomatik olarak oluşturmak için Visual Studio 'dan faydalanır. Ayrıca, veritabanı modeli sınıflarınızı otomatik olarak oluşturmak için Entity Framework avantajlarından de yararlanıyoruz.

Şu anda Contact Manager uygulamasıyla kişi kayıtlarını listeliyoruz, oluşturabilir, düzenleyebilir ve silebilirsiniz. Diğer bir deyişle, veritabanı odaklı bir Web uygulaması için gereken tüm temel veritabanı işlemlerini gerçekleştirebiliriz.

Ne yazık ki uygulamamız bazı sorunlar içeriyor. İlk olarak bunu kabul etmek için, Ilgili kişi Yöneticisi uygulaması en çekici uygulama değildir. Bazı tasarım işleri gerektirir. Bir sonraki yinelemede, uygulamanın görünümünü geliştirmek için varsayılan görünüm ana sayfasını ve basamaklı stil sayfasını nasıl değiştirebileceğimizi inceleyeceğiz.

İkincisi, herhangi bir form doğrulaması uygulamadık. Örneğin, form alanlarından herhangi birine değer girmeden kişi oluştur formunu göndermenizi önleyen bir şey yoktur. Ayrıca, geçersiz telefon numaralarını ve e-posta adreslerini de girebilirsiniz. Yineleme #3, form doğrulama sorununun üstesinden gelmeye başladık.

Son olarak, en önemlisi, Contact Manager uygulamasının geçerli yinelemesi kolayca değiştirilemez veya korunmaz. Örneğin, veritabanı erişim mantığı, denetleyici eylemlerine göre doğru bir şekilde yapılır. Bu, denetleyicilerimizi değiştirmeden veri erişim kodumuzu değiştiremeyeceğiniz anlamına gelir. Daha sonraki yinelemelerde, Iletişim yöneticisinin değişiklik yapmasını daha dayanıklı hale getirmek için uygulayabilmemiz gereken yazılım tasarım düzenlerini araştırıyoruz.

> [!div class="step-by-step"]
> [Next](iteration-2-make-the-application-look-nice-cs.md)
