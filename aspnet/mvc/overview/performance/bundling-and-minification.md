---
uid: mvc/overview/performance/bundling-and-minification
title: Paketleme ve küçültmeye yönelik | Microsoft Docs
author: Rick-Anderson
description: Paketleme ve küçültme, ASP.NET 4,5 içinde, istek yükleme süresini geliştirmek için kullanabileceğiniz iki tekniklerdir. Paketleme ve küçültme, reducin ile yükleme süresini iyileştirir...
ms.author: riande
ms.date: 08/23/2012
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 239980d747c6e0d6be1e9b4fe0371e276e37cf21
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519290"
---
# <a name="bundling-and-minification"></a>Paketleme ve Küçültme

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

> Paketleme ve küçültme, ASP.NET 4,5 içinde, istek yükleme süresini geliştirmek için kullanabileceğiniz iki tekniklerdir. Paketleme ve minbirleşme, sunucuya yapılan istek sayısını azaltarak ve istenen varlıkların boyutunu azaltarak (CSS ve JavaScript gibi) yükleme süresini geliştirir.

Geçerli büyük tarayıcıların çoğu her ana bilgisayar için [eşzamanlı bağlantı](http://www.browserscope.org/?category=network) sayısını altı olarak sınırlar. Bu, altı isteğin işlendiği sırada bir konaktaki varlık isteklerinin tarayıcı tarafından kuyruğa alınıp işlenemeyeceği anlamına gelir. Aşağıdaki görüntüde, IE F12 geliştirici araçları ağ sekmeleri, örnek bir uygulamanın hakkında bilgi görünümü tarafından istenen varlıkların zamanlamasını gösterir.

![B/M](bundling-and-minification/_static/image1.png)

Gri çubuklar, isteğin tarayıcı tarafından Sıradaki, altı bağlantı sınırının beklediği süreyi gösterir. Sarı çubuk, ilk bayta olan istek süresi, diğer bir deyişle, isteği göndermek ve sunucudan ilk yanıtı almak için geçen süredir. Mavi çubuklar sunucudan yanıt verilerinin alınması için geçen süreyi gösterir. Ayrıntılı zamanlama bilgileri almak için bir varlığa çift tıklayabilirsiniz. Örneğin, aşağıdaki görüntüde */Scripts/myscripts/javascript6.js* dosyasını yüklemek için zamanlama ayrıntıları gösterilmektedir.

![](bundling-and-minification/_static/image2.png)

Önceki görüntüde, tarayıcı eşzamanlı bağlantı sayısını kısıtlayacağından, isteğin sıraya alındığı saati veren **Başlangıç** olayı gösterilmektedir. Bu durumda, başka bir isteğin tamamlanmasını bekleyen 46 milisaniye için istek sıraya alındı.

## <a name="bundling"></a>Paketleme

Paketleme, ASP.NET 4,5 ' deki yeni bir özelliktir ve birden çok dosyayı tek bir dosyada birleştirmeyi veya paketlemeyi kolaylaştırır. CSS, JavaScript ve diğer paketleri de oluşturabilirsiniz. Daha az sayıda dosya daha az HTTP isteği ve ilk sayfa yükleme performansını iyileştirebilirler.

Aşağıdaki görüntüde, daha önce gösterilen hakkında bilgi için aynı zamanlama Görünümü gösterilmektedir, ancak bu kez paketleme ve küçültmeye karşı etkin.

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>Küçültme

Minbirleşme, gereksiz beyaz boşluğu ve açıklamaları kaldırma ve değişken adlarını tek bir karaktere kısaltma gibi betiklere veya CSS 'ye yönelik çeşitli kod iyileştirmeleri uygular. Aşağıdaki JavaScript işlevini göz önünde bulundurun.

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

Minbirleşme sonrasında, işlev aşağıdakilere düşürülür:

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

Açıklamaları ve gereksiz boşlukları kaldırmanın yanı sıra, aşağıdaki parametreler ve değişken adları (kısaltılmış) aşağıdaki gibi yeniden adlandırıldı:

| **Özgün** | **İsim** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | ı |

## <a name="impact-of-bundling-and-minification"></a>Paketleme ve küçültmeye yönelik etkileri

Aşağıdaki tabloda, örnek programda tüm varlıkların tek tek listelenmesi ve paketleme ve minlıle (B/M) kullanılarak çeşitli önemli farklılıklar gösterilmektedir.

|  | **B/M kullanma** | **B/M olmadan** | **Değişebilir** |
| --- | --- | --- | --- |
| **Dosya Istekleri** | 9 | 34 | 256% |
| **KB gönderildi** | 3.26 | 11.92 | 266% |
| **KB alındı** | 388.51 | 530 | 36% |
| **Yükleme saati** | 510 MS | 780 MS | 53% |

Gönderilen Baytlar, tarayıcılar üzerinde uygulanan HTTP üst bilgilerinde oldukça ayrıntılıdır. En büyük dosyalar (*betikler\\jQuery-ui-1.8.11. min. js* ve *betikler\\jQuery-1.7.1. min. js*) zaten küçültülmüş olduğundan, alınan baytların azaltılması büyük değil. Note: örnek programdaki zamanlamalar yavaş bir ağın benzetimini yapmak için [Fiddler](http://www.fiddler2.com/fiddler2/) aracını kullandı. (Fiddler **kuralları** menüsünde, **performans** ' ı seçin ve ardından **modem hızlarından benzetim**yapın.)

## <a name="debugging-bundled-and-minified-javascript"></a>Paketlenmiş ve küçültülmüş JavaScript hatalarını ayıklama

JavaScript dosyaları paketlenmiş veya küçültülmüş olmadığından, *Web. config* dosyasındaki [derleme öğesinin](https://msdn.microsoft.com/library/s10awwz0.aspx) `debug="true"`) olarak ayarlandığı bir geliştirme ortamında JavaScript 'te hata ayıklaması kolaydır. Ayrıca, JavaScript dosyalarınızın paketlenmiş ve küçültülmüş olduğu bir yayın derlemesinde hata ayıklayabilirsiniz. IE F12 geliştirici araçlarını kullanarak, mini kullanılan bir pakete eklenen bir JavaScript işlevinde aşağıdaki yaklaşımı kullanarak hata ayıklaması yapabilirsiniz:

1. **Betik** sekmesini seçin ve ardından **hata ayıklamayı Başlat** düğmesini seçin.
2. Varlıklar düğmesini kullanarak hata ayıklamak istediğiniz JavaScript işlevini içeren paketi seçin.  
    ![](bundling-and-minification/_static/image4.png)
3. **Yapılandırma düğmesini** ![](bundling-and-minification/_static/image5.png)seçip **JavaScript Biçimlendir**' i seçerek küçültülmüş JavaScript 'i biçimlendirin.
4. **Arama betiği** giriş kutusunda, hata ayıklamak istediğiniz işlevin adını seçin. Aşağıdaki görüntüde, **arama betiği** giriş kutusuna **Addalttoimg** girildi.  
    ![](bundling-and-minification/_static/image6.png)

F12 geliştirici araçlarıyla hata ayıklama hakkında daha fazla bilgi için, [JavaScript hatalarında hata ayıklama Için F12 geliştirici araçları kullanarak](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)MSDN makalesine bakın.

## <a name="controlling-bundling-and-minification"></a>Paketlemeyi ve küçültmeye göre denetleme

*Web. config* dosyasındaki [derleme öğesinde](https://msdn.microsoft.com/library/s10awwz0.aspx) hata ayıklama özniteliğinin değeri ayarlanarak paketleme ve minbirleşme etkin veya devre dışı bırakılmıştır. Aşağıdaki XML 'de, paketleme ve minbirleşme devre dışı olduğundan `debug` true olarak ayarlanır.

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

Paketlemeyi ve küçültmeye olanak tanımak için `debug` değerini "false" olarak ayarlayın. *Web. config* ayarını `BundleTable` sınıfındaki `EnableOptimizations` özelliği ile geçersiz kılabilirsiniz. Aşağıdaki kod, paketlemeyi ve küçültmeye izin verebilir ve *Web. config* dosyasındaki herhangi bir ayarı geçersiz kılar.

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> `EnableOptimizations` `true` veya *Web. config* dosyasındaki [derleme öğesinde](https://msdn.microsoft.com/library/s10awwz0.aspx) hata ayıklama özniteliği `false`olarak ayarlı değilse, dosyalar paketlenmiş veya küçültülmüş olmayacaktır. Ayrıca, dosyaların. min sürümü kullanılmayacak, tam hata ayıklama sürümleri seçilecek. `EnableOptimizations`, *Web. config* dosyasındaki [derleme öğesinde](https://msdn.microsoft.com/library/s10awwz0.aspx) hata ayıklama özniteliğini geçersiz kılar

## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>ASP.NET Web Forms ve Web sayfaları ile paketleme ve küçültmeye yönelik kullanma

- Web sayfaları için Web [sayfaları sitesine Web Iyileştirmesi ekleme](https://docs.microsoft.com/archive/blogs/rickandy/adding-web-optimization-to-a-web-pages-site)Blog girdisine bakın.
- Web Forms için, [Web Forms Için paketleme ve küçültmeye ekleme](https://docs.microsoft.com/archive/blogs/rickandy/adding-bundling-and-minification-to-web-forms)başlıklı blog girişine bakın.

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>ASP.NET MVC ile paketleme ve küçültmeye yönelik kullanma

Bu bölümde, paketleme ve küçültmeye yönelik İnceleme için bir ASP.NET MVC projesi oluşturacağız. İlk olarak, varsayılan değerleri değiştirmeden **Mvcbm** adlı yeni BIR ASP.NET MVC Internet projesi oluşturun.

*Uygulama\\açın \_\\BundleConfig.cs dosyasını başlatın* ve paketleri oluşturmak, kaydettirmek ve yapılandırmak için kullanılan `RegisterBundles` yöntemini inceleyin. Aşağıdaki kod `RegisterBundles` yönteminin bir bölümünü gösterir.

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

Yukarıdaki kod, tüm uygun (hata ayıklama veya küçültülmüş, ancak değil) içeren *~/paketles/jQuery* adlı yeni bir JavaScript paketi oluşturur. *vsdoc*) dosyaları *komut* dosyaları klasöründe "~/Scripts/jQuery-{Version}.exe" olan joker karakter dizesiyle eşleşir. ASP.NET MVC 4 için bu bir hata ayıklama yapılandırması, *jQuery-1.7.1. js* dosyası pakete eklenecektir. Bir sürüm yapılandırmasında, *jQuery-1.7.1. min. js* eklenecektir. Paketleme çerçevesi aşağıdaki gibi çeşitli yaygın kurallara sahiptir:

- *FileX. min. js* ve *FileX. js* olduğunda yayın için ". min" dosyası seçiliyor.
- Hata ayıklama için ". min" sürümü seçiliyor.
- Yalnızca IntelliSense tarafından kullanılan "-vsdoc" dosyaları (örneğin, *jQuery-1.7.1-vsdoc. js*) yoksayılıyor.

Yukarıda gösterilen `{version}` joker karakter eşleştirme kartı, *komut dosyaları* klasörünüzdeki jQuery 'in uygun sürümüyle otomatik olarak jQuery paketi oluşturmak için kullanılır. Bu örnekte, bir joker karakter kullanmak aşağıdaki avantajları sağlar:

- , Görünüm sayfalarınızda önceki paketleme kodunu veya jQuery başvurularını değiştirmeden daha yeni bir jQuery sürümüne güncelleştirme yapmak için NuGet 'i kullanmanıza olanak sağlar.
- , Hata ayıklama yapılandırmalarının tam sürümünü ve sürüm derlemeleri için ". min" sürümünü otomatik olarak seçer.

## <a name="using-a-cdn"></a>CDN kullanma

 Takip kodu yerel jQuery paketinin yerini bir CDN jQuery paketiyle değiştirir.

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

Yukarıdaki kodda, yayın modundayken CDN 'den ve hata ayıklama sürümü yerel olarak hata ayıklama modunda getirilecektir. CDN kullanırken, CDN isteğinin başarısız olması durumunda bir geri dönüş mekanizmasına sahip olmanız gerekir. Düzen dosyasının sonundaki aşağıdaki biçimlendirme parçası, CDN 'nin başarısız olmasına neden olan komut dosyasını gösterir.

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>Paket oluşturma

[Paket](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) sınıfı `Include` yöntemi, her bir dizenin kaynağa bir sanal yol olduğu dizeler dizisini alır. Uygulama\\`RegisterBundles` yönteminden aşağıdaki kod *\_başlat\\BundleConfig.cs* dosyası bir pakete birden çok dosya eklendiğini gösterir:

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

[Paket](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) sınıfı `IncludeDirectory` yöntemi, bir arama düzeniyle eşleşen bir dizindeki tüm dosyaları (ve isteğe bağlı olarak tüm alt dizinleri) eklemek için sağlanır. [Paket](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) sınıfı `IncludeDirectory` API 'si aşağıda gösterilmektedir:

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

Paketlerde, Işleme yöntemi kullanılarak görünümlerde başvurulur (CSS için`Styles.Render` ve JavaScript için `Scripts.Render`). *Görünümler\\paylaşılan\\\_Layout. cshtml* dosyasında bulunan aşağıdaki biçimlendirme, varsayılan ASP.net Internet projesinin nasıl BAŞVURULACAĞıNı CSS ve JavaScript demeti gösterir.

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

Işleme metotlarının bir dize dizisi aldığını ve bir kod satırında birden çok paket ekleyebilmesini unutmayın. Genellikle varlığa başvurmak için gerekli HTML 'yi oluşturan render yöntemlerini kullanmak isteyeceksiniz. Varlığa başvurmak için gereken biçimlendirme olmaksızın varlığın URL 'sini oluşturmak için `Url` yöntemini kullanabilirsiniz. Yeni HTML5 [Async](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async) özniteliğini kullanmayı istediğinizi varsayalım. Aşağıdaki kod, `Url` yöntemi kullanılarak modernize 'a nasıl başvurulacağını gösterir.

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>Dosyaları seçmek için "\*" joker karakterini kullanma

`Include` yönteminde belirtilen sanal yol ve `IncludeDirectory` yönteminde arama deseninin en son yol kesimindeki bir ön ek veya sonek olarak bir "\*" joker karakteri kabul edebilir. Arama dizesi büyük/küçük harfe duyarlıdır. `IncludeDirectory` yönteminde alt dizinler aranıyor seçeneği vardır.

Aşağıdaki JavaScript dosyalarıyla bir proje düşünün:

- *Betikler\\ortak\\AddAltToImg. js*
- *Betikler\\ortak\\ToggleDiv. js*
- *Betikler\\ortak\\ToggleImg. js*
- *Betikler\\ortak\\sub1\\ToggleLinks. js*

![dır imag](bundling-and-minification/_static/image7.png)

Aşağıdaki tabloda gösterildiği gibi joker karakter kullanılarak bir pakete eklenen dosyalar gösterilmektedir:

| **Çağrı** | **Eklenen veya özel durum oluşturulan dosya** |
| --- | --- |
| Dahil et ("~/Scripts/Common/\*. js") | *AddAltToImg.js*, *ToggleDiv.js*, *ToggleImg.js* |
| Dahil et ("~/Scripts/Common/T\*. js") | Geçersiz model özel durumu. Joker karaktere yalnızca önek veya sonek üzerinde izin verilir. |
| Dahil et ("~/Scripts/Common/\*OG.\*") | Geçersiz model özel durumu. Yalnızca bir joker karaktere izin verilir. |
| Dahil et ("~/Scripts/Common/T\*") | *Togglediv. js*, *toggleimg. js* |
| Dahil et ("~/Scripts/Common/\*") | Geçersiz model özel durumu. Saf joker karakter segmenti geçerli değil. |
| Includedirectory ("~/Scripts/Common", "T\*") | *Togglediv. js*, *toggleimg. js* |
| Includedirectory ("~/Scripts/Common", "T\*", true) | *Togglediv. js*, *toggleimg. js*, *togglelinks. js* |

Her bir dosyayı bir pakete açıkça eklemek, genellikle dosyaların aşağıdaki nedenlerle joker karakter yüklemesi üzerinde tercih edilir:

- Joker karaktere göre komut dosyaları eklemek, genellikle istediğiniz şekilde değil, alfabetik sırada yükleme yapar. CSS ve JavaScript dosyalarının sıklıkla belirli (alfabetik olmayan) bir sıraya eklenmesi gerekir. Özel bir [ıpaketleme Liorderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) uygulaması ekleyerek bu riski azaltabilirsiniz, ancak her bir dosyanın açıkça eklenmesi daha az hataya açıktır. Örneğin, gelecekteki bir klasöre yeni varlıklar ekleyebilirsiniz ve bu da, [ıpaketleyici](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) uygulamanızı değiştirmenizi gerektirebilir.
- Joker karakter yükleme kullanılarak bir dizine eklenen belirli dosyaları görüntüleme, bu pakete başvuran tüm görünümlere eklenebilir. Belirli bir betiğe görüntüle bir pakete eklenirse, pakete başvuran diğer görünümlerde JavaScript hatası alabilirsiniz.
- Diğer dosyaları içeri alan CSS dosyaları, içeri aktarılan dosyaların iki kez yüklendiği sonucu. Örneğin, aşağıdaki kod, jQuery kullanıcı arabirimi teması CSS dosyalarının çoğunu iki kez yüklemiş bir paket oluşturur. 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  "\*. css" joker karakter Seçicisi, *içerik\\temaları\\temel\\jQuery. UI. ALL. css* dosyası dahil olmak üzere, klasördeki her bir CSS dosyasını getirir. *JQuery. UI. ALL. css* dosyası diğer CSS dosyalarını içeri aktarır.

## <a name="bundle-caching"></a>Paket önbelleğe alma

Paketler, Paket oluşturulduğu zaman bir yıl boyunca HTTP Expires üst bilgisini ayarlar. Daha önce görüntülenen bir sayfaya gittiğinizde, Fiddler, paket için koşullu bir istek yapmaz, yani bu, paketteki paketleri için bir HTTP GET isteği ve sunucudan HTTP 304 yanıtı yoktur. Her paket için F5 tuşuyla koşullu bir istek oluşturmak üzere IE 'yi zorlayabilirsiniz (her paket için bir HTTP 304 yanıtı ile sonuçlanır). ^ F5 kullanarak tam yenilemeyi zorlayabilirsiniz (her paket için bir HTTP 200 yanıtına neden olur.)

Aşağıdaki görüntüde Fiddler yanıt bölmesinin **önbelleğe alma** sekmesi gösterilmektedir:

![Fiddler önbelleğe alma resmi](bundling-and-minification/_static/image8.png)

İstek   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 , Grup olarak **Allmyscripts** ve bir sorgu dizesi çifti **v = R0sLDicvP58AIXN\\\_mc3QdyVvVj5euZNzdsa2N1PKvb81**içerir. Sorgu dizesi **v** , önbelleğe alma için kullanılan benzersiz bir tanımlayıcı olan bir değer belirtecine sahiptir. Paket değişmedikçe, ASP.NET uygulaması bu belirteci kullanarak **Allmyscripts** paketini ister. Paketteki herhangi bir dosya değişirse, ASP.NET iyileştirme çerçevesi yeni bir belirteç oluşturur ve bu, paket için tarayıcı isteklerinin en son paketi almasını garanti eder.

IE9 F12 geliştirici araçlarını çalıştırırsanız ve daha önce yüklenmiş bir sayfaya gittiğinizde, IE, her bir pakete ve HTTP 304 ' i döndüren sunucuya yapılan koşullu GET isteklerini yanlış gösterir. IE9 'in, CDNs kullanarak blog girişinde koşullu bir istek olup olmadığını [ve Web sitesi performansını geliştirmek Için süresinin dolacağını anlamak için](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)nasıl sorun olduğunu bulabilirsiniz.

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS, CoffeeScript, SCSS, Sass paketleme.

Paketleme ve küçültmeye yönelik Framework, [SCSS](http://sass-lang.com/), [Sass](http://sass-lang.com/), [Less](http://www.dotlesscss.org/) veya [CoffeeScript](http://coffeescript.org/)gibi ara dilleri işlemek için bir mekanizma sağlar ve sonuçta elde edilen pakete minbirleşme gibi dönüşümler uygular. Örneğin, MVC 4 projenize [. Less](http://www.dotlesscss.org/) dosyaları eklemek için:

1. DAHA az içeriğiniz için bir klasör oluşturun. Aşağıdaki örnek, *MyLess klasörünü\\içeriği* kullanır.
2. Projenize noktasız [. Less](http://www.dotlesscss.org/) NuGet paketini ekleyin.  
    ![, bir NuGet noktasız yüklemeyi](bundling-and-minification/_static/image9.png)
3. [Ipaketleme Tatransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx) arabirimini uygulayan bir sınıf ekleyin. . Less dönüştürmesi için aşağıdaki kodu projenize ekleyin.

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. `LessTransform` ve [Cssminbelirt](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx) DÖNÜŞÜMÜYLE daha az dosya paketi oluşturun. Aşağıdaki kodu *uygulama\\_Start\\BundleConfig.cs* dosyası `RegisterBundles` yöntemine ekleyin.

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. Aşağıdaki kodu, daha az pakete başvuran görünümlere ekleyin.

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>Paket konuları

Paket oluştururken izlenmesi uygun bir kural, paket adına ön ek olarak "paket oluşturma" ekler. Bu, olası bir [yönlendirme çakışmasını](https://forums.asp.net/post/5012037.aspx)engeller.

Bir paketteki bir dosyayı güncelleştirdikten sonra, paket sorgu dizesi parametresi için yeni bir belirteç oluşturulur ve istemci paket içeren bir sayfa istediğinde tam paket indirilmelidir. Her varlığın ayrı olarak listelendiği geleneksel biçimlendirmede yalnızca değiştirilen dosya indirilir. Sık değişen varlıklar, paketleme için iyi aday olmayabilir.

Paketleme ve minbirleştirmesi birincil olarak ilk sayfa isteği yükleme süresini geliştirir. Bir Web sayfası istendiğinde, tarayıcı varlıkları (JavaScript, CSS ve görüntüler) önbelleğe alır, böylece paketleme ve küçültme, aynı sayfayı veya aynı varlıkları talep eden aynı sitedeki sayfaları talep etmek için herhangi bir performans artışı sağlamaz. Kullanım süresi üst bilgisini varlıklarınızda doğru ayarlamazsanız ve paketleme ve küçültme 'yı kullanmıyorsanız, tarayıcıların yeniliği buluşsal yöntemler, varlıkları birkaç günden sonra eski olarak işaretleyecek ve tarayıcı her varlık için bir doğrulama isteği gerektirecektir. Bu durumda, paketleme ve minbirleşme, ilk sayfa isteğinden sonra bir performans artışı sağlar. Ayrıntılar için bkz. [CDNs kullanarak blog ve Web sitesi performansını geliştirmek Için süre sonu](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx).

Her konak adı için aynı anda altı bağlantının tarayıcı sınırlaması bir [CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)kullanılarak azaltılabilir. CDN, barındırma sitenizden farklı bir ana bilgisayar adına sahip olduğundan, CDN 'den gelen varlık istekleri barındırma ortamınıza altı eşzamanlı bağlantı sınırına göre sayılmaz. CDN ayrıca ortak paket önbelleğe alma ve uç önbelleğe alma avantajları da sağlayabilir.

Paketler, gereken sayfalarla bölümlendirilmelidir. Örneğin, bir Internet uygulaması için varsayılan ASP.NET MVC şablonu jQuery 'tan ayrı bir jQuery doğrulama paketi oluşturur. Oluşturulan varsayılan görünümlerin girişi olmadığından ve değer göndermediğinden, doğrulama paketini içermez.

`System.Web.Optimization` ad alanı *System. Web. Optimization. dll*' de uygulanır. Daha sonra *Antlr3. Runtime. dll*' yi kullanan, minlıme özellikleri için WebGrease kitaplığından (*WebGrease. dll*) yararlanır.

*Hızlı postalar oluşturmak ve bağlantı paylaşmak Için Twitter kullanıyorum. Twitter tanıtıcım*: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>Ek kaynaklar

- Video: [barındırma](https://twitter.com/#!/howard_dierking) ile[paketleme ve iyileştirme](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing)
- Web [sayfaları sitesine Web Iyileştirmesi ekleme](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx).
- [Web Forms paketleme ve küçültmeye yönelik ekleme](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx).
- [Henrik F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk) [Web 'e göz atmaya yönelik paketleme ve küçültmeye yönelik performans etkileri](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx)
- Rick Anderson ile [Web sitesi performansını geliştirmek Için CDNs kullanma ve süresi doluyor](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)
- [RTT 'yi Küçült (gidiş dönüş süreleri)](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>Katkıda Bulunanlar

- Hao Kung
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana Lagül
