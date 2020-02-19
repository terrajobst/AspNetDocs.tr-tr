---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: Üyelik ve Kullanıcı profillerinin evrensel sağlayıcı verilerini ASP.NET Identity (C#)-ASP.NET 4. x öğesine geçirme
author: rustd
description: Bu öğreticide, mevcut bir uygulamanın evrensel sağlayıcıları kullanılarak oluşturulan kullanıcı ve rol verilerinin ve Kullanıcı profili verilerinin geçirilmesi için gereken adımlar açıklanmaktadır...
ms.author: riande
ms.date: 12/13/2013
ms.custom: seoapril2019
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 31f02a0cec3c531c45c37b7aad8456e01e80b5ea
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456120"
---
# <a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>Üyelik ve Kullanıcı Profilleri için Evrensel Sağlayıcı Verilerini ASP.NET Identity’ye Geçirme (C#)

, [Pranav Rastogi](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Robert McMurray](https://github.com/rmcmurray), [suwith Joshi](https://github.com/suhasj)

> Bu öğreticide, mevcut bir uygulamanın evrensel sağlayıcıları kullanılarak oluşturulan kullanıcı ve rol verilerini ve Kullanıcı profili verilerini ASP.NET Identity modeline geçirmek için gereken adımlar açıklanmaktadır. Kullanıcı profili verilerini geçirmek için burada bahsedilen yaklaşım, SQL üyeliğiyle birlikte bir uygulama içinde de kullanılabilir.

Visual Studio 2013 sürümünde, ASP.NET ekibi yeni bir ASP.NET Identity sistemi sunmuştur ve bu sürüm hakkında [buradan](../../index.md)daha fazla bilgi edinebilirsiniz. Web uygulamalarını [SQL üyeliğinden yeni kimlik sistemine](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)geçirme makalesinde takip edilen bu makalede, Kullanıcı ve rol yönetimi için sağlayıcılar modelini izleyen mevcut uygulamaları yeni kimlik modeline geçirme adımları gösterilmektedir. Bu öğreticinin odağı öncelikle Kullanıcı profili verilerinin yeni sisteme sorunsuz bir şekilde geçişini sağlamak için kullanılacaktır. Kullanıcı ve rol bilgilerinin geçirilmesi SQL üyeliğiyle benzerdir. Profil verilerini geçirmek için yaklaşım, SQL üyeliğiyle birlikte bir uygulamada de kullanılabilir.

Örnek olarak, sağlayıcılar modelini kullanan Visual Studio 2012 kullanılarak oluşturulan bir Web uygulamasıyla başlayacağız. Daha sonra profil yönetimi için kod ekleyecek, Kullanıcı kaydeden, kullanıcılar için profil verileri ekleyecek, veritabanı şemasını geçireceğiz ve ardından uygulamayı kullanıcı ve rol yönetimi için kimlik sistemini kullanacak şekilde değiştirmelisiniz. Geçişin bir testi olarak, evrensel sağlayıcılar kullanılarak oluşturulan kullanıcılar oturum açabiliyor ve yeni kullanıcıların kaydolabilebilmelidir.

> [!NOTE]
> [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations)bir bütün örneği bulabilirsiniz.

## <a name="profile-data-migration-summary"></a>Profil verileri geçiş Özeti

Geçişlere başlamadan önce, profil verilerini sağlayıcılar modelinde depolama deneyimiyle karşılaşmamıza izin verin. Uygulama kullanıcıları için profil verileri birden çok şekilde depolanabilir ve bu, evrensel sağlayıcılarla birlikte sunulan yerleşik profil sağlayıcılarını kullanmakla en yaygın şekilde depolanabilir. Adımlarda şunlar yer alır

1. Profil verilerini depolamak için kullanılan özellikleri olan bir sınıf ekleyin.
2. ' ProfileBase ' öğesini genişleten bir sınıf ekleyin ve Kullanıcı için yukarıdaki profil verilerini almak üzere yöntemleri uygular.
3. *Web. config* dosyasında varsayılan profil sağlayıcılarını kullanmayı etkinleştirin ve profil bilgilerine erişirken kullanılacak adım #2 içinde belirtilen sınıfı tanımlayın.

Profil bilgileri veritabanındaki ' profiller ' tablosunda serileştirilmiş XML ve ikili veri olarak depolanır.

Yeni ASP.NET Identity sistemini kullanmak üzere uygulamayı geçirdikten sonra, profil bilgileri seri durumdan çıkarılacak ve Kullanıcı sınıfında Özellikler olarak depolanır. Her özellik daha sonra Kullanıcı tablosundaki sütunlarla eşlenebilir. Buradaki avantajda, özelliklerin her erişirken veri bilgisinin serileştirilmesinin yanı sıra Kullanıcı sınıfı kullanılarak doğrudan üzerinde da çalışılabilecek.

## <a name="getting-started"></a>Başlarken

1. Visual Studio 2012 ' de yeni bir ASP.NET 4,5 Web Forms uygulaması oluşturun. Geçerli örnek Web Forms şablonunu kullanır, ancak MVC uygulamasını da kullanabilirsiniz.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. Profil bilgilerini depolamak için yeni bir ' modeller ' klasörü oluştur  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. Örnek olarak, profilde kullanıcının Doğum, şehir, yükseklik ve ağırlığının tarihini depolamamıza izin verin. Yükseklik ve ağırlık, ' Personal stats ' adlı özel bir sınıf olarak depolanır. Profili depolamak ve almak için ' ProfileBase 'i genişleten bir sınıfa ihtiyacımız var. Profil bilgilerini almak ve depolamak için yeni bir ' AppProfile ' sınıfı oluşturalım.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. *Web. config* dosyasında profili etkinleştirin. #3 adımında oluşturulan kullanıcı bilgilerini depolamak/almak için kullanılacak sınıf adını girin.

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. Kullanıcının profil verilerini almak ve depolamak için ' Account ' klasörüne bir Web Forms sayfası ekleyin. Projeye sağ tıklayın ve ' yeni öğe Ekle ' öğesini seçin. ' AddProfileData. aspx ' ana sayfasına sahip yeni bir WebForms sayfası ekleyin. ' MainContent ' bölümünde aşağıdakileri kopyalayın:

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   Aşağıdaki kodu arkasındaki koda ekleyin:

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   Derleme hatalarını kaldırmak için AppProfile sınıfının tanımlandığı ad alanını ekleyin.
6. Uygulamayı çalıştırın ve Kullanıcı adı '**olduser '** olan yeni bir kullanıcı oluşturun. ' AddProfileData ' sayfasına gidin ve Kullanıcı için profil bilgilerini ekleyin.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

Verilerin, Sunucu Gezgini penceresini kullanarak ' profiller ' tablosunda serileştirilmiş XML olarak depolandığını doğrulayabilirsiniz. Visual Studio 'da, ' Görünüm ' menüsünden ' Sunucu Gezgini ' seçeneğini belirleyin. *Web. config* dosyasında tanımlanan veritabanı için bir veri bağlantısı olması gerekir. Veri bağlantısına tıkladığınızda farklı alt kategoriler gösterilmektedir. Veritabanınızdaki farklı tabloları göstermek için ' Tables ' ' ı genişletin, ardından ' profiles ' öğesine sağ tıklayın ve ' tablo verilerini göster ' öğesini seçerek profiller tablosunda depolanan profil verilerini görüntüleyin.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>Veritabanı şeması geçiriliyor

Mevcut veritabanının kimlik sistemi ile çalışmasını sağlamak için, özgün veritabanına eklediğimiz alanları desteklemek üzere kimlik veritabanındaki şemayı güncelleştirmemiz gerekir. Bu, yeni tablolar oluşturmak ve mevcut bilgileri kopyalamak için SQL betikleri kullanılarak yapılabilir. ' Sunucu Gezgini ' penceresinde, tabloları göstermek için ' DefaultConnection ' ' ı genişletin. Tablolar ' a sağ tıklayın ve ' yeni sorgu ' seçeneğini belirleyin

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

[https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) SQL betiğini yapıştırın ve çalıştırın. ' DefaultConnection ' yenilendiğinde yeni tabloların eklendiğini görebiliriz. Bilgilerin geçirildiğini görmek için tabloların içindeki verileri kontrol edebilirsiniz.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>Uygulamayı kullanmak ASP.NET Identity geçirme

1. ASP.NET Identity için gereken NuGet paketlerini yükler:

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft. Owin. Security. Facebook
    - Microsoft. Owin. Security. Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   NuGet paketlerini yönetme hakkında daha fazla bilgi için [burada](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog) bulunabilir
2. Tablodaki mevcut verilerle çalışmak için, tablolara geri eşlenen ve bunları kimlik sisteminde bağlayan model sınıfları oluşturmanız gerekir. Kimlik sözleşmesinin bir parçası olarak model sınıfları, Identity. Core dll dosyasında tanımlanan arabirimleri uygulamalıdır ya da Microsoft. AspNet. Identity. EntityFramework içinde bulunan bu arabirimlerin mevcut uygulamasını genişletebilir. Rol, Kullanıcı oturumu açma ve kullanıcı talepleri için mevcut sınıfları kullanacağız. Örneğimiz için özel bir Kullanıcı kullanmanız gerekir. Projeye sağ tıklayın ve ' ıdentitymodeller ' yeni klasörünü oluşturun. Aşağıda gösterildiği gibi yeni bir ' user ' sınıfı ekleyin:

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   ' ProfileInfo ' özelliğinin artık Kullanıcı sınıfında bir özelliği olduğuna dikkat edin. Bu nedenle, profil verileriyle doğrudan çalışmak için Kullanıcı sınıfını kullanabiliriz.

**IdentityModel** ve **ıdentityaccount** klasörlerindeki dosyaları indirme kaynağından ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ) kopyalayın. Bunlar, ASP.NET Identity API 'Leri kullanılarak Kullanıcı ve rol yönetimi için gereken kalan model sınıflarına ve yeni sayfalara sahiptir. Kullanılan yaklaşım SQL üyeliğiyle benzerdir ve ayrıntılı açıklama [burada](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)bulunabilir.

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>Yeni tablolara profil verileri kopyalanıyor

Daha önce belirtildiği gibi, profiller tablolarında XML verilerinin serisini çıkardık ve bunu AspNetUsers tablosunun sütunlarında depolarız. Önceki adımda bulunan kullanıcılar tablosunda yeni sütunlar oluşturulmuştur, böylece tüm sol tanesi bu sütunları gerekli verilerle doldurmaktır. Bunu yapmak için, kullanıcılar tablosunda yeni oluşturulan sütunları doldurmak üzere bir kez çalıştırılan konsol uygulamasını kullanacağız.

1. Çıkış çözümünde yeni bir konsol uygulaması oluşturun.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. Entity Framework paketinin en son sürümünü yükler.
3. Yukarıda oluşturulan Web uygulamasını konsol uygulamasına başvuru olarak ekleyin. Bunu yapmak için projeye sağ tıklayın, ardından ' başvuru Ekle ', sonra çözüm ' e tıklayın ve ardından projeye tıklayın ve Tamam ' a tıklayın.
4. Aşağıdaki kodu Program.cs sınıfında kopyalayın. Bu mantık her bir kullanıcı için profil verilerini okur, ' ProfileInfo ' nesnesi olarak serileştirir ve veritabanına geri depolar.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   Kullanılan modellerden bazıları Web uygulaması projesinin ' ıdentitymodeller ' klasöründe tanımlanmıştır, bu nedenle karşılık gelen ad alanlarını dahil etmeniz gerekir.
5. Yukarıdaki kod, önceki adımlarda oluşturulan Web uygulaması projesinin App\_Data klasöründeki veritabanı dosyasında çalışmaktadır. Bu dosyaya başvurmak için, konsol uygulamasının App. config dosyasındaki bağlantı dizesini Web uygulamasının Web. config dosyasında bulunan bağlantı dizesiyle güncelleştirin. Ayrıca, ' AttachDbFilename ' özelliğinde tam fiziksel yolu da sağlayın.
6. Bir komut istemi açın ve yukarıdaki konsol uygulamasının bin klasörüne gidin. Yürütülebilir dosyayı çalıştırın ve aşağıdaki görüntüde gösterildiği gibi günlük çıkışını gözden geçirin.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. Sunucu Gezgini ' AspNetUsers ' tablosunu açın ve özellikleri tutan yeni sütunlardaki verileri doğrulayın. Bunlara karşılık gelen özellik değerleriyle güncelleştirilmeleri gerekir.

## <a name="verify-functionality"></a>İşlevselliği doğrulama

Eski veritabanından bir kullanıcının oturumu açmak için ASP.NET Identity kullanılarak uygulanan yeni eklenen üyelik sayfalarını kullanın. Kullanıcının aynı kimlik bilgilerini kullanarak oturum açabiliyor olması gerekir. OAuth ekleme, yeni bir Kullanıcı oluşturma, parola değiştirme, rol ekleme, rollere kullanıcı ekleme gibi diğer işlevleri deneyin.

Eski Kullanıcı ve yeni kullanıcılar için profil verileri, kullanıcılar tablosunda alınıp depolanmalıdır. Eski tabloya artık başvurulmamalıdır.

## <a name="conclusion"></a>Sonuç

ASP.NET Identity üyelik için sağlayıcı modelini kullanan Web uygulamalarını geçirme sürecini tarif eden makale. Makalede ayrıca, kullanıcıların kimlik sistemine bağlanılmasına yönelik profil verilerinin geçirilmesi de özetlenmektedir. Uygulamanızı geçirirken lütfen sorular ve sorunlar için aşağıdaki açıklamaları bırakın.

*Makaleyi gözden geçirmek için Rick Anderson ve Robert McMurray sayesinde teşekkürler.*
