---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: ASP.NET AJAX hata ayıklama yeteneklerini anlama | Microsoft Docs
author: scottcate
description: Kod hatalarını ayıklama özelliği, her geliştiricinin kullandıkları teknolojiden bağımsız olarak kendi Arsenal 'da sahip olması gereken bir yetencdır. Birçok geliştirici...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 08ced380f3551407d757524dbc84b5feeeb5482b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601431"
---
# <a name="understanding-aspnet-ajax-debugging-capabilities"></a>ASP.NET AJAX Hata Ayıklama Özelliklerini Anlama

[Scott](https://github.com/scottcate) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> Kod hatalarını ayıklama özelliği, her geliştiricinin kullandıkları teknolojiden bağımsız olarak kendi Arsenal 'da sahip olması gereken bir yetencdır. Birçok geliştirici, VB.NET veya C# kod kullanan ASP.NET uygulamalarında hata ayıklamak Için Visual Studio .NET veya web geliştirici Express kullanmaya alışkın olsa da, bazıları JavaScript gibi istemci tarafı kodda hata ayıklama için son derece yararlı olduğunu bilmez. .NET uygulamalarında hata ayıklamak için kullanılan aynı tekniklerin türü, AJAX etkinleştirilmiş uygulamalara ve daha özel ASP.NET AJAX uygulamalarına da uygulanabilir.

## <a name="debugging-aspnet-ajax-applications"></a>ASP.NET AJAX uygulamalarında hata ayıklama

Dan Wahlin

Kod hatalarını ayıklama özelliği, her geliştiricinin kullandıkları teknolojiden bağımsız olarak kendi Arsenal 'da sahip olması gereken bir yetencdır. Kullanılabilir farklı hata ayıklama seçeneklerinin anlaşılmasına gerek kalmadan, bir projeye çok fazla miktarda zaman kazandırabilir ve belki de birkaç kez daha olabilir. Birçok geliştirici, VB.NET veya C# kod kullanan ASP.NET uygulamalarında hata ayıklamak Için Visual Studio .NET veya web geliştirici Express kullanmaya alışkın olsa da, bazıları JavaScript gibi istemci tarafı kodda hata ayıklama için son derece yararlı olduğunu bilmez. .NET uygulamalarında hata ayıklamak için kullanılan aynı tekniklerin türü, AJAX etkinleştirilmiş uygulamalara ve daha özel ASP.NET AJAX uygulamalarına da uygulanabilir.

Bu makalede, hataları ve diğer sorunları hızlı bir şekilde bulmak için Visual Studio 2008 ve diğer birçok araçların ASP.NET AJAX uygulamalarında hata ayıklamak için nasıl kullanılabileceğini görürsünüz. Bu tartışma, hata ayıklama için Internet Explorer 6 veya üstünü etkinleştirme, Visual Studio 2008 ve betik Gezgini kullanılarak Web geliştirme Yardımcısı gibi diğer ücretsiz araçların kullanılması hakkında bilgiler içerir. Ayrıca, diğer herhangi bir araç olmadan doğrudan tarayıcıda JavaScript kodunu adım adım gerçekleştirmenizi sağlayan Firebug adlı bir uzantıyı kullanarak Firefox 'ta ASP.NET AJAX uygulamalarında hata ayıklamayı öğreneceksiniz. Son olarak, izleme ve kod onaylama deyimleri gibi çeşitli hata ayıklama görevlerinde yardımcı olabilecek ASP.NET AJAX kitaplığındaki sınıflara tanıtılcaksınız.

Internet Explorer 'da görüntülenen sayfalarda hata ayıklamayı denemeden önce, hata ayıklama için etkinleştirmek üzere yapmanız gereken birkaç temel adım vardır. Çalışmaya başlamak için gerçekleştirilmesi gereken bazı temel kurulum gereksinimlerine göz atalım.

## <a name="configuring-internet-explorer-for-debugging"></a>Internet Explorer 'ı hata ayıklama için yapılandırma

Çoğu kişi, Internet Explorer ile görüntülenen bir Web sitesinde karşılaşılan JavaScript sorunlarını görmekten ilgilenmiyor. Aslında, ortalama kullanıcı bir hata mesajı gördük ne yapmanız gerektiğini de bilmez. Sonuç olarak, hata ayıklama seçenekleri tarayıcıda varsayılan olarak kapalıdır. Ancak, hata ayıklamayı açmak ve yeni AJAX uygulamaları geliştirdikçe kullanmak için koymak çok basittir.

Hata ayıklama işlevselliğini etkinleştirmek için Internet Explorer menüsündeki Araçlar Internet Seçenekleri ' ne gidin ve Gelişmiş sekmesini seçin. Göz atma bölümü içinde, aşağıdaki öğelerin işaretinin kaldırıldığından emin olun:

- Betik hata ayıklamayı devre dışı bırak (Internet Explorer)
- Betik hata ayıklamayı devre dışı bırak (diğer)

Gerekli olmamasına rağmen, bir uygulamada hata ayıklamaya çalışıyorsanız, sayfada tüm JavaScript hatalarının hemen görünür ve belirgin olmasını istersiniz. "Her komut dosyası hatası hakkında bir bildirim göster" onay kutusunu işaretleyerek tüm hataları bir ileti kutusuyla gösterilmeye zorlayabilirsiniz. Bir uygulama geliştirirken açık olan harika bir seçenek olsa da, JavaScript hatalarıyla karşılaşma olasılıklarınız oldukça iyi olduğundan, diğer Web sitelerini kullanıyorsanız hızla sinir bozucu hale gelebilir.

Şekil 1 ' de, Internet Explorer Gelişmiş iletişim kutusunun hata ayıklama için düzgün bir şekilde yapılandırıldıktan sonra nasıl görünmesi gerektiğini gösterir.

[hata ayıklama için Internet Explorer 'ı yapılandırma ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**Şekil 1**: Internet Explorer 'ı hata ayıklama için yapılandırma.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png))

