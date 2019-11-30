---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
title: Rolleri oluşturma ve yönetme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğretici, roller çerçevesini yapılandırmak için gerekli olan adımları inceler. Bundan sonra, rolleri oluşturmak ve silmek için Web sayfaları oluşturacağız.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 113f10b3-a19a-471b-8ff6-db3c79ce8a91
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
msc.type: authoredcontent
ms.openlocfilehash: a7883d0b05f2fa5a3fdac887f8c8b39d70418fb3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595959"
---
# <a name="creating-and-managing-roles-c"></a>Rolleri Oluşturma ve Yönetme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.09.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_cs.pdf)

> Bu öğretici, roller çerçevesini yapılandırmak için gerekli olan adımları inceler. Bundan sonra, rolleri oluşturmak ve silmek için Web sayfaları oluşturacağız.

## <a name="introduction"></a>Giriş

<a id="_msoanchor_1"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisinde, bir sayfa kümesinden belirli kullanıcıları kısıtlamak için URL yetkilendirmesi kullanma ve bir ASP.net sayfasının işlevselliğini ziyaret eden kullanıcıya göre ayarlamak için programlı teknikler hakkında baktık. Kullanıcı tarafından Kullanıcı bazında sayfa erişimi veya işlevselliği için izin verilmesi, ancak çok sayıda kullanıcı hesabının olduğu ve kullanıcıların ayrıcalıkların genellikle değişmediği senaryolarda bir bakım olabilir. Bir Kullanıcı belirli bir görevi gerçekleştirmek için Yetkilendirmeyi her aldığında veya kaybettiğinde, yöneticinin uygun URL yetkilendirme kurallarını, bildirime dayalı biçimlendirmeyi ve kodu güncelleştirmesi gerekir.

Genellikle kullanıcıları gruplar veya *Roller* halinde sınıflandırarak, rol rol temelinde izinleri uygulamanıza yardımcı olur. Örneğin, çoğu Web uygulamasında yalnızca yönetici kullanıcılar için ayrılan belirli bir sayfa veya görev kümesi vardır. *Kullanıcı tabanlı yetkilendirme* öğreticisinde öğrenilen teknikleri kullanarak, belirtilen kullanıcı hesaplarının yönetim görevlerini gerçekleştirmesine izin vermek IÇIN uygun URL yetkilendirme kurallarını, bildirime dayalı biçimlendirmeyi ve kodu ekleyeceğiz. Ancak yeni bir yönetici eklendiyse veya yönetim haklarının iptal edilmesini sağlamak için gerekli olan bir yönetici varsa, yapılandırma dosyalarını ve Web sayfalarını döndürmemiz ve güncelleştirmeniz gerekir. Ancak, roller ile yöneticiler adlı bir rol oluşturabilir ve bu güvenilir kullanıcıları Yöneticiler rolüne atayabilirsiniz. Daha sonra, yönetici rolünün çeşitli yönetim görevlerini gerçekleştirmesine izin vermek için uygun URL yetkilendirme kurallarını, bildirime dayalı biçimlendirmeyi ve kodu ekleyeceğiz. Bu altyapı söz konusu olduğunda, siteye yeni yöneticiler eklemek veya var olanları kaldırmak, kullanıcıyı dahil etmek veya Yöneticiler rolünden kaldırmak kadar basittir. Yapılandırma, bildirime dayalı biçimlendirme veya kod değişikliği gerekli değildir.

ASP.NET rolleri tanımlamak ve bunları Kullanıcı hesaplarıyla ilişkilendirmek için bir rol çerçevesi sunar. Rol çerçevesi ile roller oluşturup silebilir, bir role kullanıcı ekleyebilir veya gruptan kullanıcıları kaldırabilir, belirli bir role ait olan kullanıcı kümesini belirleyebilir ve bir kullanıcının belirli bir role ait olup olmadığını anlayabilirsiniz. Rol çerçevesi yapılandırıldıktan sonra, URL Yetkilendirme kuralları aracılığıyla bir rol temelinde görevlere erişimi sınırlayabilir ve şu anda oturum açmış olan kullanıcının rollerine bağlı olarak bir sayfada ek bilgi ya da işlevsellik gösterebilir veya gizleyebilirsiniz.

