---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
title: Içerik sayfalarında denetim KIMLIĞI adlandırma (VB) | Microsoft Docs
author: rick-anderson
description: ContentPlaceHolder denetimlerinin adlandırma kapsayıcısı olarak nasıl çalıştığını gösterir ve bu nedenle programlı olarak bir denetim ile çalışır (FindControl aracılığıyla)...
ms.author: riande
ms.date: 06/10/2008
ms.assetid: dbb024a6-f043-4fc5-ad66-56556711875b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 3cb8dec47040bc65f1a024325c91590729ffbdb7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586649"
---
# <a name="control-id-naming-in-content-pages-vb"></a>İçerik Sayfalarında Denetim Kimliği Adlandırma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_VB.pdf)

> ContentPlaceHolder denetimlerinin adlandırma kapsayıcısı olarak nasıl çalıştığını gösterir ve bu nedenle programlı olarak bir denetim ile çalışır (FindControl aracılığıyla). Bu soruna ve geçici çözümlere bakar. Ayrıca, elde edilen ClientID değerine programlı olarak nasıl erişebileceğinizi açıklar.

## <a name="introduction"></a>Giriş

Tüm ASP.NET Server denetimleri, denetimi benzersiz bir şekilde tanımlayan bir `ID` özelliği içerir ve denetimin arka plan kod sınıfında programlı olarak eriştiği anlamına gelir. Benzer şekilde, bir HTML belgesindeki öğeler, öğeyi benzersiz bir şekilde tanımlayan bir `id` özniteliği içerebilir; Bu `id` değerler genellikle belirli bir HTML öğesine programlı olarak başvurmak için istemci tarafı betikte kullanılır. Bu şekilde, bir ASP.NET sunucu denetimi HTML 'de işlendiğinde, `ID` değerinin işlenmiş HTML öğesinin `id` değeri olarak kullanıldığını varsayabilirsiniz. Bu durum, belirli koşullarda tek bir `ID` değeri olan tek bir denetimin, işlenmiş biçimlendirmede birden çok kez görünebileceğinden, bu durum değildir. `ProductName``ID` bir değeri olan bir etiket Web denetimiyle TemplateField içeren bir GridView denetimi düşünün. GridView, çalışma zamanında veri kaynağına bağlandığında, bu etiket her GridView satırı için yinelenir. İşlenen her etiketin benzersiz bir `id` değeri olması gerekir.

Bu tür senaryoları işlemek için, ASP.NET, belirli denetimlerin adlandırma kapsayıcıları olarak kullanılmasına izin verir. Adlandırma kapsayıcısı yeni bir `ID` ad alanı işlevi görür. Adlandırma kapsayıcısı içinde görünen tüm sunucu denetimleri, adlandırma kapsayıcısı denetiminin `ID` önekli `id` değerine sahiptir. Örneğin, `GridView` ve `GridViewRow` sınıfları, her iki adlandırma kapsayıcılarıdır. Sonuç olarak, `ID` `ProductName` olan bir GridView TemplateField 'da tanımlanan bir etiket denetimine `GridViewID_GridViewRowID_ProductName`işlenmiş `id` değeri verilir. *Gridviewrowıd* her GridView satırı için benzersiz olduğundan, sonuçta elde edilen `id` değerleri benzersizdir.

> [!NOTE]
> [`INamingContainer` arabirimi](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx) , belirli bir ASP.NET Server denetiminin bir adlandırma kapsayıcısı olarak çalışması gerektiğini belirtmek için kullanılır. `INamingContainer` arabirimi, sunucu denetiminin uygulaması gereken herhangi bir yöntemi değil; Bunun yerine işaret olarak kullanılır. İşlenmiş biçimlendirmeyi oluştururken, bir denetim bu arabirimi uygularsa, ASP.NET altyapısı `ID` değerini otomatik olarak alt öğelerinden ' işlenmiş `id` öznitelik değerlerine ekler. Bu işlem, adım 2 ' de daha ayrıntılı bir şekilde ele alınmıştır.

Adlandırma kapsayıcıları yalnızca işlenen `id` öznitelik değerini değiştirmez, ancak aynı zamanda denetimin ASP.NET sayfasının arka plan kod sınıfından programlama yoluyla nasıl başvurduğunu da etkiler. `FindControl("controlID")` yöntemi, yaygın olarak bir Web denetimine başvurmak için kullanılır. Ancak `FindControl`, adlandırma kapsayıcıları aracılığıyla sızmaz. Sonuç olarak, GridView veya diğer adlandırma kapsayıcısı içindeki denetimlere başvurmak için `Page.FindControl` yöntemini doğrudan kullanamazsınız.

