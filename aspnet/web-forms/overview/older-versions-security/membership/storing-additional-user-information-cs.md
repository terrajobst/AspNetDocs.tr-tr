---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
title: Ek Kullanıcı bilgilerini depolama (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, çok ilkel bir konuk defteri uygulaması oluşturarak bu soruyu yanıtlarız. Bunu yaparken, modeli için farklı seçeneklere bakacağız...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 1642132a-1ca5-4872-983f-ab59fc8865d3
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 24b96e86bc93e03d2639b73e35ed1fd1271bac5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634871"
---
# <a name="storing-additional-user-information-c"></a>Ek Kullanıcı Bilgileri Depolama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_cs.pdf)

> Bu öğreticide, çok ilkel bir konuk defteri uygulaması oluşturarak bu soruyu yanıtlarız. Bunu yaparken, bir veritabanındaki kullanıcı bilgilerini modelleyerek farklı seçeneklere bakacağız ve bu verileri üyelik çerçevesi tarafından oluşturulan kullanıcı hesaplarıyla ilişkilendirme konusuna bakın.

## <a name="introduction"></a>Giriş

ASP.net. NET 'in üyelik çerçevesi, kullanıcıları yönetmek için esnek bir arabirim sunar. Üyelik API 'SI, kimlik bilgilerini doğrulama, şu anda oturum açmış kullanıcıyla ilgili bilgileri alma, yeni bir kullanıcı hesabı oluşturma ve başka bir kullanıcı hesabını silme yöntemlerini içerir. Üyelik çerçevesindeki her kullanıcı hesabı yalnızca kimlik bilgilerini doğrulamak ve Kullanıcı hesabı ile ilgili gerekli görevleri gerçekleştirmek için gereken özellikleri içerir. Bu, üyelik çerçevesindeki bir kullanıcı hesabını modelleyen [`MembershipUser` sınıfının](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)yöntemleri ve özellikleri tarafından belirlenir. Bu sınıfta [`UserName`](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx), [`Email`](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)ve [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx)gibi özellikler ve [`GetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx) ve [`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)gibi yöntemler bulunur.

Oftentimes, uygulamaların üyelik çerçevesine dahil bulunmayan ek kullanıcı bilgilerini depolaması gerekir. Örneğin, bir çevrimiçi satıcı, her bir kullanıcının Sevkiyat ve fatura adreslerini, ödeme bilgilerini, teslim tercihlerini ve iletişim telefon numarasını depolamasına izin verebilir. Ayrıca, sistemdeki her sıra belirli bir kullanıcı hesabıyla ilişkilendirilir.

`MembershipUser` sınıfı `PhoneNumber` veya `DeliveryPreferences` ya da `PastOrders`gibi özellikleri içermez. Bu nedenle, uygulamanın gerektirdiği Kullanıcı bilgilerini nasıl izliyoruz ve üyelik çerçevesiyle tümleştirirsiniz mi? Bu öğreticide, çok ilkel bir konuk defteri uygulaması oluşturarak bu soruyu yanıtlarız. Bunu yaparken, bir veritabanındaki kullanıcı bilgilerini modelleyerek farklı seçeneklere bakacağız ve bu verileri üyelik çerçevesi tarafından oluşturulan kullanıcı hesaplarıyla ilişkilendirme konusuna bakın. Haydi başlayın!

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>1\. Adım: Konuk defteri uygulamasının veri modelini oluşturma

Kullanıcı bilgilerini bir veritabanında yakalamak ve üyelik çerçevesi tarafından oluşturulan kullanıcı hesaplarıyla ilişkilendirmek için kullanılabilecek çeşitli teknikler vardır. Bu teknikleri anlamak için öğretici Web uygulamasını, Kullanıcı ile ilgili bazı verileri yakalayacak şekilde geliştirmemiz gerekir. (Şu anda, uygulamanın veri modeli yalnızca `SqlMembershipProvider`gereken uygulama hizmetleri tablolarını içerir.)

Kimliği doğrulanmış bir kullanıcının bir yorum bırakabileceği çok basit bir konuk defteri uygulaması oluşturalım. Konuk defteri açıklamalarını depolamanın yanı sıra, her bir kullanıcının ev kasasını, giriş sayfasını ve imzasını depolamasına izin verlim. Sağlanmışsa, kullanıcının ev şehir, giriş sayfası ve imza, Konuk defteri 'nde bıraktığınız her iletide görüntülenir.

### <a name="adding-theguestbookcommentstable"></a>`GuestbookComments`tablosu ekleme

Konuk defteri açıklamalarını yakalamak için, `CommentId`, `Subject`, `Body`ve `CommentDate`gibi sütunları içeren `GuestbookComments` adlı bir veritabanı tablosu oluşturuyoruz. Ayrıca, `GuestbookComments` tablodaki her bir kayıt, yorumu kapatan kullanıcıya başvuru yapmış olmaları gerekir.

Bu tabloyu veritabanınıza eklemek için, Visual Studio 'daki Veritabanı Gezgini gidin ve `SecurityTutorials` veritabanının ayrıntılarına gidin. Tablolar klasörüne sağ tıklayın ve yeni tablo Ekle ' yi seçin. Bu, yeni tablo için sütunları tanımlayabileceğimizi sağlayan bir arabirim getirir.

[![Securityöğreticileri veritabanına yeni bir tablo ekleme](storing-additional-user-information-cs/_static/image2.png)](storing-additional-user-information-cs/_static/image1.png)

**Şekil 1**: `SecurityTutorials` veritabanına yeni bir tablo ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image3.png))

Sonra, `GuestbookComments`sütunlarını tanımlayın. `uniqueidentifier`türünde `CommentId` adlı bir sütun ekleyerek başlayın. Bu sütun, Konuk defteri 'ndeki her yorumu benzersiz şekilde tanımlar, `NULL` s 'ye izin vermeyin ve tablonun birincil anahtarı olarak işaretlemez. Her `INSERT``CommentId` alanı için bir değer sağlamak yerine, sütunun varsayılan değerini `NEWID()`olarak ayarlayarak `INSERT` üzerinde bu alan için yeni bir `uniqueidentifier` değeri otomatik olarak oluşturulması gerektiğini belirtebiliriz. Bu ilk alanı ekledikten, birincil anahtar olarak işaretleyerek ve varsayılan değerini ayarladıktan sonra, ekranınızın Şekil 2 ' de gösterilen ekran görüntüsüne benzer olması gerekir.

[![Yorumtıd adlı birincil sütun Ekle](storing-additional-user-information-cs/_static/image5.png)](storing-additional-user-information-cs/_static/image4.png)

**Şekil 2**: `CommentId` adlı bir birincil sütun ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image6.png))

Sonra, `nvarchar(50)` türünde `Subject` adlı ve `nvarchar(MAX)`türünde `Body` adlı bir sütun ekleyin, her iki sütunda da `NULL` izin vermez. Bunu izleyerek `datetime`türünde `CommentDate` adlı bir sütun ekleyin. `NULL` s öğesine izin vermeyin ve `CommentDate` sütununun varsayılan değerini `getdate()`olarak ayarlayın.

Her şey, bir kullanıcı hesabını her konuk defteri açıklamasıyla ilişkilendiren bir sütun eklemektir. Bir seçenek, `nvarchar(256)`türünde `UserName` adlı bir sütun eklemektir. Bu, `SqlMembershipProvider`dışında bir üyelik sağlayıcısı kullanırken uygun bir seçenektir. Ancak `SqlMembershipProvider`kullanılırken, bu öğretici serisinde olduğu gibi `aspnet_Users` tablosundaki `UserName` sütununun benzersiz olması garanti edilmez. `aspnet_Users` tablonun birincil anahtarı `UserId` ve `uniqueidentifier`türündedir. Bu nedenle, `GuestbookComments` tablosu `uniqueidentifier` türünde `UserId` adlı bir sütuna (`NULL` değerlere izin vermeme) ihtiyaç duyuyor. Devam edin ve bu sütunu ekleyin.

> [!NOTE]
> SQL Server öğreticide [*Üyelik şeması oluşturma*](creating-the-membership-schema-in-sql-server-cs.md) konusunda anlatıldığı gibi, üyelik çerçevesi farklı Kullanıcı hesapları olan birden çok Web uygulamasının aynı kullanıcı mağazasını paylaşmasına olanak tanımak üzere tasarlanmıştır. Bunu, Kullanıcı hesaplarını farklı uygulamalara bölümleyerek yapar. Her Kullanıcı adının bir uygulama içinde benzersiz olduğu garanti edilirken aynı Kullanıcı adı aynı kullanıcı mağazasını kullanan farklı uygulamalarda kullanılabilir. `UserName` ve `ApplicationId` alanlarındaki `aspnet_Users` tablosunda bir bileşik `UNIQUE` kısıtlaması vardır ancak yalnızca `UserName` alanında değil. Sonuç olarak, ASPNET\_kullanıcıları tablosunun aynı `UserName` değerine sahip iki (veya daha fazla) kaydı olması mümkündür. Ancak, `aspnet_Users` tablosunun `UserId` alanında (birincil anahtar olduğundan) bir `UNIQUE` kısıtlaması vardır. `UNIQUE` kısıtlaması, `GuestbookComments` ve `aspnet_Users` tabloları arasında yabancı anahtar kısıtlaması kuramadığı için önemlidir.

`UserId` sütununu ekledikten sonra, araç çubuğundaki Kaydet simgesine tıklayarak tabloyu kaydedin. Yeni tablo `GuestbookComments`adlandırın.