Hata ayıklama açıldıktan sonra, komut dosyası hata ayıklayıcısı adlı Görünüm menüsünde Yeni bir menü öğesi görünür. Next Ifadesinde Open ve break dahil olmak üzere iki seçeneği vardır. Açık seçildiğinde, Visual Studio 2008 sayfasında hata ayıklaması yapmanız istenir (Visual Web Developer Express 'in de hata ayıklama için kullanılabileceğini unutmayın). Visual Studio .NET şu anda çalışıyorsa, bu örneği kullanmayı veya yeni bir örnek oluşturmayı tercih edebilirsiniz. Sonraki Ifadede kesme seçildiğinde, JavaScript kodu yürütüldüğünde sayfada hata ayıklaması yapmanız istenir. JavaScript kodu sayfanın onLoad olayında yürütülüyorsa hata ayıklama oturumu tetiklemek için sayfayı yenileyebilirsiniz. Bir düğmeye tıklandıktan sonra JavaScript kodu çalışıyorsa, düğme tıklandığında hata ayıklayıcı hemen çalışacaktır.

> [!NOTE]
> Kullanıcı Access Control (UAC) özellikli Windows Vista 'da çalıştırıyorsanız ve Visual Studio 2008 ' i yönetici olarak çalışacak şekilde ayarlarsanız, iliştirdiğinizde Visual Studio işleme iliştirilemiyor. Bu sorunu geçici olarak çözmek için, önce Visual Studio 'yu başlatın ve bu örneği kullanarak hata ayıklayın.

Sonraki bölümde bir ASP.NET AJAX sayfasında doğrudan Visual Studio 2008 içinden hata ayıklama işlemi gösterilmektedir, ancak bir sayfa zaten açık olduğunda ve daha fazla tam incelemek istediğinizde, Internet Explorer betik hata ayıklayıcısı seçeneğinin kullanılması yararlı olur.

## <a name="debugging-with-visual-studio-2008"></a>Visual Studio 2008 ile hata ayıklama

Visual Studio 2008, dünyanın dört bir yanındaki geliştiricilerin .NET uygulamalarında hata ayıklamak için günlük olarak kullandığı hata ayıklama işlevselliği sağlar. Yerleşik hata ayıklayıcı kod içinde ileretmenize, nesne verilerini görüntülemenize, belirli değişkenleri izlemenize, çağrı yığınını ve çok daha fazlasını izlemenize olanak sağlar. VB.NET veya C# kodun hata ayıklamasına ek olarak, hata AYıKLAYıCı ASP.NET Ajax uygulamalarında hata ayıklamak için de yardımcı olur ve JavaScript kod satırını satıra göre ilerleyerek adım adım sağlar. Aşağıdaki ayrıntılar, Visual Studio 2008 kullanarak uygulamaların hata ayıklamasının genel sürecinde bir Discourse sağlamak yerine, istemci tarafı betik dosyalarında hata ayıklamak için kullanılabilen teknikler üzerinde odaklanmaktadır.

Visual Studio 2008 ' de bir sayfada hata ayıklama işlemi birkaç farklı yolla başlatılabilir. İlk olarak, önceki bölümde bahsedilen Internet Explorer betik hata ayıklayıcı seçeneğini kullanabilirsiniz. Bu, tarayıcıya zaten bir sayfa yüklendiğinde ve bu sayfada hata ayıklamaya başlamak istediğinizde iyi bir şekilde geçerlidir. Alternatif olarak, Çözüm Gezgini bir. aspx sayfasına sağ tıklayıp menüden başlangıç sayfası olarak ayarla ' yı seçebilirsiniz. ASP.NET sayfalarında hata ayıklamaya alışkın değilseniz, büyük olasılıkla bunu daha önce yapmış olursunuz. F5 tuşuna basıldığında sayfada hata ayıklanabilir. Ancak, genellikle VB.NET veya C# Code içinde istediğiniz her yerde bir kesme noktası ayarlayabilmeniz sırasında, daha sonra göreceğiniz şekilde JavaScript 'te her zaman durum değildir.

*Katıştırılmış dış betiklere karşı*

Visual Studio 2008 hata ayıklayıcı, dış JavaScript dosyalarından farklı bir sayfada eklenmiş JavaScript 'e davranır. Dış betik dosyaları ile, dosyayı açabilir ve seçtiğiniz herhangi bir satırda bir kesme noktası ayarlayabilirsiniz. Kesme noktaları, kod Düzenleyicisi penceresinin solundaki gri tepsi alanına tıklanarak ayarlanabilir. JavaScript `<script>` etiketi kullanılarak doğrudan bir sayfaya katıştırıldığında, gri tepsi alanını tıklatmak için bir kesme noktası ayarlamak bir seçenek değildir. Katıştırılmış betiğin bir satırında kesme noktası ayarlamaya çalışır, "Bu bir kesme noktası için geçerli bir konum değildir" durumuna neden olur.

Kodu harici bir. js dosyasına taşıyarak ve &lt;betiği&gt; etiketinin src özniteliğini kullanarak bu sorunu çözebilirsiniz:

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

Kodu harici bir dosyaya taşımak bir seçenek değilse veya bu değerden daha fazla çalışma gerektiriyorsa ne olur? Düzenleyiciyi kullanarak bir kesme noktası ayarlayamıyorum, hata ayıklayıcı ifadesini doğrudan hata ayıklamaya başlamak istediğiniz koda ekleyebilirsiniz. Hata ayıklamayı başlatmak için ASP.NET AJAX kitaplığı 'nda bulunan sys. Debug sınıfını da kullanabilirsiniz. Sys. Debug sınıfı hakkında daha sonra bu makalede daha fazla bilgi edineceksiniz.

`debugger` anahtar sözcüğünü kullanma örneği, liste 1 ' de gösterilmiştir. Bu örnek, bir güncelleştirme işlevine yapılan bir çağrı yapılmadan önce hata ayıklayıcıyı sağa kesmeyi zorlar.

**Listeleme 1. Visual Studio .NET hata ayıklayıcısını kesintiye zorlamak için hata ayıklayıcı anahtar sözcüğü kullanma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

Hata ayıklayıcı ifadesine ulaşıldığında, Visual Studio .NET kullanarak sayfada hata ayıklaması yapmanız istenir ve koddan adımlamayı başlatabilir. Bunu yaparken, sayfada kullanılan ASP.NET AJAX kitaplık betik dosyalarına erişmede bir sorunla karşılaşabilirsiniz. böylece, Visual Studio 'Yu kullanmaya göz atalım. NET 'in betik Gezgini.

## <a name="using-visual-studio-net-windows-to-debug"></a>Hata ayıklamak için Visual Studio .NET Windows kullanma

Bir hata ayıklama oturumu başlatıldıktan ve varsayılan F11 tuşunu kullanarak kodla ilerledikten sonra, sayfada kullanılan tüm betik dosyaları açık ve hata ayıklama için kullanılabilir olmadığı takdirde Şekil 2 ' de gösterilen hata iletişim kutusu ile karşılaşabilirsiniz.

[Hata ayıklama için kullanılabilir kaynak kodu olmadığında gösterilen ![hatası iletişim kutusu.](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**Şekil 2**: hata ayıklama için kullanılabilir kaynak kodu olmadığında gösterilen hata iletişim kutusu.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png))

Visual Studio .NET, sayfanın başvurduğu bazı betiklerin kaynak koduna nasıl ulaşılamadığından emin olmadığı için bu iletişim kutusu gösterilir. Bu, ilk başta oldukça sinir bozucu olabilir, ancak basit bir çözüm vardır. Bir hata ayıklama oturumu başlattığınızda ve bir kesme noktasına vurduktan sonra, Visual Studio 2008 menüsündeki Windows betik Gezgini penceresine Hata Ayıkla veya Ctrl + Alt + N kısayol tuşlarını kullanın.

> [!NOTE]
> Betik Gezgini menüsünü listede göremiyorsanız, Visual Studio .NET menüsündeki **araçlar** >  > komutlarını **Özelleştir** ' e gidin. Kategoriler bölümünde **hata ayıklama** girişini bulun ve tüm kullanılabilir menü girişlerini göstermek için tıklayın. Komutlar listesinde, komut dosyası Gezgini ' ne gidin ve daha önce bahsedilen hata ayıklama pencereleri menüsüne sürükleyin. Bunu yapmak, Visual Studio .NET her çalıştırdığınızda betik Gezgini menü girişini kullanılabilir hale getirir.

Betik Gezgini, bir sayfada kullanılan tüm betikleri görüntülemek ve bunları kod düzenleyicisinde açmak için kullanılabilir. Betik Gezgini açıldıktan sonra, kod Düzenleyicisi penceresinde açmak için şu anda hata ayıklanan. aspx sayfasına çift tıklayın. Betik Gezgini 'nde gösterilen diğer tüm betikler için aynı eylemi gerçekleştirin. Kod penceresinde tüm betikler açık olduktan sonra, kodunuzda ilerlemek için F11 tuşuna basabilir (ve diğer hata ayıklama kısayol tuşlarını kullanabilirsiniz). Şekil 3 ' te betik Gezgini örneği gösterilmektedir. Hata ayıklanan geçerli dosyayı (demo. aspx) ve ASP.NET AJAX ScriptManager tarafından sayfaya dinamik olarak eklenen iki özel betik ve iki komut dosyası listeler.

[Betik Gezgini ![, bir sayfada kullanılan betiklerine kolay erişim sağlar.](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**Şekil 3**. Betik Gezgini, bir sayfada kullanılan betiklerine kolay erişim sağlar.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png))

Bir sayfada kodda adım adım ilerlediğimde yararlı bilgiler sağlamak için diğer birçok Windows da kullanılabilir. Örneğin, sayfada kullanılan farklı değişkenlerin değerlerini görmek için yerel öğeler penceresini, belirli değişkenleri veya koşulları değerlendirmek ve çıktıyı görüntülemek için hemen penceresini kullanabilirsiniz. Çıktı penceresini, sys. Debug. Trace işlevini (Bu makalenin ilerleyen kısımlarında ele alınacaktır) veya Internet Explorer 'ın Debug. writeln işlevini kullanarak yazılan Trace deyimlerini görüntülemek için de kullanabilirsiniz.

Hata ayıklayıcıyı kullanarak kodda adım adım ilerlerse, atandıkları değeri görüntülemek için koddaki değişkenlerin üzerine farenizi de kullanabilirsiniz. Ancak, komut dosyası hata ayıklayıcısı bazen belirli bir JavaScript değişkeninin üzerinde fare gibi hiçbir şey göstermez. Değeri görmek için, kod Düzenleyicisi penceresinde görmeyi denediğiniz ifadeyi veya değişkeni vurgulayın ve sonra fareyi üzerine getirin. Bu teknik her durumda çalışmasa da, birçok kez Yereller penceresi gibi farklı bir hata ayıklama penceresine bakmak zorunda kalmadan değeri görebileceksiniz.

Burada açıklanan özelliklerden bazılarını gösteren bir video öğreticisi [http://www.xmlforasp.net](http://www.xmlforasp.net)' de görüntülenebilir.

## <a name="debugging-with-web-development-helper"></a>Web geliştirme Yardımcısı Ile hata ayıklama

Visual Studio 2008 (ve Visual Web Developer Express 2008) çok özellikli hata ayıklama araçları olmakla birlikte, daha hafif bir şekilde kullanılabilecek ek seçenekler de vardır. Yayımlanacak en son araçlardan biri web geliştirme yardımcısından biridir. Microsoft 'un Nikhil Kothari (Microsoft 'ta anahtar ASP.NET AJAX mimarlarından biri), HTTP isteği ve yanıt iletilerini görüntülemek için basit hata ayıklamadan birçok farklı görev gerçekleştirebilen bu mükemmel aracı yazdı. Web geliştirme Yardımcısı [http://projects.nikhilk.net/Projects/WebDevHelper.aspx](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)' de indirilebilir.

Web geliştirme Yardımcısı doğrudan Internet Explorer 'ın içinde kullanılabilir, bu sayede kullanımı uygun hale gelir. Internet Explorer menüsünden Araçlar Web geliştirme Yardımcısı seçilerek başlatılır. Bu işlem, tarayıcıyı, HTTP isteği ve yanıt iletisi günlüğü gibi çeşitli görevleri gerçekleştirmek için tarayıcıdan ayrılmamanız gerekmez Şekil 4 ' te gösterildiği gibi web geliştirme Yardımcısı gösterilmektedir.

[![Web geliştirme Yardımcısı](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**Şekil 4**: Web geliştirme Yardımcısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))

Web geliştirme Yardımcısı, Visual Studio 2008 ' de olduğu gibi, kod satırını satır içine almak için kullanacağınız bir araç değildir. Ancak, izleme çıkışını görüntülemek, bir betikteki değişkenleri kolayca değerlendirmek veya bir JSON nesnesinin içindeki verileri araştırmak için kullanılabilir. Ayrıca, bir ASP.NET AJAX sayfasına ve bir sunucusuna geçirilen verileri görüntülemek için de kullanışlıdır.

Web geliştirme Yardımcısı Internet Explorer 'da açıldıktan sonra, Şekil 4 ' te daha önce gösterildiği gibi web geliştirme Yardımcısı menüsünden betik hata ayıklamayı etkinleştir ' i seçerek betik hata ayıklaması etkinleştirilmelidir. Bu, aracın bir sayfa çalıştırıldığı sürece oluşan hataları ele almasını sağlar. Ayrıca, sayfada çıktı olan iletileri izlemeye kolay erişim sağlar. Bir sayfada farklı işlevleri test etmek üzere izleme bilgilerini görüntülemek veya betik komutlarını yürütmek için Web geliştirme Yardımcısı menüsünden betik konsolunu göster ' i seçin. Bu, bir komut penceresine ve basit bir pencereye erişim sağlar.

*Izleme Iletilerini ve JSON nesnesi verilerini görüntüleme*

Komut penceresi, betik komutlarının yürütülmesi veya bir sayfadaki farklı işlevleri test etmek için kullanılan komut dosyalarını yüklemek ya da kaydetmek için kullanılabilir. Komut penceresi, görüntülenen sayfa tarafından yazılan izleme veya hata ayıklama iletilerini görüntüler. 2\. liste, Internet Explorer 'ın Debug. writeln işlevini kullanarak bir izleme iletisinin nasıl yazılacağını gösterir.

**Listeleme 2. Hata ayıklama sınıfını kullanarak istemci tarafı izleme iletisi yazma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

LastName özelliği bir tikan değeri içeriyorsa Web geliştirme Yardımcısı, komut dosyası konsolunun komut penceresinde "kişi adı: tikan" iletisini görüntüler (hata ayıklamanın etkinleştirildiği varsayılarak). Web geliştirme Yardımcısı ayrıca, izleme bilgilerini yazmak veya JSON nesnelerinin içeriğini görüntülemek için kullanılabilecek sayfalara üst düzey debugService nesnesi ekler. Kod 3 ' te debugService sınıfının Trace işlevini kullanma örneği gösterilmektedir.

**Listeleme 3. Web geliştirme Yardımcısı 'nın debugService sınıfını kullanarak bir izleme iletisi yazma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService sınıfının iyi bir özelliği, Internet Explorer 'da hata ayıklama etkinleştirilmemiş olsa bile, Web geliştirme Yardımcısı çalışırken izleme verilerine her zaman erişmenizi kolaylaştırır. Araç bir sayfada hata ayıklamak için kullanılmazsa, Window. debugService çağrısı yanlış döndürecek şekilde Trace deyimleri yok sayılır.

DebugService sınıfı, JSON nesne verilerinin Web geliştirme Yardımcısı Denetçisi penceresi kullanılarak görüntülenmesine de olanak tanır. 4\. liste, kişi verilerini içeren basit bir JSON nesnesi oluşturur. Nesne oluşturulduktan sonra, JSON nesnesinin görsel olarak incelenebilmesini sağlamak için debugService sınıfının INSPECTION işlevine bir çağrı yapılır.

**4. liste. JSON nesne verilerini görüntülemek için debugService. INSPECTION işlevini kullanma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

Sayfada veya anlık pencere aracılığıyla GetPerson () işlevini çağırmak, Şekil 5 ' te gösterildiği gibi nesne denetçisi iletişim penceresinin görünmesine neden olur. Nesne içindeki özellikler, değer metin kutusunda gösterilen değeri değiştirerek ve ardından Güncelleştir bağlantısına tıklanarak dinamik olarak değiştirilebilir. Nesne denetçisini kullanmak, JSON nesne verilerini görüntülemeyi ve özelliklere farklı değerler uygulamayı denemeyi kolaylaştırır.

*Hata ayıklama hataları*

Web geliştirme Yardımcısı, izleme verilerinin ve JSON nesnelerinin görüntülenmesine izin vermenin yanı sıra sayfadaki hata ayıklama hatalarına de yardımcı olabilir. Bir hata ile karşılaşırsanız, bir sonraki kod satırına devam etmeniz veya betikte hata ayıklaması yapmanız istenir (bkz. Şekil 6). Betik hatası iletişim penceresi, tüm çağrı yığınını ve satır numaralarını gösterir, böylece sorunların bir betikde olduğunu kolayca tanımlayabilmenizi sağlayabilirsiniz.

[JSON nesnesini görüntülemek için nesne denetçisi penceresini kullanarak ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**Şekil 5**: JSON nesnesini görüntülemek Için nesne denetçisi penceresini kullanma.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png))

Hata Ayıkla seçeneğinin belirlenmesi, doğrudan web geliştirme Yardımcısı penceresinde, değişkenlerin değerini görüntülemek, JSON nesneleri yazmak ve daha fazlasını görmek için betik deyimlerini doğrudan pencerede yürütmanızı sağlar. Hatayı tetikleyen aynı eylem yeniden yapılır ve makinede Visual Studio 2008 varsa, önceki bölümde anlatıldığı gibi kod satırı satırı üzerinden ileredebilmeniz için bir hata ayıklama oturumu başlatmanız istenir.

[![Web geliştirme Yardımcısı komut dosyası hatası Iletişim kutusu](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**Şekil 6**: Web geliştirme Yardımcısı 'Nın betik hatası iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png))

*Istek ve yanıt Iletilerini İnceleme*

ASP.NET AJAX sayfalarında hata ayıklarken, bir sayfa ve sunucu arasında gönderilen istek ve yanıt iletilerini görmek genellikle yararlı olur. İletilerin içindeki içeriği görüntülemek, doğru verilerin geçtiğini ve iletilerin boyutunu görmenizi sağlar. Web geliştirme Yardımcısı, verileri ham metin olarak veya daha okunabilir bir biçimde görüntülemeyi kolaylaştıran harika bir HTTP ileti günlükçüsü özelliği sunar.

ASP.NET AJAX istek ve yanıt iletilerini görüntülemek için, http günlükçüsü 'nin Web geliştirme Yardımcısı menüsünden http günlük kaydını etkinleştir seçilerek etkinleştirilmesi gerekir. Etkinleştirildikten sonra, geçerli sayfadan gönderilen tüm iletiler http günlüğü görüntüleyicisinde görüntülenebilir ve http göster HTTP günlükleri seçilerek erişilebilirler.

Her istek/yanıt iletisinde gönderilen ham metnin görüntülenmesi kesinlikle yararlı olsa da (ve Web geliştirme Yardımcısı 'nda bir seçenek), ileti verilerini daha fazla grafik biçiminde görüntülemek genellikle daha kolay olur. HTTP günlüğü etkinleştirildikten ve iletiler günlüğe kaydedildikten sonra, HTTP günlüğü görüntüleyicisinde iletiye çift tıklayarak ileti verileri görüntülenebilir. Bunun yapılması, bir iletiyle ilişkili tüm üstbilgileri ve gerçek ileti içeriğini görüntülemenize olanak sağlar. Şekil 7 ' de HTTP günlük Görüntüleyici penceresinde görüntülenen istek iletisi ve yanıt iletisi örneği gösterilmektedir.

[istek ve yanıt iletisi verilerini görüntülemek için HTTP günlük görüntüleyicisini kullanarak ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**Şekil 7**: istek ve yanıt iletisi verilerini görüntülemek Için http günlük görüntüleyicisini kullanma.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png))

HTTP günlük Görüntüleyici, JSON nesnelerini otomatik olarak ayrıştırır ve nesnenin özellik verilerini görüntülemeyi hızlı ve kolay hale getiren bir ağaç görünümü kullanarak görüntüler. Bir UpdatePanel bir ASP.NET AJAX sayfasında kullanıldığında, Görüntüleyici, Şekil 8 ' de gösterildiği gibi, iletinin her bölümünü ayrı parçalara ayırır. Bu, ham ileti verilerinin görüntülenmesine kıyasla iletinin ne olduğunu görmeyi ve anlamayı çok daha kolay hale getiren harika bir özelliktir.

[HTTP günlük Görüntüleyicisi kullanılarak görüntülenen bir UpdatePanel yanıt iletisi ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**Şekil 8**: http günlük Görüntüleyicisi kullanılarak görüntülenen bir UpdatePanel yanıt iletisi.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png))

Web geliştirme Yardımcısı 'na ek olarak istek ve yanıt iletilerini görüntülemek için kullanılabilen çeşitli araçlar vardır. [http://www.fiddlertool.com](http://www.fiddlertool.com)' de ücretsiz olarak kullanılabilen Fiddler, başka bir iyi seçenektir. Fiddler burada açıklanmayacak olsa da, ileti üst bilgilerini ve verilerini kapsamlı bir şekilde incelemeniz gerektiğinde iyi bir seçenektir.

## <a name="debugging-with-firefox-and-firebug"></a>Firefox ve Firebug ile hata ayıklama

Internet Explorer hala en yaygın olarak kullanılan tarayıcıdayken, Firefox gibi diğer tarayıcılar oldukça popüler hale gelmiştir ve daha fazla ve daha fazlasını kullanır. Sonuç olarak, uygulamalarınızın düzgün çalıştığından emin olmak için ASP.NET AJAX sayfalarınızı Firefox 'ta ve Internet Explorer 'da da görüntülemek ve hatalarını ayıklamak isteyeceksiniz. Firefox hata ayıklama için doğrudan Visual Studio 2008 ' e bağlanamıyor olsa da, sayfada hata ayıklamak için kullanılabilecek Firebug adlı bir uzantıya sahiptir. Firebug, [http://www.getfirebug.com](http://www.getfirebug.com)giderek ücretsiz olarak indirilebilir.

Firebug, kod hattını satır içine almak, bir sayfada kullanılan tüm betiklerle erişmek, DOM yapılarını görüntülemek ve hatta bir sayfada oluşan olayları izlemek için kullanılabilecek tam özellikli bir hata ayıklama ortamı sağlar. Yüklendikten sonra, Araçlar menüsünden Araçlar Firebug açık Firebug ' ı seçerek Firebug 'a erişebilirsiniz. Web geliştirme Yardımcısı gibi, Firebug, tek başına bir uygulama olarak da kullanılabilmesine rağmen doğrudan tarayıcıda kullanılır.

Firebug çalışmaya başladıktan sonra, betiğin bir sayfada gömülü olup olmadığı bir JavaScript dosyasının herhangi bir satırında kesme noktaları ayarlanabilir. Bir kesme noktası ayarlamak için öncelikle Firefox 'ta hata ayıklamak istediğiniz uygun sayfayı yükleyin. Sayfa yüklendikten sonra, Firebug 'ın betikleri açılan listesinden hata ayıklamak için betiği seçin. Sayfa tarafından kullanılan tüm betikler gösterilir. Kesme noktası, kesme noktasının gitmesi gereken satırda, Visual Studio 2008 ' de yapacağınız gibi, Firebug 'in gri tepsi alanı tıklatılarak ayarlanır.

Firebug 'da bir kesme noktası ayarlandıktan sonra, bir düğmeye tıklanması veya onLoad olayını tetiklemek için tarayıcıyı yenilemek gibi hata ayıklaması yapılması gereken betiği yürütmek için gerekli eylemi gerçekleştirebilirsiniz. Yürütme, kesme noktasını içeren satırda otomatik olarak durur. Şekil 9, Firebug 'da tetiklenen bir kesme noktasına bir örnek gösterir.

[Firebug 'da kesme noktaları Işleme ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**Şekil 9**: Firebug 'da kesme noktaları işleniyor.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png))

Kesme noktası isabet aldıktan sonra, ok düğmelerini kullanarak koda adım adım ilerledikten veya kodun dışına ileredebilirsiniz. Kod içinde adımlayın, komut dosyası değişkenleri hata ayıklayıcının sağ bölümünde görüntülenir ve nesneler üzerinde detaya gitmeyi sağlar. Firebug Ayrıca, betiğin ayıklanmakta olan geçerli satıra kadar olan yürütme adımlarını görüntülemek için çağrı yığını açılan listesini de içerir.

Firebug, farklı betik deyimlerini test etmek, değişkenleri değerlendirmek ve izleme çıkışını görüntülemek için kullanılabilecek bir konsol penceresi de içerir. Firebug penceresinin en üstündeki konsol sekmesine tıklanarak erişilir. Hata ayıklamakta olan sayfa ayrıca, Inceleme sekmesine tıklayarak DOM yapısını ve içeriğini görmek için "incelenebilir" olabilir. Inspector penceresinde gösterilen farklı DOM öğelerinin üzerinde fare ettiğiniz gibi, sayfada öğenin nerede kullanıldığını görmeyi kolaylaştırmak için sayfanın uygun bölümü vurgulanacaktır. Belirli bir öğeyle ilişkili öznitelik değerleri, bir öğeye farklı genişlikler, stiller vb. uygulamayı denemek için "canlı" değiştirilebilir. Bu, ne kadar basit değişikliklerin bir sayfayı etkilediklerini görüntülemek için kaynak kodu Düzenleyicisi ile Firefox tarayıcısı arasında sürekli geçiş yapmak zorunda kalmanızı sağlayan iyi bir özelliktir.

Şekil 10 ' da, sayfada txtCountry adlı bir metin kutusunu bulmak için DOM denetçisini kullanma örneği gösterilmektedir. Firebug denetçisi ayrıca bir sayfada kullanılan CSS stillerini, düğme tıklamalarını ve daha fazlasını izleyen olayları görüntülemek için de kullanılabilir.

[Firebug 'ın DOM denetçisini kullanarak ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**Şekil 10**: Firebug 'ın Dom denetçisini kullanma.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png))

