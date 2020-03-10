---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: Sunucu denetimleri | Microsoft Docs
author: microsoft
description: ASP.NET 2,0, sunucu denetimlerini birçok şekilde geliştirir. Bu modülde, ASP.NET 2,0 ve Visual Studio 200 gibi mimari değişikliklerden bazılarını ele alacağız...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641444"
---
# <a name="server-controls"></a>Sunucu Denetimleri

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 2,0, sunucu denetimlerini birçok şekilde geliştirir. Bu modülde, ASP.NET 2,0 ve Visual Studio 2005 ile sunucu denetimleriyle ilgilenen bazı mimari değişiklikleri ele alacağız.

ASP.NET 2,0, sunucu denetimlerini birçok şekilde geliştirir. Bu modülde, ASP.NET 2,0 ve Visual Studio 2005 ile sunucu denetimleriyle ilgilenen bazı mimari değişiklikleri ele alacağız.

## <a name="view-state"></a>Durumu görüntüle

ASP.NET 2,0 ' deki görünüm durumundaki birincil değişiklik, boyutun önemli bir azalmasıyla sonuçlanır. Yalnızca üzerinde bir Takvim denetimi olan bir sayfa düşünün. ASP.NET 1,1 ' deki görünüm durumu aşağıda verilmiştir.

[!code-css[Main](server-controls/samples/sample1.css)]

Artık ASP.NET 2,0 ' deki özdeş bir sayfada görünüm durumu aşağıda verilmiştir.

[!code-css[Main](server-controls/samples/sample2.css)]

Bu, oldukça önemli bir değişiklik olduğunu ve Görünüm durumunun tel üzerinden geri ve ileri doğru şekilde gerçekleştirileceğini düşünürken, bu değişiklik geliştiricilere önemli bir performans artışı verebilir. Görünüm durumu boyutunun azaltılması, büyük ölçüde bunu dahili olarak işlediğimiz yoldur. Görünüm durumunun Base64 olarak kodlanmış bir dize olduğunu unutmayın. ASP.NET 2,0 ' de görünüm durumundaki değişikliği daha iyi anlamak için, yukarıdaki örneklerden kodu çözülmüş değerlere göz atalım.

Kodu çözülen 1,1 Görünüm durumu aşağıda verilmiştir:

[!code-css[Main](server-controls/samples/sample3.css)]

