---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-cs
title: Kullanıcı tabanlı yetkilendirme (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, sayfaların erişimini sınırlandırma ve çeşitli teknikler aracılığıyla sayfa düzeyindeki işlevleri kısıtlama bölümüne bakacağız.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 3c815a9e-2296-4b9b-b945-776d54989daa
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 059dbf42956268884dcfdade696491ac39e32da9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574342"
---
# <a name="user-based-authorization-c"></a>Kullanıcı Tabanlı Yetkilendirme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_cs.pdf)

> Bu öğreticide, sayfaların erişimini sınırlandırma ve çeşitli teknikler aracılığıyla sayfa düzeyindeki işlevleri kısıtlama bölümüne bakacağız.

## <a name="introduction"></a>Giriş

Kullanıcı hesapları sunan çoğu Web uygulaması, bazı ziyaretçilerin site içindeki belirli sayfalara erişmesini kısıtlamak için bu bölümü bir parçası olarak sunar. Çoğu çevrimiçi messageboard sitesinde, örneğin, anonim ve kimliği doğrulanmış tüm kullanıcılar, messagepanonun gönderilerini görüntüleyebilir, ancak yalnızca kimliği doğrulanmış kullanıcılar Web sayfasını ziyaret ederek yeni bir gönderi oluşturabilir. Ve yalnızca belirli bir Kullanıcı (veya belirli bir kullanıcı kümesi) için erişilebilir olan Yönetim sayfaları olabilir. Üstelik, sayfa düzeyi işlevsellik Kullanıcı tarafından Kullanıcı bazında farklılık gösterebilir. Bir gönderi listesi görüntülerken, kimliği doğrulanmış kullanıcılar her gönderiyi derecelendirirken bir arabirim gösterilir, ancak bu arabirim anonim ziyaretçilere uygun değildir.

ASP.NET, Kullanıcı tabanlı yetkilendirme kurallarını tanımlamanızı kolaylaştırır. Yalnızca `Web.config`bir bit biçimlendirme sayesinde belirli Web sayfaları veya tüm dizinler, yalnızca belirtilen kullanıcı alt kümesiyle erişilebilmesi için kilitlenir. Sayfa düzeyi işlevsellik, şu anda oturum açmış olan kullanıcıya programlı ve bildirim temelli yollarla açılabilir veya kapatılabilir.

Bu öğreticide, sayfaların erişimini sınırlandırma ve çeşitli teknikler aracılığıyla sayfa düzeyindeki işlevleri kısıtlama bölümüne bakacağız. Haydi başlayın!

## <a name="a-look-at-the-url-authorization-workflow"></a>URL yetkilendirmesi Iş akışına bakış

[*Form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-cs.md) bölümünde açıklandığı gibi, ASP.NET çalışma zamanı bir ASP.NET kaynağı için bir isteği işlediğinde, istek yaşam döngüsü boyunca birkaç olay oluşturur. *Http modülleri* , kodu istek yaşam döngüsünde belirli bir olaya yanıt olarak yürütülen yönetilen sınıflardır. ASP.NET, arka planda önemli görevleri gerçekleştiren bir dizi HTTP modülleriyle birlikte gelir.

Bu tür bir HTTP modülü [`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx). Önceki öğreticilerde anlatıldığı gibi, `FormsAuthenticationModule` birincil işlevi geçerli isteğin kimliğini belirlemektir. Bu, bir tanımlama bilgisinde bulunan ya da URL içine katıştırılmış olan Forms kimlik doğrulama bileti incelenerek gerçekleştirilir. Bu kimlik [`AuthenticateRequest` olay](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)sırasında gerçekleşir.

Başka bir önemli HTTP modülü, [`AuthorizeRequest` olayına](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx) yanıt olarak oluşturulan [`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)(`AuthenticateRequest` olayından sonra olur). `UrlAuthorizationModule`, geçerli kimliğin belirtilen sayfayı ziyaret etme yetkisine sahip olup olmadığını belirlemede `Web.config` yapılandırma işaretlemesini inceler. Bu işleme *URL yetkilendirmesi*denir.

Adım 1 ' de URL Yetkilendirme kuralları için sözdizimi inceleyeceğiz, ancak ilk olarak isteğin yetkili olup olmadığına bağlı olarak `UrlAuthorizationModule` bakalım. `UrlAuthorizationModule` isteğin yetkilendirildiğini belirlerse, hiçbir şey yapmaz ve istek yaşam döngüsü boyunca devam eder. Ancak, istek *yetkilendirilmezse* `UrlAuthorizationModule` yaşam döngüsünü durdurur ve `Response` nesnesine [http 401 Yetkisiz](http://www.checkupdown.com/status/E401.html) durumunu döndürmesini söyler. Form kimlik doğrulaması kullanılırken bu HTTP 401 durumu hiçbir zaman istemciye döndürülmez çünkü `FormsAuthenticationModule` bir HTTP 401 durumu algılarsa, oturum açma sayfasına bir [http 302 yeniden yönlendirmesine](http://www.checkupdown.com/status/E302.html) değiştirir.

Şekil 1 ' de, yetkisiz bir istek geldiğinde ASP.NET işlem hattının, `FormsAuthenticationModule`ve `UrlAuthorizationModule` iş akışı gösterilmektedir. Özellikle Şekil 1, anonim kullanıcılara erişimi engelleyen bir sayfa olan `ProtectedPage.aspx`için anonim bir ziyaretçi tarafından bir istek gösterir. Ziyaretçi anonim olduğundan, `UrlAuthorizationModule` isteği iptal eder ve HTTP 401 Yetkisiz durumunu döndürür. `FormsAuthenticationModule` sonra 401 durumunu 302 bir yeniden yönlendirme sayfasına dönüştürür. Kullanıcının kimliği, oturum açma sayfası aracılığıyla doğrulandıktan sonra, `ProtectedPage.aspx`yeniden yönlendirilir. Bu kez `FormsAuthenticationModule`, kimlik doğrulama biletini temel alarak kullanıcıyı tanımlar. Artık ziyaretçi kimliğinin doğrulandığına göre `UrlAuthorizationModule` sayfaya erişime izin verir.

[Forms kimlik doğrulaması ve URL yetkilendirmesi Iş akışını ![](user-based-authorization-cs/_static/image2.png)](user-based-authorization-cs/_static/image1.png)

**Şekil 1**: form kimlik doğrulaması ve URL yetkilendirmesi iş akışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image3.png))

Şekil 1 anonim bir ziyaretçi anonim kullanıcılar tarafından kullanılamayan bir kaynağa erişmeyi denediğinde gerçekleşen etkileşimi gösterir. Böyle bir durumda anonim ziyaretçi, oturum açma sayfasına, QueryString öğesinde belirtilen ziyaret etmeyi deneyen bir sayfayla yeniden yönlendirilir. Kullanıcı başarıyla oturum açtıktan sonra, başlangıçta görüntülemeye çalışan kaynağa otomatik olarak yeniden yönlendirilir.

Yetkisiz istek anonim bir kullanıcı tarafından yapıldığında, bu iş akışı basittir ve ziyaretçilerin ne olduğunu ve neden olduğunu anlamak kolaydır. Ancak, isteğin kimliği doğrulanmış bir kullanıcı tarafından yapılmış olsa bile, `FormsAuthenticationModule` *Tüm* yetkisiz kullanıcıları oturum açma sayfasına yönlendirdiğini aklınızda bulundurun. Kimliği doğrulanmış bir Kullanıcı, yetkisi olmayan bir sayfayı ziyaret etmeyi denerse bu, kafa karıştırıcı bir kullanıcı deneyimine neden olabilir.