`GuestbookComments` tabloyla ilgili en son bir sorun var: `GuestbookComments.UserId` sütunuyla `aspnet_Users.UserId` sütunu arasında bir [yabancı anahtar kısıtlaması](https://msdn.microsoft.com/library/ms175464.aspx) oluşturuyoruz. Bunu başarmak için, yabancı anahtar Ilişkileri iletişim kutusunu başlatmak için araç çubuğundaki Ilişki simgesine tıklayın. (Alternatif olarak, Tablo Tasarımcısı menüsüne gidip Ilişkiler ' i seçerek bu iletişim kutusunu da başlatabilirsiniz.)

Yabancı anahtar Ilişkileri iletişim kutusunun sol alt köşesindeki Ekle düğmesine tıklayın. Bu, yeni bir yabancı anahtar kısıtlaması ekler, ancak yine de ilişkiye katılan tabloları tanımlamanız gerekir.

[![bir tablonun yabancı anahtar kısıtlamalarını yönetmek için yabancı anahtar Ilişkileri Iletişim kutusunu kullanın](storing-additional-user-information-cs/_static/image8.png)](storing-additional-user-information-cs/_static/image7.png)

**Şekil 3**: bir tablonun yabancı anahtar kısıtlamalarını yönetmek Için yabancı anahtar Ilişkileri iletişim kutusunu kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image9.png))

Ardından, sağdaki "Tablo ve sütun belirtimleri" satırındaki üç nokta simgesine tıklayın. Bu işlem, `GuestbookComments` tablosundan birincil anahtar tablosunu ve sütunu ve yabancı anahtar sütununu belirtebileceğiniz tablolar ve sütunlar iletişim kutusunu başlatır. Özellikle, birincil anahtar tablo ve sütun olarak `aspnet_Users` ve `UserId` ' i seçin ve `GuestbookComments` tablosundan yabancı anahtar sütunu olarak `UserId` (bkz. Şekil 4). Birincil ve yabancı anahtar tabloları ve sütunları tanımladıktan sonra, yabancı anahtar Ilişkileri iletişim kutusuna dönmek için Tamam ' ı tıklatın.

[aspnet_Users ve GuesbookComments tabloları arasında yabancı anahtar kısıtlaması oluşturma ![](storing-additional-user-information-cs/_static/image11.png)](storing-additional-user-information-cs/_static/image10.png)

**Şekil 4**: `aspnet_Users` ve `GuesbookComments` tabloları arasında yabancı anahtar kısıtlaması oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image12.png))

Bu noktada yabancı anahtar kısıtlaması oluşturulmuştur. Bu kısıtlamanın varlığı, mevcut olmayan bir kullanıcı hesabına başvuran bir konuk defteri girişi olmadığı garanti altına alarak, iki tablo arasında [ilişkisel bütünlük](http://en.wikipedia.org/wiki/Referential_integrity) sağlar. Varsayılan olarak, bir yabancı anahtar kısıtlaması, karşılık gelen alt kayıtlar varsa bir üst kaydın silinmesine izin vermez. Diğer bir deyişle, bir Kullanıcı bir veya daha fazla konuk defteri açıklaması yapıyorsa ve bu kullanıcı hesabını silmeye çalışarız, Konuk defteri açıklamaları önce silinmedikçe silme işlemi başarısız olur.

Yabancı anahtar kısıtlamaları, bir üst kayıt silindiğinde ilişkili alt kayıtları otomatik olarak silecek şekilde yapılandırılabilir. Diğer bir deyişle, bu yabancı anahtar kısıtlamasını, Kullanıcı hesabı silindiğinde kullanıcının Konuk defteri girdilerinin otomatik olarak silinmesi için ayarlayabiliriz. Bunu gerçekleştirmek için "INSERT and UPDATE Specification" bölümünü genişletin ve "kuralı Sil" özelliğini Cascade olarak ayarlayın.

[Yabancı anahtar kısıtlamasını Cascade silmeleri olarak yapılandırmak ![](storing-additional-user-information-cs/_static/image14.png)](storing-additional-user-information-cs/_static/image13.png)

**Şekil 5**: yabancı anahtar kısıtlamasını Cascade silmesi için yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image15.png))

Yabancı anahtar kısıtlamasını kaydetmek için, yabancı anahtar Ilişkilerinin dışına çıkmak için Kapat düğmesine tıklayın. Ardından, tabloyu ve bu ilişkiyi kaydetmek için araç çubuğundaki Kaydet simgesine tıklayın.

### <a name="storing-the-users-home-town-homepage-and-signature"></a>Kullanıcının ev kasasıdır, giriş sayfasını ve Imzasını depolama

`GuestbookComments` tabloda, Kullanıcı hesaplarıyla bire çok ilişkiyi paylaşan bilgilerin nasıl depolandığı gösterilmektedir. Her Kullanıcı hesabının rastgele sayıda ilişkili açıklaması olabileceğinden, bu ilişki, her yorumu belirli bir kullanıcıya bağlayan bir sütun içeren açıklamalar kümesini tutacak bir tablo oluşturularak modellenir. `SqlMembershipProvider`kullanılırken, bu bağlantı en iyi şekilde `uniqueidentifier` türünde `UserId` adlı bir sütun ve bu sütun ile `aspnet_Users.UserId`arasında yabancı anahtar kısıtlaması oluşturularak belirlenir.

Artık kullanıcının ev kasasını, giriş sayfasını ve imzasını depolamak için her bir kullanıcı hesabıyla üç sütunu ilişkilendirmemiz gerekir. Bu, Konuk defteri açıklamalarında görünecektir. Bunu yapmanın birkaç farklı yolu vardır:

- <strong>`aspnet_Users`</strong> <strong>veya</strong> <strong>`aspnet_Membership`</strong> <strong>tablolarına</strong> <strong>yeni sütunlar ekleyin</strong> . `SqlMembershipProvider`tarafından kullanılan şemayı değiştirdiği için bu yaklaşımı önermiyoruz. Bu karar, yolda daha fazla yola geçmek için geri dönebilir. Örneğin, gelecekteki bir ASP.NET sürümü farklı bir `SqlMembershipProvider` şeması kullanıyorsa. Microsoft, ASP.NET 2,0 `SqlMembershipProvider` verilerini yeni şemaya geçirebileceğiniz bir araç içerebilir, ancak ASP.NET 2,0 `SqlMembershipProvider` şemasını değiştirdiyseniz, böyle bir dönüştürme mümkün olmayabilir.

- **ASP kullanın. Evdeki şehir, giriş sayfası ve imza için bir profil özelliği tanımlayarak NET 'in profil çerçevesi.** ASP.NET, kullanıcıya özgü ek verileri depolamak için tasarlanan bir profil çerçevesini içerir. Üyelik çerçevesi gibi, profil çerçevesi de sağlayıcı modeline göre oluşturulmuştur. .NET Framework, profil verilerini bir SQL Server veritabanında depolayan `SqlProfileProvider` Sile birlikte gelir. Aslında, veritabanı, uygulama hizmetlerini SQL Server öğreticide <a id="_msoanchor_2"> </a> [*Üyelik şeması oluşturma*](creating-the-membership-schema-in-sql-server-cs.md) bölümünde eklendiği sırada eklendiğinden, zaten `SqlProfileProvider` (`aspnet_Profile`) tarafından kullanılan tablo vardır.   
  Profil çerçevesinin başlıca avantajı, geliştiricilerin `Web.config` içinde profil özelliklerini tanımlamasına izin vermeidir. profil verilerini temel alınan veri deposuna seri hale getirmek için hiçbir kod yazılması gerekmez. Kısacası, bir dizi profil özelliklerini tanımlamak ve kod içinde bunlarla çalışmak inanılmaz kolaydır. Ancak, profil sistemi, sürüm oluşturma sırasında bir çok zaman istediğiniz kadar sürer. bu nedenle, yeni kullanıcıya özgü özelliklerin daha sonra eklenmesini veya kaldırılması ya da değiştirilmesini bekleyen bir uygulamanız varsa, profil çerçevesi  en iyi seçenek. Ayrıca, `SqlProfileProvider` profil özelliklerini yüksek oranda yoğun bir biçimde depolar, böylece sorgu doğrudan profil verilerine (örneğin, yeni bir ev kasasında yer aldığı Kullanıcı) karşı sorguları çalıştırmak olanaksız hale getirilir.   
  Profil çerçevesi hakkında daha fazla bilgi için, Bu öğreticinin sonundaki "daha fazla okuma" bölümüne bakın.

- Bu <strong>üç sütunu veritabanında yeni bir tabloya ekleyin ve bu tablo ile`aspnet_Users`arasında bire bir ilişki kurun</strong> <strong>.</strong> Bu yaklaşım, profil çerçevesi ile biraz daha fazla iş içerir, ancak ek kullanıcı özelliklerinin veritabanında modellendiği en yüksek esnekliği sunar. Bu öğreticide kullanacağınız seçenektir.

Her Kullanıcı için giriş Town, giriş sayfası ve imzayı kaydetmek üzere `UserProfiles` adlı yeni bir tablo oluşturacağız. Veritabanı Gezgini penceresindeki tablolar klasörüne sağ tıklayın ve yeni bir tablo oluşturmayı seçin. İlk sütunu `UserId` adlandırın ve türünü `uniqueidentifier`olarak ayarlayın. `NULL` değerlere izin vermeyin ve sütunu birincil anahtar olarak işaretlemez. Sonra, `nvarchar(50)`türündeki `HomeTown` adlı sütunları ekleyin. `nvarchar(100)`türündeki `HomepageUrl`; `nvarchar(500)`türünde Imza. Bu üç sütunun her biri bir `NULL` değeri kabul edebilir.

[![UserProfiles tablosu oluşturma](storing-additional-user-information-cs/_static/image17.png)](storing-additional-user-information-cs/_static/image16.png)

**Şekil 6**: `UserProfiles` tablosunu oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image18.png))

Tabloyu kaydedin ve `UserProfiles`adlandırın. Son olarak, `UserProfiles` tablonun `UserId` alanı ve `aspnet_Users.UserId` alanı arasında bir yabancı anahtar kısıtlaması oluşturun. `GuestbookComments` ve `aspnet_Users` tabloları arasındaki yabancı anahtar kısıtlamasıyla yaptığımız gibi, bu kısıtlamanın basamaklı silmeleri vardır. `UserProfiles` `UserId` alanı birincil anahtar olduğundan, bu, her kullanıcı hesabı için `UserProfiles` tablosunda birden fazla kayıt olmamasını sağlar. Bu tür bir ilişki bire bir olarak adlandırılır.