Bu öğretici, roller çerçevesini yapılandırmak için gerekli olan adımları inceler. Bundan sonra, rolleri oluşturmak ve silmek için Web sayfaları oluşturacağız. <a id="_msoanchor_2"> </a> [*Kullanıcılara roller atama*](assigning-roles-to-users-cs.md) öğreticisinde, rolleri Kullanıcı ekleme ve rollerden kaldırma bölümüne bakacağız. Rol <a id="_msoanchor_3"> </a> [*tabanlı yetkilendirme*](role-based-authorization-cs.md) öğreticisinde, bir rol rol temelinde sayfalara erişimi, ziyaret eden kullanıcının rolüne bağlı olarak sayfa işlevselliğinin nasıl ayarlanacağını öğreneceğiz. Haydi başlayın!

## <a name="step-1-adding-new-aspnet-pages"></a>1\. Adım: yeni ASP.NET sayfaları ekleme

Bu öğreticide ve sonraki iki adımda, rollerle ilgili çeşitli işlevler ve yetenekler incelenmeyecektir. Bu öğreticiler genelinde incelenen konuları uygulamak için bir dizi ASP.NET sayfasına ihtiyacımız olacak. Bu sayfaları oluşturalım ve site haritasını güncelleştirlim.

`Roles`adlı projede yeni bir klasör oluşturarak başlayın. Sonra, `Roles` klasöre dört yeni ASP.NET sayfası ekleyerek her sayfayı `Site.master` ana sayfayla bağlantılandırın. Sayfaları adlandırın:

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

Bu noktada, projenizin Çözüm Gezgini Şekil 1 ' de gösterilen ekran görüntüsüne benzer olması gerekir.

[Roller klasörüne dört yeni sayfa ![eklenmiştir](creating-and-managing-roles-cs/_static/image2.png)](creating-and-managing-roles-cs/_static/image1.png)

**Şekil 1**: `Roles` klasöre dört yeni sayfa eklenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image3.png))

Her sayfa, her bir ana sayfanın Contenttutucuları: `MainContent` ve `LoginContent`olmak üzere iki Içerik denetimine sahip olmalıdır.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample1.aspx)]

`LoginContent` ContentPlaceHolder 'ın varsayılan biçimlendirmesinin, kullanıcının kimliğinin doğrulanmadığına bağlı olarak, oturum açma veya site oturumunu kapatma bağlantısı görüntülediğini geri çekin. Ancak ASP.NET sayfasındaki Içerik denetiminin `Content2` varlığı, ana sayfanın varsayılan işaretlemesini geçersiz kılar. <a id="_msoanchor_4"> </a> [*Form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-cs.md) konusunda anlatıldığı gibi, varsayılan biçimlendirmeyi geçersiz kılmak, oturum açma ile ilgili seçenekleri sol sütunda göstermek istemediğimiz sayfalarda yararlıdır.

Bununla birlikte, bu dört sayfa için ana sayfanın varsayılan biçimlendirmesini `LoginContent` ContentPlaceHolder olarak göstermek istiyoruz. Bu nedenle, `Content2` Içerik denetimi için bildirim temelli biçimlendirmeyi kaldırın. Bunu yaptıktan sonra dört sayfa biçimlendirmesinin her biri yalnızca bir Içerik denetimi içermelidir.

Son olarak, site haritasını (`Web.sitemap`) bu yeni Web sayfalarını içerecek şekilde güncelleştirelim. Üyelik öğreticileri için eklediğimiz `<siteMapNode>` sonra aşağıdaki XML 'i ekleyin.

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample2.xml)]

Site Haritası güncelleştirildikten sonra, siteyi bir tarayıcı aracılığıyla ziyaret edin. Şekil 2 ' de gösterildiği gibi, sol taraftaki Gezinti artık rol öğreticilerine yönelik öğeler içerir.

[Roller klasörüne dört yeni sayfa ![eklenmiştir](creating-and-managing-roles-cs/_static/image5.png)](creating-and-managing-roles-cs/_static/image4.png)

**Şekil 2**: `Roles` klasöre dört yeni sayfa eklenmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image6.png))

## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>2\. Adım: roller çerçeve sağlayıcısını belirtme ve yapılandırma

Üyelik çerçevesi gibi, rol çerçevesi de sağlayıcı modeline göre oluşturulmuştur. <a id="_msoanchor_5"> </a> [*Güvenlik temelleri ve ASP.NET Destek*](../introduction/security-basics-and-asp-net-support-cs.md) öğreticisinde açıklandığı gibi .NET Framework üç yerleşik rol sağlayıcısıyla birlikte gelir: [`AuthorizationStoreRoleProvider`](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx), [`WindowsTokenRoleProvider`](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)ve [`SqlRoleProvider`](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx). Bu öğretici serisi, rol deposu olarak bir Microsoft SQL Server veritabanı kullanan `SqlRoleProvider`odaklanır.