Web sitemizin URL yetkilendirme kurallarının ASP.NET sayfa `OnlyTito.aspx`, yalnızca Tito ile erişilebilir olması gibi yapılandırıldığını düşünün. Şimdi, Sam 'ın siteyi ziyaret ettiği, oturum açtığı ve `OnlyTito.aspx`ziyaret etmeyi denediği hakkında düşünün. `UrlAuthorizationModule`, istek yaşam döngüsünü durdurur ve bir HTTP 401 Yetkisiz durumu döndürür ve bu `FormsAuthenticationModule`, Sam 'ı oturum açma sayfasına yönlendirir. Sam zaten oturum açtığından, bu nedenle oturum açma sayfasına geri gönderilmesini merak edebilir. Oturum açma kimlik bilgilerinin bir şekilde kaybolması veya geçersiz kimlik bilgileri girmiş olması neden olabilirler. Sam oturum açma sayfasından kimlik bilgilerini yeniden girerse, oturum açılır (yeniden) ve `OnlyTito.aspx`yeniden yönlendirilir. `UrlAuthorizationModule`, Sam 'nin bu sayfayı ziyaret edemeyeceğini algılar ve oturum açma sayfasına geri dönecektir.

Şekil 2 Bu kafa karıştırıcı iş akışını gösterir.

[![varsayılan Iş akışı kafa karıştırıcı bir döngüye neden olabilir](user-based-authorization-cs/_static/image5.png)](user-based-authorization-cs/_static/image4.png)

**Şekil 2**: varsayılan Iş akışı kafa karıştırıcı bir döngüye neden olabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](user-based-authorization-cs/_static/image6.png))

Şekil 2 ' de gösterilen iş akışı, en çok bilgisayar bilgili ziyaretçisinden bile hızlı bir şekilde hızla olabilir. 2\. adımda bu kafa karıştırıcı döngüsünü önlemenin yollarını inceleyeceğiz.

> [!NOTE]
> ASP.NET, geçerli kullanıcının belirli bir Web sayfasına erişip erişemeyeceğini anlamak için iki mekanizma kullanır: URL yetkilendirmesi ve dosya yetkilendirmesi. Dosya yetkilendirmesi, istenen dosya (ler) ACL 'Lerine danışarak yetkiyi belirleyen [`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)tarafından uygulanır. ACL 'Ler Windows hesapları için uygulanan izinler olduğundan, dosya yetkilendirmesi en yaygın olarak Windows kimlik doğrulama ile kullanılır. Form kimlik doğrulaması kullanılırken, siteyi ziyaret eden Kullanıcı ne olursa olsun, tüm işletim sistemi ve dosya sistemi düzeyi istekleri aynı Windows hesabı tarafından yürütülür. Bu öğretici serisi form kimlik doğrulamasına odaklandığından, dosya yetkilendirmesini ele vermeyecektir.

### <a name="the-scope-of-url-authorization"></a>URL yetkilendirmesi kapsamı

`UrlAuthorizationModule`, ASP.NET çalışma zamanının bir parçası olan yönetilen koddur. Microsoft 'un [Internet Information Services (IIS)](https://www.iis.net/) Web sunucusu sürüm 7 ' den önce, IIS 'nin http işlem hattı ve ASP.NET çalışma zamanının işlem hattı arasında ayrı bir engel vardı. Kısaca, IIS 6 ve önceki sürümlerde ASP. NET `UrlAuthorizationModule` yalnızca, IIS 'den ASP.NET çalışma zamanına bir istek atandığında yürütülür. Varsayılan olarak IIS, statik içeriğin kendisini, HTML sayfaları ve CSS, JavaScript ve resim dosyaları gibi işler ve yalnızca `.aspx`, `.asmx`veya `.ashx` uzantılı bir sayfa istendiğinde ASP.NET çalışma zamanına yönelik istekleri devre dışı bırakır.

Ancak IIS 7, tümleşik IIS ve ASP.NET işlem hatları sağlar. Birkaç yapılandırma ayarı sayesinde, IIS 7 ' yi *Tüm* istekler için `UrlAuthorizationModule` çağırmak üzere ayarlayabilirsiniz. Bu, URL yetkilendirme kurallarının herhangi bir türdeki dosyalar için tanımlanması anlamına gelir. Ayrıca, IIS 7 kendi URL yetkilendirme altyapısını içerir. ASP.NET Integration ve IIS 7 ' nin yerel URL yetkilendirme işlevselliği hakkında daha fazla bilgi için bkz. [ııS7 URL yetkilendirmesini anlama](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization). ASP.NET ve IIS 7 tümleştirmesinde daha ayrıntılı bir bakış için, shahram Khoskıı 'nin kitabı, *profesyonel IIS 7 ve ASP.NET tümleşik programlama* (ısbn: 978-0470152539) bir kopyasını seçin.

IIS 7 ' den önceki sürümlerde, bir Nutshell 'de, URL Yetkilendirme kuralları yalnızca ASP.NET çalışma zamanı tarafından işlenen kaynaklara uygulanır. Ancak IIS 7 ile IIS 'nin yerel URL yetkilendirme özelliğini kullanmak veya ASP 'yi bütünleştirmek mümkündür. NET ' in IIS 'in HTTP işlem hattına `UrlAuthorizationModule`, dolayısıyla bu işlevselliği tüm isteklere genişlettin.

