---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: ASP.NET AJAX ile kısmi sayfa güncelleştirmelerini anlama | Microsoft Docs
author: scottcate
description: ASP.NET AJAX uzantılarının en belirgin özelliği, t 'ye tam geri gönderme yapmadan kısmi veya artımlı bir sayfa güncelleştirmesi yapma yeteneğidir...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4b87cb8f58dbd7f27b16bcb0d488ff361770d4fe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545971"
---
# <a name="understanding-partial-page-updates-with-aspnet-ajax"></a>ASP.NET AJAX ile Kısmi Sayfa Güncelleştirmelerini Anlama

[Scott](https://github.com/scottcate) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> ASP.NET AJAX uzantılarının en iyi görünür özelliği, bir kod değişikliği ve en az biçimlendirme değişikliği olmadan, sunucuya tam bir geri gönderim yapmadan kısmi veya artımlı bir sayfa güncelleştirmesi yapma olanağıdır. Avantajlar kapsamlıdır: çoklu ortamlarınızın (Adobe Flash veya Windows Media gibi) durumu değiştirilmez, bant genişliği maliyetleri azalır ve istemci, genellikle geri gönderme ile ilişkili titreşimi etkilemez.

## <a name="introduction"></a>Giriş

Microsoft 'un ASP.NET teknolojisi, nesne odaklı ve olay odaklı bir programlama modeli sağlar ve derlenmiş kodun avantajları ile birleştirir. Ancak, sunucu tarafı işleme modelinin teknolojide birçok Sakıncaı vardır:

- Sayfa güncelleştirmeleri, sunucuya bir sayfa yenilemesi gerektiren gidiş dönüş gerektirir.
- Gidiş-dönüş, JavaScript veya diğer istemci tarafı teknolojileri (Adobe Flash gibi) tarafından oluşturulan etkileri kalıcı olarak sürdürmez
- Geri gönderme sırasında Microsoft Internet Explorer dışındaki tarayıcılar, kaydırma konumunu otomatik olarak geri yüklemeyi desteklemez. Internet Explorer 'da bile, sayfa yenilenmeye devam eden bir titreşim de vardır.
- Geri göndermeler, \_\_VIEWSTATE form alanı, özellikle GridView denetimi veya repeaters gibi denetimlerle ilgilenirken genişleyebileceği kadar yüksek miktarda bant genişliğine sahip olabilir.
- JavaScript veya diğer istemci tarafı teknolojisiyle Web hizmetlerine erişmek için birleştirilmiş bir model yoktur.

Microsoft 'un ASP.NET AJAX uzantılarını girin. **Bir** ND **X** ml için **zaman** uyumlu **J** Avascrıpt temsil eden Ajax, Microsoft AJAX çerçevesini kapsayan sunucu tarafı koddan ve Microsoft Ajax betik kitaplığı adlı bir betik bileşeninden oluşan, platformlar arası JavaScript aracılığıyla artımlı sayfa güncelleştirmeleri sağlamaya yönelik tümleşik bir çerçevedir. ASP.NET AJAX Uzantıları, JavaScript aracılığıyla ASP.NET Web hizmetlerine erişim için platformlar arası destek de sağlar.

Bu Teknik İnceleme, ScriptManager bileşenini, UpdatePanel denetimini ve UpdateProgress denetimini içeren ASP.NET AJAX uzantılarının kısmi sayfa güncelleştirme işlevlerini inceler ve bunların olmaması ya da olmaması gereken senaryoları dikkate alır kullanılan.

Bu Teknik İnceleme, Visual Studio 2008 Beta 2 sürümüne ve ASP.NET AJAX uzantılarını temel sınıf kitaplığı 'nda tümleştiren .NET Framework 3,5 ' dir. Bu, daha önce ASP.NET 2,0 için kullanılabilir bir eklenti bileşenidir. Bu Teknik İnceleme, Visual Studio 2008 kullandığınızı ve Visual Web Developer Express Edition 'ı kullandığınızı varsayar; başvurulan bazı proje şablonları, Visual Web Developer Express kullanıcıları tarafından kullanılamayabilir.

## <a name="partial-page-updates"></a>Kısmi sayfa güncelleştirmeleri

ASP.NET AJAX uzantılarının en iyi görünür özelliği, bir kod değişikliği ve en az biçimlendirme değişikliği olmadan, sunucuya tam bir geri gönderim yapmadan kısmi veya artımlı bir sayfa güncelleştirmesi yapma olanağıdır. Avantajlar oldukça-çoklu ortamlarınızın (Adobe Flash veya Windows Media gibi) durumu değiştirilmez, bant genişliği maliyetleri azalır ve istemci, genellikle geri gönderme ile ilişkili titreşimle karşılaşmaz.

Kısmi sayfa işlemeyi tümleştirme özelliği, projenizde en az değişiklikle ASP.NET ile tümleşiktir.

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>İzlenecek yol: kısmi Işlemeyi varolan bir projeyle tümleştirme

1. Microsoft Visual Studio 2008 ' de, <em>dosya</em> <em>-&gt; Yeni</em> <em>-&gt; Web sitesi</em> ' ne giderek ve iletişim kutusundan ASP.NET Web sitesi ' ni seçerek yeni bir ASP.NET Web sitesi projesi oluşturun. İstediğiniz gibi adlandırabilirsiniz ve bunu dosya sistemine veya Internet Information Services (IIS) ' e yükleyebilirsiniz.
2. Temel ASP.NET işaretlemesi (sunucu tarafı form ve bir `@Page` yönergesi) ile boş bir varsayılan sayfa sunulur. `Label1` adlı bir etiketi ve `Button1` adlı bir düğmeyi form öğesi içindeki sayfaya bırakın. Metin özelliklerini dilediğiniz şekilde ayarlayabilirsiniz.
3. Tasarım görünümü ' de, arka plan kod işleyicisi oluşturmak için `Button1` ' a çift tıklayın. Bu olay işleyicisi içinde, düğmesine tıklandınız `Label1.Text` ayarlayın! arasında yetersiz alanla karşılaştı.

**Listeleme 1: Kısmi işleme etkinleştirilmeden önce default. aspx için biçimlendirme etkin**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**Listeleme 2: default.aspx.cs içinde codebehind (kırpılmış)**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. Web sitenizi başlatmak için F5 tuşuna basın. Visual Studio, hata ayıklamayı etkinleştirmek için Web. config dosyası eklemenizi ister; Bunu yapın. Düğmeye tıkladığınızda, sayfanın etiketteki metni değiştirmek için yenilendiğine ve sayfa yeniden çizildikçe kısa bir titreşim olduğuna dikkat edin.
2. Tarayıcı pencerenizi kapattıktan sonra, Visual Studio 'ya ve işaretleme sayfasına dönün. Visual Studio araç kutusu 'nda aşağı kaydırın ve AJAX Uzantıları etiketli sekmeyi bulun. (AJAX veya Atlas uzantılarının daha eski bir sürümünü kullandığınız için bu sekmeye sahip değilseniz, bu teknik incelemeye daha sonra AJAX Uzantıları araç kutusu öğelerini kaydetme kılavuzunuza bakın veya Windows Installer indirilebilen geçerli sürümü yükleyebilirsiniz Web sitesinden).

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png))

