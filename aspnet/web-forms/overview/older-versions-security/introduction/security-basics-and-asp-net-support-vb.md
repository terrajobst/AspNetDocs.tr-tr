---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
title: Güvenlik temelleri ve ASP.NET desteği (VB) | Microsoft Docs
author: rick-anderson
description: Bu, bir Web formu aracılığıyla ziyaretçilerin kimliğini doğrulamaya yönelik teknikleri keşfedebileceğiniz ve partic 'e erişim yetkisi veren bir öğretici serisinin ilk öğreticisidir...
ms.author: riande
ms.date: 01/13/2008
ms.assetid: ab68a92b-fc81-40a4-a7dc-406625d2c5d4
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
msc.type: authoredcontent
ms.openlocfilehash: 99e986013cb5a923ddb150022013e3a75852ce55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575343"
---
# <a name="security-basics-and-aspnet-support-vb"></a>Temel Güvenlik Kavramları ve ASP.NET Desteği (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_vb.pdf)

> Bu, bir Web formu aracılığıyla ziyaretçilerin kimliğini doğrulama, belirli sayfalara ve işlevlere erişimi yetkilendirme ve bir ASP.NET uygulamasındaki Kullanıcı hesaplarını yönetme tekniklerini keşfedeceğim bir dizi öğreticideki ilk öğreticidir.

## <a name="introduction"></a>Giriş

BT forumları, eCommerce siteleri, çevrimiçi e-posta web siteleri, Portal Web siteleri ve sosyal ağ sitelerinin hepsi ortak bir şeydir? Hepsi *Kullanıcı hesapları*sunar. Kullanıcı hesapları sunan sitelerde bir dizi hizmet sağlanmalıdır. En azından yeni ziyaretçilerin bir hesap oluşturabilmesinin yanı sıra ziyaretçilerin oturum açabiliyor olması gerekir. Bu tür web uygulamaları, oturum açmış kullanıcıya göre kararlar alabilir: bazı sayfalar veya eylemler yalnızca oturum açmış kullanıcılarla veya belirli bir kullanıcı alt kümesiyle kısıtlanabilir. diğer sayfalar, oturum açmış kullanıcıya özgü bilgileri gösterebilir veya sayfayı görüntüleyen kullanıcının ne olduğuna bağlı olarak daha fazla veya daha az bilgi gösterebilir.

Bu, bir Web formu aracılığıyla ziyaretçilerin kimliğini doğrulama, belirli sayfalara ve işlevlere erişimi yetkilendirme ve bir ASP.NET uygulamasındaki Kullanıcı hesaplarını yönetme tekniklerini keşfedeceğim bir dizi öğreticideki ilk öğreticidir. Bu öğreticilerin kursa göre şunları nasıl yapılacağını inceleyeceğiz:

- Bir Web sitesinde kullanıcıları tanımla ve günlüğe kaydet
- ASP kullanın. Kullanıcı hesaplarını yönetmek için NET 'in üyelik çerçevesi
- Kullanıcı hesapları oluşturun, güncelleştirin ve silin
- Oturum açmış kullanıcı tabanlı bir Web sayfasına, dizine veya belirli bir işlevselliğe erişimi sınırlayın
- ASP kullanın. Kullanıcı hesaplarını rollerle ilişkilendirmek için NET 'in rol çerçevesi
- Kullanıcı rollerini yönetme
- Oturum açmış kullanıcının rolüne bağlı olarak bir Web sayfası, dizin veya belirli bir işlevselliğe erişimi sınırlayın
- ASP 'yi özelleştirin ve genişletin. NET ' in güvenlik Web denetimleri

Bu öğreticilerin kısa olması ve işlem boyunca görsel olarak size yol göstermek için çok sayıda ekran görüntüsü ile adım adım yönergeler sağlaması gerekir. Her öğretici, C# ve Visual Basic sürümlerde mevcuttur ve kullanılan kodun tamamını karşıdan yükleme içerir. (Bu ilk öğretici, üst düzey bir bakış açısından güvenlik kavramlarına odaklanmaktadır ve bu nedenle herhangi bir ilişkili kod içermez.)

