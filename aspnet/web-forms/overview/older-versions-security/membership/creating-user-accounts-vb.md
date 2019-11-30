---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
title: Kullanıcı hesapları oluşturma (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, Yeni Kullanıcı hesapları oluşturmak için üyelik çerçevesini (SqlMembershipProvider aracılığıyla) kullanarak araştıracağız. Yeni ABD oluşturma hakkında bilgi göndereceğiz...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 9ef3e893-bebe-4b13-9fe5-8b71720dd85e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 01be198c329f372ddcd529ad8a369f2d3426a9fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74628073"
---
# <a name="creating-user-accounts-vb"></a>Kullanıcı Hesapları Oluşturma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_vb.pdf)

> Bu öğreticide, Yeni Kullanıcı hesapları oluşturmak için üyelik çerçevesini (SqlMembershipProvider aracılığıyla) kullanarak araştıracağız. Programlama yoluyla ve ASP aracılığıyla yeni Kullanıcı oluşturma hakkında bilgi göndereceğiz. NET 'in yerleşik CreateUserWizard denetimi.

## <a name="introduction"></a>Giriş

<a id="_msoanchor_1"> </a> [Önceki öğreticide](creating-the-membership-schema-in-sql-server-vb.md) , uygulama Hizmetleri şemasını, `SqlMembershipProvider` ve `SqlRoleProvider`gereken tabloları, görünümleri ve saklı yordamları ekleyen bir veritabanına yükledik. Bu işlem, bu serideki öğreticilerin geri kalanı için gereken altyapıyı oluşturdu. Bu öğreticide, Yeni Kullanıcı hesapları oluşturmak için üyelik çerçevesi (`SqlMembershipProvider`aracılığıyla) kullanılarak araştıracağız. Programlama yoluyla ve ASP aracılığıyla yeni Kullanıcı oluşturma hakkında bilgi göndereceğiz. NET 'in yerleşik CreateUserWizard denetimi.

Yeni Kullanıcı hesapları oluşturmayı öğrenmenin yanı sıra,  *<a id="_msoanchor_2">[ ](../introduction/an-overview-of-forms-authentication-vb.md)</a>form kimlik doğrulaması öğreticisine genel bakış* ve ardından  *<a id="_msoanchor_3">[ ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)</a>Forms kimlik doğrulaması yapılandırması ve gelişmiş konular* öğreticisinde geliştirilmiş olan demo Web sitesini de güncelleştirmeniz gerekecektir. Tanıtım web uygulamamız, kullanıcıların kimlik bilgilerini sabit kodlanmış Kullanıcı adı/parola çiftlerine göre doğrulayan bir oturum açma sayfasına sahiptir. Ayrıca, `Global.asax` kimliği doğrulanmış kullanıcılar için özel `IPrincipal` ve `IIdentity` nesneleri oluşturan kodu içerir. Kullanıcı kimlik bilgilerini üyelik çerçevesinde doğrulamak ve özel asıl ve kimlik mantığını kaldırmak için oturum açma sayfasını güncelleştireceğiz.

Haydi başlayın!

## <a name="the-forms-authentication-and-membership-checklist"></a>Forms kimlik doğrulaması ve üyelik denetim listesi

Üyelik çerçevesiyle çalışmaya başlamadan önce, bu noktaya ulaşmak için gerçekleştirdiğimiz önemli adımları gözden geçirmeniz biraz zaman atalım. Bir form tabanlı kimlik doğrulama senaryosunda üyelik çerçevesini `SqlMembershipProvider` kullanırken, Web uygulamanızda üyelik işlevselliği uygulamadan önce aşağıdaki adımların gerçekleştirilmesi gerekir:

1. **Form tabanlı kimlik doğrulamasını etkinleştirin.** *<a id="_msoanchor_4">[ ](../introduction/an-overview-of-forms-authentication-vb.md)</a>Forms kimlik doğrulamasına genel bakış*konusunda anlatıldığı gibi, form kimlik doğrulaması `Web.config` düzenleyerek ve `<authentication>` öğenin `mode` özniteliği `Forms`olarak ayarlanarak etkinleştirilir. Forms kimlik doğrulaması etkinken, her gelen istek bir *Forms kimlik doğrulama bileti*için incelenir, bu da varsa istek sahibine tanıtır.
2. **Uygulama Hizmetleri şemasını uygun veritabanına ekleyin.** `SqlMembershipProvider` kullanırken, uygulama Hizmetleri şemasını bir veritabanına yüklememiz gerekir. Genellikle bu şema, uygulamanın veri modelini tutan veritabanına eklenir. SQL Server öğreticide  *<a id="_msoanchor_5">[ ](creating-the-membership-schema-in-sql-server-vb.md)</a>üyelik şemasının oluşturulması* , bunu gerçekleştirmek için `aspnet_regsql.exe` Aracı kullanılarak aranır.
3. **Web uygulamasının ayarlarını adım 2 ' deki veritabanına başvuracak şekilde özelleştirin.** SQL Server öğreticide *Üyelik şeması oluşturma* , Web uygulamasını yapılandırmak için iki yol gösterdi. bu sayede, `SqlMembershipProvider` 2. adım: `LocalSqlServer` bağlantı dizesi adını değiştirerek bu veritabanı seçilmiş veritabanını kullanacaktır. veya üyelik çerçevesi sağlayıcıları listesine yeni bir kayıtlı sağlayıcı ekleyerek ve bu yeni sağlayıcıyı 2. adımdaki veritabanını kullanacak şekilde özelleştirerek.

`SqlMembershipProvider` ve form tabanlı kimlik doğrulaması kullanan bir Web uygulaması oluştururken, `Membership` sınıfını veya ASP.NET Login Web denetimlerini kullanmadan önce bu üç adımı gerçekleştirmeniz gerekir. Önceki öğreticilerde bu adımları zaten gerçekleştirdiğimiz için, üyelik çerçevesini kullanmaya başlamaya hazırız!

## <a name="step-1-adding-new-aspnet-pages"></a>1\. Adım: yeni ASP.NET sayfaları ekleme

Bu öğreticide ve sonraki üç, üyelikte ilgili çeşitli işlevleri ve özellikleri inceleyeceğiz. Bu öğreticiler genelinde incelenen konuları uygulamak için bir dizi ASP.NET sayfasına ihtiyacımız olacak. Bu sayfaları ve sonra bir site haritası dosyası `(Web.sitemap)`oluşturalım.

`Membership`adlı projede yeni bir klasör oluşturarak başlayın. Sonra, `Membership` klasöre beş yeni ASP.NET sayfası ekleyerek her sayfayı `Site.master` ana sayfayla bağlantılandırın. Sayfaları adlandırın:

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

Bu noktada, projenizin Çözüm Gezgini Şekil 1 ' de gösterilen ekran görüntüsüne benzer olması gerekir.

[Üyelik klasörüne beş yeni sayfa ![eklenmiştir](creating-user-accounts-vb/_static/image2.png)](creating-user-accounts-vb/_static/image1.png)

**Şekil 1**: `Membership` klasöre beş yeni sayfa eklenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image3.png))

Her sayfa, her bir ana sayfanın Contenttutucuları: `MainContent` ve `LoginContent`olmak üzere iki Içerik denetimine sahip olmalıdır.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample1.aspx)]