Firebug, sayfada bulunan farklı öğeleri incelemek için harika bir araç ve doğrudan Firefox 'ta bir sayfada hata ayıklamanın hafif bir yolunu sağlar.

## <a name="debugging-support-in-aspnet-ajax"></a>ASP.NET AJAX 'ta hata ayıklama desteği

ASP.NET AJAX kitaplığı, bir Web sayfasına AJAX özellikleri ekleme işlemini basitleştirmek için kullanılabilecek birçok farklı sınıf içerir. Bu sınıfları bir sayfada öğeleri bulmak ve işlemek, yeni denetimler eklemek, Web hizmetlerini çağırmak ve hatta olayları işlemek için kullanabilirsiniz. ASP.NET AJAX kitaplığı, sayfaların hata ayıklama işlemini iyileştirmek için kullanılabilecek sınıflar da içerir. Bu bölümde, sys. Debug sınıfına tanıtırsınız ve uygulamalarda nasıl kullanılabileceğini görürsünüz.

*Sys. Debug sınıfını kullanma*

Sys. Debug sınıfı (sys ad alanında bulunan bir JavaScript sınıfı), izleme çıktısı yazma, kod onaylamaları gerçekleştirme ve kodun ayıklanabilmesi için kodu zorlama gibi çeşitli farklı işlevleri gerçekleştirmek için kullanılabilir. Koşullu testleri gerçekleştirmek için ASP.NET AJAX kitaplığının hata ayıklama dosyalarında (varsayılan olarak C:\Program Files\Microsoft ASP. NET\ASP.NET 2,0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 ' de yüklüdür) kapsamlı olarak kullanılır ( onayları olarak adlandırılır) parametrelerin işlevlerine doğru şekilde geçirildiğinden emin olan nesneler, beklenen verileri içerir ve Trace deyimlerini yazar.

Sys. Debug sınıfı, Tablo 1 ' de gösterildiği gibi izleme, kod onaylama veya hataları işlemek için kullanılabilecek çeşitli farklı işlevleri kullanıma sunar.

**Tablo 1. Sys. Debug sınıfı işlevleri.**

| **İşlev adı** | **Açıklama** |
| --- | --- |
| onaylama (koşul, ileti, displayCaller) | Koşul parametresinin true olduğunu onaylar. Test edilen koşul false ise, ileti parametresi değerini göstermek için bir ileti kutusu kullanılır. DisplayCaller parametresi true ise, yöntemi çağıran hakkındaki bilgileri de görüntüler. |
| clearTrace () | İzleme işlemlerinin deyimlerini siler. |
| başarısız (ileti) | Programın yürütmeyi durdurmasına ve hata ayıklayıcıya kesintiye uğramasına neden olur. İleti parametresi hata nedenini sağlamak için kullanılabilir. |
| Trace (ileti) | İleti parametresini izleme çıktısına yazar. |
| traceDump (nesne, ad) | Nesnenin verilerini okunabilir bir biçimde verir. Ad parametresi, izleme dökümü için bir etiket sağlamak üzere kullanılabilir. Dökümekte olan nesne içindeki tüm alt nesneler varsayılan olarak yazılır. |

İstemci tarafı izleme, ASP.NET ' de bulunan izleme işleviyle aynı şekilde kullanılabilir. Uygulamanın akışını kesintiye uğramadan, farklı iletilerin kolayca görüntülenmesine izin verir. 5\. liste, izleme günlüğüne yazmak için sys. Debug. Trace işlevinin kullanılmasına bir örnek gösterir. Bu işlev yalnızca bir parametre olarak yazılması gereken iletiyi alır.

**5. liste. Sys. Debug. Trace işlevini kullanma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

5\. listede gösterilen kodu çalıştırırsanız, sayfada herhangi bir izleme çıkışı görmezsiniz. Bunu görmenin tek yolu, Visual Studio .NET, Web geliştirme Yardımcısı veya Firebug 'da bulunan bir konsol penceresini kullanmaktır. Sayfada izleme çıkışını görmek isterseniz, bir TextArea etiketi eklemeniz ve bir sonraki adımda gösterildiği gibi bir Izlenebilir konsol kimliği vermeniz gerekir:

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

Sayfadaki tüm sys. Debug. Trace deyimleri TraceConsole TextArea öğesine yazılır.

JSON nesnesinde yer alan verileri görmek istediğiniz durumlarda, sys. Debug sınıfının traceDump işlevini kullanabilirsiniz. Bu işlev, izleme konsoluna dökülecekleri nesne ve izleme çıkışında nesneyi tanımlamak için kullanılabilecek bir ad dahil olmak üzere iki parametre alır. 6\. liste, traceDump işlevinin kullanımına ilişkin bir örnek gösterir.

**Liste 6. Sys. Debug. traceDump işlevini kullanma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

Şekil 11, sys. Debug. traceDump işlevini çağıran çıktıyı gösterir. Kişi nesnesinin verilerini yazmanın yanı sıra adres alt nesnesinin verilerini de yazdığına dikkat edin.

İzlemeye ek olarak, sys. Debug sınıfı kod onaylama işlemleri gerçekleştirmek için de kullanılabilir. Onaylamalar, bir uygulama çalışırken belirli koşulların karşılandığını sınamak için kullanılır. ASP.NET AJAX kitaplığı betiklerinin hata ayıklama sürümü, çeşitli koşulları test etmek için çeşitli onay deyimleri içerir.

7\. liste, bir koşulu sınamak için sys. Debug. onaylama işlevinin kullanılmasına bir örnek gösterir. Kod, bir kişi nesnesini güncelleştirmeden önce Address nesnesinin null olup olmadığını test eder.

[Sys. Debug. traceDump işlevinin çıkışı ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**Şekil 11**: sys. Debug. tracedump işlevinin çıktısı.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png))