Altında, rollerinin çerçevesini ve `SqlRoleProvider`, üyelik çerçevesi ve `SqlMembershipProvider`gibi çalışır. .NET Framework, rol çerçevesine API görevi gören bir `Roles` sınıfı içerir. `Roles` sınıfında `CreateRole`, `DeleteRole`, `GetAllRoles`, `AddUserToRole`, `IsUserInRole`gibi statik yöntemler bulunur. Bu yöntemlerin biri çağrıldığında `Roles` sınıfı, yapılandırılan sağlayıcıya çağrıyı devreder. `SqlRoleProvider`, yanıt olarak role özgü tablolar (`aspnet_Roles` ve `aspnet_UsersInRoles`) ile birlikte kullanılabilir.

Uygulamamızda `SqlRoleProvider` sağlayıcıyı kullanmak için, mağaza olarak kullanılacak veritabanını belirtmemiz gerekir. `SqlRoleProvider`, belirtilen rol mağazasının belirli veritabanı tabloları, görünümler ve saklı yordamları olmasını bekler. Bu önkoşul veritabanı nesneleri [`aspnet_regsql.exe` aracı](https://msdn.microsoft.com/library/ms229862.aspx)kullanılarak eklenebilir. Bu noktada, `SqlRoleProvider`için gereken şemaya sahip bir veritabanı zaten var. <a id="_msoanchor_6"> </a> [*SQL Server öğreticide üyelik şeması oluşturmaya*](../membership/creating-the-membership-schema-in-sql-server-cs.md) geri döndüğünüzde, `SecurityTutorials.mdf` adlı bir veritabanı oluşturdunuz ve `SqlRoleProvider`gereken veritabanı nesnelerini içeren uygulama hizmetlerini eklemek için `aspnet_regsql.exe` kullandınız. Bu nedenle, roller çerçevesini rol desteğini etkinleştirmek ve `SqlRoleProvider` rol deposu olarak `SecurityTutorials.mdf` veritabanı ile kullanmak için söylememiz gerekir.

Rol çerçevesi, uygulamanın `Web.config` dosyasındaki &lt;`roleManager`&gt; öğesi aracılığıyla yapılandırılır. Rol desteği varsayılan olarak devre dışıdır. Bunu etkinleştirmek için, [&lt;`roleManager`&gt;](https://msdn.microsoft.com/library/ms164660.aspx) öğenin `enabled` `true` özniteliğini şöyle olacak şekilde ayarlamanız gerekir:

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample3.xml)]

Varsayılan olarak, tüm Web uygulamalarının `SqlRoleProvider`türünde `AspNetSqlRoleProvider` adlı bir rol sağlayıcısı vardır. Bu varsayılan sağlayıcı `machine.config` kaydedilir (`%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`konumunda bulunur):

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample4.xml)]

Sağlayıcının `connectionStringName` özniteliği kullanılan rol deposunu belirtir. `AspNetSqlRoleProvider` sağlayıcı, bu özniteliği aynı zamanda `machine.config` ve `LocalSqlServer`olarak, `App_Data` adlı `aspnet.mdf`klasöründeki bir SQL Server 2005 Express Sürüm veritabanına da tanımlanmış olarak ayarlar.

Sonuç olarak, uygulamanın `Web.config` dosyasında herhangi bir sağlayıcı bilgisi belirtmeden rol çerçevesini etkinleştireceğiz, uygulama varsayılan kayıtlı rol sağlayıcısını kullanır, `AspNetSqlRoleProvider`. `~/App_Data/aspnet.mdf` veritabanı yoksa, ASP.NET çalışma zamanı otomatik olarak oluşturur ve uygulama Hizmetleri şemasını ekler. Ancak, `aspnet.mdf` veritabanını kullanmak istemiyorum; Bunun yerine, önceden oluşturmuş olduğumuz `SecurityTutorials.mdf` veritabanını kullanmak ve uygulama Hizmetleri şemasını eklemek istiyoruz. Bu değişiklik, iki şekilde gerçekleştirilebilir:

- <strong>`Web.config`</strong><strong>`LocalSqlServer`</strong> <strong>bağlantı dizesi adı</strong> <strong>için bir değer belirtin</strong> <strong>.</strong> `Web.config``LocalSqlServer` bağlantı dizesi adı değerinin üzerine yazarak, varsayılan kayıtlı rol sağlayıcısını (`AspNetSqlRoleProvider`) kullanabilir ve `SecurityTutorials.mdf` veritabanıyla doğru bir şekilde çalışabilir. Bu teknik hakkında daha fazla bilgi için bkz. [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin blog gönderisi, [SQL Server 2000 veya SQL Server 2005 kullanmak için ASP.NET 2,0 uygulama hizmetleri yapılandırma](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>`SqlRoleProvider`türünde yeni bir kayıtlı sağlayıcı ekleyin</strong> <strong>ve</strong> <strong>`connectionStringName`</strong>ayarını<strong>`SecurityTutorials.mdf`</strong> <strong>veritabanına</strong> <strong>işaret etmek üzere</strong> yapılandırın. Bu, önerilen ve SQL Server öğreticide <a id="_msoanchor_7"> </a> [*Üyelik şeması oluşturma*](../membership/creating-the-membership-schema-in-sql-server-cs.md) bölümünde kullanılan yaklaşım ve bu öğreticide de kullandığım yaklaşımdır.

Aşağıdaki rol yapılandırması işaretlemesini `Web.config` dosyasına ekleyin. Bu biçimlendirme `SecurityTutorialsSqlRoleProvider`adlı yeni bir sağlayıcı kaydeder.

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample5.xml)]

