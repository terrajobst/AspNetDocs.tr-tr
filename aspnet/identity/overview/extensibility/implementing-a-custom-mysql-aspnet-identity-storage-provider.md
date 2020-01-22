---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: Özel MySQL ASP.NET Identity depolama sağlayıcısı uygulama-ASP.NET 4. x
author: raquelsa
description: ASP.NET Identity, kendi depolama sağlayıcınızı oluşturmanızı ve appli 'ı yeniden çalıştırmadan uygulamanıza eklemenizi sağlayan genişletilebilir bir sistemdir...
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519134"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>Özel MySQL ASP.NET Identity Depolama Sağlayıcısı Uygulama

[Raquel Soares de Almete](https://github.com/raquelsa), [Susize Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity, kendi depolama sağlayıcınızı oluşturmanızı ve uygulamayı yeniden çalıştırmadan uygulamanıza takmanızı sağlayan genişletilebilir bir sistemdir. Bu konu, ASP.NET Identity için bir MySQL depolama sağlayıcısı oluşturmayı açıklar. Özel depolama sağlayıcıları oluşturmaya genel bakış için bkz. [ASP.NET Identity Için özel depolama sağlayıcılarına genel bakış](overview-of-custom-storage-providers-for-aspnet-identity.md).
> 
> Bu öğreticiyi tamamlayabilmeniz için güncelleştirme 2 ile Visual Studio 2013 sahip olmanız gerekir.
> 
> Bu öğretici şu şekilde olur:
> 
> - Azure 'da MySQL veritabanı örneği oluşturmayı gösterir.
> - Azure üzerinde tablo oluşturmak ve uzak veritabanınızı yönetmek için MySQL istemci aracının (MySQL çalışma ekranı) nasıl kullanılacağını gösterir.
> - Varsayılan ASP.NET Identity depolama uygulamasının bir MVC uygulama projesindeki özel uygulamamız ile nasıl değiştirileceğini gösterir.
> 
> Bu öğretici, ilk olarak Raquel Soares ve almede Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) tarafından yazılmıştır. Örnek proje, Susize Joshi tarafından 2,0 kimliği için güncelleştirildi. Konu, Tom FitzMacken kimlik 2,0 kimliği için güncelleştirildi.

## <a name="download-completed-project"></a>Tamamlanmış projeyi indir

Bu öğreticinin sonunda, Azure 'da barındırılan bir MySQL veritabanıyla çalışan ASP.NET Identity bir MVC uygulama projesine sahip olursunuz.

Tamamlanan MySQL depolama sağlayıcısını [Aspnet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)adresinden indirebilirsiniz.

## <a name="the-steps-you-will-perform"></a>Gerçekleştirilecek adımlar

Bu öğreticide şunları yapmanız gerekir:

1. Azure 'da MySQL veritabanı oluşturma
2. MySQL 'de ASP.NET Identity tabloları oluşturma
3. MVC uygulaması oluşturma ve MySQL sağlayıcısını kullanmak için yapılandırma
4. Uygulamayı çalıştırma

Bu konu, ASP.NET Identity mimarisini ve bir müşteri depolama sağlayıcısını uygularken yapmanız gereken kararları kapsamaz. Bu bilgi için bkz. [ASP.NET Identity Için özel depolama sağlayıcılarına genel bakış](overview-of-custom-storage-providers-for-aspnet-identity.md).

## <a name="review-mysql-storage-provider-classes"></a>MySQL depolama sağlayıcısı sınıflarını gözden geçirin

MySQL depolama sağlayıcısını oluşturmaya yönelik adımlara geçmeden önce, depolama sağlayıcısını oluşturan sınıflara göz atalım. Kullanıcıları ve rolleri yönetmek için uygulamadan çağrılan veritabanı işlemlerini ve sınıflarını yöneten sınıflara ihtiyaç duyarsınız.

### <a name="storage-classes"></a>Depolama sınıfları