Yukarıda da belirtildiği gibi, ana sayfalar ve Contentyertutucuların her ikisi de adlandırma kapsayıcıları olarak uygulanır. Bu öğreticide, ana sayfaların HTML öğesi `id` nasıl etkilediğini ve `FindControl`kullanarak bir içerik sayfasında program aracılığıyla Web denetimlerine nasıl başvurulacağını inceleyeceğiz.

## <a name="step-1-adding-a-new-aspnet-page"></a>1\. Adım: yeni bir ASP.NET sayfası ekleme

Bu öğreticide ele alınan kavramları göstermek için Web sitemize yeni bir ASP.NET sayfası ekleyelim. Kök klasörde `IDIssues.aspx` adlı yeni bir içerik sayfası oluşturun ve `Site.master` ana sayfasına bağlama.

![Idissues. aspx Içerik sayfasını kök klasöre ekleyin](control-id-naming-in-content-pages-vb/_static/image1.png)

**Şekil 01**: içerik sayfası `IDIssues.aspx` kök klasöre ekleyin

Visual Studio, ana sayfanın dört Contentiyertutucusu için otomatik olarak bir Içerik denetimi oluşturur. [*Birden çok Contenttutucuları ve varsayılan içerik*](multiple-contentplaceholders-and-default-content-vb.md) öğreticisinde belirtildiği gibi, içerik denetimi yoksa, ana sayfanın varsayılan ContentPlaceHolder içeriği yayılır. `QuickLoginUI` ve `LeftColumnContent` Contentyertutucuları Bu sayfa için uygun varsayılan biçimlendirmeyi içerdiğinden, devam edin ve ilgili Içerik denetimlerini `IDIssues.aspx`kaldırın. Bu noktada, içerik sayfasının bildirim temelli biçimlendirme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample1.aspx)]

[*Ana sayfada başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirtme*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) öğreticisinde, açıkça ayarlanmamışsa sayfanın başlığını otomatik olarak yapılandıran özel bir temel sayfa sınıfı (`BasePage`) oluşturduk. `IDIssues.aspx` sayfasında bu işlevselliği kullanmak için, sayfanın arka plan kod sınıfı `BasePage` sınıfından türetmelidir (`System.Web.UI.Page`yerine). Arka plan kod sınıfının tanımını, aşağıdakine benzer şekilde değiştirin:

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample2.vb)]

Son olarak, `Web.sitemap` dosyasını bu yeni ders için bir giriş içerecek şekilde güncelleştirin. `<siteMapNode>` bir öğesi ekleyin ve `title` ve `url` özniteliklerini sırasıyla "Denetim KIMLIĞI adlandırma sorunları" ve `~/IDIssues.aspx`olarak ayarlayın. Bunu yaptıktan sonra `Web.sitemap` dosyanızın biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-xml[Main](control-id-naming-in-content-pages-vb/samples/sample3.xml)]

Şekil 2 ' de gösterildiği gibi, `Web.sitemap` yeni site haritası girişi, sol sütundaki dersler bölümünde hemen yansıtılır.

![Dersler bölümü artık &quot;denetim KIMLIĞI adlandırma sorunlarına bir bağlantı Içerir&quot;](control-id-naming-in-content-pages-vb/_static/image2.png)

**Şekil 02**: dersler bölümü artık "denetim kimliği adlandırma sorunları" bağlantısını içerir

## <a name="step-2-examining-the-renderedidchanges"></a>2\. Adım: Işlenmiş`ID`değişikliklerini Inceleme

ASP.NET altyapısının, sunucu denetimlerinin işlenmiş `id` değerlerinde yaptığı değişiklikleri daha iyi anlamak için, `IDIssues.aspx` sayfasına birkaç Web denetimi ekleyelim ve sonra tarayıcıya gönderilen işlenmiş biçimlendirmeyi görüntüleyelim. Özellikle, "Lütfen yaşını girin:" ve ardından bir metin kutusu Web denetimi yazın. Sayfada daha fazla bir düğme web denetimi ve bir etiket Web denetimi ekleyin. TextBox 'ın `ID` ve `Columns` özelliklerini sırasıyla `Age` ve 3 olarak ayarlayın. Düğmenin `Text` ve `ID` özelliklerini "Gönder" ve `SubmitButton`olarak ayarlayın. Etiketin `Text` özelliğini temizleyin ve `ID` `Results`olarak ayarlayın.