> [!NOTE]
> ASP. adımda bazı hafif bazı önemli farklılıklar vardır. NET ' in `UrlAuthorizationModule` ve IIS 7 ' nin URL yetkilendirmesi özelliği yetkilendirme kurallarını işler. Bu öğretici, IIS 7 ' nin URL yetkilendirme işlevini veya `UrlAuthorizationModule`kıyasla yetkilendirme kurallarını ayrıştırmayla farklarını etkilemez. Bu konular hakkında daha fazla bilgi için MSDN 'de veya [www.iis.net](https://www.iis.net/)adresindeki IIS 7 belgelerine bakın.

## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>1\. Adım: URL yetkilendirme kurallarını`Web.config` tanımlama

`UrlAuthorizationModule`, uygulamanın yapılandırmasında tanımlanan URL yetkilendirme kurallarına dayalı olarak belirli bir kimlik için istenen kaynağa erişim izni verip vermemeyi belirler. Yetkilendirme kuralları, `<allow>` ve `<deny>` alt öğeleri biçimindeki [`<authorization>` öğesinde](https://msdn.microsoft.com/library/8d82143t.aspx) yazılır. Her `<allow>` ve `<deny>` alt öğesi şunları belirtebilir:

- Belirli bir Kullanıcı
- Virgülle ayrılmış kullanıcı listesi
- Soru işareti (?) ile belirtilen tüm anonim kullanıcılar
- Yıldız işaretiyle (\*) belirtilen tüm kullanıcılar

Aşağıdaki biçimlendirme, kullanıcıların Tito ve Scott 'a ve diğerlerini reddetmeye izin vermek için URL yetkilendirme kurallarının nasıl kullanılacağını göstermektedir:

[!code-xml[Main](user-based-authorization-cs/samples/sample1.xml)]

`<allow>` öğesi, kullanıcıların hangi kullanıcılara izin verileceğini tanımlar, ancak `<deny>` öğesi *Tüm* kullanıcıların reddedildiğini bildirir.

> [!NOTE]
> `<allow>` ve `<deny>` öğeleri, roller için yetkilendirme kuralları da belirtebilir. Daha sonraki bir öğreticide rol tabanlı yetkilendirmeyi inceleyeceğiz.

Aşağıdaki ayar Sam dışındaki herkese (anonim ziyaretçiler dahil) erişim izni verir:

[!code-xml[Main](user-based-authorization-cs/samples/sample2.xml)]

Yalnızca kimliği doğrulanmış kullanıcılara izin vermek için, tüm anonim kullanıcılara erişimi engelleyen aşağıdaki yapılandırmayı kullanın:

[!code-xml[Main](user-based-authorization-cs/samples/sample3.xml)]

Yetkilendirme kuralları, `Web.config` `<system.web>` öğesi içinde tanımlanır ve Web uygulamasındaki tüm ASP.NET kaynaklarına uygulanır. Oftentimes, bir uygulamanın farklı bölümler için farklı yetkilendirme kuralları vardır. Örneğin, bir eCommerce sitesinde, tüm ziyaretçiler ürünleri kullanabilir, ürün incelemeleri görebilir, katalogda arama yapın ve bu şekilde devam edebilir. Ancak, yalnızca kimliği doğrulanmış kullanıcılar, tek bir sevkiyat geçmişini yönetmek için kullanıma alma veya sayfalara ulaşabilirler. Ayrıca, site yöneticileri gibi yalnızca seçim yapan kullanıcılar tarafından erişilebilen bir bölümü olabilir.

ASP.NET, sitedeki farklı dosya ve klasörler için farklı yetkilendirme kuralları tanımlamanızı kolaylaştırır. Kök klasörün `Web.config` dosyasında belirtilen yetkilendirme kuralları, sitedeki tüm ASP.NET kaynakları için geçerlidir. Ancak, bu varsayılan yetkilendirme ayarları, bir `Web.config` `<authorization>` bölümü ekleyerek belirli bir klasör için geçersiz kılınabilir.

Yalnızca kimliği doğrulanmış kullanıcıların `Membership` klasöründeki ASP.NET sayfalarını ziyaret edebilmesi için Web sitemizi güncelleştirelim. Bunu gerçekleştirmek için, `Membership` klasöre bir `Web.config` dosyası eklemesi ve yetkilendirme ayarlarını anonim kullanıcıları reddedecek şekilde ayarlaması gerekir. Çözüm Gezgini `Membership` klasöre sağ tıklayın, bağlam menüsünden Yeni öğe Ekle menüsünü seçin ve `Web.config`adlı yeni bir Web yapılandırma dosyası ekleyin.

[Üyelik klasörüne Web. config dosyası eklemek ![](user-based-authorization-cs/_static/image8.png)](user-based-authorization-cs/_static/image7.png)

**Şekil 3**: `Membership` klasörüne bir `Web.config` dosyası ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image9.png))

Bu noktada, projeniz iki `Web.config` dosya içermelidir: biri kök dizinde ve diğeri `Membership` klasöründedir.

[![uygulamanızın Şu anda Iki Web. config dosyası Içermesi gerekir](user-based-authorization-cs/_static/image11.png)](user-based-authorization-cs/_static/image10.png)

**Şekil 4**: uygulamanız artık Iki `Web.config` dosya içermeli ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image12.png))

`Membership` klasördeki yapılandırma dosyasını, anonim kullanıcılara erişimi yasakladığından güncelleştirin.

[!code-xml[Main](user-based-authorization-cs/samples/sample4.xml)]

İşte bu kadar kolay!

Bu değişikliği test etmek için tarayıcıda giriş sayfasını ziyaret edin ve oturum açtığınızdan emin olun. Bir ASP.NET uygulamasının varsayılan davranışı tüm ziyaretçilere izin vermedikten ve kök dizinin `Web.config` dosyasında herhangi bir yetkilendirme değişikliği yapamadığımızdan, kök dizindeki dosyaları anonim bir ziyaretçi olarak ziyaret edebiliyoruz.

Sol sütunda bulunan Kullanıcı hesapları oluşturma bağlantısına tıklayın. Bu işlem sizi `~/Membership/CreatingUserAccounts.aspx`götürür. `Membership` klasöründeki `Web.config` dosyası anonim erişimi engelleyecek yetkilendirme kurallarını tanımladığından, `UrlAuthorizationModule` isteği iptal eder ve HTTP 401 Yetkisiz durumunu döndürür. `FormsAuthenticationModule` bunu, oturum açma sayfasına gönderdiğiniz bir 302 yeniden yönlendirme durumunda değiştirir. Erişmeye çalıştığınız sayfanın (`CreatingUserAccounts.aspx`) `ReturnUrl` QueryString parametresi aracılığıyla oturum açma sayfasına geçtiğini unutmayın.

[URL Yetkilendirme kuralları anonim erişimi yasakladığından ![, oturum açma sayfasına yönlendirilirsiniz](user-based-authorization-cs/_static/image14.png)](user-based-authorization-cs/_static/image13.png)

**Şekil 5**: URL Yetkilendirme kuralları anonim erişimi yasakladığından, oturum açma sayfasına yönlendirilirsiniz ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image15.png))

Başarıyla oturum açtıktan sonra `CreatingUserAccounts.aspx` sayfasına yönlendirilirsiniz. Bu kez `UrlAuthorizationModule` artık anonim olmadığınızdan sayfaya erişime izin verir.

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>URL Yetkilendirme kuralları belirli bir konuma uygulanıyor

`Web.config` `<system.web>` bölümünde tanımlanan yetkilendirme ayarları, bu dizin ve alt dizinlerindeki tüm ASP.NET kaynakları için geçerlidir (başka bir `Web.config` dosyası tarafından aksi belirtilmedikçe). Bazı durumlarda, belirli bir dizindeki tüm ASP.NET kaynaklarının belirli bir veya iki sayfa hariç belirli bir yetkilendirme yapılandırmasına sahip olmasını isteyebilirsiniz. Bu, `Web.config``<location>` öğesi eklenerek, yetkilendirme kuralları farklı olan dosyaya işaret ederek ve içindeki benzersiz yetkilendirme kurallarını tanımlayarak elde edilebilir.

Belirli bir kaynak için yapılandırma ayarlarını geçersiz kılmak üzere `<location>` öğesini kullanmayı görmek için, yetkilendirme ayarlarını yalnızca Tito tarafından `CreatingUserAccounts.aspx`ziyaret edilebilir olacak şekilde özelleştirelim. Bunu gerçekleştirmek için, `Membership` klasörünün `Web.config` dosyasına bir `<location>` öğesi ekleyin ve biçimlendirmesini aşağıdaki gibi görünecek şekilde güncelleştirin:

[!code-xml[Main](user-based-authorization-cs/samples/sample5.xml)]

`<system.web>` `<authorization>` öğesi, `Membership` klasöründe ve alt klasörlerinde ASP.NET kaynakları için varsayılan URL yetkilendirme kurallarını tanımlar. `<location>` öğesi belirli bir kaynak için bu kuralları geçersiz kılmamızı sağlar. Yukarıdaki İşaretlemede `<location>` öğesi `CreatingUserAccounts.aspx` sayfasına başvurur ve Tito 'ya izin vermek, ancak diğer herkesin erişimini engellemek gibi yetkilendirme kurallarını belirtir.

