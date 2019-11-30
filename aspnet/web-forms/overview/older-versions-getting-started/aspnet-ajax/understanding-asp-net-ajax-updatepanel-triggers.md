---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: ASP.NET AJAX UpdatePanel tetikleyicilerini anlama | Microsoft Docs
author: scottcate
description: Visual Studio 'da biçimlendirme düzenleyicisinde çalışırken, bir UpdatePanel denetiminin iki alt öğesi olduğunu fark edebilirsiniz (IntelliSense 'den). Bir wh...
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: b1cc869f373d4f8283b4d92af74707c3f11fef61
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588806"
---
# <a name="understanding-aspnet-ajax-updatepanel-triggers"></a>ASP.NET AJAX UpdatePanel Tetikleyicilerini Anlama

[Scott](https://github.com/scottcate) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Visual Studio 'da biçimlendirme düzenleyicisinde çalışırken, bir UpdatePanel denetiminin iki alt öğesi olduğunu fark edebilirsiniz (IntelliSense 'den). Bunlardan biri, sayfada bulunan denetimleri belirten (veya kullanıyorsanız Kullanıcı denetimi), öğenin bulunduğu UpdatePanel denetiminin kısmi bir işlemesini tetikleyecek Tetikleyiciler öğesidir.

## <a name="introduction"></a>Giriş

Microsoft 'un ASP.NET teknolojisi, nesne odaklı ve olay odaklı bir programlama modeli sağlar ve derlenmiş kodun avantajları ile birleştirir. Ancak, sunucu tarafı işleme modelinin, teknolojide bulunan birçok Sakıncaı vardır ve bunların birçoğu Microsoft ASP.NET 3,5 AJAX uzantılarında eklenen yeni özellikler tarafından çözülebilir. Bu uzantılar, tam sayfa yenilemesi gerektirmeden sayfaların kısmi işlenmesi, istemci betiği (ASP.NET profil oluşturma API 'SI dahil) ve kapsamlı bir istemci tarafı API 'SI aracılığıyla Web hizmetlerine erişme özelliği dahil olmak üzere birçok yeni zengin istemci özelliğini etkinleştirir ASP.NET sunucu tarafı denetim kümesinde görülen denetim düzenlerinin çoğunu yansıtmak için tasarlanmıştır.

Bu Teknik İnceleme, ASP.NET AJAX `UpdatePanel` bileşeninin XML Tetikleyicileri işlevlerini inceler. XML Tetikleyicileri, belirli UpdatePanel denetimleri için kısmi işlemeye neden olabilecek bileşenler üzerinde ayrıntılı denetim sağlar.

Bu Teknik İnceleme, 3,5 ve Visual Studio 2008 .NET Framework Beta 2 sürümünü temel alır. Daha önce ASP.NET 2,0 'e hedeflenmiş bir eklenti derlemesi olan ASP.NET AJAX Uzantıları artık .NET Framework temel sınıf kitaplığıyla tümleşiktir. Bu Teknik İnceleme, Visual Studio 2008, Visual Web Developer Express değil, Visual Studio ile çalıştığın ve Visual Studio 'nun Kullanıcı arabirimine göre izlenecek yollar sağlayacak olduğunu varsaymaktadır (kod listelerinin ne olursa olsun tamamen uyumlu olacağını da unutmayın) geliştirme ortamı).

## <a name="triggers"></a>*Tetikleyiciler*

Verilen bir UpdatePanel için Tetikleyiciler, varsayılan olarak, `AutoPostBack` özelliği **true**olarak ayarlanan TextBox denetimleri dahil, bir geri gönderme çağıran tüm alt denetimleri otomatik olarak ekler. Ancak, Tetikleyiciler biçimlendirme kullanılarak bildirimli olarak da dahil edilebilir; Bu, UpdatePanel denetim bildiriminin `<triggers>` bölümü içinde yapılır. Tetikleyicilere `Triggers` Collection özelliği aracılığıyla erişilebilmesine rağmen, çalışma zamanında (örneğin, bir denetim tasarım zamanında kullanılabilir değilse), `Page_Load` sayfanıza ait ScriptManager nesnesinin `RegisterAsyncPostBackControl(Control)` yöntemini kullanarak (örneğin, tasarım zamanında kullanılabilir değilse) tüm kısmi işleme tetikleyicilerini kaydetmeniz önerilir. Sayfaların durum bilgisiz olduğunu ve bu denetimlerin her oluşturulışında bu denetimleri yeniden kaydetmeniz gerektiğini unutmayın.