Yukarıdaki biçimlendirme `SecurityTutorialsSqlRoleProvider` varsayılan sağlayıcı olarak tanımlar (`<roleManager>` öğesinde `defaultProvider` özniteliği aracılığıyla). Ayrıca, `SecurityTutorialsSqlRoleProvider``applicationName` ayarını üyelik sağlayıcısı tarafından kullanılan `applicationName` ayarı olan `SecurityTutorials`olarak ayarlar (`SecurityTutorialsSqlMembershipProvider`). Burada gösterilmediğinden, `SqlRoleProvider` için [`<add>` öğesi](https://msdn.microsoft.com/library/ms164662.aspx) , veritabanı zaman aşımı süresini saniye cinsinden belirtmek için bir `commandTimeout` özniteliği de içerebilir. Varsayılan değer 30 ' dur.

Bu yapılandırma işaretlemesi varken, uygulamamız içinde rol işlevselliğini kullanmaya başlamaya hazırız.

> [!NOTE]
> Yukarıdaki yapılandırma biçimlendirmesinde, &lt;`roleManager`&gt; öğesinin `enabled` ve `defaultProvider` özniteliklerinin kullanımı gösterilmektedir. Rol çerçevesinin Kullanıcı bazında rol bilgilerini nasıl ilişkilendirdiğini etkileyen çeşitli öznitelikler vardır. <a id="_msoanchor_8"> </a> [*Rol tabanlı yetkilendirme*](role-based-authorization-cs.md) öğreticisinde bu ayarları inceleyeceğiz.

## <a name="step-3-examining-the-roles-api"></a>3\. Adım: rol API 'sini Inceleme

Roller çerçevesinin işlevselliği, rol tabanlı işlemleri gerçekleştirmek için on dört statik yöntem içeren [`Roles` sınıfı](https://msdn.microsoft.com/library/system.web.security.roles.aspx)aracılığıyla sunulur. 4 ve 6. adımlarda rol oluşturma ve silme konusunda baktığımızda, sistemden bir rol ekleyen veya bir rol ekleyen [`CreateRole`](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx) ve [`DeleteRole`](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx) yöntemlerini kullanacağız.

Sistemdeki tüm rollerin bir listesini almak için [`GetAllRoles` yöntemi](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx) kullanın (bkz. 5. adım). [`RoleExists` yöntemi](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx) , belirtilen bir rolün var olup olmadığını gösteren bir Boole değeri döndürür.

Sonraki öğreticide, kullanıcıların rollerle nasıl ilişkilendirileceğini inceleyeceğiz. `Roles` sınıfın [`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx), [`AddUserToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx), [`AddUsersToRole`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)ve [`AddUsersToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx) yöntemleri bir veya daha fazla role bir veya daha fazla kullanıcı ekler. Kullanıcıları rollerden kaldırmak için [`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx), [`RemoveUserFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx), [`RemoveUsersFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)veya [`RemoveUsersFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx) yöntemlerini kullanın.

<a id="_msoanchor_9"> </a> [*Rol tabanlı yetkilendirme*](role-based-authorization-cs.md) öğreticisinde, şu anda oturum açmış olan kullanıcının rolüne bağlı olarak işlevselliği programlı bir şekilde gösterme veya gizleme yollarına bakacağız. Bunu gerçekleştirmek için `Role` sınıfının [`FindUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx), [`GetRolesForUser`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx), [`GetUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)veya [`IsUserInRole`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx) yöntemlerini kullanabiliriz.

> [!NOTE]
> Bu yöntemlerin birinin çağrılışında `Roles` sınıfı, yapılandırılan sağlayıcıya çağrıyı devreder. Bu durumda, çağrının `SqlRoleProvider`gönderildiği anlamına gelir. `SqlRoleProvider`, çağrılan yönteme göre uygun veritabanı işlemini gerçekleştirir. Örneğin, kod `Roles.CreateRole("Administrators")`, Yöneticiler adlı `aspnet_Roles` tabloya yeni bir kayıt ekleyen `aspnet_Roles_CreateRole` saklı yordamını yürüten `SqlRoleProvider` sonuçlanır.

Bu öğreticinin geri kalanı, sistemdeki rolleri yönetmek için `Roles` sınıfının `CreateRole`, `GetAllRoles`ve `DeleteRole` yöntemlerini kullanmaya bakar.

## <a name="step-4-creating-new-roles"></a>4\. Adım: yeni roller oluşturma

Roller, kullanıcıları rastgele gruplamak için bir yol sunar ve en yaygın olarak bu gruplandırma, yetkilendirme kuralları uygulamak için daha uygun bir yol için kullanılır. Ancak, rolleri bir yetkilendirme mekanizması olarak kullanmak için önce uygulamada bulunan rolleri tanımlamanız gerekir. Ne yazık ki, ASP.NET bir CreateRoleWizard denetimi içermez. Yeni roller eklemek için uygun bir kullanıcı arabirimi oluşturmak ve API kendimize rollerini çağırmak gerekir. İyi haber, bunun kolayca gerçekleştirilmesi çok kolaydır.

> [!NOTE]
> CreateRoleWizard Web denetimi olmasa da, Web uygulamanızın yapılandırmasını görüntülemeye ve yönetmeye yardımcı olmak üzere tasarlanmış bir yerel ASP.NET uygulaması olan [ASP.NET Web sitesi yönetim aracı](https://msdn.microsoft.com/library/ms228053.aspx)vardır. Ancak, ASP.NET Web sitesi yönetim aracının iki nedenden dolayı büyük bir fanı olmadım. İlk olarak, bu biraz hata yaşar ve Kullanıcı deneyimi istenen kadar çok kalır. İkincisi, ASP.NET Web sitesi yönetim aracı yalnızca yerel olarak çalışacak şekilde tasarlanmıştır, yani canlı bir sitede rolleri uzaktan yönetmeniz gerekiyorsa kendi rol yönetimi Web sayfalarınızı oluşturmanız gerekecektir. Bu iki nedenden dolayı, bu öğretici ve bir sonraki, ASP.NET Web sitesi yönetim aracına güvenmek yerine, gerekli rol yönetim araçlarını bir Web sayfasında oluşturmaya odaklanacaktır.

`Roles` klasöründeki `ManageRoles.aspx` sayfasını açın ve sayfaya bir TextBox ve bir Button Web denetimi ekleyin. TextBox denetiminin `ID` özelliğini `RoleName` ve düğmenin `ID` ve `Text` özellikleri sırasıyla `CreateRoleButton` ve rol oluştur olarak ayarlayın. Bu noktada, sayfanızın bildirime dayalı biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample6.aspx)]

Sonra, `Click` olay işleyicisi oluşturmak için tasarımcıda `CreateRoleButton` Button denetimine çift tıklayın ve ardından aşağıdaki kodu ekleyin:

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample7.cs)]

Yukarıdaki kod, `newRoleName` değişkenine `RoleName` metin kutusuna girilen bölünen rol adı atanarak başlatılır. Daha sonra, rol `newRoleName` sistemde zaten mevcut olup olmadığını anlamak için `Roles` sınıfının `RoleExists` yöntemi çağırılır. Rol yoksa, `CreateRole` yöntemine yapılan bir çağrı aracılığıyla oluşturulur. `CreateRole` yöntemi sistemde zaten bulunan bir rol adı geçirtiyse, bir `ProviderException` özel durumu oluşturulur. Bu, kodun, `CreateRole`çağrılmadan önce rolün zaten sistemde mevcut olmadığından emin olmak için ilk kez kontrol eder. `Click` olay işleyicisi `RoleName` TextBox 'ın `Text` özelliğini temizleyerek sonlanır.

> [!NOTE]
> Kullanıcı `RoleName` metin kutusuna herhangi bir değer girmezse ne olacağını merak ediyor olabilirsiniz. `CreateRole` yöntemine geçirilen değer `null` veya boş bir dize ise, bir özel durum oluşturulur. Benzer şekilde, rol adı virgül içeriyorsa bir özel durum oluşturulur. Sonuç olarak, sayfa, kullanıcının bir rol girip hiç virgül içermediğinden emin olmak için doğrulama denetimleri içermelidir. Okuyucu için alıştırma olarak bırakıyorum.

Yöneticiler adlı bir rol oluşturalım. `ManageRoles.aspx` sayfasını bir tarayıcıda ziyaret edin, metin kutusuna Yöneticiler yazın (bkz. Şekil 3) ve ardından rol Oluştur düğmesine tıklayın.

[![yönetici rolü oluşturma](creating-and-managing-roles-cs/_static/image8.png)](creating-and-managing-roles-cs/_static/image7.png)

**Şekil 3**: bir yönetici rolü oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image9.png))

Ne olur? Geri gönderme gerçekleşir, ancak rolün sisteme gerçekten eklenmiş olduğu görsel bir ipucu yoktur. Bu sayfayı, adım 5 ' te görsel geri bildirim içerecek şekilde güncelleştireceğiz. Ancak şimdilik, `SecurityTutorials.mdf` veritabanına giderek ve `aspnet_Roles` tablosundan verileri görüntüleyerek rolün oluşturulduğunu doğrulayabilirsiniz. Şekil 4 ' te gösterildiği gibi, `aspnet_Roles` tablosu, yalnızca eklenen Yöneticiler rolleri için bir kayıt içerir.

[![aspnet_Roles tablosunda Yöneticiler için bir satır bulunur](creating-and-managing-roles-cs/_static/image11.png)](creating-and-managing-roles-cs/_static/image10.png)

**Şekil 4**: `aspnet_Roles` tablosu Yöneticiler Için bir satıra sahiptir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image12.png))

## <a name="step-5-displaying-the-roles-in-the-system"></a>5\. Adım: rolleri sistemde görüntüleme

`ManageRoles.aspx` sayfasını, sistemdeki geçerli rollerin bir listesini içerecek şekilde kullanalım. Bunu gerçekleştirmek için, sayfaya bir GridView denetimi ekleyin ve `ID` özelliğini `RoleList`olarak ayarlayın. Ardından, aşağıdaki kodu kullanarak, sayfanın arka plan kod sınıfına `DisplayRolesInGrid` bir yöntem ekleyin:

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample8.cs)]

`Roles` sınıfının `GetAllRoles` yöntemi, sistemdeki tüm rolleri dize dizisi olarak döndürür. Bu dize dizisi daha sonra GridView 'a bağlanır. Sayfa ilk yüklendiğinde rol listesini GridView 'a bağlamak için, sayfanın `Page_Load` olay işleyicisinden `DisplayRolesInGrid` yöntemini çağırmanız gerekir. Aşağıdaki kod, sayfa ilk kez ziyaret edildiğinde, sonraki geri göndermeler üzerinde değil, bu yöntemi çağırır.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample9.cs)]

Bu kodla birlikte, sayfayı bir tarayıcıdan ziyaret edin. Şekil 5 ' i gösterdiği gibi, öğe etiketli tek sütunlu bir kılavuz görmeniz gerekir. Kılavuz 4. adımda eklediğimiz Yöneticiler rolü için bir satır içerir.

[GridView ![rolleri tek bir sütunda görüntülüyor](creating-and-managing-roles-cs/_static/image14.png)](creating-and-managing-roles-cs/_static/image13.png)

**Şekil 5**: GridView, rolleri tek bir sütunda görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image15.png))

GridView, GridView 'un `AutoGenerateColumns` özelliği true olarak ayarlandığı için (varsayılan) GridView 'un `DataSource`her özellik için otomatik olarak bir sütun oluşturmasına neden olan bir tek sütunu, öğe olarak etiketlenmiş bir sütun görüntüler. Bir dizinin dizideki öğeleri temsil eden tek bir özelliği vardır, bu nedenle GridView 'daki tek sütun.

GridView ile verileri görüntülerken, GridView tarafından örtülü olarak oluşturulmasını sağlamak yerine sütunlarımı açıkça tanımlamanızı tercih ediyorum. Sütunları açıkça tanımlayarak, verileri biçimlendirmek, sütunları yeniden düzenlemek ve diğer ortak görevleri gerçekleştirmek çok daha kolaydır. Bu nedenle, sütunlarının açıkça tanımlanması için GridView 'un bildirim temelli işaretlemesini güncelleştirelim.

GridView 'un `AutoGenerateColumns` özelliğini false olarak ayarlayarak başlayın. Ardından, kılavuza bir TemplateField ekleyin, `HeaderText` özelliğini roller olarak ayarlayın ve `ItemTemplate` dizinin içeriğini görüntüleyecek şekilde yapılandırın. Bunu gerçekleştirmek için, `ItemTemplate` `RoleNameLabel` adlı bir etiket Web denetimi ekleyin ve `Text` özelliğini `Container.DataItem`bağlayın.

Bu özellikler ve `ItemTemplate`içerikleri bildirimli olarak veya GridView 'un alanlar iletişim kutusu ve düzenleme şablonları arabirimi aracılığıyla ayarlanabilir. Alanlar iletişim kutusuna ulaşmak için GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayın. Sonra, `AutoGenerateColumns` özelliğini false olarak ayarlamak için alanları otomatik oluştur onay kutusunun işaretini kaldırın ve GridView 'a bir TemplateField ekleyin ve `HeaderText` özelliğini role olarak ayarlayın. `ItemTemplate`içeriğini tanımlamak için GridView 'un akıllı etiketindeki Şablonları Düzenle seçeneğini belirleyin. Bir etiket Web denetimini `ItemTemplate`sürükleyin, `ID` özelliğini `RoleNameLabel`olarak ayarlayın ve `Text` özelliğinin `Container.DataItem`'e bağlanması için veri bağlama ayarlarını yapılandırın.

Kullandığınız yaklaşımdan bağımsız olarak, oluşturduğunuz zaman, GridView 'un elde edilen bildirim zaman biçimlendirmesi aşağıdakine benzer görünmelidir.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample10.aspx)]

> [!NOTE]
> Dizinin içerikleri, `<%# Container.DataItem %>`DataBinding sözdizimi kullanılarak görüntülenir. GridView 'a göre bir dizinin içeriğini görüntülerken bu sözdiziminin neden kullanıldığı hakkında kapsamlı bir açıklama, Bu öğreticinin kapsamının dışındadır. Bu konuyla ilgili daha fazla bilgi için, bir [skalar diziyi veri Web denetimine bağlama](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)konusuna bakın.

Şu anda, `RoleList` GridView yalnızca sayfa ilk kez ziyaret edildiğinde rol listesine bağlanır. Her yeni rol eklendiğinde Kılavuzu yenilememiz gerekir. Bunu gerçekleştirmek için, yeni bir rol oluşturulduysa `CreateRoleButton` düğmenin `Click` olay işleyicisini `DisplayRolesInGrid` yöntemini çağıracak şekilde güncelleştirin.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample11.cs)]

Artık Kullanıcı yeni bir rol eklediğinde `RoleList` GridView, geri gönderme sırasında hemen eklenen rolü gösterir ve bu da rolün başarıyla oluşturulduğu görsel geri bildirim sağlar. Bunu göstermek için, bir tarayıcı aracılığıyla `ManageRoles.aspx` sayfasını ziyaret edin ve Supervisors adlı bir rol ekleyin. Rol Oluştur düğmesine tıklandıktan sonra, bir geri gönderme yapılır ve kılavuz, yeni rol, süper yönetici ve yöneticiler dahil olmak üzere günceldir.

[![ana bilgisayar rolü eklendi](creating-and-managing-roles-cs/_static/image17.png)](creating-and-managing-roles-cs/_static/image16.png)

**Şekil 6**: Supervisors rolü eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image18.png))