Bu yetkilendirme değişikliğini test etmek için, Web sitesini anonim kullanıcı olarak ziyaret ederek başlayın. `UserBasedAuthorization.aspx`gibi `Membership` klasördeki herhangi bir sayfayı ziyaret etmeye çalışırsanız `UrlAuthorizationModule` isteği reddeder ve oturum açma sayfasına yönlendirilirsiniz. Olarak oturum açtıktan sonra Scott, `CreatingUserAccounts.aspx`*hariç* `Membership` klasördeki herhangi bir sayfayı ziyaret edebilirsiniz. Herkes oturum açma sayfasına geri yönlendirilmeye izin vermek için, bir kişi olarak oturum açmış `CreatingUserAccounts.aspx` ziyaret edilmeye çalışıldı.

> [!NOTE]
> `<location>` öğesi yapılandırmanın `<system.web>` öğesinin dışında görünmelidir. Yetkilendirme ayarlarını geçersiz kılmak istediğiniz her kaynak için ayrı bir `<location>` öğesi kullanmanız gerekir.

### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>`UrlAuthorizationModule`erişim vermek veya reddetmek için yetkilendirme kurallarını nasıl kullandığını gösteren bir bakış

`UrlAuthorizationModule`, URL yetkilendirme kurallarını her seferinde bir kez analiz ederek belirli bir URL için belirli bir kimliğin yetkilendirilip yetkilendirilmeyeceğini belirler. Eşleşme bulunduğunda, eşleşme bir `<allow>` veya `<deny>` öğesinde bulunmuna bağlı olarak, Kullanıcı erişim izni verilir veya reddedilir. <strong>Hiçbir eşleşme bulunmazsa, kullanıcıya erişim verilir.</strong> Sonuç olarak, erişimi kısıtlamak isterseniz, URL yetkilendirme yapılandırmasındaki son öğe olarak bir `<deny>` öğesi kullanmanız zorunludur. <strong>Bir</strong> <strong>`<deny>`</strong> <strong>öğesini atlarsanız, tüm kullanıcılara erişim izni verilir.</strong>

`UrlAuthorizationModule` tarafından yetkilendirmeyi öğrenmek için kullanılan işlemi daha iyi anlamak için, bu adımda daha önce bakdığımız örnek URL yetkilendirme kurallarını göz önünde bulundurun. İlk kural, Tito ve Scott 'a erişim sağlayan bir `<allow>` öğesidir. İkinci kurallar herkese erişimi engelleyen bir `<deny>` öğesidir. Anonim bir kullanıcı ziyaret ederse `UrlAuthorizationModule`, Scott ya da Tito anonimdir. Yanıt, açıkça Hayır, bu yüzden ikinci kurala devam eder. Herkes bir herkes kümesinde mi anonimdir? Buradaki yanıt Evet olduğundan, `<deny>` kuralı devreye konur ve ziyaretçi oturum açma sayfasına yönlendirilir. Benzer şekilde, Jisun ziyaret etirse `UrlAuthorizationModule`, ister Jisun Scott ya da Tito? BT olmadığından `UrlAuthorizationModule` ikinci soruya devam ediyor, her biri bir herkes kümesi değil mi? Yani, çok, erişimi engellenmiş. Son olarak, Eğer ziyaret edirse, `UrlAuthorizationModule` ortaya etkilenen ilk soru, bu nedenle erişim izni verilir.

`UrlAuthorizationModule`, kimlik doğrulama kurallarını yukarıdan aşağı doğru işlediği ve herhangi bir eşleşmede durduğundan, daha belirli kuralların daha az spesifik olanlardan önce gelmesi önemlidir. Diğer bir deyişle, Jisun ve anonim kullanıcıları teklif eden, ancak diğer tüm kimliği doğrulanmış tüm kullanıcılara izin veren yetkilendirme kurallarını tanımlamak için en belirli kuralla başlayacaksınız; Jisun 'yi etkileyen ve daha az özel kurallara devam eden kimliği doğrulanmış kullanıcılar, ancak tüm anonim kullanıcılar reddediliyor. Aşağıdaki URL Yetkilendirme kuralları, önce Jisun ' ı reddettikten sonra anonim kullanıcıları reddettikten sonra bu ilkeyi uygular. Bu `<deny>` deyimlerinin hiçbiri eşleşmediğinden, Jisun dışında kimliği doğrulanmış bir kullanıcıya erişim izni verilir.

[!code-xml[Main](user-based-authorization-cs/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>2\. Adım: yetkisiz, kimliği doğrulanmış kullanıcılar için Iş akışını düzeltme

Bu öğreticide daha önce açıklanan URL yetkilendirmesi Iş akışı bölümünde, yetkisiz bir istek transpires, `UrlAuthorizationModule` isteği durdurur ve HTTP 401 Yetkisiz durumunu döndürür. Bu 401 durumu, Kullanıcı oturum açma sayfasına gönderen bir 302 yeniden yönlendirme durumuna `FormsAuthenticationModule` tarafından değiştirilir. Bu iş akışı, kullanıcının kimliği doğrulansa bile, tüm yetkisiz istekler üzerinde gerçekleşir.

Kimliği doğrulanmış bir kullanıcının oturum açma sayfasına döndürülmesi, sistemde zaten oturum açtığından bu yana şaşırmaları olasıdır. Çok az iş sayesinde bu iş akışını, kısıtlı bir sayfaya erişmeye çalıştıolduklarını açıklayan, kimliği doğrulanmış kullanıcıları bir sayfaya yönlendirerek iyileştirebiliriz.

Web uygulamasının `UnauthorizedAccess.aspx`adlı kök klasörde yeni bir ASP.NET sayfası oluşturarak başlayın. Bu sayfayı `Site.master` ana sayfasıyla ilişkilendirmeyi unutmayın. Bu sayfayı oluşturduktan sonra ana sayfanın varsayılan içeriğinin görüntülenmesi için `LoginContent` ContentPlaceHolder öğesine başvuran Içerik denetimini kaldırın. Ardından, durumu açıklayan bir ileti ekleyin, yani kullanıcı korumalı bir kaynağa erişmeyi denedi. Böyle bir ileti eklendikten sonra, `UnauthorizedAccess.aspx` sayfanın bildirim temelli işaretleme aşağıdakine benzer şekilde görünmelidir:

[!code-aspx[Main](user-based-authorization-cs/samples/sample7.aspx)]

Artık, yetkisiz bir istek kimliği doğrulanmış bir kullanıcı tarafından, oturum açma sayfası yerine `UnauthorizedAccess.aspx` sayfasına gönderiliyorsa, iş akışını değiştirmemiz gerekiyor. Yetkisiz istekleri oturum açma sayfasına yönlendiren mantık `FormsAuthenticationModule` sınıfının özel bir yöntemi içine eklenir, bu nedenle bu davranışı özelleştiremezsiniz. Ancak, bunu yapabiliriz, oturum açma sayfasına, gerekirse kullanıcıyı `UnauthorizedAccess.aspx`yeniden yönlendiren kendi mantığımızı ekliyoruz.

`FormsAuthenticationModule` yetkisiz bir ziyaretçiye oturum açma sayfasına yönlendirirse, istenen, yetkisiz URL 'yi QueryString öğesine `ReturnUrl`adı ile ekler. Örneğin, yetkisiz bir Kullanıcı `OnlyTito.aspx`ziyaret etmeyi denediğinde `FormsAuthenticationModule` `Login.aspx?ReturnUrl=OnlyTito.aspx`yeniden yönlendirir. Bu nedenle, oturum açma sayfasına `ReturnUrl` parametresi içeren bir QueryString ile kimliği doğrulanmış bir kullanıcı tarafından ulaşılırsa, bu kimliği doğrulanmamış kullanıcının görüntüleme yetkisine sahip olmayan bir sayfayı ziyaret etmeyi denediğini biliyoruz. Böyle bir durumda, `UnauthorizedAccess.aspx`' a yönlendirmek istiyoruz.

Bunu gerçekleştirmek için, oturum açma sayfasının `Page_Load` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample8.cs)]

