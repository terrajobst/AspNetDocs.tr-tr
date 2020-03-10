---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: Proje dosyasını anlama | Microsoft Docs
author: jrjlee
description: Microsoft Build Engine (MSBuild) proje dosyaları, derleme ve dağıtım sürecinin kalbi tarafında yer almalıdır. Bu konu, MSBuild 'e kavramsal bir genel bakış ile başlar...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 419fe51aaf65bddcc2c50380f099f842a8d9439c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626233"
---
# <a name="understanding-the-project-file"></a>Proje dosyasını anlama

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Microsoft Build Engine (MSBuild) proje dosyaları, derleme ve dağıtım sürecinin kalbi tarafında yer almalıdır. Bu konu, MSBuild ve proje dosyasına kavramsal bir genel bakış ile başlar. Bu, proje dosyalarıyla çalışırken sunabileki temel bileşenleri açıklar ve gerçek dünya uygulamalarını dağıtmak için proje dosyalarını nasıl kullanabileceğinizi gösteren bir örnek üzerinden çalışır.
> 
> Öğrenecekleriniz:
> 
> - MSBuild, projeleri oluşturmak için MSBuild proje dosyalarını nasıl kullanır.
> - MSBuild, Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) gibi dağıtım teknolojileriyle tümleştirilir.
> - Bir proje dosyasının temel bileşenlerini anlama.
> - Karmaşık uygulamalar oluşturmak ve dağıtmak için proje dosyalarını nasıl kullanabileceğinizi öğrenin.

## <a name="msbuild-and-the-project-file"></a>MSBuild ve proje dosyası

Visual Studio 'da çözümler oluşturup yapılandırdığınızda, Visual Studio, çözümünüzde her bir projeyi derlemek için MSBuild kullanır. Her Visual Studio projesi, projenin&#x2014;türünü yansıtan bir dosya uzantısına sahip bir MSBuild proje dosyası içerir, örneğin bir C# proje (. csproj), bir Visual Basic.NET projesi (. vbproj) veya bir veritabanı projesi (. dbproj). Bir proje oluşturmak için MSBuild, projeyle ilişkili proje dosyasını işlemelidir. Proje dosyası, projenizi oluşturmak için, dahil edilecek içerik, Platform gereksinimleri, sürüm bilgileri, Web sunucusu veya veritabanı sunucusu ayarları gibi MSBuild 'in ihtiyaç duyacağı tüm bilgileri ve yönergeleri içeren bir XML belgesidir. gerçekleştirilmesi gereken görevler.

MSBuild proje dosyaları, [MSBUILD XML şemasını](/visualstudio/msbuild/msbuild-project-file-schema-reference)temel alır ve sonuç olarak derleme işlemi tamamen açık ve şeffaf olur. Ayrıca, MSBuild altyapısını&#x2014;kullanabilmeniz Için Visual Studio 'yu yüklemeniz gerekmez MSBuild. exe yürütülebilir dosyası .NET Framework bir parçasıdır ve bunu bir komut isteminden çalıştırabilirsiniz. Bir geliştirici olarak, projelerinizin nasıl oluşturulup dağıtıldığı hakkında gelişmiş ve ayrıntılı denetim sağlamak için MSBuild XML şemasını kullanarak kendi MSBuild proje dosyalarınızı oluşturabilirsiniz. Bu özel proje dosyaları, Visual Studio 'Nun otomatik olarak oluşturduğu proje dosyalarıyla tam olarak aynı şekilde çalışır.

> [!NOTE]
> MSBuild proje dosyalarını, Team Foundation Server (TFS) içindeki Team Build Service ile de kullanabilirsiniz. Örneğin, yeni kod iade edildiğinde bir test ortamına dağıtımı otomatikleştirmek için, sürekli tümleştirme (CI) senaryolarında proje dosyalarını kullanabilirsiniz. Daha fazla bilgi için bkz. [Otomatik Web dağıtımı için Team Foundation Server yapılandırma](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).

### <a name="project-file-naming-conventions"></a>Proje dosyası adlandırma kuralları

Kendi proje dosyalarınızı oluştururken istediğiniz dosya uzantısını kullanabilirsiniz. Ancak, çözümlerinizi başkalarının anlaması için daha kolay hale getirmek üzere şu ortak kuralları kullanmanız gerekir:

- Projeleri oluşturan bir proje dosyası oluştururken. proj uzantısını kullanın.
- Başka proje dosyalarına aktarmak için yeniden kullanılabilir bir proje dosyası oluşturduğunuzda. targets uzantısını kullanın. . Targets uzantısına sahip dosyalar genellikle hiçbir şey oluşturmazlar, yalnızca. proj dosyalarınıza aktarabileceğiniz yönergeleri içerirler.

### <a name="integration-with-deployment-technologies"></a>Dağıtım teknolojileriyle tümleştirme

Visual Studio 2010 ' de ASP.NET Web uygulamaları ve ASP.NET MVC web uygulamaları gibi Web uygulaması projeleriyle çalıştıysanız, bu projelerin, Web uygulamasını paketleme ve hedef bir ortama dağıtmaya yönelik yerleşik destek içerir. Bu projelere yönelik **Özellikler** sayfaları, uygulamanızın bileşenlerinin paketlenmesi ve dağıtılması Için kullanabileceğiniz **paket/yayımlama Web** ve **paket/yayımlama SQL** sekmelerini içerir. Bu, **paketle/Yayımla Web** sekmesini gösterir:

![](understanding-the-project-file/_static/image1.png)

Bu yeteneklerin arkasındaki temel teknoloji Web yayımlama işlem hattı (WPP) olarak bilinir. WPP, Web uygulamalarınız için kapsamlı bir derleme, paket ve dağıtım işlemi sağlamak üzere MSBuild ve [Web dağıtımı](https://go.microsoft.com/?linkid=9805122) bir araya getirir.

İyi haber, Web projeleri için özel proje dosyaları oluştururken WPP 'nin sağladığı tümleştirme noktalarından faydalanabilir. Proje dosyanıza, projelerinizi oluşturmanıza, Web dağıtım paketleri oluşturmanıza ve bu paketleri tek bir proje dosyası ve MSBuild 'e tek bir çağrı aracılığıyla uzak sunuculara yüklemenize olanak tanıyan dağıtım yönergelerini dahil edebilirsiniz. Ayrıca, yapı işleminizin bir parçası olarak diğer yürütülebilir dosyaları da çağırabilirsiniz. Örneğin, bir şema dosyasından bir veritabanı dağıtmak için VSDBCMD. exe komut satırı aracını çalıştırabilirsiniz. Bu konu başlığı altında, kurumsal dağıtım senaryolarınızın gereksinimlerini karşılamak için bu özelliklerden nasıl yararlanabileceksiniz göreceksiniz.

> [!NOTE]
> Web uygulaması dağıtım işleminin nasıl çalıştığı hakkında daha fazla bilgi için bkz. [ASP.NET Web uygulaması proje dağıtımına genel bakış](https://msdn.microsoft.com/library/dd394698.aspx).

## <a name="the-anatomy-of-a-project-file"></a>Proje dosyasının Anatomumu

Yapı işlemine daha ayrıntılı bir şekilde bakmadan önce, bir MSBuild proje dosyasının temel yapısıyla ilgili bilgi edinmek için birkaç dakika harcamanız gerekir. Bu bölüm, bir proje dosyasını gözden geçirdikten, düzenlerken veya oluştururken karşılaşabileceğiniz daha yaygın öğelere genel bir bakış sağlar. Özellikle şunları öğreneceksiniz:

- Yapı işlemi için değişkenleri yönetmek üzere *özellikleri* kullanma.
- Kod dosyaları gibi yapı işleminin girişlerini tanımlamak için *öğeleri* kullanma.
- Proje dosyasında başka bir yerde tanımlanan *özellikleri* ve *öğeleri* kullanarak MSBuild 'e yürütme yönergeleri sağlamak için *hedefleri* ve *görevleri* kullanma.

Bu, MSBuild proje dosyasındaki anahtar öğeleri arasındaki ilişkiyi gösterir:

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>Proje öğesi

[Proje](https://msdn.microsoft.com/library/bcxfsh87.aspx) öğesi her proje dosyasının kök öğesidir. Proje dosyasının XML şemasını tanımlamaya ek olarak, **Proje** öğesi yapı işlemi için giriş noktalarını belirtmek üzere öznitelikler içerebilir. Örneğin, [Contact Manager örnek çözümünde](the-contact-manager-solution.md) *Publish. proj* dosyası, değişkenin **fullpublish**adlı hedefi çağırarak başlaması gerektiğini belirtir.

[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]

### <a name="properties-and-conditions"></a>Özellikler ve koşullar

Projeleri başarıyla derlemek ve dağıtmak için bir proje dosyasının genellikle çok sayıda farklı bilgi sağlaması gerekir. Bu bilgi parçaları arasında sunucu adları, bağlantı dizeleri, kimlik bilgileri, derleme yapılandırması, kaynak ve hedef dosya yolları ve özelleştirmeyi desteklemek için eklemek istediğiniz diğer bilgiler yer alır. Bir proje dosyasında, özellikler bir [PropertyGroup](https://msdn.microsoft.com/library/t4w159bs.aspx) öğesi içinde tanımlanmalıdır. MSBuild özellikleri anahtar-değer çiftlerinden oluşur. **PropertyGroup** öğesi içinde, öğe adı özellik anahtarını ve öğenin içeriği özellik değerini tanımlar. Örneğin, bir statik sunucu adı ve bağlantı dizesi depolamak için **ServerName** ve **ConnectionString** adlı özellikler tanımlayabilirsiniz.

[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]

Bir özellik değerini almak için, *$ (PropertyName)* biçimini kullanın. Örneğin, **ServerName** özelliğinin değerini almak için şunu yazın:

[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]

> [!NOTE]
> Bu konunun ilerleyen kısımlarında özellik değerlerinin nasıl ve ne zaman kullanılacağı hakkında örnekler görürsünüz.

Bilgileri bir proje dosyasında statik özellikler olarak katıştırma, yapı sürecini yönetmek için her zaman ideal bir yaklaşım değildir. Birçok senaryoda, diğer kaynaklardan bilgileri almak veya kullanıcıyı komut isteminden bilgileri sağlamaya güç vermek isteyeceksiniz. MSBuild, herhangi bir özellik değerini bir komut satırı parametresi olarak belirtmenizi sağlar. Örneğin, Kullanıcı komut satırından MSBuild. exe çalıştırıyorsa, **ServerName** için bir değer sağlayabilir.

[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]

> [!NOTE]
> MSBuild. exe ile kullanabileceğiniz bağımsız değişkenler ve anahtarlar hakkında daha fazla bilgi için bkz. [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311.aspx).

Ortam değişkenlerinin ve yerleşik proje özelliklerinin değerlerini elde etmek için aynı özellik sözdizimini kullanabilirsiniz. Yaygın olarak kullanılan birçok özellik sizin için tanımlanır ve ilgili parametre adını ekleyerek bunları proje dosyalarınızda kullanabilirsiniz. &#x2014;Örneğin, geçerli proje platformunu almak için örneğin, **x86** veya **AnyCpu**&#x2014;, proje dosyanıza **$ (Platform)** özelliği başvurusunu dahil edebilirsiniz. Daha fazla bilgi için bkz. [derleme komutları ve özellikleri Için makrolar](https://msdn.microsoft.com/library/c02as0cs.aspx), [Ortak MSBuild proje özellikleri](https://msdn.microsoft.com/library/bb629394.aspx)ve [ayrılmış Özellikler](https://msdn.microsoft.com/library/ms164309.aspx).

Özellikler, genellikle *koşullarla*birlikte kullanılır. Çoğu MSBuild öğesi **koşul** özniteliğini destekler, bu, MSBuild 'in öğeyi değerlendirmesi gereken kriterleri belirtmenize olanak tanır. Örneğin, bu özellik tanımını göz önünde bulundurun:

[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]

MSBuild bu özellik tanımını işlediğinde, önce bir **$ (Outputroot)** Özellik değerinin kullanılabilir olup olmadığını kontrol eder. Özellik değeri başka bir sözcükte&#x2014;boşsa, Kullanıcı bu özellik&#x2014;için bir değer sağlamadıysa koşulun **true** olarak değerlendirilir ve özellik değeri olarak ayarlanır **... \Publish\Out**. Kullanıcı bu özellik için bir değer sağladıysa, koşul **yanlış** olarak değerlendirilir ve statik özellik değeri kullanılmaz.

Koşulları belirtebileceğiniz farklı yollar hakkında daha fazla bilgi için bkz. [MSBuild koşulları](https://msdn.microsoft.com/library/7szfhaft.aspx).

### <a name="items-and-item-groups"></a>Öğeler ve öğe grupları

Proje dosyasının önemli rollerinden biri, yapı işlemine yönelik girişleri tanımlamaktır. Genellikle, bu girişler dosya&#x2014;kodu dosyaları, yapılandırma dosyaları, komut dosyaları ve yapı sürecinin bir parçası olarak işlenmesi veya kopyalamanız gereken diğer dosyalardır. MSBuild proje şemasında, bu girişler [öğe](https://msdn.microsoft.com/library/ms164283.aspx) öğeleri tarafından temsil edilir. Bir proje dosyasında, öğelerin bir [ItemGroup](https://msdn.microsoft.com/library/646dk05y.aspx) öğesi içinde tanımlanması gerekir. Tıpkı **özellik** öğelerine benzer şekilde, bir **öğe** öğesi olarak istediğiniz şekilde ad verebilirsiniz. Ancak, öğenin temsil ettiği dosyayı veya joker karakterini tanımlamak için bir **içerme** özniteliği belirtmeniz gerekir.

[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]

Aynı ada sahip birden çok **öğe** öğesi belirterek, adlandırılmış kaynak listesini etkin bir şekilde oluşturursunuz. Bu işlemi, Visual Studio 'nun oluşturduğu proje dosyalarından birinin içinde görmenin iyi bir yoludur. Örneğin, örnek çözümdeki *ContactManager. Mvc. csproj* dosyası, her biri aynı şekilde adlandırılmış **öğe** öğeleri olan çok sayıda öğe grubu içerir.

[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]

Bu şekilde, proje dosyası, **başvuru** listesi başarılı bir derleme için yerinde olması gereken derlemeleri Içerir, **derleme** listesi derlenmesi gereken kod dosyalarını&#x2014;içerir ve **içerik** listesi, değiştirilmemiş olarak kopyalanmaları gereken kaynakları içerir, aynı şekilde işlenmesi gereken dosya listeleri oluşturmak için MSBuild. Yapı sürecinin bu öğelerin ilerleyen kısımlarında bu öğeleri nasıl başvurtığlarından ve bu öğelerin nasıl kullandığına bakacağız.

Öğe öğeleri, [ItemMetadata](https://msdn.microsoft.com/library/ms164284.aspx) alt öğelerini de içerebilir. Bunlar, Kullanıcı tanımlı anahtar-değer çiftleridir ve temelde bu öğeye özgü özellikleri temsil eder. Örneğin, proje dosyasındaki **derleme** öğesi öğelerinin çok sayıda alt öğe **üzerinde dependentöğesi** vardır.

[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]

> [!NOTE]
> Kullanıcı tarafından oluşturulan öğe meta verilerine ek olarak, tüm öğelere oluşturma sırasında çeşitli ortak meta veriler atanır. Daha fazla bilgi için bkz. [tanınmış öğe meta verileri](https://msdn.microsoft.com/library/ms164313.aspx).

Kök düzeyindeki **Proje** öğesi veya belirli **hedef** öğeleri içinde **ItemGroup** öğeleri oluşturabilirsiniz. **ItemGroup** öğeleri ayrıca, proje yapılandırması veya platformu gibi koşullara göre yapı işlemine girişleri uyarlamanızı sağlayan **koşul** özniteliklerini de destekler.

### <a name="targets-and-tasks"></a>Hedefler ve Görevler

MSBuild şemasında, bir [görev](https://msdn.microsoft.com/library/77f2hx1s.aspx) öğesi, tek bir yapı yönergesini (veya görevini) temsil eder. MSBuild, önceden tanımlanmış çok sayıda görev içerir. Örneğin:

- **Kopyalama** görevi dosyaları yeni bir konuma kopyalar.
- **CSC** görevi, görsel C# derleyicisini çağırır.
- **Vbc** görevi Visual Basic derleyicisini çağırır.
- **Exec** görevi belirtilen programı çalıştırır.
- **İleti** görevi bir günlükçü için bir ileti yazar.

> [!NOTE]
> Kullanıma hazır görevlerin tam ayrıntıları için bkz. [MSBuild görev başvurusu](https://msdn.microsoft.com/library/7z253716.aspx). Kendi özel görevlerinizi oluşturma da dahil olmak üzere görevler hakkında daha fazla bilgi için bkz. [MSBuild Tasks](https://msdn.microsoft.com/library/ms171466.aspx).

Görevler her zaman [hedef](https://msdn.microsoft.com/library/t50z2hka.aspx) öğeler içinde bulunmalıdır. **Hedef** öğe, sırayla yürütülen bir veya daha fazla görev kümesidir ve bir proje dosyası birden fazla hedef içerebilir. Bir görevi veya bir dizi görevi çalıştırmak istediğinizde, bunları içeren hedefi çağırılır. Örneğin, bir iletiyi günlüğe kaydeden basit bir proje dosyanız olduğunu varsayalım.

[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]

Hedefi belirtmek için **/t** anahtarını kullanarak komut satırından hedefi çağırabilirsiniz.

[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]

Alternatif olarak, çağırmak istediğiniz hedefleri belirtmek için **Proje** öğesine **DefaultTargets** özniteliği ekleyebilirsiniz.

[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]

Bu durumda, hedefi komut satırından belirtmeniz gerekmez. Yalnızca proje dosyasını belirtebilirsiniz ve MSBuild, sizin için **Fullpublish** hedefini çağırır.

[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]

Hem hedefler hem de görevler, **koşul** özniteliklerini içerebilir. Bu nedenle, belirli koşullar karşılanıyorsa tüm hedefleri veya ayrı görevleri atlayabilirsiniz.

Genel olarak, faydalı görevler ve hedefler oluşturduğunuzda, proje dosyasında başka bir yerde tanımladığınız özelliklere ve öğelere başvurmanız gerekir:

- Bir özellik değeri kullanmak için, **$ (***PropertyName***)** yazın; burada *PropertyName* , **özellik** öğesinin adı veya parametrenin adıdır.
- Bir öğeyi kullanmak için, *ItemName* **öğesi** element öğesinin adı olan **@ (***ItemName***)** yazın.

> [!NOTE]
> Aynı ada sahip birden fazla öğe oluşturursanız, bir liste oluşturduğunuzu unutmayın. Buna karşılık, aynı ada sahip birden fazla özellik oluşturursanız, sağladığınız son özellik değeri, aynı ada&#x2014;sahip önceki tüm özelliklerin üzerine yazılır ve bir özellik yalnızca tek bir değer içerebilir.

Örneğin, örnek çözümde *Publish. proj* dosyasında, **buildprojects** hedefine göz atın.

[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]

Bu örnekte, şu anahtar noktalarını gözlemleyebilirsiniz:

- **Buildinginteambuild** parametresi belirtilmişse ve değeri **true**ise, bu hedef içindeki görevlerden hiçbiri yürütülmez.
- Hedef, [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) görevinin tek bir örneğini içerir. Bu görev, diğer MSBuild projelerini oluşturmanızı sağlar.
- **ProjectsToBuild** öğesi göreve geçirilir. Bu öğe, bir öğe grubu içindeki **ProjectsToBuild** öğe öğeleri tarafından tanımlanan proje veya çözüm dosyalarının bir listesini temsil eder. Bu durumda, **ProjectsToBuild** öğesi tek bir çözüm dosyasına başvurur.

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- **MSBuild** görevine geçirilen özellik değerleri **Outputroot** ve **Configuration**adlı parametreler içerir. Bunlar, sağlandıklarında parametre değerlerine veya yoksa statik özellik değerlerine ayarlanır.

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

**MSBuild** görevinin **derleme**adlı hedefi çağırdığını da görebilirsiniz. Bu, Visual Studio proje dosyalarında yaygın olarak kullanılan ve **derleme**, **Temizleme**, **yeniden oluşturma**ve **Yayımlama**gibi özel proje dosyalarınızda kullanabileceğiniz çeşitli yerleşik hedeflerden biridir. Oluşturma işlemini denetlemek için hedefleri ve görevleri kullanma hakkında daha fazla bilgi edineceksiniz ve bu konunun ilerleyen kısımlarında bulunan **MSBuild** göreviyle ilgili olarak.

> [!NOTE]
> Hedefler hakkında daha fazla bilgi için bkz. [MSBuild hedefleri](https://msdn.microsoft.com/library/ms171462.aspx).

## <a name="splitting-project-files-to-support-multiple-environments"></a>Birden çok ortamı desteklemek için proje dosyalarını bölme

Test sunucuları, hazırlama platformları ve üretim ortamları gibi birden çok ortama bir çözüm dağıtabilmek istediğinizi varsayalım. Bu ortamlar sunucu adı, bağlantı dizeleri,&#x2014;vb. açısından değil, büyük olasılıkla kimlik bilgileri, güvenlik ayarları ve diğer birçok faktörde olmak üzere bu ortamlar arasında önemli ölçüde farklılık gösterebilir. Bunu düzenli olarak yapmanız gerekiyorsa, hedef ortamı her değiştirdiğinizde proje dosyanızdaki birden çok özelliği düzenlemek gerçekten gerekli değildir. Ayrıca, yapı işlemine sağlanması gereken özellik değerlerinin sonsuz bir listesini gerektiren ideal bir çözümdür.

Neyse ki bir alternatif vardır. MSBuild, Yapı yapılandırmanızı birden çok proje dosyası arasında bölmenizi sağlar. Bunun nasıl çalıştığını görmek için, örnek çözümde, iki özel proje dosyası olduğuna dikkat edin:

- Tüm ortamlarda ortak olan özellikleri, öğeleri ve hedefleri içeren *Publish. proj*.
- Bir geliştirici ortamına özel özellikler içeren *env-dev. proj*.

Şimdi *Publish. proj* dosyasının açılış **projesi** etiketinin hemen altındaki bir [içeri aktarma](https://msdn.microsoft.com/library/92x05xfs.aspx) öğesi içerdiğine dikkat edin.

[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]

**Içeri aktarma** öğesi, başka bir MSBuild proje dosyasının Içeriğini geçerli MSBuild proje dosyasına aktarmak için kullanılır. Bu durumda, **Targetenvpropsfile** parametresi, içe aktarmak istediğiniz proje dosyasının dosya adını sağlar. MSBuild çalıştırdığınızda bu parametre için bir değer sağlayabilirsiniz.

[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]

Bu, iki dosyanın içeriğini tek bir proje dosyasında etkin bir şekilde birleştirir. Bu yaklaşımı kullanarak, evrensel Yapı yapılandırmanızı içeren bir proje dosyası ve ortama özgü özellikler içeren birden fazla tamamlayıcı proje dosyası oluşturabilirsiniz. Sonuç olarak, bir komutu farklı bir parametre değeriyle çalıştırmak, çözümünüzü farklı bir ortama dağıtmanızı sağlar.

![](understanding-the-project-file/_static/image3.png)

Proje dosyalarınızı bu şekilde bölmek, izlenmesi iyi bir uygulamadır. Geliştiricilerin tek bir komut çalıştırarak birden çok ortama dağıtmasını sağlar, ancak evrensel derleme özelliklerinin birden çok proje dosyası arasında çoğaltılmasını önler.

> [!NOTE]
> Kendi sunucu ortamlarınız için ortama özgü proje dosyalarını özelleştirmeye ilişkin yönergeler için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

## <a name="conclusion"></a>Sonuç

Bu konu, MSBuild proje dosyalarına genel bir giriş sağlamıştır ve derleme işlemini denetlemek için kendi özel proje dosyalarınızı nasıl oluşturabileceğiniz açıklanmıştır. Ayrıca, birden çok hedefe proje oluşturmayı ve dağıtmayı kolaylaştırmak için proje dosyalarını evrensel derleme yönergelerine ve ortama özgü derleme özelliklerine bölme kavramı de tanıtılmıştır.

Sonraki konu, [Yapı sürecini anlamak](understanding-the-build-process.md)için, gerçekçi bir karmaşıklık düzeyine sahip bir çözüm dağıtımı boyunca sizi yürüyerek derleme ve dağıtımı denetlemek için proje dosyalarını nasıl kullanabileceğiniz hakkında daha fazla öngörü sağlar.

## <a name="further-reading"></a>Daha Fazla Bilgi

Proje dosyalarına ve WPP 'ye yönelik daha ayrıntılı bir giriş için, bkz. [Microsoft Build Engine Içindeki MSBuild ve Team Foundation Build](http://amzn.com/0735645248) , Sayed Ibrampahashler ve William BARTHOLOMEW, ısbn: 978-0-7356-4524-0.

> [!div class="step-by-step"]
> [Önceki](setting-up-the-contact-manager-solution.md)
> [İleri](understanding-the-build-process.md)