Veri modeli oluşturulduğuna göre, artık kullanıma hazır hale gelmiştir. 2 ve 3. adımlarda, şu anda oturum açmış olan kullanıcının ev kasalarını, giriş bilgilerini ve imza bilgilerini görüntüleyip düzenleyebilmesi için bakacağız. 4\. adımda, kimliği doğrulanmış kullanıcıların konuk defterine yeni açıklamalar göndermesi ve var olanları görüntülemesi için arabirim oluşturacağız.

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>2\. Adım: kullanıcının ev kasasıdır, giriş sayfasını ve Imzasını görüntüleme

Şu anda oturum açmış olan kullanıcının ev Town, giriş sayfası ve imza bilgilerini görüntülemesine ve düzenlemesine izin veren çeşitli yollar vardır. Kullanıcı arabirimini metin kutusu ve etiket denetimleriyle el ile oluşturabilir veya DetailsView denetimi gibi veri Web denetimlerinden birini kullanabiliriz. Veritabanı `SELECT` ve `UPDATE` deyimlerini gerçekleştirmek için, sayfanın arka plan kod sınıfında ADO.NET kodu yazabilir veya alternatif olarak, SqlDataSource ile bildirime dayalı bir yaklaşım kullanabilirsiniz. İdeal olarak uygulamamız, sayfanın arka plan kod sınıfından programlama yoluyla ya da ObjectDataSource denetimi aracılığıyla bildirimli olarak çağırabileceğimiz katmanlı bir mimari içerir.

Bu öğretici serisi form kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rollere odaklandığından, bu farklı veri erişimi seçeneklerinin tam bir tartışması veya SQL deyimlerini doğrudan yürütmek yerine katmanlı bir mimarinin neden tercih edildiğini belirtmeyecektir. ASP.NET sayfasından. Bir DetailsView ve SqlDataSource (en hızlı ve en kolay seçenek) ile adım adım kılavuzluk eteceğiz, ancak ele alınan kavramlar, farklı Web denetimlerine ve veri erişim mantığına uygulanabilir. ASP.NET 'deki verilerle çalışma hakkında daha fazla bilgi için ASP.NET 2,0 öğretici serisinde *[bulunan verilerle çalışma](../../data-access/index.md)* bölümüne bakın.

`Membership` klasöründeki `AdditionalUserInfo.aspx` sayfasını açın ve sayfaya bir DetailsView denetimi ekleyin, `ID` özelliğini `UserProfile` olarak ayarlayıp `Width` ve `Height` özelliklerini temizleyerek. DetailsView 'un akıllı etiketini genişletin ve yeni bir veri kaynağı denetimine bağlamayı seçin. Bu, veri kaynağı Yapılandırma Sihirbazı 'nı başlatacaktır (bkz. Şekil 7). İlk adım, veri kaynağı türünü belirtmenizi ister. `SecurityTutorials` veritabanına doğrudan bağlandığımız için, veritabanı simgesini seçin ve `ID` `UserProfileDataSource`olarak belirtin.

[![UserProfileDataSource adlı yeni bir SqlDataSource denetimi ekleyin](storing-additional-user-information-cs/_static/image20.png)](storing-additional-user-information-cs/_static/image19.png)

**Şekil 7**: `UserProfileDataSource` adlı yeni bir SqlDataSource denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image21.png))

Sonraki ekranda veritabanının kullanması istenir. `SecurityTutorials` veritabanı için `Web.config` bir bağlantı dizesi zaten tanımladık. Bu bağlantı dizesi adı – `SecurityTutorialsConnectionString` – açılan listede olmalıdır. Bu seçeneği belirleyip Ileri ' ye tıklayın.

[aşağı açılan listeden SecurityTutorialsConnectionString ![seçin](storing-additional-user-information-cs/_static/image23.png)](storing-additional-user-information-cs/_static/image22.png)

**Şekil 8**: açılan listeden `SecurityTutorialsConnectionString` seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image24.png))

Sonraki ekranda, sorgulanacak tablo ve sütunları belirtmemizi istenir. Aşağı açılan listeden `UserProfiles` tablosunu seçin ve tüm sütunları kontrol edin.

[![tüm sütunları UserProfiles tablosundan geri getir](storing-additional-user-information-cs/_static/image26.png)](storing-additional-user-information-cs/_static/image25.png)

**Şekil 9**: `UserProfiles` tablosundan tüm sütunları geri getir ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image27.png))

Şekil 9 ' daki geçerli sorgu `UserProfiles`*Tüm* kayıtları döndürür, ancak şu anda oturum açmış olan kullanıcının kaydıyla ilgileniyoruz. `WHERE` yan tümcesi eklemek için `WHERE` düğmesine tıklayarak `WHERE` yan tümce Ekle iletişim kutusunu açın (bkz. Şekil 10). Burada süzülecek sütunu, işleç ' i ve filtre parametresinin kaynağını seçebilirsiniz. Sütun olarak `UserId` ve Işleç olarak "=" seçeneğini belirleyin.

Ne yazık ki şu anda oturum açmış olan kullanıcının `UserId` değerini döndürecek yerleşik bir parametre kaynağı yok. Bu değeri programlı bir şekilde almak gerekecektir. Bu nedenle, kaynak açılan listesini "none" olarak ayarlayın, parametreyi eklemek için Ekle düğmesine tıklayın ve ardından Tamam ' a tıklayın.

[UserID sütununa bir filtre parametresi eklemek ![](storing-additional-user-information-cs/_static/image29.png)](storing-additional-user-information-cs/_static/image28.png)

**Şekil 10**: `UserId` sütununa bir filtre parametresi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image30.png))

Tamam ' a tıkladıktan sonra Şekil 9 ' da gösterilen ekrana geri dönersiniz. Ancak, bu kez, ekranın alt kısmındaki SQL sorgusu bir `WHERE` yan tümcesi içermelidir. "Test sorgusu" ekranına gitmek için Ileri ' ye tıklayın. Burada sorguyu çalıştırabilir ve sonuçları görebilirsiniz. Sihirbazı tamamladığınızda son ' a tıklayın.

Veri kaynağı Yapılandırma Sihirbazı 'nı tamamladıktan sonra, Visual Studio, sihirbazda belirtilen ayarları temel alarak SqlDataSource denetimi oluşturur. Üstelik, SqlDataSource 'ın `SelectCommand`tarafından döndürülen her bir sütun için DetailsView 'a el ile BoundFields ekler. Kullanıcının bu değeri bilmeleri gerektiğinden, DetailsView içinde `UserId` alanı gösterilmesi gerekmez. Bu alanı doğrudan DetailsView denetiminin bildirim temelli işaretlerinden veya akıllı etiketinden "alanları Düzenle" bağlantısına tıklayarak kaldırabilirsiniz.

Bu noktada sayfanızın bildirime dayalı biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample1.aspx)]

Veri seçmeden önce SqlDataSource denetiminin `UserId` parametresini Şu anda oturum açmış kullanıcının `UserId` olarak belirlememiz gerekir. Bu, SqlDataSource 'un `Selecting` olayına bir olay işleyicisi oluşturularak ve aşağıdaki kodu ekleyerek gerçekleştirilebilir:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample2.cs)]

Yukarıdaki kod, `Membership` sınıfının `GetUser` yöntemini çağırarak, şu anda oturum açmış olan kullanıcıya bir başvuru edinerek başlar. Bu, `ProviderUserKey` özelliği `UserId`içeren bir `MembershipUser` nesnesi döndürür. `UserId` değeri daha sonra SqlDataSource 'un `@UserId` parametresine atanır.

> [!NOTE]
> `Membership.GetUser()` yöntemi şu anda oturum açmış olan kullanıcı hakkında bilgi döndürür. Anonim bir Kullanıcı sayfayı ziyaret ettiğse, `null`bir değer döndürür. Böyle bir durumda, bu, `ProviderUserKey` özelliğini okumaya çalışırken aşağıdaki kod satırında bir `NullReferenceException` yol açacaktır. Tabii ki, önceki bir öğreticide URL yetkilendirmesi yapılandırdığımız ve bu klasördeki ASP.NET kaynaklarına yalnızca kimliği doğrulanmış kullanıcıların erişebileceği için, `AdditionalUserInfo.aspx` sayfada bir `null` değeri döndürtiğimiz `Membership.GetUser()` endişelenmemiz gerekmiyor. Şu anda oturum açmış olan kullanıcıyla ilgili bilgilere anonim erişime izin verilen bir sayfada erişmeniz gerekiyorsa, özelliklerine başvurulmadan önce `GetUser()` yönteminden`null MembershipUser` olmayan bir nesnenin döndürüldüğünü kontrol ettiğinizden emin olun.

`AdditionalUserInfo.aspx` sayfasını bir tarayıcıda ziyaret ederseniz boş bir sayfa görürsünüz, çünkü henüz `UserProfiles` tablosuna herhangi bir satır eklememiz gerekir. Adım 6 ' da, yeni bir kullanıcı hesabı oluşturulduğunda `UserProfiles` tablosuna otomatik olarak yeni bir satır eklemek için CreateUserWizard denetimini nasıl özelleştireceğinizi inceleyeceğiz. Ancak şimdilik, tabloda el ile bir kayıt oluşturmanız gerekecektir.

Visual Studio 'daki Veritabanı Gezgini gidin ve Tablolar klasörünü genişletin. `aspnet_Users` tabloya sağ tıklayın ve tablodaki kayıtları görmek için "tablo verilerini göster" i seçin; `UserProfiles` tablosu için aynı şeyi yapın. Şekil 11 dikey olarak döşeli olduğunda bu sonuçları gösterir. My veritabanımda, şu anda deneme CE, Fred ve Tito için kayıt `aspnet_Users`, ancak `UserProfiles` tablosunda hiçbir kayıt yok.