Otomatik alt tetikleyici ekleme özelliği de devre dışı bırakılabilir (böylece geri göndermeler oluşturan alt denetimler, `ChildrenAsTriggers` özelliğini **false**olarak ayarlayarak otomatik olarak kısmi oluşturmaları tetiklemez). Bu, hangi belirli denetimlerin bir sayfa işlemesini çağırabileceği ve tavsiye edilen tüm olayları işlemek yerine bir olaya yanıt vermeyi kabul edecek şekilde en büyük esnekliği sağlar.

UpdatePanel denetimleri iç içe olduğunda, UpdateMode değeri **Conditional**olarak ayarlandığında, alt UpdatePanel tetikleniyorsa ancak üst öğe değilse, yalnızca alt UpdatePanel yenilenir. Ancak, üst UpdatePanel yenilenirse, alt UpdatePanel da yenilenir.

## <a name="the-lttriggersgt-element"></a>*&lt;&gt; öğesini tetikler*

Visual Studio 'da biçimlendirme düzenleyicisinde çalışırken, bir `UpdatePanel` denetiminin iki alt öğesi olduğunu fark edebilirsiniz (IntelliSense 'den). En sık görülen öğe, genellikle güncelleştirme paneli tarafından tutulacak içeriği (kısmi işleme etkinleştiriyoruz içerik) kapsülleyen `<ContentTemplate>` öğesidir. Diğer öğesi `<Triggers>` öğesidir ve bu, &lt;tetikleme&gt; öğenin bulunduğu UpdatePanel denetiminin kısmi işlemesini tetikleyebilecek, sayfadaki denetimleri (veya kullanıyorsanız Kullanıcı denetimi) belirtir.

`<Triggers>` öğesi iki alt düğümün her birini içerebilir: `<asp:AsyncPostBackTrigger>` ve `<asp:PostBackTrigger>`. Her ikisi de iki özniteliği kabul eder, `ControlID` ve `EventName`ve geçerli kapsülleme birimi içinde herhangi bir denetimi belirtebilir (örneğin, UpdatePanel denetiminiz bir Web Kullanıcı denetimi içinde bulunuyorsa, Kullanıcı denetiminin bulunacağı sayfada bir denetime başvurulması gerekmez).

`<asp:AsyncPostBackTrigger>` öğesi özellikle, yalnızca bu tetikleyicinin alt öğesi olan UpdatePanel 'ın değil, kapsülleme birimindeki *herhangi* bir UpdatePanel denetiminin alt öğesi olarak var olan bir denetimden herhangi bir olay hedefleyebileceği için yararlıdır. Bu nedenle, kısmi sayfa güncelleştirmesini tetiklemek için herhangi bir denetim yapılabilir.

Benzer şekilde, `<asp:PostBackTrigger>` öğesi kısmi sayfa işlemeyi tetiklemek için kullanılabilir, ancak sunucu için tam gidiş dönüş gerektiren bir tane. Bu tetikleyici öğesi, bir denetim normalde kısmi sayfa işlemeyi tetikleyeceğinden (örneğin, bir UpdatePanel denetiminin `<ContentTemplate>` öğesinde bir `Button` denetimi olduğunda) tam sayfa işlemesini zorlamak için de kullanılabilir. Yine, PostBackTrigger öğesi, geçerli kapsülleme birimindeki herhangi bir UpdatePanel denetiminin alt öğesi olan herhangi bir denetimi belirtebilir.

## <a name="lttriggersgt-element-reference"></a>*&lt;Tetikleyiciler&gt; öğe başvurusu*

*Biçimlendirme alt öğeleri:*