Bu, biraz benzer bir şekilde görünebilir, ancak burada bir model vardır. ASP.NET 1. x içinde, &lt;&gt; karakterlerini kullanarak veri türlerini ve sınırlandırılmış değerleri belirlemek için tek karakter kullandık. Yukarıdaki görünüm durumu örneğindeki "t", bir üçlü ifade temsil eder. Üçlü dizi listesi içerir ("l" bir ArrayList 'i temsil eder.) Bu ArrayLists, 1 değerine sahip bir Int32 ("i"), diğeri ise başka bir üçlü içeriyor. Üçlü liste, vb. çiftleri içerir. Dikkat edilmesi gereken önemli şey, çiftler içeren Üçlü olanak sağlar, veri türlerini bir harf aracılığıyla tanımladık ve &lt; ve &gt; karakterlerini sınırlayıcılar olarak kullanıyoruz.

ASP.NET 2,0 ' de, kodu çözülmüş görünüm durumu biraz farklı görünüyor.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

Kodu çözülen görünüm durumunun görünümünde büyük bir değişiklik fark etmelisiniz. Bu değişikliğin birkaç mimari underpinnings vardır. ASP.NET 1. x içinde görünüm durumu, verileri seri hale getirmek için LosFormatter kullandı. 2,0 ' de, yeni ObjectStateFormatter sınıfını kullanıyoruz. Bu sınıf, Görünüm durumu ve denetim durumunun serileştirilmesi ve serisini kaldırma konusunda yardımcı olmak için özel olarak tasarlanmıştır. (Denetim durumu sonraki bölümde ele alınacaktır.) Serileştirme ve seri durumundan çıkarma yöntemi değiştirilerek elde edilen birçok avantaj vardır. En çarpıcı özelliklerden biri, bir TextWriter kullanan LosFormatter 'ın aksine, ObjectStateFormatter bir BinaryWriter kullanır. Bu, ASP.NET 2,0 'in, dize yerine görüntüleme durumunun bir dizi bayt depolamasına izin verir. Örneğin, bir tamsayı alın. ASP.NET 1,1 ' de, bir tamsayı için Görünüm durumu 4 baytı gerekir. ASP.NET 2,0 ' de, aynı tamsayı yalnızca 1 bayt gerektirir. Depolanan görünüm durumu miktarını azaltmak için diğer geliştirmeler yapılmıştır. Örneğin, DateTime değerleri, artık dize yerine bir TickCount kullanılarak depolanır.

Hepsi yeterince olmadığı için, 1. x içinde durum görüntüleme durumundaki en büyük tüketicilerden biri DataGrid ve benzer denetimlerdi. Görünüm durumunun ilgili olduğu DataGrid gibi denetimlerin önemli bir dezavantajı, genellikle büyük miktarlarda yinelenen bilgiler içermesidir. ASP.NET 1. x içinde, yinelenen bilgiler daha fazla bir şekilde depolanır ve bir görünüm durumuna neden olur. ASP.NET 2,0 ' de, bu tür verileri depolamak için yeni IndexedString sınıfını kullanırız. Bir dize yinelenirse IndexedString için belirteci ve dizine ait bir IndexedString nesne tablosu içindeki dizini depolarız.

## <a name="control-state"></a>Denetim durumu

Geliştiricilerin görünüm durumu ile sahip olduğu ana kavraymalardaki bir tane, HTTP yüküne eklenen boyutdaydı. Daha önce belirtildiği gibi, görünüm durumundaki en büyük tüketicilerden biri DataGrid denetimidir. DataGrid tarafından oluşturulan çok büyük miktarlarda görünüm durumunu önlemek için, birçok geliştirici bu denetim için görünüm durumunu devre dışı bırakmış olur. Ne yazık ki bu çözüm her zaman iyi bir çözümdür. ASP.NET 1. x içindeki görünüm durumu yalnızca denetimin doğru işlevselliği için gerekli olan verileri içermez. Ayrıca, denetimin kullanıcı arabiriminin durumu ile ilgili bilgiler de içerir. Bu, bir DataGrid üzerinde sayfalandırma için izin vermek istiyorsanız, durumu görüntüleme durumunu içeren tüm Kullanıcı arabirimi bilgilerine gerek duymasa bile görünüm durumunu etkinleştirmeniz gerektiğini gösterir. Bu, hepsi veya Nothing bir senaryodur.

ASP.NET 2,0 ' de denetim durumu, denetim durumunun tanıtımı aracılığıyla sorunu çözer. Denetim durumu, denetimin doğru işlevselliği için kesinlikle gerekli olan verileri içerir. Görünüm durumundan farklı olarak denetim durumu devre dışı bırakılamaz. Bu nedenle, denetim durumunda saklanan verilerin dikkatle denetlenmesi önemlidir.

> [!NOTE]
> Denetim durumu, \_\_VIEWSTATE gizli form alanındaki görünüm durumu ile birlikte kalıcıdır.

Bu video, durumu ve denetim durumunu görüntüleme yönergedir.

![](server-controls/_static/image1.png)

[Tam ekran videosunu açın](server-controls/_static/state1.wmv)

Sunucu denetiminin denetim durumunu okuyup yazabilmesi için üç adım gerçekleştirmeniz gerekir.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>1\. Adım: RegisterRequiresControlState metodunu çağırma

RegisterRequiresControlState yöntemi bir denetimin denetim durumunu kalıcı hale getirmek için ASP.NET bildirir. Kayıtlı olan denetim olan denetim türünde bir bağımsız değişken alır.

Kayıt isteğinin istek için kalıcı olmadığına dikkat edin. Bu nedenle, denetim durumunun kalıcı hale getirilmesi durumunda bu yöntemin her istekte çağrılması gerekir. Yönteminin OnInit içinde çağrılması önerilir.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>2\. Adım: SaveControlState 'i geçersiz kılma

SaveControlState yöntemi, son geri gönderinden bu yana denetim için denetim durumu değişikliklerini kaydeder. Denetimin durumunu temsil eden bir nesne döndürür.

## <a name="step-3-override-loadcontrolstate"></a>3\. Adım: LoadControlState 'i geçersiz kılma

LoadControlState yöntemi kaydedilmiş durumu bir denetime yükler. Yöntemi, denetimin kaydedilmiş durumunu tutan Object türünde bir bağımsız değişken alır.

## <a name="full-xhtml-compliance"></a>Tam XHTML uyumluluğu

Web geliştiricileri, Web uygulamalarındaki standartların önemini bilir. Standart tabanlı bir geliştirme ortamını sürdürmek için, ASP.NET 2,0 tamamen XHTML uyumludur. Bu nedenle, tüm etiketler HTML 4,0 veya üstünü destekleyen tarayıcılarda XHTML standartlarına göre işlenir.

ASP.NET 1,1 ' de DOCTYPE tanımı aşağıdaki gibidir:

[!code-html[Main](server-controls/samples/sample6.html)]

ASP.NET 2,0 ' de varsayılan DOCTYPE tanımı aşağıdaki gibidir:

[!code-html[Main](server-controls/samples/sample7.html)]

Seçeneğini belirlerseniz, yapılandırma dosyasındaki Xhtmluygunluğu düğümü aracılığıyla varsayılan XHTML uyumluluğunu değiştirebilirsiniz. Örneğin, Web. config dosyasındaki aşağıdaki düğüm, XHTML uyumluluğunu XHTML 1,0 katı olarak değiştirecek:

[!code-xml[Main](server-controls/samples/sample8.xml)]

Seçeneğini belirlerseniz, ASP.NET ASP.NET 1. x içinde kullanılan eski yapılandırmayı kullanmak için aşağıdaki gibi yapılandırabilirsiniz:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>Bağdaştırıcıları kullanarak Uyarlamalı Işleme

ASP.NET 1. x içinde, yapılandırma dosyası HttpBrowserCapabilities nesnesini dolduran bir &lt;browserCaps&gt; bölümü içeriyordu. Bu nesne, bir geliştiricinin belirli bir isteği ve işleme kodunu doğru şekilde yaptığını belirlemesine izin vermez. ASP.NET 2,0 ' de, model geliştirilmiştir ve şimdi yeni ControlAdapter sınıfını kullanır. ControlAdapter sınıfı, denetimin yaşam döngüsünün olaylarını geçersiz kılar ve denetimlerin işlenmesini Kullanıcı aracısının özelliklerine göre denetler. Belirli bir Kullanıcı aracısının özellikleri, c:\Windows\Microsoft.NET\Framework\v2.0. depolanan bir tarayıcı tanım dosyası (. Browser dosya uzantısına sahip bir dosya) tarafından tanımlanır.\*\*\*\*\Browsers klasörü.

> [!NOTE]
> ControlAdapter sınıfı soyut bir sınıftır.

1\. x içindeki &lt;browserCaps&gt; bölümüne benzer şekilde, tarayıcı tanım dosyası, istenen tarayıcıyı tanımlamak için Kullanıcı aracısı dizesini ayrıştırmak üzere bir normal Ifade kullanır. Bu, Kullanıcı aracısının özel yeteneklerini tanımlar. ControlAdapter, denetimi Render yöntemi aracılığıyla işler. Bu nedenle, Render metodunu geçersiz kılarsınız, temel sınıfta Işlemeyi çağırmamalıdır. Bunun yapılması, işleme, bağdaştırıcı için bir kez ve denetimin kendisi için bir kez oluşmasına neden olabilir.

## <a name="developing-a-custom-adapter"></a>Özel bir bağdaştırıcı geliştirme

ControlAdapter 'ten devralarak kendi özel bağdaştırıcınızı geliştirebilirsiniz. Ayrıca, sayfa için bir bağdaştırıcının gerekli olduğu durumlarda, PageAdapter soyut sınıfından devralma yapabilirsiniz. Denetimlerin özel bağdaştırıcınıza eşlenmesi, tarayıcı tanım dosyasındaki &lt;controlAdapters&gt; öğesi aracılığıyla gerçekleştirilir. Örneğin, bir tarayıcı tanım dosyasındaki aşağıdaki XML menü denetimini MenuAdapter sınıfıyla eşleştirir:

[!code-html[Main](server-controls/samples/sample10.html)]

Bu modeli kullanarak, bir denetim geliştiricisinin belirli bir cihazı veya tarayıcıyı hedeflemesi oldukça kolay hale gelir. Ayrıca, bir geliştiricinin sayfaların her cihazda nasıl işlendiğinden tam denetim sahibi olması çok basittir.

## <a name="per-device-rendering"></a>Cihaz başına Işleme

ASP.NET 2,0 içindeki sunucu denetimi özellikleri, tarayıcıya özgü bir ön ek kullanılarak cihaz başına belirtilebilir. Örneğin, aşağıdaki kod, sayfaya gözatmakta olan cihazın hangi cihaza kullanıldığı üzerine bağlı olarak bir etiketin metnini değiştirir.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

Bu etiketi içeren sayfa Internet Explorer 'dan gözatılırken, "Internet Explorer 'dan gözatıyoruz" ifadesini gösteren bir metin görüntülenir. Sayfa Firefox 'tan gözatılırken etiket, "Firefox 'tan göz attığınız" metni görüntüler. Sayfa başka bir cihazdan gözatılırken, "bilinmeyen bir cihazdan Gözatılıyor" görüntülenir. Herhangi bir özellik, bu özel söz dizimi kullanılarak belirtilebilir.

## <a name="setting-focus"></a>Odak ayarlama

ASP.NET 1. x geliştiricileri genellikle belirli bir denetimde ilk odak ayarlamayı istedi. Örneğin, bir oturum açma sayfasında, sayfa ilk yüklendiğinde Kullanıcı KIMLIĞI metin kutusunun odağı alması yararlı olur. ASP.NET 1. x içinde, bazı istemci tarafı komut dosyalarını yazmak gerekir. Böyle bir komut dosyası önemsiz bir görev olsa da, ASP.NET 2,0 ' de SetFocus yöntemi için artık gerekli değildir. SetFocus yöntemi, odağı alması gereken denetimi gösteren bir bağımsız değişken alır. Bu bağımsız değişken, denetimin istemci KIMLIĞI ya da bir denetim nesnesi olarak sunucu denetiminin adı olabilir. Örneğin, ilk odağı sayfa ilk yüklendiğinde Txtuserıd adlı bir TextBox denetimine ayarlamak için aşağıdaki kodu Page\_Load sayfasına ekleyin:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

--veya

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2,0, odağı ayarlayan bir istemci tarafı işlevini işlemek için WebResource. axd işleyicisini (daha önce tartııldıı) kullanır. İstemci tarafı işlevinin adı, burada gösterildiği gibi, WebForm\_.

[!code-html[Main](server-controls/samples/sample14.html)]

Alternatif olarak, bir denetim için odak yöntemini, ilk odağı bu denetime ayarlamak için de kullanabilirsiniz. Focus yöntemi Denetim sınıfından türetilir ve tüm ASP.NET 2,0 denetimlerinde kullanılabilir. Bir doğrulama hatası oluştuğunda odağı belirli bir denetime ayarlamak da mümkündür. Bu, sonraki bir modülde ele alınacaktır.

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2,0 ' de yeni sunucu denetimleri

ASP.NET 2,0 ' deki yeni sunucu denetimleri aşağıda verilmiştir. Daha sonraki modüllerde bazıları hakkında daha fazla ayrıntıya gidecağız.

## <a name="imagemap-control"></a>ImageMap denetimi

ImageMap denetimi bir görüntüye geri dönüş başlatabilecek veya URL 'ye gidebileceğiniz etkin noktaları eklemenize olanak tanır. Üç tür etkin nokta mevcuttur; CircleHotSpot, RectangleHotSpot ve PolygonHotSpot. Etkin noktalar, Visual Studio 'daki bir koleksiyon Düzenleyicisi aracılığıyla veya kodda programlı olarak eklenir. Bir görüntüde etkin noktaları çizmek için kullanılabilecek Kullanıcı arabirimi yok. Etkin noktanın koordinatları ve boyutu ya da yarıçapı bildirimli olarak belirtilmelidir. Tasarımcıda bir etkin noktanın görsel temsili de yoktur. Bir etkin nokta bir URL 'ye gitmek üzere yapılandırıldıysa, URL, etkin noktanın NavigateUrl özelliği aracılığıyla belirtilir. Bir geri dönüş ön eki söz konusu olduğunda, PostBackValue özelliği sunucu tarafı kodunda alınabilecek geri gönderiye bir dize iletmenize olanak tanır.

![Visual Studio 'da etkin nokta koleksiyonu Düzenleyicisi](server-controls/_static/image1.jpg)

**Şekil 1**: Visual Studio 'da etkin nokta koleksiyonu Düzenleyicisi

## <a name="bulletedlist-control"></a>BulletedList denetimi

BulletedList denetimi, kolayca veri bağlaması olabilecek madde işaretli bir listesidir. Liste, madde işaretleri stili özelliği aracılığıyla sıralanabilir (numaralandırılır) veya sıralanmamış olabilir. Listedeki her öğe bir ListItem nesnesi tarafından temsil edilir.

![Visual Studio 'da BulletedList denetimi](server-controls/_static/image1.gif)

**Şekil 2**: Visual Studio 'Da BulletedList denetimi

## <a name="hiddenfield-control"></a>HiddenField denetimi

HiddenField denetimi sayfanıza bir gizli form alanı ekler. Bu değer, sunucu tarafı kodunda kullanılabilir. Gizli form alanının değeri genellikle geri gönderme arasında değişmeden kalması beklenir. Ancak, kötü niyetli bir kullanıcının yeniden Gönderi yapmadan önce değeri değiştirmesi mümkündür. Bu durumda, HiddenField denetimi ValueChanged olayını yükseltir. HiddenField denetiminde hassas bilgileriniz varsa ve bunun değişmeden kalmasını sağlamak istiyorsanız kodunuzda ValueChanged olayını işlemeniz gerekir.

## <a name="fileupload-control"></a>Dosya karşıya yükleme denetimi

ASP.NET 2,0 ' deki dosya karşıya yükleme denetimi bir ASP.NET sayfası aracılığıyla bir Web sunucusuna dosya yüklemeyi mümkün hale getirir. Bu denetim, birkaç özel durum dışında ASP.NET 1. x Htmlputfile sınıfına oldukça benzerdir. ASP.NET 1. x içinde, iyi bir dosyanız olup olmadığınızı belirleyebilmek için PostedFile özelliğinin null için denetlenmesi önerilir. ASP.NET 2,0 ' deki dosya yükleme denetimi, aynı amaçla kullanabileceğiniz yeni bir HasFile özelliği ekler ve bu biraz daha etkilidir.

PostedFile özelliği, HttpPostedFile nesnesine erişim için hala kullanılabilir, ancak HttpPostedFile işlevinin bazı işlevleri artık FileUpload denetimiyle doğası gereği kullanılabilir. Örneğin, karşıya yüklenen bir dosyayı ASP.NET 1. x konumuna kaydetmek için HttpPostedFile nesnesi üzerinde SaveAs yöntemini çağırın. ASP.NET 2,0 ' de dosya karşıya yükleme denetimini kullanarak, dosya yükleme denetimi üzerinde SaveAs metodunu çağırabilirsiniz.

2,0 davranışında başka bir önemli değişiklik (ve büyük olasılıkla en önemli değişiklik), artık karşıya yüklenen bir dosyanın tamamını kaydedilmeden önce belleğe yüklemek için gerekli değildir. 1\. x içinde karşıya yüklenen tüm dosyalar diske yazılmadan önce tamamen belleğe kaydedilir. Bu mimari, büyük dosyaların karşıya yüklenmesini engeller.

ASP.NET 2,0 ' de, httpRuntime öğesinin requestLengthDiskThreshold özniteliği, diske yazılmadan önce bellekteki bir arabellekte kaç kilobayt tutulması gerektiğini yapılandırmanıza olanak tanır.

**Önemli**: MSDN belgeleri (ve diğer bir deyişle belgeler) bu değerin bayt cinsinden (kilobayt değil) olduğunu ve varsayılan değerin 256 olduğunu belirtir. Değer aslında kilobayt cinsinden belirtilir ve varsayılan değer 80 ' dir. Varsayılan bir 80K değeri sunarak, arabelleğin büyük nesne yığınında bitmemesini sağlamaktır.

## <a name="wizard-control"></a>Sihirbaz denetimi

ASP.NET geliştiricilerle, panoları kullanarak veya sayfadan sayfaya aktararak bir dizi "sayfa" ile bilgi toplamaya çalışan geliştiriciler ile uğraşarak karşılaşmanız oldukça yaygındır. Daha sık değil, Endeavor sinir bozucu bir işlemdir ve zaman alabilir. Yeni sihirbaz denetimi, kullanıcıların alışkın olduğu bir sihirbaz arabirimindeki doğrusal ve doğrusal olmayan adımlara izin vererek sorunları çözer. Sihirbaz denetimi, giriş formlarını bir dizi adımda sunar. Her adım, denetimin StepType özelliği tarafından belirtilen belirli bir türdür. Kullanılabilir adım türleri şunlardır:

| **Adım türü** | **Açıklama** |
| --- | --- |
| Otomatik | Sihirbaz, adım hiyerarşisi içindeki konumuna göre adım türünü otomatik olarak belirler. |
| Başlat | İlk adım, genellikle bir tanıtıcı ifade sunmak için kullanılır. |
| Adım | Normal bir adım. |
| Son | Son adım, genellikle Sihirbazı tamamlayacak bir düğme sunmak için kullanılır. |
| Complete | Başarı veya hata iletişim kuran bir ileti gösterir. |

> [!NOTE]
> Sihirbaz denetimi ASP.NET denetim durumunu kullanarak durumunu izler. Bu nedenle, EnableViewState özelliği herhangi bir yaklaşım olmadan false olarak ayarlanabilir.

Bu video, sihirbaz denetimi kılavuzsunda bir yönergedir.

![](server-controls/_static/image2.png)

[Tam ekran videosunu açın](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>Yerelleşme denetimi

Yereldenetim, değişmez bir denetime benzer. Ancak, Yereldenetim, öğesine eklenen biçimlendirmenin nasıl işleneceğini denetleyen bir **Mode** özelliğine sahiptir. Mode özelliği aşağıdaki değerleri destekler:

| **Modundaysa** | **Açıklama** |
| --- | --- |
| Dönüşüm | Biçimlendirme, isteği yapan tarayıcının protokolüne göre dönüştürülür. |
| Doğrudan geçiş | Biçimlendirme olduğu gibi işlenir. |
| Kodlama | Denetime eklenen biçimlendirme HtmlEncode kullanılarak kodlanır. |

## <a name="multiview-and-view-controls"></a>MultiView ve View denetimleri

MultiView denetimi, görünüm denetimleri için bir kapsayıcı olarak davranır ve görünüm denetimi, diğer denetimler için bir kapsayıcı (panel denetimi gibi) gibi davranır. Bir MultiView denetimindeki her görünüm tek bir görünüm denetimiyle temsil edilir. MultiView içindeki ilk görünüm denetimi 0, ikincisi ise 1, vb. şeklinde görüntülenir. MultiView denetiminin ActiveViewIndex ' i belirterek görünümler arasında geçiş yapabilirsiniz.

## <a name="substitution-control"></a>Değiştirme denetimi

Değiştirme denetimi ASP.NET Caching ile birlikte kullanılır. Önbelleğe almanın avantajlarından yararlanmak istediğiniz durumlarda, ancak her istekte (diğer bir deyişle, önbelleğe alma işleminden muaf tutulan bir sayfanın bölümleri) güncellenmesi gereken bir sayfa yerleriniz varsa, değiştirme bileşeni harika bir çözüm sağlar. Denetim aslında herhangi bir çıktıyı kendi kendine işlemez. Bunun yerine, sunucu tarafı koddaki bir yönteme bağlanır. Sayfa istendiğinde, yöntemi çağrılır ve değiştirme denetiminin yerine döndürülen biçimlendirme işlenir.

Değiştirme denetiminin bağlandığı Yöntem **MethodName** özelliği aracılığıyla belirtilir. Bu yöntemin aşağıdaki ölçütlere uyması gerekir:

- Statik (VB. paylaşılan) yöntemi olmalıdır.
- HttpContext türünde bir parametre kabul eder.
- Sayfadaki denetimin yerini alacak olan işaretlemeyi temsil eden bir dize döndürür.

Değiştirme denetiminin sayfada başka bir denetimi değiştirebilme özelliği yoktur, ancak geçerli HttpContext 'e parametresi aracılığıyla erişebilir.

## <a name="gridview-control"></a>GridView denetimi

GridView denetimi, DataGrid denetiminin yerini alır. Bu denetim, sonraki bir modülde daha ayrıntılı olarak ele alınacaktır.

## <a name="detailsview-control"></a>DetailsView denetimi

DetailsView denetimi, bir veri kaynağından tek bir kayıt görüntülemenizi ve onu düzenlemenizi veya silmenizi sağlar. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="formview-control"></a>FormView denetimi

FormView denetimi, yapılandırılabilir arabirimdeki bir veri kaynağından tek bir kayıt göstermek için kullanılır. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="accessdatasource-control"></a>AccessDataSource denetimi

AccessDataSource denetimi, Access veritabanına veri bağlamak için kullanılır. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="objectdatasource-control"></a>ObjectDataSource denetimi

ObjectDataSource denetimi, denetimlerin doğrudan veri kaynağına bağlandığı iki katmanlı bir modelin aksine, bir orta katman iş nesnesine veri bağlanması için üç katmanlı mimariyi desteklemek üzere kullanılır. Daha sonraki bir modülde daha ayrıntılı olarak ele alınacaktır.

## <a name="xmldatasource-control"></a>XmlDataSource denetimi

XmlDataSource denetimi bir XML veri kaynağına veri bağlamak için kullanılır. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="sitemapdatasource-control"></a>SiteMapDataSource denetimi

SiteMapDataSource denetimi, site haritasını temel alan site gezinti denetimleri için veri bağlama sağlar. Daha sonraki bir modülde daha ayrıntılı olarak ele alınacaktır.

## <a name="sitemappath-control"></a>SiteMapPath Control

Bu denetim, genellikle içerik haritaları olarak adlandırılan bir dizi gezinti bağlantısını görüntüler. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="menu-control"></a>Menü denetimi

Menü denetimi DHTML kullanarak dinamik menüler görüntüler. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="treeview-control"></a>TreeView Denetimi

TreeView denetimi, verilerin hiyerarşik ağaç görünümünü görüntülemek için kullanılır. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="login-control"></a>Oturum açma denetimi

Oturum açma denetimi bir Web sitesinde oturum açmak için bir mekanizma sağlar. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="loginview-control"></a>LoginView denetimi

LoginView denetimi, kullanıcının oturum açma durumunu temel alan farklı şablonların görüntülenmesini sağlar. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="passwordrecovery-control"></a>PasswordRecovery denetimi

PasswordRecovery denetimi bir ASP.NET uygulamasının kullanıcıları tarafından unutulmuş parolaları almak için kullanılır. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="loginstatus"></a>LoginStatus

LoginStatus denetimi, kullanıcının oturum açma durumunu görüntüler. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="loginname"></a>loginName

LoginName denetimi bir ASP.NET uygulamasına oturum açıldıktan sonra kullanıcının Kullanıcı adını görüntüler. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard, kullanıcılara bir ASP.NET uygulamasında kullanmak üzere bir ASP.NET üyelik hesabı oluşturma yeteneği sağlayan yapılandırılabilir bir sihirbazdır. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="changepassword"></a>Parola

ChangePassword denetimi, kullanıcıların bir ASP.NET uygulamasının parolalarını değiştirmesine izin verir. Daha sonraki bir modülde daha ayrıntılı bir şekilde ele alınmıştır.

## <a name="various-webparts"></a>Çeşitli Web bölümleri

ASP.NET 2,0, çeşitli Web Bölümleri birlikte gelir. Bunlar, sonraki bir modülde ayrıntılı olarak ele alınacaktır.