Bu öğreticide, Forms kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rolleri uygulama konusunda yardımcı olmak için önemli güvenlik kavramlarını ve ASP.NET 'de hangi tesislerin kullanılabildiğini tartışacağız. Haydi başlayın!

> [!NOTE]
> Güvenlik, fiziksel, teknolojik ve ilke kararlarını kapsayan tüm uygulamaların önemli bir yönüdür ve yüksek düzeyde planlama ve etki alanı bilgisi gerektirir. Bu öğretici serisi, güvenli Web uygulamaları geliştirmeye yönelik bir kılavuz olarak tasarlanmamıştır. Bunun yerine, özellikle form kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rollere odaklanır. Bu sorunlar etrafında dönen bazı güvenlik kavramları bu seride tartışılıyor olsa da, diğerleri araştırılmayan.

## <a name="authentication-authorization-user-accounts-and-roles"></a>Kimlik doğrulama, yetkilendirme, Kullanıcı hesapları ve roller

Kimlik doğrulama, yetkilendirme, Kullanıcı hesapları ve roller, bu öğretici serisinin tamamında çok sık kullanılacak dört terimdir, bu nedenle bu terimleri web güvenliği bağlamında tanımlamak için kısa bir süre sonra almak istiyorum. Internet gibi bir istemci-sunucu modelinde, sunucunun isteği yapan istemciyi tanımlaması için gereken birçok senaryo vardır. *Kimlik doğrulaması* , istemcinin kimliğini belirlememe işlemidir. Başarıyla tanımlanan bir istemci, *kimlik doğrulama*olarak kabul edilir. Tanımlanamayan bir istemci, *kimliği doğrulanmamış* veya *anonim*olarak kabul edilir.

Güvenli kimlik doğrulama sistemleri, aşağıdaki üç modelden en az birini içerir: [bildiğiniz bir şey, sahip olduğunuz veya sizin oluşturduğunuz](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)bir şeydir. Çoğu Web uygulaması, bir parola veya PIN gibi istemcinin bildiği bir şeyi kullanır. Kullanıcı adını ve parolasını tanımlamak için kullanılan bilgiler, örneğin, *kimlik bilgileri*olarak adlandırılır. Bu öğretici serisi, kullanıcıların kimlik bilgilerini bir Web sayfası formunda sağlayarak sitede oturum açarken kullandığı bir kimlik doğrulama modeli olan *Forms kimlik doğrulamasına*odaklanır. Daha önce bu kimlik doğrulaması türüyle karşılaştık. Herhangi bir eCommerce sitesine gidin. Kullanıma hazır olduğunuzda, bir Web sayfasındaki metin kutularına Kullanıcı adınızı ve parolanızı girerek oturum açmanız istenir.

İstemcileri tanımlamaya ek olarak, bir sunucunun, isteği yapan istemciye bağlı olarak hangi kaynakların veya işlevlerin erişilebilir olduğunu sınırlaması gerekebilir. *Yetkilendirme* , belirli bir kullanıcının belirli bir kaynağa veya işlevselliğe erişme yetkisine sahip olup olmadığını belirleme işlemidir.

*Kullanıcı hesabı* , belirli bir kullanıcı hakkında kalıcı bilgiler için bir depodır. Kullanıcı hesapları, kullanıcının oturum açma adı ve parolası gibi kullanıcıyı benzersiz şekilde tanımlayan bilgileri en az düzeyde içermelidir. Bu temel bilgilerle birlikte, Kullanıcı hesapları şu gibi şeyler içerebilir: kullanıcının e-posta adresi; hesabın oluşturulduğu tarih ve saat; Son oturum açtıkları tarih ve saat; First ve Last adı; telefon numarası; ve posta adresi. Form kimlik doğrulaması kullanılırken, Kullanıcı hesabı bilgileri genellikle Microsoft SQL Server gibi bir ilişkisel veritabanında depolanır.