Bu noktada, Içerik denetiminizin bildirime dayalı biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](control-id-naming-in-content-pages-vb/samples/sample4.aspx)]

Şekil 3 ' te, Visual Studio 'nun Tasarımcısı aracılığıyla görüntülendiğinde sayfa gösterilmektedir.

[Sayfa ![üç Web denetimi Içerir: TextBox, Button ve Label](control-id-naming-in-content-pages-vb/_static/image4.png)](control-id-naming-in-content-pages-vb/_static/image3.png)

**Şekil 03**: sayfa üç Web denetimi içerir: bir TextBox, düğme ve etiket ([tam boyutlu görüntüyü görüntülemek için tıklayın](control-id-naming-in-content-pages-vb/_static/image5.png))

Sayfayı bir tarayıcıda ziyaret edin ve HTML kaynağını görüntüleyin. Aşağıdaki biçimlendirme gösterildiği gibi, TextBox, Button ve Label Web denetimlerinin HTML öğelerinin `id` değerleri, Web denetimlerinin `ID` değerlerinin ve sayfadaki adlandırma kapsayıcılarının `ID` değerlerinin bir birleşimidir.

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample5.html)]

Bu öğreticide daha önce belirtildiği gibi, hem ana sayfa hem de onun Içerik yer tutucuları adlandırma kapsayıcıları olarak görev yapar. Sonuç olarak, her ikisi de iç içe denetimlerinin işlenmiş `ID` değerlerini katkıda bulunur. TextBox 'ın `id` özniteliğini al, örneğin: `ctl00_MainContent_Age`. TextBox denetiminin `ID` değerinin `Age`olduğunu hatırlayın. Bu, ContentPlaceHolder denetimin `ID` değeri `MainContent`ön ekine sahiptir. Ayrıca, bu değere ana sayfanın `ID` değeri `ctl00`ön eki eklenir. Net etkisi, ana sayfanın `ID` değerlerini, ContentPlaceHolder denetimini ve metin kutusunun kendisini içeren bir `id` özniteliği değeridir.

Şekil 4 ' te bu davranış gösterilmektedir. `Age` TextBox 'ın işlenmiş `id` belirlenmesi için, `Age`TextBox denetiminin `ID` değeri ile başlayın. Sonra, denetim hiyerarşisi için bir yöntem çalışın. Her adlandırma kapsayıcısında (açık rengi olan bu düğümler), adlandırma kapsayıcısının `id`geçerli olarak işlenen `id` ön eki.

![Işlenmiş kimlik öznitelikleri, adlandırma kapsayıcılarının KIMLIK değerlerine dayalıdır](control-id-naming-in-content-pages-vb/_static/image6.png)

**Şekil 04**: Işlenmiş `id` öznitelikleri, adlandırma kapsayıcılarının `ID` değerlerine dayalıdır

> [!NOTE]
> Tartışıyoruz, işlenmiş `id` özniteliğinin `ctl00` kısmı ana sayfanın `ID` değerini oluşturur, ancak bu `ID` değerin nasıl geldiğini merak ediyor olabilirsiniz. Ana veya içerik sayfamızda bir yere belirtmedik. Bir ASP.NET sayfasındaki çoğu sunucu denetimi, sayfanın bildirim temelli işaretlemesi aracılığıyla açıkça eklenir. `MainContent` ContentPlaceHolder denetimi, `Site.master`biçimlendirmesinde açıkça belirtilmiştir; `Age` metin kutusu `IDIssues.aspx`biçimlendirmesi olarak tanımlandı. Bu denetim türlerinin `ID` değerlerini Özellikler penceresi veya bildirime dayalı sözdiziminden belirteceğiz. Ana sayfanın kendisi gibi diğer denetimler, bildirim temelli biçimlendirmede tanımlanmamıştır. Sonuç olarak, `ID` değerlerinin ABD için otomatik olarak oluşturulması gerekir. ASP.NET altyapısı, kimlikleri açıkça ayarlanmamış olan denetimler için çalışma zamanında `ID` değerlerini ayarlar. `ctlXX`adlandırma modelini kullanır, burada *xx* sıralı olarak artan tamsayı değeridir.