[aspnet_Users ve UserProfiles tablolarının Içeriğini ![görüntülenir](storing-additional-user-information-cs/_static/image32.png)](storing-additional-user-information-cs/_static/image31.png)

**Şekil 11**: `aspnet_Users` ve `UserProfiles` tablolarının içerikleri görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image33.png))

`HomeTown`, `HomepageUrl`ve `Signature` alanları için değerleri el ile yazarak `UserProfiles` tabloya yeni bir kayıt ekleyin. Yeni `UserProfiles` kaydında geçerli bir `UserId` değeri almanın en kolay yolu `aspnet_Users` tablosundaki belirli bir kullanıcı hesabından `UserId` alanını seçmek ve bunu kopyalayıp `UserId` alanına yapıştırmaktır.`UserProfiles` Şekil 12 ' de, deneme için yeni bir kayıt eklendikten sonra `UserProfiles` tablosu gösterilmektedir.

[![deneme için UserProfiles 'a bir kayıt eklendi](storing-additional-user-information-cs/_static/image35.png)](storing-additional-user-information-cs/_static/image34.png)

**Şekil 12**: deneme ce için `UserProfiles` bir kayıt eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image36.png))

`AdditionalUserInfo.aspx` sayfasına dönüp, deneme olarak oturum açar. Şekil 13 ' ün gösterdiği gibi, deneme 'un ayarları görüntülenir.

[![Şu anda ziyaret eden Kullanıcı ayarları gösteriliyor](storing-additional-user-information-cs/_static/image38.png)](storing-additional-user-information-cs/_static/image37.png)

**Şekil 13**: Şu anda ziyaret eden Kullanıcı ayarları gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image39.png))

> [!NOTE]
> Tüm üyelik kullanıcıları için `UserProfiles` tablosuna gidin ve kayıtları el ile ekleyin. Adım 6 ' da, yeni bir kullanıcı hesabı oluşturulduğunda `UserProfiles` tablosuna otomatik olarak yeni bir satır eklemek için CreateUserWizard denetimini nasıl özelleştireceğinizi inceleyeceğiz.

## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>3\. Adım: kullanıcının ev Town, giriş sayfası ve Imzasını düzenlemesine Izin verme

Bu noktada, şu anda oturum açmış olan Kullanıcı kendi giriş kasalarını, giriş sayfasını ve imza ayarlarını görüntüleyebilir, ancak onları henüz değiştiremezler. DetailsView denetimini, verilerin düzenlenebilmesi için güncelleştirelim.

Yapmanız gereken ilk şey, SqlDataSource için bir `UpdateCommand` eklemektir, yürütülecek `UPDATE` bildirisini ve karşılık gelen parametrelerini belirterek. SqlDataSource ' ı seçin ve ardından Özellikler penceresi UpdateQuery özelliğinin yanındaki üç nokta işaretine tıklayarak komut ve parametre Düzenleyicisi iletişim kutusunu açın. Metin kutusuna aşağıdaki `UPDATE` ifadesini girin:

[!code-sql[Main](storing-additional-user-information-cs/samples/sample3.sql)]

Sonra, `UPDATE` deyimindeki parametrelerin her biri için SqlDataSource denetiminin `UpdateParameters` koleksiyonunda bir parametre oluşturacak "parametreleri Yenile" düğmesine tıklayın. Tüm parametrelerin kaynağını yok olarak bırakın ve Tamam düğmesine tıklayarak iletişim kutusunu doldurun.

[![SqlDataSource 'un UpdateCommand ve UpdateParameters 'ı belirtin](storing-additional-user-information-cs/_static/image41.png)](storing-additional-user-information-cs/_static/image40.png)

**Şekil 14**: SqlDataSource 'un `UpdateCommand` ve `UpdateParameters` belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image42.png))

SqlDataSource denetimine yaptığımız eklemeler nedeniyle, DetailsView denetimi artık düzenlemeleri destekleyebilir. DetailsView 'un akıllı etiketinde "Düzenle özelliğini etkinleştir" onay kutusunu işaretleyin. Bu, denetimin `Fields` koleksiyonuna `ShowEditButton` özelliği true olarak ayarlanmış bir CommandField ekler. Bu, DetailsView salt okuma modunda görüntülenirken ve düzenleme modunda görüntülendiğinde güncelleştir ve Iptal düğmeleri olduğunda bir düzenleme düğmesi oluşturur. Kullanıcının Düzenle ' ye tıklamasına gerek kalmadan, DetailsView denetiminin [`DefaultMode` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx) `Edit`olarak ayarlayarak DetailsView 'un "her zaman düzenlenebilir" durumda işlemesini sağlayabilirsiniz.

Bu değişikliklerle, DetailsView denetiminizin bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample4.aspx)]

CommandField ve `DefaultMode` özelliğinin eklenmesini aklınızda edin.

Devam edin ve bu sayfayı bir tarayıcı üzerinden test edin. `UserProfiles`ilgili kayda sahip bir kullanıcıyla ziyaret edildiğinde, kullanıcının ayarları düzenlenebilir bir arabirimde görüntülenir.

[DetailsView ![düzenlenebilir bir arabirim oluşturur](storing-additional-user-information-cs/_static/image44.png)](storing-additional-user-information-cs/_static/image43.png)

**Şekil 15**: DetailsView düzenlenebilir bir arabirim işler ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image45.png))

Değerleri değiştirmeyi ve Güncelleştir düğmesine tıklayarak deneyin. Hiçbir şey olmuyor gibi görünür. Bir geri gönderme vardır ve değerler veritabanına kaydedilir, ancak bu, kaydetme işlemi meydana gelen bir görsel geri bildirim yoktur.

Bu sorunu gidermek için, Visual Studio 'ya dönün ve DetailsView 'un üzerine bir etiket denetimi ekleyin. `ID` `SettingsUpdatedMessage`, `Text` özelliğini "ayarlarınız güncelleştirildi" olarak ayarlayın ve `Visible` ve `EnableViewState` özelliklerini `false`.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample5.aspx)]

DetailsView her güncelleştirildiğinde `SettingsUpdatedMessage` etiketini görüntüliyoruz. Bunu gerçekleştirmek için, DetailsView 'un `ItemUpdated` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample6.cs)]

Bir tarayıcı aracılığıyla `AdditionalUserInfo.aspx` sayfasına dönün ve verileri güncelleştirin. Bu kez, yararlı bir durum iletisi görüntülenir.

[Ayarlar güncelleştirilirken kısa bir Ileti ![görüntülenir](storing-additional-user-information-cs/_static/image47.png)](storing-additional-user-information-cs/_static/image46.png)

**Şekil 16**: ayarlar güncelleştirilirken kısa mesaj görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image48.png))

> [!NOTE]
> DetailsView denetiminin düzen arabirimi istenildiği kadar çok kalır. Standart boyutlu Textboxes kullanır, ancak Imza alanı muhtemelen çok satırlı bir metin kutusu olmalıdır. RegularExpressionValidator, giriş sayfası URL 'sinin girilmişse "http://" veya "https://" ile başlamasını sağlamak için kullanılmalıdır. Üstelik, DetailsView denetiminin `DefaultMode` özelliği `Edit`olarak ayarlanmış olduğundan, Iptal düğmesi hiçbir şey yapmaz. Kaldırılması gerekir ya da tıklandığında, kullanıcıyı başka bir sayfaya (örneğin, `~/Default.aspx`) yeniden yönlendirin. Bu geliştirmeleri okuyucu için bir alıştırma olarak bırakıyorum.

### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>Ana sayfadaki`AdditionalUserInfo.aspx`sayfasına bağlantı ekleme

Şu anda Web sitesi `AdditionalUserInfo.aspx` sayfasına herhangi bir bağlantı sağlamıyor. Buna ulaşmak için tek yol sayfanın URL 'sini doğrudan tarayıcının adres çubuğuna girmelidir. `Site.master` ana sayfasında bu sayfanın bağlantısını ekleyelim.

Ana sayfanın, `LoginContent` ContentPlaceHolder öğesinde, kimliği doğrulanmış ve anonim ziyaretçiler için farklı biçimlendirme görüntüleyen bir LoginView Web denetimi içerdiğini hatırlayın. `AdditionalUserInfo.aspx` sayfasına bir bağlantı eklemek için LoginView denetiminin `LoggedInTemplate` güncelleştirin. Bu değişiklikleri yaptıktan sonra, LoginView denetiminin bildirim temelli işaretleme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample7.aspx)]

`lnkUpdateSettings` köprü denetimini `LoggedInTemplate`eklemeyi dikkate alın. Bu bağlantıyla birlikte, kimliği doğrulanmış kullanıcılar giriş kasalarını, giriş sayfasını ve imza ayarlarını görüntülemek ve değiştirmek için sayfaya hızlıca atlayabilirler.

## <a name="step-4-adding-new-guestbook-comments"></a>4\. Adım: yeni Konuk defteri açıklamaları ekleme

`Guestbook.aspx` sayfası, kimliği doğrulanmış kullanıcıların Konuk defteri 'ni görüntüleyebileceği ve bir yorum bırakabileceği yerdir. Yeni Konuk defteri açıklamaları eklemek için arabirimi oluşturmaya başlayalım.

Visual Studio 'da `Guestbook.aspx` sayfasını açın ve biri yeni açıklamanın konusu ve gövdesi için olmak üzere iki metin kutusu denetimlerinden oluşan bir kullanıcı arabirimi oluşturun. İlk TextBox denetiminin `ID` özelliğini `Subject` ve `Columns` özelliğini 40 olarak ayarlayın; İkincinin `ID` `Body`, `TextMode` `MultiLine`ve `Width` ve `Rows` özelliklerini sırasıyla "95%" ve 8 "olarak ayarlayın. Kullanıcı arabirimini gerçekleştirmek için, `PostCommentButton` adlı bir düğme web denetimi ekleyin ve `Text` özelliğini "yorumunuzu gönder" olarak ayarlayın.