1. <em>Bilinen sorun:</em> Visual Studio 2008 ' yi zaten ASP.NET 2,0 AJAX uzantılarıyla yüklenmiş Visual Studio 2005 ' nin yüklü olduğu bir bilgisayara yüklerseniz, Visual Studio 2008, AJAX Uzantıları araç kutusu öğelerini içeri aktarır. Bileşenlerin araç ipucunu inceleyerek bunun durum olup olmadığını belirleyebilirsiniz; Sürüm 3.5.0.0 söylemelidir. 2\.0.0.0 sürümü varsa, eski araç kutusu öğelerinizi içeri aktarırsınız ve Visual Studio 'daki araç kutusu öğelerini Seç iletişim kutusunu kullanarak el ile içeri aktarılmaları gerekir. Tasarımcı aracılığıyla sürüm 2 denetimleri ekleyemeyecektir.

2. `<asp:Label>` etiketi başlamadan önce, bir boşluk satırı oluşturun ve araç kutusunda UpdatePanel denetimine çift tıklayın. Sayfanın üst kısmına, System. Web. UI ad alanı içindeki denetimlerin `asp:` öneki kullanılarak içeri aktarıldığını belirten yeni bir `@Register` yönergesinin ekleneceğini unutmayın.
3. Düğme öğesinin sonundaki kapanış `</asp:UpdatePanel>` etiketini sürükleyin, böylece öğe etiket ve düğme denetimleriyle sarmalanmış şekilde doğru oluşturulur.
4. Açma `<asp:UpdatePanel>` etiketinden sonra yeni bir etiket açmaya başlayın. IntelliSense 'in size iki seçenek girmesini istediğinizi unutmayın. Bu durumda, bir `<ContentTemplate>` etiketi oluşturun. Biçimlendirmenin doğru biçimlendirildiğinden emin olmak için bu etiketi etiketinizin ve Düğinizin etrafında sarmalayın.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png))

1. `<form>` öğesi içinde herhangi bir yerde, araç kutusundaki `ScriptManager` öğesine çift tıklayarak bir ScriptManager denetimi ekleyin.
2. `<asp:ScriptManager>` etiketini, `EnablePartialRendering= true`özniteliğini içerecek şekilde düzenleyin.

**Listeleme 3: varsayılan. aspx için kısmi işleme etkinken biçimlendirme**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. Web. config dosyanızı açın. Visual Studio 'Nun System. Web. Extensions. dll dosyasına otomatik olarak bir derleme başvurusu eklediğini unutmayın.