Ana sayfanın kendisi bir adlandırma kapsayıcısı olarak görev yaptığından, ana sayfada tanımlanan Web denetimleri, işlenen `id` öznitelik değerlerini de değiştirmiş. Örneğin, [*Ana sayfa Ile site genelinde düzen oluşturma*](creating-a-site-wide-layout-using-master-pages-vb.md) öğreticisinde ana sayfaya eklediğimiz `DisplayDate` etiketi aşağıdaki işlenmiş biçimlendirmeye sahiptir:

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample6.html)]

`id` özniteliğinin hem ana sayfanın `ID` değerini (`ctl00`) hem de etiketin Web denetiminin `ID` değerini (`DateDisplay`) içerdiğini unutmayın.

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>3\. Adım: program aracılığıyla Web denetimlerine başvurma`FindControl`

Her ASP.NET sunucu denetimi, denetimin alt öğelerinden *ControlID*adlı bir denetim için arama yapan bir `FindControl("controlID")` yöntemi içerir. Böyle bir denetim bulunursa, döndürülür; eşleşen bir denetim bulunamazsa, `FindControl` `Nothing`döndürür.

`FindControl`, bir denetime erişmeniz gereken ancak kendisine doğrudan başvurmayan senaryolarda yararlıdır. GridView gibi veri Web denetimleriyle çalışırken, örneğin, GridView 'un alanlarındaki denetimler bildirim temelli sözdiziminde bir kez tanımlanır, ancak çalışma zamanında her GridView satırı için bir denetimin örneği oluşturulur. Sonuç olarak, çalışma zamanında oluşturulan denetimler mevcuttur, ancak arka plan kod sınıfından kullanılabilecek doğrudan bir başvuruya sahip değildir. Sonuç olarak, GridView 'un alanları içindeki belirli bir denetimle programlı bir şekilde çalışmak için `FindControl` kullanmanız gerekir. (Bir veri Web denetiminin şablonları içindeki denetimlere erişmek için `FindControl` kullanma hakkında daha fazla bilgi için, bkz. [verileri temel alan özel biçimlendirme](../../data-access/custom-formatting/custom-formatting-based-upon-data-vb.md).) Bu senaryo, [dinamik veri girişi kullanıcı arabirimleri oluşturma](https://msdn.microsoft.com/library/aa479330.aspx)bölümünde ele alınan bir konu olan Web formuna dinamik olarak Web denetimleri eklerken meydana gelir.

Bir içerik sayfasında denetimleri aramak için `FindControl` yöntemini kullanmayı göstermek için, `SubmitButton``Click` olayı için bir olay işleyicisi oluşturun. Olay işleyicisinde, `FindControl` yöntemini kullanarak `Age` TextBox ve `Results` etiketine programlı olarak başvuran aşağıdaki kodu ekleyin ve ardından kullanıcının girişine göre `Results` bir ileti görüntüler.

> [!NOTE]
> Tabii ki, bu örnek için etiket ve metin kutusu denetimlerine başvurmak üzere `FindControl` kullanmıyoruz. Bunlara `ID` özellik değerleri aracılığıyla doğrudan başvuracağız. Bir içerik sayfasından `FindControl` kullanırken ne olduğunu göstermek için `FindControl` burada kullanıyorum.

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample7.vb)]

`FindControl` yöntemini çağırmak için kullanılan sözdizimi, `SubmitButton_Click`ilk iki satırda biraz farklı olsa da, anlamsal olarak eşdeğerdir. Tüm ASP.NET Server denetimlerinin bir `FindControl` yöntemi içerdiğini hatırlayın. Bu, tüm ASP.NET arka plan kod sınıflarının türetmesini gerektiren `Page` sınıfını içerir. Bu nedenle, `FindControl("controlID")` çağrısı `Page.FindControl("controlID")`çağırma ile eşdeğerdir, ancak arka plan kod sınıfında veya özel bir temel sınıfta `FindControl` yöntemini geçersiz kılmadığınız varsayılır.

Bu kodu girdikten sonra tarayıcıda `IDIssues.aspx` sayfasını ziyaret edin, yaşını girin ve "Gönder" düğmesine tıklayın. "Gönder" düğmesine tıklandıktan sonra bir `NullReferenceException` tetiklenir (bkz. Şekil 5).

[Bir NullReferenceException ![tetiklenir](control-id-naming-in-content-pages-vb/_static/image8.png)](control-id-naming-in-content-pages-vb/_static/image7.png)

**Şekil 05**: bir `NullReferenceException` tetiklenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](control-id-naming-in-content-pages-vb/_static/image9.png))

