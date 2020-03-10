---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 'Uygulamalı laboratuvar: sürdürülebilir Azure Web siteleri: değişikliği ve ölçeği yönetme | Microsoft Docs'
author: rick-anderson
description: Bu laboratuvarda, Microsoft Azure Web sitelerini üretime derlemeyi ve dağıtmayı nasıl kolaylaştırdığını öğrenin.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624273"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>Uygulamalı Laboratuvar: Sürdürülebilir Azure Web Siteleri: Değişiklikleri ve Ölçeği Yönetme

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

> Microsoft Azure Web sitelerini üretime oluşturup dağıtmayı kolaylaştırır. Ancak uygulamanız canlı olduğunda bu işlemi siz yapmanız yeterlidir! Değiştirme gereksinimleri, veritabanı güncelleştirmeleri, ölçek ve daha fazlasını ele almanız gerekir. Neyse ki, sitelerinizi sorunsuz bir şekilde çalışmaya devam etmenize yardımcı olacak çok sayıda özellik ile birlikte Azure App Service.
>
> Azure, her boyuttaki web uygulaması için güvenli ve esnek geliştirme, dağıtım ve ölçeklendirme seçenekleri sunar. Altyapıyı yönetme zahmetsiz olmayan uygulamalar oluşturmak ve dağıtmak için mevcut araçlarınızdan yararlanın.
>
> En sevdiğiniz geliştirme aracını kullanarak oluşturulan içeriği kolayca dağıtarak bir üretim Web uygulamasını dakikalar içinde kendiniz sağlayın. Var olan bir siteyi **Git**, **GitHub**, **Bitbucket**, **TFS**ve hatta **Dropbox**desteğiyle doğrudan kaynak denetiminden dağıtabilirsiniz. En sevdiğiniz IDE 'den veya Windows 'da **PowerShell** kullanarak veya HERHANGI bir işletim sisteminde çalışan **CLI** araçlarından doğrudan bir dağıtım yapın. Dağıtıldıktan sonra, sürekli dağıtım desteğiyle sitelerinizi sürekli güncel tutun.
>
> Azure, büyük veya küçük tüm veriler için ölçeklenebilir, dayanıklı bulut depolama, yedekleme ve kurtarma çözümleri sağlar. Uygulamalar bir üretim ortamına dağıtıldığında, tablolar, Bloblar ve SQL veritabanları gibi depolama hizmetleri, uygulamanızı bulutta ölçeklendirmenize yardımcı olur.
>
> SQL veritabanları ile uygulamanızın yeni sürümlerini dağıttığınızda üretken veritabanınızı güncel tutmanız önemlidir. **Entity Framework Code First Migrations**teşekkür ederiz, veri modelinizin geliştirilmesi ve dağıtılması, ortamınızı dakikalar içinde güncelleştirmek üzere basitleştirilmiştir. Bu uygulamalı laboratuvarda, Web uygulamanızı Microsoft Azure ' de üretim ortamlarına dağıttığınızda karşılaşabileceğiniz farklı konular gösterilecektir.
>
> Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.
>
> Bu konuda daha ayrıntılı bilgi için bkz. [Azure e-kitabı Ile gerçek dünyada bulut uygulamaları oluşturma](building-real-world-cloud-apps-with-windows-azure/introduction.md).

<a id="Overview"></a>
## <a name="overview"></a>Genel bakış

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Mevcut bir modelle Entity Framework geçişleri etkinleştir
- Nesne modelini ve veritabanını Entity Framework geçişleri kullanarak uygun şekilde güncelleştirme
- Git kullanarak Azure App Service dağıtma
- Azure yönetim portalı 'nı kullanarak önceki bir dağıtıma geri alma
- Bir Web uygulamasını ölçeklendirmek için Azure Storage 'ı kullanma
- Azure Yönetim Portalı kullanarak bir Web uygulaması için otomatik ölçeklendirmeyi yapılandırma
- Visual Studio 'da bir yük testi projesi oluşturma ve yapılandırma

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:

- Web veya daha büyük [için Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [.NET 2,2 için Azure SDK](https://www.microsoft.com/windowsazure/sdk/)
- [GIT sürüm denetimi sistemi](http://git-scm.com/download)
- Microsoft Azure aboneliği

    - [Ücretsiz deneme](https://aka.ms/watk-freetrial) için kaydolun
    - MSDN veya MSDN Platformları abonesine sahip bir Visual Studio Professional, Test Professional, Premium veya Ultimate kullanıyorsanız, Azure 'da geliştirme ve test etmeye başlamak için [MSDN avantajınızı](https://aka.ms/watk-msdn) şimdi etkinleştirin
    - [BizSpark](https://aka.ms/watk-bizspark) üyeleri Azure avantajını Visual Studio Ultimate with MSDN aboneliklerine göre otomatik olarak alır
    - [Microsoft iş ortağı ağı](https://aka.ms/watk-mpn) Cloud Essentials programı üyeleri, aylık Azure kredilerini ücretsiz olarak alır

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.

1. Windows Gezgini 'ni açın ve laboratuvarın **kaynak** klasörüne gidin.
2. Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.
3. Kullanıcı hesabı denetimi iletişim kutusu gösteriliyorsa, devam etmek için eylemi onaylayın.

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

1. [Entity Framework geçişleri kullanma](#Exercise1)
2. [Bir Web uygulamasını hazırlama için dağıtma](#Exercise2)
3. [Üretimde dağıtım geri alma gerçekleştiriliyor](#Exercise3)
4. [Azure Storage kullanarak ölçeklendirme](#Exercise4)
5. [Web Apps Için otomatik ölçeklendirmeyi kullanma](#Exercise5) (Visual Studio 2013 Ultimate Edition için isteğe bağlı)

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **75 dakika**

> [!NOTE]
> Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir. Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler. Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır. Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>Alıştırma 1: Entity Framework geçişlerini kullanma

Bir uygulama geliştirirken, veri modeliniz zaman içinde değişebilir. Bu değişiklikler, veritabanınızdaki mevcut modeli etkileyebilir (yeni bir sürüm oluşturuyorsanız) ve hataları önlemek için veritabanınızı güncel tutmak önemlidir.

Modelinizdeki bu değişikliklerin izlenmesini basitleştirmek için **Entity Framework Code First Migrations** , modelinizi veritabanı şemasıyla karşılaştıran değişiklikleri otomatik olarak algılar ve veritabanınızı güncelleştirmek ve veritabanınızın yeni *sürümlerini* oluşturmak için belirli bir kod oluşturur.

Bu alıştırmada, uygulamanız için **geçişlerinizi** etkinleştirme ve veritabanlarınızı güncelleştirmek için nasıl kolayca tespit ve değişiklik oluşturabileceğiniz gösterilmektedir.

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>Görev 1 – geçişleri etkinleştirme

Bu görevde, **Geek test** veritabanına **Entity Framework Code First Migrations** etkinleştirme, modeli değiştirme ve bu değişikliklerin veritabanına nasıl yansıtıldığını anlama adımlarını öğreneceksiniz.

1. Visual Studio 'Yu açın ve **Source\Ex1-UsingEntityFrameworkMigrations\Begin**adresinden **geeksınav. sln** çözüm dosyasını açın.
2. **NuGet** paketi bağımlılıklarını indirmek ve yüklemek için çözümü derleyin. Bunu yapmak için çözüme sağ tıklayın ve **çözüm oluştur** ' a tıklayın veya **CTRL + SHIFT + B**tuşlarına basın.
3. Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' na tıklayın.
4. **Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın. Mevcut modeli temel alan bir ilk geçiş oluşturulacaktır.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![Geçişleri etkinleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Geçişleri etkinleştirme")

    *Geçişleri etkinleştirme*

    > [!NOTE]
    > Bu komut, **Configuration.cs**adlı bir dosya Içeren Geek test projesine bir **geçişler** klasörü ekler. **Yapılandırma** sınıfı, geçiş işleminin bağlam için nasıl davranacağını yapılandırmanıza olanak tanır.
5. Geçişler etkinken, veritabanını **Geek sınavın** gerektirdiği ilk verilerle doldurmak için **yapılandırma** sınıfını güncelleştirmeniz gerekir. **Geçişler**altında **Configuration.cs** dosyasını, bu laboratuvarın **source\varlıklar** klasöründe bulunan ile değiştirin.

    > [!NOTE]
    > **Geçişler** her veritabanı güncelleştirmesiyle ilgili **çekirdek** yöntemini çağıracak olduğundan, kayıtların veritabanında yinelenmediğinden emin olmanız gerekir. **AddOrUpdate** yöntemi yinelenen verilerin engellenmesine yardımcı olur.
6. İlk geçiş eklemek için aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.

    > [!NOTE]
    > LocalDB örneğiniz içinde &quot;GeekQuizProd&quot; adlı bir veritabanı olmadığından emin olun.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![Temel şema geçişi ekleniyor](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Temel şema geçişi ekleniyor")

    *Temel şema geçişi ekleniyor*

    > [!NOTE]
    > **Geçiş geçişi** , son geçişten sonra, modelinizde yaptığınız değişikliklere dayalı olarak bir sonraki geçişi kankatacaktır. Bu durumda, projenin ilk geçişi olduğu için, **Triviacontext** sınıfında tanımlanmış tüm tabloları oluşturmak üzere betikleri ekler.
7. Aşağıdaki komutu çalıştırarak veritabanını güncelleştirmek için geçişi yürütün. Bu komut için, hedef veritabanına uygulanan SQL deyimlerini görüntülemek üzere **verbose** bayrağını belirtin.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![İlk veritabanı oluşturuluyor](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "İlk veritabanı oluşturuluyor")

    *İlk veritabanı oluşturuluyor*

    > [!NOTE]
    > **Update-Database** bekleyen geçişleri veritabanına uygular. Bu durumda, Web. config dosyanızda tanımlanan bağlantı dizesini kullanarak veritabanını oluşturur.
8. **Görünüm** menüsüne gidin ve **SQL Server Nesne Gezgini**açın.

    ![SQL Server Nesne Gezgini aç](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server Nesne Gezgini aç")

    *SQL Server Nesne Gezgini aç*
9. **SQL Server Nesne Gezgini** penceresinde, **SQL Server** düğümüne sağ tıklayıp **SQL Server Ekle...** seçeneğini belirleyerek LocalDB örneğinizi bağlayın.

    ![SQL Server örneği ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server örneği ekleme")

    *SQL Server Nesne Gezgini SQL Server örnek ekleme*
10. **Sunucu adını** *(LocalDB) \v11.0* olarak ayarlayın ve **Windows kimlik doğrulamasını** kimlik doğrulama modu olarak bırakın. Devam etmek için **Bağlan**’a tıklayın.

    ![LocalDB 'ye bağlanma](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB 'ye bağlanma")

    *LocalDB 'ye bağlanma*
11. **GeekQuizProd** veritabanını açın ve **Tablolar** düğümünü genişletin. Gördüğünüz gibi, **Update-Database** komutu **triviacontext** sınıfında tanımlanmış tüm tabloları üretti. Dbo 'yi bulun **. Triviasorular** tablosu ve Columns düğümünü açın. Sonraki görevde, bu tabloya yeni bir sütun ekleyecek ve **geçişleri**kullanarak veritabanını güncellendirilecektir.

    ![Soruların sütunları](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Soruların sütunları")

    *Soruların sütunları*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>Görev 2 – geçişler kullanılarak veritabanı şemasını güncelleştirme

Bu görevde, modelinizde bir değişikliği algılamak ve veritabanını güncelleştirmek için gerekli kodu oluşturmak üzere **Entity Framework Code First Migrations** kullanacaksınız. Yeni bir özellik ekleyerek **Triviasoruların** varlığını güncelleşirsiniz. Daha sonra yeni bir geçiş oluşturmak için komutları çalıştırarak tabloya yeni bir sütun ekleyin.

1. **Çözüm Gezgini**, **modeller** klasörünün içinde bulunan **TriviaQuestion.cs** dosyasına çift tıklayın.
2. Aşağıdaki kod parçacığında gösterildiği gibi **İpucu**adlı yeni bir özellik ekleyin.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. **Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın. Modelimizin değişikliğini yansıtan yeni bir geçiş oluşturulacaktır.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![Geçiş Ekle](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Geçiş Ekle")

    *Geçiş Ekle*

    > [!NOTE]
    > Geçiş dosyası, **yukarı** ve **aşağı**olmak üzere iki yöntemden oluşur.
    >
    > - **Up** yöntemi, uygulamamız için geçerli sürümünün veritabanına hangi değişikliklerin uygulanacağını belirtmek için kullanılacaktır.
    > - **Up** yöntemine eklediğimiz değişiklikleri tersine çevirmek için **aşağı** doğru kullanılır.
    >
    > Veritabanı geçişi veritabanını güncelleştirdiğinde, zaman damgası sırasındaki tüm geçişleri çalıştırır ve yalnızca son güncelleştirmeden bu yana kullanılmamış olanlar (\_MigrationHistory tablosu, hangi geçişlerin uygulandığını izler). Tüm geçişlerin **up** metodu çağrılır ve veritabanına belirttiğimiz değişiklikleri yapar. Önceki bir geçişe geri dönmek isterseniz, değişiklikleri ters sırada yinelemek için **azaltma** yöntemi çağırılır.
4. **Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. **Update-Database** komutunun çıktısı, aşağıdaki görüntüde gösterildiği gibi **triviasorular** tablosuna yeni bir sütun eklemek için **alter table** SQL deyimini oluşturdu.

    ![Oluşturulan sütun SQL açıklaması ekle](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Oluşturulan sütun SQL açıklaması ekle")

    *Oluşturulan sütun SQL açıklaması ekle*
6. **SQL Server Nesne Gezgini**, dbo 'yı yenileyin **. Triviasorular** tablosu ve yeni **İpucu** sütununun görüntülendiğini kontrol edin.

    ![Yeni Ipucu sütununu gösterme](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Yeni Ipucu sütununu gösterme")

    *Yeni Ipucu sütununu gösterme*
7. **TriviaQuestion.cs** düzenleyicisine geri döndüğünüzde, aşağıdaki kod parçacığında gösterildiği gibi *Ipucu* özelliğine bir **StringLength** kısıtlaması ekleyin.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. **Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. **Paket Yöneticisi konsolunda**, aşağıdaki komutu girin ve ardından **ENTER**tuşuna basın.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. **Update-Database** komutunun çıktısı, aşağıdaki görüntüde gösterildiği gibi **üç aylık** dönemin *İpucu* sütun türünü güncelleştirmek için bir **alter table** SQL deyimini oluşturdu.

    ![ALTER COLUMN SQL ifadesi oluşturuldu](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "ALTER COLUMN SQL ifadesi oluşturuldu")

    *ALTER COLUMN SQL ifadesi oluşturuldu*
11. **SQL Server Nesne Gezgini**, dbo 'yı yenileyin **. Triviasorular** tablosu ve **İpucu** sütun türünün **nvarchar (150)** olup olmadığını denetleyin.

    ![Yeni kısıtlama gösteriliyor](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Yeni kısıtlama gösteriliyor")

    *Yeni kısıtlama gösteriliyor*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>Alıştırma 2: hazırlama için bir Web uygulaması dağıtma

**Azure App Service Web Apps** , hazırlanan yayımlamayı gerçekleştirmenize olanak sağlar. Hazırlanan yayımlama, her varsayılan üretim sitesi için bir hazırlama site yuvası oluşturur ve bu yuvaları bir süre sonra takas etmenize olanak sağlar. Bu, genel kullanıma sunulmadan önce değişiklikleri doğrulamak, site içeriğini artımlı olarak bütünleştirmek ve değişiklikler beklendiği gibi çalışmıyorsa geri dönmek için yararlıdır.

Bu alıştırmada, git kaynak denetimi 'ni kullanarak **Geek test** uygulamasını Web uygulamanızın hazırlama ortamına dağıtacaksınız. Bunu yapmak için, Web uygulamasını oluşturur ve yönetim portalında gerekli bileşenleri temin eder, bir **Git** deposu yapılandırır ve uygulama kaynak kodunu yerel bilgisayarınızdan hazırlama yuvasına gönderirsiniz. Ayrıca, üretim veritabanınızı önceki alıştırmada oluşturduğunuz **Code First Migrations** de güncelleştirebilirsiniz. Sonra, işlemini doğrulamak için bu test ortamında uygulamayı yürütecaksınız. Beklentilerinize göre çalıştığından emin olduktan sonra, uygulamayı üretime yükseltemeirsiniz.

> [!NOTE]
> Hazırlanmış yayımlamayı etkinleştirmek için Web uygulamasının **Standart modda**olması gerekir. Web uygulamanızı standart moda değiştirirseniz ek ücretler tahakkuk ettiğine unutmayın. Fiyatlandırma hakkında daha fazla bilgi için bkz. [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>Görev 1 – Azure App Service bir Web uygulaması oluşturma

Bu görevde, yönetim portalından **Azure App Service** bir Web uygulaması oluşturacaksınız. Ayrıca, uygulama verilerini kalıcı hale getirmek ve kaynak denetimi için yerel bir git deposu yapılandırmak üzere bir **SQL veritabanı** yapılandıracaksınız.

1. [Azure yönetim portalı](https://manage.windowsazure.com) ' na gidin ve aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.

    ![Azure yönetim portalı 'nda oturum açın](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *Azure yönetim portalı 'nda oturum açın*
2. Sayfanın alt kısmındaki komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web uygulaması oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Yeni bir Web uygulaması oluşturma")

    *Yeni bir Web uygulaması oluşturma*
3. **İşlem**, **Web sitesi** ve sonra **özel oluştur**' a tıklayın.

    ![Özel oluştur kullanarak yeni bir Web uygulaması oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Özel oluştur kullanarak yeni bir Web uygulaması oluşturma")

    *Özel oluştur kullanarak yeni bir Web uygulaması oluşturma*
4. **Yeni Web sitesi-özel oluştur** iletişim kutusunda, kullanılabilir bir **URL** (örn. *Geek-test*) girin, **bölge** açılan listesinden bir konum seçin ve **veritabanı** açılır listesinden **Yeni bir SQL veritabanı oluştur** ' u seçin. Son olarak, **kaynak denetiminden yayınla** onay kutusunu seçin ve **İleri**' ye tıklayın.

    ![Yeni Web uygulamasını özelleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *Yeni Web uygulamasını özelleştirme*
5. Veritabanı ayarları için aşağıdaki bilgileri belirtin:

   - **Ad** metin kutusuna bir veritabanı adı girin (örn. *geektest\_DB*)
   - Sunucu **açılan** listesinde, **Yeni SQL veritabanı sunucusu**' nu seçin. Alternatif olarak, var olan bir sunucuyu seçebilirsiniz.
   - **Veritabanı Kullanıcı adı** ve **VERITABANı parolası** kutularına SQL veritabanı sunucusu için yönetici kullanıcı adını ve parolasını girin. Zaten oluşturduğunuz bir sunucuyu seçerseniz parola istenir.

     ![Veritabanı ayarlarını belirtme](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *Veritabanı ayarlarını belirtme*
6. Devam etmek için **İleri** 'ye tıklayın.
7. Kullanılacak kaynak denetimi için **yerel Git deposu** ' nu seçin ve **İleri**' ye tıklayın.

    > [!NOTE]
    > Dağıtım kimlik bilgileri (Kullanıcı adı ve parola) istenebilir.

    ![Git deposu oluşturuluyor](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *Git deposu oluşturuluyor*
8. Yeni Web uygulaması oluşturuluncaya kadar bekleyin.

    > [!NOTE]
    > Azure, varsayılan olarak *azurewebsites.net* adresinde etki alanları sağlar, ancak Azure yönetim portalı 'nı kullanarak özel etki alanları ayarlama olasılığından de olanak tanır. Ancak, yalnızca belirli Azure App Service modlarını kullanıyorsanız özel etki alanlarını yönetebilirsiniz.
    >
    > Azure App Service ücretsiz, paylaşılan, temel, standart ve Premium sürümlerde kullanılabilir. Ücretsiz ve paylaşılan modda tüm Web uygulamaları çok kiracılı bir ortamda çalışır ve CPU, bellek ve ağ kullanımı için kotalar vardır. En fazla ücretsiz uygulama sayısı planınızda değişiklik gösterebilir. Standart modda, standart Azure işlem kaynaklarına karşılık gelen adanmış sanal makinelerde çalışan uygulamaları seçersiniz. Web uygulaması modu yapılandırmasını Web uygulamanızın **Ölçek** menüsünde bulabilirsiniz.
    >
    > ![Azure App Service modları](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service modları")
    >
    > **Paylaşılan** veya **Standart** mod kullanıyorsanız, uygulamanızın **Yapılandır** menüsüne gidip *etki alanı adları*altındaki **etki alanlarını yönet** ' e tıklayarak web uygulamanız için özel etki alanlarını yönetebilirsiniz.
    >
    > ![Etki alanlarını yönetme](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Etki Alanlarını Yönet")
    >
    > ![Özel etki alanlarını yönetme](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Özel etki alanlarını yönetme")
9. Web uygulaması oluşturulduktan sonra, yeni Web uygulamasının çalıştığını denetlemek için **URL** sütununun altındaki bağlantıya tıklayın.

    ![Yeni Web uygulamasına göz atma](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *Yeni Web uygulamasına göz atma*

    ![çalışan Web uygulaması](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *çalışan Web uygulaması*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>Görev 2 – üretim SQL veritabanı oluşturuluyor

Bu görevde, önceki görevde oluşturduğunuz **Azure SQL veritabanı** örneğini hedefleyen veritabanını oluşturmak için **Entity Framework Code First Migrations** kullanacaksınız.

1. Yönetim Portalı, önceki görevde oluşturduğunuz Web uygulamasına gidin ve **panosuna**gidin.
2. **Pano** sayfasında, **Hızlı bakış** bölümünün altındaki **bağlantı dizelerini görüntüle** bağlantısını tıklatın.

    ![Bağlantı dizelerini görüntüle](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "Bağlantı dizelerini görüntüle")

    *Bağlantı dizelerini görüntüle*
3. **Bağlantı dizesi** değerini kopyalayın ve iletişim kutusunu kapatın.

    ![Azure Yönetim Portalı bağlantı dizesi](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure Yönetim Portalı bağlantı dizesi")

    *Azure Yönetim Portalı bağlantı dizesi*
4. Azure 'da SQL veritabanlarının listesini görmek için **SQL veritabanları** ' na tıklayın

    ![SQL veritabanı menüsü](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL veritabanı menüsü")

    *SQL veritabanı menüsü*
5. Önceki görevde oluşturduğunuz veritabanını bulun ve sunucusuna tıklayın.

    ![SQL veritabanı sunucusu](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Veritabanı sunucusu")

    *SQL veritabanı sunucusu*
6. Sunucusunun **hızlı başlangıç** sayfasında, **Yapılandır**' a tıklayın.

    ![Menüyü Yapılandır](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Menüyü Yapılandır")

    *Menüyü Yapılandır*
7. **Izin VERILEN IP adresleri** bölümünde, IP 'Nizin SQL veritabanı sunucusuna bağlanmasını sağlamak için **izin verilen IP adresleri bağlantısına Ekle** ' ye tıklayın.

    ![İzin verilen IP adresleri](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "İzin verilen IP adresleri")

    *İzin verilen IP adresleri*
8. Adımı gerçekleştirmek için sayfanın alt kısmındaki **Kaydet** ' e tıklayın.
9. Visual Studio 'ya geri dönün.
10. **Paket Yöneticisi konsolunda**, *[bağlantı-dize]* yer tutucusunu Azure 'dan kopyaladığınız bağlantı dizesiyle değiştirerek aşağıdaki komutu yürütün

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![Windows Azure SQL veritabanı 'nı hedefleyen veritabanını güncelleştir](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL veritabanı 'nı hedefleyen veritabanını güncelleştir")

    *Azure SQL veritabanı 'nı hedefleyen veritabanını güncelleştirme*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>Görev 3 – git kullanarak hazırlama için Geek sınavını dağıtma

Bu görevde, Web uygulamanızda hazırlanan yayımlamayı etkinleştirecektir. Daha sonra, Geek test uygulamasını doğrudan yerel bilgisayarınızdan Web uygulamanızın hazırlama ortamına yayımlamak için git ' i kullanacaksınız.

1. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web uygulamasının adına tıklayın.

    ![Web uygulaması yönetim sayfalarını açma](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *Web uygulaması yönetim sayfalarını açma*
2. **Ölçek** sayfasına gidin. **Genel** bölümünde, yapılandırma için **Standart** ' ı seçin ve komut çubuğunda **Kaydet** ' e tıklayın.

    > [!NOTE]
    > Tüm Web uygulamalarını geçerli bölgede ve abonelikte **Standart** modda çalıştırmak Için, **siteleri seçin** yapılandırması ' nda **Tümünü Seç** onay kutusunu seçili bırakın. Aksi takdirde, **Tümünü Seç** onay kutusunu temizleyin.

    ![Web uygulamasını standart moda yükseltme](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Web uygulamasını standart moda yükseltme")

    *Web uygulamasını standart moda yükseltme*
3. Değişiklikleri onaylamak için **Evet** ' e tıklayın.

    ![Standart mod değişikliğini onaylama](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Web uygulaması modunun değiştirilmesine devam etme")

    *Standart mod değişikliğini onaylama*
4. **Pano** sayfasına gidin ve **Hızlı bakış** bölümünde **hazırlanan yayımlamayı etkinleştir** ' e tıklayın.

    ![Hazırlanan yayımlamayı etkinleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Hazırlanan yayımlamayı etkinleştirme")

    *Hazırlanan yayımlamayı etkinleştirme*
5. Hazırlanmış yayımlamayı etkinleştirmek için **Evet** ' i tıklatın.

    ![Hazırlanan yayımlamayı onaylama](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Aşamalı yayımlamayı etkinleştirmek için Evet 'i tıklatın")

    *Hazırlanan yayımlamayı onaylama*
6. Web Apps listesinde, hazırlama site yuvasını göstermek için Web uygulaması adınızın solundaki işareti genişletin. Web uygulamanızın adı ve sonra ***(hazırlama)*** bulunur. Yönetim sayfasına gitmek için hazırlama sitesine tıklayın.

    ![Hazırlama Web uygulamasına gitme](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Hazırlama Web uygulamasına gitme")

    *Hazırlama uygulamasına gitme*
7. Yönetim sayfasının diğer Web uygulamaları yönetim sayfası gibi göründüğünü unutmayın. **Dağıtımlar** sayfasına gidin ve **Git URL 'si** değerini kopyalayın. Bu alıştırmanın ilerleyen kısımlarında kullanacaksınız.

    ![Git URL 'SI değeri kopyalanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *Git URL 'SI değeri kopyalanıyor*
8. Yeni bir **Git Bash** konsolu açın ve aşağıdaki komutları yürütün. *[-APPLICATION-Path]* yer tutucusunu, bu laboratuvarın **Source\ex1-deployingwebsitetostaging\begin** klasöründe bulunan **geektest** çözümünün yoluyla güncelleştirin.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git başlatması ve ilk kayıt](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git başlatması ve ilk kayıt*
9. Web uygulamanızı uzak **Git** deposuna göndermek için aşağıdaki komutu çalıştırın. Yer tutucusunu, yönetim portalından edindiğiniz URL ile değiştirin. Sizden dağıtım parolanızı girmeniz istenir.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Microsoft Azure 'a gönderiliyor](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *Azure 'a gönderiliyor*

    > [!NOTE]
    > Bir Web uygulamasının FTP ana bilgisayarına veya GIT deposuna içerik dağıttığınızda, Web uygulamasının **hızlı başlangıç** veya **Pano** yönetim sayfalarından oluşturduğunuz **dağıtım kimlik bilgilerini** kullanarak kimlik doğrulaması yapmanız gerekir. Dağıtım kimlik bilgilerinizi görmüyorsanız, yönetim portalı 'nı kullanarak bunları kolayca sıfırlayabilirsiniz. Web uygulaması **panosu** sayfasını açın ve **dağıtım kimlik bilgilerinizi sıfırlayın** bağlantısına tıklayın. Yeni bir parola girin ve **Tamam 'a**tıklayın. Dağıtım kimlik bilgileri, aboneliğinizle ilişkili tüm Web uygulamalarıyla birlikte kullanılmak üzere geçerlidir.
10. Web uygulamasının başarıyla Azure 'a itildiğini doğrulamak için yönetim portalına dönün ve **Web siteleri**' ne tıklayın.
11. Web uygulamanızı bulun ve hazırlama site yuvasını göstermek için girişi genişletin. Yönetim sayfasına gitmek için **adına** tıklayın.
12. **Dağıtım geçmişini**görmek için **dağıtımlar** ' a tıklayın. *&quot;Ilk işlemesini&quot;* **etkin bir dağıtım** olduğunu doğrulayın.

    ![Etkin dağıtım](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *Etkin dağıtım*
13. Son olarak, Web uygulamasına gitmek için komut çubuğunda bulunan **Araştır** ' a tıklayın.

    ![Web uygulamasına gözatamıyorum](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *Web uygulamasına gözatamıyorum*
14. Uygulama başarıyla dağıtılırsa Geek test oturum açma sayfasını görürsünüz.

    > [!NOTE]
    > Dağıtılan uygulamanın adres URL 'SI, Web uygulamanızın adını ve ardından *hazırlamayı*içerir.

    ![Hazırlama ortamında çalışan uygulama](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *Hazırlama ortamında çalışan uygulama*
15. Uygulamayı araştırmak isterseniz, yeni bir kullanıcı kaydetmek için **Kaydet** ' e tıklayın. Hesap ayrıntılarını bir Kullanıcı adı, e-posta adresi ve parola girerek doldurun. Ardından, uygulama, test ilk sorusunu gösterir. Beklenen şekilde çalıştığından emin olmak için birkaç soruyu yanıtlayın.

    ![Uygulama kullanılmak üzere hazırlanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *Uygulama kullanılmak üzere hazırlanıyor*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>Görev 4 – Web uygulamasını üretime yükseltme

Artık, Web uygulamasının hazırlama ortamında düzgün çalıştığını doğruladığınıza göre, bunu üretime yükseltmeye hazırsınız demektir. Bu görevde, hazırlama site yuvasını üretim site yuvası ile takas edersiniz.

1. Yönetim portalına geri dönün ve hazırlama site yuvasını seçin. Komut çubuğunda **takas et** ' e tıklayın.

    ![Üretime değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *Üretime değiştirme*
2. Değiştirme işlemine devam etmek için onay iletişim kutusunda **Evet** ' e tıklayın. Azure, üretim sitesinin içeriğini hazırlama sitesinin içeriğiyle hemen takas eder.

    > [!NOTE]
    > Hazırlanan sürümden bazı ayarlar otomatik olarak üretim sürümüne (örn. bağlantı dizesi geçersiz kılmaları, işleyici eşlemeleri vb.) kopyalanacak, ancak diğer ayarlar değişmeyecektir (örneğin, DNS uç noktaları, SSL bağlamaları vb.).

    ![Değiştirme işlemi onaylanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *Değiştirme işlemi onaylanıyor*
3. Değiştirme tamamlandıktan sonra üretim yuvasını seçin ve komut çubuğunda, üretim sitesini açmak için **Araştır** ' a tıklayın. Adres çubuğundaki URL 'ye dikkat edin.

    > [!NOTE]
    > Önbelleği temizlemek için tarayıcınızı yenilemeniz gerekebilir. Internet Explorer 'da, **CTRL + R**tuşlarına basarak bunu yapabilirsiniz.

    ![Üretim ortamında çalışan Web uygulaması](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. **GitBash** konsolunda, yerel git deposunun uzak URL 'sini üretim yuvasını hedefleyecek şekilde güncelleştirin. Bunu yapmak için, yer tutucuları dağıtım Kullanıcı adınızla ve Web uygulamanızın adıyla değiştirerek aşağıdaki komutu çalıştırın.

    > [!NOTE]
    > Aşağıdaki alıştırmalarda, değişiklikleri yalnızca laboratuvarın basitliği için hazırlama yerine üretim sitesine gönderirsiniz. Gerçek dünyada bir senaryoda, üretime yükseltmeden önce hazırlama ortamındaki değişikliklerin doğrulanması önerilir.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>Alıştırma 3: üretimde dağıtım geri alma Işlemi gerçekleştiriliyor

Hazırlama ve üretim arasında, örneğin, **ücretsiz** veya **paylaşılan** modla çalışıyorsanız, hazırlık ve üretim arasında dinamik değiştirme gerçekleştirmek için bir hazırlama yuvalarınızın olmadığı senaryolar vardır. Bu senaryolarda, üretime dağıtım yapmadan önce, uygulamanızı yerel olarak veya uzak bir sitede bir test ortamında test etmeniz gerekir. Ancak, üretim sitesinde test aşamasında algılanamayan bir sorun ortaya çıkabilir. Bu durumda, mümkün olduğunca hızlı bir şekilde uygulamanın önceki ve daha kararlı bir sürümüne kolayca geçiş mekanizması olması önemlidir.

**Azure App Service**, kaynak denetiminden sürekli dağıtım, yönetim portalı 'nda kullanılabilir yeniden **dağıtma** eylemi sayesinde bunu mümkün hale getirir. Azure, depoya gönderilen işlemelerle ilişkili dağıtımları izler ve istediğiniz zaman, önceki dağıtımlarınızdan herhangi birini kullanarak uygulamanızı yeniden dağıtmaya yönelik bir seçenek sağlar.

Bu alıştırmada, bir *hatayı*kasıtlı olarak gösteren **Geek test** uygulamasındaki kodda bir değişiklik gerçekleştirirsiniz. Hatayı görmek için uygulamayı üretime dağıtırsınız ve ardından önceki duruma geri dönmek için yeniden dağıtma özelliğinden faydalanabilirsiniz.

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>Görev 1 – Geek test uygulamasını güncelleştirme

Bu görevde, seçilen test seçeneğini veritabanından yeni bir yönteme alan mantığın bir kısmını ayıklamak için **Triviacontroller** sınıfının küçük bir kod parçasını yeniden düzenlemelisiniz.

1. Önceki alıştırmada **Geektest** çözümüyle Visual Studio örneğine geçin.
2. **Çözüm Gezgini**, **TriviaController.cs** dosyasını **denetleyiciler** klasörü içinde açın.
3. **Storeasync** yöntemini bulun ve aşağıdaki şekilde vurgulanan kodu seçin.

    ![Kodu seçme](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *Kodu seçme*
4. Seçili koda sağ tıklayın, yeniden **Düzenle** menüsünü genişletin ve **yöntemi ayıkla...** seçeneğini belirleyin.

    ![Kod yeni bir yöntem olarak ayıklanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *Ayıklama yöntemi seçiliyor*
5. **Yöntemi Ayıkla** iletişim kutusunda, yeni yöntem *matchesoption* olarak adlandırın ve **Tamam**' a tıklayın.

    ![Yöntem adını belirtme](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *Ayıklanan metodun adını belirtme*
6. Daha sonra seçili kod **Matchesoption** yöntemine ayıklanır. Elde edilen kod aşağıdaki kod parçacığında gösterilmiştir.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>Görev 2 – Geek test uygulamasını yeniden dağıtma

Artık önceki görevde yaptığınız değişiklikleri depoya göndererek, üretim ortamına yeni bir dağıtım tetikleyitecaksınız. Daha sonra, Internet Explorer tarafından sunulan **F12 geliştirme araçlarını** kullanarak bir sorun troubleshot ve ardından Azure Yönetim portalından önceki dağıtıma geri alma işlemi gerçekleştirirsiniz.

1. Güncelleştirilmiş uygulamayı Azure App Service dağıtmak için yeni bir **Git Bash** konsolu açın.
2. Değişiklikleri Azure 'a göndermek için aşağıdaki komutları yürütün. *[-APPLICATION-Path]* yer tutucusunu **geektest** çözümünün yoluyla güncelleştirin. Sizden dağıtım parolanızı girmeniz istenir.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Yeniden düzenlenmiş kodunu Azure 'a iletme](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *Yeniden düzenlenmiş kodunu Azure 'a iletme*
3. Internet Explorer 'ı açın ve Web uygulamanıza gidin (örn. `http://<your-web-site>.azurewebsites.net`). Önceden oluşturulan kimlik bilgilerini kullanarak oturum açın.
4. Geliştirici araçlarını başlatmak için **F12** tuşuna basın, **ağ** sekmesini seçin ve kaydetmeye başlamak için **Yürüt** düğmesine tıklayın.

    ![Ağ kaydı başlatılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Ağ kaydı başlatılıyor")

    *Ağ kaydı başlatılıyor*
5. Sınavın herhangi bir seçeneğini belirleyin. Hiçbir şeyin gerçekleşmeyecek olduğunu göreceksiniz.
6. **F12** PENCERESINDE, http post isteğine karşılık gelen GIRIŞ bir http **500** sonucunu gösterir.

    ![HTTP 500 hatası](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 hatası*
7. **Konsol** sekmesini seçin. Hatanın ayrıntıları ile bir hata günlüğe kaydedilir.

    ![Günlüğe kaydedilen hata](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *Günlüğe kaydedilen hata*
8. Hatanın Ayrıntılar bölümünü bulun. Açıkça, bu hata önceki adımlarda yaptığınız kod yeniden düzenlemesi nedeniyle oluşur.

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.
9. Tarayıcıyı kapatmayın.
10. Yeni bir tarayıcı örneğinde [Azure yönetim portalı](https://manage.windowsazure.com) ' na gidin ve aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.
11. **Web siteleri** ' ni seçin ve alıştırma 2 ' de oluşturduğunuz Web uygulamasına tıklayın.
12. **Dağıtımlar** sayfasına gidin. Gerçekleştirilen tüm yürütmelerin dağıtım geçmişinde listelendiğini unutmayın.

    ![Mevcut dağıtımların listesi](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *Mevcut dağıtımların listesi*
13. Önceki yürütmeyi seçin ve komut çubuğunda yeniden **Dağıt** ' a tıklayın.

    ![Önceki işleme yeniden dağıtılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *Önceki işleme yeniden dağıtılıyor*
14. Onaylamanız istendiğinde **Evet**' e tıklayın.

    ![Yeniden dağıtımı onaylama](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. Dağıtım tamamlandığında, Web uygulamanızla birlikte tarayıcı örneğine dönün ve **CTRL + F5**tuşlarına basın.
16. Seçeneklerden herhangi birine tıklayın. Ters çevir animasyonu artık alınacaktır ve sonuç (*doğru/yanlış*) görüntülenecektir.
17. Seçim **Git Bash** konsoluna geçin ve önceki işlemeye dönmek için aşağıdaki komutları yürütün.

    > [!NOTE]
    > Bu komutlar, hatalı işlemede gerçekleştirilen git deposundaki tüm değişiklikleri geri yükleyen yeni bir kayıt oluşturur. Daha sonra Azure, yeni yürütmeyi kullanarak uygulamayı yeniden dağıtırsınız.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>Alıştırma 4: Azure Storage kullanarak ölçeklendirme

**BLOB 'lar** , büyük miktarlarda yapılandırılmamış metin veya video, ses ve görüntü gibi ikili verileri depolamanın en kolay yoludur. Uygulamanızın statik içeriğini depolamaya taşımak, doğrudan tarayıcıya görüntü veya belge sunarak uygulamanızı ölçeklendirmenize yardımcı olur.

Bu alıştırmada, uygulamanızın statik içeriğini bir blob kapsayıcısına taşıyacaksınız. Daha sonra, içeriğinizi blob kapsayıcısına yönlendirmek üzere **Web. config** dosyasına BIR **ASP.net URL yeniden yazma kuralı** eklemek için uygulamanızı yapılandıracaksınız.

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>Görev 1 – Azure depolama hesabı oluşturma

Bu görevde, yönetim portalını kullanarak yeni bir depolama hesabı oluşturmayı öğreneceksiniz.

1. [Azure yönetim portalı](https://manage.windowsazure.com) ' na gidin ve aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.
2. Yeni ' yi seçin **| Veri Hizmetleri | Depolama |** Yeni bir depolama hesabı oluşturmaya başlamak için hızlı oluştur. Hesap için benzersiz bir ad girin ve listeden bir **bölge** seçin. Devam etmek için **depolama hesabı oluştur** ' a tıklayın.

    ![Yeni depolama hesabı oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Yeni depolama hesabı oluşturma")

    *Yeni depolama hesabı oluşturma*
3. **Depolama** bölümünde, aşağıdaki adımla devam etmek için yeni depolama hesabının durumu *çevrimiçi* olarak değişene kadar bekleyin.

    ![Depolama hesabı oluşturuldu](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Depolama hesabı oluşturuldu")

    *Depolama hesabı oluşturuldu*
4. Depolama hesabı adına tıklayın ve ardından sayfanın üst kısmındaki **Pano** bağlantısına tıklayın. **Pano** sayfası, hesap durumu ve uygulamalarınız dahilinde kullanılabilecek hizmet uç noktaları hakkında bilgi sağlar.

    ![Depolama hesabı panosunu görüntüleme](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Depolama hesabı panosunu görüntüleme")

    *Depolama hesabı panosunu görüntüleme*
5. Gezinti çubuğundaki **erişim tuşlarını Yönet** düğmesine tıklayın.

    ![Erişim anahtarlarını Yönet düğmesi](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Erişim anahtarlarını Yönet düğmesi")

    *Erişim anahtarlarını Yönet düğmesi*
6. **Erişim anahtarlarını Yönet** iletişim kutusunda, Aşağıdaki alıştırmada gerekli olacak şekilde **depolama hesabı adı** ve **birincil erişim anahtarı** ' nı kopyalayın. Sonra iletişim kutusunu kapatın.

    ![Erişim anahtarını Yönet iletişim kutusu](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Erişim anahtarını Yönet iletişim kutusu")

    *Erişim anahtarını Yönet iletişim kutusu*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>Görev 2 – bir varlığı Azure Blob depolamaya yükleme

Bu görevde, depolama hesabınıza bağlanmak için Visual Studio 'daki Sunucu Gezgini penceresini kullanacaksınız. Daha sonra bir blob kapsayıcısı oluşturacak ve kapsayıcıya Geek test logosu içeren bir dosya yükleyeceksiniz.

1. Önceki alıştırmada **Geektest** çözümüyle Visual Studio örneğine geçin.
2. Menü çubuğundan **Görünüm** ' ü seçin ve ardından **Sunucu Gezgini**' ye tıklayın.
3. **Sunucu Gezgini**, **Azure** düğümüne sağ tıklayın ve **Azure 'a Bağlan...** seçeneğini belirleyin. Aboneliğinizle ilişkili Microsoft hesabı kullanarak oturum açın.

    ![Microsoft Azure'a Bağlan](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *Azure'a bağlanma*
4. **Azure** düğümünü genişletin, **depolama alanı** ' na sağ tıklayın ve **dış depolama Ekle...** seçeneğini belirleyin.
5. **Yeni depolama hesabı ekle** iletişim kutusunda, önceki görevde edindiğiniz **hesap adını** ve **hesap anahtarını** girip **Tamam**' a tıklayın.

    ![Yeni depolama hesabı Ekle iletişim kutusu](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *Yeni depolama hesabı Ekle iletişim kutusu*
6. Depolama hesabınız **depolama** düğümünün altında görünmelidir. Depolama hesabınızı genişletin, **Bloblar** ' a sağ tıklayıp **BLOB kapsayıcısı oluştur...** ' u seçin.

    ![Blob kapsayıcısı oluştur](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob kapsayıcısı oluştur")

    *Blob kapsayıcısı oluştur*
7. **BLOB kapsayıcısı oluştur** iletişim kutusunda, blob kapsayıcısı için bir ad girin ve **Tamam**' a tıklayın.

    ![Blob kapsayıcısı oluştur iletişim kutusu](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob kapsayıcısı oluştur iletişim kutusu")

    *Blob kapsayıcısı oluştur iletişim kutusu*
8. Yeni blob kapsayıcısı **Bloblar** düğümüne eklenmelidir. Kapsayıcıyı ortak hale getirmek için kapsayıcıdaki erişim izinlerini değiştirin. Bunu yapmak için, **görüntüler** kapsayıcısını sağ tıklatın ve **Özellikler**' i seçin.

    ![görüntü kapsayıcısı özellikleri](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "görüntü kapsayıcısı özellikleri")

    *Görüntü kapsayıcısı özellikleri*
9. **Özellikler** penceresinde, **kapsayıcıya** **Genel okuma erişimi** ayarlayın.

    ![Genel okuma erişimi Özelliği değiştiriliyor](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Genel okuma erişimi Özelliği değiştiriliyor")

    *Genel okuma erişimi Özelliği değiştiriliyor*
10. Genel erişim özelliğini değiştirmek istediğinizden emin olup istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Microsoft Visual Studio uyarısı](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio uyarısı")

    *Microsoft Visual Studio uyarısı*
11. **Sunucu Gezgini**, **görüntüler** blob kapsayıcısını sağ tıklatın ve **BLOB kapsayıcısını görüntüle**' yi seçin.

    ![Blob kapsayıcısını görüntüle](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob kapsayıcısını görüntüle")

    *Blob kapsayıcısını görüntüle*
12. Görüntüler kapsayıcısının yeni bir pencerede açılması ve girişin gösterilmemelidir. Blob kapsayıcısına bir dosya yüklemek için **karşıya yükle** simgesine tıklayın.

    ![Girişi olmayan görüntü kapsayıcısı](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Girişi olmayan görüntü kapsayıcısı")

    *Girişi olmayan görüntü kapsayıcısı*
13. **Blobu karşıya yükle** iletişim kutusunda, laboratuvarın **varlıklar** klasörüne gidin. **Logo-Big. png** dosyasını seçin ve **Aç**' a tıklayın.
14. Dosya karşıya yüklenene kadar bekleyin. Karşıya yükleme tamamlandığında, dosyanın görüntüler kapsayıcısında listelenmesi gerekir. Dosya girdisine sağ tıklayıp **URL 'Yi Kopyala**' yı seçin.

    ![Blob URL 'sini Kopyala](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Blob dosyası URL 'sini Kopyala")

    *Blob URL 'sini Kopyala*
15. Internet Explorer 'ı açın ve URL 'YI yapıştırın. Aşağıdaki görüntü tarayıcıda gösterilmelidir.

    ![Windows blob depolamadan logo-Big. png görüntüsü](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "depolamadan logo-Big. png görüntüsü")

    *Azure Blob depolamadan logo-Big. png görüntüsü*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>Görev 3 – Azure Blob depolama alanından statik Içerik kullanmak için çözümü güncelleştirme

Bu görevde, **Web. config** dosyasına BIR ASP.net URL yeniden yazma kuralı ekleyerek Azure Blob depolama alanına (Web uygulamasında bulunan görüntü yerine) yüklenen görüntüyü kullanmak Için **geektest** çözümünü yapılandıracaksınız.

1. Visual Studio 'da, **Geektest** projesi içindeki **Web. config** dosyasını açın ve **&lt;System. webserver&gt;** öğesini bulun.
2. Bir URL yeniden yazma kuralı eklemek için aşağıdaki kodu ekleyin ve yer tutucuyu depolama hesabınızın adıyla güncelleyerek.

    (Kod parçacığı- *Websitesinproduction-EX4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL yeniden yazma, gelen bir web isteğini kesintiye uğratan ve isteği farklı bir kaynağa yönlendirmeye yönelik bir işlemdir. URL yeniden yazma kuralları yeniden yazma motoruna bir isteğin yeniden yönlendirilmesi gerektiğinde ve nereye yönlendirilmeleri gerektiğini söyler. Yeniden yazma kuralı iki dizeden oluşur: istenen URL 'de (genellikle normal ifadeler kullanılarak) aranacak model ve bulunursa, deseninin yerini alacak dize. Daha fazla bilgi için bkz. [ASP.net Içinde URL yeniden yazma](https://msdn.microsoft.com/library/ms972974.aspx).
3. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.
4. Güncelleştirilmiş uygulamayı Azure App Service dağıtmak için yeni bir **Git Bash** konsolu açın.
5. Değişiklikleri Azure 'a göndermek için aşağıdaki komutları yürütün. *[-APPLICATION-Path]* yer tutucusunu **geektest** çözümünün yoluyla güncelleştirin. Sizden dağıtım parolanızı girmeniz istenir.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Güncelleştirme Azure 'a dağıtılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *Güncelleştirme Azure 'a dağıtılıyor*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>Görev 4 – doğrulama

Bu görevde, **Geek test** uygulamasına göz atabilmeniz Için **Internet Explorer** 'ı kullanacaksınız ve görüntülerin URL yeniden yazma kuralının çalışıp çalışmadığını ve **Azure Blob depolamada**barındırılan görüntüye yönlendirildiğini kontrol edersiniz.

1. Internet Explorer 'ı açın ve Web uygulamanıza gidin (örn. `http://<your-web-site>.azurewebsites.net`). Önceden oluşturulan kimlik bilgilerini kullanarak oturum açın.

    ![Görüntüyle birlikte Geek test Web uygulamasını gösterme](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Görüntüyle birlikte Geek test Web uygulamasını gösterme")

    *Görüntüyle birlikte Geek test Web uygulamasını gösterme*
2. Geliştirici araçlarını başlatmak için **F12** tuşuna basın, **ağ** sekmesini seçin ve kaydı başlatın.

    ![Ağ kaydı başlatılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Ağ kaydı başlatılıyor")

    *Ağ kaydı başlatılıyor*
3. Web sayfasını yenilemek için **CTRL + F5** tuşlarına basın.
4. Sayfa yükleme tamamlandıktan sonra, http **301** sonucuyla **/IMG/logo-Big.png** URL 'si için BIR http isteği ve http **200** sonucuyla birlikte `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` URL 'si için bir istek görmeniz gerekir.

    ![URL yeniden yönlendirmesi doğrulanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Geliştirme araçlarındaki yeniden yönlendirmeyi gösterme")

    *URL yeniden yönlendirmesi doğrulanıyor*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>Alıştırma 5: Web Apps için otomatik ölçeklendirmeyi kullanma

> [!NOTE]
> Bu alıştırma isteğe bağlıdır, çünkü yalnızca **Visual Studio 2013 Ultimate Edition**Için kullanılabilen Web yükü &amp; performans testi için destek gerektirir. Belirli Visual Studio 2013 özellikleri hakkında daha fazla bilgi için, sürümleri [burada](https://www.microsoft.com/visualstudio/eng/products/compare)karşılaştırın.

**Azure App Service Web Apps** , **Standart modda**çalışan Web uygulamaları için otomatik ölçeklendirme özelliğini sağlar. Otomatik ölçeklendirme, Azure 'un yük 'e bağlı olarak Web uygulamanızın örnek sayısını otomatik olarak ölçeklendirmesine imkan tanır. Otomatik ölçeklendirme etkinleştirildiğinde Azure, Web uygulamanızın CPU 'sunu her beş dakikada bir denetler ve bu noktada gerektiğinde örnekler ekler. CPU kullanımı düşükse, Azure, Web uygulamanızın performansının düşürülmemesini sağlamak için örnekleri iki saatte bir daha kaldırır.

Bu alıştırmada, **Geek test** Web uygulaması Için **Otomatik ölçeklendirme** özelliğini yapılandırmak için gerekli olan adımlara gidecaksınız. Uygulama üzerinde bir örnek yükseltmesi tetikleyecek kadar CPU yükü oluşturmak için bir Visual Studio yük testi çalıştırarak bu özelliği doğrulayacaksınız.

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>Görev 1 – CPU ölçüsüne göre otomatik ölçeklendirmeyi yapılandırma

Bu görevde, alıştırma 2 ' de oluşturduğunuz Web uygulamasına yönelik otomatik ölçeklendirme özelliğini etkinleştirmek için Azure yönetim portalını kullanacaksınız.

1. [Azure yönetim portalı](https://manage.windowsazure.com/)' nda **Web siteleri** ' ni seçin ve alıştırma 2 ' de oluşturduğunuz Web uygulamasına tıklayın.
2. **Ölçek** sayfasına gidin. **Kapasite** bölümünde, **ölçüm için ölçek yapılandırmasına göre** **CPU** ' yı seçin.

    > [!NOTE]
    > CPU 'ya göre ölçeklendirilirken, Azure, CPU kullanımı değişirse uygulamanın kullandığı örneklerin sayısını dinamik olarak ayarlar.

    ![CPU 'ya göre ölçeklendirmeye seçme](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Otomatik ölçeklendirme için CPU ölçüsünü seçme")

    *CPU 'ya göre ölçeklendirmeye seçme*
3. **Hedef CPU** yapılandırmasını **20**-yüzde **40** olarak değiştirin.

    > [!NOTE]
    > Bu Aralık, Web uygulamanız için Ortalama CPU kullanımını temsil eder. Azure, Web uygulamanızı bu aralıkta tutmak için örnekler ekler veya kaldırır. Ölçeklendirme için kullanılan minimum ve maksimum örnek sayısı **örnek sayısı** yapılandırmasında belirtilmiştir. Azure hiçbir şekilde bu sınırın üzerinde veya ötesine geçmeyecektir.
    >
    > Varsayılan **hedef CPU** değerleri yalnızca bu laboratuvarın amaçları doğrultusunda değiştirilir. CPU aralığını küçük değerlerle yapılandırarak, uygulamaya bir orta yük yerleştirildiğinde otomatik ölçeklendirmeyi tetikleme olasılığını artırırsınız.

    ![Hedef CPU 'YU 20 ila %40 arasında olacak şekilde değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Hedef CPU 'YU 20 ila %40 arasında olacak şekilde değiştirme")

    *Hedef CPU 'YU 20 ila %40 arasında olacak şekilde değiştirme*
4. Değişiklikleri kaydetmek için komut çubuğunda **Kaydet** ' e tıklayın.

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>Görev 2 – Visual Studio ile yük testi

**Otomatik ölçeklendirme** yapılandırıldıktan sonra, Web UYGULAMANıZDA bazı CPU yükü oluşturmak Için Visual Studio 'Da bir **Web performansı ve yük testi projesi** oluşturacaksınız.

1. **Visual Studio Ultimate 2013** açın ve dosya ' yı seçin **| Yeni | Proje..** . Yeni bir çözüm başlatmak için.

    ![Yeni bir proje oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Yeni proje oluşturma")

    *Yeni bir proje oluşturma*
2. **Yeni proje** iletişim kutusunda, Web performansı ' nı seçin ve görsel  **C# ' ün altında yük testi projesi | Test** sekmesi. **.NET Framework 4,5** ' nin seçildiğinden emin olun, projeyi *webandloadtestproject*olarak adlandırın, bir **konum** seçin ve **Tamam**' a tıklayın.

    ![Yeni bir Web ve yük testi projesi oluşturma](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Yeni bir Web ve yük testi projesi oluşturma")

    *Yeni bir Web ve yük testi projesi oluşturma*
3. **WebTest1. webtest** içinde **WebTest1** düğümüne sağ tıklayıp **istek ekle**' ye tıklayın.

    ![WebTest1 'e istek ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "WebTest1 'e istek ekleme")

    *WebTest1 'e istek ekleme*
4. Yeni istek düğümünün **Özellikler** penceresinde **URL** özelliğini Web uygulamanızın URL 'sini işaret etmek üzere güncelleştirin (ör. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ).

    ![URL özelliğini değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "URL özelliğini değiştirme")

    *URL özelliğini değiştirme*
5. **WebTest1. webtest** penceresinde, **WebTest1** öğesine sağ tıklayın ve **döngü Ekle...** öğesine tıklayın.

    ![WebTest1 'e döngü ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "WebTest1 'e döngü ekleme")

    *WebTest1 'e döngü ekleme*
6. **Koşullu kural ve Döngülenecek öğe Ekle** iletişim kutusunda, **for döngüsü** kuralını seçin ve aşağıdaki özellikleri değiştirin.

   1. **Sonlandırma değeri:** 1000
   2. **Bağlam parametresi adı:** İden
   3. **Artış değeri:** 1

      ![For döngüsü kuralını seçme ve özellikleri güncelleştirme](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For döngüsü kuralını seçme ve özellikleri güncelleştirme")

      *For döngüsü kuralını seçme ve özellikleri güncelleştirme*
7. **Döngüdeki öğeler** bölümünde, döngünün ilk ve son öğesi olarak daha önce oluşturduğunuz isteği seçin. Devam etmek için **Tamam** 'a tıklayın.

    ![Döngünün ilk ve son öğelerini seçme](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Döngünün ilk ve son öğelerini seçme")

    *Döngünün ilk ve son öğelerini seçme*
8. **Çözüm Gezgini**, **webandloadtestproject** projesine sağ tıklayın, **Ekle** menüsünü ve **Yük testi seç...** öğesini seçin.

    ![WebAndLoadTestProject projesine yük testi ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject projesine yük testi ekleme")

    *WebAndLoadTestProject projesine yük testi ekleme*
9. **Yeni Yük Testi Sihirbazı** Iletişim kutusunda **İleri**' ye tıklayın.

    ![Yeni Yük Testi Sihirbazı](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "Yeni Yük Testi Sihirbazı")

    *Yeni Yük Testi Sihirbazı*
10. **Senaryo** sayfasında **düşünme süreleri kullanmayın** ' ı seçin ve **İleri**' ye tıklayın.

    ![Düşünme sürelerini kullanmayı seçme](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Düşünme sürelerini kullanmayı seçme")

    *Düşünme sürelerini kullanmayı seçme*
11. **Yük kalıbı** sayfasında, **sabit yükleme** seçeneğinin seçildiğinden emin olun. **Kullanıcı sayısı** ayarını **250** Kullanıcı olarak değiştirin ve **İleri**' ye tıklayın.

    ![Kullanıcı sayısını 250 olarak değiştirme](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Kullanıcı sayısını 250 olarak değiştirme")

    *Kullanıcı sayısını 250 olarak değiştirme*
12. **Test karışımı modeli** sayfasında, **sıralı test sırasına göre** ' yi seçin ve **İleri**' ye tıklayın.

    ![Test karışımı modelini seçme](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Test karışımı modelini seçme")

    *Test karışımı modelini seçme*
13. **Test karışımı modeli** sayfasında, karışıma bir test eklemek için **Ekle...** ' ye tıklayın.

    ![Test karışımına test ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Test karışımına test ekleme")

    *Test karışımına test ekleme*
14. **Testleri Ekle** iletişim kutusunda, **Seçili testler** listesine test eklemek için **WebTest1** öğesine çift tıklayın. Devam etmek için **Tamam** 'a tıklayın.

    ![WebTest1 testi ekleme](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "WebTest1 testi ekleme")

    *WebTest1 testi ekleme*
15. **Test karışımı** sayfasına geri döndüğünüzde **İleri**' ye tıklayın.

    ![Test karışımı sayfası Tamamlanıyor](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Test karışımı sayfası Tamamlanıyor")

    *Test karışımı sayfası Tamamlanıyor*
16. **Ağ karışımı** sayfasında, **İleri**' ye tıklayın.

    ![Ağ karışımı sayfasında ileri 'ye tıklama](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Ağ karışımı sayfasında ileri 'ye tıklama")

    *Ağ karışımı sayfasında ileri 'ye tıklama*
17. **Tarayıcı karışımı** sayfasında, tarayıcı türü olarak **Internet Explorer 10,0** ' ı seçin ve **İleri**' ye tıklayın.

    ![Tarayıcı türünü seçme](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Tarayıcı türünü seçme")

    *Tarayıcı türünü seçme*
18. **Sayaç kümeleri** sayfasında, **İleri**' ye tıklayın.

    ![Sayaç kümeleri sayfasında Ileri 'ye tıklama](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Sayaç kümeleri sayfasında Ileri 'ye tıklama")

    *Sayaç kümeleri sayfasında Ileri 'ye tıklama*
19. **Ayarları Çalıştır** sayfasında, **Yük testi süresini** **5 dakikaya** ayarlayın ve **son**' a tıklayın.

    ![Yük testi süresini 5 dakikaya ayarlama](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Yük testi süresini 5 dakikaya ayarlama")

    *Yük testi süresini 5 dakikaya ayarlama*
20. **Çözüm Gezgini**, test ayarlarını araştırmak için **yerel. Settings** dosyasına çift tıklayın. Varsayılan olarak, Visual Studio Testleri çalıştırmak için yerel bilgisayarınızı kullanır.

    > [!NOTE]
    > Alternatif olarak, test projenizi **Azure test Plans**kullanarak bulutta yük testlerini çalıştıracak şekilde yapılandırabilirsiniz. Azure Test Plans, daha gerçekçi bir yükü taklit eden, CPU kapasitesi, kullanılabilir bellek ve ağ bant genişliği gibi yerel ortam kısıtlamalarını önyükleyen bulut tabanlı bir yük testi hizmeti sağlar. Yük testlerini çalıştırmak için Azure Test Plans kullanma hakkında daha fazla bilgi için bkz. [Yük testi senaryoları](/azure/devops/test/load-test/overview?view=vsts).

    ![Test ayarları](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>Görev 3 – otomatik ölçeklendirme doğrulaması

Şimdi, önceki görevde oluşturduğunuz yük testini yürütülecektir ve Web uygulamanızın yük altında nasıl davrandığını görürsünüz.

1. **Çözüm Gezgini**, yük testini açmak için **LoadTest1. LoadTest** öğesine çift tıklayın.

    ![LoadTest1. LoadTest açılıyor](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "LoadTest1. LoadTest açılıyor")

    *LoadTest1. LoadTest açılıyor*
2. **LoadTest1. LoadTest** penceresinde, yük testini çalıştırmak için araç kutusundaki ilk düğmesine tıklayın.

    ![Yük testini çalıştırma](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Yük testini çalıştırma")

    *Yük testini çalıştırma*
3. Yük testi tamamlanana kadar bekleyin.

    > [!NOTE]
    > Yük testi, istekleri Web uygulamasına aynı anda gönderen birden çok kullanıcıyı benzetir. Test çalışırken, herhangi bir hata, uyarı veya yük testi çalıştırla ilgili diğer bilgileri algılamak için kullanılabilir sayaçları izleyebilirsiniz.

    ![Yük testi çalışıyor](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Yük testi tamamlanana kadar bekleniyor")

    *Yük testi çalışıyor*
4. Test tamamlandıktan sonra, yönetim portalına geri dönün ve Web uygulamanızın **Ölçek** sayfasına gidin. **Kapasite** bölümünde, grafikte yeni bir örneğin otomatik olarak dağıtıldığını görmeniz gerekir.

    ![Yeni örnek otomatik olarak dağıtıldı](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *Yeni örnek otomatik olarak dağıtıldı*

    > [!NOTE]
    > Değişikliklerin grafikte görünmesi birkaç dakika sürebilir (sayfayı yenilemek için **CTRL + F5** tuşlarına basın). Herhangi bir değişiklik görmüyorsanız, aşağıdakileri deneyebilirsiniz:
    >
    > - Yük testinin süresini artırın (ör. **10 dakika**)
    > - Web uygulamanızın otomatik ölçeklendirme yapılandırmasındaki **hedef CPU** aralığının maksimum ve en düşük değerlerini azaltın
    > - Yük testini bulutta **Azure test Plans**ile çalıştırın. [Buradan](/azure/devops/test/load-test/index?view=vsts) daha fazla bilgi

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı laboratuvarda, uygulamanızı ayarlamayı ve Azure 'da üretim Web uygulamalarına dağıtmayı öğrendiniz. **Entity Framework Code First Migrations**kullanarak veritabanlarınızı algılayıp güncelleştirerek ve sonra **Git** kullanarak sitenizin yeni sürümlerini dağıtarak ve sitenizin en son kararlı sürümüne geri dönme gerçekleştirerek çalışmaya devam edersiniz. Ayrıca, statik içeriğinizi bir blob kapsayıcısına taşımak için depolamayı kullanarak uygulamanızı nasıl ölçeklendirebileceğinizi öğrendiniz.