1. Visual Studio 2008 ' deki yenilikler: ASP.NET Web sitesi proje şablonlarıyla birlikte gelen Web. config, ASP.NET AJAX uzantılarına gereken tüm başvuruları otomatik olarak içerir ve olabilecek yapılandırma bilgilerinin açıklamalı bölümlerini içerir ek işlevselliği etkinleştirmek için açıklama kaldırıldı. ASP.NET 2,0 AJAX Uzantıları yüklendiğinde Visual Studio 2005 benzer şablonlar içeriyordu. Ancak, Visual Studio 2008 ' de, AJAX uzantıları varsayılan olarak kabul edilir (diğer bir deyişle, varsayılan olarak başvurulur, ancak başvuru olarak kaldırılabilirler).

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png))

1. Web sitenizi başlatmak için F5 tuşuna basın. Kısmi işlemeyi desteklemek için kaynak kodu değişikliklerinin nasıl gerekmediğini ve yalnızca biçimlendirmenin değiştirildiğini aklınızda yapın.

Web sitenizi başlattığınızda, bu düğmeye tıkladığınızda bir titreşimi yok ya da sayfa kaydırma konumunda herhangi bir değişiklik olacak şekilde (Bu örnek bunu göstermez), kısmi işlemenin etkin olduğunu görmeniz gerekir. Düğmeye tıkladıktan sonra sayfanın işlenmiş kaynağına bakadıysanız, aslında geri gönderme gerçekleşmediğinden emin olur; özgün etiket metni hala kaynak biçimlendirmesinin bir parçası ve etiket JavaScript aracılığıyla değiştirilmiştir.

Visual Studio 2008, ASP.NET AJAX özellikli bir Web sitesi için önceden tanımlanmış bir şablonla birlikte görünüyor. Ancak, Visual Studio 2005 ve ASP.NET 2,0 AJAX Uzantıları yüklenmişse bu tür bir şablon Visual Studio 2005 içinde mevcuttur. Sonuç olarak, bir Web sitesi yapılandırmak ve AJAX özellikli Web sitesi şablonuyla başlamak büyük olasılıkla daha da kolay olur, çünkü şablon tam olarak yapılandırılmış bir Web. config dosyası (Web Hizmetleri erişimi de dahil olmak üzere tüm ASP.NET AJAX uzantılarını destekler). ve JSON serileştirme-JavaScript Nesne Gösterimi) ve varsayılan olarak ana Web Forms sayfası içinde bir UpdatePanel ve ContentTemplate içerir. Bu varsayılan sayfa ile kısmi işlemenin etkinleştirilmesi, Bu izlenecek yolun 10. adımını yeniden ziyaret etme ve denetimleri sayfaya bırakma kadar basittir.

## <a name="the-scriptmanager-control"></a>ScriptManager denetimi

## <a name="scriptmanager-control-reference"></a>ScriptManager denetim başvurusu

Biçimlendirme etkin özellikler:

| **Özellik adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| AllowCustomErrors-yeniden yönlendirme | Bool | Hataları işlemek için Web. config dosyasının özel hata bölümünün kullanılıp kullanılmayacağını belirtir. |
| AsyncPostBackError-Ileti | Dize | Bir hata ortaya çıktığında istemciye gönderilen hata iletisini alır veya ayarlar. |
| AsyncPostBack-zaman aşımı | Int32 | İstemcinin zaman uyumsuz isteğin tamamlanmasını beklemesi gereken varsayılan süreyi alır veya ayarlar. |
| ENABLESCRIPT-Genelleştirme | Bool | Betik genelleştirmesi 'nin etkinleştirilip etkinleştirilmeyeceğini alır veya ayarlar. |
| ENABLESCRIPT-yerelleştirme | Bool | Betik yerelleştirmenin etkinleştirilip etkinleştirilmediğini alır veya ayarlar. |
| ScriptLoadTimeout | Int32 | İstemciye betikleri yüklemeye izin verilen saniye sayısını belirler |
| ScriptMode | Sabit Listesi (otomatik, hata ayıklama, yayın, devralma) | Betiklerin yayın sürümlerinin oluşturulup oluşturulmayacağını alır veya ayarlar |
| ScriptPath | Dize | İstemciye gönderilecek betik dosyalarının konumunun kök yolunu alır veya ayarlar. |

Yalnızca kod özellikleri:

| **Özellik adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-yönetici | İstemciye gönderilecek ASP.NET kimlik doğrulama hizmeti proxy 'si hakkındaki ayrıntıları alır. |
| Ihata ayıklama Ggingenabled | Bool | Betik ve kod hata ayıklamanın etkinleştirilip etkinleştirilmeyeceğini alır. |
| IsInAsyncPostback | Bool | Sayfanın Şu anda zaman uyumsuz bir geri gönderme isteği içinde olup olmadığını alır. |
| ProfileService | ProfileService-yönetici | İstemciye gönderilecek ASP.NET profil oluşturma hizmeti proxy 'si hakkındaki ayrıntıları alır. |
| Komut dosyaları | Koleksiyon&lt;betiği başvurusu&gt; | İstemciye gönderilecek bir betik başvuruları koleksiyonunu alır. |
| Hizmetler | Koleksiyon&lt;hizmeti-başvuru&gt; | İstemciye gönderilecek Web hizmeti proxy başvuruları koleksiyonunu alır. |
| SupportsPartialRendering | Bool | Geçerli istemcinin kısmi işlemeyi destekleyip desteklemediğini alır. Bu özellik **false**döndürürse, tüm sayfa istekleri standart geri göndermeler olur. |

Ortak kod yöntemleri:

| **Yöntem adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| SetFocus (dize) | Kağıt | İstek tamamlandığında istemcinin odağını belirli bir denetime ayarlar. |

Biçimlendirme alt öğeleri:

| **Tag** | **Açıklama** |
| --- | --- |
| &lt;AuthenticationService&gt; | Proxy hakkında ASP.NET kimlik doğrulama hizmetine ilişkin ayrıntıları sağlar. |
| &lt;ProfileService&gt; | ASP.NET profil oluşturma hizmetine ara sunucu hakkında ayrıntılar sağlar. |
| &lt;Betikler&gt; | Ek betik başvuruları sağlar. |
| &lt;ASP: ScriptReference&gt; | Belirli bir betik başvurusunu gösterir. |
| &lt;Hizmet&gt; | Proxy sınıfları oluşturulacak ek Web hizmeti başvuruları sağlar. |
| &lt;ASP: ServiceReference&gt; | Belirli bir Web hizmeti başvurusunu gösterir. |

ScriptManager denetimi, ASP.NET AJAX uzantıları için temel temeldir. Betik kitaplığına (yaygın istemci tarafı komut dosyası türü sistemi dahil) erişim sağlar, kısmi işlemeyi destekler ve ek ASP.NET Hizmetleri (kimlik doğrulaması ve profil oluşturma ve diğer Web Hizmetleri gibi) için kapsamlı destek sağlar. ScriptManager denetimi, istemci betikleri için Genelleştirme ve yerelleştirme desteği de sağlar.

## <a name="providing-alternative-and-supplemental-scripts"></a>Alternatif ve ek betikler sağlama

Microsoft ASP.NET 2,0 AJAX uzantıları hem hata ayıklama hem de sürüm sürümlerindeki tüm betik kodunu, başvurulan derlemelere gömülü kaynaklar olarak içerirken, geliştiriciler ScriptManager 'ı özelleştirilmiş betik dosyalarına yeniden yönlendirmek ve kaydetmek için ücretsizdir ek gerekli betikler.

Genellikle dahil edilen betikler için varsayılan bağlamayı (sys. WebForms Ad alanını ve özel yazma sistemini destekleyen olanlar gibi) geçersiz kılmak için, ScriptManager sınıfının `ResolveScriptReference` olayına kaydolabilirsiniz. Bu yöntem çağrıldığında, olay işleyicisi, söz konusu komut dosyasının yolunu değiştirme fırsatına sahiptir; betik Yöneticisi daha sonra komut dosyalarının farklı veya özelleştirilmiş bir kopyasını istemciye gönderir.

Ayrıca, komut dosyası başvuruları (`ScriptReference` sınıfı tarafından temsil edilir) program aracılığıyla veya biçimlendirme aracılığıyla dahil edilebilir. Bunu yapmak için `ScriptManager.Scripts` koleksiyonunu programlı olarak değiştirin ya da ScriptManager denetiminin ilk düzey alt öğesi olan `<Scripts>` etiketinin altına `<asp:ScriptReference>` etiketleri ekleyin.

## <a name="custom-error-handling-for-updatepanels"></a>UpdatePanel için özel hata Işleme

Güncelleştirmeler UpdatePanel denetimleri tarafından belirtilen Tetikleyiciler tarafından işlense de, hata işleme ve özel hata iletileri desteği bir sayfanın ScriptManager denetim örneği tarafından işlenir. Bu, daha sonra özel özel durum işleme mantığı sağlayabilen bir olay, `AsyncPostBackError`ve sayfa ortaya çıkararak yapılır.

AsyncPostBackError olayını tüketerek `AsyncPostBackErrorMessage` özelliğini belirtebilir, bu, geri çağırma tamamlandıktan sonra bir uyarı kutusunun oluşturulmasına neden olur.

Varsayılan uyarı kutusunun kullanılması yerine istemci tarafı özelleştirmesi da mümkündür; Örneğin, varsayılan tarayıcı kalıcı iletişim kutusu yerine özelleştirilmiş bir `<div>` öğesi göstermek isteyebilirsiniz. Bu durumda, istemci komut dosyasında hatayı işleyebilirsiniz:

**Listeleme 5: özel hataları göstermek için Istemci tarafı betiği**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

Yalnızca, Yukarıdaki betik, zaman uyumsuz isteğin tamamlandığı zaman için istemci tarafı AJAX çalışma zamanına bir geri çağırma kaydeder. Daha sonra bir hatanın raporlanıp raporlanmadığını denetler ve bu durumda, son olarak hatanın özel betikte işlendiği çalışma zamanına işaret eden ayrıntılarını işler.

## <a name="globalization-and-localization-support"></a>Genelleştirme ve yerelleştirme desteği

ScriptManager denetimi, komut dosyası dizelerinin ve Kullanıcı arabirimi bileşenlerinin yerelleştirilmesi için kapsamlı destek sağlar; Ancak bu konu, bu teknik incelemeye ait kapsamın dışındadır. Daha fazla bilgi için bkz. ASP.NET AJAX uzantılarında genelleştirme desteği.

## <a name="the-updatepanel-control"></a>UpdatePanel denetimi

## <a name="updatepanel-control-reference"></a>UpdatePanel denetim başvurusu

Biçimlendirme etkin özellikler:

| **Özellik adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| ChildrenAsTriggers | bool | Alt denetimlerin geri gönderme sırasında yenilemeyi otomatik olarak çağırmayacağını belirtir. |
| RenderMode | Enum (blok, satır Içi) | İçeriğin görsel olarak sunulama şeklini belirtir. |
| UpdateMode | Enum (her zaman, koşullu) | UpdatePanel 'ın kısmi bir işleme sırasında her zaman yenilenmesini mi yoksa yalnızca bir tetikleyici isabet edildiğinde yenilenmesini mi istediğinizi belirtir. |

Yalnızca kod özellikleri:

| **Özellik adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| Ipartialrendering | bool | UpdatePanel 'ın geçerli istek için kısmi işlemeyi destekleyip desteklemediğini alır. |
| ContentTemplate | ITemplate | Güncelleştirme isteği için biçimlendirme şablonunu alır. |
| ContentTemplateContainer | Denetim | Güncelleştirme isteği için programlı şablonu alır. |
| Tetikleyiciler | UpdatePanel-TriggerCollection | Geçerli UpdatePanel ile ilişkili tetikleyicilerin listesini alır. |

Ortak kod yöntemleri:

| **Yöntem adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| Update () | Kağıt | Belirtilen UpdatePanel 'ı programlı olarak güncelleştirir. Bir sunucu isteğinin, aksi takdirde tetiklenmiş bir UpdatePanel 'ın kısmi işlemesini tetiklemesine olanak sağlar. |

Biçimlendirme alt öğeleri:

| **Tag** | **Açıklama** |
| --- | --- |
| &lt;ContentTemplate&gt; | Kısmi işleme sonucunu işlemek için kullanılacak biçimlendirmeyi belirtir. &lt;ASP: UpdatePanel&gt;alt öğesi. |
| &lt;Tetikleyiciler&gt; | Bu UpdatePanel 'ın güncelleştirilmesiyle ilişkili *n* denetim koleksiyonunu belirtir. &lt;ASP: UpdatePanel&gt;alt öğesi. |
| &lt;ASP: AsyncPostBackTrigger&gt; | Verilen UpdatePanel için kısmi sayfa işlemeyi çağıran bir tetikleyiciyi belirtir. Bu, söz konusu UpdatePanel 'ın alt öğesi olarak bir denetim olmayabilir veya olmayabilir. Olay adının ayrıntılı olması. &lt;tetikleyicilerinin alt öğesi&gt;. |
| &lt;ASP: PostBackTrigger&gt; | Tüm sayfanın yenilenmesini sağlayan bir denetim belirtir. Bu, söz konusu UpdatePanel 'ın alt öğesi olarak bir denetim olmayabilir veya olmayabilir. Nesneyi ayrıntılı olarak. &lt;tetikleyicilerinin alt öğesi&gt;. |

`UpdatePanel` denetimi, AJAX uzantılarının kısmi işleme işlevselliğinde bir parçası olacak sunucu tarafı içeriğini sınırlandıran denetimdir. Bir sayfada olabilecek UpdatePanel denetimleri sayısı için bir sınır yoktur ve bunlar iç içe olabilir. Her bir UpdatePanel, her biri bağımsız olarak çalışacak şekilde yalıtılarak (aynı anda çalışan iki UpdatePanel, sayfanın geri gönderilerinden bağımsız olarak sayfanın farklı parçalarını işlemek için).