- [Identityuser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -kullanıcının özelliklerini içerir.
- [UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -kullanıcıları ekleme, güncelleştirme veya alma işlemlerini içerir.
- [Identityrole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -rollerin özelliklerini içerir.
- [Rolestore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -rolleri ekleme, silme, güncelleştirme ve alma işlemlerini içerir.

### <a name="data-access-layer-classes"></a>Veri erişim katmanı sınıfları

Bu örnekte, veri erişim katmanı sınıfları tablolarla çalışmak için SQL deyimlerini içerir; Ancak, kodunuzda Entity Framework veya Nhazırda bekleme gibi nesne ilişkisel eşleme (ORM) kullanmak isteyebilirsiniz. Özellikle, uygulamanız, yavaş yükleme ve nesne önbelleği içeren bir ORM olmadan düşük performansa sahip olabilir. Daha fazla bilgi için, [Entity Framework olmadan ASP.NET Identity 2,0](https://aspnetidentity.codeplex.com/discussions/561828) ' ya bakın.

- [Mysqldatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -MySQL veritabanı bağlantısını ve veritabanı işlemlerini gerçekleştirmeye yönelik yöntemleri içerir. UserStore ve RoleStore, her ikisi de bu sınıfın örneğiyle birlikte oluşturulur.
- [Roletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -rolleri depolayan tablo için veritabanı işlemlerini içerir.
- [Userclaimstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -Kullanıcı taleplerini depolayan tablo için veritabanı işlemlerini içerir.
- [Userloginstable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -Kullanıcı oturum açma bilgilerini depolayan tablo için veritabanı işlemlerini içerir.
- [Userroletable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -hangi kullanıcıların hangi rollere atandığını depolayan tablo için veritabanı işlemlerini içerir.
- [Usertable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -kullanıcıları depolayan tablo için veritabanı işlemlerini içerir.

## <a name="create-a-mysql-database-instance-on-azure"></a>Azure 'da MySQL veritabanı örneği oluşturma

1. [Azure Portal](https://manage.windowsazure.com/)’da oturum açın.
2. Sayfanın alt kısmındaki **+ Yeni** ' ye tıklayın ve ardından **Mağaza**' yı seçin.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. **Seçme ve eklenti** sihirbazında **ClearDB MySQL veritabanı** ' nı seçin ve iletişim kutusunun sağ alt köşesindeki sonraki oka tıklayın.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. Varsayılan **ücretsiz** planı koruyun ve **adı** **ıdentitymysqldatabase**olarak değiştirin. En yakın bölgeyi seçin ve ardından ileri okuna tıklayın.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. Veritabanı oluşturma işleminin tamamlanabilmesi için onay işaretine tıklayın.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. Veritabanınız oluşturulduktan sonra yönetim portalındaki **Eklentiler sekmesinden bu** dosyayı yönetebilirsiniz.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. Sayfanın alt kısmındaki **bağlantı bilgileri** ' ne tıklayarak veritabanı bağlantı bilgilerini alabilirsiniz.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. Kopyala düğmesine tıklayarak bağlantı dizesini kopyalayın ve daha sonra MVC Uygulamanızda kullanabilmek için kaydedin.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>MySQL veritabanında ASP.NET Identity tabloları oluşturma

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>MySQL veritabanını bağlamak ve yönetmek için MySQL çalışma ekranı aracını yükler

1. MySQL [İndirmeleri sayfasından](http://dev.mysql.com/downloads/windows/installer/) **MySQL çalışma ekranı** aracını yükler
2. Uygulamayı başlatın ve yeni bir bağlantı eklemek için **Mysqlconnections +** düğmesine tıklayın. Bu öğreticide daha önce oluşturduğunuz Azure MySQL veritabanından kopyaladığınız bağlantı dizesi verilerini kullanın.
3. Bağlantıyı kurduktan sonra yeni bir **sorgu** sekmesi açın; [Mysqlidentity. SQL](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) dosyasındaki komutları sorguya yapıştırın ve veritabanı tabloları oluşturmak için yürütün.
4. Artık, aşağıda gösterildiği gibi Azure üzerinde barındırılan bir MySQL veritabanında oluşturulan tüm ASP.NET Identity gerekli tabloları vardır.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>Şablondan MVC uygulama projesi oluşturma ve MySQL sağlayıcısını kullanacak şekilde yapılandırma

Gerekirse, [Web için Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) ' i veya güncelleştirme 2 ' yi [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) .

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>GitHub 'dan ASP. NET. Identity. MySQL projesini indirin

1. [Aspnet. Identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)KONUMUNDAKI depo URL 'sine gidin.
2. Kaynak kodunu indirin.
3. . Zip dosyasını yerel bir klasöre ayıklayın.
4. AspNet. Identity. MySQL çözümünü açın ve oluşturun.

### <a name="create-a-new-mvc-application-project-from-template"></a>Şablondan yeni bir MVC uygulama projesi oluştur

1. **Aspnet. Identity. MySQL** çözümüne sağ tıklayın ve **Yeni proje** **ekleyin**
2. **Yeni Proje Ekle** iletişim kutusunda sol taraftaki **görsel C#**  **' i seçin ve ardından** **ASP.NET Web uygulaması**' nı seçin. Projeyi **ıdentitymysqldemo**; olarak adlandırın ardından Tamam ' a tıklayın.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. **Yeni ASP.NET projesi** iletişim kutusunda, varsayılan seçeneklerle (kimlik doğrulama yöntemi olarak **bireysel kullanıcı hesapları** da dahIl olmak üzere) MVC şablonunu seçin ve **Tamam**' a tıklayın.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. Çözüm Gezgini, ıdentitymysqldemo projenize sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin. Arama metin kutusu iletişim kutusunda **Identity. EntityFramework**yazın. Sonuçlar listesinde bu paketi seçin ve **Kaldır**' a tıklayın. EntityFramework bağımlılık paketini kaldırmanız istenecektir. Bu uygulamada artık bu paketin olmadığı sürece Evet ' e tıklayın.
5. Identitymysqldemo projesine sağ tıklayın, **Ekle**, **başvuru, çözüm, projeler** ' i seçin, ASPNET. Identity. MySQL projesini seçin ve **Tamam**' a tıklayın.
6. Identitymysqldemo projesinde, tüm başvuruları Değiştir  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   ile  
     `using AspNet.Identity.MySQL;`
7. IdentityModels.cs ' de, **Applicationdbcontext** ' i **mysqldatabase** 'dan türetebilir ve bağlantı adı ile tek bir parametre alan bir Oluşturucu ekleyin.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. IdentityConfig.cs dosyasını açın. **Applicationusermanager. Create** yönteminde, UserManager örneğini aşağıdaki kodla değiştirin:  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Web. config dosyasını açın ve DefaultConnection dizesini, vurgulanan değerleri önceki adımlarda oluşturduğunuz MySQL veritabanının bağlantı dizesiyle değiştirerek bu girdiyle değiştirin:  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>Uygulamayı çalıştırma ve MySQL DB 'ye bağlanma

1. **Identitymysqldemo** projesine sağ tıklayın ve **Başlangıç projesi olarak ayarla** ' yı seçin.
2. Uygulamayı derlemek ve çalıştırmak için **CTRL + F5** tuşlarına basın.
3. Sayfanın üst kısmındaki **Kaydet** sekmesine tıklayın.
4. Yeni bir Kullanıcı adı ve parola girin ve ardından **Kaydet**' e tıklayın.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. Yeni Kullanıcı artık kaydettirildi ve oturum açtı.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. MySQL çalışma ekranı aracına geri dönün ve **ıdentitymysqldatabase** tablosunun içeriğini inceleyin. Yeni kullanıcıları kaydettiğinizde, girişler için kullanıcılar tablosunu inceleyin.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>Sonraki Adımlar

Bu uygulamada diğer kimlik doğrulama yöntemlerinin nasıl etkinleştirileceği hakkında daha fazla bilgi için bkz. [Facebook ve Google OAuth2 Ile OpenID oturum açma ile ASP.NET MVC 5 uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).

Veritabanınızı OAuth ile tümleştirme hakkında bilgi edinmek ve kullanıcıların uygulamanıza erişimini sınırlamak için roller ayarlamayı öğrenmek için bkz. [Azure 'A üyelik, OAuth ve SQL veritabanı Ile güvenli bir ASP.NET MVC 5 uygulaması dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).