**Listeleme 7. Debug. onaylama işlevini kullanma.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

Değerlendirmek için koşul dahil olmak üzere üç parametre geçirilir, onaylama yanlış döndürürse görüntülenecek ileti ve arayan hakkındaki bilgilerin görüntülenip görüntülenmeyeceğini gösterir. Bir onaylama işlemi başarısız olduğunda, üçüncü parametre doğruysa ileti ve arayan bilgileri de görüntülenir. Şekil 12 ' de, liste 7 ' de gösterilen onaylama başarısız olursa görüntülenen hata iletişim kutusunun bir örneği gösterilmektedir.

Kapsayan son işlev sys. Debug. Fail ' dir. Kodun bir betikteki belirli bir satırda başarısız olmasına zorlamak istediğinizde, genellikle JavaScript uygulamalarında kullanılan hata ayıklayıcı deyimleri yerine bir sys. Debug. Fail çağrısı ekleyebilirsiniz. Sys. Debug. Fail işlevi, daha sonra gösterildiği gibi hatanın nedenini temsil eden tek bir dize parametresini kabul eder:

[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]

[Bir sys. Debug. onaylama hata iletisi ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**Şekil 12**: bir sys. Debug. onaylama hata iletisi.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png))

Bir betik yürütülürken bir sys. Debug. Fail ifadesiyle karşılaşıldığında, Message parametresinin değeri Visual Studio 2008 gibi bir hata ayıklama uygulamasının konsolunda görüntülenir ve uygulamada hata ayıklaması yapmanız istenir. Bunun çok yararlı olabileceği bir durum, bir satır içi betikte Visual Studio 2008 ile bir kesme noktası ayarlayamadığınızda, ancak değişkenlerin değerini incelemenize olanak sağlamak için kodun belirli bir satırda durdurulmasını de istersiniz.

