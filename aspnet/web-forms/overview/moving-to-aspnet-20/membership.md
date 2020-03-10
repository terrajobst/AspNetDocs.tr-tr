---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: Üyelik | Microsoft Docs
author: microsoft
description: ASP.NET üyeliği, ASP.NET 1. x adresinden Forms kimlik doğrulama modelinin başarısı üzerinde oluşturulur. ASP.NET Forms kimlik doğrulaması, incorp için uygun bir yol sağlar...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642158"
---
# <a name="membership"></a>Üyelik

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET üyeliği, ASP.NET 1. x adresinden Forms kimlik doğrulama modelinin başarısı üzerinde oluşturulur. ASP.NET Forms kimlik doğrulaması, ASP.NET uygulamanıza oturum açma formu eklemenin ve bir veritabanı ya da başka bir veri deposuna karşı kullanıcıları doğrulamanın kolay bir yolunu sağlar.

ASP.NET üyeliği, ASP.NET 1. x adresinden Forms kimlik doğrulama modelinin başarısı üzerinde oluşturulur. ASP.NET Forms kimlik doğrulaması, ASP.NET uygulamanıza oturum açma formu eklemenin ve bir veritabanı ya da başka bir veri deposuna karşı kullanıcıları doğrulamanın kolay bir yolunu sağlar. FormsAuthentication sınıfının üyeleri, kimlik bilgilerinin kimlik bilgilerini işlemesini, geçerli bir oturum açma olup olmadığını kontrol etmek, bir kullanıcının oturumunu günlüğe kaydetmek için mümkün hale getirir. Ancak, Forms kimlik doğrulamasının bir ASP.NET 1. x uygulamasında uygulanması için bir miktar kod gerekebilir.

ASP.NET 2,0 ' de üyelik, tek başına form kimlik doğrulaması kullanmanın önemli bir gelişimidir. (Üyelik, Forms kimlik doğrulamasıyla birlikte kullanıldığında en sağlam bir gereksinimdir, ancak form kimlik doğrulaması kullanılması bir gereksinim değildir.) Yakında gördüğünüz gibi, ASP.NET üyeliğini ve ASP.NET 2,0 ' de oturum açma denetimlerini kullanarak bir çok kodu hiç yazmadan güçlü bir üyelik sistemi uygulayabilirsiniz.

## <a name="implementing-membership-in-aspnet-20"></a>ASP.NET 2,0 ' de üyelik uygulama

Üyelik dört adımdan sonraki bir şekilde uygulanır. Dahil edilen birçok alt adım ve ayrıca uygulanabilecek isteğe bağlı yapılandırma olduğunu unutmayın. Bu adımlar, üyeliği yapılandırmanın büyük resmini göstermek için tasarlanmıştır.

1. Üyelik veritabanınızı oluşturun (SQL Server üyelik deposu olarak kullanılır.)
2. Uygulama yapılandırma dosyalarınızda üyelik seçeneklerini belirtin. (Üyelik varsayılan olarak etkindir.)
3. Kullanmak istediğiniz üyelik deposunun türünü saptayın. Seçenekler şunlardır: 

    - Microsoft SQL Server (sürüm 7,0 veya üzeri)
    - Active Directory deposu
    - Özel üyelik sağlayıcısı
4. Uygulamayı ASP.NET Forms kimlik doğrulaması için yapılandırın. Bir kez daha, üyelik Forms kimlik doğrulamasından faydalanmak için tasarlanmıştır, ancak form kimlik doğrulamasının kullanılması bir gereklilik değildir.
5. Üyelik için Kullanıcı hesaplarını tanımlayın ve isterseniz rolleri yapılandırın.

## <a name="creating-the-membership-database"></a>Üyelik veritabanı oluşturuluyor

Üyelik depoluyorsanız SQL Server 7,0 veya sonraki bir sürümünü kullanıyorsanız, veritabanınızı yapılandırmak için ASPNET\_regsql yardımcı programını (Visual Studio .NET 2005 komut Isteminden en kolay şekilde kullanılabilir) kullanabilirsiniz. ASPNET\_regsql yardımcı programı, bir komut istemi aracı veya bir GUI Sihirbazı aracılığıyla kullanılabilir. Sihirbaz yöntemi, veritabanınızı yapılandırmanın en kolay yoludur. Sihirbaza erişmek için aşağıdaki komutu çalıştırmanız yeterlidir:

`aspnet_regsql W`