Yukarıdaki kod kimliği doğrulanmış, yetkisiz kullanıcıları `UnauthorizedAccess.aspx` sayfasına yönlendirir. Bu mantığı çalışırken görmek için, siteyi anonim bir ziyaretçi olarak ziyaret edin ve sol sütundaki Kullanıcı hesapları oluşturma bağlantısına tıklayın. Bu işlem sizi, 1. adımda yalnızca Tito 'a erişime izin verecek şekilde yapılandırdığımız `~/Membership/CreatingUserAccounts.aspx` sayfasına götürür. Anonim kullanıcılar yasaklanmış olduğundan `FormsAuthenticationModule`, bize oturum açma sayfasına yeniden yönlendirir.

Bu noktada anonim olarak `Request.IsAuthenticated` `false` `UnauthorizedAccess.aspx`geri yönlendirilmedik. Bunun yerine, oturum açma sayfası görüntülenir. Deneme sürümünden farklı bir kullanıcı olarak oturum açın. Uygun kimlik bilgilerini girdikten sonra, oturum açma sayfası bize yeniden `~/Membership/CreatingUserAccounts.aspx`yönlendirir. Ancak, bu sayfaya yalnızca Tito tarafından erişilebileceğinden, görüntüleme yetkisi veriyoruz ve oturum açma sayfasına hemen geri döndürülüyor. Ancak, `Request.IsAuthenticated` `true` döndürür (ve `ReturnUrl` QueryString parametresi bulunur), bu nedenle `UnauthorizedAccess.aspx` sayfasına yönlendirilirsiniz.

[![kimliği doğrulanmış, yetkisiz kullanıcılar UnauthorizedAccess. aspx 'e yeniden yönlendirildi](user-based-authorization-cs/_static/image17.png)](user-based-authorization-cs/_static/image16.png)

**Şekil 6**: kimliği doğrulanmış, yetkisiz kullanıcılar `UnauthorizedAccess.aspx` yönlendirilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](user-based-authorization-cs/_static/image18.png))

Bu özelleştirilmiş iş akışı, Şekil 2 ' de gösterilen döngüyü kısa bir süre sonra çok daha kolay ve kolay bir şekilde bir kullanıcı deneyimi sunar.

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>3\. Adım: Şu anda oturum açmış olan kullanıcıya göre Işlevselliği sınırlandırma

URL yetkilendirmesi, kaba yetkilendirme kuralları belirtmeyi kolaylaştırır. Adım 1 ' de gördüğünüz gibi, URL yetkilendirmesi ile, hangi kimliklerin izin verileceğini ve hangilerinin belirli bir sayfayı veya bir klasördeki tüm sayfaları görüntülemesi reddedildiğini succinctly olabilir. Ancak, bazı senaryolarda, tüm kullanıcıların bir sayfayı ziyaret etmesini sağlamak isteyebilir, ancak sayfayı ziyaret eden kullanıcıya göre sayfanın işlevlerini sınırlayabilirsiniz.

Kimliği doğrulanmış ziyaretçilerin ürünlerini gözden geçirmesine izin veren bir eCommerce Web sitesinin durumunu göz önünde bulundurun. Anonim Kullanıcı bir ürünün sayfasını ziyaret ettiğinde yalnızca ürün bilgilerini görürler ve bir gözden geçirme bırakma fırsatı verilmeyebilir. Ancak, aynı sayfayı ziyaret eden kimliği doğrulanmış bir Kullanıcı İnceleme arabirimini görür. Kimliği doğrulanmış kullanıcı henüz bu ürünü gözden geçirmediyse, arabirim bunları bir gözden geçirme göndermelerini sağlar; Aksi takdirde, önceden gönderilen gözden geçirmeyi gösterir. Bu senaryoyu daha ayrıntılı bir şekilde gerçekleştirmek için, ürün sayfasında, e-ticaret şirketi için çalışan kullanıcılar için ek bilgiler gösterilebilir ve genişletilmiş özellikler sunabilir. Örneğin, ürün sayfası envanterdeki stoku listeleyebilir ve bir çalışan tarafından ziyaret edildiğinde ürünün fiyatını ve açıklamasını düzenleme seçeneklerini içerir.

Bu tür ince yetkilendirme kuralları, bildirimli veya programlı olarak (ya da ikisinin bir birleşimi aracılığıyla) uygulanabilir. Sonraki bölümde, LoginView denetimi aracılığıyla ince bir yetkilendirmeyi nasıl uygulayacağınızı öğreneceksiniz. Bundan sonra, programlama tekniklerini keşfedecektir. Ancak, ince gretik yetkilendirme kuralları uygulamaya bakmadan önce, işlevselliği ziyaret eden kullanıcıya bağlı olan bir sayfa oluşturmanız gerekir.

GridView içindeki belirli bir dizindeki dosyaları listeleyen bir sayfa oluşturalım. Her bir dosyanın adını, boyutunu ve diğer bilgilerini listelemesi ile GridView, LinkButtons 'ın iki sütununu içerir: One başlıklı görünüm ve bir DELETE. Bağlantı görüntüle düğmesine tıklandıysanız, seçili dosyanın içeriği görüntülenir; Bağlantı Sil düğmesine tıklandıysanız dosya silinir. İlk olarak bu sayfayı, görüntüleme ve silme işlevinin tüm kullanıcılar tarafından kullanılabilmesini sağlayan şekilde oluşturalım. LoginView denetimini kullanarak ve Işlev bölümlerini programlı olarak sınırlayarak, sayfayı ziyaret eden kullanıcıya göre bu özelliklerin nasıl etkinleştirileceğini veya devre dışı bırakılacağını öğreneceğiz.

> [!NOTE]
> Derlemek üzere yaptığımız ASP.NET sayfası, bir dosya listesini göstermek için bir GridView denetimi kullanır. Bu öğretici serisi form kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rollere odaklandığından, GridView denetiminin iç çalışmalarını ele almak çok fazla zaman harcamayı istemiyorum. Bu öğretici, bu sayfayı ayarlamaya yönelik belirli adım adım yönergeler sağlarken, belirli seçimlerin neden yapıldığına ilişkin ayrıntıları veya işlenen çıktıda belirli özellikler hangi etkilerle olduğunu anlamaz. GridView denetimini kapsamlı bir şekilde incelemek için ASP.NET 2,0 öğretici serisinde *[verilerle çalışmama](../../data-access/index.md)* bakın.

`UserBasedAuthorization.aspx` dosyasını `Membership` klasöründe açıp `FilesGrid`adlı sayfaya bir GridView denetimi ekleyerek başlayın. GridView 'un akıllı etiketinde alanları Düzenle bağlantısına tıklayarak alanları başlatın iletişim kutusunu seçin. Buradan sol alt köşedeki alanları otomatik oluştur onay kutusunun işaretini kaldırın. Ardından, sol üst köşeden bir SELECT düğmesi, Delete düğmesi ve iki BoundFields ekleyin (Select ve DELETE düğmeleri CommandField türü altında bulunabilir). Select düğmesinin `SelectText` özelliğini View ve ilk BoundField 'ın `HeaderText` ve `DataField` özelliklerini olacak şekilde ayarlayın. İkinci BoundField 'ın `HeaderText` özelliğini bayt cinsinden, `DataField` özelliğinin uzunluğu, `DataFormatString` özelliğini {0:N0} ve `HtmlEncode` özelliğini false olarak ayarlayın.