*ScriptManager denetiminin ScriptMode özelliğini anlama*

ASP.NET AJAX kitaplığı, varsayılan olarak C:\Program Files\Microsoft ASP. NET\ASP.NET 2,0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 'e yüklenen hata ayıklama ve sürüm betiği sürümlerini içerir. Hata ayıklama betikleri oldukça kolay biçimlendirilmiştir, okunması kolaydır ve birçok sys. Debug. onay çağrısı, yayın betiklerinde boşluk yerleştirilirken ve sys. Debug sınıfını gelişigüzel bir şekilde kullanarak genel boyutunu en aza indirir.

ASP.NET AJAX sayfalarına eklenen ScriptManager denetimi, kitaplık betiklerinin hangi sürümlerinin yükleneceğini belirleyen Web. config içindeki derleme öğesinin hata ayıklama özniteliğini okur. Ancak, ScriptMode özelliğini değiştirerek hata ayıklama veya sürüm betikleri (kitaplık betikleri veya kendi özel komut dosyalarınız) yüklenip yüklenmediğini kontrol edebilirsiniz. ScriptMode, üyeleri otomatik, hata ayıklama, yayınlama ve devralma içeren bir ScriptMode numaralandırması kabul eder.

ScriptMode varsayılan değer olan Auto değeridir. Bu, ScriptManager 'ın Web. config 'deki Debug özniteliğini denetmeyeceği anlamına gelir. Hata ayıklama yanlış olduğunda, ScriptManager ASP.NET AJAX kitaplık betikleri yayın sürümünü yükler. Hata ayıklama doğru olduğunda, betiklerin hata ayıklama sürümü yüklenir. ScriptMode özelliğinin Release veya Debug olarak değiştirilmesi, hata ayıklama özniteliğinin Web. config dosyasında sahip olduğu değerden bağımsız olarak, ScriptManager 'ın uygun betikleri yüklemesine zorlar. 8. liste, ASP.NET AJAX kitaplığından hata ayıklama komut dosyalarını yüklemek için ScriptManager denetimini kullanmanın bir örneğini gösterir.