UpdatePanel denetimi birincil olarak denetim tetikleyicilerle ilgilenir. varsayılan olarak, bir UpdatePanel 'ın geri gönderme işlemi oluşturan `ContentTemplate` içinde yer alan tüm denetimler, UpdatePanel için bir tetikleyici olarak kaydedilir. Bu, UpdatePanel 'ın, Kullanıcı denetimleri ile, varsayılan veri bağlantılı denetimlerle (GridView gibi) çalışabileceği ve komut dosyasında programlanabilir olabileceği anlamına gelir.

Varsayılan olarak, kısmi sayfa işleme tetiklendiğinde, sayfada tüm UpdatePanel denetimleri yenilenir, bu da UpdatePanel, bu eylem için tanımlanan Tetikleyicileri denetler. Örneğin, bir UpdatePanel bir düğme denetimini tanımlıyorsa ve bu düğme denetimine tıklandığında, bu sayfadaki tüm UpdatePanel denetimleri varsayılan olarak yenilenir. Bunun nedeni, varsayılan olarak, UpdatePanel 'ın `UpdateMode` özelliği `Always`olarak ayarlanmıştır. Alternatif olarak, UpdateMode özelliğini `Conditional`olarak ayarlayabilirsiniz. Bu, UpdatePanel 'ın yalnızca belirli bir tetikleyici isabet edildiğinde yenileneceği anlamına gelir.

## <a name="custom-control-notes"></a>Özel denetim notları

Bir UpdatePanel, herhangi bir kullanıcı denetimine veya özel denetime eklenebilir; Ancak, bu denetimlerin dahil olduğu sayfa, EnablePartialRendering özelliği **true**olarak ayarlanmış bir ScriptManager denetimi de içermelidir.

Web özel denetimlerini kullanırken Bunun için hesap oluşturmanın bir yolu, `CompositeControl` sınıfının korunan `CreateChildControls()` yöntemini geçersiz kılmalıdır. Bunu yaparak, sayfanın kısmen işlemeyi desteklediğini belirlerseniz, denetimin alt öğeleri ve dış dünya arasına bir UpdatePanel ekleyebilirsiniz; Aksi takdirde, yalnızca alt denetimleri bir kapsayıcı `Control` örneğine katman haline getirebilirsiniz.

## <a name="updatepanel-considerations"></a>UpdatePanel konuları

UpdatePanel, bir siyah kutu olarak çalışır ve bir JavaScript XMLHttpRequest bağlamı içinde ASP.NET geri göndermeler sarmalama. Ancak, hem davranış hem de hız açısından göz önünde bulundurmanız gereken önemli performans konuları vardır. UpdatePanel 'ın nasıl çalıştığını anlamak için, kullanım için uygun olduğunda en iyi şekilde karar verebilmeniz için AJAX Exchange 'i incelemeniz gerekir. Aşağıdaki örnek, mevcut bir siteyi ve Firefirefox 'u Firebug uzantısıyla (Firebug, XMLHttpRequest verilerini yakalar) kullanır.

Diğer nesnelerin yanı sıra bir form veya denetimdeki şehir ve eyalet alanını doldurmanız beklenen bir posta kodu metin kutusu olduğunu düşünün. Bu form, son olarak kullanıcının adı, adresi ve iletişim bilgileri dahil olmak üzere üyelik bilgilerini toplar. Belirli bir projenin gereksinimlerine bağlı olarak dikkate alınması gereken birçok tasarım konusu vardır.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png))

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png))

Bu uygulamanın özgün yinelemesinde, posta kodu, şehir ve eyalet dahil olmak üzere Kullanıcı kayıt verilerinin tamamını kapsayan bir denetim oluşturulmuştur. Tüm denetim bir UpdatePanel içinde sarmalanmış ve bir Web formu üzerine bırakılmış. Posta kodu Kullanıcı tarafından girildiğinde, UpdatePanel olayı (Tetikleyicileri belirterek ya da ChildrenAsTriggers özelliğini true olarak ayarlayarak), arka uçta olayını algılar. AJAX, FireBug tarafından yakalanan şekilde UpdatePanel içindeki tüm alanları gönderir (sağdaki diyagrama bakın).

Ekran yakalama gösterdiği gibi, UpdatePanel içindeki her denetimin değeri (Bu durumda, hepsi boştur) ve ViewState alanı görüntülenir. Her türlü, bu belirli isteği yapmak için yalnızca beş bayt veri gerektiğinde, 9kb 'tan fazla veri gönderilir. Yanıt daha da daha fazla blok olur: Toplam, 57kb istemciye gönderilir, yalnızca bir metin alanını ve bir açılır alanı güncelleştirebilir.

Ayrıca, ASP.NET AJAX 'un sunumu nasıl güncelleştirdiklerini görmek de istenebilir. UpdatePanel 'ın Güncelleştirme isteğinin yanıt bölümü, sol tarafta, Firehata konsolunda görüntülenir; Bu, istemci betiği tarafından bölünen ve sonra sayfada yeniden birleştirilen, özel olarak formül ayrılmış bir dizedir. Özellikle, ASP.NET AJAX, UpdatePanel 'ı temsil eden istemcideki HTML öğesinin *InnerHtml* özelliğini ayarlar. Tarayıcı DOM 'ı yeniden oluşturduğunda, işlenmesi gereken bilgi miktarına bağlı olarak küçük bir gecikme olur.