Her konuk defteri yorumu bir konu ve gövde gerektirdiğinden her metin kutularının her biri için bir RequiredFieldValidator ekleyin. Bu denetimlerin `ValidationGroup` özelliğini "EnterComment" olarak ayarlayın; benzer şekilde, `PostCommentButton` denetiminin `ValidationGroup` özelliğini "EnterComment" olarak ayarlayın. ASP.net hakkında daha fazla bilgi için. NET ' in doğrulama denetimleri, [ASP.NET 2,0 ' deki doğrulama denetimlerini](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)ve doğrulama sunucusu [w3schools](http://www.w3schools.com/)üzerindeki [öğreticiyi denetleyen](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp) [ASP.net 'de form doğrulamayı](http://www.4guysfromrolla.com/webtech/090200-1.shtml)inceleyin.

Kullanıcı arabirimini oluşturduktan sonra sayfanızın bildirime dayalı biçimlendirmesi aşağıdakine benzer şekilde görünmelidir:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample8.aspx)]

Kullanıcı arabirimi tamamlandığında bir sonraki göreviniz, `PostCommentButton` tıklandığında `GuestbookComments` tabloya yeni bir kayıt eklemedir. Bu, çeşitli yollarla gerçekleştirilebilir: düğmenin `Click` olay işleyicisine ADO.NET kodu yazalım. sayfaya bir SqlDataSource denetimi ekleyebiliyoruz, `InsertCommand`yapılandırıp `Insert` yöntemini `Click` olay işleyicisinden çağırabiliriz; ya da yeni Konuk defteri açıklamalarını eklemekten sorumlu bir orta katman oluşturabilir ve bu işlevselliği `Click` olay işleyicisinden çağırabiliriz. Adım 3 ' te bir SqlDataSource kullanmaya baktığı için burada ADO.NET kodunu kullanalım.

> [!NOTE]
> Microsoft SQL Server veritabanından verilere programlı bir şekilde erişmek için kullanılan ADO.NET sınıfları `System.Data.SqlClient` ad alanında bulunur. Bu ad alanını sayfanızın arka plan kod sınıfına (yani, `using System.Data.SqlClient;`) içeri aktarmanız gerekebilir.

`PostCommentButton``Click` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample9.cs)]

`Click` olay işleyicisi, Kullanıcı tarafından sağlanan verilerin geçerli olup olmadığını denetleyerek başlar. Değilse, kayıt eklemeden önce olay işleyicisi çıkar. Sağlanan verilerin geçerli olduğu varsayıldığında, şu anda oturum açmış olan kullanıcının `UserId` değeri alınır ve `currentUserId` yerel değişkeninde depolanır. Bu değer, `GuestbookComments`bir kayıt eklerken `UserId` bir değer sağlamaları gerektiğinden gereklidir.

Bundan sonra, `SecurityTutorials` veritabanı için bağlantı dizesi `Web.config` alınır ve `INSERT` SQL ifadesiyle belirtilir. Daha sonra bir `SqlConnection` nesnesi oluşturulup açılır. Sonra, bir `SqlCommand` nesnesi oluşturulur ve `INSERT` sorgusunda kullanılan parametrelerin değerleri atanır. `INSERT` deyimleri yürütülür ve bağlantı kapatılır. Olay işleyicisinin sonunda, Kullanıcı değerlerinin geri göndermede kalıcı olmaması için `Subject` ve `Body` TextBoxes ' `Text` özellikleri temizlenir.

Devam edin ve bu sayfayı bir tarayıcıda test edin. Bu sayfa `Membership` klasörde olduğundan, anonim ziyaretçilerin erişimine açık değildir. Bu nedenle, önce oturum açmanız gerekir (henüz yoksa). `Subject` ve `Body` metin kutularına bir değer girin ve `PostCommentButton` düğmesine tıklayın. Bu, `GuestbookComments`yeni bir kaydın eklenmesine neden olur. Geri göndermede, verdiğiniz konu ve gövde, metin kutularına silinir.

`PostCommentButton` düğmesine tıkladıktan sonra, yorumun konuk defterine eklendiği görsel geri bildirimde bulunmamıştı. Yine de bu sayfayı, 5. adımda yapacağız mevcut Konuk defteri açıklamalarını göstermek için güncelleştirmemiz gerekiyor. Bunu başardıktan sonra, yeterli görsel geribildirim sağlayan, yeni eklenen açıklama açıklama listesinde görünür. Şimdilik, `GuestbookComments` tablosunun içeriğini inceleyerek, Konuk defteri yorumlarınızın kaydedildiğinden emin olun.

Şekil 17 ' de, iki yorum ayrıldıktan sonra `GuestbookComments` tablosunun içerikleri gösterilmektedir.

[![GuestbookComments tablosunda Konuk defteri açıklamalarını görebilirsiniz](storing-additional-user-information-cs/_static/image50.png)](storing-additional-user-information-cs/_static/image49.png)

**Şekil 17**: `GuestbookComments` tablosunda Konuk defteri açıklamalarını görebilirsiniz ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image51.png))

> [!NOTE]
> Bir Kullanıcı, olası tehlikeli biçimlendirme içeren bir konuk defteri açıklaması eklemeye çalışırsa (HTML – ASP.NET gibi) bir `HttpRequestValidationException`oluşturur. Bu özel durum hakkında daha fazla bilgi edinmek için neden oluşturulduğu ve kullanıcıların potansiyel olarak tehlikeli değerler göndermesine izin verme hakkında daha fazla bilgi edinmek için [Istek doğrulama teknik incelemesine](../../../../whitepapers/request-validation.md)başvurun.

## <a name="step-5-listing-the-existing-guestbook-comments"></a>5\. Adım: mevcut Konuk defteri açıklamalarını listeleme

Açıklamaları bırakmanın yanı sıra, `Guestbook.aspx` sayfasını ziyaret eden bir Kullanıcı de konuk defteri 'nin varolan açıklamalarını görüntüleyebilmelidir. Bunu gerçekleştirmek için, sayfanın en altına `CommentList` adlı bir ListView denetimi ekleyin.

> [!NOTE]
> ListView denetimi ASP.NET sürüm 3,5 ' e yenidir. Çok özelleştirilebilir ve esnek bir düzende öğelerin listesini görüntüleyecek, ancak yine de GridView gibi yerleşik düzenleme, ekleme, silme, sayfalama ve sıralama işlevlerini sunmaya yönelik olarak tasarlanmıştır. ASP.NET 2,0 kullanıyorsanız, bunun yerine DataList veya Repeater denetimini kullanmanız gerekir. ListView 'u kullanma hakkında daha fazla bilgi için bkz. [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin blog girdisi, [ASP: ListView denetimi](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)ve My article, [ListView denetimiyle verileri görüntüleme](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx).

ListView 'un akıllı etiketini açın ve veri kaynağı seç açılan listesinden denetimi yeni bir veri kaynağına bağlayın. 2\. adımda gördüğünüz gibi, bu işlem veri kaynağı Yapılandırma Sihirbazı 'nı başlatacaktır. Veritabanı simgesini seçin, sonuçta elde edilen SqlDataSource `CommentsDataSource`adlandırın ve Tamam ' a tıklayın. Sonra, açılan listeden `SecurityTutorialsConnectionString` bağlantı dizesini seçin ve Ileri ' ye tıklayın.

2\. adımdaki bu noktada, açılan listeden `UserProfiles` tablosunu seçip döndürülecek sütunları seçerek Sorgulanacak verileri belirttik (Şekil 9 ' a geri başvurabilirsiniz). Ancak, bu kez yalnızca `GuestbookComments`kayıtları değil, aynı zamanda yorum ana şehir, giriş sayfası, imza ve Kullanıcı adı gibi bir SQL ifadesini geri çeker. Bu nedenle, "özel bir SQL ifadesini veya saklı yordamı belirtin" radyo düğmesini seçin ve Ileri ' ye tıklayın.

Bu, "özel deyimleri veya saklı yordamları tanımla" ekranını getirir. Sorguyu grafik olarak oluşturmak için Sorgu Tasarımcısı düğmesine tıklayın. Sorgu Tasarımcısı, sorgu yapmak istediğimiz tabloları belirtmemizi isteyerek başlar. `GuestbookComments`, `UserProfiles`ve `aspnet_Users` tabloları seçip Tamam ' a tıklayın. Bu, üç tabloyu Tasarım yüzeyine ekler. `GuestbookComments`, `UserProfiles`ve `aspnet_Users` tabloları arasında yabancı anahtar kısıtlamaları olduğundan, Sorgu Tasarımcısı bu tabloları otomatik olarak `JOIN`.

Kalan şey döndürülecek sütunları belirtmektir. `GuestbookComments` tablosundan `Subject`, `Body`ve `CommentDate` sütunlarını seçin; `UserProfiles` tablosundan `HomeTown`, `HomepageUrl`ve `Signature` sütunları döndürün; ve `aspnet_Users``UserName` döndürün. Ayrıca, en son postaların ilk döndürülmesi için `SELECT` sorgusunun sonuna "`ORDER BY CommentDate DESC`" ekleyin. Bu seçimleri yaptıktan sonra, Sorgu Tasarımcısı arabiriminiz, Şekil 18 ' de ekran görüntüsüne benzer görünmelidir.

[Oluşturulan sorgu GuestbookComments, UserProfiles ve aspnet_Users tablolarına katılır ![](storing-additional-user-information-cs/_static/image53.png)](storing-additional-user-information-cs/_static/image52.png)

**Şekil 18**: oluşturulan sorgu `GuestbookComments`, `UserProfiles`ve `aspnet_Users` tabloları `JOIN` ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image54.png))

Sorgu Tasarımcısı penceresini kapatmak ve "özel deyimleri veya saklı yordamları tanımla" ekranına geri dönmek için Tamam ' ı tıklatın. Sorgu sonuçlarını test sorgu düğmesine tıklayarak görüntüleyebileceğiniz "test sorgusu" ekranına ilerlemek için Ileri ' ye tıklayın. Hazırsanız, veri kaynağı Yapılandırma Sihirbazı 'nı gerçekleştirmek için son ' a tıklayın.

