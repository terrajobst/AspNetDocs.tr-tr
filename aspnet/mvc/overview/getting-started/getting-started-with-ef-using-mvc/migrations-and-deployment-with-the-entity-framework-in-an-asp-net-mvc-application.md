---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: "Öğretici: Bir ASP.NET MVC uygulamasında EF geçişlerini kullanma ve Azure 'a dağıtma"
author: tdykstra
description: Bu öğreticide, Code First geçişleri etkinleştirir ve uygulamayı Azure 'da buluta dağıtırsınız.
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 989dd0f0e18b338be057b9c5657586eff996d8ea
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000763"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>Öğretici: Bir ASP.NET MVC uygulamasında EF geçişlerini kullanma ve Azure 'a dağıtma

Şu ana kadar Contoso Üniversitesi örnek Web uygulaması, geliştirme bilgisayarınızda IIS Express ' de yerel olarak çalışmaktadır. Gerçek bir uygulamayı diğer kişilerin Internet üzerinden kullanmasına olanak sağlamak için, bir Web barındırma sağlayıcısına dağıtmanız gerekir. Bu öğreticide, Code First geçişleri etkinleştirir ve uygulamayı Azure 'da buluta dağıtırsınız:

- Code First Migrations etkinleştirin. Geçişler özelliği, veritabanını bırakıp yeniden oluşturmaya gerek kalmadan veritabanı şemasını güncelleştirerek veri modelini değiştirmenize ve yaptığınız değişiklikleri üretime dağıtmanıza olanak sağlar.
- Azure 'a dağıtın. Bu adım isteğe bağlıdır; projeyi dağıtmadan kalan öğreticilerle devam edebilirsiniz.

Dağıtım için kaynak denetimiyle sürekli bir tümleştirme işlemi kullanmanızı öneririz, ancak bu öğretici bu konuları kapsamaz. Daha fazla bilgi için bkz. [Azure Ile gerçek dünyada bulut uygulamaları oluşturmanın](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction) [kaynak denetimi](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control) ve [sürekli tümleştirme](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) bölümleri.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Code First geçişlerini etkinleştir
> * Uygulamayı Azure 'da dağıtma (isteğe bağlı)

## <a name="prerequisites"></a>Önkoşullar