`LoginContent` ContentPlaceHolder 'ın varsayılan biçimlendirmesinin, kullanıcının kimliğinin doğrulanmadığına bağlı olarak, oturum açma veya site oturumunu kapatma bağlantısı görüntülediğini geri çekin. Ancak `Content2` Içerik denetiminin varlığı, ana sayfanın varsayılan işaretlemesini geçersiz kılar. *<a id="_msoanchor_6">[ ](../introduction/an-overview-of-forms-authentication-vb.md)</a>Forms kimlik doğrulaması öğreticisine genel bakış* konusunda anlatıldığı gibi, bu, sol sütunda oturum ilgili seçenekleri göstermek istemediğimiz sayfalarda yararlıdır.

Bununla birlikte, bu beş sayfa için ana sayfanın varsayılan biçimlendirmesini `LoginContent` ContentPlaceHolder olarak göstermek istiyoruz. Bu nedenle, `Content2` Içerik denetimi için bildirim temelli biçimlendirmeyi kaldırın. Bunu yaptıktan sonra, beş sayfa biçimlendirmesinin her biri yalnızca bir Içerik denetimi içermelidir.

## <a name="step-2-creating-the-site-map"></a>2\. Adım: site haritasını oluşturma

Ancak, en önemsiz Web sitelerinin bir kullanıcı arabirimi formu uygulaması gerekir. Gezinti Kullanıcı arabirimi, sitenin çeşitli bölümlerine yönelik bağlantıların basit bir listesi olabilir. Alternatif olarak, bu bağlantılar menülerde veya ağaç görünümlerinde düzenlenebilir. Sayfa geliştiricileri olarak, Gezinti Kullanıcı arabirimini oluşturmak öykünün yalnızca yarısıdır. Ayrıca, sitenin mantıksal yapısını sürdürülebilir ve güncelleştirilebilir bir biçimde tanımlamak için bazı yollarla de ihtiyacımız vardır. Yeni sayfalar eklendikçe veya varolan sayfalar kaldırıldığından, tek bir kaynağı güncelleştirebilmek istiyoruz ve site haritasını ve bu değişiklikleri sitenin gezinti kullanıcı arabirimine yansımış olmak istiyoruz.

Bu iki görev, site haritasını temel alan ve site haritasını temel alan bir gezinti kullanıcı arabirimini tanımlayan, site haritası çerçevesi ve ASP.NET sürüm 2,0 ' ye eklenen gezinti Web denetimleri sayesinde kolayca gerçekleştirilmesi kolay bir işlemdir. Site Haritası çerçevesi, bir geliştiricinin bir site haritası tanımlamasına ve ardından programlı bir API ( [`SiteMap` sınıfı](https://msdn.microsoft.com/library/system.web.sitemap.aspx)) aracılığıyla erişmesini sağlar. Yerleşik gezinti Web denetimleri, bir [menü denetimi](https://msdn.microsoft.com/library/bz09dy46.aspx), [TreeView denetimi](https://msdn.microsoft.com/library/3eafky27.aspx)ve bir [Denetim](https://msdn.microsoft.com/library/3eafky27.aspx)listesini içerir.

Üyelik ve rol çerçeveleri gibi, site haritası çerçevesi de [sağlayıcı modeline](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)göre oluşturulmuştur. Site haritası sağlayıcısı sınıfının işi, bir XML dosyası veya veritabanı tablosu gibi kalıcı bir veri deposundan `SiteMap` sınıfı tarafından kullanılan bellek içi yapıyı oluşturmak için kullanılır. .NET Framework, bir XML dosyasından ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)) site haritası verilerini okuyan varsayılan bir site haritası sağlayıcısıyla birlikte gelir ve bu öğreticide kullanacağız sağlayıcıdır. Bazı alternatif site haritası sağlayıcısı uygulamaları için, Bu öğreticinin sonundaki diğer okumalar bölümüne bakın.

Varsayılan site haritası sağlayıcısı, `Web.sitemap` adlı doğru biçimli bir XML dosyasının kök dizine sahip olmasını bekler. Bu varsayılan sağlayıcıyı kullandığımızda, bu tür bir dosyayı eklememiz ve site haritasının yapısını uygun XML biçiminde tanımlamalıdır. Dosyayı eklemek için Çözüm Gezgini içindeki proje adına sağ tıklayın ve yeni öğe Ekle ' yi seçin. İletişim kutusunda, `Web.sitemap`adlı site haritası türünde bir dosya eklemeyi tercih edin.

[![, projenin kök dizinine Web. sitemap adlı bir dosya ekleyin](creating-user-accounts-vb/_static/image5.png)](creating-user-accounts-vb/_static/image4.png)

**Şekil 2**: projenin kök dizinine `Web.sitemap` adlı bir dosya ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image6.png))

XML site eşleme dosyası Web sitesinin yapısını hiyerarşi olarak tanımlar. Bu hiyerarşik ilişki, XML dosyasında `<siteMapNode>` öğelerinin ancei aracılığıyla modellenir. `Web.sitemap`, tam olarak bir `<siteMapNode>` alt öğesi olan `<siteMap>` bir üst düğüm ile başlamalıdır. Bu üst düzey `<siteMapNode>` öğesi hiyerarşinin kökünü temsil eder ve rastgele sayıda alt düğüm içerebilir. Her `<siteMapNode>` öğesi bir `title` özniteliği içermeli ve isteğe bağlı olarak, diğerleri arasında `url` ve `description` özniteliklerini de içerebilir; boş olmayan her bir `url` özniteliği benzersiz olmalıdır.

Aşağıdaki XML 'i `Web.sitemap` dosyasına girin:

[!code-xml[Main](creating-user-accounts-vb/samples/sample2.xml)]

Yukarıdaki site haritası biçimlendirmesi şekil 3 ' te gösterilen hiyerarşiyi tanımlar.

[Site Haritası hiyerarşik bir gezinti yapısını temsil ![](creating-user-accounts-vb/_static/image8.png)](creating-user-accounts-vb/_static/image7.png)

**Şekil 3**: site haritası hiyerarşik bir gezinti yapısını temsil eder ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image9.png))

## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>3\. Adım: Ana sayfayı bir gezinti kullanıcı arabirimi Içerecek şekilde güncelleştirme

ASP.NET, bir kullanıcı arabirimi tasarlamak için bir dizi gezinmede ilgili Web denetimi içerir. Bunlar menü, TreeView ve, bu denetimleri içerir. Menü ve TreeView denetimleri, site haritası yapısını sırasıyla bir menü ya da ağaç içinde işler, ancak bu, yeni, ziyaret edilen geçerli düğümü ve bunların üst öğelerinden oluşan bir içerik haritası gösterir. Site haritası verileri, SiteMapDataSource kullanılarak diğer veri Web denetimlerine bağlanabilir ve `SiteMap` sınıfı aracılığıyla programlı olarak erişilebilir.

Site Haritası çerçevesi ve gezinti denetimlerinin kapsamlı bir açıklaması bu öğretici serisinin kapsamı dışında olduğundan, kendi gezinme Kullanıcı arabirimimizi bir adım adım yerine, Şekil 4 ' te gösterildiği gibi, iki derin madde işaretli gezinti bağlantıları listesini göstermek için bir yineleyici denetimi kullanan *[ASP.NET 2,0 öğretici serisindeki verilerle çalıştım](../../data-access/index.md)* .

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>Sol sütundaki Iki düzeyli bir bağlantı listesi ekleme