`SubmitButton_Click` olay işleyicisinde bir kesme noktası ayarlarsanız, `FindControl` `Nothing`döndüren her iki çağrının de olduğunu görürsünüz. `NullReferenceException`, `Age` TextBox 'ın `Text` özelliğine erişmeye çalıştıklarında tetiklenir.

Sorun, yalnızca *denetimin*aynı adlandırma kapsayıcısında olan alt öğelerinden yalnızca arama `Control.FindControl`. Ana sayfa yeni bir adlandırma kapsayıcısı oluşturduğundan, `Page.FindControl("controlID")` bir çağrı ana sayfa nesnesinin `ctl00`hiçbir şekilde hiçbir şekilde hiçbir şekilde değildir. (`Page` nesnesini ana sayfa `ctl00`nesnesinin üst öğesi olarak gösteren denetim hiyerarşisini görüntülemek için Şekil 4 ' e geri dönün.) Bu nedenle, `Results` etiketi ve `Age` metin kutusu bulunamadı ve `ResultsLabel` ve `AgeTextBox` `Nothing`değerler atanır.

Bu zorluk için iki geçici çözüm vardır: aynı anda bir adlandırma kapsayıcısı, uygun denetime göre ayrıntıya gidebiliriz; ya da, ad kapsayıcılarını engelleyen kendi `FindControl` yöntemi oluşturuyoruz. Bu seçeneklerin her birini inceleyelim.

### <a name="drilling-into-the-appropriate-naming-container"></a>Uygun adlandırma kapsayıcısının detayına gitme

`Results` etiketine veya `Age` metin kutusuna başvurmak için `FindControl` kullanmak için, aynı adlandırma kapsayıcısında bir üst denetimden `FindControl` çağırdık. Şekil 4 ' te gösterildiği gibi, `MainContent` ContentPlaceHolder denetimi aynı adlandırma kapsayıcısı içindeki `Results` veya `Age` tek üst öğesi. Diğer bir deyişle, aşağıdaki kod parçacığında gösterildiği gibi, `MainContent` denetiminden `FindControl` yöntemini çağırmak, `Results` veya `Age` denetimlerine doğru bir başvuru döndürür.

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample8.vb)]

Ancak, ContentPlaceHolder ana sayfada tanımlandığından, yukarıdaki sözdizimini kullanarak içerik sayfanızın arka plan kod sınıfından ContentPlaceHolder `MainContent` ile çalışıyoruz. Bunun yerine, `MainContent`bir başvuru almak için `FindControl` kullandık. `SubmitButton_Click` olay işleyicisindeki kodu aşağıdaki değişikliklerle değiştirin:

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample9.vb)]

Sayfayı bir tarayıcı aracılığıyla ziyaret ederseniz, yaşını girip "Gönder" düğmesine tıkladığınızda bir `NullReferenceException` oluşturulur. `SubmitButton_Click` olay işleyicisinde bir kesme noktası ayarlarsanız, `MainContent` nesnesinin `FindControl` yöntemini çağırmaya çalışırken bu özel durumun oluştuğunu görürsünüz. `FindControl` yöntemi "MainContent" adlı bir nesne bulamadığından, `MainContent` nesnesi `Nothing` eşittir. Temel neden, `Results` etiketi ve `Age` metin kutusu denetimleriyle aynıdır: `FindControl`, arama denetimini denetim hiyerarşisinin en üstünden başlatır ve adlandırma kapsayıcılarını göstermez, ancak `MainContent` ContentPlaceHolder, bir adlandırma kapsayıcısı olan ana sayfa içindedir.

`MainContent`bir başvuru almak için `FindControl` kullanabilmeniz için önce ana sayfa denetimine bir başvuruya ihtiyacımız var. Ana sayfaya bir başvurduktan sonra, `FindControl` ile ContentPlaceHolder `MainContent` bir başvuru alabilir ve buradan, `Results` etiketine ve `Age` metin kutusuna (`FindControl`kullanarak) başvurur. Ancak ana sayfaya nasıl bir başvuru alırız? İşlenmiş biçimlendirmede `id` özniteliklerini inceleyerek ana sayfanın `ID` değerinin `ctl00`olması önerilir. Bu nedenle, ana sayfaya başvuru almak için `Page.FindControl("ctl00")` kullanabiliriz, sonra da `MainContent`bir başvuru almak için bu nesneyi kullanabilirsiniz. Aşağıdaki kod parçacığı bu mantığı göstermektedir:

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample10.vb)]

Bu kod tamamen çalışacaktır, ana sayfanın otomatik olarak oluşturulan `ID` her zaman `ctl00`olacağını varsayar. Otomatik olarak oluşturulan değerler hakkında varsayımlar yapmak hiç iyi bir fikir değildir.