Bu komutu çalıştırdığınızda, aşağıda gösterildiği gibi ASP.NET SQL Server Kurulum Sihirbazı görüntülenir.

![](membership/_static/image1.jpg)

**Şekil 1**

ASP.NET SQL Server Kurulum Sihirbazı, sihirbazda belirttiğiniz örnekte Web sitesini oluşturur. Ancak, ASP.NET, veritabanınıza bağlanmak için Machine. config dosyasındaki bağlantı dizesini kullanır. Varsayılan olarak, bu bağlantı dizesi bir SQL Server 2005 örneğine işaret eder, bu nedenle SQL Server 2000 veya SQL Server 7,0 örneği kullanıyorsanız, Machine. config dosyasındaki bağlantı dizesini değiştirmeniz gerekecektir. Bu bağlantı dizesi şurada bulunabilir:

[!code-xml[Main](membership/samples/sample1.xml)]

Ne yazık ki bağlantı dizesini değiştirmezseniz, ASP.NET açıklayıcı bir hata vermeyecektir. Veritabanını oluşturduğmadığınız söyleyerek şikayet etmeye devam eder. Yukarıdaki durumda, bağlantı dizesini yerel SQL Server 2000 örneğinden işaret etmek üzere değiştirdim.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>Yapılandırma belirtme ve Kullanıcı ve rol ekleme

Üyeliği yapılandırmanın bir sonraki adımı, gerekli bilgileri uygulamanın Web. config dosyasına eklemektir. ASP.NET 1. x içinde, Web. config dosyasının değiştirilmesi, küçük harfli ve IntelliSense 'in olmamasından dolayı bazen zor. Visual Studio .NET 2005, yapılandırma dosyaları için, görevi IntelliSense ile çok daha kolay hale getirir, ancak ASP.NET 2,0, yapılandırma dosyalarını düzenleyerek bir Web arabirimi sağlayarak bir adım daha artar.

Web arabirimini aşağıda gösterildiği gibi Çözüm Gezgini araç çubuğundaki ASP.NET yapılandırma düğmesine tıklayarak başlatabilirsiniz. Ayrıca, oturum açma denetimleri eklenirken görüntülenen açılır pencereler aracılığıyla Web arabirimini de başlatabilirsiniz.

![](membership/_static/image2.jpg)

**Şekil 2**

Bu, aşağıda gösterilen ASP.NET Web sitesi yönetim aracını başlatır. ASP.NET Web sitesi yönetimi, uygulama ayarlarının yönetilmesini kolaylaştıran dört sekmeli bir arabirimdir. Aşağıdaki sekmeler mevcuttur:

- **Sayfa**
- **Güvenlik** Kullanıcıları, rolleri ve erişimi yapılandırın.
- **Uygulama** Uygulama ayarlarını yapılandırın.
- **Sağlayıcı** Uygulamalarınızın üyelik sağlayıcınızı yapılandırın ve test edin.

Web sitesi yönetim aracı kolayca yeni kullanıcı oluşturmanıza, yeni roller oluşturmanıza ve kullanıcıları ve rolleri yönetmenize olanak sağlar. Bu özellik Windows arabiriminde kullanılamaz. Windows arabirimi, Web sitesi yönetim aracında olmayan yetkilendirme ayarlarını kolayca tanımlamanızı ve sağlayıcılar ekleme, silme ve yönetme olanakları sağlar.

Windows arabirimini başlatmak için Internet Information Services ek bileşenini açın, uygulamanıza sağ tıklayın ve Özellikler ' i seçin. ASP.NET sekmesine tıklayın ve ardından yapılandırmayı Düzenle düğmesine tıklayın. (Yapılandırma Düzenle düğmesinin etkinleştirilmesi için uygulamanın ASP.NET 2,0 altında çalışıyor olması gerekir. ASP.NET sürümünü ASP.NET iletişim kutusunda da yapılandırabilirsiniz.) ASP.NET yapılandırma ayarları iletişim kutusu aşağıda gösterildiği gibi görüntülenir.

![](membership/_static/image3.jpg)

**Şekil 3**

Genel sekmesinde, bağlantı dizeleri ve uygulama ayarları listelenir. İtalik ayarları bir üst yapılandırma dosyasında (Machine. config veya Web. config daha yüksek bir düzeyde) tanımlanır ve italik olmayan ayarlar uygulama yapılandırma dosyasından alınır. Uygulama düzeyinde bir ayar eklenirse, kaldırılırsa veya düzenlenirse, ASP.NET ayarı, devralınan yapılandırma dosyasından kaldırmak yerine Web. config uygulama düzeylerinde ayarı ekler, kaldırır veya değiştirir.