Bu arabirimi oluşturmak için, aşağıdaki bildirime dayalı işaretlemeyi `Site.master` ana sayfanın sol sütununa ekleyin ve bu metnin TODO: Menu buraya gidecektir... Şu anda bulunuyor.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample3.aspx)]

Yukarıdaki biçimlendirme `menu` adlı bir yineleyici denetimini, `Web.sitemap`tanımlanan site haritası hiyerarşisini döndüren bir SiteMapDataSource 'a bağlar. SiteMapDataSource denetiminin [`ShowStartingNode` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) false olarak ayarlandığından, giriş düğümünün alt öğelerinden başlayarak site haritasının hiyerarşisini döndürmeye başlar. Yineleyici, bu düğümlerin her birini bir `<li>` öğesinde görüntüler (Şu anda yalnızca üyelik). Diğer bir deyişle, iç Yineleyici daha sonra geçerli düğümün alt öğelerini iç içe sıralanmamış bir listede görüntüler.

Şekil 4 ' te, adım 2 ' de oluşturduğumuz site haritası yapısıyla yukarıdaki biçimlendirmenin işlenmiş çıktısını gösterir. Yineleyici, Vanilla sırasız liste işaretlemesini oluşturur; `Styles.css` ' de tanımlanan geçişli stil sayfası kuralları, aesthetik-pkiralama düzeninden sorumludur. Yukarıdaki biçimlendirmenin nasıl çalıştığı hakkında daha ayrıntılı bir açıklama için, [ana sayfalar ve site gezinti](https://asp.net/learn/data-access/tutorial-03-vb.aspx) öğreticisine bakın.

[Gezinti Kullanıcı arabirimi ![, Iç Içe sıralanmamış listeler kullanılarak Işlenir](creating-user-accounts-vb/_static/image11.png)](creating-user-accounts-vb/_static/image10.png)

**Şekil 4**: gezinme Kullanıcı arabirimi, Iç Içe sıralanmamış listeler kullanılarak işlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image12.png))

### <a name="adding-breadcrumb-navigation"></a>Içerik Haritası gezintisi ekleme

Sol sütundaki bağlantıların listesine ek olarak, her sayfanın bir [içerik haritası](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29)görüntülemesini de sağlayabilirsiniz. Bir içerik haritası, kullanıcıları site hiyerarşisi içindeki geçerli konumlarını hızlıca gösteren bir gezinti kullanıcı arabirimi öğesidir. Bu, site haritasında geçerli sayfanın konumunu tespit etmek için site haritası çerçevesini kullanır ve ardından bu bilgilere göre bir içerik haritası görüntüler.

Özellikle, ana sayfanın üstbilgi `<div>` öğesine bir `<span>` öğesi ekleyin ve yeni `<span>` öğesinin `class` özniteliğini içerik haritası olarak ayarlayın. (`Styles.css` sınıfı bir içerik haritası sınıfına yönelik bir kural içerir.) Sonra, bu yeni `<span>` öğesine bir bir bir bir bir II ekleyin.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample4.aspx)]

Şekil 5 ' te `~/Membership/CreatingUserAccounts.aspx`ziyaret edildiğinde, bu değer ' in çıktısını gösterir.

[Içerik Haritası ![, geçerli sayfayı ve onun üst öğelerini site haritasında görüntüler](creating-user-accounts-vb/_static/image14.png)](creating-user-accounts-vb/_static/image13.png)

**Şekil 5**: içerik haritası, geçerli sayfayı ve onun üst öğelerini site haritasında görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image15.png))

## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>4\. Adım: özel sorumluyu ve kimlik mantığını kaldırma

*<a id="_msoanchor_7">[ ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)</a>Forms kimlik doğrulaması yapılandırması ve gelişmiş konular* öğreticisinde, özel sorumlunun ve kimlik nesnelerinin kimliği doğrulanmış kullanıcıyla nasıl ilişkilendirileceğini gördük. Bunu, uygulamanın `PostAuthenticateRequest` olayı için `Global.asax` bir olay işleyicisi oluşturarak yaptık `FormsAuthenticationModule` kimliği doğrulandıktan sonra harekete geçirilir. Bu olay işleyicisinde, `FormsAuthenticationModule` tarafından eklenen `GenericPrincipal` ve `FormsIdentity` nesneleri, bu öğreticide oluşturduğumuz `CustomPrincipal` ve `CustomIdentity` nesneleriyle değiştirdik.

Özel asıl ve kimlik nesneleri belirli senaryolarda faydalıdır, çoğu durumda `GenericPrincipal` ve `FormsIdentity` nesneleri yeterlidir. Sonuç olarak, varsayılan davranışa geri dönebileceğimizi düşündüm. `PostAuthenticateRequest` olay işleyicisini kaldırarak veya yorum yaparak ya da `Global.asax` dosyasını tamamen silerek bu değişikliği yapın.

> [!NOTE]
> `Global.asax`kodu açıklamalı veya kaldırdıktan sonra, `User.Identity` özelliğini bir `CustomIdentity` örneğine veren `Default.aspx's` arka plan kod sınıfında kodu açıklamanız gerekir.

## <a name="step-5-programmatically-creating-a-new-user"></a>5\. Adım: program aracılığıyla yeni bir Kullanıcı oluşturma

Üyelik çerçevesi aracılığıyla yeni bir kullanıcı hesabı oluşturmak için `Membership` sınıfının [`CreateUser` yöntemini](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)kullanın. Bu yöntemin Kullanıcı adı, parola ve kullanıcıyla ilgili diğer alanlar için giriş parametreleri vardır. Çağırma sırasında, Yeni Kullanıcı hesabının oluşturulmasını yapılandırılmış üyelik sağlayıcısına devreder ve ardından, yalnızca oluşturulan kullanıcı hesabını temsil eden bir [`MembershipUser` nesnesi](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) döndürür.

`CreateUser` yönteminin, her biri farklı sayıda giriş parametresi kabul eden dört aşırı yüklemesi vardır:

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

Bu dört aşırı yükleme, toplanan bilgi miktarına göre farklılık gösterir. Örneğin, ilk aşırı yükleme yeni kullanıcı hesabı için yalnızca Kullanıcı adı ve parola gerektirir, ancak ikinci tane de kullanıcının e-posta adresini gerektirir.

Yeni bir kullanıcı hesabı oluşturmak için gereken bilgiler, üyelik sağlayıcısının yapılandırma ayarlarına bağlı olduğundan bu aşırı yüklemeler vardır. *<a id="_msoanchor_8">[ ](creating-the-membership-schema-in-sql-server-vb.md)</a>SQL Server içinde üyelik şeması oluşturma* öğreticisinde, `Web.config`üyelik sağlayıcısı yapılandırma ayarlarını belirtmeyi inceledik. Tablo 2, yapılandırma ayarlarının kapsamlı bir listesini içeriyordu.