2\. adımdaki veri kaynağını yapılandırma Sihirbazı 'nı tamamladığımızda, ilişkili DetailsView denetiminin `Fields` koleksiyonu, `SelectCommand`tarafından döndürülen her bir sütun için bir BoundField eklemek üzere güncelleştirildi. Ancak ListView değişmeden kalır; Hala yerleşimini tanımlamanız gerekiyor. ListView 'un düzeni, bildirim temelli biçimlendirme veya akıllı etiketindeki "ListView yapılandırma" seçeneğinden el ile oluşturulabilir. Genellikle biçimlendirmeyi el ile tanımlamayı tercih ediyorum, ancak sizin için en doğal yöntemi kullanın.

ListView denetimi için aşağıdaki `LayoutTemplate`, `ItemTemplate`ve `ItemSeparatorTemplate` kullanarak bitiririm:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample10.aspx)]

`LayoutTemplate`, denetimin verdiği biçimlendirmeyi tanımlar, `ItemTemplate` SqlDataSource tarafından döndürülen her öğeyi işler. `ItemTemplate`ortaya çıkan biçimlendirme `LayoutTemplate``itemPlaceholder` denetimine yerleştirilir. `itemPlaceholder`ek olarak, `LayoutTemplate`, ListView 'u sayfa başına yalnızca 10 Konuk defteri açıklaması (varsayılan) gösterecek şekilde sınırlayan ve bir sayfalama arabirimi işleyen bir DataPager denetimi içerir.

`ItemTemplate`, her konuk defteri yorumunu konunun altında bulunan gövdedeki bir `<h4>` öğesinde görüntüler. Gövdeyi görüntülemek için kullanılan sözdiziminin `Eval("Body")` DataBinding ifadesinin döndürdüğü verileri aldığını, dizeyi bir dizeye dönüştürdüğüne ve satır sonlarını `<br />` öğesiyle değiştirdiğine unutmayın. Bu dönüştürme, boşluk HTML tarafından yoksayıldığından yorumu gönderirken girilen satır sonlarını göstermek için gereklidir. Kullanıcının imzası, bir kullanıcının giriş Town, ana sayfasının bir bağlantısı, yorumun yapıldığı tarih ve saat ve yorumu kapatan kişinin Kullanıcı adı tarafından görüntülenir.

Sayfayı bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Burada görüntülenen 5. adımda bulunan konuk defterine eklediğiniz açıklamaları görmeniz gerekir.

[![Konuk defteri. aspx artık Konuk defteri açıklamalarını görüntülüyor](storing-additional-user-information-cs/_static/image56.png)](storing-additional-user-information-cs/_static/image55.png)

**Şekil 19**: `Guestbook.aspx` artık Konuk defteri 'Nin açıklamalarını görüntülüyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image57.png))

Konuk defterine yeni bir açıklama eklemeyi deneyin. `PostCommentButton` düğmesine tıklandıktan sonra sayfa geri gönderilir ve açıklama veritabanına eklenir, ancak ListView denetimi yeni yorumu gösterecek şekilde güncellenmez. Bu, aşağıdakilerden biri tarafından düzeltilebilir:

- Yeni açıklamayı veritabanına ekledikten sonra ListView denetiminin `DataBind()` yöntemini çağırabilmesi için `PostCommentButton` düğmenin `Click` olay işleyicisini güncelleştirme veya
- ListView denetiminin `EnableViewState` özelliği `false`olarak ayarlanıyor. Bu yaklaşım, denetimin görünüm durumunu devre dışı bırakarak, her geri göndermede temel alınan verileri yeniden bağlamanız gerekir.

Bu öğreticiden indirilebilir öğretici Web sitesi her iki tekniği de gösterir. ListView denetiminin `EnableViewState` `false` özelliği ve verileri ListView 'e programlı olarak yeniden bağlamak için gereken kod `Click` olay işleyicisinde mevcuttur, ancak açıklama eklenir.

> [!NOTE]
> Şu anda `AdditionalUserInfo.aspx` sayfası kullanıcının ev kasalarını, giriş sayfasını ve imza ayarlarını görüntülemesine ve düzenlemesine izin verir. Oturum açmış kullanıcının Konuk defteri açıklamalarını görüntülemesi `AdditionalUserInfo.aspx` güncelleştirmek iyi olabilir. Diğer bir deyişle, bilgilerini İnceleme ve değiştirme özelliklerinin yanı sıra, bir Kullanıcı geçmişte hangi Konuk defteri açıklamalarını yaptığını görmek için `AdditionalUserInfo.aspx` sayfasını ziyaret edebilir. Bunu ilgilendiğiniz okuyucu için bir alıştırma olarak bırakıyorum.

## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>6\. Adım: CreateUserWizard denetimini ev Town, ana sayfa ve Imza için bir arabirim Içerecek şekilde özelleştirme

`Guestbook.aspx` sayfasında kullanılan `SELECT` sorgusu, `GuestbookComments`, `UserProfiles`ve `aspnet_Users` tabloları arasında ilişkili kayıtları birleştirmek için bir `INNER JOIN` kullanır. `UserProfiles` kaydı olmayan bir Kullanıcı Konuk defteri yorumu yaptığında, `INNER JOIN` yalnızca `UserProfiles` ve `aspnet_Users`eşleşen kayıtlar olduğunda `GuestbookComments` kayıtlar döndürdüğünden açıklama ListView 'da gösterilmez. Adım 3 ' te gördüğümüz bir Kullanıcı `UserProfiles` içinde bir kayıt yoksa, `AdditionalUserInfo.aspx` sayfasındaki ayarlarını görüntüleyemez veya düzenleyemez.

, Tasarım kararlarımız nedeniyle, üyelik sistemindeki her kullanıcı hesabının `UserProfiles` tablosunda eşleşen bir kayda sahip olması önemlidir. CreateUserWizard aracılığıyla her yeni üyelik kullanıcı hesabı oluşturulduğunda `UserProfiles`, ilgili kaydın eklenmesi için ne istiyoruz.

[*Kullanıcı hesapları oluşturma*](creating-user-accounts-cs.md) öğreticisinde açıklandığı gibi, yeni üyelik kullanıcı hesabı oluşturulduktan sonra, CreateUserWizard denetimi [`CreatedUser` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx)başlatır. Bu olay için bir olay işleyicisi oluşturabilir, yeni oluşturulan kullanıcıya yönelik kullanıcı kimliğini alabilir ve ardından `UserProfiles` tabloya `HomeTown`, `HomepageUrl`ve `Signature` sütunları için varsayılan değerleri içeren bir kayıt ekleyebilirsiniz. Ayrıca, CreateUserWizard denetiminin arabirimini ek TextBoxes dahil etmek üzere özelleştirerek kullanıcıya bu değerleri istemek mümkündür.

İlk olarak, `CreatedUser` olay işleyicisindeki `UserProfiles` tablosuna varsayılan değerlerle yeni bir satır ekleme bölümüne bakalım. Bunun için, CreateUserWizard denetiminin Kullanıcı arabirimini, yeni kullanıcının ev kasasından, ana sayfasına ve imzasına toplanacak ek form alanları içerecek şekilde nasıl özelleştireceğiz.

### <a name="adding-a-default-row-touserprofiles"></a>`UserProfiles` varsayılan satır ekleme

[*Kullanıcı hesapları oluşturma*](creating-user-accounts-cs.md) öğreticisinde, `Membership` klasöründeki `CreatingUserAccounts.aspx` sayfasına bir CreateUserWizard denetimi ekledik. CreateUserWizard denetiminin Kullanıcı hesabı oluşturulduktan sonra `UserProfiles` tabloya bir kayıt eklemesini sağlamak için, CreateUserWizard denetiminin işlevselliğini güncelleştirmemiz gerekir. `CreatingUserAccounts.aspx` sayfasında bu değişiklikleri yapmak yerine `EnhancedCreateUserWizard.aspx` sayfasına yeni bir CreateUserWizard denetimi ekleyip bu öğreticide Bu öğreticiye yönelik değişiklikleri yapabilirsiniz.

Visual Studio 'da `EnhancedCreateUserWizard.aspx` sayfasını açın ve araç kutusundan bir CreateUserWizard denetimi sayfaya sürükleyin. CreateUserWizard denetiminin `ID` özelliğini `NewUserWizard`olarak ayarlayın. <a id="_msoanchor_5"> </a> [*Kullanıcı hesapları oluşturma*](creating-user-accounts-cs.md) öğreticisinde anlatıldığı gibi, CreateUserWizard 'in varsayılan kullanıcı arabirimi ziyaretçiye gerekli bilgileri ister. Bu bilgiler sağlandığında denetim, üyelik çerçevesinde dahili olarak yeni bir kullanıcı hesabı oluşturur, tek bir kod satırı yazmak zorunda kalmamalıdır.

CreateUserWizard denetimi, iş akışı sırasında birkaç olay oluşturur. Bir ziyaretçi istek bilgilerini girdikten ve formu gönderdikten sonra, CreateUserWizard denetimi başlangıçta [`CreatingUser` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)harekete tetikler. Oluşturma işlemi sırasında bir sorun varsa [`CreateUserError` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) tetiklenir; Ancak, Kullanıcı başarıyla oluşturulduysa [`CreatedUser` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) tetiklenir. <a id="_msoanchor_6"> </a> [*Kullanıcı hesapları oluşturma*](creating-user-accounts-cs.md) öğreticisinde, sağlanan kullanıcı adının başında veya sonunda boşluk içermediğinden ve Kullanıcı adının parolada herhangi bir yerde görünmediğinden emin olmak için `CreatingUser` olayı için bir olay işleyicisi oluşturduk.