Neyse ki, ana sayfaya yapılan bir başvuruya `Page` sınıfının `Master` özelliği aracılığıyla erişilebilir. Bu nedenle, `MainContent` ContentPlaceHolder öğesine erişmek için ana sayfanın bir başvurusunu almak üzere `FindControl("ctl00")` kullanmak yerine `Page.Master.FindControl("MainContent")`de kullanabilirsiniz. `SubmitButton_Click` olay işleyicisini aşağıdaki kodla güncelleştirin:

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample11.vb)]

Bu kez, sayfayı bir tarayıcı ile ziyaret ederek, yaşını girerek ve "Gönder" düğmesine tıklamak, `Results` etiketinde iletiyi beklenen şekilde görüntüler.

[Kullanıcının yaşı etikette görüntülenir ![](control-id-naming-in-content-pages-vb/_static/image11.png)](control-id-naming-in-content-pages-vb/_static/image10.png)

**Şekil 06**: kullanıcının yaşı etikette görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](control-id-naming-in-content-pages-vb/_static/image12.png))

### <a name="recursively-searching-through-naming-containers"></a>Adlandırma kapsayıcılarında yinelemeli arama

Önceki kod örneğine, ana sayfadan `MainContent` ContentPlaceHolder denetimine başvuruldu ve sonra `MainContent`olan `Results` etiketi ve `Age` TextBox denetimleri, `Control.FindControl` yönteminin yalnızca *denetimin*adlandırma kapsayıcısı içinde arama yaptığından oluşur. İki farklı adlandırma kapsayıcılarındaki iki denetim aynı `ID` değerine sahip olabileceğinden, adlandırma kapsayıcısı içinde `FindControl` olması çoğu senaryo açısından anlamlı hale gelir. TemplateFields içinde `ProductName` adlı bir etiket Web denetimi tanımlayan bir GridView 'un durumunu göz önünde bulundurun. Veriler GridView 'a çalışma zamanında bağlandığında her GridView satırı için bir `ProductName` etiketi oluşturulur. `FindControl` tüm adlandırma kapsayıcılarında arama yaptıysanız ve `Page.FindControl("ProductName")`çağırdık, `FindControl` hangi etiket örneği döndürmelidir? İlk GridView satırındaki `ProductName` etiketi mi? Son satırdaki bir tane?

`Control.FindControl` arama yalnızca *denetimin*adlandırma kapsayıcısı çoğu durumda daha anlamlı hale gelir. Ancak, tüm adlandırma kapsayıcıları genelinde benzersiz bir `ID` olduğu ve bir denetime erişmek için denetim hiyerarşisindeki her adlandırma kapsayıcısına daha fazla başvuru yapmaktan kaçınmak isteyen, bizim gibi başka durumlar da vardır. Tüm adlandırma kapsayıcılarını özyinelemeli olarak arayan `FindControl` bir değişken olması çok anlamlı olur. Ne yazık ki .NET Framework böyle bir yöntemi içermez.

İyi haber, tüm adlandırma kapsayıcılarını özyinelemeli olarak arayan kendi `FindControl` yöntemi oluşturabileceğiz. Aslında, *genişletme yöntemlerini* kullanarak, var olan `FindControl` yöntemine eşlik etmek için `Control` sınıfına `FindControlRecursive` bir yöntemi üzerinde Raptiye yapabilirsiniz.

> [!NOTE]
> Uzantı yöntemleri, 3,5 ve Visual Studio C# 2008 .NET Framework sürümü ile birlikte gelen diller Visual Basic 3,0 ve 9 ' a yeni bir özelliktir. Kısaca uzantı yöntemleri, bir geliştiricinin özel bir sözdizimi aracılığıyla mevcut bir sınıf türü için yeni bir yöntem oluşturmasına izin verir. Bu yardımcı özellik hakkında daha fazla bilgi için, [uzantı yöntemleriyle temel tür Işlevselliğini genişleterek](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)makaleme bakın.

Uzantı yöntemini oluşturmak için, `PageExtensionMethods.vb`adlı `App_Code` klasöre yeni bir dosya ekleyin. `controlID`adlı bir `String` parametresi girişi olarak alan `FindControlRecursive` adlı bir uzantı yöntemi ekleyin. Uzantı yöntemlerinin düzgün çalışması için, sınıfın bir `Module` olarak işaretlenmesi ve genişletme yöntemlerinin `<Extension()>` özniteliğiyle ön eki olması çok önemlidir. Üstelik, tüm genişletme yöntemleri, ilk parametresi olarak Uzantı yönteminin uygulandığı türün bir nesnesi olarak kabul etmelidir.