## <a name="step-6-deleting-roles"></a>6\. Adım: rolleri silme

Bu noktada, bir Kullanıcı yeni bir rol oluşturabilir ve `ManageRoles.aspx` sayfasından tüm mevcut rolleri görüntüleyebilir. Ayrıca kullanıcıların rolleri silmesine izin verlim. `Roles.DeleteRole` yönteminin iki aşırı yüklemesi vardır:

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) - *roleName*rolünü siler. Rol bir veya daha fazla üye içeriyorsa bir özel durum oluşturulur.
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) - *roleName*rolünü siler. *ThrowOnPopulateRole* `true`ise, rol bir veya daha fazla üye içeriyorsa bir özel durum oluşturulur. *ThrowOnPopulateRole* `false`ise, rol, üye içerip içermediğini değil, silinir. Dahili olarak, `DeleteRole(roleName)` yöntemi `DeleteRole(roleName, true)`çağırır.

*Rolename* `null` veya boş bir dize veya *roleName* bir virgül içeriyorsa `DeleteRole` yöntemi de bir özel durum oluşturur. *RoleName* sistemde yoksa, `DeleteRole` özel durum oluşturmadan sessizce başarısız olur.

`ManageRoles.aspx` ' deki GridView 'u, tıklandığı zaman seçili rolü sildiği bir Delete düğmesi içerecek şekilde kullanalım. Alanlar iletişim kutusuna gidip CommandField seçeneğinin altında bulunan bir Delete düğmesi ekleyerek GridView 'a bir Delete düğmesi ekleyerek başlayın. Sil düğmesini en soldaki sütunda yapın ve `DeleteText` özelliğini rol sil olarak ayarlayın.