Yeni oluşturulan kullanıcının `UserProfiles` tablosuna bir satır eklemek için, `CreatedUser` olayı için bir olay işleyicisi oluşturmanız gerekir. `CreatedUser` olayın tetiklenme zamanına göre, Kullanıcı hesabı üyelik çerçevesinde zaten oluşturulmuştur ve hesabın UserID değerini almamızı sağlar.

`NewUserWizard``CreatedUser` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample11.cs)]

Yukarıdaki kod, yeni eklenen Kullanıcı hesabının kullanıcı kimliğini alarak oluşur. Bu, belirli bir kullanıcı hakkında bilgi döndürmek için `Membership.GetUser(username)` yöntemi kullanılarak ve sonra Kullanıcı kimliğini almak için `ProviderUserKey` özelliğini kullanarak gerçekleştirilir. CreateUserWizard denetimindeki kullanıcı tarafından girilen Kullanıcı adı [`UserName` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx)aracılığıyla kullanılabilir.

Sonra bağlantı dizesi `Web.config` alınır ve `INSERT` ifade belirtilir. Gerekli ADO.NET nesneleri örneklenmiştir ve komut yürütülür. Kod, `NULL`, `HomeTown`ve `HomepageUrl`alanları için veritabanı `Signature` değerleri ekleme etkisi olan `@HomeTown`, `@HomepageUrl`ve `@Signature` parametrelerine [`DBNull`](https://msdn.microsoft.com/library/system.dbnull.aspx) bir örnek atar.

`EnhancedCreateUserWizard.aspx` sayfasını bir tarayıcıda ziyaret edin ve yeni bir kullanıcı hesabı oluşturun. Bunu yaptıktan sonra Visual Studio 'ya dönün ve `aspnet_Users` ve `UserProfiles` tablolarının içeriğini inceleyin (Şekil 12 ' de geri döntiğimiz gibi). Yeni Kullanıcı hesabını `aspnet_Users` ve karşılık gelen bir `UserProfiles` satırında görmeniz gerekir (`HomeTown`, `HomepageUrl`ve `Signature`için `NULL` değerleriyle).

[![yeni bir kullanıcı hesabı ve UserProfiles kaydı eklendi](storing-additional-user-information-cs/_static/image59.png)](storing-additional-user-information-cs/_static/image58.png)

**Şekil 20**: yeni bir kullanıcı hesabı ve `UserProfiles` kaydı eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image60.png))

Ziyaretçi yeni hesap bilgilerini girdikten ve "Kullanıcı Oluştur" düğmesine tıkladıktan sonra, Kullanıcı hesabı oluşturulur ve `UserProfiles` tablosuna bir satır eklenir. CreateUserWizard ardından, bir başarı iletisi ve devam düğmesi görüntüleyen `CompleteWizardStep`görüntüler. Devam düğmesine tıklamak geri göndermeye neden olur, ancak hiçbir işlem yapılmaz ve Kullanıcı `EnhancedCreateUserWizard.aspx` sayfasında takılmaya devam eder.

CreateUserWizard denetiminin [`ContinueDestinationPageUrl` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)aracılığıyla devam düğmesine tıklandığında kullanıcıyı göndermek IÇIN bir URL belirtebilirsiniz. `ContinueDestinationPageUrl` özelliğini "~/Membership/additionaluserınfo.aspx" olarak ayarlayın. Bu, yeni kullanıcıyı `AdditionalUserInfo.aspx`, ayarlarını görüntüleyebileceği ve güncelleştirebilecekleri şekilde alır.

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>Yeni kullanıcının ana Town, giriş sayfası ve Imzasını Istemek için CreateUserWizard 'in arabirimini özelleştirme

CreateUserWizard denetiminin varsayılan arabirimi, yalnızca Kullanıcı adı, parola ve e-posta için gereken çekirdek Kullanıcı hesabı bilgilerinin toplanması için yeterli olan basit hesap oluşturma senaryolarında yeterlidir. Ancak ziyaretçiye hesabı oluştururken ev kasasın, giriş sayfası ve imza girmesini istemek istiyorsam ne olacak? Kayıt sırasında ek bilgi toplamak için CreateUserWizard denetiminin arabirimini özelleştirmek mümkündür ve bu bilgiler temel alınan veritabanına ek kayıtlar eklemek için `CreatedUser` olay işleyicisinde kullanılabilir.

CreateUserWizard denetimi, sayfa geliştiricisinin bir dizi sıralı `WizardSteps`tanımlamasına izin veren bir denetim olan ASP.NET Sihirbazı denetimini genişletir. Sihirbaz denetimi etkin adımı işler ve ziyaretçinin bu adımlarla hareket etmesine izin veren bir gezinti arabirimi sağlar. Sihirbaz denetimi, uzun bir görevi birkaç kısa adıma bölmek için idealdir. Sihirbaz denetimi hakkında daha fazla bilgi için, bkz. [ASP.NET 2,0 sihirbaz denetimiyle adım adım kullanıcı arabirimi oluşturma](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx).

CreateUserWizard denetiminin varsayılan biçimlendirmesi iki `WizardSteps`tanımlar: `CreateUserWizardStep` ve `CompleteWizardStep`.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample12.aspx)]

İlk `WizardStep``CreateUserWizardStep`, Kullanıcı adı, parola, e-posta vb. için istemde bulunan arabirimi işler. Ziyaretçi bu bilgileri belirledikten ve "Kullanıcı Oluştur" seçeneğine tıkladıktan sonra, başarı iletisini ve devam düğmesini gösteren `CompleteWizardStep`gösterilir.

CreateUserWizard denetiminin arabirimini ek form alanları içerecek şekilde özelleştirmek için şunları yapabilirsiniz:

- <strong>Ek kullanıcı arabirimi öğelerini içerecek</strong> <strong>bir veya daha fazla yeni</strong> <strong>`WizardStep`</strong>s oluşturun. CreateUserWizard 'e yeni bir `WizardStep` eklemek için, `WizardStep` koleksiyonu düzenleyicisini başlatmak üzere akıllı etiketindeki "`WizardSteps`Ekle/Kaldır" bağlantısına tıklayın. Buradan, sihirbazdaki adımları ekleyebilir, kaldırabilir veya yeniden sıralayabilirsiniz. Bu öğreticide kullanacağınız yaklaşım budur.

- <strong>`CreateUserWizardStep`</strong> <strong>düzenlenebilir bir</strong> <strong>`WizardStep`</strong>dönüştürür <strong>.</strong> Bu, `CreateUserWizardStep`, biçimlendirmesi `CreateUserWizardStep`ile eşleşen bir kullanıcı arabirimini tanımlayan eşdeğer bir `WizardStep` ile değiştirir. `CreateUserWizardStep` bir `WizardStep` dönüştürerek, bu adıma denetimleri yeniden konumlandırabilirsiniz veya ek kullanıcı arabirimi öğeleri ekleyebilirsiniz. `CreateUserWizardStep` veya `CompleteWizardStep` düzenlenebilir bir `WizardStep`dönüştürmek için, denetimin akıllı etiketindeki "Kullanıcı oluşturma adımını Özelleştir" veya "tüm adımı Özelleştir" bağlantısını tıklatın.

- **Yukarıdaki iki seçenekten bir birleşimini kullanın.**

Göz önünde bulundurmanız gereken önemli bir şey, "Kullanıcı Oluştur" düğmesine `CreateUserWizardStep`içinden tıklandığı zaman CreateUserWizard denetiminin Kullanıcı hesabı oluşturma işlemini yürütmesidir. `CreateUserWizardStep` sonra ek `WizardStep` s ne olursa olsun.

Ek kullanıcı girişi toplamak için CreateUserWizard denetimine özel bir `WizardStep` eklerken, özel `WizardStep` `CreateUserWizardStep`önce veya sonra yerleştirilebilir. `CreateUserWizardStep` önce geliyorsa, özel `WizardStep` toplanan ek kullanıcı girişi `CreatedUser` olay işleyicisi için kullanılabilir. Ancak, özel `WizardStep` `CreateUserWizardStep` sonrasında özel `WizardStep` görüntülendiğinde, Yeni Kullanıcı hesabı zaten oluşturulmuştur ve `CreatedUser` olayı zaten tetiklendi.

Şekil 21, eklenen `WizardStep` `CreateUserWizardStep`önünde olduğunda iş akışını gösterir. Ek Kullanıcı bilgileri `CreatedUser` olayının tetiklendiği zamana göre toplandığı için, tüm yapmanız gereken `CreatedUser` olay işleyicisini bu girdileri almak ve `INSERT` deyimin parametre değerleri (`DBNull.Value`yerine) için kullanmak üzere güncelleştirmelerdir.