DOM 'ın yeniden oluşturulması bir dizi ek sorunu tetikler:

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png))

- Odaklanmış HTML öğesi UpdatePanel içindeyse, odağı kaybeder. Bu nedenle, posta kodu metin kutusundan çıkmak üzere SEKME tuşuna basmış kullanıcılar için, bir sonraki hedefi şehir metin kutusu olacaktır. Ancak, UpdatePanel görüntüyü yeniledi, form artık odağa sahip olmaz ve Tab tuşuna basmak odak öğelerini (örneğin, bağlantılar) vurgulamaya başlamalıdır.
- DOM öğelerine erişen herhangi bir tür özel istemci tarafı komut dosyası kullanılıyorsa, kısmen geri gönderme sonrasında işlevlere göre kalıcı olan başvurular geçersiz hale gelebilir.

UpdatePanel, tüm çözümleri yakalamak üzere tasarlanmamıştır. Bunun yerine, prototipleme, küçük denetim güncelleştirmeleri dahil olmak üzere belirli durumlar için hızlı bir çözüm sağlar ve .NET nesne modeli hakkında tanıdık olabilecek ASP.NET geliştiricilere ve DOM ile daha az bu şekilde tanıdık bir arabirim sağlar. Uygulama senaryosuna bağlı olarak daha iyi performansa neden olabilecek çeşitli alternatifler vardır:

- PageMethods ve JSON kullanmayı düşünün (JavaScript Nesne Gösterimi), geliştiricinin bir Web hizmeti çağrısı çağrılmakta olduğu gibi bir sayfada statik yöntemleri çağırmasına izin verir. Yöntemler statik olduğu için hiçbir durum gerekli değildir; betik çağıran, parametreleri sağlar ve sonuç zaman uyumsuz olarak döndürülür.
- Tek bir denetimin bir uygulama genelinde birkaç yerde kullanılması gerekiyorsa, bir Web hizmeti ve JSON kullanmayı düşünün. Bu yeniden çok az özel iş gerektirir ve zaman uyumsuz olarak çalışır.

Web Hizmetleri veya sayfa yöntemleri aracılığıyla işlevselliği eklemek de dezavantajlara sahiptir. Birincisi ve foremost, ASP.NET geliştiricileri genellikle kullanıcı denetimlerine (. ascx dosyaları) küçük işlevsellik bileşenleri oluşturmaya eğilimlidir. Sayfa metotları bu dosyalarda barındırılamaz; Bunların gerçek. aspx sayfa sınıfında barındırılması gerekir. Benzer şekilde, Web Hizmetleri. asmx sınıfında barındırılmalıdır. Uygulamaya bağlı olarak, bu mimari tek sorumluluk Ilkesini ihlal edebilir, bu da tek bir bileşen için işlevselliğin artık çok fazla veya hiç bir bağlı olmayan iki veya daha fazla fiziksel bileşene yayılmasını sağlayabilir.

Son olarak, bir uygulama UpdatePanel 'in kullanılmasını gerektiriyorsa, aşağıdaki kılavuzlar sorun giderme ve bakım konusunda yardımcı olmalıdır.

- **Yalnızca birimler içinde değil, ancak kod birimleri boyunca, UpdatePanel 'i mümkün olduğunca az iç içe geçirebilirsiniz.** Örneğin, bir denetimi sarmalayan bir sayfada bir UpdatePanel varsa, bu denetim, bir UpdatePanel içeren başka bir denetimi içeren bir UpdatePanel da içerdiğinde, çapraz birim iç içe geçme olur. Bu, hangi öğelerin yenilenmesi gerektiğini açık tutmaya ve alt UpdatePanel için beklenmeyen yenilemelerin yapılmasını engeller.
- ***ChildrenAsTriggers* özelliğini false olarak ayarlayın ve tetikleme olaylarını açık olarak ayarlayın.** `<Triggers>` koleksiyonunun kullanılmasıyla olayları işlemek için çok daha net bir yoldur ve bakım görevlerine yardımcı olur ve bir geliştiricinin bir olay için kabul etmeyi zorlamaları zorunlu olabilir.
- **İşlevselliği başarmak için mümkün olan en küçük birimi kullanın.** Posta kodu hizmetinin tartışmasında belirtildiği gibi, yalnızca en düşük değeri kaydırma işlemi sunucuya, toplam işleme ve istemci-sunucu değişim parmak izine göre performansı artırır.

## <a name="the-updateprogress-control"></a>UpdateProgress denetimi

## <a name="updateprogress-control-reference"></a>UpdateProgress denetim başvurusu

