---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
title: Hangi dosyaların dağıtılması gerektiğini belirleme (C#) | Microsoft Docs
author: rick-anderson
description: Geliştirme ortamından üretim ortamına dağıtılması gereken dosyalar, ASP.NET uygulamasının ABD tarafından oluşturulup oluşturulmayacağı bölümüne bağlıdır...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: f8d78a88-cc91-40d8-bce3-3d7954f6033b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-cs
msc.type: authoredcontent
ms.openlocfilehash: 1dd4a1179d32f776626c08a07205dc9aabed588d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596367"
---
# <a name="determining-what-files-need-to-be-deployed-c"></a>Hangi Dosyaların Dağıtılması Gerektiğini Belirleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_cs.pdf)

> Geliştirme ortamından üretim ortamına dağıtılması gereken dosyalar, ASP.NET uygulamasının Web sitesi modeli veya Web uygulaması modeli kullanılarak oluşturulup oluşturulmayacağı bölümüne bağlıdır. Bu iki proje modeli ve proje modelinin dağıtımı nasıl etkilediği hakkında daha fazla bilgi edinin.

## <a name="introduction"></a>Giriş

Bir ASP.NET Web uygulaması dağıtmak, ASP.NET ile ilgili dosyaları geliştirme ortamından üretim ortamına kopyalamayı gerektirir. ASP.NET ile ilgili dosyalar ASP.NET Web sayfası işaretleme ve kod ve istemci ve sunucu tarafı destek dosyalarını içerir. İstemci tarafı destek dosyaları, Web sayfalarınız tarafından başvurulan dosyalardır ve örneğin doğrudan tarayıcı-görüntüler, CSS dosyaları ve JavaScript dosyalarına gönderilir. Sunucu tarafı destek dosyaları, sunucu tarafında bir isteği işlemek için kullanılan işlemleri içerir. Bu yapılandırma dosyalarını, Web hizmetlerini, sınıf dosyalarını, yazılan veri kümelerini ve LINQ to SQL dosyaları içerir.

Genel olarak, tüm istemci tarafı destek dosyaları geliştirme ortamından üretim ortamına kopyalanmalıdır, ancak hangi sunucu tarafı destek dosyalarının kopyalanacağı, sunucu tarafı kodu bir derlemeye (bir `.dll` dosyası) açık olarak derlemenizin veya bu derlemelerin otomatik olarak oluşturulup oluşturulmadığınıza bağlıdır. Bu öğreticide, kodu bir derlemeye açıkça derlerken hangi dosyaların dağıtılması gerektiği vurgulanmıştır ve bu derleme adımı otomatik olarak gerçekleştirilir.

## <a name="explicit-compilation-versus-automatic-compilation"></a>Açık derleme ve otomatik derleme karşılaştırması

ASP.NET Web sayfaları, bildirime dayalı biçimlendirme ve kaynak koduna bölünmüştür. Bildirime dayalı biçimlendirme bölümü HTML, Web denetimleri ve veri bağlama söz dizimini içerir; kod bölümü Visual Basic veya C# kodda yazılan olay işleyicilerini içerir. Biçimlendirme ve kod bölümleri genellikle farklı dosyalara ayrılmıştır: `WebPage.aspx` kodun barındırıldığı `WebPage.aspx.cs`, bildirime dayalı biçimlendirme içerir.

Metin özelliği, sayfanın yüklendiği geçerli tarih ve saate ayarlanmış bir etiket denetimi içeren Clock. aspx adlı bir ASP.NET sayfasını göz önünde bulundurun. Bildirim temelli biçimlendirme bölümü (`Clock.aspx`), bir etiket Web denetimi-`<asp:Label runat="server" id="TimeLabel" />`-, ancak kod bölümü (`Clock.aspx.cs`) aşağıdaki kodla bir `Page_Load` olay işleyicisine sahip olacaktır:

[!code-csharp[Main](determining-what-files-need-to-be-deployed-cs/samples/sample1.cs)]

ASP.NET altyapısının bu sayfaya yönelik bir isteğe hizmet vermek için, önce sayfanın kod bölümü (`WebPage.aspx.cs` dosyası) derlenmesi gerekir. Bu derleme açık bir şekilde veya otomatik olarak gerçekleşebilir.

Derleme açık bir şekilde gerçekleşirse, uygulamanın kaynak kodu, uygulamanın `Bin` dizininde bulunan bir veya daha fazla derlemeye (`.dll` dosya) derlenir. Derleme otomatik olarak gerçekleşirse, elde edilen otomatik oluşturulan derleme, varsayılan olarak, `%WINDOWS%\Microsoft.NET\Framework\` *&lt;sürümü&gt;* bulunan `Temporary ASP.NET` Files klasörüne yerleştirilir, ancak bu konum`<compilation>` `Web.config`[öğesi](https://msdn.microsoft.com/library/s10awwz0.aspx) aracılığıyla yapılandırılabilir. Açık derleme ile ASP.NET uygulamasının kodunu bir derlemeye derlemek için bazı eylemler gerçekleştirmeniz ve bu adım dağıtımdan önce oluşur. Otomatik derleme ile, kaynak ilk kez erişildiğinde derleme işlemi Web sunucusunda gerçekleşir.

Kullandığınız derleme modelinden bağımsız olarak, tüm ASP.NET sayfalarının (`WebPage.aspx` dosyaları) biçimlendirme bölümünün üretim ortamına kopyalanması gerekir. Açık derleme ile `Bin` klasöründeki derlemeleri kopyalamanız gerekir, ancak ASP.NET Pages ' Code kısımlarını (`WebPage.aspx.cs` dosyaları) kopyalamanız gerekmez. Otomatik derleme ile kod bölüm dosyalarını kopyalamanız gerekir, böylece kod mevcut olur ve sayfa ziyaret edildiğinde otomatik olarak derlenebilir. Her bir ASP.NET Web sayfasının biçimlendirme bölümü, sayfanın ilişkili kodunun zaten açıkça derlendiğini veya otomatik olarak derlenmesi gerekip gerekmediğini belirten özniteliklere sahip `@Page` yönergesini içerir. Sonuç olarak, üretim ortamı derleme modeliyle sorunsuz çalışabilir ve açık ya da otomatik derlemenin kullanıldığını belirtmek için özel yapılandırma ayarları uygulamanız gerekmez.

Tablo 1, açık derleme kullanılırken otomatik derlemeye karşı dağıtılacak farklı dosyaları özetler. Kullanılan derleme modelinden bağımsız olarak, bu klasör varsa `Bin` klasöründeki derlemeleri her zaman dağıtmanız gerektiğini unutmayın. `Bin` klasörü, açık derleme modeli kullanılırken derlenen kaynak kodu içeren Web uygulamasına özgü derlemeleri içerir. `Bin` Dizin, diğer projelerden ve kullanmakta olduğunuz açık kaynaklı ya da üçüncü taraf derlemelerden derlemeler içerir ve bunların üretim sunucusunda olması gerekir. Bu nedenle, bir Thumb genel kuralı olarak, `Bin` klasörünü dağıtma sırasında üretime kopyalayın. (Otomatik derleme modeli kullanıyorsanız ve herhangi bir dış derlemeyi kullanmıyorsanız, `Bin` dizininiz yoktur!)

| **Derleme modeli** | **Biçimlendirme bölümü dosyası dağıtılsın mı?** | **Kaynak kodu dosyası dağıtılsın mı?** | **Derlemeler `Bin` dizinde dağıtılsın mı?** |
| --- | --- | --- | --- |
| Açık derleme | Evet | Hayır | Evet |
| Otomatik derleme | Evet | Evet | Evet (varsa) |

**Tablo 1:** Dağıttığınız dosyalar kullanılan derleme modeline bağlıdır.

## <a name="taking-a-trip-down-memory-lane"></a>Bellek yoluna seyahat alma

Hangi derleme yaklaşımının kullanıldığı, kısmen, ASP.NET uygulamasının Visual Studio 'da nasıl yönetildiği konusuna bağlıdır. Getirildikten. NET ' in 2000 yılında, Visual Studio 'nun dört farklı sürümü (Visual Studio .NET 2002, Visual Studio .NET 2003, Visual Studio 2005 ve Visual Studio 2008) vardır. *Web uygulaması proje modelini*kullanarak Visual Studio .NET 2002 ve 2003 yönetilen ASP.NET uygulamaları. Web uygulaması proje modelinin temel özellikleri şunlardır:

- Projeyi oluşturan dosyalar tek bir proje dosyasında tanımlanır. Proje dosyasında tanımlı olmayan dosyalar, Visual Studio tarafından Web uygulamasının bir parçası olarak kabul edilmez.
- Açık derlemeyi kullanır. Projeyi oluşturmak, proje içindeki kod dosyalarını `Bin` klasörüne yerleştirilmiş tek bir derlemede derler.

Microsoft, Visual Studio 2005 ' i kullanıma sunduklarında, Web uygulaması proje modeli için destek bıraktı ve onu Web sitesi proje modeliyle değiştirdi. Web sitesi proje modeli, Web uygulaması proje modelinden kendisini aşağıdaki yollarla ayırt ediyor:

- Projenin dosyalarını içeren tek bir proje dosyası olması yerine, bunun yerine dosya sistemi kullanılır. Kısacası, Web uygulaması klasörü (veya alt klasörleri) içindeki herhangi bir dosya projenin bir parçası olarak kabul edilir.
- Visual Studio 'da bir proje oluşturmak `Bin` dizininde bütünleştirilmiş kod oluşturmaz. Bunun yerine, bir Web sitesi projesi oluşturma, derleme zamanı hatalarını bildirir.
- Otomatik derleme desteği. Web sitesi projeleri genellikle, biçimlendirme ve kaynak kodu üretim ortamına kopyalanarak dağıtılır, ancak kodun ön derlenmiş olmasına (açık derleme) olanak sağlar.

Microsoft, Visual Studio 2005 Service Pack 1 ' i kullanıma sunduktan sonra Web uygulaması proje modelini yeniden canlandırmış. Ancak, Visual Web Developer yalnızca Web sitesi proje modelini desteklemeye devam eder. İyi haber, bu sınırlamanın Visual Web Developer 2008 Service Pack 1 ile bırakılmasıdır. Bugün, Web uygulaması proje modeli veya Web sitesi proje modelini kullanarak Visual Studio 'da (ve Visual Web Developer) ASP.NET uygulamaları oluşturabilirsiniz. Her iki modelde de profesyonelleri ve olumsuz yönleri vardır. [Web uygulaması projelerine giriş: Web sitesi projelerini ve Web uygulaması projelerini](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5) iki modelin karşılaştırması için karşılaştırma ve hangi proje modelinin durumunuz için en uygun olduğuna karar vermeye yardımcı olma.

## <a name="exploring-the-sample-web-application"></a>Örnek Web uygulamasını keşfetme

Bu öğreticiye yönelik indirme, kitap Incelemeleri adlı bir ASP.NET uygulaması içerir. Web sitesi, bir kişinin, kitap incelemelerini çevrimiçi topluluk ile paylaşmak için oluşturacağı bir hobweb sitesini taklit edebilir. Bu ASP.NET Web uygulaması çok basittir ve aşağıdaki kaynaklardan oluşur:

- `Web.config`, uygulamanın yapılandırma dosyası.
- Ana sayfa (`Site.master`).
- Yedi farklı ASP.NET sayfası: 

    - ~`/Default.aspx`-sitenin giriş sayfası.
    - ~`/About.aspx`-"site hakkında" sayfası.
    - ~`/Fiction/Default.aspx`-gözden geçirilen kurgu kitaplarının listelendiği bir sayfa. 

        - ~`/Fiction/Blaze.aspx`-Richard Bachman Nolik *güçlendirme*için gözden geçirin.
    - ~/`Tech/Default.aspx`-gözden geçirilmiş teknoloji defterlerini listelemesi için bir sayfa. 

        - ~/`Tech/CYOW.aspx`- *kendi web sitenizi oluşturma*konusunu gözden geçirin.
        - ~/`Tech/TYASP35.aspx`- *24 saat Içinde kendinize ASP.NET 3,5 eğitim*konusunu gözden geçirin.
- Stiller klasöründe üç farklı CSS dosyası.
- Dört görüntü dosyası-bir ASP.NET logosu ve `Images` klasöründe bulunan üç gözden geçirilmiş defterin kapakları görüntülerinin görüntüleri.
- Site haritasını tanımlayan ve bir `Web.sitemap` dosyası, bu dosya, kök dizin ve `Fiction` ve `Tech` klasörlerinin `Default.aspx` sayfalarında menüleri göstermek için kullanılır.
- Temel bir `Page` sınıfını tanımlayan `BasePage.cs` adlı bir sınıf dosyası. Bu sınıf, `Title` özelliğini sayfanın site eşlemesindeki konumuna göre otomatik olarak ayarlayarak `Page` sınıfının işlevselliğini genişletir. Bir Nutshell 'de, `BasePage` genişleten tüm ASP.NET arka plan kod (`System.Web.UI.Page`) sınıfının başlığı, site eşlemesindeki konumuna bağlı olarak bir değere ayarlanır. Örneğin, ~/`Tech/CYOW.aspx` sayfasını görüntülerken, başlık "Home: Technology: kendi web sitenizi oluşturma" olarak ayarlanır.

Şekil 1 ' de bir tarayıcıdan görüntülendiklerinde kitap Incelemeleri Web sitesinin ekran görüntüsü gösterilmektedir. Burada, kitabın *ASP.NET 3,5 ' u 24 saat Içinde öğretmeyi*inceleyen ~/`Tech/TYASP35.aspx`sayfasını görürsünüz. Sayfanın üst kısmına yayılan içerik haritası ve sol sütundaki menü, `Web.sitemap`tanımlanan site haritası yapısını temel alır. Sağ üst köşedeki görüntü, `Images` klasöründe bulunan kitap kapak görüntülerinden biridir. Web sitesinin görünümü, stil klasöründeki CSS dosyaları tarafından yazılmış geçişli stil sayfası kuralları aracılığıyla tanımlanır, ancak `Site.master`, ana sayfada fazla kullanılabilir sayfa düzeni tanımlanmıştır.

[Book Incelemeleri Web sitesinin bir başlık hakkında incelemeler sağladığı ![](determining-what-files-need-to-be-deployed-cs/_static/image2.png)](determining-what-files-need-to-be-deployed-cs/_static/image1.png)

**Şekil 1:** Book Incelemeleri Web sitesi, bir dizi başlığa ilişkin incelemeler sunar ([tam boyutlu görüntüyü görüntülemek Için tıklayın](determining-what-files-need-to-be-deployed-cs/_static/image3.png))

Bu uygulama bir veritabanı kullanmaz; her İnceleme, uygulamada ayrı bir Web sayfası olarak uygulanır. Bu öğretici (ve sonraki birkaç öğretici), veritabanı olmayan bir Web uygulamasını dağıtmaya kılavuzluk yapar. Bununla birlikte, gelecekteki bir öğreticide incelemeleri, okuyucu açıklamalarını ve diğer bilgileri bir veritabanı içinde depolamak için bu uygulamayı geliştireceğiz ve veri odaklı bir Web uygulamasını doğru şekilde dağıtmak için hangi adımların gerçekleştirilmesi gerektiğini keşfedecektir.

> [!NOTE]
> Bu öğreticiler, Web ana bilgisayar sağlayıcısıyla ASP.NET uygulamalarını barındırmak ve ASP gibi yardımcı konuları araştırmaya odaklanmaktadır. NET 'in site eşleme sistemi veya temel bir `Page` sınıfı kullanma. Bu teknolojiler hakkında daha fazla bilgi edinmek ve öğreticide ele alınan diğer konularda daha fazla arka plan için, her öğreticinin sonunda daha fazla okuma bölümüne bakın.

Bu öğreticinin indirilmesi, her biri farklı bir Visual Studio proje türü olarak uygulanan Web uygulamasının iki kopyasına sahiptir: Bookbelgele değiştirme, bir Web uygulaması projesi ve kitap, bir Web sitesi projesi. Her iki proje de Visual Web Developer 2008 SP1 ile oluşturulmuştur ve ASP.NET 3,5 SP1 kullanın. Bu projelerle çalışmak için içeriği masaüstünüze göndererek başlayın. Web uygulaması projesini (Bookgözden geçirmeyi değiştirme) açmak için, Bookgözden değiştirme klasörüne gidin ve `BookReviewsWAP.sln`çözüm dosyasına çift tıklayın. Web sitesi projesini (Bookgözden geçirme \ SP) açmak için, Visual Studio 'Yu başlatın ve ardından Dosya menüsünden Web sitesi aç seçeneğini belirleyin, masaüstünüzdeki `BookReviewsWSP` klasöre gidin ve Tamam ' a tıklayın.

Bu öğreticideki kalan iki bölüm, uygulamayı dağıttığınızda üretim ortamına kopyalamak için gereken dosyaları arar. Sonraki iki öğretici- *[SITENIZI FTP kullanarak dağıtma](deploying-your-site-using-an-ftp-client-cs.md)* ve *[sitenizi Visual Studio kullanarak dağıtma](deploying-your-site-using-visual-studio-cs.md)* -bu dosyaları bir Web ana bilgisayar sağlayıcısına kopyalamak için farklı yollar gösterir.

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>Web uygulaması projesi için dağıtılacak dosyaları belirleme

Web uygulaması proje modeli açık derlemeyi kullanır; projenin kaynak kodu, uygulamayı her oluşturduğunuzda tek bir derlemede derlenir. Bu derleme, ASP.NET Pages 'in arka plan kod dosyalarını (~/`Default.aspx.cs`, ~/`About.aspx.cs`vb.) ve `BasePage.cs` sınıfını içerir. Elde edilen derleme Book, swap. dll olarak adlandırılır ve uygulamanın `Bin` dizininde bulunur.

Şekil 2 ' de, kitap Incelemeleri Web uygulaması projesini oluşturan dosyalar gösterilir.

[Çözüm Gezgini, Web uygulaması projesini oluşturan dosyaları listeler ![](determining-what-files-need-to-be-deployed-cs/_static/image5.png)](determining-what-files-need-to-be-deployed-cs/_static/image4.png)

**Şekil 2**: Çözüm Gezgini Web uygulaması projesini oluşturan dosyaları listeler

Web uygulaması proje modeli kullanılarak geliştirilen bir ASP.NET uygulamasını dağıtmak için, uygulamayı yapılandırarak, en son kaynak kodu bir derlemede açıkça derlemek gibi. Ardından, aşağıdaki dosyaları üretim ortamına kopyalayın:

- Her ASP.NET sayfası için bildirim temelli biçimlendirme içeren dosyalar; örneğin ~/`Default.aspx`, ~/`About.aspx`, vb. Ayrıca, tüm ana sayfalar ve Kullanıcı denetimleri için bildirim temelli biçimlendirmeyi kopyalayın.
- `Bin` klasöründeki derlemeler (`.dll` dosyalar). Program veritabanı dosyalarını (`.pdb`) veya `Bin` dizininde bulabileceğiniz herhangi bir XML dosyasını kopyalamanız gerekmez.

ASP.NET Pages kaynak kodu dosyalarını üretim ortamına kopyalamanız veya `BasePage.cs` sınıf dosyasını kopyalamanız gerekir.

> [!NOTE]
> Şekil 2 ' de gösterildiği gibi, `BasePage` sınıfı projede bir sınıf dosyası olarak uygulanır ve `HelperClasses`adlı klasöre yerleştirilir. Proje derlendiğinde `BasePage.cs` dosyadaki kod, tek derlemede ASP.NET Pages 'in arka plan kod sınıfları ile birlikte derlenir, `BookReviewsWAP.dll.` ASP.NET, Web sitesi projeleri için sınıf dosyalarını tutmak üzere tasarlanan `App_Code` adlı özel bir klasöre sahiptir. `App_Code` klasöründeki kod otomatik olarak derlenir ve bu nedenle Web uygulaması projeleriyle kullanılmamalıdır. Bunun yerine, uygulamanızın sınıf dosyalarını `HelperClasses`veya `Classes`ya da benzer bir şekilde adlandırılan normal bir klasöre yerleştirmeniz gerekir. Alternatif olarak, sınıf dosyalarını ayrı bir sınıf kitaplığı projesine yerleştirebilirsiniz.

ASP.NET ile ilgili biçimlendirme dosyalarını ve derlemeyi `Bin` klasöre kopyalamanın yanı sıra, Ayrıca, istemci tarafı destek dosyalarını (görüntüler ve CSS dosyaları) ve diğer sunucu tarafı destek dosyalarını, `Web.config` ve `Web.sitemap`kopyalamanız gerekir. Bu istemci ve sunucu tarafı destek dosyalarının, açık veya otomatik derleme kullanıp kullanmadığına bakılmaksızın üretim ortamına kopyalanması gerekir.

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>Web sitesi proje dosyaları için dağıtılacak dosyaları belirleme

Web sitesi proje modeli, Web uygulaması proje modeli kullanılırken kullanılamayan bir özellik olan otomatik derlemeyi destekler. Açık derleme ile projenizin kaynak kodunu bir derlemede derleyip bu derlemeyi üretim ortamına kopyalamanız gerekir. Diğer taraftan, otomatik derleme ile kaynak kodu üretim ortamına kopyalamanız yeterlidir ve gerektiğinde çalışma zamanı tarafından derlenir.

Visual Studio 'daki derleme menü seçeneği hem Web uygulaması projelerinde hem de Web sitesi projelerinde bulunur. Web uygulaması projeleri oluşturmak, projenin kaynak kodunu `Bin` dizininde bulunan tek bir derlemede derler; bir Web sitesi projesi oluşturma, derleme zamanı hataları olup olmadığını denetler, ancak hiçbir derleme oluşturmaz. Web sitesi proje modeli kullanılarak geliştirilen bir ASP.NET uygulamasını dağıtmak için tüm yapmanız gereken, uygun dosyaları üretim ortamına kopyalamam, ancak derleme zamanı hataları bulunmadığından emin olmak için projeyi derlemeyi öneririz.

Şekil 3 ' te, Book Incelemeleri Web sitesi projesini oluşturan dosyalar gösterilir.

 [Çözüm Gezgini ![Web sitesi projesini oluşturan dosyaları listeler](determining-what-files-need-to-be-deployed-cs/_static/image7.png)](determining-what-files-need-to-be-deployed-cs/_static/image6.png) 

**Şekil 3**: Çözüm Gezgini Web sitesi projesini oluşturan dosyaları listeler

Bir Web sitesi projesini dağıtmak, ASP.NET ile ilgili tüm dosyaları üretim ortamına kopyalamayı içerir. Bu, kod dosyalarıyla birlikte ASP.NET sayfaları, ana sayfalar ve Kullanıcı denetimleri için biçimlendirme sayfaları içerir. Ayrıca, BasePage.cs gibi herhangi bir sınıf dosyasını kopyalamanız gerekir. `BasePage.cs` dosyasının, sınıf dosyaları için Web sitesi projelerinde kullanılan özel bir ASP.NET klasörü olan `App_Code` klasöründe bulunduğunu unutmayın. Özel klasörün Üretimde oluşturulması gerekir, geliştirme ortamındaki `App_Code` klasöründeki sınıf dosyaları da üretimde `App_Code` klasörüne kopyalanmalıdır.

ASP.NET işaretleme ve kaynak kodu dosyalarını kopyalamaya ek olarak, Ayrıca, istemci tarafı destek dosyalarını (görüntüler ve CSS dosyaları) ve diğer sunucu tarafı destek dosyalarını, `Web.config` ve `Web.sitemap`kopyalamanız gerekir.

> [!NOTE]
> Web sitesi projeleri açık derlemeyi de kullanabilir. Gelecekteki bir öğretici, bir Web sitesi projesini açık olarak derlemeyi inceler.

## <a name="summary"></a>Özet

Bir ASP.NET uygulamasının dağıtımı, gerekli dosyaları geliştirme ortamından üretim ortamına kopyalamayı gerektirir. Eşitlenmesi gereken tam dosya kümesi, ASP.NET uygulamasının kodunun açıkça mi yoksa otomatik olarak mı derlendiğine bağlıdır. Çalışan derleme stratejisi, Visual Studio 'Nun Web uygulaması proje modeli veya Web sitesi proje modeli kullanılarak ASP.NET uygulamasını yönetmek üzere yapılandırılıp yapılandırılmadığını etkileyenden etkilenir.

Web uygulaması proje modeli açık derlemeyi kullanır ve projenin kodunu `Bin` klasöründeki tek bir derlemede derler. Uygulamayı dağıttığınızda, ASP.NET sayfalarının biçimlendirme bölümü ve `Bin` klasörünün içeriği üretim ortamına itilmiş olmalıdır; uygulamadaki kaynak kodu-kod dosyaları ve arka plan kod sınıfları, örneğin, üretim ortamına kopyalanmaları gerekmez.

Web sitesi proje modeli varsayılan olarak otomatik derleme kullanır, ancak sonraki öğreticilerde göreceğiniz gibi bir Web sitesi projesini açıkça derlemek mümkün olsa da. Otomatik derleme kullanan bir ASP.NET uygulamasını dağıtmak için, işaretleme bölümünün *ve* kaynak kodunun üretim ortamına kopyalanması gerekir. Kod, ilk kez istendiğinde üretim ortamında otomatik olarak derlenir.

Geliştirme ve üretim ortamları arasında hangi dosyaların eşitlenmesi gerektiğini incelediğimiz için, kitap Incelemeleri uygulamasını bir Web ana sağlayıcısına dağıtmaya hazır olduğumuz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET derlemesine genel bakış](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET Kullanıcı denetimleri](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [ASP 'yi İnceleme. NET 'in site gezintisi](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Web uygulaması projelerine giriş](https://msdn.microsoft.com/library/aa730880.aspx)
- [Ana sayfa öğreticileri](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [Sayfalar arasında kod paylaşma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [ASP.NET sayfalarınızın arka plan kod sınıfları Için özel bir temel sınıf kullanma](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005 Web sitesi proje sistemi: nedir ve neden bunu yaptık?](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [İzlenecek yol: bir Web sitesi projesini Visual Studio 'da bir Web uygulaması projesine dönüştürme](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [Önceki](asp-net-hosting-options-cs.md)
> [İleri](deploying-your-site-using-an-ftp-client-cs.md)