[Ek bir WizardStep, CreateUserWizardStep 'ten önce CreateUserWizard Iş akışını ![](storing-additional-user-information-cs/_static/image62.png)](storing-additional-user-information-cs/_static/image61.png)

**Şekil 21**: ek `WizardStep` `CreateUserWizardStep` önce ([tam boyutlu görüntüyü görüntülemek Için tıklayın](storing-additional-user-information-cs/_static/image63.png)) CreateUserWizard iş akışı

Ancak, özel `WizardStep` `CreateUserWizardStep`*sonra* yerleştirilmişse, Kullanıcı hesabı oluştur işlemi, kullanıcının ev Town, giriş sayfası veya imza girme şansı olmadan önce oluşur. Böyle bir durumda, Şekil 22 ' de gösterildiği gibi bu ek bilgilerin, Kullanıcı hesabı oluşturulduktan sonra veritabanına eklenmesi gerekir.

[CreateUserWizard Iş akışını, CreateUserWizardStep sonrasında ek bir WizardStep geldiğinde ![](storing-additional-user-information-cs/_static/image65.png)](storing-additional-user-information-cs/_static/image64.png)

**Şekil 22**: `CreateUserWizardStep` sonra ek `WizardStep` olduğunda CreateUserWizard iş akışı ([tam boyutlu görüntüyü görüntülemek için tıklatın](storing-additional-user-information-cs/_static/image66.png))

Şekil 22 ' de gösterilen iş akışı, 2. adım tamamlanana kadar `UserProfiles` tabloya bir kayıt eklemeyi bekler. Ancak, ziyaretçi 1. adımdan sonra tarayıcıyı kapatırsa, bir kullanıcı hesabının oluşturulduğu bir duruma ulaşacağız, ancak `UserProfiles`hiçbir kayıt eklenmedi. Bir geçici çözüm `CreatedUser` olay işleyicisine (1. adımdan sonra ateşlenir) `UserProfiles` eklenecek `NULL` veya varsayılan değerler içeren bir kayda sahip olmak ve 2. adım tamamlandıktan sonra bu kaydı güncelleştirmeniz gerekir. Bu, Kullanıcı kayıt işlemini Midway 'den kaldırsa bile Kullanıcı hesabı için bir `UserProfiles` kaydı eklenmesini sağlar.

Bu öğreticide, `CreateUserWizardStep` sonra, `CompleteWizardStep`önce gerçekleşen yeni bir `WizardStep` oluşturalım. İlk olarak WizardStep 'yi yerinde ve yapılandırılmış olarak öğreneceğiz ve ardından koda bakacağız.

CreateUserWizard denetiminin akıllı etiketinden sonra, `WizardStep` koleksiyon Düzenleyicisi iletişim kutusunu gösteren "`WizardStep` s Ekle/Kaldır" ı seçin. Yeni bir `WizardStep`ekleyin, `ID` `UserSettings`, `Title` "ayarlarınızı" ve `StepType` için `Step`olarak ayarlayarak. Ardından, Şekil 23 ' te gösterildiği gibi, `CreateUserWizardStep` ("yeni hesabınız için kaydolun") ve `CompleteWizardStep` ("Tamam") öncesi olacak şekilde konumlandırın.

[CreateUserWizard denetimine yeni bir WizardStep eklemek ![](storing-additional-user-information-cs/_static/image68.png)](storing-additional-user-information-cs/_static/image67.png)

**Şekil 23**: CreateUserWizard denetimine yeni bir `WizardStep` ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](storing-additional-user-information-cs/_static/image69.png))

`WizardStep` koleksiyon Düzenleyicisi iletişim kutusunu kapatmak için Tamam ' ı tıklatın. Yeni `WizardStep`, CreateUserWizard denetiminin güncelleştirilmiş bildirim temelli biçimlendirme tarafından belirlenir:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample13.aspx)]

Yeni `<asp:WizardStep>` öğesini aklınızda edin. Yeni kullanıcının giriş kasasından, giriş sayfasına ve imzasına toplanacak Kullanıcı arabirimini eklememiz gerekiyor. Bu içeriği bildirime dayalı söz dizimine veya tasarımcı aracılığıyla girebilirsiniz. Tasarımcıyı kullanmak için, tasarımcıda adımı görmek üzere akıllı etiketteki açılan listeden "ayarlarınız" adımını seçin.

> [!NOTE]
> Akıllı etiketin açılan listesinde bir adım seçtiğinizde, başlangıç adımının dizinini belirten CreateUserWizard denetiminin [`ActiveStepIndex` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)güncellenir. Bu nedenle, tasarımcıda "Ayarlar" adımını düzenlemek için bu açılan listeyi kullanırsanız, kullanıcılar `EnhancedCreateUserWizard.aspx` sayfasını ilk kez ziyaret ettiğinde bu adımın gösterilmesi için, bu açılan listeyi "yeni hesabınız için kaydolun" olarak ayarladığınızdan emin olun.

`HomeTown`, `HomepageUrl`ve `Signature`adlı üç TextBox denetimi içeren "ayarlarınız" adımındaki bir kullanıcı arabirimi oluşturun. Bu arabirim oluşturulduktan sonra, CreateUserWizard 'in bildirime dayalı biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample14.aspx)]

Devam edin ve bu sayfayı bir tarayıcı aracılığıyla ziyaret edin ve giriş Town, giriş sayfası ve imza değerlerini belirterek yeni bir kullanıcı hesabı oluşturun. `CreateUserWizardStep` tamamladıktan sonra, Kullanıcı hesabı üyelik çerçevesinde oluşturulur ve `CreatedUser` olay işleyicisi çalışır ve bu, `UserProfiles`yeni bir satır ekler ve `HomeTown`, `HomepageUrl`ve `Signature`için bir veritabanı `NULL` değeri ile. Ev şehir, giriş sayfası ve imza için girilen değerler hiçbir şekilde kullanılmaz. Net sonuç, `HomeTown`, `HomepageUrl`ve `Signature` alanları henüz belirtilmemiş `UserProfiles` kaydıyla yeni bir kullanıcı hesabıdır.

Kullanıcı tarafından girilen ev kasasıdır, honepage ve imza değerlerini alan ve uygun `UserProfiles` kaydını güncelleştiren "ayarlarınız" adımından sonra kodu yürütmemiz gerekir. Bir sihirbaz denetimindeki adımlar arasında Kullanıcı her hareket ettirildiğinde, sihirbazın [`ActiveStepChanged` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx) ateşlenir. Bu olay için bir olay işleyicisi oluşturabilir ve "ayarlarınız" adımı tamamlandığında `UserProfiles` tablosunu güncelleştirebilirsiniz.

CreateUserWizard 'ın `ActiveStepChanged` olayı için bir olay işleyicisi ekleyin ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample15.cs)]

Yukarıdaki kod, "tam" adıma ulaşdığımızda belirlenir. "Tam" adım "ayarlarınız" adımından hemen sonra gerçekleşmesinden sonra, ziyaretçi "tam" adıma ulaştığında "ayarlarınız" adımını tamamlamış demektir.

Böyle bir durumda, `UserSettings WizardStep`içindeki TextBox denetimlerine programlı bir şekilde başvuracağız. Bu, önce `UserSettings WizardStep`programlı olarak başvurmak için `FindControl` yöntemi kullanılarak ve sonra da `WizardStep`içinden metin kutularına başvurulmaya karşı yapılır. Metin kutularına başvurulduktan sonra `UPDATE` ifadesini yürütmeye hazırız. `UPDATE` deyimin `CreatedUser` olay işleyicisindeki `INSERT` ifadesiyle aynı sayıda parametresi vardır, ancak burada Kullanıcı tarafından sağlanan giriş Town, giriş sayfası ve imza değerlerini kullanırız.

Bu olay işleyicisi yerine, bir tarayıcı aracılığıyla `EnhancedCreateUserWizard.aspx` sayfasını ziyaret edin ve ev Town, giriş sayfası ve imza değerlerini belirten yeni bir kullanıcı hesabı oluşturun. Yeni hesap oluşturulduktan sonra, tam olarak girilen giriş kasasındaki, giriş sayfasının ve imza bilgilerinin görüntülendiği `AdditionalUserInfo.aspx` sayfasına yönlendirilmelisiniz.

> [!NOTE]
> Web sitemiz şu anda bir ziyaretçinin yeni bir hesap oluşturbileceği iki sayfa içeriyor: `CreatingUserAccounts.aspx` ve `EnhancedCreateUserWizard.aspx`. Web sitesinin sitemap ve Login sayfası `CreatingUserAccounts.aspx` sayfasına işaret etmez, ancak `CreatingUserAccounts.aspx` sayfası kullanıcıdan kendi giriş kasalarını, giriş sayfasını ve imza bilgilerini istemez ve `UserProfiles`öğesine karşılık gelen bir satır eklemez. Bu nedenle `CreatingUserAccounts.aspx` sayfasını, bu işlevselliği sağlayacak şekilde güncelleştirin ya da sitemap ve Login sayfasını `CreatingUserAccounts.aspx`yerine `EnhancedCreateUserWizard.aspx` başvuracak şekilde güncelleştirin. İkinci seçeneği belirlerseniz, anonim kullanıcıların `EnhancedCreateUserWizard.aspx` sayfasına erişmesine izin vermek için `Membership` klasörünün `Web.config` dosyasını güncelleştirdiğinizden emin olun.

## <a name="summary"></a>Özet

Bu öğreticide, üyelik çerçevesi içindeki kullanıcı hesaplarıyla ilgili modelleme verileri hakkında bir teknik inceledik. Özellikle, Kullanıcı hesaplarıyla bire çok ilişkiyi paylaşan modelleme varlıklarına ve bire bir ilişkiyi paylaşan verilere baktık. Ayrıca, bu ilgili bilgilerin nasıl görüntülenemediğini, ekleneceğini ve güncelleştirileceğini, SqlDataSource denetimi ve ADO.NET Code kullanan diğer diğer örnekleri de gördük.

Bu öğreticide Kullanıcı hesaplarımızın görünümü tamamlanır. Sonraki öğreticiden başlayarak, rollere dikkat eteceğiz. Rol çerçevesine göz atacağız bir sonraki birkaç öğreticilerde, bkz. yeni roller oluşturma, kullanıcılara rol atama, bir kullanıcının ait olduğu rolleri belirleme ve rol tabanlı yetkilendirmeyi uygulama.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 2,0 ' deki verilere erişme ve verileri güncelleştirme](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 2,0 sihirbaz denetimi](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [ASP.NET 2,0 sihirbaz denetimiyle adım adım kullanıcı arabirimi oluşturma](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [Özel veri kaynağı denetim parametreleri oluşturma](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [CreateUserWizard denetimini özelleştirme](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [DetailsView denetimi hızlı başlangıçlarını](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [ListView denetimiyle verileri görüntüleme](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 2,0 ' de doğrulama denetimlerini kapatma](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [Ekleme ve silme verilerini Düzenle](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [ASP.NET 'de form doğrulaması](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [Özel Kullanıcı kayıt bilgileri toplanıyor](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [ASP.NET 2,0 içindeki profiller](http://www.odetocode.com/Articles/440.aspx)
- [ASP: ListView denetimi](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [Kullanıcı profilleri hızlı başlangıç](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](user-based-authorization-cs.md)
> [İleri](creating-the-membership-schema-in-sql-server-vb.md)