Kimlik doğrulama sekmesi aşağıda gösterilmiştir. Üyelik ayarlarınızı yapılandıracaksınız. Forms kimlik doğrulama ayarları, üyelik sağlayıcıları ve rol sağlayıcıları burada yapılandırılabilir.

![](membership/_static/image4.jpg)

**Şekil 4**

## <a name="implementing-membership-in-your-application"></a>Uygulamanızda üyelik uygulama

Uygulamanıza ASP.NET 2,0 üyeliği uygulamanın en kolay yolu, belirtilen oturum açma denetimlerini kullanmaktır. Bu yöntem, hiçbir kodu yazmadan ASP.NET 2,0 üyelik temellerini uygulamanıza olanak tanır.

ASP.NET 2,0 ' de aşağıdaki oturum açma denetimleri mevcuttur:

## <a name="login-control"></a>Oturum açma denetimi

Oturum açma denetimi, birisinin üyelik sisteminizde oturum açmasını sağlayan bir arabirim sağlar. Bir Kullanıcı adı ve parola metin kutusu ve oturum açma düğmesi sağlar. Henüz yapılmamış kişilere kaydolma bağlantısı gibi diğer birçok ortak özellik, kullanıcının sonraki ziyaretlerde otomatik olarak oturum açmasına izin veren bir onay kutusu, parola anımsatıcısı için bir bağlantı ve vb. Oturum açma denetiminin tüm özellikleri, denetimin özellikleri aracılığıyla özelleştirilebilir.

ASP.NET 1. x içinde, geliştiricilerin form kimlik doğrulaması kullanırken arama yapmak için bir miktar kod yazması gerekiyordu. ASP.NET 2,0 üyeliğiyle, hiçbir kodu yazmadan kullanıcıları doğrulayabilirsiniz. ASP.NET, kullanıcının sizin için otomatik olarak görünmesini sağlayacak. (ASP.NET üyeliğini kullanmadan oturum açma denetimini kullanıyorsanız, kullanıcıyı doğrulamak için **OnAuthenticate** yöntemini kullanabilirsiniz.)

## <a name="loginview-control"></a>LoginView denetimi

LoginView denetimi, varsayılan olarak iki şablon sağlayan şablonlu bir denetimdir; AnonymousTemplate ve LoggedInTemplate. Görüntülenen şablon, kullanıcının üyelik sisteminizde oturum açmış olup olmadığına göre belirlenir. Bu denetim genellikle kullanıcı oturum açmadığında bir oturum açma denetimini ve Kullanıcı oturum açtığında bir LoginStatus denetimi ve/veya diğer oturum açma denetimlerini göstermek için kullanılır. ASP.NET uygulamanızda rol yönetimi kullanıyorsanız, LoginView denetimi kullanıcı rolünü temel alan belirli bir şablonu görüntüleyebilir. (Daha fazla ASP.NET rol yönetimi daha sonra ele alınacaktır.)

## <a name="passwordrecovery-control"></a>PasswordRecovery denetimi

PasswordRecovery denetimi, kullanıcıların geçerli parolasıyla bir e-posta almasına veya parolasını sıfırlamasına olanak sağlar. Şifresiz metin ve şifrelenmiş parolalar kurtarılabilir ve kullanıcılara gönderilebilir. Parola karma hale getirilir, kurtarılamaz. Bunun yerine kullanıcının parola sıfırlama yapması gerekecektir.

## <a name="loginstatus-control"></a>LoginStatus denetimi

LoginStatus denetimi oturum açan kullanıcılar için bir oturum açma göstergesi ve şu anda oturum açmış kullanıcılar için bir oturum kapatma göstergesi göstermek için kullanılır. Request. IsAuthenticated özelliği görüntülenecek göstergeyi tespit etmek için kullanılır. LoginStatus denetimi tarafından görünen gösterge, metin ( **LoginText** ve **LogoutText** özellikleri ile uygulanabilir) veya görüntülerle ( **LoginImageUrl** ve **LogoutImageUrl** özellikleri ile uygulanır) olabilir.

Bir Kullanıcı LoginStatus denetimi aracılığıyla oturum açtığında **LogoutPageUrl** özelliği tarafından belirtilen URL 'ye yeniden yönlendirilir. Bu özellik ayarlanmamışsa, geçerli sayfa yenilenir. Site muhtemelen form kimlik doğrulaması tarafından korunduğu için, geçerli sayfanın yenilenmesi, kullanıcıyı site için oturum açma sayfasına yönlendirecektir.