Kullanıcı hesaplarını destekleyen Web uygulamaları, isteğe bağlı olarak kullanıcıları *rollere*gruplandırabilir. Rol yalnızca bir kullanıcıya uygulanan bir etikettir ve yetkilendirme kurallarını ve sayfa düzeyi işlevselliği tanımlamak için bir soyutlama sağlar. Örneğin, bir Web sitesi, herhangi bir yöneticinin belirli bir Web sayfaları kümesine erişmesini engelleyen yetkilendirme kurallarına sahip bir yönetici rolü içerebilir. Üstelik, tüm kullanıcılar (yönetici olmayanlar dahil) tarafından erişilebilen çeşitli sayfalar ek veriler görüntüleyebilir veya Yöneticiler rolünde kullanıcılar tarafından ziyaret edildiğinde ek işlevsellik sunabilir. Rolleri kullanarak, bu yetkilendirme kurallarını Kullanıcı tarafından değil, rol temelinde tanımlayabiliriz.

## <a name="authenticating-users-in-an-aspnet-application"></a>Bir ASP.NET uygulamasında kullanıcıların kimliğini doğrulama

Bir Kullanıcı bir URL 'YI tarayıcının adres penceresine girdiğinde veya bir bağlantıya tıkladığı zaman, tarayıcı Web sunucusuna belirtilen içerik için bir [Köprü Metni Aktarım Protokolü (http)](http://en.wikipedia.org/wiki/HTTP) isteği koyar, bir ASP.NET sayfası, görüntü, JavaScript dosyası veya başka bir içerik türü olur. Web sunucusu, istenen içeriğin döndürülmesinden sonra yapılır. Bunu yaparken, istek hakkında, isteği kimin yaptığını ve kimliğin istenen içeriği alma yetkisi olup olmadığını içeren bir dizi şeyi belirlemesi gerekir.

Tarayıcılar, varsayılan olarak herhangi bir tanımlama bilgisi sıralaması olmayan HTTP istekleri gönderir. Ancak tarayıcı kimlik doğrulama bilgilerini içeriyorsa, Web sunucusu, isteği yapan istemciyi belirlemeyi deneyen kimlik doğrulama iş akışını başlatır. Kimlik doğrulama iş akışı adımları, Web uygulaması tarafından kullanılan kimlik doğrulaması türüne bağlıdır. ASP.NET üç tür kimlik doğrulamasını destekler: Windows, Passport ve Forms. Bu öğretici serisi, Forms kimlik doğrulamasına odaklanır, ancak Windows kimlik doğrulama Kullanıcı mağazalarını ve iş akışını karşılaştırmak ve karşılaştırmak için bir dakikanızı atalım.

### <a name="authentication-via-windows-authentication"></a>Windows kimlik doğrulaması aracılığıyla kimlik doğrulaması

Windows kimlik doğrulama iş akışı aşağıdaki kimlik doğrulama tekniklerinden birini kullanır:

- Temel kimlik doğrulama
- Özet kimlik doğrulaması
- Windows Tümleşik Kimlik Doğrulaması

Her üç teknik de kabaca aynı şekilde çalışır: yetkisiz, anonim bir istek geldiğinde Web sunucusu, devam etmek için yetkilendirmenin gerekli olduğunu belirten bir HTTP yanıtı geri gönderir. Ardından tarayıcı, kullanıcıdan Kullanıcı adı ve parola isteyen bir kalıcı iletişim kutusu görüntüler (bkz. Şekil 1). Bu bilgiler daha sonra bir HTTP üst bilgisi aracılığıyla Web sunucusuna geri gönderilir.

![Kalıcı Iletişim kutusu kullanıcıdan kimlik bilgilerini Ister](security-basics-and-asp-net-support-vb/_static/image1.png)