GridView 'un sütunlarını yapılandırdıktan sonra, alanlar iletişim kutusunu kapatmak için Tamam ' ı tıklatın. Özellikler penceresi, GridView 'un `DataKeyNames` özelliğini `FullName`olarak ayarlayın. Bu noktada, GridView 'un bildirim temelli işaretleme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](user-based-authorization-cs/samples/sample9.aspx)]

GridView 'un biçimlendirmesi oluşturulduktan sonra, belirli bir dizindeki dosyaları alacak ve GridView 'a bağlayacağınız kodu yazmaya hazırız. Aşağıdaki kodu sayfanın `Page_Load` olay işleyicisine ekleyin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample10.cs)]

Yukarıdaki kod, uygulamanın kök klasöründeki dosyaların listesini almak için [`DirectoryInfo` sınıfını](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx) kullanır. [`GetFiles()` yöntemi](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx) , dizindeki tüm dosyaları bir [`FileInfo` nesneleri](https://msdn.microsoft.com/library/system.io.fileinfo.aspx)dizisi olarak döndürür ve daha sonra GridView 'a bağlanır. `FileInfo` nesnesi, diğerleri arasında `Name`, `Length`ve `IsReadOnly`gibi bir özellikler sınıfmıştır. Bildirim temelli işaretlerinden görebileceğiniz gibi, GridView yalnızca `Name` ve `Length` özelliklerini görüntüler.

> [!NOTE]
> `DirectoryInfo` ve `FileInfo` sınıfları [`System.IO` ad alanında](https://msdn.microsoft.com/library/system.io.aspx)bulunur. Bu nedenle, bu sınıf adlarını ad alanı adlarıyla önceden hissetmek ya da ad alanını sınıf dosyasına (`using System.IO`aracılığıyla) içeri aktarmış olmanız gerekir.

Bir tarayıcı aracılığıyla bu sayfayı ziyaret etmek için bir dakikanızı ayırın. Uygulamanın kök dizininde bulunan dosyaların listesini görüntüler. Görünüm veya silme bağlantı düğmelerinden herhangi birine tıklamak geri göndermeye neden olur, ancak henüz gerekli olay işleyicilerini oluşturduğumuz için hiçbir işlem gerçekleşmez.

[GridView ![Web uygulamasının kök dizinindeki dosyaları listeler](user-based-authorization-cs/_static/image20.png)](user-based-authorization-cs/_static/image19.png)

**Şekil 7**: GridView, Web uygulamasının kök dizinindeki dosyaları listeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image21.png))

Seçili dosyanın içeriğini göstermek için bir yol gerekir. Visual Studio 'ya dönün ve GridView 'un üzerinde `FileContents` adlı bir metin kutusu ekleyin. `TextMode` özelliğini `MultiLine` ve `Columns` ve `Rows` özellikleri sırasıyla %95 ve 10 olarak ayarlayın.

[!code-aspx[Main](user-based-authorization-cs/samples/sample11.aspx)]

Sonra, GridView 'un [`SelectedIndexChanged` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx) için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample12.cs)]

Bu kod, seçili dosyanın tam dosya adını öğrenmek için GridView 'un `SelectedValue` özelliğini kullanır. Dahili olarak, `SelectedValue`almak için `DataKeys` koleksiyonuna başvurulur, bu nedenle bu adımda daha önce anlatıldığı gibi GridView 'un `DataKeyNames` özelliğini ad olarak ayarlamanız zorunludur. [`File` sınıfı](https://msdn.microsoft.com/library/system.io.file.aspx) seçili dosyanın içeriğini bir dizeye okumak için kullanılır. Bu, daha sonra `FileContents` TextBox 'ın `Text` özelliğine atanır ve bu sayede seçili dosyanın içeriğini sayfada görüntüler.

[![seçili dosyanın Içeriği metin kutusunda görüntülenir](user-based-authorization-cs/_static/image23.png)](user-based-authorization-cs/_static/image22.png)

**Şekil 8**: Seçili dosyanın içeriği metin kutusunda görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image24.png))

> [!NOTE]
> HTML işaretlemesi içeren bir dosyanın içeriğini görüntüleyip bir dosyayı görüntülemeyi veya silmeyi denerseniz, bir `HttpRequestValidationException` hatası alırsınız. Bunun nedeni, geri göndermede metin kutusu içeriğinin Web sunucusuna geri gönderilmesi nedeniyle oluşur. Varsayılan olarak, ASP.NET, olası tehlikeli geri gönderme içerikleri (HTML biçimlendirme gibi) algılandığında `HttpRequestValidationException` bir hata oluşturur. Bu hatanın oluşmasını devre dışı bırakmak için `@Page` yönergesine `ValidateRequest="false"` ekleyerek sayfanın istek doğrulamasını kapatın. İstek doğrulamanın avantajları ve bunu devre dışı bırakırken gerçekleştirmeniz gereken önlemler hakkında daha fazla bilgi için, [Istek doğrulama-betiği engellemeyi](https://asp.net/learn/whitepapers/request-validation/)okuyun.

Son olarak, GridView 'un [`RowDeleting` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)için aşağıdaki kodla bir olay işleyicisi ekleyin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample13.cs)]

Kod, dosyanın gerçekten *silinmeksizin* `FileContents` metin kutusunda silinecek dosyanın tam adını görüntüler.

[Sil düğmesine tıklamak ![dosyayı gerçekten silmez](user-based-authorization-cs/_static/image26.png)](user-based-authorization-cs/_static/image25.png)

**Şekil 9**: Sil düğmesine tıklamak dosyayı gerçekten silmez ([tam boyutlu görüntüyü görüntülemek için tıklatın](user-based-authorization-cs/_static/image27.png))

1\. adımda, anonim kullanıcıların `Membership` klasöründeki sayfaları görüntülemesini engellemek için URL yetkilendirme kurallarını yapılandırdık. İnce bir kimlik doğrulaması daha iyi bir şekilde sergilebilmek için anonim kullanıcıların `UserBasedAuthorization.aspx` sayfasını ziyaret edebilmesine izin verlim, ancak sınırlı işlevsellikle. Bu sayfayı tüm kullanıcılar tarafından erişilecek şekilde açmak için, aşağıdaki `<location>` öğesini `Membership` klasöründeki `Web.config` dosyasına ekleyin:

[!code-xml[Main](user-based-authorization-cs/samples/sample14.xml)]

Bu `<location>` öğesi eklendikten sonra, site oturumunu kapatarak yeni URL yetkilendirme kurallarını test edin. Anonim bir kullanıcı olarak `UserBasedAuthorization.aspx` sayfasını ziyaret etmeniz gerekir.

Şu anda, kimliği doğrulanmış veya anonim kullanıcı `UserBasedAuthorization.aspx` sayfasını ziyaret edebilir ve dosyaları görüntüleyebilir veya silebilir. Yalnızca kimliği doğrulanmış kullanıcıların bir dosyanın içeriğini görüntüleyebilmesini ve bir dosyayı silebilmesini sağlamak için bunu yapalim. Bu tür ince yetkilendirme kuralları bildirimli, programlı bir şekilde veya her iki yöntemin bir birleşimi aracılığıyla uygulanabilir. Bir dosyanın içeriğini kimlerin görebileceğini sınırlamak için bildirim temelli yaklaşımı kullanalım; bir dosyayı kimin silebilen ile sınırlamak için programlama yaklaşımını kullanacağız.

### <a name="using-the-loginview-control"></a>LoginView denetimini kullanma

Geçmiş öğreticilerde gördüğünüze göre, LoginView denetimi, kimliği doğrulanmış ve anonim kullanıcılara yönelik farklı arabirimleri görüntülemek için yararlıdır ve anonim kullanıcılar tarafından erişilemeyen işlevselliği gizlemek için kolay bir yol sunar. Anonim kullanıcılar dosyaları görüntüleyemez veya silemezduğundan, sayfa kimliği doğrulanmış bir kullanıcı tarafından ziyaret edildiğinde yalnızca `FileContents` metin kutusunu göstermemiz gerekir. Bunu başarmak için, sayfaya bir LoginView denetimi ekleyin, `LoginViewForFileContentsTextBox`adlandırın ve `FileContents` metin kutusunun bildirime dayalı işaretlemesini LoginView denetiminin `LoggedInTemplate`taşıyın.

[!code-aspx[Main](user-based-authorization-cs/samples/sample15.aspx)]

LoginView şablonlarındaki Web denetimlerine artık arka plan kod sınıfından doğrudan erişilebilir. Örneğin, `FilesGrid` GridView 'un `SelectedIndexChanged` ve `RowDeleting` olay işleyicileri Şu anda `FileContents` TextBox denetimine şu şekilde başvurabilir:

[!code-csharp[Main](user-based-authorization-cs/samples/sample16.cs)]

Ancak, bu kod artık geçerli değildir. `FileContents` metin kutusunu `LoggedInTemplate` içine taşıyarak TextBox 'a doğrudan erişilemez. Bunun yerine, denetime programlı olarak başvurmak için `FindControl("controlId")` metodunu kullandık. `FilesGrid` olay işleyicilerini metin kutusuna başvuracak şekilde güncelleştirin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample17.cs)]

TextBox 'ı LoginView 'ın `LoggedInTemplate` taşıdıktan ve sayfanın kodunu, `FindControl("controlId")` modelini kullanarak TextBox 'a başvuracak şekilde güncelleştirdikten sonra, sayfayı anonim kullanıcı olarak ziyaret edin. Şekil 10 ' da gösterildiği gibi, `FileContents` metin kutusu görüntülenmez. Bununla birlikte, View LinkButton hala görüntülenir.

[![LoginView denetimi yalnızca kimliği doğrulanmış kullanıcılar için dosya Içeriği metin kutusunu Işler](user-based-authorization-cs/_static/image29.png)](user-based-authorization-cs/_static/image28.png)

**Şekil 10**: LoginView denetimi yalnızca kimliği doğrulanmış kullanıcılar Için `FileContents` metin kutusunu işler ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image30.png))