## <a name="loginname-control"></a>LoginName denetimi

LoginName denetimi şu anda sitede oturum açmış olan kullanıcının Kullanıcı adını görüntüler.

## <a name="createuserwizard-control"></a>CreateUserWizard denetimi

CreateUserWizard denetimi kullanıcılara üyelik sisteminize kaydolmak için uygun bir yol sağlar. Aşağıda gösterilen arabirimi kullanarak adımları (WizardSteps koleksiyonu olarak uygulanır) ekleyebilirsiniz.

![](membership/_static/image5.jpg)

**Şekil 5**

CreateUserWizard, sihirbaz sınıfından türetilen ve aşağıdaki şablonları sağlayan şablonlu bir denetimdir:

- **HeaderTemplate** Bu şablon, sihirbazın üstbilgisinin görünümünü denetler.
- **SideBarTemplate** Bu şablon, sihirbazın kenar çubuğunun görünümünü denetler.
- **StartNavigationTemplate** Bu şablon, başlangıç adımındaki sihirbazın Gezinti görünümünü denetler.
- **StepNavigationTemplate** Bu şablon, başlangıç veya bitiş adımında değil, gezinti alanının görünümünü denetler.
- **Sonlandırhnavigationtemplate** Bu şablon, son adımla gezinti alanının görünümünü denetler.

Ayrıca, sihirbaza eklediğiniz her adım için, ASP.NET, bu adım için hem ContentTemplate hem de CustomNavigationTemplate içeren özel bir şablon oluşturur. CreateUserWizard özelleştirme hakkında tam Ayrıntılar için VS.NET 2005 belgelerine bakın:

## <a name="changepassword-control"></a>ChangePassword denetimi

