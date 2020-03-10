---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: Kaynak denetimi (Azure ile gerçek dünyada bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5a1e0d7cd3c396d4be79c8958422602055eb3db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617455"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a>Kaynak denetimi (Azure ile gerçek dünyada bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Kaynak denetimi, yalnızca ekip ortamları değil tüm bulut geliştirme projeleri için gereklidir. Geri alma işlevi ve otomatik yedeklemeler olmadan kaynak kodunu veya bir Word belgesini düzenlemenizi düşünmez ve kaynak denetimi bir proje düzeyinde, bir şeyler yanlış kaldığında daha fazla zaman kaydedebilecekleri bu işlevleri sağlar. Bulut kaynak denetimi hizmetleriyle, artık karmaşık kurulum konusunda endişelenmenize gerek kalmaz ve Azure Repos kaynak denetimini ücretsiz olarak 5 Kullanıcı için ücretsiz olarak kullanabilirsiniz.

Bu bölümün ilk bölümünde aklınızda bulundurmanız gereken üç temel en iyi yöntem açıklanmaktadır:

- [Otomasyon komut dosyalarını kaynak kodu olarak değerlendirin](#scripts) ve uygulama kodunuzla birlikte sürüm yapın.
- Bir kaynak kodu deposuna [hiçbir şekilde gizli](#secrets) dizi (kimlik bilgileri gibi hassas veriler) iade etme.
- DevOps iş akışını etkinleştirmek için [kaynak dallarını ayarlayın](#devops) .

Bu bölümün geri kalanı, Visual Studio, Azure ve Azure Repos bu desenlerin bazı örnek uygulamalarını vermektedir:

- [Visual Studio 'da kaynak denetimine betikler ekleme](#vsscripts)
- [Hassas verileri Azure 'da depolayın](#appsettings)
- [Visual Studio 'da git 'i kullanın ve Azure Repos](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>Otomasyon betikleri kaynak kodu olarak davran

Bir bulut projesi üzerinde çalışırken, şeyleri sık sık değiştiriyorsunuz ve müşterileriniz tarafından bildirilen sorunlara hızlı bir şekilde tepki vermek istiyorsunuz. Hızlı yanıt verme, [her şeyi otomatikleştirin](automate-everything.md) bölümünde açıklandığı gibi Otomasyon betikleri kullanılarak oluşur. Ortamınızı oluşturmak için kullandığınız tüm betikler, ona dağıtın, ölçeklendirin, vb., uygulama kaynak kodunuzla eşitlenmiş olması gerekir.

Betikleri kod ile eşitlenmiş halde tutmak için, onları kaynak denetimi sisteminizde depolayın. Daha sonra, değişiklikleri geri almanız veya geliştirme kodundan farklı olan üretim koduna hızlı bir çözüm yapmanız gerekiyorsa, hangi ayarların değiştirildiğini veya hangi takım üyelerinin ihtiyacınız olan sürümün kopyalarına sahip olduğunu izlemeye çalışırken zaman harcanmak zorunda kalmazsınız. İhtiyacınız olan betiklerin, sizin için ihtiyaç duyduğunuz kod tabanı ile eşitlenmiş olduğundan ve tüm takım üyelerinin aynı betiklerle çalıştığından emin olmanız gerekir. Daha sonra üretime veya yeni özellik geliştirmeye yönelik bir sık düzeltme testi ve dağıtımını otomatikleştirmeniz gerekip gerekmediği için, güncelleştirilmesi gereken kod için doğru betiğe sahip olacaksınız.

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>Gizli dizileri denetleme

Kaynak kodu deposuna genellikle, parola gibi hassas veriler için uygun bir güvenli yer olması çok fazla kişi tarafından erişilebilir. Betikler parolalar gibi gizli dizileri kullanıyorsa, bu ayarları kaynak koda kaydedilmemesi için parametreleştirin ve sırlarınızı başka bir yere depolarlar.

Örneğin Azure, yayımlama profillerinin oluşturulmasını otomatik hale getirmek için yayımlama ayarları içeren dosyaları indirmenizi sağlar. Bu dosyalar, Azure hizmetlerinizi yönetme yetkisine sahip kullanıcı adlarını ve parolalarını içerir. Yayımlama profilleri oluşturmak için bu yöntemi kullanırsanız ve bu dosyaları kaynak denetimine iade ederseniz, deponuza erişimi olan herkes bu kullanıcı adlarını ve parolalarını görebilir. Parolayı, şifreli olduğu ve bir *. pubxml. User* dosyası varsayılan olarak kaynak denetimine dahil olmayan bir. pubxml dosyasında güvenli bir şekilde, yayımlama profilinde güvenli bir şekilde depolayabilirsiniz.

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>DevOps iş akışını kolaylaştırmak için yapı kaynağı dalları

Deponuzdaki dalları nasıl uygulayabileceğiniz, her ikisi de yeni özellikler geliştirme ve üretimde sorunları çözme yeteneğinizi etkiler. İşte çok sayıda orta ölçekli ekibin kullanması gereken bir örüntü:

![Kaynak dal yapısı](source-control/_static/image1.png)

Ana dal her zaman üretimde olan kodla eşleşir. Ana altındaki dallar geliştirme yaşam döngüsünde farklı aşamalara karşılık gelir. Geliştirme Dalı, yeni özellikleri uyguladığınız yerdir. Küçük bir takım için yalnızca ana ve geliştirmeye sahip olabilirsiniz, ancak çoğu zaman geliştirme ve ana arasında bir hazırlama dalı olmasını öneririz. Güncelleştirme üretime taşınmadan önce son tümleştirme testi için hazırlama kullanabilirsiniz.

Büyük takımlar için, her yeni özellik için ayrı dallar olabilir; daha küçük bir takım için, geliştirme dalında herkesin iade ettiğine sahip olabilirsiniz.

Her bir özellik için bir dala sahipseniz, özelliği bir, geliştirme dalında ve diğer özellik dallarına göre kaynak kodu değişikliklerini birleştirir. Bu kaynak kodu birleştirme işlemi zaman alabilir ve özellikleri ayrı tutarken bu çalışmayı önlemek için, bazı ekipler *[özellik](http://en.wikipedia.org/wiki/Feature_toggle)* ( *özellik bayrakları*olarak da bilinir) adlı bir alternatif uygular. Bu, tüm özelliklerin tüm kodunun aynı dalda olduğu, ancak koddaki anahtarları kullanarak her bir özelliği etkinleştirdiğiniz veya devre dışı bırakacağı anlamına gelir. Örneğin, özellik A 'nın BT uygulama görevlerini gidermeye yönelik yeni bir alan olduğunu ve B özelliği de önbelleğe alma işlevselliği ekliyor olduğunu varsayalım. Her iki özellik için de kod, geliştirme dalında olabilir, ancak uygulama yalnızca bir değişken true olarak ayarlandığında yeni alanı görüntüler ve yalnızca farklı bir değişken true olarak ayarlandığında önbelleğe alma kullanır. Özellik A yükseltilmeye hazırsa, ancak B özelliği hazırsanız, tüm kodu bir geçiş özelliği ve B özelliği ile birlikte üretime yükseltebilirsiniz. Daha sonra, özellik A 'yı ve daha sonra kaynak kodu birleştirme olmadan daha sonra yükseltebilirsiniz.

Dallar veya özellikler için geçiş tuşlarını kullanmanıza bakılmaksızın, bu gibi bir dallanma yapısı, kodunuzu geliştirmede çevik ve yinelenebilir bir şekilde üretim ortamına göndermenizi sağlar.

Bu yapı ayrıca müşteri geri bildirimlerine hızlı bir şekilde tepki sağlamanıza olanak sağlar. Üretime hızlı bir çözüm yapmanız gerekiyorsa, bunu çevik bir şekilde de verimli bir şekilde yapabilirsiniz. Ana veya hazırlama dışında bir dal oluşturabilir ve bu özelliği, ana öğe ile, geliştirme ve özellik dallarına göre daha düşük bir şekilde birleştirin.

![Düzeltme dalı](source-control/_static/image2.png)

Üretim ve geliştirme dallarının ayrımı ile buna benzer bir dallanma yapısı olmadan bir üretim sorunu, üretim düzeltmeinizle birlikte yeni özellik kodu yükseltme zorunlulukla ilgili olarak sizi bir araya geçirebilir. Yeni özellik kodu tam olarak sınanmayabilir ve üretime hazır olmayabilir ve hazır olmayan değişiklikleri yedeklemek için çok sayıda iş yapmanız gerekebilir. Ya da değişiklikleri test etmek ve dağıtıma hazırlamak için düzeltmelerinizi geciktirebilmeniz gerekebilir.

Daha sonra, bu üç deseni Visual Studio, Azure ve Azure Repos nasıl uygulayacağınızı gösteren örnekler görürsünüz. Bunlar, ayrıntılı adım adım nasıl yapılır yönergeleri yerine örnek olarak verilmiştir; gerekli tüm bağlamı sağlayan ayrıntılı yönergeler için, bölümün sonundaki [kaynaklar](#resources) bölümüne bakın.

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>Visual Studio 'da kaynak denetimine betikler ekleme

Visual Studio 'da kaynak denetimine komut dosyalarını bir Visual Studio çözüm klasörüne dahil ederek ekleyebilirsiniz (projenizin kaynak denetiminde olduğu varsayılırsa). Bunu yapmanın bir yolu aşağıda verilmiştir.

Çözüm klasörünüzdeki betikler için bir klasör oluşturun ( *. sln* dosyanızı içeren klasör).

![Otomasyon klasörü](source-control/_static/image3.png)

Betik dosyalarını klasörüne kopyalayın.

![Otomasyon klasörü içeriği](source-control/_static/image4.png)

Visual Studio 'da projeye bir çözüm klasörü ekleyin.

![Yeni çözüm klasörü menü seçimi](source-control/_static/image5.png)

Ve betik dosyalarını çözüm klasörüne ekleyin.

![Varolan öğe menü seçimini Ekle](source-control/_static/image6.png)

![Varolan öğe Ekle iletişim kutusu](source-control/_static/image7.png)

Betik dosyaları artık projenize dahil edilmiştir ve kaynak denetimi, bunlara karşılık gelen kaynak kodu değişiklikleriyle birlikte sürüm değişikliklerini izliyor.

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>Hassas verileri Azure 'da depolayın

Uygulamanızı bir Azure Web sitesinde çalıştırırsanız, kaynak denetiminde kimlik bilgilerini depolamanın bir yolu, bunları Azure 'da depolayamaktır.

Örneğin, BT uygulaması, Web. config dosyasında depolar, üretimde parolalara sahip olacak iki bağlantı dizesi ve Azure depolama hesabınıza erişim sağlayan bir anahtar.

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

Bu ayarların gerçek üretim değerlerini *Web. config* dosyanıza yerleştirirseniz veya Web. *Release. config* dosyasına yerleştirirseniz, dağıtım sırasında bunları eklemek üzere bir Web. config dönüşümü yapılandırırsanız, bunlar kaynak deposunda depolanır. Veritabanı bağlantı dizelerini üretim yayımlama profiline girerseniz, parola *. pubxml* dosyanızda olur. ( *. Pubxml* dosyasını kaynak denetiminden dışlayabilirsiniz, ancak diğer tüm dağıtım ayarlarını paylaşma avantajını kaybedersiniz.)

Azure, *Web. config* dosyasının **appSettings** ve bağlantı dizeleri bölümlerine bir alternatif sağlar. Azure yönetim portalı 'nda bir Web sitesi için **yapılandırma** sekmesinin ilgili bölümü aşağıda verilmiştir:

![Portalda appSettings ve connectionStrings](source-control/_static/image8.png)

Bu Web sitesine bir proje dağıttığınızda ve uygulama çalıştığında, Azure 'da depoladığınız her türlü değer, Web. config dosyasında her türlü değeri geçersiz kılar.

Bu değerleri, yönetim portalı veya betikleri kullanarak Azure 'da ayarlayabilirsiniz. [Her şeyi otomatikleştirin](automate-everything.md) bölümünde gördüğünüz ortam oluşturma Otomasyon betiği BIR Azure SQL veritabanı oluşturur, depolama ve SQL veritabanı bağlantı dizelerini alır ve bu gizli dizileri Web sitenizin ayarlarında depolar.

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

Gerçek değerlerin kaynak depoya kalıcı hale getirmemesi için betiklerin parametreleştirildiğine dikkat edin.

Geliştirme ortamınızda yerel olarak çalıştırdığınızda, uygulama yerel Web. config dosyanızı okur ve bağlantı dizeniz Web projenizin *app\_Data* klasöründe bir localdb SQL Server veritabanına işaret eder. Uygulamayı Azure 'da çalıştırdığınızda ve uygulama Web. config dosyasından bu değerleri okumaya çalıştığında, ne geri aldığı ve kullandığı, Web. config dosyasında gerçekte değil, Web sitesi için depolanan değerlerdir.

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a>Visual Studio ve Azure DevOps 'da git 'i kullanma

Daha önce sunulan DevOps dallanma yapısını uygulamak için herhangi bir kaynak denetimi ortamını kullanabilirsiniz. Dağıtılmış takımlar için [Dağıtılmış bir sürüm denetim sistemi](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS) en iyi şekilde çalışabilir; diğer ekipler için [merkezi bir sistem](http://en.wikipedia.org/wiki/Revision_control) daha iyi çalışabilir.

[Git](http://git-scm.com/) , popüler bir dağıtılmış sürüm denetim sistemidir. Kaynak denetimi için git kullandığınızda, yerel bilgisayarınızdaki tüm geçmişiyle birlikte deponun tamamen bir kopyasına sahip olursunuz. Ağ bağlantısı olmadığında çalışmaya devam etmek daha kolay olduğundan çok sayıda kişi bunu tercih eder; işleme ve geri alma işlemlerini gerçekleştirmeye devam edebilir, dalları oluşturup geçiş yapabilirsiniz. Ağa bağlı olduğunuzda bile, dallar oluşturmak ve her şey yerel olduğunda dalları değiştirmek daha kolay ve hızlıdır. Ayrıca, diğer geliştiricilere etki vermeden yerel işlemeler ve geri alma işlemlerini de gerçekleştirebilirsiniz. Ve toplu işleme işlemlerini sunucuya göndermeden önce gerçekleştirebilirsiniz.

[Azure Repos](/azure/devops/repos/index?view=vsts) hem [Git](/azure/devops/repos/git/?view=vsts) hem de [Team Foundation sürüm denetimi](/azure/devops/repos/tfvc/index?view=vsts) (TFVC; merkezi kaynak denetimi) sağlar. [Burada](https://app.vsaex.visualstudio.com/signup)Azure DevOps ile çalışmaya başlayın.

Visual Studio 2017, yerleşik, birinci sınıf [Git desteğini](https://msdn.microsoft.com/library/hh850437.aspx)içerir. Bunun nasıl çalıştığına ilişkin hızlı bir tanıtım aşağıda verilmiştir.

Visual Studio 'da açık bir proje ile **Çözüm Gezgini**' de çözüme sağ tıklayın ve ardından **kaynak denetimine çözüm Ekle**' yi seçin.

![Kaynak denetimine çözüm ekleme](source-control/_static/image9.png)

Visual Studio, TFVC (merkezi sürüm denetimi) veya git kullanmak isteyip istemediğinizi sorar.

![Kaynak denetimi seçin](source-control/_static/image10.png)

Git ' i ve **Tamam**' ı seçtiğinizde, Visual Studio çözüm klasörünüzde yeni bir yerel Git deposu oluşturur. Yeni depoda henüz dosya yok; bir git işlemi gerçekleştirerek bunları depoya eklemeniz gerekir. **Çözüm Gezgini**çözüme sağ tıklayın ve ardından **Yürüt**' e tıklayın.

![İşleme](source-control/_static/image11.png)

Visual Studio, tüm proje dosyalarını işlemeye göre otomatik olarak aşamalar ve **Içerilen değişiklikler** bölmesinde **Takım Gezgini** listeler. (İşlemeye eklemek istemediğiniz bir sorun varsa, bunları seçebilir, sağ tıklayıp **Dışla**' ya tıklayabilirsiniz.)

![Ekip Gezgini](source-control/_static/image12.png)

Bir tamamlama açıklaması girin ve **Yürüt**' e tıklayın ve Visual Studio yürütmeyi yürütür ve yürütme kimliğini görüntüler.

![Takım Gezgini değişiklikler](source-control/_static/image13.png)

Bundan sonra bazı kodları depodaki verilerden farklı olacak şekilde değiştirirseniz, farkları kolayca görebilirsiniz. Değiştirdiğiniz bir dosyaya sağ tıklayın, **değiştirilmemiş olan Karşılaştır**' ı seçin ve kaydedilmemiş değişiklerinizi gösteren bir karşılaştırma ekranı alırsınız.

![Değiştirilmemiş ile karşılaştır](source-control/_static/image14.png)

![Değişiklikleri gösteren fark](source-control/_static/image15.png)

Yaptığınız değişiklikleri kolayca görebilir ve iade edebilirsiniz.

Bir dal oluşturmanız gerektiğini varsayın; bunu Visual Studio 'da da yapabilirsiniz. **Takım Gezgini**' de, **yeni dal**' ı tıklatın.

![Yeni dalı Takım Gezgini](source-control/_static/image16.png)

Bir dal adı girin, **dal oluştur**' a tıklayın ve **dalı kullanıma al**' ı seçtiyseniz, Visual Studio otomatik olarak yeni dalı kontrol eder.

![Yeni dalı Takım Gezgini](source-control/_static/image17.png)

Artık dosyalarda değişiklik yapabilir ve bu dala iade edebilirsiniz. Ve dallar arasında kolayca geçiş yapabilirsiniz ve Visual Studio dosyaları kullanıma aldığınız dala göre otomatik olarak eşitler. Bu örnekte, *\_Layout. cshtml* içindeki Web sayfası başlığı HotFix1 dalında "Hot düzeltmesini 1" olarak değiştirilmiştir.

![Hotfix1 dalı](source-control/_static/image18.png)

Ana dala geri geçerseniz, *\_Layout. cshtml* dosyasının içeriği otomatik olarak ana dalda oldukları gibi döndürülür.

![Ana dal](source-control/_static/image19.png)

Bu, bir dalı hızlı bir şekilde oluşturma ve dallar arasında geri çevirme hakkında basit bir örnektir. Bu özellik [her şeyi otomatikleştirin](automate-everything.md) bölümünde sunulan dal yapısını ve otomasyon betiklerini kullanarak yüksek derecede çevik bir iş akışını mümkün hale getirir. Örneğin, geliştirme dalında çalışıyor, ana öğe üzerinde etkin bir düzeltme dalı oluşturabilir, yeni dala geçebilir, değişikliklerinizi orada yapabilir ve kaydedebilir ve sonra geliştirme dalına geri dönüp yaptığınız işleme devam edebilirsiniz.

Burada gördüğünüz özellikler, Visual Studio 'da yerel bir git deposu ile nasıl çalışdıklardır. Bir ekip ortamında, genellikle değişiklikleri ortak bir depoya gönderebilirsiniz. Visual Studio Araçları Ayrıca uzak bir git deposuna işaret etmeniz için de sağlar. Bu amaçla GitHub.com kullanabilir veya iş öğesi ve hata izleme gibi diğer tüm Azure DevOps özellikleri ile tümleştirilmiş [Git ve Azure Repos](/azure/devops/repos/git/overview?view=vsts) kullanabilirsiniz.

Bu, tabii ki çevik bir dallanma stratejisi uygulayabileceğiniz tek yoldur. Merkezi bir kaynak denetimi deposu kullanarak aynı çevik iş akışını etkinleştirebilirsiniz.

## <a name="summary"></a>Özet

Kaynak denetim sisteminizin başarısını, ne kadar hızlı bir şekilde değişiklik yapabileceğiniz ve güvenli ve öngörülebilir bir şekilde canlı hale getirebileceğinizi ölçmenize göre ölçün. Üzerinde el ile test yapmak zorunda olduğunuz için bir gün veya iki testi yapmanız gereken bir değişiklik yapmak için kendinizi korkmuş olmanız fark ederseniz, bu değişikliği dakikalar içinde veya en kötü bir saatten uzun bir süre olmayacak şekilde kendinize, işlem tabanlı veya test temelinde ne yapmak istediğinizi sorabilirsiniz. Bir [sonraki bölümde](continuous-integration-and-continuous-delivery.md)ele alacağız ve sürekli tümleştirme ve sürekli teslim uygulamak için bir stratejidir.

<a id="resources"></a>
## <a name="resources"></a>Kaynaklar

Dallanma stratejileri hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Team Foundation Server 2012 Ile yayın Işlem hattı oluşturuluyor](https://msdn.microsoft.com/library/dn449957.aspx). Microsoft düzenleri ve uygulamalar belgeleri. Dallanma stratejilerinin tartışılması için Bölüm 6 ' ya bakın. Advobir özelliği özellik dallarına geçiş yapar ve özellikler için dallar kullanılırsa, kısa ömürlü (en fazla saat veya gün) tasarruf edin.
- [Sürüm denetimi kılavuzu](https://aka.ms/vsarsolutions). ALM derecelendirmeleri tarafından dallanma stratejilerine kılavuzluk edin. Indirmeler sekmesinde bkz. dallandırma stratejileri. PDF.
- [Özelliği olan yazılım geliştirme özelliği geçiş yapar](https://msdn.microsoft.com/magazine/dn683796.aspx). MSDN Magazine makalesi.
- [Özellik geçişi](http://martinfowler.com/bliki/FeatureToggle.html). Marwler 'in blogdaki Özellik geçiş ve özellik bayraklarının tanıtımı.
- [Özellik, vs Özellik dallarına geçiş yapar](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx). Özelliği ile ilgili başka bir blog gönderisi, Dylan Smith 'e göre geçiş yapar.

Kaynak denetimi depolarında tutulmayacak gizli bilgilerin nasıl işleneceği hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.net ve Azure App Service için parola ve diğer hassas verileri dağıtmaya yönelik en iyi uygulamalar](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
- [Azure Web siteleri: uygulama dizeleri ve bağlantı dizeleri nasıl çalışır?](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) *Web. config* dosyasında `appSettings` ve `connectionStrings` verileri geçersiz kılan Azure özelliğini açıklar.
- [Azure Web sitelerinde özel yapılandırma ve uygulama ayarları, Stefan Schackow ile](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/).

Gizli bilgileri kaynak denetiminden tutmanın diğer yöntemleri hakkında daha fazla bilgi için bkz. [ASP.NET MVC: özel ayarları kaynak denetiminden koruyun](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).

> [!div class="step-by-step"]
> [Önceki](automate-everything.md)
> [İleri](continuous-integration-and-continuous-delivery.md)