Biçimlendirme etkin özellikler:

| **Özellik adı** | **Tür** | **Açıklama** |
| --- | --- | --- |
| Ilişkili güncelleştirme-PanelID | Dize | Bu UpdateProgress 'in rapor etmesi gereken UpdatePanel 'ın KIMLIĞINI belirtir. |
| DisplayAfter | int | Zaman uyumsuz istek başladıktan sonra bu denetim görüntülenmeden önce geçen süreyi milisaniye olarak belirtir. |
| DynamicLayout | bool | İlerleme durumunun dinamik olarak işlenip işlenmediğini belirtir. |

Biçimlendirme alt öğeleri:

| **Tag** | **Açıklama** |
| --- | --- |
| &lt;ProgressTemplate&gt; | Bu denetimle görüntülenecek içerik için ayarlanan denetim şablonunu içerir. |

UpdateProgress denetimi, kullanıcılara sunucuya aktarım yaparken gerekli işleri gerçekleştirirken ilgilendiğiniz bir geribildirim ölçüsü sağlar. Bu, özellikle de büyük bir şekilde durum çubuğunun vurgulanmasını ve bakmadığını görmek için, kullanıcılarınızın çok fazla şey yaptığını bilmesini sağlayabilir.

Bir notta, UpdateProgress denetimleri bir sayfa hiyerarşisinde herhangi bir yerde görünebilir. Ancak, kısmi geri gönderimin bir alt UpdatePanel 'dan başlatıldığı durumlarda (bir UpdatePanel 'ın başka bir UpdatePanel içinde iç içe olduğu durumlarda), alt UpdatePanel 'ı tetikleyen geri göndermeler, alt öğe için UpdateProgress şablonlarının görüntülenmesine neden olur UpdatePanel 'ın yanı sıra üst UpdatePanel. Ancak, tetikleyici üst UpdatePanel 'ın doğrudan bir alt öğesi ise, yalnızca üst öğeyle ilişkili UpdateProgress şablonları görüntülenir.

## <a name="summary"></a>Özet

Microsoft ASP.NET AJAX Uzantıları, Web içeriğinizi daha erişilebilir hale getirmenize ve Web uygulamalarınıza daha zengin bir kullanıcı deneyimi sağlamaya yardımcı olmak için tasarlanan gelişmiş ürünlerdir. ASP.NET AJAX uzantılarının bir parçası olarak, ScriptManager, UpdatePanel ve UpdateProgress denetimleri de dahil olmak üzere kısmi sayfa işleme denetimleri araç setinin en görünür bileşenlerinden bazılarıdır.

ScriptManager bileşeni, uzantılar için istemci JavaScript 'in sağlamasını tümleştirir ve ayrıca çeşitli sunucu ve istemci tarafı bileşenlerinin en düşük geliştirme yatırımıyla birlikte çalışmasını sağlar.

UpdatePanel denetimi, sunucu tarafı codebehind ve bir sayfa yenilemeyi tetikleyemeyebilir. UpdatePanel denetimleri iç içe olabilir ve diğer UpdatePanel denetimlerindeki denetimlere bağımlı olabilir. Varsayılan olarak, UpdatePanel alt denetimleri tarafından çağrılan geri göndermeler işler, ancak bu işlev bildirimli olarak veya programlı bir şekilde ayarlanabilir.

UpdatePanel denetimini kullanırken, geliştiriciler olası olabilecek performans etkilerine karşı farkında olmalıdır. Olası alternatifler Web Hizmetleri ve sayfa yöntemleri içerir, ancak uygulamanın tasarımı göz önünde bulundurulmalıdır.

UpdateProgress denetimi, kullanıcının olmadığını ve yok ettiğini ve sayfada kullanıcı girişine yanıt vermek için herhangi bir şey yapmamaya devam etmediğini bilmesini sağlar. Ayrıca, kısmi işleme sonuçlarını durdurma özelliğini de içerir.

Bu araçlar birlikte, sunucu Kullanıcı tarafından daha az görünür hale getirerek ve iş akışını daha düşük bir şekilde gerçekleştirerek zengin ve sorunsuz bir kullanıcı deneyimi oluşturmaya yardımcı olur.

## <a name="bio"></a>Biyografisi

Scott, 1997 tarihinden itibaren Microsoft Web teknolojileriyle çalışmaktadır ve Bilgi Bankası yazılım çözümlerine odaklanmış ASP.NET tabanlı uygulamalar yazma konusunda uzmanımız myKB.com ([www.myKB.com](http://www.myKB.com)) Başkan Yardımcısı. Scott 'da e-posta ile [scott.cate@myKB.com](mailto:scott.cate@myKB.com) veya blogundan [ScottCate.com](http://ScottCate.com) adresinden iletişim kurulabilirler

> [!div class="step-by-step"]
> [Next](understanding-asp-net-ajax-updatepanel-triggers.md)