| **Etiket** | **Açıklama** |
| --- | --- |
| &lt;ASP: AsyncPostBackTrigger&gt; | Bu tetikleyici başvurusunu içeren UpdatePanel için kısmi sayfa güncelleştirmesine neden olacak bir denetim ve olay belirtir. |
| &lt;ASP: PostBackTrigger&gt; | Tam sayfa güncelleştirmesine neden olacak bir denetim ve olay belirtir (tam sayfa yenileme). Bu etiket, bir denetim başka bir şekilde kısmi işleme tetikleyeceği zaman tam yenilemeyi zorlamak için kullanılabilir. |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*İzlenecek yol: çapraz UpdatePanel Tetikleyicileri*

1. Kısmi işlemeyi etkinleştirmek için ScriptManager nesnesi ayarlanmış yeni bir ASP.NET sayfası oluşturun. Bu sayfaya iki UpdatePanel ekleyin-ilk içinde bir etiket denetimi (Label1) ve iki düğme denetimi (Button1 ve Button2) ekleyin. Button1, her Ikisini de güncelleştirmek için tıklamalıdır ve bu satırları güncelleştirmek için tıklayın. İkinci UpdatePanel 'da yalnızca bir etiket denetimi (etiket 2) ekleyin, ancak ForeColor özelliğini ayırt etmek için varsayılan değer dışında bir değere ayarlayın.
2. Her iki UpdatePanel etiketlerinin UpdateMode özelliğini **Conditional**olarak ayarlayın.

**Listeleme 1: default. aspx için biçimlendirme:** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. Button1 için Click olay işleyicisinde, Label1. Text ve etiket 2. Text ' i zamana bağımlı bir değere ayarlayın (DateTime. Now. ToLongTimeString ()). Button2 için Click olay işleyicisi için, yalnızca Label1. Text değerini zamana bağlı değere ayarlayın.

**Listeleme 2: default.aspx.cs içinde codebehind (kırpılmış):** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. Projeyi derlemek ve çalıştırmak için F5 tuşuna basın. Her iki paneli de Güncelleştir ' e tıkladığınızda her iki etiket de metni değiştirir; Ancak, bu paneli Güncelleştir ' e tıkladığınızda yalnızca Label1 güncelleştirmeleri vardır.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png))

## <a name="under-the-hood"></a>*Üzerinde*

Yeni oluşturduğumuz örneği kullanarak, ASP.NET AJAX 'un yaptığı ve UpdatePanel çapraz panel tetikleyicilerimizin nasıl çalıştığı hakkında bir göz atalım. Bunu yapmak için, oluşturulan sayfa kaynağı HTML 'si ile ve FireBug adlı bir, ile birlikte çalışan Mozilla Firefox uzantısının yanı sıra AJAX geri yükleme işlemlerini kolayca inceleyebilirsiniz. Ayrıca, Lutz Roeder tarafından sunulan .NET yansıtıcısı aracını da kullanacağız. Bu araçların her ikisi de çevrimiçi olarak kullanılabilir ve bir internet aramayla bulunabilir.

Sayfa kaynak kodu incelemesi, neredeyse hiçbir şey yok demektir; UpdatePanel denetimleri `<div>` kapsayıcılar olarak işlenir ve `<asp:ScriptManager>`tarafından sağlanmış olan betik kaynağı bilgilerini görebiliriz. Ayrıca, AJAX istemci komut dosyası kitaplığı için dahili olan PageRequestManager 'a yönelik yeni bir AJAX 'a özgü çağrı de vardır. Son olarak, `<span>` kapsayıcılar olarak işlenen iki `<asp:Label>` denetimi ile işlenen `<input>` düğmeleriyle bir tane olmak üzere iki UpdatePanel kapsayıcısı görüyoruz. (FireBug 'da DOM ağacını incelerse, etiketlerin görünür bir içerik üretmediğinden emin olmak için soluk olduğunu fark edeceksiniz.

Bu paneli Güncelleştir düğmesine tıklayın ve en üstteki UpdatePanel 'ın geçerli sunucu saatine göre güncelleştirileceğini unutmayın. FireBug 'da, isteği incelemek için konsol sekmesini seçin. Önce POST isteği parametrelerini inceleyin:

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png))