Bu `Module` ve `FindControlRecursive` uzantısı yöntemini tanımlamak için aşağıdaki kodu `PageExtensionMethods.vb` dosyasına ekleyin:

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample12.vb)]

Bu kodla birlikte `IDIssues.aspx` sayfanın arka plan kod sınıfına dönün ve geçerli `FindControl` yöntemi çağrılarını not edin. Bunları `Page.FindControlRecursive("controlID")`çağrılarıyla değiştirin. Uzantı yöntemleriyle ilgili yenilikler, doğrudan IntelliSense açılan listelerinde görünürler. Şekil 7 ' de gösterildiği gibi, `Page` yazdığınızda ve sonra da nokta tuşuna bastığınızda, `FindControlRecursive` yöntemi diğer `Control` sınıfı yöntemleriyle birlikte IntelliSense açılır.

[![uzantısı yöntemleri, IntelliSense açılır listeleri 'ne dahildir](control-id-naming-in-content-pages-vb/_static/image14.png)](control-id-naming-in-content-pages-vb/_static/image13.png)

**Şekil 07**: uzantı yöntemleri, IntelliSense açılan listeleri 'ne dahildir ([tam boyutlu görüntüyü görüntülemek için tıklayın](control-id-naming-in-content-pages-vb/_static/image15.png))

`SubmitButton_Click` olay işleyicisine aşağıdaki kodu girin ve ardından sayfayı ziyaret ederek, yaşınızı girerek ve "Gönder" düğmesine tıklayarak test edin. Şekil 6 ' da gösterildiği gibi, sonuçta elde edilen çıktı, "yaş yıllardır!" iletisi olacaktır.

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample13.vb)]

> [!NOTE]
> Uzantı yöntemleri C# 3,0 ve Visual Basic 9 ' a yeni olduklarından, Visual Studio 2005 kullanıyorsanız uzantı yöntemlerini kullanamazsınız. Bunun yerine, `FindControlRecursive` yöntemini bir yardımcı sınıfında uygulamanız gerekir. [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx) , blog gönderisine, [ASP.net Maser sayfalarına ve `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)bir örnektir.

## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>4\. Adım: Istemci tarafı betikte doğru`id`öznitelik değerini kullanma

Bu öğreticinin giriş bölümünde belirtildiği gibi, bir Web denetiminin işlenmiş `id` özniteliği, belirli bir HTML öğesine programlı bir şekilde başvurmak için istemci tarafı betikte kullanılan kullanım zamanıdır. Örneğin, aşağıdaki JavaScript `id` bir HTML öğesine başvurur ve sonra değerini bir kalıcı ileti kutusunda görüntüler:

[!code-csharp[Main](control-id-naming-in-content-pages-vb/samples/sample14.cs)]

ASP.NET sayfalarında bir adlandırma kapsayıcısı içermeyen, işlenmiş HTML öğesinin `id` özniteliği Web denetiminin `ID` Özellik değeri ile aynı olduğunu hatırlayın. Bu nedenle, `id` öznitelik değerleri ile JavaScript koduna sabit koda sahiptir. Diğer bir deyişle, `Age` metin kutusu Web denetimine istemci tarafı komut dosyası aracılığıyla erişmek istediğinizi biliyorsanız, bunu `document.getElementById("Age")`çağrısı aracılığıyla yapın.

Bu yaklaşımda sorun, ana sayfalar (veya diğer adlandırma kapsayıcı denetimleri) kullanılırken, işlenmiş HTML `id` Web denetiminin `ID` özelliği ile eş anlamlı olmadığı bir sorundur. İlk eğim, sayfayı bir tarayıcı aracılığıyla ziyaret edip gerçek `id` özniteliğini belirleyecek kaynağı görüntüleyebiliriz. İşlenmiş `id` değerini öğrendikten sonra, istemci tarafı komut dosyası aracılığıyla birlikte çalışmanız gereken HTML öğesine erişmek için `getElementById` çağrısına yapıştırabilirsiniz. Bu yaklaşım ideal olandan daha küçüktür çünkü sayfanın denetim hiyerarşisinde veya adlandırma denetimlerinin `ID` özelliklerinde yapılan değişiklikler, elde edilen `id` özniteliğini değiştirecek ve böylece JavaScript kodunuzu bozacaktır.