- [Bağlantı Dayanıklılığı ve Komut Durdurma](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>Code First geçişlerini etkinleştir

Yeni bir uygulama geliştirirken, veri modeliniz sıklıkla değişir ve model her değiştiğinde veritabanıyla eşitlenmemiş olur. Veri modelini her değiştirişinizde veritabanını otomatik olarak bırakıp yeniden oluşturmak için Entity Framework yapılandırdınız. Varlık sınıfları eklediğinizde, kaldırdığınızda veya değiştirdiğinizde ya da `DbContext` sınıfınızı değiştirdiğinizde, uygulamayı bir sonraki çalıştırışınızda, otomatik olarak mevcut veritabanınızı siler, modelle eşleşen yeni bir tane oluşturur ve test verileriyle birlikte olur.

Veritabanını veri modeliyle eşitlenmiş halde tutma yöntemi, uygulamayı üretime dağıtana kadar iyi çalışır. Uygulama üretimde çalışırken, genellikle tutmak istediğiniz verileri saklar ve yeni sütun ekleme gibi her değişiklik yaptığınızda her şeyi kaybetmek istemezsiniz. [Code First Migrations](https://msdn.microsoft.com/data/jj591621) özelliği, veritabanını bırakıp yeniden oluşturmak yerine veritabanı şemasını güncelleştirmesine Code First etkinleştirerek bu sorunu çözer. Bu öğreticide, uygulamayı dağıtırsınız ve geçişleri etkinleştireceksiniz.

1. Uygulama Web. config dosyasına eklediğiniz `contexts` öğeyi açıklama ekleyerek veya silerek daha önce ayarladığınız başlatıcıyı devre dışı bırakın.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. Ayrıca, uygulama *Web. config* dosyasında, bağlantı dizesindeki veritabanının adını ContosoUniversity2 olarak değiştirin.

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    Bu değişiklik, ilk geçişin yeni bir veritabanı oluşturması için projeyi ayarlar. Bu gerekli değildir ancak daha sonra iyi bir fikir olduğunu göreceksiniz.
3. Gelen **Araçları** menüsünde **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.

1. `PM>` İsteminde aşağıdaki komutları girin:

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    Komut, contosouniversity projesinde bir *geçişler* klasörü oluşturur ve bu klasöre geçişleri yapılandırmak için düzenleyebileceğiniz bir Configuration.cs dosyası koyar. `enable-migrations`

    (Yukarıdaki adımı kaçırdıysanız, veritabanı adını değiştirmenizi yönlendirirsiniz, geçişler var olan veritabanını bulur ve `add-migration` komutu otomatik olarak kullanacaktır. Bu sorun, veritabanını dağıtmadan önce geçiş kodunun bir testini çalıştırmayacağınızı gösterir. Daha sonra `update-database` komutu çalıştırdığınızda hiçbir şey gerçekleşmeyecektir çünkü veritabanı zaten var.)

    *Contosoüniversıty\migrations\configuration.cs* dosyasını açın. Daha önce gördüğünüz Başlatıcı sınıfı gibi, `Configuration` sınıfı bir `Seed` yöntemi içerir.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    [Çekirdek](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yönteminin amacı, Code First veritabanını oluşturduktan veya güncelleştirdikten sonra test verilerini ekleme veya güncelleştirme olanağı sağlamaktır. Yöntemi, veritabanı oluşturulduğunda ve bir veri modeli değişikliğinden sonra veritabanı şeması her güncelleştirildiği zaman çağrılır.

### <a name="set-up-the-seed-method"></a>Çekirdek yöntemi ayarlama

Her veri modeli değişikliği için veritabanını bırakıp yeniden oluşturduğunuzda, test verilerini eklemek için Başlatıcı sınıfının `Seed` yöntemini kullanırsınız, çünkü her model, veritabanını değiştirdikten sonra tüm test verileri kaybedilir. Code First Migrations ile test verileri, veritabanı değişikliklerinden sonra tutulur, bu nedenle [temel](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemde test verilerinin dahil edilmesi genellikle gerekli değildir. Aslında, `Seed` yöntemi üretimde çalışacak şekilde veritabanını `Seed` üretime dağıtmak için geçişler kullanacaksanız, yöntemi test verileri eklemek istemezsiniz. Bu durumda, `Seed` yönteminin yalnızca üretimde ihtiyacınız olan verileri veritabanına eklemesini istersiniz. Örneğin, uygulama üretimde kullanılabilir hale geldiğinde veritabanının gerçek bölüm adlarını `Department` tabloya dahil etmek isteyebilirsiniz.

Bu öğreticide, dağıtım için geçişler kullanacaksınız, ancak `Seed` Yöntem test verilerini el ile çok sayıda veri eklemek zorunda kalmadan nasıl çalıştığını görmeyi kolaylaştırmak için de test verileri ekleyecektir.

1. *Configuration.cs* dosyasının içeriğini, test verilerini yeni veritabanına yükleyen aşağıdaki kodla değiştirin.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [Çekirdek](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemi, veritabanı bağlamı nesnesini bir giriş parametresi olarak alır ve yöntemdeki kod bu nesneyi veritabanına yeni varlıklar eklemek için kullanır. Her varlık türü için, kod yeni varlıkların bir koleksiyonunu oluşturur, bunları uygun [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) özelliğine ekler ve değişiklikleri veritabanına kaydeder. Burada yapılan her bir varlık grubundan sonra [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) yöntemini çağırmak gerekmez, ancak bu, kod veritabanına yazılırken bir özel durum oluşursa bir sorunun kaynağını bulmanıza yardımcı olur.

    Veri ekleyen deyimlerden bazıları, "upsert" bir işlem gerçekleştirmek için [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) yöntemini kullanır. `Seed` Yöntemi `update-database` komutu her yürüttüğünüzde çalışır, genellikle her geçişten sonra, eklemeye çalıştığınız satırlar veritabanını oluşturan ilk geçişten sonra zaten mevcut olacağı için yalnızca veri ekleyemezsiniz. "Upsert" işlemi, zaten var olan bir satır eklemeye çalışırsanız, ancak uygulamayı test ederken yapmış olduğunuz verilerde yapılan değişiklikleri ***geçersiz kılar*** . Bazı tablolardaki test verileri ile bu durum oluşmasını istemeyebilirsiniz: bazı durumlarda verileri değiştirirken değişiklikler veritabanı güncelleştirmelerinden sonra kalmasını istiyor. Bu durumda, bir koşullu ekleme işlemi yapmak istiyorsanız, yalnızca mevcut değilse bir satır ekleyin. Çekirdek yöntemi her iki yaklaşımı kullanır.

    [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) metoduna geçirilen ilk parametre, bir satırın zaten var olup olmadığını denetlemek için kullanılacak özelliği belirtir. Sağladınız test öğrenci verileri için, `LastName` listedeki her bir ad benzersiz olduğundan bu amaçla özellik kullanılabilir:

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    Bu kod, son adların benzersiz olduğunu varsayar. Yinelenen son ada sahip bir öğrenci el ile eklerseniz, bir sonraki geçiş işlemi yaptığınızda aşağıdaki özel durumu alırsınız:

    **Sıra birden fazla öğe içeriyor**

    "Alexander Carson" adlı iki öğrenci gibi gereksiz verilerin nasıl işleneceği hakkında daha fazla bilgi için, bkz. Rick Anderson 'ın blogu üzerinde [Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) . `AddOrUpdate` Yöntemi hakkında daha fazla bilgi için bkz. Julie Lerman 'ın blogda [EF 4,3 AddOrUpdate yöntemiyle dikkatli olunmalıdır](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) .

    Varlıkları oluşturan `Enrollment` kod, koleksiyondaki varlıklarda `students` bulunan `ID` değer olduğunu varsayar, ancak bu özelliği koleksiyonu oluşturan kodda ayarlayamazsınız.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    Bu `ID` özelliği, `ID` koleksiyonu`students` çağırdığınızda `SaveChanges` değer ayarlandığı için kullanabilirsiniz. EF, veritabanına bir varlık eklediğinde, birincil anahtar değerini otomatik olarak alır ve bu varlık, belleğin `ID` özelliğini bellekte güncelleştirir.

    Her `Enrollment` varlığı `Enrollments` varlıkkümesineekleyen`AddOrUpdate` kod yöntemini kullanmaz. Bir varlığın zaten var olup olmadığını denetler ve varlık yoksa varlığı ekler. Bu yaklaşım, uygulama kullanıcı arabirimini kullanarak bir kayıt sınıfı üzerinde yaptığınız değişiklikleri korur. Kod, `Enrollment` [listedeki](https://msdn.microsoft.com/library/6sh2ey19.aspx) her üye boyunca döngü yapar ve kayıt veritabanında bulunmazsa kaydı veritabanına ekler. Veritabanını ilk güncelleştirdiğinizde, veritabanı boş olur, bu nedenle her bir kayıt eklenir.

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. Projeyi oluşturun.

### <a name="execute-the-first-migration"></a>İlk geçişi yürütme

`add-migration` Komutunu çalıştırdığınızda geçişler, veritabanını sıfırdan oluşturacak kodu oluşturdu. Bu kod ayrıca,  *&lt;zaman&gt;damgası\_InitialCreate.cs*adlı dosyadaki *geçişler* klasöründedir. Sınıfının yöntemi, veri modeli `Down` varlık kümelerine karşılık gelen veritabanı tablolarını oluşturur ve yöntemi onları siler. `Up` `InitialCreate`

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Geçişler, `Up` geçiş için veri modeli değişikliklerini uygulamak üzere yöntemini çağırır. Güncelleştirmeyi geri almak için bir komut girdiğinizde, geçişler `Down` yöntemini çağırır.

Bu, `add-migration InitialCreate` komutu girdiğinizde oluşturulan ilk geçişdir. Parametresi (`InitialCreate` örnekteki) dosya adı için kullanılır ve istediğiniz her şey olabilir; genellikle, geçişte nelerin yapıldığını özetleyen bir sözcük veya tümcecik seçersiniz. Örneğin, daha sonra bir geçiş &quot;AddDepartmentTable&quot;adı yazabilirsiniz.

Veritabanı zaten mevcut olduğunda ilk geçişi oluşturduysanız veritabanı oluşturma kodu oluşturulur, ancak veritabanı veri modeliyle zaten eşleştiğinden çalıştırması gerekmez. Uygulamayı, veritabanının mevcut olmadığı başka bir ortama dağıttığınızda, bu kod veritabanınızı oluşturmak için çalışır, bu nedenle ilk önce test etmek iyi bir fikirdir. Bu nedenle, geçişlerin sıfırdan yeni bir tane oluşturabilmesi için bağlantı dizesindeki veritabanının adını daha&mdash;önce değiştirmiş olursunuz.

1. **Paket Yöneticisi konsolu** penceresinde, aşağıdaki komutu girin:

    `update-database`

    Komutu veritabanını oluşturmak için `Up` yöntemini çalıştırır `Seed` ve sonra veritabanını doldurmak için yöntemini çalıştırır. `update-database` Aynı işlem, uygulamayı dağıttıktan sonra, aşağıdaki bölümde göreceğiniz gibi otomatik olarak çalıştırılır.
2. İlk öğreticide yaptığınız gibi veritabanını incelemek için **Sunucu Gezgini** kullanın ve uygulamayı çalıştırarak her şeyin daha önce olduğu gibi çalıştığını doğrulayın.

## <a name="deploy-to-azure"></a>Azure’a dağıtma

Şimdiye kadar uygulama, geliştirme bilgisayarınızda IIS Express yerel olarak çalışıyor. Diğer kişilerin Internet üzerinden kullanmasını sağlamak için, bir Web barındırma sağlayıcısına dağıtmanız gerekir. Öğreticinin bu bölümünde Azure 'a dağıtırsınız. Bu bölüm isteğe bağlıdır; Bu adımı atlayabilir ve aşağıdaki öğreticiye devam edebilir ya da seçtiğiniz farklı bir barındırma sağlayıcısı için bu bölümdeki yönergeleri uyarlayabilirsiniz.

### <a name="use-code-first-migrations-to-deploy-the-database"></a>Veritabanını dağıtmak için Code First geçişleri kullanma

Veritabanını dağıtmak için Code First Migrations kullanırsınız. Visual Studio 'dan dağıtma ayarlarını yapılandırmak için kullandığınız yayımlama profilini oluşturduğunuzda, **veritabanını güncelleştir**etiketli bir onay kutusunu seçersiniz. Bu ayar, dağıtım işleminin, Code First `MigrateDatabaseToLatestVersion` Başlatıcı sınıfını kullanması için hedef sunucudaki uygulama *Web. config* dosyasını otomatik olarak yapılandırmasına neden olur.

Visual Studio, projenizi hedef sunucuya kopyalarken dağıtım işlemi sırasında veritabanıyla hiçbir şey yapmaz. Dağıtılan uygulamayı çalıştırdığınızda ve dağıtımdan sonra veritabanına ilk kez eriştiğinde, veritabanının veri modeliyle eşleşip eşleşmediğini denetler Code First. Bir uyumsuzluk varsa, Code First otomatik olarak veritabanını oluşturur (henüz yoksa) veya veritabanı şemasını en son sürüme güncelleştirir (bir veritabanı varsa ancak modelle eşleşmezse). Uygulama bir geçişler `Seed` yöntemi uygularsa, yöntem veritabanı oluşturulduktan sonra veya şema güncelleştirildikten sonra çalışır.

Geçişler `Seed` yönteminiz test verileri ekler. Bir üretim ortamına dağıtım yapıyorsanız, `Seed` yöntemi yalnızca üretim veritabanınıza eklemek istediğiniz verileri içerecek şekilde değiştirmeniz gerekir. Örneğin, geçerli veri modelinizde gerçek kurslar olmasını, ancak geliştirme veritabanında öğrenci öğrencilerine sahip olmak isteyebilirsiniz. Geliştirme sırasında her ikisini `Seed` de yüklemek için bir yöntem yazabilir ve ardından üretime dağıtmadan önce kurgusal öğrencileri açıklama olarak girebilirsiniz. Ya da yalnızca kursları yüklemek `Seed` için bir yöntem yazabilir ve uygulamanın kullanıcı arabirimini kullanarak test veritabanına kurgusal öğrencileri el ile girebilirsiniz.

### <a name="get-an-azure-account"></a>Azure hesabı alın

Bir Azure hesabınız olması gerekir. Henüz bir tane yoksa ancak Visual Studio aboneliğiniz varsa, [abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)etkinleştirebilirsiniz. Aksi takdirde, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/free/).

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>Azure 'da bir Web sitesi ve SQL veritabanı oluşturma

Azure 'daki Web uygulamanız paylaşılan bir barındırma ortamında çalışacak, bu da diğer Azure istemcileriyle paylaşılan sanal makinelerde (VM) çalıştığı anlamına gelir. Paylaşılan barındırma ortamı, buluta başlamak için düşük maliyetli bir yoldur. Daha sonra, Web trafiğiniz arttıkça, uygulama adanmış VM 'lerde çalışırken ihtiyacı karşılayacak şekilde ölçeklendirebilir. Azure App Service için fiyatlandırma seçenekleri hakkında daha fazla bilgi edinmek için [App Service fiyatlandırmayı](https://azure.microsoft.com/pricing/details/app-service/)okuyun.

Veritabanını Azure SQL veritabanı 'na dağıtırsınız. SQL veritabanı, SQL Server teknolojileri üzerinde geliştirilen bulut tabanlı bir ilişkisel veritabanı hizmetidir. SQL Server ile birlikte çalışan araçlar ve uygulamalar SQL veritabanı ile de çalışır.

1. [Azure yönetim portalı](https://portal.azure.com), sol sekmede **kaynak oluştur** ' u seçin ve ardından tüm kullanılabilir kaynakları görmek için **Yeni** bölmede (veya *Dikey*pencerede) **Tümünü göster** ' i seçin. **Her şey** dikey penceresinin **Web** bölümünde **Web uygulaması + SQL** ' i seçin. Son olarak **Oluştur**' u seçin.

    ![Azure portalında kaynak oluşturma](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   Yeni **Yeni bir Web uygulaması** oluşturmak için kullanılacak form + SQL kaynağı açılır.

2. Uygulamanızın benzersiz URL 'SI olarak kullanmak için **uygulama adı** kutusuna bir dize girin. URL 'nin tamamı buraya girdiklerinizi ve Azure Uygulama Hizmetleri 'nin (. azurewebsites.net) varsayılan etki alanını içerir. **Uygulama adı** zaten alınmış Ise, sihirbaz sizi kırmızı bir *uygulama adı* yok iletisi ile bilgilendirir. **Uygulama adı** kullanılabiliyorsa yeşil bir onay işareti görürsünüz.

3. **Abonelik** kutusunda **App Service** bulunmasını istediğiniz Azure aboneliğini seçin.

4. **Kaynak grubu** metin kutusunda, bir kaynak grubu seçin veya yeni bir tane oluşturun. Bu ayar, Web sitenizin çalışacağı veri merkezini belirtir. Kaynak grupları hakkında daha fazla bilgi için bkz. [kaynak grupları](/azure/azure-resource-manager/resource-group-overview#resource-groups).

5. *App Service bölümüne*tıklayıp **App Service** **Yeni oluştur**' a tıklayarak yeni bir **App Service planı** oluşturun (App Service Ile aynı ad olabilir), **konum**ve **fiyatlandırma katmanı** (ücretsiz bir seçenek mevcuttur).

6. **SQL veritabanı**' na tıklayın ve ardından **Yeni veritabanı oluştur** ' u seçin veya varolan bir veritabanını seçin.

7. **Ad** kutusuna veritabanınız için bir ad girin.
8. **Hedef sunucu** kutusuna tıklayın ve sonra **Yeni sunucu oluştur**' u seçin. Alternatif olarak, daha önce bir sunucu oluşturduysanız, bu sunucuyu kullanılabilir sunucular listesinden seçebilirsiniz.
9. **Fiyatlandırma katmanı** bölümünü seçin, *ücretsiz*' i seçin. Ek kaynaklar gerekiyorsa, veritabanı istediğiniz zaman ölçeklendirilebilir. Azure SQL fiyatlandırması hakkında daha fazla bilgi edinmek için bkz. [Azure SQL veritabanı fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/managed/).
10. [Harmanlamayı](/sql/relational-databases/collations/collation-and-unicode-support) gerektiği şekilde değiştirin.
11. Yönetici **SQL Yöneticisi Kullanıcı adı** ve **SQL yönetici parolası**girin.

    - **Yenı SQL veritabanı sunucusu**' nu seçtiyseniz, veritabanına erişirken daha sonra kullanacağınız yeni bir ad ve parola tanımlayın.
    - Daha önce oluşturduğunuz bir sunucu seçtiyseniz, bu sunucunun kimlik bilgilerini girin.

12. Telemetri toplama, Application Insights kullanılarak App Service için etkinleştirilebilir. Çok az yapılandırma sayesinde, Application Insights değerli olay, özel durum, bağımlılık, istek ve izleme bilgilerini toplar. Application Insights hakkında daha fazla bilgi edinmek için bkz. [Azure izleyici](https://azure.microsoft.com/services/monitor/).
13. Bittiğini göstermek için en altta **Oluştur** ' a tıklayın.

    Yönetim Portalı, pano sayfasına döner ve sayfanın üst kısmındaki **Bildirimler** alanı sitenin oluşturulduğunu gösterir. Bir süre sonra (genellikle bir dakikadan kısa bir süre), dağıtımın başarılı olduğunu belirten bir bildirim vardır. Sol taraftaki Gezinti çubuğunda, yeni App Service **App Services** bölümünde görünür ve **SQL VERITABANLARı** bölümünde yeni SQL veritabanı görüntülenir.

### <a name="deploy-the-app-to-azure"></a>Uygulamayı Azure'a dağıtma

1. Visual Studio 'da **Çözüm Gezgini** projeye sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.

2. **Bir yayımlama hedefi seçin** sayfasında **App Service** ' yi seçin ve ardından **var**' ı seçin ve ardından **Yayımla**' yı seçin.

    ![Bir yayımlama hedefi sayfası seçin](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/publish-select-existing-azure-app-service.png)

3. Daha önce Azure aboneliğinizi Visual Studio 'ya eklemediyseniz, ekrandaki adımları uygulayın. Bu adımlar, Visual Studio 'nun Azure aboneliğinize bağlanmasını sağlayarak **uygulama hizmetleri** listesinin Web sitenizi içermesini sağlar.

4. **App Service** sayfasında, App Service eklediğiniz **aboneliği** seçin. **Görünüm**bölümünde **kaynak grubu**' nu seçin. App Service eklediğiniz kaynak grubunu genişletin ve App Service seçin. Uygulamayı yayımlamak için **Tamam ' ı** seçin.

5. **Çıkış** penceresinde hangi dağıtım eylemlerinin alındığı ve dağıtımın başarılı bir şekilde tamamlandığını raporlayan görüntülenir.

6. Dağıtım başarılı olduğunda, varsayılan tarayıcı otomatik olarak dağıtılan Web sitesinin URL 'SI olarak açılır.

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    Uygulamanız artık bulutta çalışmaktadır.

Bu noktada, **Execute Code First Migrations (uygulama başlangıcında çalışır)** öğesini SEÇTIĞINIZDEN Azure SQL veritabanında *SchoolContext* veritabanı oluşturulmuştur. *Web. config* dosyası dağıtılmış web sitesinde değiştirilmiştir, bu sayede, kodunuzun veritabanına veri okuması veya yazması ( **öğrenciler** sekmesini seçtiğinizde meydana gelir) Için [Migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) başlatıcısı 'nın ilk kez çalışması. ):

![Web. config dosyası alıntısı](https://asp.net/media/4367421/mig.png)

Dağıtım işlemi ayrıca, veritabanı şemasını güncelleştirmek ve veritabanını dengeli yapmak için Code First Migrations için yeni bir bağlantı dizesi *(SchoolContext\_databasepublish*) oluşturmuştur.

![Web. config dosyasında bağlantı dizesi](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

Web. config dosyasının dağıtılan sürümünü *ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*' de kendi bilgisayarınızda bulabilirsiniz. Dağıtılmış *Web. config* dosyasının kendisini FTP kullanarak erişebilirsiniz. Yönergeler için bkz [. Visual Studio kullanarak ASP.NET Web dağıtımı: Kod güncelleştirmesi](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)dağıtma. "FTP aracını kullanmak Için" ile başlayan yönergeleri izleyin: FTP URL 'SI, Kullanıcı adı ve parola. "

> [!NOTE]
> Web uygulaması güvenlik uygulamaz, böylece URL 'YI bulan herkes verileri değiştirebilir. Web sitesinin güvenliğini sağlama hakkında yönergeler için bkz. Membership, [OAuth ve SQL veritabanı Ile güvenli bir ASP.NET MVC uygulamasını Azure 'A dağıtma](/aspnet/core/security/authorization/secure-data). Visual Studio 'da Azure Yönetim Portalı veya **Sunucu Gezgini** kullanarak hizmeti durdurarak diğer kişilerin siteyi kullanmasını engelleyebilirsiniz.

![App Service menü öğesini durdur](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>Gelişmiş geçiş senaryoları

Bu öğreticide gösterildiği gibi geçişleri otomatik olarak çalıştırarak bir veritabanını dağıtırsanız ve birden çok sunucu üzerinde çalışan bir Web sitesine dağıtıyorsanız, geçişleri aynı anda çalıştırmaya çalışan birden fazla sunucu alabilirsiniz. Geçişler atomik olduğundan, iki sunucu aynı geçişi çalıştırmaya çalışırsanız, biri başarılı olur ve diğeri başarısız olur (işlemlerin iki kez yapılamaması durumunda). Bu senaryoda, bu sorunlardan kaçınmak istiyorsanız geçişleri el ile çağırabilir ve yalnızca bir kez gerçekleşmeleri için kendi kodunuzu ayarlayabilirsiniz. Daha fazla bilgi için bkz. Rowa Miller 'in blogu ve [migrate. exe](/ef/ef6/modeling/code-first/migrations/migrate-exe) ' de [Koddan çalıştırılan ve betik geçişleri](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/) (komut satırından geçişleri yürütmek için).

Diğer geçiş senaryoları hakkında daha fazla bilgi için bkz. [geçişleri ekran kaydı serisi](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx).

## <a name="update-specific-migration"></a>Belirli geçişi Güncelleştir

`update-database -target MigrationName`

Komut `update-database -target MigrationName` , hedeflenen geçişi çalıştırır.

## <a name="ignore-migration-changes-to-database"></a>Veritabanına yapılan geçiş değişikliklerini yoksay

`Add-migration MigrationName -ignoreChanges`

`ignoreChanges`geçerli modelle anlık görüntü olarak boş bir geçiş oluşturur.

## <a name="code-first-initializers"></a>Code First başlatıcıları

Dağıtım bölümünde, kullanılmakta olan [Migratedatabasetolatestversion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx) başlatıcısı 'nı gördünüz. Code First Ayrıca, [Createdatabaseifnotexists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) (varsayılan), [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) (daha önce kullandığınız) ve [dropcreatedatabaseher zaman](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)dahil diğer başlatıcıları da sağlar. Başlatıcı `DropCreateAlways` , birim testlerine yönelik koşulları ayarlamak için yararlı olabilir. Ayrıca kendi başlatıcılarınızı yazabilir ve uygulamanın veritabanından okuma veya veritabanına yazma işlemlerini beklemek istemiyorsanız bir başlatıcıyı açıkça çağırabilirsiniz.

Başlatıcılar hakkında daha fazla bilgi için bkz. [Entity Framework Code First veritabanı başlatıcıları anlama](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm) ve kitap [programlama Entity Framework Bölüm 6: Julie](http://shop.oreilly.com/product/0636920022220.do) Lerman ve Rowa Miller tarafından Code First.

## <a name="get-the-code"></a>Kodu alın

[Tamamlanmış projeyi indirin](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar, [ASP.NET Data Access-önerilen kaynaklar](xref:whitepapers/aspnet-data-access-content-map)bölümünde bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Code First geçişleri etkinleştirildi
> * Uygulamayı Azure 'da dağıtıldı (isteğe bağlı)

Bir ASP.NET MVC uygulaması için daha karmaşık bir veri modeli oluşturmayı öğrenmek üzere bir sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Daha karmaşık veri modeli oluşturma](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
