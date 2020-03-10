---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: "ASP.NET Identity: MySQL Storage 'ı bir EntityFramework MySQL sağlayıcısıyla kullanma (C#)-ASP.NET 4. x"
author: maumar
description: Bu öğreticide, ASP.NET Identity için varsayılan veri depolama mekanizmanın (SQL istemci sağlayıcısı) MySQL provid... ile nasıl değiştirileceği gösterilmektedir.
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584009"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity: Bir EntityFramework MySQL Sağlayıcısı ile MySQL Depolama Kullanma (C#)

by [Maurycy Markowski](https://github.com/maumar), [Raquel Soares de almete](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)

> Bu öğreticide, [**ASP.NET Identity**](introduction-to-aspnet-identity.md) için varsayılan veri depolama mekanizmasını bir MySQL sağlayıcısı Ile EntityFramework (SQL istemci sağlayıcısı) ile nasıl değiştireceğiniz gösterilir.

Bu öğreticide aşağıdaki konular ele alınacaktır:

- Azure 'da MySQL veritabanı oluşturma
- Visual Studio 2013 MVC şablonu kullanarak MVC uygulaması oluşturma
- EntityFramework 'Ü bir MySQL veritabanı sağlayıcısıyla çalışacak şekilde yapılandırma
- Sonuçları doğrulamak için uygulamayı çalıştırma

Bu öğreticinin sonunda, Azure 'da barındırılan bir MySQL veritabanı kullanan ASP.NET Identity deposuna sahip bir MVC uygulamanız olacaktır.

## <a name="creating-a-mysql-database-instance-on-azure"></a>Azure 'da MySQL veritabanı örneği oluşturma

1. [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)’da oturum açın.
2. Sayfanın alt kısmındaki **Yeni** ' ye tıklayın ve ardından **Mağaza**' ı seçin:

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. **Seçim ve eklenti** sihirbazında **ClearDB MySQL veritabanı**' nı seçin ve ardından çerçevenin altındaki **İleri** okuna tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. Varsayılan **ücretsiz** planı koruyun, **adı** **ıdentitymysqldatabase**olarak değiştirin, size en yakın bölgeyi seçin ve ardından çerçevenin altındaki **İleri** okuna tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. Veritabanı oluşturma işleminin tamamlanabilmesi için **satın alma** onay işaretine tıklayın.

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. Veritabanınız oluşturulduktan sonra yönetim portalındaki **Eklentiler sekmesinden bu** dosyayı yönetebilirsiniz. Veritabanınızın bağlantı bilgilerini almak için sayfanın altındaki **bağlantı bilgileri** ' ne tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. Bağlantı dizesini, **CONNECTIONSTRING** alanına tıklayarak Kopyala düğmesine tıklayıp kaydedin; Bu bilgileri, MVC uygulamanız için bu öğreticide daha sonra kullanacaksınız:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>MVC uygulama projesi oluşturma

Öğreticinin bu bölümündeki adımları tamamlayabilmeniz için öncelikle Web veya [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) ' i yüklemeniz gerekir. Visual Studio yüklendikten sonra, yeni bir MVC uygulama projesi oluşturmak için aşağıdaki adımları kullanın:

1. Visual Studio 2103 ' i açın.
2. **Başlangıç** sayfasından **Yeni proje** ' ye tıklayın veya **Dosya** menüsünü ve ardından **Yeni proje**' ye tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. **Yeni proje** iletişim kutusu görüntülendiğinde, şablonlar listesinde **görsel C#**  ' i genişletin, **Web**' e tıklayın ve **ASP.NET Web uygulaması**' nı seçin. Projenizi **ıdentitymysqldemo** olarak adlandırın ve ardından **Tamam**' a tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. **Yeni ASP.NET projesi** iletişim kutusunda varsayılan seçeneklerle **MVC** template' i seçin; Bu, **bireysel kullanıcı hesaplarını** kimlik doğrulama yöntemi olarak yapılandırır. **Tamam 'a**tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>EntityFramework 'Ü bir MySQL veritabanıyla çalışacak şekilde yapılandırma

### <a name="update-the-entity-framework-assembly-for-your-project"></a>Projeniz için Entity Framework derlemeyi güncelleştirme

Visual Studio 2013 şablondan oluşturulan MVC uygulaması [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) paketine yönelik bir başvuru içerir, ancak bu derleme için önemli performans iyileştirmeleri içeren sürümünden bu yana güncelleştirmeler yapılmıştır. Uygulamanızda bu en son güncelleştirmeleri kullanmak için aşağıdaki adımları kullanın.

1. Visual Studio 'da MVC projenizi açın.
2. **Araçlar**' a ve ardından **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. **Paket Yöneticisi konsolu** , Visual Studio 'nun alt bölümünde görüntülenir. &quot;**Update-Package EntityFramework**&quot; yazın ve ENTER tuşuna basın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>EntityFramework için MySQL sağlayıcısını yükler

EntityFramework 'Ün MySQL veritabanına bağlanabilmesi için bir MySQL sağlayıcısı yüklemeniz gerekir. Bunu yapmak için, **Paket Yöneticisi konsolunu** açın ve **Install-Package MySQL. Data. Entity-pre**&quot;&quot;yazın ve ardından ENTER tuşuna basın.

> [!NOTE]
> Bu, derlemenin yayın öncesi sürümüdür ve bu nedenle hata içerebilir. Üretimde sağlayıcının yayın öncesi bir sürümünü kullanmamalısınız.

[Genişletmek için aşağıdaki resme tıklayın.]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>Uygulamanızın Web. config dosyasında proje yapılandırması değişiklikleri yapılıyor

Bu bölümde, yeni yüklediğiniz MySQL sağlayıcısını kullanmak için Entity Framework yapılandıracaksınız, MySQL sağlayıcı fabrikasını kaydedebilir ve Bağlantı dizenizi Azure 'dan eklersiniz.

> [!NOTE]
> Aşağıdaki örneklerde MySql. Data. dll için belirli bir derleme sürümü bulunur. Derleme sürümü değişirse, uygun yapılandırma ayarlarını doğru sürümle değiştirmeniz gerekir.

1. Projeniz için Web. config dosyasını Visual Studio 2013 açın.
2. Entity Framework için varsayılan veritabanı sağlayıcısını ve fabrikası tanımlayan aşağıdaki yapılandırma ayarlarını bulun:

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. Bu yapılandırma ayarlarını aşağıdaki ile değiştirin ve bu, Entity Framework MySQL sağlayıcısını kullanacak şekilde yapılandırır:

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. &lt;connectionStrings&gt; bölümünü bulun ve Azure üzerinde barındırılan MySQL veritabanınızın bağlantı dizesini tanımlayacak aşağıdaki kodla değiştirin (providerName değeri de orijinalden değiştirildiğini unutmayın):

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>Özel MigrationHistory bağlamı ekleniyor

Entity Framework Code First, model değişikliklerini izlemek ve veritabanı şeması ile kavramsal şema arasındaki tutarlılığı sağlamak için bir **Migrationhistory** tablosu kullanır. Ancak, birincil anahtar çok büyük olduğundan bu tablo MySQL için varsayılan olarak çalışmaz. Bu durumu gidermek için, bu tablo için anahtar boyutunu küçültmenize gerek duyarsınız. Bunu yapmak için aşağıdaki adımları kullanın:

1. Bu tablo için şema bilgileri, başka bir **DbContext**olarak değiştirilebilen bir, bir bir bir bir bir bir bir bir bir **bağlam**içinde yakalanır. Bunu yapmak için projeye **MySqlHistoryContext.cs** adlı yeni bir sınıf dosyası ekleyin ve içeriğini şu kodla değiştirin:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. Daha sonra, Entity Framework varsayılan bir yerine değiştirilen bir değiştirme **bağlamını**kullanacak şekilde yapılandırmanız gerekecektir. Bu, kod tabanlı yapılandırma özelliklerinden yararlanarak yapılabilir. Bunu yapmak için, **MySqlConfiguration.cs** adlı yeni sınıf dosyasını projenize ekleyin ve içeriğini ile değiştirin:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>ApplicationDbContext için özel bir EntityFramework başlatıcısı oluşturma

Bu öğreticide tanıtılan MySQL sağlayıcısı şu anda Entity Framework geçişleri desteklemediğinden, veritabanına bağlanmak için model başlatıcılarının kullanılması gerekir. Bu öğretici Azure üzerinde bir MySQL örneği kullandığından, özel bir Entity Framework başlatıcısı oluşturmanız gerekir.

> [!NOTE]
> Azure 'da bir SQL Server örneğine bağlanıyorsanız veya şirket içinde barındırılan bir veritabanı kullanıyorsanız bu adım gerekli değildir.

MySQL için özel bir Entity Framework başlatıcısı oluşturmak için aşağıdaki adımları kullanın:

1. Projeye **MySqlInitializer.cs** adlı yeni bir sınıf dosyası ekleyin ve içeriğini şu kodla değiştirin:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. Projeniz için **modeller** dizininde bulunan **IdentityModels.cs** dosyasını açın ve içeriğini aşağıdakiler ile değiştirin:

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>Uygulamayı çalıştırma ve veritabanını doğrulama

Yukarıdaki bölümlerde bulunan adımları tamamladıktan sonra, veritabanınızı test etmelisiniz. Bunu yapmak için aşağıdaki adımları kullanın:

1. Web uygulamasını derlemek ve çalıştırmak için **CTRL + F5** tuşlarına basın.
2. Sayfanın üst kısmındaki **Kaydet** sekmesine tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. Yeni bir Kullanıcı adı ve parola girin ve ardından **Kaydet**' e tıklayın:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. Bu noktada, ASP.NET Identity tabloları MySQL veritabanında oluşturulur ve Kullanıcı kaydedilir ve uygulamaya kaydedilir:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>Verileri doğrulamak için MySQL bir aracı yükleniyor

1. MySQL [İndirmeleri sayfasından](http://dev.mysql.com/downloads/windows/installer/) **MySQL çalışma ekranı** aracını yükler
2. Yükleme Sihirbazı: **Özellik seçimi** sekmesinde, **uygulamalar** bölümünde **MySQL çalışma ekranı** ' nı seçin.
3. Uygulamayı başlatın ve Bu öğreticinin başında oluşturduğunuz Azure MySQL veritabanındaki bağlantı dizesi verilerini kullanarak yeni bir bağlantı ekleyin.
4. Bağlantıyı kurduktan sonra, **ıdentitymysqldatabase** üzerinde oluşturulan **ASP.NET Identity** tablolarını inceleyin.
5. Aşağıdaki görüntüde gösterildiği gibi, gerekli tüm ASP.NET Identity tablolarının oluşturulduğunu görürsünüz:

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. Yeni kullanıcıları kaydettiğinizde girişleri denetlemek üzere örnek için **aspnetusers** tablosunu inceleyin.

   [Genişletmek için aşağıdaki görüntüye tıklayın. ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