İyi haber, işlenen `id` öznitelik değerinin Web denetiminin [`ClientID` özelliği](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)aracılığıyla sunucu tarafı kodda erişilebilir olması. İstemci tarafı betikte kullanılan `id` öznitelik değerini öğrenmek için bu özelliği kullanmanız gerekir. Örneğin, bu sayfaya bir JavaScript işlevi eklemek için, çağrıldığında, `Age` metin kutusunun değerini bir kalıcı ileti kutusunda görüntüler, `Page_Load` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-vb[Main](control-id-naming-in-content-pages-vb/samples/sample15.vb)]

Yukarıdaki kod, `Age` TextBox 'ın `ClientID` özelliğinin değerini `getElementById`için JavaScript çağrısına çıkartır. Bu sayfayı bir tarayıcı aracılığıyla ziyaret ederseniz ve HTML kaynağını görüntülediğinizde, aşağıdaki JavaScript kodunu bulacaksınız:

[!code-html[Main](control-id-naming-in-content-pages-vb/samples/sample16.html)]

`ctl00_MainContent_Age``id` özniteliği değerinin `getElementById`çağrısı içinde nasıl göründüğünü unutmayın. Bu değer çalışma zamanında hesaplandığı için, sayfa denetimi hiyerarşisinde daha sonraki değişikliklerden bağımsız olarak da kullanılır.

> [!NOTE]
> Bu JavaScript örneği yalnızca bir sunucu denetimi tarafından işlenen HTML öğesine doğru şekilde başvuran bir JavaScript işlevinin nasıl ekleneceğini gösterir. Bu işlevi kullanmak için, belge yüklendiğinde veya belirli bir kullanıcı eylemi transpires olduğunda işlevi çağırmak için ek JavaScript yazmak gerekir. Bu ve ilgili konular hakkında daha fazla bilgi için, [Istemci tarafı betiği Ile çalışma](https://msdn.microsoft.com/library/aa479302.aspx)makalesini okuyun.

## <a name="summary"></a>Özet

Bazı ASP.NET Server denetimleri, kendi alt denetimlerinin işlenmiş `id` öznitelik değerlerini ve `FindControl` yöntemi tarafından canvassed 'ın kapsamını etkileyen adlandırma kapsayıcıları olarak davranır. Ana sayfaların yanı sıra, ana sayfanın kendisi ve ContentPlaceHolder denetimleri adlandırma kapsayıcılarıdır. Sonuç olarak, `FindControl`kullanarak içerik sayfası içindeki denetimlere programlı bir şekilde daha fazla iş yerleştirmemiz gerekir. Bu öğreticide, iki teknik inceliyoruz: ContentPlaceHolder denetimine detaya gitme ve `FindControl` metodunu çağırma. ve tüm adlandırma kapsayıcılarında yinelemeli olarak arama yapan `FindControl` kendi uygulamamızı yuvarlama.

Sunucu tarafı sorunları adlandırma kapsayıcılarının yanı sıra, Web denetimlerine başvurmayla ilgili olarak, istemci tarafı sorunları da vardır. Adlandırma kapsayıcıları yokluğunda, Web denetiminin `ID` Özellik değeri ve işlenmiş `id` öznitelik değeri aynı bir değerdir. Ancak, adlandırma kapsayıcısının eklenmesiyle, işlenen `id` özniteliği Web denetiminin hem `ID` değerlerini hem de denetim hiyerarşisinin aile içindeki adlandırma kapsayıcısını içerir. Bu adlandırma sorunları, Web denetiminin `ClientID` özelliğini kullandığınız ve istemci tarafı betikinizdeki işlenmiş `id` öznitelik değerini belirlemede olduğu sürece bir sorun değildir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET ana sayfaları ve `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [Dinamik veri girişi kullanıcı arabirimleri oluşturma](https://msdn.microsoft.com/library/aa479330.aspx)
- [Uzantı yöntemleriyle temel tür Işlevselliğini genişletme](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [Nasıl yapılır: ASP.NET ana sayfa Içeriğine başvurma](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [Mater sayfaları: Ipuçları, püf noktaları ve tuzaklar](http://www.odetocode.com/articles/450.aspx)
- [Istemci tarafı betiği ile çalışma](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticiye yönelik lider gözden geçirenler Zack Jones ve Suçi Barnerjee. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](urls-in-master-pages-vb.md)
> [İleri](interacting-with-the-master-page-from-the-content-page-vb.md)