**Şekil 1**: kalıcı Iletişim kutusu kullanıcıdan kimlik bilgilerini ister

Sağlanan kimlik bilgileri Web sunucusunun Windows kullanıcı deposunda onaylanır. Bu, Web uygulamanızdaki kimliği doğrulanan her kullanıcının kuruluşunuzda bir Windows hesabı olması gerektiği anlamına gelir. Bu, intranet senaryolarında ortak bir yerdir. Aslında, bir intranet ayarında Windows tümleşik kimlik doğrulaması kullanılırken, tarayıcı otomatik olarak Web sunucusunu ağda oturum açmak için kullanılan kimlik bilgileriyle sağlar ve böylece Şekil 1 ' de gösterilen iletişim kutusunu görünmez. Windows kimlik doğrulaması, intranet uygulamaları için harika olsa da, sitenizde kaydolan her bir kullanıcı için Windows hesapları oluşturmak istemenizden bu yana genellikle Internet uygulamaları için uygun değildir.

### <a name="authentication-via-forms-authentication"></a>Form kimlik doğrulaması aracılığıyla kimlik doğrulaması

Diğer yandan Forms kimlik doğrulaması, Internet Web uygulamaları için idealdir. Form kimlik doğrulamasının, kullanıcının kimlik bilgilerini bir Web formu aracılığıyla girmesini isteyerek kullanıcıyı tanımladığını unutmayın. Sonuç olarak, bir kullanıcı yetkisiz bir kaynağa erişmeyi denediğinde, kimlik bilgilerini girebilecekleri oturum açma sayfasına otomatik olarak yönlendirilir. Gönderilen kimlik bilgileri daha sonra özel bir kullanıcı deposunda (genellikle bir veritabanına) onaylanır.

Gönderilen kimlik bilgilerini doğruladıktan sonra, Kullanıcı için bir *Forms kimlik doğrulama bileti* oluşturulur. Bu bilet, kullanıcının kimliğinin doğrulandığını ve Kullanıcı adı gibi tanımlama bilgilerini içerdiğini belirtir. Forms kimlik doğrulama anahtarı (genellikle) istemci bilgisayarda bir tanımlama bilgisi olarak depolanır. Bu nedenle, Web sitesine yapılan sonraki ziyaretler, HTTP isteğine Forms kimlik doğrulama bileti içerir ve bu sayede Web uygulamasının oturum açtıktan sonra kullanıcıyı tanımlamasına olanak tanır.

Şekil 2 ' de, üst düzey bir vansat noktasından Forms kimlik doğrulama iş akışı gösterilmektedir. ASP.NET ' deki kimlik doğrulama ve yetkilendirme parçalarının iki ayrı varlık olarak nasıl davrandığına dikkat edin. Forms kimlik doğrulama sistemi, kullanıcıyı (veya anonim oldukları raporları) tanımlar. Yetkilendirme sistemi, kullanıcının istenen kaynağa erişip erişemeyeceğini belirler. Kullanıcı yetkilendirilmemiş (ProtectedPage. aspx ' i anonim olarak ziyaret ederken, Şekil 2 ' de olduğu gibi), yetkilendirme sistemi kullanıcının reddedildiğini bildirir ve bu da Forms kimlik doğrulama sisteminin kullanıcıyı otomatik olarak oturum açma sayfasına yönlendirmesine neden olur.

Kullanıcı başarıyla oturum açtıktan sonra, sonraki HTTP istekleri Forms kimlik doğrulama biletini içerir. Forms kimlik doğrulama sistemi kullanıcıyı yalnızca tanımlar. Bu, kullanıcının istenen kaynağa erişip erişemeyeceğini belirleyen yetkilendirme sistemidir.

![Forms kimlik doğrulama Iş akışı](security-basics-and-asp-net-support-vb/_static/image2.png)

**Şekil 2**: Forms kimlik doğrulama iş akışı