Anonim kullanıcılar için Görünüm düğmesini gizlemenin bir yolu, GridView alanını bir TemplateField 'a dönüştürmesidir. Bu, View LinkButton için bildirim temelli biçimlendirmeyi içeren bir şablon oluşturur. Daha sonra TemplateField 'a bir LoginView denetimi ekleyebilir ve LinkButton öğesini LoginView 'ın `LoggedInTemplate`içine yerleştirebilir ve böylece, anonim ziyaretçilerin Görünüm düğmesini gizliyoruz. Bunu gerçekleştirmek için GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayarak alanlar iletişim kutusunu başlatın. Sonra sol alt köşedeki listeden Seç düğmesini seçin ve ardından bu alanı bir TemplateField öğesine Dönüştür bağlantısına tıklayın. Bunun yapılması, alanın bildirim temelli işaretlemesini şuradan değiştirecek:

[!code-aspx[Main](user-based-authorization-cs/samples/sample18.aspx)]

 Hedef: 

[!code-aspx[Main](user-based-authorization-cs/samples/sample19.aspx)]

Bu noktada, TemplateField 'a bir LoginView ekleyebiliriz. Aşağıdaki biçimlendirme yalnızca kimliği doğrulanmış kullanıcılar için Linkview düğmesini görüntüler.

[!code-aspx[Main](user-based-authorization-cs/samples/sample20.aspx)]

Şekil 11 ' de gösterildiği gibi, son sonuç, sütun içindeki görüntüleme bağlantı düğmeleri gizlense de görünüm sütununun görüntülenmesiyle ilgili değildir. Sonraki bölümde tüm GridView sütununu (yalnızca LinkButton değil) nasıl gizleyelim.

[![LoginView denetimi, anonim ziyaretçi için LinkButtons görünümünü gizler](user-based-authorization-cs/_static/image32.png)](user-based-authorization-cs/_static/image31.png)

**Şekil 11**: LoginView denetimi anonim ziyaretçilerin görünüm Linkbuttons 'ı gizler ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image33.png))

### <a name="programmatically-limiting-functionality"></a>Işlevselliği programlı bir şekilde sınırlandırma

Bazı durumlarda, bir sayfada işlevselliği kısıtlamak için bildirim temelli teknikler yetersizdir. Örneğin, belirli sayfa işlevselliğinin kullanılabilirliği, sayfayı ziyaret eden kullanıcının anonim veya kimliği doğrulanmış olduğu ölçütlere bağlı olabilir. Bu gibi durumlarda, çeşitli kullanıcı arabirimi öğeleri programlı yollarla görüntülenebilir veya gizlenebilir.

İşlevselliği programlı bir şekilde sınırlandırmak için iki görev gerçekleştirmeniz gerekir:

1. Sayfayı ziyaret eden kullanıcının işlevlere erişip erişemeyeceğini belirleme ve
2. Kullanıcı arabirimini, kullanıcının söz konusu işlevselliğe erişiminin olup olmadığına göre programlı bir şekilde değiştirin.

Bu iki görevin uygulamasını göstermek için, yalnızca GridView 'dan dosyaları silmeye izin veriyorum. İlk göreviniz, sayfanın ziyaret edilip edilmeyeceğini belirlemektir. Bu belirlendikten sonra GridView 'un silme sütununu gizlemeniz (veya göstermemiz) gerekir. GridView 'un sütunlarına `Columns` özelliği aracılığıyla erişilebilir; bir sütun yalnızca `Visible` özelliği `true` (varsayılan) olarak ayarlandıysa işlenir.

Verileri GridView 'a bağlamadan önce aşağıdaki kodu `Page_Load` olay işleyicisine ekleyin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample21.cs)]

[*Forms kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-cs.md) konusunda anlatıldığı gibi, `User.Identity.Name` kimliğin adını döndürür. Bu, oturum açma denetiminde girilen kullanıcı adına karşılık gelir. Sayfayı ziyaret etmek için, GridView 'un ikinci sütununun `Visible` özelliği `true`olarak ayarlanır; Aksi takdirde, `false`olarak ayarlanır. Net sonuç, sayfada başka bir kimliği doğrulanmış kullanıcı veya anonim kullanıcı, silme sütununun işlenmediğinde (bkz. Şekil 12); Ancak, sayfa ne zaman ziyaret edildiğinde silme sütunu mevcuttur (bkz. Şekil 13).