**8. liste. ScriptManager kullanarak hata ayıklama betikleri yükleniyor**.

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

Ayrıca, ScriptManager 'ın Scripts özelliğini kullanarak kendi özel betiklerinizin farklı sürümlerini (hata ayıklama veya sürüm), kod 9 ' da gösterildiği gibi ScriptReference bileşeniyle birlikte da yükleyebilirsiniz.

**9. liste. ScriptManager kullanarak özel betikler yükleme.**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> ScriptReference bileşenini kullanarak özel betikler yüklüyorsanız, betiğin alt kısmına aşağıdaki kodu ekleyerek komut dosyasının yüklemesi tamamlandığında ScriptManager 'a bildirimde bulunmak zorundasınız:

[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

Liste 9 ' da gösterilen kod, ScriptManager 'ın Person. js yerine Person. Debug. js ' yi otomatik olarak araması için kişi betiğinin hata ayıklama sürümünü bakmasını söyler. Person. Debug. js dosyası bulunmazsa bir hata oluşur.

ScriptManager denetiminde ayarlanan ScriptMode özelliğinin değerine bağlı olarak özel bir betiğin hata ayıklama veya yayınlama sürümünün yüklenmesini istediğiniz durumlarda ScriptReference denetiminin ScriptMode özelliğini Inherit olarak ayarlayabilirsiniz. Bu, özel betiğin doğru sürümünün, ScriptManager 'ın ScriptMode özelliğine göre, 10. listede gösterildiği gibi yüklenememesine neden olur. ScriptManager denetiminin ScriptMode özelliği hata ayıklama olarak ayarlandığından, Person. Debug. js betiği sayfada yüklenir ve kullanılacaktır.

**10 dökümünü yapın. Özel betikler için ScriptManager 'dan ScriptMode devralınıyor.**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

ScriptMode özelliğini uygun şekilde kullanarak uygulamalar üzerinde daha kolay hata ayıklama yapabilir ve genel işlemi basitleştirebilirsiniz. Hata ayıklama betikleri özel olarak hata ayıklama amacıyla biçimlendirilirken, ASP.NET AJAX kitaplığı 'nın sürüm betikleri, kod biçimlendirme kaldırıldıktan sonra ilerlemeleri ve okumak zor olabilir.

## <a name="conclusion"></a>Sonuç

Microsoft 'un ASP.NET AJAX teknolojisi, son kullanıcının genel deneyimini geliştirebilecek AJAX özellikli uygulamalar oluşturmaya yönelik sağlam bir temel sağlar. Ancak, tüm programlama teknolojilerinde olduğu gibi hatalar ve diğer uygulama sorunları da kesinlikle meydana olur. Kullanılabilir farklı hata ayıklama seçeneklerinin bilinmesi çok zaman kazandırabilir ve daha kararlı bir ürüne neden olabilir.

Bu makalede, Visual Studio 2008, Web geliştirme Yardımcısı ve Firebug ile Internet Explorer dahil olmak üzere ASP.NET AJAX sayfalarında hata ayıklama için birkaç farklı teknik sunulmuştur. Bu araçlar, değişken verilerine erişebilmeniz için, satır satırına göre kod satırı ve izleme deyimlerini görüntüleme gibi genel hata ayıklama sürecini basitleştirebilir. Ayrıca, ele alınan farklı hata ayıklama araçlarına ek olarak, ASP.NET AJAX kitaplığı 'nın sys. Debug sınıfının bir uygulamada nasıl kullanılabileceğini ve ScriptManager sınıfının hata ayıklama veya betiklerin yayın sürümlerini yüklemek için nasıl kullanılabileceğini de gördünüz.

## <a name="bio"></a>Biyografisi

Dan Wahlin (ASP.NET ve XML Web Hizmetleri için Microsoft en değerli profesyonel), arabirim teknik eğitimi ([www.interfacett.com)](http://www.interfacett.com)adresindeki bir .NET geliştirme eğitmeni ve mimari danışmanıdır. , ASP.NET geliştiricileri Web sitesi ([www.XMLforASP.net](http://www.XMLforASP.NET)) için XML, bir konuşmacı bürosuna ve birçok konferansda konuşuyor. Dan co-yazılan profesyonel Windows DNA (SaaS x), ASP.NET: Ipuçları, öğreticiler ve kod (Sams), ASP.NET 1,1 Insider Solutions, Professional ASP.NET 2,0 AJAX (SaaS x), ASP.NET 2,0 MVP Hacks ve yazılan XML for ASP.NET Developers (Sams). Kod, makale veya kitap yazmadığınızda, bol ve çocukları kullanarak müzik yazma ve kaydetme ve Golf ve basketbol topu oynatma.

Scott, 1997 tarihinden itibaren Microsoft Web teknolojileriyle çalışmaktadır ve Bilgi Bankası yazılım çözümlerine odaklanmış ASP.NET tabanlı uygulamalar yazma konusunda uzmanımız myKB.com ([www.myKB.com](http://www.myKB.com)) Başkan Yardımcısı. Scott 'da e-posta ile [scott.cate@myKB.com](mailto:scott.cate@myKB.com) veya blogundan [ScottCate.com](http://ScottCate.com) adresinden iletişim kurulabilirler

> [!div class="step-by-step"]
> [Öncekini](understanding-asp-net-ajax-web-services.md)