UpdatePanel 'ın, bir ScriptManager1 parametresi aracılığıyla hangi denetim ağacının tetiklenme hakkında tam olarak sunucu tarafı AJAX koduna (`UpdatePanel1` denetiminin `Button1` olduğunu unutmayın. Şimdi, her Iki paneli de Güncelleştir düğmesine tıklayın. Ardından, yanıtı inceleyerek, bir dizede ayarlanan, kanal ile ayrılmış bir dizi değişken görüyoruz; Özellikle, en üst UpdatePanel, `UpdatePanel1`, tarayıcıya gönderilen HTML 'nin tamamen olduğunu görüyoruz. AJAX istemci betiği kitaplığı, UpdatePanel 'ın özgün HTML içeriğini `.innerHTML` özelliği aracılığıyla yeni içerikle değiştirir ve bu nedenle sunucu değiştirilen içeriği sunucudan HTML olarak gönderir.

Şimdi, her Iki paneli de Güncelleştir düğmesine tıklayın ve sonuçları sunucudan inceleyin. Sonuçlar çok benzer-her iki UpdatePanel de sunucudan yeni HTML alır. Önceki geri çağırmada olduğu gibi, ek sayfa durumu gönderilir.

Görebileceğiniz gibi, AJAX geri gönderme işlemini gerçekleştirmek için özel kod kullanıldığından, AJAX istemci betiği kitaplığı ek kod olmadan form geri göndermeler yapamaz. Sunucu denetimleri otomatik olarak JavaScript kullanır ve bu sayede otomatik betik kaynağı ekleme, PostBackOptions sınıfı tarafından ilk olarak elde edilen form doğrulama ve durum için önceden bir form doğrulaması ve durumu için kod otomatik olarak , ve ClientScriptManager Sınıfı.

Örneğin, bir CheckBox denetimi düşünün; .NET yansıtıcısı 'nda sınıf ayrıştırılmış derlemesini inceleyin. Bunu yapmak için, System. Web derlemenizi açık olduğundan emin olun ve `RenderInputTag` metodunu açarak `System.Web.UI.WebControls.CheckBox` sınıfına gidin. `AutoPostBack` özelliğini denetleyen bir koşullu arayın:

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png))

`CheckBox` denetiminde otomatik geri gönderme etkinleştirildiğinde (AutoPostBack özelliği true olduğunda), sonuç `<input>` etiketi bu nedenle `onclick` özniteliğinde bir ASP.NET olay işleme betiği ile işlenir. Formun gönderiminin bölünmesi, daha sonra ASP.NET AJAX 'un, büyük olasılıkla ımprecıse dize değiştirme kullanılarak oluşabilecek olası önemli değişikliklerden kaçınılmasına izin verir. Ayrıca, bu, *herhangi* bir özel ASP.net denetiminin bir UpdatePanel kapsayıcısı içinde kullanımını desteklemek için ek kod olmadan ASP.NET AJAX 'un gücünden yararlanmasına olanak sağlar.

`<triggers>` işlevi, updateControls \_için PageRequestManager çağrısında başlatılan değerlere karşılık gelir (ASP.NET AJAX istemci komut dosyası kitaplığı, bir alt çizgiyle başlayan yöntemlerin, olayların ve alan adlarının iç olarak işaretlendiğine ve kitaplığın kendisi dışında kullanılması için uygun olmayan kuralları kullanacağını unutmayın. Bununla birlikte, AJAX geri göndermeler için hangi denetimlerin hedeflendiğini gözlemlebiliriz.

Örneğin, sayfaya iki ek denetim ekleyelim, tek bir denetimi UpdatePanel dışında bırakıp bir UpdatePanel içinde bırakarak. Üst UpdatePanel içinde bir CheckBox denetimi ekleyeceğiz ve liste içinde tanımlanmış bir dizi renge sahip bir DropDownList bırakmalısınız. Yeni biçimlendirme aşağıda verilmiştir:

**Listeleme 3: yeni biçimlendirme**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

Yeni arka plan kodu aşağıda verilmiştir:

**Listeleme 4: codebehind**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

Bu sayfanın arkasındaki düşünce, açılan listede ikinci etiketi göstermek için üç renkten birini seçerse, onay kutusunun her ikisi de kalın olup olmadığını ve etiketlerin de tarihi ve saati gösterip göstermeyeceğini belirler. Onay kutusu bir AJAX güncelleştirmesine neden olmamalıdır, ancak bir UpdatePanel içinde barındırmasa bile açılan liste açılır.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png))