Sonraki iki[öğreticinin, form kimlik doğrulaması](an-overview-of-forms-authentication-vb.md) ve [Forms kimlik doğrulama yapılandırmasına ve gelişmiş konulara](forms-authentication-configuration-and-advanced-topics-vb.md)genel bakış hakkında daha ayrıntılı bilgi için form kimlik doğrulamasını ele alınacaktır. Daha fazlası için ASP. NET 'in kimlik doğrulama seçenekleri, bkz. [ASP.NET Authentication](https://msdn.microsoft.com/library/eeyk640h.aspx).

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>Web sayfaları, dizinler ve sayfa Işlevlerine erişimi sınırlandırma

ASP.NET belirli bir kullanıcının belirli bir dosyaya veya dizine erişim yetkisi olup olmadığını belirlemenin iki yolu vardır:

- **Dosya yetkilendirmesi** -ASP.NET sayfaları ve Web Hizmetleri Web sunucusunun dosya sisteminde bulunan dosyalar olarak uygulandığından, bu dosyalara erişim Access Control listeleri (ACL 'ler) ile belirtilebilir. ACL 'Ler Windows hesapları için uygulanan izinler olduğundan, dosya yetkilendirmesi en yaygın olarak Windows kimlik doğrulama ile kullanılır. Form kimlik doğrulaması kullanılırken, siteyi ziyaret eden Kullanıcı ne olursa olsun, tüm işletim sistemi ve dosya sistemi düzeyi istekleri aynı Windows hesabı tarafından yürütülür.
- **URL yetkilendirmesi**-URL yetkilendirmesi ile, sayfa geliştiricisi, Web. config 'de yetkilendirme kurallarını belirtir. Bu yetkilendirme kuralları, hangi kullanıcıların veya rollerin uygulamaya erişmelerine izin verileceğini veya uygulamadaki belirli sayfalara veya dizinlere erişimi reddedildiğini belirtir.

Dosya yetkilendirme ve URL yetkilendirmesi belirli bir ASP.NET sayfasına veya belirli bir dizindeki tüm ASP.NET sayfalarına erişmek için yetkilendirme kuralları tanımlar. Bu teknikleri kullanarak, belirli bir kullanıcı için belirli bir sayfaya istekleri reddetmesini veya bir kullanıcı kümesine erişime izin vermeyi ve diğer herkese erişimi reddetmenizi ASP.NET bildirebilirsiniz. Tüm kullanıcıların sayfaya erişebileceği senaryolar nelerdir, ancak sayfanın işlevselliği kullanıcıya bağlıdır. Örneğin, Kullanıcı hesaplarını destekleyen birçok sitenin, kimliği doğrulanmış kullanıcılar ve anonim kullanıcılara karşı farklı içerik veya verileri görüntüleyen sayfaları vardır. Anonim bir kullanıcı sitede oturum açmak için bir bağlantı görebilir, ancak kimliği doğrulanmış bir Kullanıcı, oturum kapatma bağlantısı ile birlikte, *Kullanıcı adı* gibi bir ileti görür. Başka bir örnek: bir öğe, bir açık eksiltme sitesinde görüntülenirken, bir Bidder veya öğeyi bir tane olup olmadığına bağlı olarak farklı bilgiler görürsünüz.

Bu tür sayfa düzeyi ayarlamalar bildirimli olarak veya programlı bir şekilde gerçekleştirilebilir. Kimliği doğrulanmış kullanıcıların anonim olarak farklı içeriğini göstermek için, sayfanıza bir [LoginView denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) sürükleyip, uygun Içeriği AnonymousTemplate ve LoggedInTemplate şablonlarına girmeniz yeterlidir. Alternatif olarak, geçerli isteğin kimlik doğrulamasının yapılıp yapılmayacağını, kullanıcının kim olduğunu ve ait oldukları rolleri (varsa) programlı bir şekilde belirleyebilirsiniz. Bu bilgileri, sayfadaki bir kılavuzda veya panelde sütunları göstermek veya gizlemek için kullanabilirsiniz.

Bu seri, yetkilendirmeye odaklanabilecek üç öğreticilerini içerir. ***Kullanıcı tabanlı yetkilendirme***, belirli kullanıcı hesapları için bir dizindeki sayfa veya sayfalara erişimin nasıl sınırlandıralınacağını inceler; ***Rol tabanlı yetkilendirme*** , rol düzeyinde yetkilendirme kuralları sağlamaya bakar; son olarak, ***Şu anda oturum açmış kullanıcı öğreticisini temel alan Içeriği görüntüleme*** , sayfayı ziyaret eden kullanıcıya göre belirli bir sayfanın içeriğini ve işlevselliğini değiştirmeyi araştırır. Daha fazlası için ASP. NET ' in yetkilendirme seçenekleri, bkz. [ASP.net Authorization](https://msdn.microsoft.com/library/wce3kxhd.aspx).

## <a name="user-accounts-and-roles"></a>Kullanıcı hesapları ve rolleri

ASP.net. NET Forms kimlik doğrulaması, kullanıcıların bir sitede oturum açmasını ve kimlik doğrulamalı durumunun sayfa ziyaretlerine hatırlanmasını sağlamak için bir altyapı sağlar. URL yetkilendirmesi, bir ASP.NET uygulamasındaki belirli dosyalara veya klasörlere erişimi sınırlandırmak için bir çerçeve sunar. Ancak özellik, Kullanıcı hesabı bilgilerini depolamak veya rolleri yönetmek için bir yol sağlar.

ASP.NET 2,0 ' den önce, geliştiriciler kendi Kullanıcı ve rol mağazalarını oluşturmaktan sorumludur. Bunlar aynı zamanda kullanıcı arabirimlerini tasarlamak ve oturum açma sayfası gibi önemli Kullanıcı hesabı ile ilgili sayfalar ve yeni bir hesap oluşturmak için, diğer kişiler arasında kod yazmak için de kanca üzerinde. ASP.NET ' de yerleşik bir kullanıcı hesabı çatısı olmadan, Kullanıcı hesaplarını uygulayan her geliştirici,, parolaları veya diğer hassas bilgileri Nasıl yaparım? gibi sorulara kendi tasarım kararlarına ulaşmak zorunda mıdır? parola uzunluğu ve gücüyle ilgili olarak hangi yönergeleri de getirmem gerekir?

Günümüzde, bir ASP.NET uygulamasında kullanıcı hesaplarının uygulanması, *Üyelik çerçevesi* ve yerleşik oturum açma Web denetimleri sayesinde daha basit bir uygulamadır. Üyelik çerçevesi, [System. Web. Security ad](https://msdn.microsoft.com/library/system.web.security.aspx) alanındaki, kullanıcı hesabıyla ilgili gerekli görevleri gerçekleştirmeye yönelik işlevselliği sağlayan bir dizi sınıftır. Üyelik çerçevesindeki anahtar sınıfı, şöyle Yöntemler içeren [Üyelik sınıfıdır](https://msdn.microsoft.com/library/system.web.security.membership.aspx):

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- ValidateUser

Üyelik çerçevesi, üyelik çerçevesinin API 'sini uygulamadan uygulamayı düzgün bir şekilde ayıran [sağlayıcı modelini](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)kullanır. Bu, geliştiricilerin ortak bir API kullanmasını sağlar, ancak bunları uygulamanın özel ihtiyaçlarını karşılayan bir uygulama kullanmaya güçler. Kısaca, üyelik sınıfı çerçevenin temel işlevlerini tanımlar (Yöntemler, Özellikler ve olaylar), ancak aslında hiçbir uygulama ayrıntısı sağlamaz. Bunun yerine, üyelik sınıfının yöntemleri yapılandırılmış sağlayıcıyı çağırır, bu da gerçek işi gerçekleştirir. Örneğin, üyelik sınıfının CreateUser yöntemi çağrıldığında, üyelik sınıfı Kullanıcı deposunun ayrıntılarını bilmez. Kullanıcıların bir veritabanında veya bir XML dosyasında ya da başka bir depoda tutulup tutulmakta olduğunu bilmez. Üyelik sınıfı, hangi sağlayıcının çağrının temsilciliğini belirlemek için Web uygulamasının yapılandırmasını inceler ve ilgili kullanıcı deposunda yeni kullanıcı hesabını gerçekten oluşturmaktan sorumlu olan sağlayıcı sınıfı sorumludur. Bu etkileşim şekil 3 ' te gösterilmiştir.

Microsoft .NET Framework iki üyelik sağlayıcısı sınıfı dağıtılır:

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -Active Directory ve Active Directory uygulama modu (adam) SUNUCULARıNDA üyelik API 'sini uygular.
- [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -üyelik API 'sini bir SQL Server veritabanında uygular.

Bu öğretici serisi özel olarak SqlMembershipProvider üzerinde odaklanır.

[![sağlayıcı modeli, farklı uygulamaların çerçeveye sorunsuzca takılmasına olanak sağlar](security-basics-and-asp-net-support-vb/_static/image4.png)](security-basics-and-asp-net-support-vb/_static/image3.png)

**Şekil 03**: sağlayıcı modeli, farklı uygulamaların çerçeveye sorunsuzca takılmasına olanak sağlar ([tam boyutlu görüntüyü görüntülemek için tıklatın](security-basics-and-asp-net-support-vb/_static/image5.png))

Sağlayıcı modelinin avantajı, alternatif uygulamaların Microsoft, üçüncü taraf satıcılar veya bireysel geliştiriciler tarafından geliştirilme ve üyelik çerçevesine sorunsuz bir şekilde takılabilsidir. Örneğin, Microsoft, [Microsoft Access veritabanları için bir üyelik sağlayıcısı](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)yayımlamıştır. Üyelik sağlayıcıları hakkında daha fazla bilgi için, üyelik sağlayıcıları, örnek özel sağlayıcılar, sağlayıcı modeline ait 100 sayfa üzerinde belge ve yerleşik üyelik sağlayıcılarının (yani ActiveDirectoryMembershipProvider ve SqlMembershipProvider) tam kaynak kodunu içeren [sağlayıcı araç seti](https://msdn.microsoft.com/asp.net/aa336558.aspx)' ne bakın.

ASP.NET 2,0, rol çerçevesini de kullanıma sunmuştur. Üyelik çerçevesi gibi, rol çerçevesi de sağlayıcı modeline göre oluşturulmuştur. API 'SI, [Roller sınıfı](https://msdn.microsoft.com/library/system.web.security.roles.aspx) aracılığıyla sunulur ve .NET Framework üç sağlayıcı sınıfıyla birlikte gelir:

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -ACTIVE DIRECTORY veya adam gibi bir Yetkilendirme Yöneticisi ilke deposundaki rol bilgilerini yönetir.
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -bir SQL Server veritabanında rolleri uygular.
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -ziyaretçi Windows grubuna göre rol bilgilerini ilişkilendirir. Bu yöntem genellikle Windows kimlik doğrulaması ile kullanılır.

Bu öğretici serisi özel olarak SqlRoleProvider 'a odaklanır.

Sağlayıcı modeli, tek bir iletme API 'SI (üyelik ve rol sınıfları) içerdiğinden, uygulama ayrıntıları konusunda endişelenmeden bu API 'nin etrafında işlevsellik oluşturmak mümkündür. bunlar sayfa tarafından seçilen sağlayıcılar tarafından işlenir Tasarımcı. Bu Birleşik API, Microsoft ve üçüncü taraf satıcıların üyelik ve rol çerçeveleri ile arabirim oluşturan Web denetimleri oluşturmasına izin verir. ASP.NET, ortak kullanıcı hesabı kullanıcı arabirimlerini uygulamak için bir dizi [oturum açma Web denetimi](https://msdn.microsoft.com/library/ms178329.aspx) ile birlikte sunulur. Örneğin, [oturum açma denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) bir kullanıcıdan kimlik bilgilerini ister, bunları doğrular ve ardından bunları Forms kimlik doğrulaması aracılığıyla günlüğe kaydeder. [LoginView denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) , anonim kullanıcılara karşı kimliği doğrulanmış kullanıcılara karşı farklı biçimlendirme veya kullanıcı rolüne göre farklı biçimlendirme görüntülemek için şablonlar sunar. [CreateUserWizard denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx) , yeni bir kullanıcı hesabı oluşturmak için adım adım bir kullanıcı arabirimi sağlar.

Altında, üyelik ve rol çerçeveleriyle etkileşim kuran çeşitli oturum açma denetimleri ele alınmaktadır. Birçok oturum açma denetimi, tek bir kod satırı yazmak zorunda kalmadan uygulanabilir. Bu denetimleri, işlevlerini genişletme ve özelleştirme teknikleri de dahil olmak üzere gelecekteki öğreticilerde daha ayrıntılı bir şekilde inceleyeceğiz.

## <a name="summary"></a>Özet

Kullanıcı hesaplarını destekleyen tüm Web uygulamaları, gibi benzer özellikler gerektirir; Örneğin, kullanıcıların oturum açabilme yeteneği ve sayfa ziyaretlerine ait günlük durumu hatırlanır; yeni ziyaretçilerin hesap oluşturmalarına yönelik bir Web sayfası; ve sayfa geliştiricisi 'nin hangi kaynak, veri ve işlevselliğin hangi kullanıcılar veya roller için kullanılabilir olduğunu belirtme özelliği. Kullanıcılara kimlik doğrulama ve yetkilendirme, Kullanıcı hesaplarını ve rolleri yönetme görevleri, Forms kimlik doğrulaması, URL yetkilendirmesi ve üyelik ve rol çerçeveleri sayesinde ASP.NET uygulamalarında kolayca gerçekleştirilir.

Sonraki birkaç öğreticilerde, bir adım adım izleyerek çalışan bir Web uygulamasını baştan sona oluşturarak bu yönleri inceleyeceğiz. Sonraki iki öğreticide, Forms kimlik doğrulamasını ayrıntılı olarak keşfedecektir. Forms kimlik doğrulaması iş akışını çalışırken, Forms kimlik doğrulama biletini dissect, güvenlik sorunlarını tartışacak ve ziyaretçilerin oturum açmasını ve oturumu açmasını sağlayan bir Web uygulaması oluştururken Forms kimlik doğrulaması sisteminin nasıl yapılandırılacağını görürsünüz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 2,0 üyelik, roller, form kimlik doğrulaması ve güvenlik kaynakları](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2,0 güvenlik yönergeleri](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET kimlik doğrulaması](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET yetkilendirmesi](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET oturum açma denetimlerine genel bakış](https://msdn.microsoft.com/library/ms178329.aspx)
- [ASP.NET 2.0 'ın üyeliğini, rollerini ve profilini İnceleme](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Nasıl yapılır: Üyelik ve rolleri kullanarak sitemin güvenliğini sağlama](https://asp.net/learn/videos/video-45.aspx) Video
- [Üyeliğe giriş](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN güvenlik Geliştirici Merkezi](https://msdn.microsoft.com/security/default.aspx)
- [Professional ASP.NET 2,0 güvenlik, üyelik ve rol yönetimi](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ısbn: 978-0-7645-9698-8)
- [Sağlayıcı araç seti](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni, bu öğretici serisinin birçok yararlı gözden geçiren tarafından incelendi. Bu öğreticide lider gözden geçirenler, Alicja Maziarz, John suru ve Teresa Murphy ' i içerir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](forms-authentication-configuration-and-advanced-topics-cs.md)
> [İleri](an-overview-of-forms-authentication-vb.md)