[![sütunu, Tito (deneme) dışında bir kişi tarafından ziyaret edildiğinde Işlenmez](user-based-authorization-cs/_static/image35.png)](user-based-authorization-cs/_static/image34.png)

**Şekil 12**: silme sütunu Tito (deneme) dışında bir kişi tarafından ziyaret edildiğinde işlenmez ([tam boyutlu görüntüyü görüntülemek için tıklatın](user-based-authorization-cs/_static/image36.png))

[![, Tito için silme sütunu Işlendi](user-based-authorization-cs/_static/image38.png)](user-based-authorization-cs/_static/image37.png)

**Şekil 13**: silme sütunu Tito için işlenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](user-based-authorization-cs/_static/image39.png))

## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>4\. Adım: sınıflara ve yöntemlere yetkilendirme kuralları uygulama

Adım 3 ' te anonim kullanıcıların bir dosyanın içeriğini görüntülemesini ve tüm kullanıcıları yasaklamasının yanı sıra dosyaları silmekten izin vermedik. Bu, bildirim temelli ve programlı teknikler aracılığıyla yetkisiz ziyaretçilerin ilişkili kullanıcı arabirimi öğelerini gizleyerek elde edildi. Basit örneğimiz için, Kullanıcı arabirimi öğelerinin düzgün bir şekilde gizlenmesi basittir, ancak aynı işlevselliği gerçekleştirmenin birçok farklı yolu olabileceği daha karmaşık siteler hakkında ne var? Bu işlevselliği yetkisiz kullanıcılara sınırlamak için, geçerli kullanıcı arabirimi öğelerini gizlemeyi veya devre dışı bırakmayı unuturuz ne olur?

Belirli bir işlevselliğe yetkisiz bir kullanıcı tarafından erişilememesini sağlamanın kolay bir yolu, bu sınıfı veya yöntemi [`PrincipalPermission` özniteliğiyle](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)tasarlamanız sağlamaktır. .NET çalışma zamanı bir sınıfı kullandığında veya yöntemlerinden birini yürüttüğünde, geçerli güvenlik bağlamının sınıfı kullanma veya yöntemi yürütme izni olduğundan emin olmak için kontrol eder. `PrincipalPermission` özniteliği, bu kuralları tanımlayabilmemiz için bir mekanizma sağlar.

GridView 'un `SelectedIndexChanged` ve `RowDeleting` olay işleyicilerinde `PrincipalPermission` özniteliğini kullanarak, sırasıyla adsız kullanıcılar ve kullanıcılar tarafından yürütmeyi yasaklayagörelim. Tüm yapmanız gereken, her bir işlev tanımının uygun özniteliğini eklemektir:

[!code-csharp[Main](user-based-authorization-cs/samples/sample22.cs)]

`SelectedIndexChanged` olay işleyicisi özniteliği, yalnızca kimliği doğrulanmış kullanıcıların olay işleyicisini yürütemeyeceğini belirler. burada, `RowDeleting` olay işleyicisindeki öznitelik, yürütmeyi Tito 'ya sınırlar.

`RowDeleting` olay işleyicisini yürütmeye veya kimliği doğrulanmamış bir kullanıcıya `SelectedIndexChanged` olay işleyicisini yürütmeyi denediğinde, .NET çalışma zamanı bir `SecurityException`yükseltir.

[![güvenlik bağlamının yöntemi yürütme yetkisi yoksa bir SecurityException atılır](user-based-authorization-cs/_static/image41.png)](user-based-authorization-cs/_static/image40.png)

**Şekil 14**: güvenlik bağlamının yöntemi yürütme yetkisi yoksa bir `SecurityException` oluşturulur ([tam boyutlu görüntüyü görüntülemek için tıklatın](user-based-authorization-cs/_static/image42.png))

> [!NOTE]
> Birden çok güvenlik bağlamının bir sınıfa veya yönteme erişmesine izin vermek için, her güvenlik bağlamı için bir `PrincipalPermission` özniteliğiyle sınıfı veya yöntemi süslemek. Diğer bir deyişle, her ikisinin de `RowDeleting` olay işleyicisini yürütmesine izin vermek için *iki* `PrincipalPermission` özniteliği ekleyin:

[!code-csharp[Main](user-based-authorization-cs/samples/sample23.cs)]

ASP.NET sayfalarına ek olarak, birçok uygulamanın Iş mantığı ve veri erişimi katmanları gibi çeşitli katmanları içeren bir mimarisi de vardır. Bu katmanlar genellikle sınıf kitaplıkları olarak uygulanır ve iş mantığı ve verilerle ilgili işlevleri gerçekleştirmek için sınıflar ve yöntemler sunar. `PrincipalPermission` özniteliği, bu katmanlara yetkilendirme kuralları uygulamak için yararlıdır.

Sınıflarda ve yöntemlerde yetkilendirme kurallarını tanımlamak için `PrincipalPermission` özniteliğini kullanma hakkında daha fazla bilgi için, [`PrincipalPermissionAttributes`kullanarak iş ve veri katmanlarına yetkilendirme kuralları ekleme ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx) [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin Blog girdisine bakın.

## <a name="summary"></a>Özet

Bu öğreticide, Kullanıcı tabanlı yetkilendirme kurallarının nasıl uygulanacağını inceledik. ASP 'ye göz atacağız. NET 'in URL yetkilendirme çerçevesi. Her istekte, ASP.NET altyapısının `UrlAuthorizationModule`, kimliğin istenen kaynağa erişme yetkisine sahip olup olmadığını anlamak için uygulamanın yapılandırmasında tanımlanan URL yetkilendirme kurallarını inceler. Kısaca, URL yetkilendirmesi belirli bir sayfa için veya belirli bir dizindeki tüm sayfalar için yetkilendirme kuralları belirtmeyi kolaylaştırır.

URL yetkilendirme çerçevesi, bir sayfa temelinde yetkilendirme kuralları uygular. URL yetkilendirmesi ile, istenen kimliğin belirli bir kaynağa erişme yetkisi vardır. Ancak, çok sayıda senaryo daha ince yetkilendirme kuralları için çağrı yapar. Bir sayfaya kimlerin erişebileceğini tanımlamak yerine herkesin bir sayfaya erişmesine izin vermek, ancak farklı verileri göstermek veya sayfayı ziyaret eden kullanıcıya bağlı olarak farklı işlevler sunmak için gerekli olabilir. Sayfa düzeyi yetkilendirme, genellikle yetkisiz kullanıcıların yasaklanmış işlevlere erişmesini engellemek için belirli kullanıcı arabirimi öğelerini gizlemeyi içerir. Bunlara ek olarak, belirli kullanıcılar için kendi yöntemlerinin sınıflarına ve yürütülmesine erişimi kısıtlamak üzere öznitelikleri kullanmak mümkündür.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [`PrincipalPermissionAttributes` kullanarak Iş ve veri katmanlarına yetkilendirme kuralları ekleme](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET yetkilendirmesi](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IıS6 ve ııS7 güvenliği arasındaki değişiklikler](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Belirli dosyaları ve alt dizinleri yapılandırma](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [Kullanıcıya bağlı olarak veri değişikliği Işlevselliğini sınırlama](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-cs.md)
- [LoginView denetimi hızlı başlangıçlarını Başlat](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [IıS7 URL yetkilendirmesini anlama](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` teknik belgeler](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [ASP.NET 2,0 'de verilerle çalışma](../../data-access/index.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](validating-user-credentials-against-the-membership-user-store-cs.md)
> [İleri](storing-additional-user-information-cs.md)