`CreateUser` aşırı yüklerini etkileyebilecek bir üyelik sağlayıcısı yapılandırma ayarı `requiresQuestionAndAnswer` ayardır. `requiresQuestionAndAnswer` `true` (varsayılan) olarak ayarlandıysa, yeni bir kullanıcı hesabı oluştururken bir güvenlik sorusu ve yanıtı belirtmemiz gerekir. Bu bilgiler daha sonra kullanıcının parolasını sıfırlaması ya da parolasını değiştirmesi gerektiğinde kullanılır. Özellikle, bu tarihte güvenlik sorusu gösterilmekte ve parolasını sıfırlamak ya da değiştirmek için doğru yanıtı girmeleri gerekir. Sonuç olarak, `requiresQuestionAndAnswer` `true` olarak ayarlanırsa ilk iki `CreateUser` aşırı yüklemesinin çağrılması, güvenlik sorusu ve yanıtı eksik olduğu için bir özel duruma neden olur. Uygulamamız şu anda bir güvenlik sorusu ve yanıtı gerektirecek şekilde yapılandırılmış olduğundan, kullanıcının programlı bir şekilde oluşturulması için son iki aşırı yüklemeden birini kullanmaları gerekir.

`CreateUser` yönteminin kullanımını anlamak için kullanıcıdan ad, parola, e-posta ve önceden tanımlanmış bir güvenlik sorusu için bir yanıt istediğimiz bir kullanıcı arabirimi oluşturalım. `Membership` klasöründeki `CreatingUserAccounts.aspx` sayfasını açın ve Içerik denetimine aşağıdaki Web denetimlerini ekleyin:

- `Username` adlı bir metin kutusu
- `TextMode` özelliği `Password` olarak ayarlanmış `Password`adlı bir metin kutusu
- `Email` adlı bir metin kutusu
- `Text` özelliği temizlenmiş `SecurityQuestion` adlı bir etiket
- `SecurityAnswer` adlı bir metin kutusu
- `Text` özelliği kullanıcı hesabını oluşturmak üzere ayarlanmış `CreateAccountButton` adlı düğme
- `Text` özelliği temizlenmiş `CreateAccountResults` adlı bir etiket denetimi

Bu noktada, ekranınızda Şekil 6 ' da gösterilen ekran görüntüsüne benzer görünmelidir.

[Çeşitli Web denetimlerini CreatingUserAccounts. aspx sayfasına eklemek ![](creating-user-accounts-vb/_static/image17.png)](creating-user-accounts-vb/_static/image16.png)

**Şekil 6**: `CreatingUserAccounts.aspx Page` çeşitli Web denetimlerini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image18.png))

`SecurityQuestion` etiketi ve `SecurityAnswer` metin kutusu, önceden tanımlanmış bir güvenlik sorusu göstermek ve kullanıcının yanıtını toplamak için tasarlanmıştır. Hem güvenlik sorusu hem de yanıtın Kullanıcı tarafından bir kullanıcı tarafından depolandığını ve bu nedenle her bir kullanıcının kendi güvenlik sorusunu tanımlamasına izin vermek mümkündür. Bununla birlikte, bu örnekte bir Evrensel güvenlik sorusu kullanmaya karar verdim; yani en sevdiğiniz renk nedir?

Bu önceden tanımlı güvenlik sorusunu uygulamak için, `passwordQuestion`adlı sayfanın arka plan kodu sınıfına bir sabit ekleyin, bu, güvenlik sorusu atayarak. Ardından, `Page_Load` olay işleyicisinde, bu sabiti `SecurityQuestion` etiketinin `Text` özelliğine atayın:

[!code-vb[Main](creating-user-accounts-vb/samples/sample5.vb)]

Sonra, `CreateAccountButton'` s `Click` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](creating-user-accounts-vb/samples/sample6.vb)]

`Click` olay işleyicisi, [`MembershipCreateStatus`](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx)türünde `createStatus` adlı bir değişken tanımlayarak başlar. `MembershipCreateStatus`, `CreateUser` işleminin durumunu gösteren bir numaralandırmadır. Örneğin, Kullanıcı hesabı başarıyla oluşturulursa, sonuçta elde edilen `MembershipCreateStatus` örneği diğer taraftan `Success;` bir değere ayarlanır. işlem başarısız olursa, aynı kullanıcı adına sahip bir kullanıcı zaten mevcut olduğundan, bu bir `DuplicateUserName`değerine ayarlanır. Kullandığımız `CreateUser` aşırı yüklemede yöntemine bir `MembershipCreateStatus` örneği geçirmemiz gerekiyor. Bu parametre `CreateUser` yöntemi içinde uygun değere ayarlanır ve Kullanıcı hesabının başarıyla oluşturulup oluşturulmayacağını anlamak için yöntem çağrısından sonra değerini inceleyebilirsiniz.

`CreateUser`çağrıldıktan sonra, `createStatus`geçirilerek, `createStatus`atanan değere bağlı olarak uygun bir iletiyi çıkarmak için `Select Case` bir ifade kullanılır. Şekil 7 ' de Yeni Kullanıcı başarıyla oluşturulduğunda çıkış görüntülenir. Şekil 8 ve 9 Kullanıcı hesabı oluşturulmadıysa çıktıyı gösterir. Şekil 8 ' de ziyaretçi, üyelik sağlayıcısının yapılandırma ayarlarındaki parola gücü gereksinimlerini karşılamayan beş harfli bir parola girmiştir. Şekil 9 ' da, ziyaretçi mevcut Kullanıcı adı (Şekil 7 ' de oluşturulmuştur) ile bir kullanıcı hesabı oluşturmaya çalışıyor.

[![yeni bir kullanıcı hesabı başarıyla oluşturuldu](creating-user-accounts-vb/_static/image20.png)](creating-user-accounts-vb/_static/image19.png)

**Şekil 7**: yeni bir kullanıcı hesabı başarıyla oluşturuldu ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image21.png))

[Sağlanan parola çok zayıf olduğundan kullanıcı hesabı ![oluşturulmamış](creating-user-accounts-vb/_static/image23.png)](creating-user-accounts-vb/_static/image22.png)

**Şekil 8**: sağlanan parola çok zayıf olduğu Için Kullanıcı hesabı oluşturulmadı ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image24.png))

[Kullanıcı hesabı, Kullanıcı adı zaten kullanımda olduğu için ![oluşturulmaz](creating-user-accounts-vb/_static/image26.png)](creating-user-accounts-vb/_static/image25.png)

**Şekil 9**: Kullanıcı hesabı, Kullanıcı adı zaten kullanımda olduğu için oluşturulamadı ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image27.png))

> [!NOTE]
> İlk iki `CreateUser` yöntemi aşırı yüklemeden birini kullanırken başarıyı veya hatanın nasıl belirleneceğini merak ediyor olabilirsiniz; hiçbiri `MembershipCreateStatus`türünde bir parametreye sahip değildir. Bu ilk iki aşırı yükleme, hata durumunda `MembershipCreateStatus`türünde bir [`StatusCode` özelliği](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx) içeren [`MembershipCreateUserException` bir özel durum](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx) oluşturur.

Birkaç kullanıcı hesabı oluşturduktan sonra, `SecurityTutorials.mdf` veritabanındaki `aspnet_Users` ve `aspnet_Membership` tablolarının içeriğini listeleyerek hesapların oluşturulduğunu doğrulayın. Şekil 10 ' u gösterdiği gibi, `CreatingUserAccounts.aspx` sayfa: Tito ve Bruce aracılığıyla iki Kullanıcı ekledik.