Yukarıdaki ekran görüntüsünde gösterildiği gibi, tıklatılan en son düğme, bu paneli güncelleştirme, en son saati en alt süreden bağımsız olarak güncelleştiren doğru düğmedir. Tarih, alt etikette görünebildiğinden, tıklama arasında da geçiş yapıldı. Son olarak, en alttaki etiketin rengi şunlardır: etiketin metinden daha yakın bir şekilde güncelleştirildiğinden, denetim durumunun önemli olduğunu ve kullanıcıların AJAX geri göndermeler aracılığıyla korunması beklendiğini gösterir. *Ancak*saat güncelleştirilmedi. Süre, denetimin sunucuda yeniden işlendiği sırada ASP.NET çalışma zamanı tarafından yorumlanmakta olan sayfanın \_\_VIEWSTATE alanının kalıcılığı aracılığıyla otomatik olarak yeniden doldurulmuştur. ASP.NET AJAX sunucu kodu, denetimlerin durumu değiştirmekte olan yöntemleri tanımaz; yalnızca görünüm durumundan yeniden doldurulur ve uygun olan olayları çalıştırır.

Ancak, sayfa\_yükleme olayında zamanı başlattığını belirten, zaman doğru şekilde arttı bir şekilde kullanıma alınmalıdır. Sonuç olarak, geliştiriciler uygun olay işleyicileri sırasında uygun kodun çalıştırılmakta olduğu konusunda dikkatli olmalıdır ve bir denetim olayı işleyicisi uygun olduğunda sayfa\_yükleme kullanmaktan kaçının.

## <a name="summary"></a>Özet

ASP.NET AJAX Uzantıları UpdatePanel denetimi, çok yönlüdür ve güncelleştirilmesine neden olması gereken denetim olaylarını belirlemek için birkaç yöntem kullanabilir. Bu, alt denetimleri tarafından otomatik olarak güncelleştirilmesini destekler, ancak sayfada başka bir yerde denetim olaylarına da yanıt verebilir.

Sunucu işleme yükünün potansiyelini azaltmak için, bir UpdatePanel 'ın `ChildrenAsTriggers` özelliğinin `false`olarak ayarlanması ve olayların varsayılan olarak dahil yerine kabul edilmesinin yapılması önerilir. Bu Ayrıca, doğrulama dahil olmak üzere istenmeyen etkileri ve giriş alanlarındaki değişiklikleri de önler. Bu tür hatalar yalıtmak zor olabilir, çünkü sayfa kullanıcıya şeffaf bir şekilde güncelleştirilir ve neden bu nedenle hemen açık olmayabilir.

ASP.NET AJAX form gönderi gönderme modelinin iç işleyişini inceleyerek, ASP.NET tarafından zaten sağlanmış olan Framework 'ün kullandığını tespit edebiliyoruz. Bunu yaparken, aynı Framework kullanılarak tasarlanan denetimlerle maksimum uyumluluğu korur ve sayfa için yazılan ek JavaScript üzerinde intrudes.

## <a name="bio"></a>Biyografisi

Ramiz Paveza, Tempismanda ([www.Terralever.com](http://www.terralever.com)), Tempe 'de önde gelen etkileşimli pazarlama firması olan, az bir .NET uygulama geliştiricisiyseniz. [robpaveza@gmail.com](mailto:robpaveza@gmail.com)' de erişilebilir ve blogu [http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/)adresinde bulunabilir.

Scott, 1997 tarihinden itibaren Microsoft Web teknolojileriyle çalışmaktadır ve Bilgi Bankası yazılım çözümlerine odaklanmış ASP.NET tabanlı uygulamalar yazma konusunda uzmanımız myKB.com ([www.myKB.com](http://www.myKB.com)) Başkan Yardımcısı. Scott 'da e-posta ile [scott.cate@myKB.com](mailto:scott.cate@myKB.com) veya blogundan [ScottCate.com](http://ScottCate.com) adresinden iletişim kurulabilirler

> [!div class="step-by-step"]
> [Önceki](understanding-partial-page-updates-with-asp-net-ajax.md)
> [İleri](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