[![RoleList GridView öğesine Delete düğmesi ekleyin](creating-and-managing-roles-cs/_static/image20.png)](creating-and-managing-roles-cs/_static/image19.png)

**Şekil 7**: `RoleList` GridView 'A bir Delete düğmesi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-and-managing-roles-cs/_static/image21.png))

Sil düğmesi eklendikten sonra, GridView 'un bildirime dayalı biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample12.aspx)]

Sonra, GridView 'un `RowDeleting` olayı için bir olay işleyicisi oluşturun. Bu, rol Sil düğmesine tıklandığında geri gönderme sırasında oluşturulan olaydır. Olay işleyicisine aşağıdaki kodu ekleyin.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample13.cs)]

Kod, rol Sil düğmesine tıklandığı satırdaki `RoleNameLabel` Web denetimine programlı olarak başvuruda bulunarak başlatılır. `Roles.DeleteRole` yöntemi daha sonra çağrılır, `RoleNameLabel` ve `false``Text` geçirerek rolü ile ilişkili herhangi bir kullanıcı olup olmamasına bakılmaksızın rolü de silinir. Son olarak, `RoleList` GridView yenilenir, böylece yalnızca, silinen rol artık kılavuzda görünmez.

> [!NOTE]
> Rolü Sil düğmesi, rolü silmeden önce kullanıcıdan herhangi bir onay sıralaması gerektirmez. Bir eylemi onaylamaya yönelik en kolay yollarından biri, istemci tarafı onaylama iletişim kutusunu kullanmaktır. Bu teknik hakkında daha fazla bilgi için bkz. [silerken Istemci tarafı onaylama ekleme](https://asp.net/learn/data-access/tutorial-42-cs.aspx).

## <a name="summary"></a>Özet

Birçok Web uygulamasının belirli yetkilendirme kuralları veya yalnızca belirli kullanıcı sınıfları tarafından kullanılabilen sayfa düzeyi işlevleri vardır. Örneğin, yalnızca yöneticilerin erişebileceği bir Web sayfaları kümesi olabilir. Bu yetkilendirme kurallarını bir kullanıcı temelinde tanımlamak yerine, kuralları bir role göre tanımlamak daha yararlıdır. Diğer bir deyişle, Scott ve Jisun 'ın Yönetim Web sayfalarına erişmesine açıkça izin vermek yerine, daha sürdürülebilir bir yaklaşım Yöneticiler rolünün üyelerinin bu sayfalara erişmesine izin vermek ve ardından Scott ve Jisun 'ın Yöneticiler rolü.

Rol çerçevesi, rolleri oluşturmayı ve yönetmeyi kolaylaştırır. Bu öğreticide roller çerçevesinin rol deposu olarak bir Microsoft SQL Server veritabanı kullanan `SqlRoleProvider`kullanmak için nasıl yapılandırılacağı incelendi. Ayrıca, sistemde var olan rolleri listeleyen bir Web sayfası Oluşturulduk ve yeni rollerin oluşturulmasına ve mevcut olanların silinmesine izin verir. Sonraki öğreticilerde, rollerin kullanıcılara nasıl atanacağını ve rol tabanlı yetkilendirmeyi nasıl uygulayacağınızı görüyoruz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 2.0 'ın üyeliğini, rollerini ve profilini İnceleme](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Nasıl yapılır: ASP.NET 2,0 ' de rol yöneticisini kullanma](https://msdn.microsoft.com/library/ms998314.aspx)
- [Rol sağlayıcıları](https://msdn.microsoft.com/library/aa478950.aspx)
- [Kendi web sitesi yönetim aracınızı toplama](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [`<roleManager>` öğesi için teknik belgeler](https://msdn.microsoft.com/library/ms164660.aspx)
- [Üyelik ve rol Yöneticisi API 'Lerini kullanma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Alicja Maziarz, suchi Banerjee ve Teresa Murphy ' i içerir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Next](assigning-roles-to-users-cs.md)