[![üyelik kullanıcı deposunda Iki kullanıcı vardır: Tito ve deneme CE](creating-user-accounts-vb/_static/image29.png)](creating-user-accounts-vb/_static/image28.png)

**Şekil 10**: üyelik kullanıcı deposunda iki kullanıcı vardır: Tito ve Bruce ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image30.png))

Üyelik kullanıcı deposu artık deneme ve Tito 'nun hesap bilgilerini içerirken, deneme veya Tito 'ın sitede oturum açmasına olanak sağlayan işlevselliği uyguladık. Şu anda `Login.aspx`, kullanıcının kimlik bilgilerini sabit kodlanmış bir Kullanıcı adı/parola çiftliğinde karşılaştırarak doğrular; belirtilen kimlik bilgilerini üyelik çerçevesi 'ne *karşı doğrulamaz.* Artık `aspnet_Users` Yeni Kullanıcı hesaplarını görmek için `aspnet_Membership` tablolarda yeterli bir işlem olması gerekir. Sonraki öğreticide,  *<a id="_msoanchor_9">[ ](validating-user-credentials-against-the-membership-user-store-vb.md)</a>Kullanıcı kimlik bilgilerini üyelik kullanıcı deposunda doğrulayarak*, üyelik deposuna göre doğrulanacak oturum açma sayfasını güncelleştireceğiz.

> [!NOTE]
> `SecurityTutorials.mdf` veritabanınızda hiç Kullanıcı görmüyorsanız, bunun nedeni Web uygulamanızın kullanıcı deposu olarak `ASPNETDB.mdf` veritabanını kullanan varsayılan üyelik `AspNetSqlMembershipProvider`sağlayıcısını kullanıyor olması olabilir. Sorunun bu olup olmadığını anlamak için Çözüm Gezgini Yenile düğmesine tıklayın. `App_Data` klasörüne `ASPNETDB.mdf` adlı bir veritabanı eklendiyse, bu sorun budur. Üyelik sağlayıcısını düzgün bir şekilde yapılandırma yönergeleri için SQL Server öğreticisinde  *<a id="_msoanchor_10">[ ](creating-the-membership-schema-in-sql-server-vb.md)</a>üyelik şeması oluşturma* işleminin 4. adımına dönün.

Çoğu kullanıcı hesabı senaryosunda ziyaretçi, Kullanıcı adı, parola, e-posta ve diğer önemli bilgileri girmek için yeni bir hesabın oluşturulduğu bir arabirimle sunulur. Bu adımda, bu tür bir arabirimi el ile oluşturmaya ve ardından Kullanıcı girişlerini temel alarak yeni kullanıcı hesabını programlı olarak eklemek için `Membership.CreateUser` yönteminin nasıl kullanılacağını gördük. Ancak, kodumuz Yeni Kullanıcı hesabını oluşturmuş olmanız yeterlidir. Kullanıcının yeni oluşturulan kullanıcı hesabı altındaki siteye oturum açmasını ya da kullanıcıya bir onay e-postası göndermesini sağlamak gibi herhangi bir izleme eylemi gerçekleştirmedi. Bu ek adımlar, düğmenin `Click` olay işleyicisinde ek kod gerektirir.

ASP.NET, Kullanıcı hesabı oluşturma işlemini işlemek için tasarlanan CreateUserWizard denetimiyle birlikte gelir, bu, Yeni Kullanıcı hesapları oluşturmak için bir kullanıcı arabirimi oluşturmayı, üyelik çerçevesinde hesabı oluşturma ve hesap sonrası gerçekleştirme bir onay e-postası gönderme ve yeni oluşturulan kullanıcıyı siteye kaydetme gibi oluşturma görevleri. CreateUserWizard denetimini kullanarak, CreateUserWizard denetimini araç kutusundan bir sayfaya sürüklemek ve sonra birkaç özellik ayarlamak kadar basittir. Çoğu durumda, tek satırlık bir kod yazmanız gerekmez. Bu nifty denetimini adım 6 ' da ayrıntılı olarak araştıracağız.

Yeni Kullanıcı hesapları yalnızca tipik bir hesap oluşturma Web sayfası aracılığıyla oluşturulduysa, CreateUserWizard denetimi gereksinimlerinize uygun olduğu için `CreateUser` yöntemini kullanan kodu yazmanız gerekmez. Ancak `CreateUser` yöntemi, son derece özelleştirilmiş bir hesap kullanıcı deneyimine veya alternatif bir arabirim aracılığıyla program aracılığıyla yeni kullanıcı hesapları oluşturmanız gerektiğinde yararlıdır. Örneğin, bir kullanıcının başka bir uygulamadan Kullanıcı bilgilerini içeren bir XML dosyasını karşıya yüklemesine izin veren bir sayfanız olabilir. Sayfa, karşıya yüklenen XML dosyasının içeriğini ayrıştırır ve `CreateUser` yöntemini çağırarak XML 'de temsil edilen her bir kullanıcı için yeni bir hesap oluşturabilir.

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>6\. Adım: CreateUserWizard denetimiyle yeni bir Kullanıcı oluşturma

ASP.NET, bir dizi oturum açma Web denetimi ile birlikte sunulur. Bu denetimler birçok ortak kullanıcı hesabı ve oturum açmayla ilgili senaryolar konusunda yardımcı olur. [CreateUserWizard denetimi](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx) , üyelik çerçevesine yeni bir kullanıcı hesabı eklemek için bir kullanıcı arabirimi sunmak üzere tasarlanan bir denetimdir.

Diğer oturumla ilgili Web denetimlerinin birçoğu gibi, CreateUserWizard tek bir kod satırı yazmadan kullanılabilir. BT Intuit, üyelik sağlayıcısının yapılandırma ayarlarını temel alan bir kullanıcı arabirimi sağlar ve Kullanıcı gerekli bilgileri girdikten sonra Kullanıcı Oluştur düğmesine tıkladıktan sonra `Membership` sınıfının `CreateUser` yöntemini dahili olarak çağırır. CreateUserWizard denetimi son derece özelleştirilebilir. Hesap oluşturma işleminin çeşitli aşamaları sırasında tetiklenen bir olay ana bilgisayarı vardır. Hesap oluşturma iş akışına özel mantık eklemek için gerektiğinde olay işleyicileri oluşturuyoruz. Ayrıca, CreateUserWizard 'in görünümü çok esnektir. Varsayılan arabirimin görünümünü tanımlayan bazı özellikler vardır; gerekirse, denetim bir şablona dönüştürülebilir veya ek kullanıcı kaydı adımları eklenebilir.

CreateUserWizard denetiminin varsayılan arabirimini ve davranışını kullanarak bir bakalım başlayalım. Daha sonra denetimin özellikler ve olaylar aracılığıyla görünümün nasıl özelleştirileceğini keşfedeceğiz.

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>CreateUserWizard 'in varsayılan arabirimini ve davranışını İnceleme