ChangePassword denetimi, kullanıcıların parolasını değiştirmesine izin verir. DisplayUserName özelliği true ise (varsayılan olarak false 'dur), Kullanıcı oturum açmadıklarında parolasını değiştirebilir. Kullanıcı *zaten oturum* açmışsa ve DisplayUserName özelliği true ise, Kullanıcı bu kullanıcının kullanıcı kimliğini öğrendikleri için oturum açmamış başka bir kullanıcının parolasını değiştirebilir.

Kullanıcıların oturum açmak zorunda kalmadan parola değiştirebilmesini isterseniz, ChangePassword denetiminin görüntülendiği sayfanın anonim erişime izin verdiğinden emin olmanız gerekir. Kullanıcının parolasını değiştirmek için eski parolalarını sağlaması gerekir.

## <a name="role-management"></a>Rol Yönetimi

Rol yönetimi, kullanıcıları belirli bir role atamanıza ve sonra belirli dosya veya klasörlere erişimi bu role göre kısıtlayabilmenizi sağlar. Rol yönetimi aynı zamanda bir API sağlar, böylece bir rolü programlı bir şekilde belirleyebilir veya belirli bir roldeki tüm kullanıcıları belirleyebilir ve buna uygun şekilde yanıt verebilirsiniz.

Rol yönetimi, ASP.NET üyeliğinde bir gereklilik değildir ve rol yönetiminin kullanılabilmesi için bir gereksinim üyeliğidir. Ancak, her birinin iki eki de, geliştiricilerin bunları birbirleriyle birlikte kullanmaları olasıdır.

Uygulamanızda rol yönetimini etkinleştirmek için Web. config dosyanızda aşağıdaki değişikliği yapın:

[!code-xml[Main](membership/samples/sample2.xml)]

**CacheRolesInCookie** özniteliği true olarak ayarlandığında ASP.net, istemcideki bir tanımlama bilgisinde bir kullanıcı rolü üyeliğini önbelleğe alır. Bu, rol aramalarının RoleProvider 'a çağrılar olmadan oluşmasına izin verir. Bu öznitelik kullanılırken, geliştiricilerin, **pişirme** ve tüm özellik olarak ayarlandığından emin olmak önerilir. (Bu, varsayılan ayardır.) Bu, tanımlama bilgisi verilerinin şifrelenmesini sağlar ve tanımlama bilgilerinin içeriklerinin değiştirilmediğinden emin olmaya yardımcı olur. Roller, Web sitesi yönetim aracı kullanılarak eklenebilir. Rolleri kolayca tanımlamanızı, bu rollere göre sitenin bölümlerine erişimi yapılandırmanızı ve rolleri kullanıcılara atamanızı sağlar.

![](membership/_static/image6.jpg)

**Şekil 6**

Yukarıda gösterildiği gibi, yeni roller yalnızca rolün adını girip rol Ekle ' ye tıklanarak eklenebilir. Varolan roller listesinde uygun bağlantıya tıklanarak, mevcut roller yönetilebilir veya silinebilir.

Bir rolü yönetirken, aşağıda gösterildiği gibi kullanıcı ekleyebilir veya kaldırabilirsiniz.

![](membership/_static/image7.jpg)

**Şekil 7**

Kullanıcının rol onay kutusunda olduğunu kontrol ederek, belirli bir role kolayca kullanıcı ekleyebilirsiniz. ASP.NET, üyelik veritabanınızı uygun girişlerle otomatik olarak güncelleştirir. Ayrıca, uygulamanız için erişim kurallarını yapılandırmak isteyeceksiniz. ASP.NET 1. x geliştiricileri, Web. config dosyasındaki &lt;Authorization&gt; öğesi aracılığıyla bunu yapmaya tanıdık ve bu seçenek ASP.NET 2,0 ' de hala kullanılabilir. Ancak, aşağıda gösterildiği gibi web sitesi yönetim aracı 'nı kullanarak erişim kurallarını yönetmek daha kolay olur.

![](membership/_static/image8.jpg)

**Şekil 8**

Bu durumda, Yönetim klasörü vurgulanır (Bu, aracın açık gri renkle vurgulandığı için, görme zordur) ve yöneticiler rolüne erişim verildi. Diğer tüm kullanıcılar reddedilir. Baş simgesine tıklayarak bir kural seçebilir ve sonra kuralları düzenlemek için yukarı taşı ve Aşağı Taşı düğmelerini kullanabilirsiniz. ASP.NET &lt;Authorization&gt; öğesinde olduğu gibi, kurallar göründükleri sırada işlenir. Diğer bir deyişle, yukarıdaki görüntüsündeki kuralların sırası ters çevrilirse, ASP.NET ' nin karşılaştığı ilk kural, klasörü herkesin engellediği kural olacağı için yönetim klasörüne hiç kimse erişemez.

ASP.NET 2,0, bir erişim kuralı belirttiğiniz klasöre bir Web. config dosyası ekler. Erişim kuralları, yapılandırma dosyası veya Web sitesi yönetim aracı aracılığıyla düzenlenebilir. Diğer bir deyişle, Web sitesi yönetim aracı yalnızca yapılandırma dosyasının Kullanıcı dostu bir ortamda düzenlenebildiği bir arabirimdir.

## <a name="using-roles-in-code"></a>Koddaki rolleri kullanma

Rol yönetimi için API, sürüm 1. x sürümünden beri değişmemiştir. IBir kullanıcının belirli bir rolde olup olmadığını anlamak için **IsInRole** yöntemi kullanılır.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET ayrıca geçerli bağlamın üyesi olarak bir RolePrincipal örneği oluşturur. RolePrincipal nesnesi, kullanıcının sahip olduğu tüm rolleri almak için aşağıdaki gibi kullanılabilir:

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>LoginView denetimiyle RoleGroups kullanma

Rol yönetimi ve üyelik hakkında daha fazla bilgiye sahip olduğunuza göre, ASP.NET 2,0 ' de LoginView denetiminin bu özellikten nasıl yararlandığını kısaca ele almanızı sağlar. Daha önce anlatıldığı gibi, LoginView denetimi varsayılan olarak iki şablon içeren şablonlu bir denetimdir; AnonymousTemplate ve LoggedInTemplate. LoginView görevleri iletişim kutusunda RoleGroups ' i düzenlemenizi sağlayan bir bağlantıdır (aşağıda gösterilmiştir).

![](membership/_static/image9.jpg)

**Şekil 9**

Her RoleGroup nesnesi, RoleGroup 'un hangi rollere uygulanacağını tanımlayan bir dize dizisi içerir. LoginView denetimine yeni bir RoleGroup eklemek için RoleGroups düzenle bağlantısına tıklayın. Yukarıdaki görüntüde, Yöneticiler için yeni bir RoleGroup ekledim olduğunu görebilirsiniz. Görünümler açılan listesinden bu RoleGroup ' u (RoleGroup [0]) seçerek, yalnızca Yöneticiler rolü üyelerine görüntülenecek olan bir şablonu yapılandırabiliyorum. Aşağıdaki görüntüde, satış rolü ve dağıtım rolü üyeleri için geçerli olan yeni bir RoleGroup ekledik. Bu, LoginView görevleri iletişim kutusunda görünümler açılan listesine ikinci bir RoleGroup ekler ve bu şablona eklenen her şey, satış veya dağıtım rolünde herhangi bir kullanıcı tarafından görülebilir.

![](membership/_static/image10.jpg)

**Şekil 10**

## <a name="overriding-the-existing-membership-provider"></a>Mevcut üyelik sağlayıcısını geçersiz kılma

ASP.NET üyelik işlevlerini genişletebilmeniz için birkaç yol vardır. İlki, bundan devralarak ve yöntemlerini geçersiz kılarak SqlMembershipProvider sınıfının mevcut işlevselliğini açıkça değiştirebilirsiniz. Örneğin, kullanıcılar oluşturulduğunda kendi işlevselliklerinizi uygulamak istiyorsanız, SqlMembershipProvider 'dan devralan kendi sınıfınızı aşağıdaki gibi oluşturabilirsiniz:

[!code-csharp[Main](membership/samples/sample5.cs)]

Diğer taraftan, kendi sağlayıcınızı oluşturmak isterseniz (üyelik bilgilerinizi bir erişim veritabanında depolamak için, örneğin), kendi sağlayıcınızı oluşturabilirsiniz.

## <a name="creating-your-own-membership-provider"></a>Kendi üyelik sağlayıcınızı oluşturma

Kendi üyelik sağlayıcınızı oluşturmak için önce MembershipProvider sınıfından devralan bir sınıf oluşturmanız gerekir. VB.NET kullanıyorsanız, Visual Studio 2005, geçersiz kılmak için ihtiyaç duyduğunuz tüm yöntemlerin saplamalarını ekler. Kullanıyorsanız C#, saplamaları eklemek için en fazla.

Aşağıdakileri geçersiz kılmanız gerekir:

- ApplicationName özelliği
- ChangePassword işlevi
- ChangePasswordQuestionAndAnswer işlevi
- CreateUser işlevi
- DeleteUser işlevi
- EnablePasswordReset özelliği
- Enablepasswordalımı özelliği
- FindUsersByEmail işlevi
- FindUsersByName işlevi
- GetAllUsers işlevi
- GetNumberOfUsersOnline işlevi
- GetPassword işlevi
- GetUser işlevi
- GetUserNameByEmail işlevi
- MaxInvalidPasswordAttempts özelliği
- Minrequirednonalfanümerik özelliği
- MinRequiredPasswordLength özelliği
- PasswordAttemptWindow özelliği
- PasswordFormat özelliği
- PasswordStrengthRegularExpression özelliği
- RequiresQuestionAndAnswer özelliği
- RequiresUniqueEmail Özelliği
- ResetPassword işlevi
- Kullanıcı işlevinin kilidini aç
- UpdateUser işlevi
- ValidateUser işlevi

C# Geliştirici olarak uygulanacak bir listeyi oldukça bir şekilde. Sınıfı herhangi bir uygulama olmadan VB.NET içinde oluşturmayı ve sonra kodu dönüştürmek için .NET Yansıtıcıyı veya benzer bir aracı kullanmayı daha kolay bulabilirsiniz C#.

Başlatma yönteminde bağlantı dizesi ve diğer özellikler varsayılan olarak ayarlanmalıdır. (Sağlayıcı çalışma zamanında yüklendiğinde Initialize yöntemi tetiklenir.) Initialize yönteminin ikinci parametresi System. Collections. Custom. NameValueCollection türündedir ve Web. config dosyasında özel sağlayıcınızda ilişkili &lt;Add&gt; öğesine başvurudur. Bu girdi aşağıdakine benzer şekilde görünür:

[!code-xml[Main](membership/samples/sample6.xml)]

Initialize yöntemine bir örnek aşağıda verilmiştir.

[!code-csharp[Main](membership/samples/sample7.cs)]

Kullanıcı, oturum açma formunuzu gönderdikten sonra doğrulamak için, ValidateUser yöntemini kullanmanız gerekir. Bu yöntem, Kullanıcı Login denetimindeki Login düğmesine tıkladığında ateşlenir. Bu yöntemde Kullanıcı araması yapan kodunuzu yerleştirebilirsiniz.

Gördüğünüz gibi, kendi üyelik sağlayıcınızı yazmak zor değildir ve ASP.NET 2,0 'in bu güçlü işlevlerini genişletmenizi sağlar.