`Membership` klasöründeki `CreatingUserAccounts.aspx` sayfasına dönün, tasarım veya bölme moduna geçin ve ardından sayfanın en üstüne bir CreateUserWizard denetimi ekleyin. CreateUserWizard denetimi, araç kutusunun oturum açma denetimleri bölümünün altında dosyalanır. Denetim eklendikten sonra, `ID` özelliğini `RegisterUser`olarak ayarlayın. Şekil 11 ' de ekran görüntüsü gösterildiği gibi, CreateUserWizard yeni kullanıcının Kullanıcı adı, parola, e-posta adresi ve güvenlik sorusu ve yanıtı için metin kutularına bir arabirim oluşturur.

[CreateUserWizard denetimi bir genel Kullanıcı oluşturma arabirimi Işler ![](creating-user-accounts-vb/_static/image32.png)](creating-user-accounts-vb/_static/image31.png)

**Şekil 11**: CreateUserWizard Control bir genel Kullanıcı oluşturma arabirimi işler ([tam boyutlu görüntüyü görüntülemek için tıklatın](creating-user-accounts-vb/_static/image33.png))

CreateUserWizard denetimi tarafından oluşturulan varsayılan kullanıcı arabirimini 5. adımda oluşturduğumuz arabirimle karşılaştırmak için biraz zaman atalım. Başlangıçlara yönelik olarak, CreateUserWizard denetimi ziyaretçinin hem güvenlik sorusu hem de yanıtı belirtmesini sağlar, ancak el ile oluşturulan arabirimimiz önceden tanımlanmış bir güvenlik sorusu kullanmıştı. CreateUserWizard denetiminin arabirimi doğrulama denetimlerini de içerir, ancak henüz arabirimimizin form alanlarında doğrulama uygulamamız gerekiyordu. CreateUserWizard denetim arabirimi bir parolayı onayla metin kutusunu (Password ve parola Karşılaştır metin kutularına girilen metnin eşit olduğundan emin olmak için bir CompareValidator ile birlikte) içerir.

CreateUserWizard denetimi, Kullanıcı arabirimini işlerken üyelik sağlayıcısının yapılandırma ayarlarını danışmandır. Örneğin, güvenlik sorusu ve yanıt metin kutuları yalnızca `requiresQuestionAndAnswer` true olarak ayarlandıysa görüntülenir. Benzer şekilde, CreateUserWizard, parola düzeyi gereksinimlerinin karşılanmasını sağlamak için otomatik olarak bir RegularExpressionValidator denetimi ekler ve `minRequiredPasswordLength`, `minRequiredNonalphanumericCharacters`ve `passwordStrengthRegularExpression` yapılandırma ayarlarına göre `ErrorMessage` ve `ValidationExpression` özelliklerini ayarlar.

CreateUserWizard denetimi, adı gösterdiği gibi, [sihirbaz denetiminden](https://msdn.microsoft.com/library/s2etd1ek.aspx)türetilir. Sihirbaz denetimleri, çok adımlı görevleri tamamlamak için bir arabirim sağlamak üzere tasarlanmıştır. Bir sihirbaz denetimi, her biri, bu adım için HTML ve Web denetimlerini tanımlayan bir şablon olan rastgele sayıda `WizardSteps`sahip olabilir. Sihirbaz denetimi başlangıçta ilk `WizardStep`, kullanıcının bir adımdan sonrakine geçmesini veya önceki adımlara geri dönmesini sağlayan gezinti denetimleriyle birlikte görüntüler.

Şekil 11 ' de bildirim temelli biçimlendirme olarak, CreateUserWizard denetiminin varsayılan arabirimi iki `WizardStep` s içerir:

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) ? Yeni Kullanıcı hesabını oluşturmak için bilgi toplamak üzere arabirimi işler. Bu adım Şekil 11 ' de gösterilmektedir.
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) ? Hesabın başarıyla oluşturulduğunu belirten bir ileti işler.

CreateUserWizard 'in görünümü ve davranışı, bu adımların herhangi biri şablonlara veya kendi `WizardStep` s ekleyerek değiştirilebilir. *Ek kullanıcı bilgilerini depolama* öğreticisindeki kayıt arabirimine bir `WizardStep` ekleme hakkında bilgi göndereceğiz.

CreateUserWizard denetimini görelim. `CreatingUserAccounts.aspx` sayfasını bir tarayıcıda ziyaret edin. CreateUserWizard 'un arabirimine bazı geçersiz değerler girerek başlayın. Parola düzeyi gereksinimleriyle uyumlu olmayan bir parola girmeyi deneyin veya Kullanıcı adı metin kutusunu boş bırakın. CreateUserWizard uygun bir hata iletisi görüntüler. Şekil 12 ' de, sınırsız bir güçlü parola ile kullanıcı oluşturmaya çalışırken çıkış gösterilmektedir.

[CreateUserWizard ![doğrulama denetimlerini otomatik olarak çıkarır](creating-user-accounts-vb/_static/image35.png)](creating-user-accounts-vb/_static/image34.png)

**Şekil 12**: CreateUserWizard, doğrulama denetimlerini otomatik olarak çıkarır ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image36.png))

Sonra, CreateUserWizard öğesine uygun değerleri girin ve Kullanıcı Oluştur düğmesine tıklayın. Gerekli alanların girildiğini ve parolanın kuvvetinin yeterli olduğunu varsayarsak, CreateUserWizard üyelik çerçevesi aracılığıyla yeni bir kullanıcı hesabı oluşturur ve sonra `CompleteWizardStep`arabirimini görüntüler (bkz. Şekil 13). Arka planda CreateUserWizard, tıpkı 5. adımda yaptığımız gibi `Membership.CreateUser` yöntemini çağırır.

[![yeni bir kullanıcı hesabı başarıyla oluşturuldu](creating-user-accounts-vb/_static/image38.png)](creating-user-accounts-vb/_static/image37.png)

**Şekil 13**: yeni bir kullanıcı hesabı başarıyla oluşturuldu ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image39.png))

> [!NOTE]
> Şekil 13 ' te gösterildiği gibi, `CompleteWizardStep`arabirimi devam düğmesi içerir. Ancak, bu noktada, ziyaretçi yalnızca bir geri gönderme gerçekleştirir ve ziyaretçisini aynı sayfada bırakır. CreateUserWizard 'ın görünümünü ve davranışını Özellikler bölümünde özelleştirmek için, bu düğmenin ziyaretçi `Default.aspx` (veya başka bir sayfaya) nasıl gönderileceğini inceleyeceğiz.

Yeni bir kullanıcı hesabı oluşturduktan sonra, Visual Studio 'ya dönün ve hesabın başarıyla oluşturulduğunu doğrulamak için Şekil 10 ' da yaptığımız gibi `aspnet_Users` ve `aspnet_Membership` tabloları inceleyin.

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>CreateUserWizard 'ın davranışını ve görünümünü özellikler aracılığıyla özelleştirme

CreateUserWizard, özellikler, `WizardStep` s ve olay işleyicileri aracılığıyla çeşitli yollarla özelleştirilebilir. Bu bölümde, denetimin görünümünü özellikleriyle nasıl özelleştireceğinizi inceleyeceğiz; sonraki bölüm, olay işleyicileri aracılığıyla denetimin davranışını genişletmeyi inceler.

CreateUserWizard denetiminin varsayılan kullanıcı arabiriminde görünen metnin neredeyse tamamı, Plethora özellikleri aracılığıyla özelleştirilebilir. Örneğin, metin kutularının solunda görünen Kullanıcı adı, parola, parolayı onayla, e-posta, güvenlik sorusu ve Güvenlik Yanıt etiketleri sırasıyla [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx), [`PasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx), [`ConfirmPasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx), [`EmailLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx), [`QuestionLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)ve [`AnswerLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx) özellikleri tarafından özelleştirilebilir. Benzer şekilde, `CreateUserWizardStep` ve `CompleteWizardStep`için kullanıcı oluştur ve devam et düğmeleri ve bu düğmelerin düğme, bağlantı düğmeleri veya ImageButton olarak işlenip işlendiğine ilişkin özellikler de mevcuttur.

Renkler, kenarlıklar, yazı tipleri ve diğer görsel öğeleri, bir stil özellikleri konağından yapılandırılabilir. CreateUserWizard denetiminin kendisi, ortak Web denetim stili özelliklerine sahiptir-`BackColor`, `BorderStyle`, `CssClass`, `Font`, vb. ve CreateUserWizard 'in arabiriminin belirli bölümleri için görünümü tanımlamaya yönelik bir dizi stil özelliği vardır. Örneğin [`TextBoxStyle` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx), `CreateUserWizardStep`metin kutularının stillerini tanımlar, ancak [`TitleTextStyle` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx) başlık stilini tanımlar (yeni hesabınız için kaydolun).

Görünümle ilgili özelliklere ek olarak, CreateUserWizard denetiminin davranışını etkileyen bazı özellikler vardır. [`DisplayCancelButton` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx), true olarak ayarlanırsa, kullanıcı oluştur düğmesinin yanında bir iptal düğmesi görüntüler (varsayılan değer false 'dur). Iptal düğmesini görüntülediğinizde, Iptal ' e tıkladıktan sonra kullanıcının gönderildiği sayfayı belirten [`CancelDestinationPageUrl` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)de ayarladığınızdan emin olun. Önceki bölümde belirtildiği gibi, `CompleteWizardStep`arabirimindeki devam düğmesi geri göndermeye neden olur, ancak ziyaretçi aynı sayfada kalır. Devam düğmesine tıkladıktan sonra ziyaretçi başka bir sayfaya göndermek için [`ContinueDestinationPageUrl` özelliğindeki](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)URL 'yi belirtmeniz yeterlidir.

`RegisterUser` CreateUserWizard denetimini bir Iptal düğmesi göstermek ve Iptal veya devam düğmesi tıklandığında ziyaretçi `Default.aspx` göndermek için güncelleştirelim. Bunu gerçekleştirmek için `DisplayCancelButton` özelliğini true olarak ve hem `CancelDestinationPageUrl` hem de `ContinueDestinationPageUrl` özelliklerini ~/default.exe olarak ayarlayın. Şekil 14 ' te, bir tarayıcıdan görüntülendiklerinde güncelleştirilmiş CreateUserWizard gösterilmektedir.

[CreateUserWizardStep ![bir Iptal düğmesi Içerir](creating-user-accounts-vb/_static/image41.png)](creating-user-accounts-vb/_static/image40.png)

**Şekil 14**: `CreateUserWizardStep` bir Iptal düğmesi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image42.png))

Ziyaretçi bir Kullanıcı adı, parola, e-posta adresi ve güvenlik sorusu ve yanıtı girdiğinde ve Kullanıcı Oluştur ' a tıkladığında yeni bir kullanıcı hesabı oluşturulur ve ziyaretçi yeni oluşturulan kullanıcı olarak oturum açar. Sayfayı ziyaret eden kişinin kendileri için yeni bir hesap oluşturduğundan, bu büyük olasılıkla istenen davranıştır. Ancak, yöneticilerin yeni kullanıcı hesapları eklemesine izin vermek isteyebilirsiniz. Bu durumda, Kullanıcı hesabı oluşturulur, ancak yönetici yönetici olarak oturum açmış (yeni oluşturulan hesap olarak değil) olarak kalır. Bu davranış, Boole [`LoginCreatedUser` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)aracılığıyla değiştirilebilir.

Üyelik çerçevesindeki Kullanıcı hesapları onaylanan bayrak içeriyor; onaylanmamış kullanıcılar sitede oturum açamıyor. Varsayılan olarak, yeni oluşturulan bir hesap Onaylandı olarak işaretlenir ve kullanıcının sitede hemen oturum açmasına izin verilir. Ancak, Yeni Kullanıcı hesaplarının onaylanmamış olarak işaretlenme olasılığı vardır. Yöneticiler, oturum açmadan önce yeni kullanıcıları el ile onaylamasını istiyor olabilirsiniz; ya da bir kullanıcının oturum açmasına izin vermeden önce kayıt sırasında girilen e-posta adresinin geçerli olduğunu doğrulamak istiyor olabilirsiniz. Durum ne olursa olsun, CreateUserWizard denetiminin [`DisableCreatedUser` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx) true olarak ayarlayarak yeni oluşturulan kullanıcı hesabının onaylanmamış olarak işaretlenmesini sağlayabilirsiniz (varsayılan değer false 'dur).

Nottaki diğer davranışla ilgili özellikler `AutoGeneratePassword` ve `MailDefinition`içerir. [`AutoGeneratePassword` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx) true olarak ayarlanırsa, `CreateUserWizardStep` parolayı görüntülemez ve parolayı onaylayın. Bunun yerine, yeni oluşturulan kullanıcının parolası `Membership` sınıfının [`GeneratePassword` yöntemi](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)kullanılarak otomatik olarak oluşturulur. `GeneratePassword` yöntemi, yapılandırılan parola gücü gereksinimlerini karşılamak için, belirtilen uzunlukta ve yeterince alfasayısal olmayan karakter uzunluğunda bir parola oluşturur.

[`MailDefinition` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) , hesap oluşturma işlemi sırasında belirtilen e-posta adresine bir e-posta göndermek istiyorsanız yararlıdır. `MailDefinition` özelliği, oluşturulan e-posta iletisiyle ilgili bilgileri tanımlamaya yönelik bir dizi alt özellikler içerir. Bu alt özellikler `Subject`, `Priority`, `IsBodyHtml`, `From`, `CC`ve `BodyFileName`gibi seçenekleri içerir. [`BodyFileName` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) , e-posta iletisinin gövdesini içeren bir metın veya HTML dosyasına işaret eder. Gövde önceden tanımlanmış iki yer tutucuyu destekler: `<%UserName%>` ve `<%Password%>`. `BodyFileName` dosyasında varsa, bu yer tutucular, yalnızca yeni oluşturulan kullanıcının adı ve parolasıyla birlikte değişir.

> [!NOTE]
> `CreateUserWizard` denetiminin `MailDefinition` özelliği yalnızca yeni bir hesap oluşturulduğunda gönderilen e-posta iletisiyle ilgili ayrıntıları belirtir. E-posta iletisinin gerçekten gönderilme hakkında herhangi bir ayrıntı içermez (yani, bir SMTP sunucusu veya posta bırakma dizininin kullanılıp kullanılmadığını, herhangi bir kimlik doğrulama bilgisini vb.). Bu alt düzey ayrıntıların `Web.config``<system.net>` bölümünde tanımlanması gerekir. Bu yapılandırma ayarları hakkında daha fazla bilgi ve ASP.NET 2,0 adresinden e-posta gönderme hakkında daha fazla bilgi için [ASP.NET 2,0 ' de e-posta göndererek](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)SystemNetMail.com ve makalemdeki [SSS](http://www.systemnetmail.com/) bölümüne bakın.

### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>Olay Işleyicilerini kullanarak CreateUserWizard davranışını genişletme

CreateUserWizard denetimi, iş akışı sırasında birkaç olay oluşturur. Örneğin, bir ziyaretçi Kullanıcı adı, parola ve diğer ilgili bilgileri girdikten sonra Kullanıcı Oluştur düğmesine tıkladıktan sonra, CreateUserWizard denetimi [`CreatingUser` olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx)başlatır. Oluşturma işlemi sırasında bir sorun varsa [`CreateUserError` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) tetiklenir; Ancak, Kullanıcı başarıyla oluşturulduysa [`CreatedUser` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) tetiklenir. Ortaya çıkan ek CreateUserWizard denetim olayları vardır, ancak bunlar en fazla üç gere.

Belirli senaryolarda, uygun olay için bir olay işleyicisi oluşturarak yapabilmemiz CreateUserWizard iş akışına dokunmak istiyoruz. Bunu göstermek için, Kullanıcı adı ve parola üzerinde bazı özel doğrulama eklemek üzere `RegisterUser` CreateUserWizard denetimini geliştirelim. Özellikle, Kullanıcı adlarının başında veya sonunda boşluk içerememesi ve Kullanıcı adının parolanın herhangi bir yerde görünememesi için CreateUserWizard ' yi geliştirelim. Kısacası, birisinin "Scott" gibi bir Kullanıcı adı oluşturmasını veya Scott ve Scott. 1234 gibi bir Kullanıcı adı/parola birleşimine sahip olmasını engellemek istiyoruz.

Bunu gerçekleştirmek için, ek doğrulama denetimlerini gerçekleştirmek üzere `CreatingUser` olayı için bir olay işleyicisi oluşturacağız. Sağlanan veriler geçerli değilse, oluşturma işlemini iptal etmeniz gerekir. Ayrıca, Kullanıcı adının veya parolanın geçersiz olduğunu belirten bir ileti göstermek için sayfaya bir etiket Web denetimi eklememiz gerekir. CreateUserWizard denetiminin altına bir etiket denetimi ekleyerek başlayın, `ID` özelliğini `InvalidUserNameOrPasswordMessage` ve `ForeColor` özelliğini `Red`olarak ayarlar. `Text` özelliğini temizleyin ve `EnableViewState` ve `Visible` özelliklerini false olarak ayarlayın.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample7.aspx)]

Sonra, CreateUserWizard denetiminin `CreatingUser` olayı için bir olay işleyicisi oluşturun. Bir olay işleyicisi oluşturmak için, tasarımcıda denetimi seçin ve ardından Özellikler penceresi gidin. Buradan, şimşek simgesi simgesine tıklayın ve ardından olay işleyicisini oluşturmak için uygun olaya çift tıklayın.

`CreatingUser` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-vb[Main](creating-user-accounts-vb/samples/sample8.vb)]

CreateUserWizard denetimine girilen Kullanıcı adı ve parolanın sırasıyla [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx) ve [`Password` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)aracılığıyla kullanılabildiğini unutmayın. Sağlanan kullanıcı adının baştaki veya sondaki boşluklar içerip içermediğini ve Kullanıcı adının parola içinde bulunup bulunmadığını anlamak için yukarıdaki olay işleyicisinde bu özellikleri kullanırız. Bu koşullardan biri karşılanıyorsa, `InvalidUserNameOrPasswordMessage` etiketinde bir hata iletisi görüntülenir ve olay işleyicisinin `e.Cancel` özelliği `True`olarak ayarlanır. `e.Cancel` `True`olarak ayarlanırsa, CreateUserWizard kısa süreli iş akışını, Kullanıcı hesabı oluşturma işlemini etkin bir şekilde iptal etmek için devre dışı.

Şekil 15, Kullanıcı başında boşluk olan bir Kullanıcı adı girdiğinde `CreatingUserAccounts.aspx` ekran görüntüsünü gösterir.

[Baştaki veya sondaki boşluklarla ![kullanıcı adlarıyla Izin verilmez](creating-user-accounts-vb/_static/image44.png)](creating-user-accounts-vb/_static/image43.png)

**Şekil 15**: baştaki veya sondaki boşluklara sahip olan kullanıcı adlarıyla izin verilmez ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-user-accounts-vb/_static/image45.png))

> [!NOTE]
> *<a id="_msoanchor_11">[ ](storing-additional-user-information-vb.md)</a>Ek kullanıcı bilgilerini depolama* öğreticisinde CreateUserWizard denetiminin `CreatedUser` olayını kullanma örneği görüyoruz.

## <a name="summary"></a>Özet

`Membership` sınıfının `CreateUser` yöntemi, üyelik çerçevesinde yeni bir kullanıcı hesabı oluşturur. Bu, yapılandırılan üyelik sağlayıcısına yapılan çağrının yetkisini alarak bunu yapar. `SqlMembershipProvider`durumda, `CreateUser` yöntemi `aspnet_Users` ve `aspnet_Membership` veritabanı tablolarına bir kayıt ekler.

Yeni Kullanıcı hesapları programlı bir şekilde oluşturulabilmesini sağlarken (5. adımda gördüğünüz gibi), daha hızlı ve kolay bir yaklaşım CreateUserWizard denetimini kullanmaktır. Bu denetim, Kullanıcı bilgilerini toplamak ve üyelik çerçevesinde yeni bir kullanıcı oluşturmak için çok adımlı bir kullanıcı arabirimi oluşturur. Bu denetim, kapsamalar altında, 5. adımda incelendiğiyle aynı `Membership.CreateUser` yöntemini kullanır, ancak denetim kullanıcı arabirimini, doğrulama denetimlerini oluşturur ve bir kod tat yazmak zorunda kalmadan kullanıcı hesabı oluşturma hatalarına yanıt verir.

Bu noktada, Yeni Kullanıcı hesapları oluşturmak için işlevselliğe sahip olacak. Ancak, oturum açma sayfası yine de ikinci öğreticide geri belirttiğimiz sabit kodlu kimlik bilgileri için doğrulanıyor. <a id="_msoanchor_12"> </a> [Sonraki öğreticide](validating-user-credentials-against-the-membership-user-store-vb.md) , kullanıcının sağlanan kimlik bilgilerini üyelik çerçevesine göre doğrulamak için `Login.aspx` güncelleştireceğiz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [`CreateUser` teknik belgeler](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [CreateUserWizard denetimine genel bakış](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [Dosya sistemi tabanlı bir site eşleme sağlayıcısı oluşturma](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [ASP.NET 2,0 sihirbaz denetimiyle adım adım kullanıcı arabirimi oluşturma](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [ASP.NET 2.0 'ın site gezintisi inceleniyor](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Ana sayfalar ve site gezintisi](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [Beklediğiniz SQL site eşleme sağlayıcısı](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni bir Murphy idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](creating-the-membership-schema-in-sql-server-vb.md)
> [İleri](validating-user-credentials-against-the-membership-user-store-vb.md)
