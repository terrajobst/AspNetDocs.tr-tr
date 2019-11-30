---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, Razor söz dizimi kullanarak ASP.NET Web sayfaları ile programlamaya genel bakış sunulmaktadır. ASP.NET, Microsoft 'un dinamik Web PA 'yi çalıştırmaya yönelik teknolojisidir...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564880"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (C#)

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, Razor söz dizimi kullanarak ASP.NET Web sayfaları ile programlamaya genel bakış sunulmaktadır. ASP.NET, Microsoft 'un web sunucularında dinamik Web sayfaları çalıştırmaya yönelik teknolojisidir. Bu makaleler, C# programlama dilini kullanmaya odaklanır.
> 
> Şunları **öğreneceksiniz**:
> 
> - Razor söz dizimi kullanarak programlama ASP.NET Web sayfaları ile çalışmaya başlama için en iyi 8 programlama ipuçları.
> - İhtiyaç duyacağınız temel programlama kavramları.
> - ASP.NET sunucu kodu ve Razor söz dizimi hepsi ile ilgilidir.
>   
> 
> ## <a name="software-versions"></a>Yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

## <a name="the-top-8-programming-tips"></a>Ilk 8 programlama Ipuçları

Bu bölümde, Razor söz dizimi kullanarak ASP.NET sunucu kodu yazmaya başladığınızda kesinlikle bilmeniz gereken birkaç ipucu listelenmektedir.

> [!NOTE]
> Razor söz dizimi, C# programlama dilini temel alır ve en sık kullanılan ASP.NET Web sayfaları olan dildir. Ancak Razor söz dizimi Ayrıca, Visual Basic dilini ve gördüğünüz her şeyi de Visual Basic de yapabilirsiniz. Ayrıntılar için bkz. ek [Visual Basic dili ve sözdizimi](https://go.microsoft.com/fwlink/?LinkId=202908).

Makalede daha sonra bu programlama tekniklerinin birçoğu hakkında daha fazla bilgi edinebilirsiniz.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. @ karakterini kullanarak bir sayfaya kod eklersiniz

`@` karakteri satır içi ifadeler, tek deyim blokları ve çok deyimli bloklar başlatır:

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

Bu deyimler, sayfa bir tarayıcıda çalıştırıldığında şöyle görünür:

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML kodlaması**
> 
> Önceki örneklerde olduğu gibi, `@` karakterini kullanarak bir sayfada içerik görüntülediğinizde, ASP.NET HTML-, çıktıyı kodluyor. Bu, ayrılmış HTML karakterlerinin (`<` ve `>` ve `&`), karakterlerin HTML etiketleri veya varlıklar olarak yorumlanıp bir Web sayfasında karakter olarak görüntülenmesini sağlayan kodlarla değiştirilir. HTML kodlaması olmadan, sunucu kodunuzun çıktısı doğru görüntülenmeyebilir ve güvenlik risklerine karşı bir sayfa sunabilir.
> 
> Amacınız etiketleri biçimlendirme olarak işleyen (örneğin, bir paragraf için `<p></p>` ya da metin vurgulamak için `<em></em>`) HTML işaretlemesinin çıktısını alıyorsa, bu makalenin ilerleyen kısımlarında yer alan [kod bloklarında metin, biçimlendirme ve kod birleştirme](#BM_CombiningTextMarkupAndCode) bölümüne bakın.
> 
> [Formlarla çalışırken](https://go.microsoft.com/fwlink/?LinkId=202892)HTML kodlaması hakkında daha fazla bilgi edinebilirsiniz.

### <a name="2-you-enclose-code-blocks-in-braces"></a>2. kod bloklarını küme ayraçları içine almalısınız

*Kod bloğu* bir veya daha fazla kod deyimi içerir ve küme ayraçları içine alınmıştır.

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. bir blok içinde her bir kod ifadesini noktalı virgülle sonlandırın

Bir kod bloğu içinde, tüm kod deyimlerinin noktalı virgülle bitmesi gerekir. Satır içi ifadeler noktalı virgül ile bitmiyor.

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. değerleri depolamak için değişkenleri kullanırsınız

Değerleri dizeler, sayılar ve tarihler gibi bir *değişkende*saklayabilirsiniz. `var` anahtar sözcüğünü kullanarak yeni bir değişken oluşturursunuz. `@`kullanarak doğrudan bir sayfada değişken değerleri ekleyebilirsiniz.

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-IMG3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. sabit dize değerlerini çift tırnak işaretleri içine alın

*Dize* , metin olarak kabul edilen bir karakter dizisidir. Bir dize belirtmek için, bunu çift tırnak işareti içine alın:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

Göstermek istediğiniz dize bir ters eğik çizgi karakteri (`\`) veya çift tırnak işareti (`"`) içeriyorsa, `@` işleci önekli bir tam *dize sabit değeri* kullanın. (İçinde C#, tam bir dize sabit değeri kullanmadığınız müddetçe, \ karakterinin özel anlamı vardır.)

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

Çift tırnak işaretleri eklemek için, tam bir dize değişmez değeri kullanın ve tırnak işaretlerini tekrarlayın:

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

Bu örneklerin her ikisini de bir sayfada kullanmanın sonucu aşağıda verilmiştir:

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> `@` karakterinin her ikisi de ' de C# tam dize sabit değerlerini işaretlemek için ve ASP.net sayfalarındaki kodu işaretlemek için kullanıldığına dikkat edin.

### <a name="6-code-is-case-sensitive"></a>6. kod büyük/küçük harfe duyarlıdır

' C#De, anahtar sözcükler (`var`, `true`ve `if`gibi) ve değişken adları büyük/küçük harfe duyarlıdır. Aşağıdaki kod satırları `lastName` ve `LastName.` iki farklı değişken oluşturur

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

Bir değişkeni `var lastName = "Smith";` olarak bildirir ve sayfanızdaki bu değişkene `@LastName`olarak başvuru yapmayı denerseniz, `"Smith"`yerine `"Jones"` değeri alırsınız.

> [!NOTE]
> Visual Basic, anahtar sözcükler ve değişkenler büyük/küçük harfe duyarlı *değildir* .

### <a name="7-much-of-your-coding-involves-objects"></a>7. kodlarınızın çoğu nesneleri içerir

Bir *nesne* , bir sayfa, metin kutusu, dosya &#8212; , görüntü, Web isteği, e-posta iletisi, müşteri kaydı (veritabanı satırı) vb. ile programlama yapamayacağınız şeyi temsil eder. Nesneler, özelliklerini betimleyen ve metin kutusu `Text` nesnesini okuyabilmeniz veya değiştirebilmeniz &#8212; için özelliklere sahiptir. bir istek nesnesi bir `Url` özelliğine sahiptir, bir e-posta iletisi bir `From` özelliğine sahiptir ve bir müşteri nesnesi bir `FirstName` özelliğine sahiptir. Nesneler, gerçekleştirebilecekleri&quot; &quot;fiiller olan yöntemlere de sahiptir. Bir dosya nesnesinin `Save` yöntemi, bir görüntü nesnesinin `Rotate` yöntemi ve bir e-posta nesnesinin `Send` yöntemi sayılabilir.

Genellikle sayfada metin kutularının (form alanları) değerleri, istek ne tür bir tarayıcı, isteğin URL 'SI, Kullanıcı kimliği vb. gibi bilgiler sunan `Request` nesnesiyle çalışırsınız. Aşağıdaki örnek, `Request` nesnesinin özelliklerine nasıl erişileceğinin yanı sıra sunucudaki sayfanın mutlak yolunu sağlayan `Request` nesnesinin `MapPath` yönteminin nasıl çağrılacağını gösterir:

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. kararları veren kodu yazabilirsiniz

Dinamik Web sayfalarının temel bir özelliği, koşullara göre ne yapılacağını belirleyebileceğinize bağlıdır. Bunu yapmanın en yaygın yolu `if` deyimidir (ve isteğe bağlı `else` deyimidir).

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

`if(IsPost)` ifade, `if(IsPost == true)`yazmanın bir Özet yoludur. `if` deyimleriyle birlikte, bu makalenin ilerleyen kısımlarında açıklanan koşulları test etme, kod blokları yineleme ve benzeri birçok yol vardır.

Sonuç tarayıcıda ( **Gönder**'e tıklandıktan sonra) gösterilir:

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET ve POST yöntemleri ve ıspost özelliği
> 
> Web sayfaları (HTTP) için kullanılan protokol, sunucuya istek yapmak için kullanılan çok sayıda yöntemi (fiil) destekler. En yaygın iki tane, bir sayfayı okumak için kullanılan ve bir sayfayı göndermek için kullanılan POST ' dır. Genellikle, Kullanıcı ilk kez bir sayfa istediğinde, sayfa GET kullanılarak istenir. Kullanıcı bir formu doldurduğunda ve sonra bir Gönder düğmesine tıkladığında, tarayıcı sunucuya bir POST isteği oluşturur.
> 
> Web programlamada, sayfayı nasıl işleyeceğini bilmeniz için bir sayfanın GET veya POST olarak istenmekte olduğunu bilmeniz genellikle yararlı olur. ASP.NET Web sayfalarında, bir isteğin bir GET veya POST olup olmadığını görmek için `IsPost` özelliğini kullanabilirsiniz. İstek bir GÖNDERIME ise, `IsPost` özelliği true döndürür ve bir formdaki metin kutularının değerlerini okumak gibi şeyler yapabilirsiniz. Birçok örnek, `IsPost`değerine bağlı olarak sayfayı farklı şekilde nasıl işleyeceğini gösterir.

## <a name="a-simple-code-example"></a>Basit bir kod örneği

Bu yordamda, temel programlama tekniklerini gösteren bir sayfanın nasıl oluşturulacağı gösterilmektedir. Örnekte, kullanıcıların iki sayı girmelerini sağlayan bir sayfa oluşturursunuz, sonra bunları ekler ve sonucu görüntüler.

1. Düzenleyicinizde yeni bir dosya oluşturun ve *AddNumbers. cshtml*olarak adlandırın.
2. Sayfada bulunan herhangi bir şeyi değiştirerek aşağıdaki kodu ve işaretlemeyi sayfaya kopyalayın.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    Dikkat etmeniz gereken bazı şeyler aşağıda verilmiştir:

    - `@` karakteri sayfadaki ilk kod bloğunu başlatır ve sayfanın alt kısmına yakın olan `totalMessage` değişkeninden önce gelir.
    - Sayfanın üst kısmındaki blok küme ayraçları içine alınır.
    - Üstteki blokta, tüm satırlar noktalı virgül ile biter.
    - Değişkenler `total`, `num1`, `num2`ve `totalMessage` çeşitli sayıları ve bir dizeyi depolar.
    - `totalMessage` değişkenine atanan sabit dize değeri çift tırnak işaretleri içinde.
    - Kod büyük/küçük harfe duyarlı olduğundan, `totalMessage` değişkeni sayfanın alt kısmında kullanıldığında, adının en üstteki değişkenle eşleşmesi gerekir.
    - İfade `num1.AsInt() + num2.AsInt()`, nesneler ve yöntemlerle çalışmayı gösterir. Her bir değişkendeki `AsInt` yöntemi, bir kullanıcı tarafından girilen dizeyi bir sayıya (bir tamsayı) dönüştürür, böylece bunun üzerinde aritmetik yapabilirsiniz.
    - `<form>` etiketi bir `method="post"` özniteliği içerir. Bu, Kullanıcı **Ekle**' ye tıkladığında, SAYFANıN http post yöntemi kullanılarak sunucuya gönderileceğini belirtir. Sayfa gönderildiğinde, `if(IsPost)` test doğru olarak değerlendirilir ve koşullu kod çalışır ve sayı ekleme sonucunu görüntüler.
3. Sayfayı kaydedin ve bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) İki tam sayı girin ve **Ekle** düğmesine tıklayın. 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>Temel programlama kavramları

Bu makalede, ASP.NET Web programlamaya genel bakış sunulmaktadır. Geniş bir inceleme değildir, yalnızca en sık kullanacağınız programlama kavramlarıyla hızlı bir tura katılın. Bu nedenle, ASP.NET Web sayfaları ile çalışmaya başlamak için ihtiyacınız olan neredeyse her şeyi de ele alır.

Ancak ilk olarak biraz teknik bir arka plan.

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor sözdizimi, sunucu kodu ve ASP.NET

Razor söz dizimi, bir Web sayfasına sunucu tabanlı kod eklemeye yönelik basit bir programlama sözdizimidir. Razor söz dizimi kullanan bir Web sayfasında, iki tür içerik vardır: istemci içeriği ve sunucu kodu. İstemci içeriği Web sayfalarında kullandığınız malzemedir: HTML biçimlendirme (öğeler), CSS gibi stil bilgileri, JavaScript gibi bazı istemci betikleri, belki de düz metin.

Razor söz dizimi, bu istemci içeriğine sunucu kodu eklemenize olanak tanır. Sayfada sunucu kodu varsa, sunucu tarayıcıya göndermeden önce bu kodu çalıştırır. Sunucu üzerinde çalışan kod, sunucu tabanlı veritabanlarına erişim gibi tek başına istemci içeriğini kullanarak çok daha karmaşık olabilecek görevler gerçekleştirebilir. En önemlisi, sunucu kodu istemci içeriğini &#8212; dinamik olarak oluşturabilir ve bu Işlem anında HTML biçimlendirme veya diğer içerik oluşturabilir ve ardından sayfanın içerebileceği herhangi BIR statik HTML ile birlikte tarayıcıya gönderebilir. Tarayıcınızın perspektifinden, sunucu kodunuz tarafından oluşturulan istemci içerikleri diğer istemci içeriğinden farklı değildir. Zaten gördüğünüz gibi, gereken sunucu kodu oldukça basittir.

Razor söz dizimi içeren ASP.NET Web sayfalarının özel bir dosya uzantısı ( *. cshtml* veya *. vbhtml*) vardır. Sunucu bu uzantıları tanır, Razor söz dizimi ile işaretlenen kodu çalıştırır ve sonra sayfayı tarayıcıya gönderir.

### <a name="where-does-aspnet-fit-in"></a>ASP.NET nereye sığacak?

Razor söz dizimi, Microsoft 'un Microsoft .NET Framework 'ü temel alan ASP.NET adlı bir teknolojiyi temel alır. The.NET Framework, Microsoft 'un neredeyse her türlü bilgisayar uygulamasının geliştirilmesi için büyük ve kapsamlı bir programlama çerçevesidir. ASP.NET, Web uygulamaları oluşturmak için özel olarak tasarlanan .NET Framework bölümüdür. Geliştiriciler dünyadaki en büyük ve en yüksek trafikli web sitelerinin çoğunu oluşturmak için ASP.NET kullandık. (Dosya adı uzantısı *. aspx* ' i BIR sitedeki URL 'nin bir parçası olarak gördüğünüz zaman, sitenin ASP.NET kullanılarak yazıldığını bilirsiniz.)

Razor söz dizimi, size ASP.NET 'un tüm gücünü sunar, ancak acemi bir uzman olduğunu öğrenmenizi ve uzman olduğunuzda daha üretken olmanızı sağlayan basitleştirilmiş bir sözdizimi kullanmanızı sağlar. Bu söz dizimi kullanımı basit olsa da, ASP.NET .NET Framework ile aile ilişkisi, Web siteleriniz daha karmaşık hale geldiği için, daha geniş çerçevelerin gücünden yararlanabilirsiniz.

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **Sınıflar ve örnekler**
> 
> ASP.NET sunucu kodu, sınıflarının fikir fikrini üzerine inşa edilen nesneleri kullanır. Sınıfı, bir nesnenin tanımı veya şablonudur. Örneğin, bir uygulama herhangi bir müşteri nesnesinin ihtiyacı olan özellikleri ve yöntemleri tanımlayan bir `Customer` sınıfı içerebilir.
> 
> Uygulamanın gerçek müşteri bilgileriyle çalışması gerektiğinde, bir müşteri nesnesi (veya *örnekleyen*) örneği oluşturur. Bireysel her müşteri, `Customer` sınıfının ayrı bir örneğidir. Her örnek aynı özellikleri ve yöntemleri destekler, ancak her bir müşteri nesnesi benzersiz olduğundan her örnek için özellik değerleri genellikle farklıdır. Bir müşteri nesnesinde, `LastName` özelliği "Smith" olabilir; başka bir müşteri nesnesinde, `LastName` özelliği "Jones" olabilir.
> 
> Benzer şekilde, sitenizdeki her bir Web sayfası, `Page` sınıfının bir örneği olan `Page` nesnesidir. Sayfadaki bir düğme, `Button` sınıfının bir örneği olan `Button` nesnesidir ve bu şekilde devam eder. Her örnek kendi özelliklerine sahiptir, ancak bunların hepsi nesnenin sınıf tanımında belirtilere göre belirlenir.

## <a name="basic-syntax"></a>Temel söz dizimi

Daha önce, bir ASP.NET Web sayfaları sayfası oluşturma ve HTML biçimlendirmesine sunucu kodu ekleme hakkında temel bir örnek gördünüz. Burada, programlama dili kuralları olan Razor söz dizimi &#8212; kullanarak ASP.NET sunucu kodu yazmanın temellerini öğreneceksiniz.

Programlamayla karşılaşırsanız (özellikle C, C++, C#, Visual Basic veya JavaScript kullandıysanız), burada okuduğunuzdan büyük bir şey tanıdık gelecektir. Muhtemelen yalnızca sunucu kodunun *. cshtml* dosyalarındaki biçimlendirmeye nasıl eklendiği hakkında bilgi almanız gerekir.

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>Kod bloklarında metin, biçimlendirme ve kod birleştirme

Sunucu kod blokları ' nda, genellikle sayfada metin veya biçimlendirme (veya her ikisi de) çıktısını almak istersiniz. Bir sunucu kod bloğu kod olmayan ve bunun yerine olarak işlenmesi gereken metin içeriyorsa, ASP.NET bu metni koddan ayırabilmelidir. Bunu yapmak için birkaç yol vardır.

- Metni `<p></p>` veya `<em></em>`gibi bir HTML öğesine koyun:   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML öğesi metin, ek HTML öğeleri ve sunucu kodu ifadelerini içerebilir. ASP.NET, açılan HTML etiketini (örneğin, `<p>`) gördüğünde, öğe ve içeriği gibi her şeyi tarayıcıya olduğu gibi işler ve sunucu kodu ifadelerini olduğu gibi çözer.
- `@:` işlecini veya `<text>` öğesini kullanın. `@:` düz metin veya eşleşmeyen HTML etiketleri içeren tek bir içerik satırı çıktısı verir; `<text>` öğesi çıktı için birden çok satır barındırır. Bu seçenekler, çıktının bir parçası olarak bir HTML öğesi işlemek istemediğinizde yararlıdır.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    Metnin birden çok satırını veya eşleşmeyen HTML etiketlerini çıkarmak istiyorsanız, her satırın önüne `@:`veya satırı bir `<text>` öğesine ekleyebilirsiniz. `@:` işleci gibi`<text>` Etiketler, metin içeriğini belirlemek için ASP.NET tarafından kullanılır ve sayfa çıktısında hiçbir şekilde işlenmez.

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    İlk örnek, önceki örneği yineler, ancak işlenecek metni kapsamak için tek bir çift `<text>` etiketi kullanır. İkinci örnekte, `<text>` ve `</text>` etiketleri üç satırı kapsar; bunların hepsi, sunucu kodu ve eşleşen HTML etiketleriyle birlikte, bazı metin ve eşleşmeyen HTML etiketlerine (`<br />`) sahiptir. Ayrıca, `@:` işleçle her bir satırdan de tek başına bir kez daha olabilirsiniz; Her iki yöntem de geçerlidir.

    > [!NOTE]
    > Bu bölümde &#8212; gösterildiği gibi metin yazdığınızda, bir HTML öğesi, `@:` işleci veya `<text>` öğesi &#8212; ASP.net, çıktıyı HTML olarak kodlamaz. (Daha önce belirtildiği gibi, ASP.NET, bu bölümde belirtilen özel durumlar dışında, daha önce `@`sunucu kod ifadelerinin ve sunucu kodu bloklarının çıkışını kodladır.)

### <a name="whitespace"></a>Boşlu

Deyimdeki (ve dize sabit değerinin dışında) fazladan boşluklar, bu ifadeyi etkilemez:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

Deyimdeki bir satır sonu deyim üzerinde hiçbir etkiye sahip değildir ve daha okunaklı olması için deyimleri kaydırabilirsiniz. Aşağıdaki deyimler aynıdır:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

Ancak, bir satırı dize sabit değerinin ortasında kaydıramazsınız. Aşağıdaki örnek çalışmıyor:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

Yukarıdaki kod gibi birden çok satıra kaydırılan uzun bir dizeyi birleştirmek için iki seçenek vardır. Bu makalede daha sonra göreceğiniz birleştirme işlecini (`+`) kullanabilirsiniz. Bu makalede daha önce gördüğünüz gibi, tam bir dize sabiti oluşturmak için `@` karakterini de kullanabilirsiniz. Satırlar arasında tam dize sabit değerlerini kesebilirsiniz:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>Kod (ve biçimlendirme) açıklamaları

Açıklamalar sizin veya diğerleri için Not bırakmayı sağlar. Ayrıca, çalıştırmak istemediğiniz bir kod veya biçimlendirme bölümünü (*Açıklama*olarak) devre dışı bırakabilmeniz, ancak sayfada çalışmaya devam etmek isteyeceksiniz.

Razor kodu ve HTML işaretlemesi için farklı yorum sözdizimi vardır. Tüm razor kodlarında olduğu gibi, sayfa tarayıcıya gönderilmeden önce, Razor açıklamaları sunucu üzerinde işlenir (ve sonra kaldırılır). Bu nedenle, Razor açıklama sözdizimi, dosyayı düzenlerken görebileceğiniz, ancak sayfa kaynağında bile Kullanıcı görmemiş olan koda (veya biçimlendirme içine) yorum koymanıza imkan tanır.

ASP.NET Razor açıklamaları için, yorumu `@*` ile başlatır ve `*@`ile sonlandırın. Yorum bir veya birden çok satırda olabilir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

Kod bloğu içindeki bir açıklama aşağıda verilmiştir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

Bu kod, kod satırı açıklama satırı ile birlikte, aşağıdaki çalıştırılmayacak şekilde kod bloğu aşağıda verilmiştir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

Bir kod bloğu içinde, Razor açıklama sözdizimi kullanmanın alternatifi olarak, kullanmakta olduğunuz programlama dilinin yorum söz dizimini kullanabilirsiniz, örneğin C#:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

' C#De, tek satırlık açıklamaların önünde `//` karakterleri ve çok satırlı açıklamalar `/*` ile başlayıp `*/`ile biter. (Razor yorumlarında olduğu gibi C# , açıklamalar tarayıcıda işlenmez.)

Biçimlendirme için, büyük olasılıkla bildiğiniz gibi, bir HTML açıklaması oluşturabilirsiniz:

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML açıklamaları `<!--` karakterle başlar ve `-->`biter. HTML açıklamalarını yalnızca metin değil, aynı zamanda sayfada tutmak isteyebileceğiniz ancak işlemek istemediğiniz HTML işaretlemesini kullanabilirsiniz. Bu HTML yorumu, etiketlerin ve içerdikleri metnin tüm içeriğini gizler:

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

Razor yorumlarından farklı olarak, HTML açıklamaları *sayfada işlenir ve* Kullanıcı bunları sayfa kaynağını görüntüleyerek görebilir.

Razor 'in C#iç içe bloklar üzerinde sınırlamalar vardır. Daha fazla bilgi için bkz. [ C# adlandırılmış değişkenler ve Iç Içe bloklar bozuk kod oluşturur](http://aspnetwebstack.codeplex.com/workitem/1914)

## <a name="variables"></a>Değişkenler

Değişken, verileri depolamak için kullandığınız adlandırılmış bir nesnedir. Değişkenleri herhangi bir şekilde adlandırın, ancak ad alfabetik bir karakterle başlamalı ve boşluk ya da ayrılmış karakterler içeremez.

### <a name="variables-and-data-types"></a>Değişkenler ve veri türleri

Değişken, değişkende ne tür verilerin depolandığını gösteren belirli bir veri türüne sahip olabilir. Dize değerlerini depolayan dize değişkenleriniz (&quot;Hello World&quot;), tam sayı değerlerini depolayan tamsayı değişkenleri (3 veya 79 gibi) ve tarih değerlerini çeşitli biçimlerde depolayan Tarih değişkenlerini (4/12/2012 veya Mart 2009 gibi) kullanabilirsiniz. Ve kullanabileceğiniz pek çok farklı veri türü vardır.

Ancak, genellikle bir değişken için bir tür belirtmeniz gerekmez. Çoğu zaman, ASP.NET değişkende bulunan verilerin nasıl kullanıldığını temel alarak türü belirleyebilir. (Bazen bir tür belirtmeniz gerekir; bunun doğru olduğu örnekleri görürsünüz.)

`var` anahtar sözcüğünü kullanarak bir değişken bildirir (bir tür belirtmek istemiyorsanız) veya türün adını kullanarak:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

Aşağıdaki örnekte, bir Web sayfasındaki değişkenlerin bazı tipik kullanımları gösterilmektedir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

Önceki örnekleri bir sayfada birleştirirseniz, bunu bir tarayıcıda görüntülenmiş olarak görürsünüz:

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>Veri türlerini dönüştürme ve test etme

ASP.NET genellikle bir veri türünü otomatik olarak belirleyebilse de bazen olamaz. Bu nedenle, açık bir dönüştürme gerçekleştirerek ASP.NET Out 'a yardımcı olmanız gerekebilir. Türleri dönüştürmeniz gerekmese de, ne zaman çalıştığınız veri türlerini görmek için test etmeniz yararlı olur.

En yaygın durum, bir dizeyi tamsayı veya tarih gibi başka bir türe dönüştürmeniz gerekir. Aşağıdaki örnek, bir dizeyi bir sayıya dönüştürmeniz gereken tipik bir durumu gösterir.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

Kural olarak, Kullanıcı girişi size dizeler olarak gelir. Kullanıcılardan bir sayı girmeleri ve bir rakam girseler bile, Kullanıcı girişi gönderildiğinde ve kodu kodda okuduğunuzda, veriler dize biçimindedir. Bu nedenle, dizeyi bir sayıya dönüştürmeniz gerekir. Örnekte, değerleri dönüşümlemeden aritmetik gerçekleştirmeye çalışırsanız, ASP.NET iki dize ekleyemediğinden aşağıdaki hata oluşur:

*' String ' türü örtük olarak ' int ' türüne dönüştürülemez.*

Değerleri tamsayılara dönüştürmek için `AsInt` yöntemini çağırın. Dönüştürme başarılı olursa, sayıları ekleyebilirsiniz.

Aşağıdaki tabloda, değişkenler için bazı ortak dönüştürme ve test yöntemleri listelenmektedir.

:::row:::
    :::column:::
    <strong>Yöntemidir</strong>
    :::column-end:::
    :::column:::
    <strong>Açıklama</strong>
    :::column-end:::
    :::column:::
    <strong>Örnek</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    Tam sayıyı temsil eden bir dizeyi ("593" gibi) tamsayıya dönüştürür.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    &quot;true&quot; veya &quot;false&quot; gibi bir dizeyi Boolean bir türe dönüştürür.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    &quot;1,3&quot; veya &quot;&quot; 7,439 gibi ondalık değeri olan bir dizeyi kayan noktalı bir sayıya dönüştürür.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    &quot;1,3&quot; veya &quot;&quot; 7,439 gibi ondalık bir değere sahip bir dizeyi ondalık bir sayıya dönüştürür. (ASP.NET ' de, ondalık sayı bir kayan noktalı sayıdan daha belirgin olur.)
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    Bir tarih ve saat değerini temsil eden bir dizeyi ASP.NET `DateTime` türüne dönüştürür.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    Diğer veri türlerini bir dizeye dönüştürür.
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>İşleçler

İşleci, bir ifadede ne tür komutun gerçekleştirileceğini ASP.NET söyleyen bir anahtar sözcüktür veya karakterdir. C# Dil (ve buna dayalı Razor söz dizimi) birçok işleci destekler, ancak kullanmaya başlamak için yalnızca birkaç tane tanımak yeterlidir. Aşağıdaki tabloda en yaygın operatörler özetlenmektedir.

:::row:::
    :::column:::
    <strong>İşlecinde</strong>
    :::column-end:::
    :::column:::
    <strong>Açıklama</strong>
    :::column-end:::
    :::column:::
    <strong>Örnekler</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    Sayısal ifadelerde kullanılan matematik işleçleri.
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    Atama. Bir deyimin sağ tarafındaki değeri, sol taraftaki nesneye atar.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    Eþit. Değerler eşitse `true` döndürür. (`=` işleci ve `==` işleci arasındaki ayrımı fark ettiğini unutmayın.)
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    Olmama. Değerler eşit değilse `true` döndürür.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    Küçüktür, büyüktür, küçüktür, küçüktür ve eşittir, veya eşittir.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    Dizeleri birleştirmek için kullanılan birleştirme. ASP.NET bu işleç ile toplama işleci arasındaki farkı, ifadenin veri türüne göre bilir.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=``-=`
    :::column-end:::
    :::column:::
    Bir değişkenden 1 (sırasıyla) ekleyen ve çıkartacak artırma ve azaltma işleçleri.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    Nokta. Nesneleri ve bunların özelliklerini ve yöntemlerini ayırt etmek için kullanılır.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    Ayraçlar. İfadeleri gruplandırmak ve parametreleri yöntemlere geçirmek için kullanılır.
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    Köşeli. Dizilerde veya koleksiyonlardaki değerlere erişmek için kullanılır.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    Başlatılmadı. `true` bir değeri `false` tersine çevirir ve tam tersi de geçerlidir. Genellikle `false` test etmek için (`true`değil) kısayol yöntemi olarak kullanılır.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&``||`
    :::column-end:::
    :::column:::
    Koşulları birbirine bağlamak için kullanılan mantıksal AND ve OR.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a>Kodda dosya ve klasör yollarıyla çalışma

Genellikle kodunuzda dosya ve klasör yolları ile çalışırsınız. Geliştirme bilgisayarınızda görünebilen bir Web sitesi için fiziksel klasör yapısına bir örnek aşağıda verilmiştir:

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

URL 'Ler ve yollarla ilgili bazı temel ayrıntılar aşağıda verilmiştir:

- URL, bir etki alanı adı (`http://www.example.com`) veya sunucu adı (`http://localhost`, `http://mycomputer`) ile başlar.
- Bir URL, ana bilgisayardaki fiziksel bir yola karşılık gelir. Örneğin, `http://myserver` sunucuda *C:\websites\mywebsite* klasörüne karşılık gelebilir.
- Sanal yol, tüm yolu belirtmek zorunda kalmadan koddaki yolları temsil etmek için toplu bir yoldur. Bu, etki alanı veya sunucu adını izleyen bir URL 'nin bölümünü içerir. Sanal yollar kullandığınızda, yolları güncelleştirmek zorunda kalmadan kodunuzu farklı bir etki alanına veya sunucuya taşıyabilirsiniz.

Farklılıkları anlamanıza yardımcı olacak bir örnek aşağıda verilmiştir:

| URL 'YI doldurun | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| Sunucu adı | *mycompanyserver* |
| Sanal yol | */humanresources/CompanyPolicy.htm* |
| Fiziksel yol | *C:\websites\humanresources\companypolicy.htm* |

Sanal kök, C: sürücünüzün kökünde olduğu gibi/olur. (Sanal klasör yolları her zaman eğik çizgi kullanır.) Bir klasörün sanal yolunun fiziksel klasörle aynı ada sahip olması gerekmez; Bu bir diğer ad olabilir. (Üretim sunucularında, sanal yol nadiren tam bir fiziksel yolla eşleşir.)

Kodda dosya ve klasörlerle çalışırken, çalıştığınız nesnelere bağlı olarak, bazen fiziksel yola ve bazen bir sanal yola başvurmanız gerekir. ASP.NET, kodda dosya ve klasör yollarıyla çalışmak için size bu araçları sağlar: `Server.MapPath` yöntemi ve `~` işleci ve `Href` yöntemi.

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>Sanal fiziksel yollara dönüştürme: Server. MapPath yöntemi

`Server.MapPath` yöntemi, bir sanal yolu ( */default.exe*gibi) mutlak bir fiziksel yola ( *C:\websites\mywebsitefolder\default.exe*gibi) dönüştürür. Bu yöntemi, tüm fiziksel yola ihtiyacınız olduğunda kullanırsınız. Tipik bir örnek, Web sunucusunda bir metin dosyası veya resim dosyası okurken veya yazarken bir örnektir.

Genellikle sitenizin bir barındırma sitesinin sunucusunda mutlak fiziksel yolunu bilemezsiniz; bu nedenle, bu yöntem, bildiğiniz yolu (sanal yol) sizin için sunucuda karşılık gelen yola dönüştürebilir. Bir dosya veya klasörün sanal yolunu yöntemine geçirirsiniz ve fiziksel yolu döndürür:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>Sanal köke başvuruluyor: ~ operator ve href yöntemi

Bir *. cshtml* veya *. vbhtml* dosyasında, `~` işlecini kullanarak sanal kök yoluna başvurabilirsiniz. Sayfaları bir sitede bir konuma taşıyabilmeniz ve içerdikleri bağlantıların diğer sayfalara bölünememesi nedeniyle bu çok yararlı olur. Web sitenizi farklı bir konuma taşımanız durumunda da yararlıdır. Aşağıda bazı örnekler verilmiştir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

Web sitesi `http://myserver/myapp`, sayfa çalışırken ASP.NET bu yolları nasıl değerlendilecektir:

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`

(Bu yolları gerçekten değişkenin değerleri olarak görmezsiniz, ancak ASP.NET, bu gibi yollar gibi davranır.)

`~` işlecini hem sunucu kodunda (yukarıdaki gibi) hem de biçimlendirme ' de şu şekilde kullanabilirsiniz:

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

Biçimlendirme ' de, görüntü dosyaları, diğer Web sayfaları ve CSS dosyaları gibi kaynaklara yollar oluşturmak için `~` işlecini kullanırsınız. Sayfa çalıştığında, ASP.NET sayfayı (hem kod hem de biçimlendirme) arar ve tüm `~` başvurularını uygun yola çözümler.

## <a name="conditional-logic-and-loops"></a>Koşullu mantık ve döngüler

ASP.NET sunucu kodu, koşullara göre görevleri gerçekleştirmenize ve deyimleri belirli sayıda kez tekrardan (bir döngü çalıştıran kod) tekrarlamanızı sağlar.

### <a name="testing-conditions"></a>Test koşulları

Basit bir koşulu test etmek için, belirttiğiniz bir teste göre doğru veya yanlış döndüren `if` deyiminizi kullanırsınız:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if` anahtar sözcüğü bir blok başlatır. Gerçek test (koşul) parantez içinde ve true veya false değerini döndürür. Test true olursa çalıştırılan deyimler küme ayraçları içine alınmıştır. `if` deyimi, koşul yanlış ise çalıştırılacak deyimleri belirten bir `else` bloğu içerebilir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

`else if` bloğunu kullanarak birden çok koşul ekleyebilirsiniz:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

Bu örnekte, IF bloğundaki ilk koşul true değilse `else if` koşulu denetlenir. Bu koşul karşılanıyorsa, `else if` bloğundaki deyimler yürütülür. Koşulların hiçbiri karşılanmazsa, `else` bloğundaki deyimler yürütülür. Herhangi bir sayıda başka If bloğu ekleyebilirsiniz ve ardından &quot;başka&quot; koşulu olan her şeyi `else` bir blok ile kapatabilirsiniz.

Çok sayıda koşulu test etmek için `switch` bloğunu kullanın:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

Sınanacak değer parantez içinde (örnekte, `weekday` değişken). Her bir test, iki nokta üst üste (:) ile biten `case` bir ifade kullanır. Bir `case` deyimin değeri test değeriyle eşleşiyorsa, bu durum bloğundaki kod yürütülür. Her Case ifadesini bir `break` ifadesiyle kapatırsınız. (Her bir `case` bloğuna kesme eklemeyi unutursanız, sonraki `case` deyimindeki kod de çalıştırılır.) `switch` bloğu, diğer durumların hiçbiri doğru değilse, başka bir &quot;her şey&quot; seçeneğinin son durumu olarak bir `default` bildirimine sahiptir.

Bir tarayıcıda görünen son iki koşullu blok sonucu:

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>Döngü kodu

Genellikle aynı deyimleri tekrar tekrar çalıştırmanız gerekir. Bu, döngüye göre yapılır. Örneğin, çoğu kez bir veri koleksiyonundaki her öğe için aynı deyimleri çalıştırırsınız. Kaç kez döngüye almak istediğinizi biliyorsanız `for` döngüsünü kullanabilirsiniz. Bu tür bir döngü, özellikle daha fazla sayım veya sayım için yararlıdır:

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

Döngü `for` anahtar sözcüğüyle başlar, sonra parantez içinde üç deyim gelir, her biri noktalı virgül ile sonlandırılır.

- Parantez içinde, ilk ifade (`var i=10;`) bir sayaç oluşturur ve 10 ' a başlatır. Herhangi bir değişkeni kullanabileceğiniz `i` &#8212; sayaç adını yazmanız gerekmez. `for` döngüsü çalıştığında, sayaç otomatik olarak artırılır.
- İkinci ifade (`i < 21;`), ne kadar saymak istediğinize ilişkin koşulu ayarlar. Bu durumda, en fazla 20 ' ye gitmesini istersiniz (yani sayaç 21 ' den az olduğunda devam edin).
- Üçüncü ifade (`i++`) bir artırma işleci kullanır, bu da her döngü her çalıştığında sayacın kendisine 1 ekleneceğini belirtir.

Küme ayraçları içinde döngünün her yinelemesi için çalıştırılacak koddur. Biçimlendirme, her seferinde yeni bir paragraf (`<p>` öğesi) oluşturur ve `i` değerini (sayaç) görüntüleyerek çıktıya bir satır ekler. Bu sayfayı çalıştırdığınızda örnek, her satırda öğe numarasını gösteren metinle birlikte çıktıyı görüntüleyen 11 satır oluşturur.

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

Bir koleksiyon veya dizi ile çalışıyorsanız, genellikle bir `foreach` döngüsü kullanırsınız. Bir koleksiyon benzer nesneler grubudur ve `foreach` döngüsü koleksiyondaki her öğe üzerinde bir görevi gerçekleştirmenizi sağlar. Bu tür bir döngü koleksiyonlar için uygundur, çünkü `for` döngüsünün aksine sayacı artırmanız veya bir sınır ayarlamanız gerekmez. Bunun yerine, `foreach` döngü kodu yalnızca, tamamlanana kadar koleksiyon üzerinden ilerler.

Örneğin, aşağıdaki kod, Web sunucunuz hakkında bilgi içeren bir nesnesi olan `Request.ServerVariables` koleksiyonundaki öğeleri döndürür. HTML madde işaretli listesinde yeni bir `<li>` öğesi oluşturarak her öğenin adını göstermek için `foreac` h döngüsünü kullanır.

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach` anahtar kelimesinin ardından, koleksiyondaki tek bir öğeyi temsil eden (örnekte, `var item`), ardından `in` anahtar sözcüğünü ve ardından, sonra da kullanmak istediğiniz koleksiyonu içeren bir değişken bildirdiğiniz parantezler gelir. `foreach` döngüsünün gövdesinde, daha önce bildirdiğiniz değişkeni kullanarak geçerli öğeye erişebilirsiniz.

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

Daha genel amaçlı bir döngü oluşturmak için `while` ifadesini kullanın:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

Bir `while` döngüsü, `while` anahtar sözcüğüyle başlar ve sonra parantez, döngünün ne kadar süreyle devam ettiğini (`countNum` 50 ' den az olduğu sürece), sonra da yinelemeyi yineleme olarak belirler. Döngüler genellikle sayma için kullanılan bir değişken veya nesneden artış (ekleme) veya azaltma (çıkarma). Örnekte, `+=` işleci döngünün her çalıştığında `countNum` 1 ' i ekler. (Döngüsel bir döngüsünde bir değişkeni azaltmak için, azaltma işleci `-=`) kullanın.

## <a name="objects-and-collections"></a>Nesneler ve koleksiyonlar

Bir ASP.NET Web sitesindeki neredeyse her şey, Web sayfasının kendisi de dahil olmak üzere bir nesnedir. Bu bölümde, kodunuzda sıkça çalışacağımız bazı önemli nesneler açıklanmaktadır.

### <a name="page-objects"></a>Sayfa nesneleri

ASP.NET ' deki en temel nesne, sayfasıdır. Sayfa nesnesinin özelliklerine, uygun herhangi bir nesne olmadan doğrudan erişebilirsiniz. Aşağıdaki kod, sayfanın `Request` nesnesini kullanarak sayfanın dosya yolunu alır:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

Geçerli sayfa nesnesindeki özelliklere ve yöntemlere başvurduğunuzdan emin olmak için, kodunuzda sayfa nesnesini göstermek üzere `this` anahtar sözcüğünü kullanabilirsiniz. Aşağıda, sayfayı göstermek için `this` eklenen önceki kod örneği verilmiştir:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

`Page` nesnenin özelliklerini kullanarak çok fazla bilgi alabilirsiniz:

- `Request`. Zaten gördüğünüze göre, bu, istek ne tür bir tarayıcı, sayfanın URL 'SI, Kullanıcı kimliği vb. gibi geçerli istek hakkındaki bilgilerin bir koleksiyonudur.
- `Response`. Bu, sunucu kodunun çalışmayı tamamladığında tarayıcıya gönderilecek yanıt (sayfa) hakkındaki bilgilerin bir koleksiyonudur. Örneğin, yanıta bilgi yazmak için bu özelliği kullanabilirsiniz. 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>Koleksiyon nesneleri (diziler ve sözlükler)

Bir *koleksiyon* , bir veritabanından `Customer` nesneleri koleksiyonu gibi aynı türde bir nesne grubudur. ASP.NET, `Request.Files` koleksiyonu gibi birçok yerleşik koleksiyon içerir.

Genellikle koleksiyonlardaki verilerle çalışırsınız. İki ortak koleksiyon türü *dizi* ve *sözlüktür*. Bir dizi benzer öğeler koleksiyonunu depolamak istediğinizde ancak her bir öğeyi tutacak ayrı bir değişken oluşturmak istemediğinizde yararlıdır:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

Diziler ile, `string`, `int`veya `DateTime`gibi belirli bir veri türünü bildirirsiniz. Değişkenin bir dizi içerebileceğini göstermek için bildirime köşeli ayraç eklersiniz (`string[]` veya `int[]`gibi). Bir dizideki öğelere konumlarını (Dizin) veya `foreach` ifadesini kullanarak erişebilirsiniz. Dizi dizinleri sıfır tabanlıdır &#8212; , ilk öğe 0 ' dır, ikinci öğe ise 1 konumunda ve bu şekilde devam eder.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

Bir dizideki öğelerin sayısını `Length` özelliğini alarak belirleyebilirsiniz. Dizideki belirli bir öğenin konumunu almak için (diziyi aramak için) `Array.IndexOf` yöntemini kullanın. Ayrıca, bir dizinin içeriğini ters çevirme (`Array.Reverse` yöntemi) veya içeriği sıralama (`Array.Sort` yöntemi) gibi işlemleri de yapabilirsiniz.

Bir tarayıcıda görünen dize dizisi kodunun çıkışı:

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

Sözlük, anahtar/değer çiftleri koleksiyonudur ve buna karşılık gelen değeri ayarlamak ya da almak için anahtarı (veya adı) sağlarsınız:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

Sözlük oluşturmak için, `new` anahtar sözcüğünü kullanarak yeni bir sözlük nesnesi kullandığınızı belirtebilirsiniz. `var` anahtar sözcüğünü kullanarak bir değişkene bir sözlük atayabilirsiniz. Sözlükteki öğelerin veri türlerini köşeli ayraç (`< >`) kullanarak gösterebilirsiniz. Bildirimin sonunda, bu gerçekte yeni bir sözlük oluşturan bir yöntem olduğundan, parantez çifti eklemeniz gerekir.

Sözlüğe öğe eklemek için, sözlük değişkeninin (Bu durumda`myScores`) `Add` yöntemini çağırabilir ve sonra bir anahtar ve bir değer belirtebilirsiniz. Alternatif olarak, aşağıdaki örnekte olduğu gibi anahtarı göstermek ve basit bir atama yapmak için köşeli ayraçları kullanabilirsiniz:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

Sözlükten bir değer almak için anahtarı köşeli ayraç içinde belirtirsiniz:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>Yöntemler parametrelerle çağırma

Bu makalede daha önce okuduğunuzdan, ile programlarındaki nesneler yöntemlere sahip olabilir. Örneğin, bir `Database` nesnesi bir `Database.Connect` yöntemine sahip olabilir. Birçok yöntemde de bir veya daha fazla parametre vardır. *Parametresi* , bir yöntemine geçirdiğiniz bir değerdir ve bu yöntem, görevini tamamlamaya yönelik yöntemi etkinleştirir. Örneğin, üç parametre alan `Request.MapPath` yöntemi için bir bildirime bakın:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

(Satır daha okunabilir hale getirmek için sarmalanmış. Satır sonlarını, tırnak işaretleri içine alınan dizeler hariç neredeyse her bir yere koyabildiğiniz unutulmamalıdır.)

Bu yöntem, belirtilen sanal yola karşılık gelen sunucudaki fiziksel yolu döndürür. Yöntemi için üç parametre `virtualPath`, `baseVirtualDir`ve `allowCrossAppMapping`. (Bildiriminde, parametrelerin kabul edeceği verilerin veri türleriyle listelendiğine dikkat edin.) Bu yöntemi çağırdığınızda, üç parametrenin de değerlerini sağlamanız gerekir.

Razor söz dizimi, parametreleri bir yönteme geçirmek için kullanabileceğiniz iki seçenek sunar: *Konumsal parametreler* ve *adlandırılmış parametreler*. Konumsal parametreleri kullanarak bir yöntemi çağırmak için, parametreleri yöntem bildiriminde belirtilen katı bir sıraya geçirin. (Bu sırayı genellikle yöntemi için belgeleri okuyarak bilirsiniz.) Sırayı izlemeniz gerekir ve gerekirse parametrelerden &#8212; hiçbirini atlayamazsınız, bir değeri olmayan bir Konumsal parametre için boş bir dize (`""`) veya `null` geçirin.

Aşağıdaki örnek, Web sitenizde *betikler* adında bir klasörünüz olduğunu varsayar. Kod `Request.MapPath` yöntemini çağırır ve üç parametrenin değerlerini doğru sırada geçirir. Ardından, sonuçta elde edilen eşleştirilmiş yolu görüntüler.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

Bir yöntemin çok sayıda parametresi olduğunda, adlandırılmış parametreleri kullanarak kodunuzun daha okunabilir olmasını sağlayabilirsiniz. Adlandırılmış parametreleri kullanarak bir yöntemi çağırmak için parametre adının ardından iki nokta üst üste (:) ve ardından değeri belirtirsiniz. Adlandırılmış parametrelerin avantajı, bunları istediğiniz sırada geçirebilmeniz. (Bir dezavantajı yöntem çağrısının sıkışık olmaması.)

Aşağıdaki örnek, yukarıdaki gibi aynı yöntemi çağırır, ancak değerleri sağlamak için adlandırılmış parametreleri kullanır:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

Görebileceğiniz gibi, parametreler farklı bir sırayla geçirilir. Ancak, önceki örneği çalıştırırsanız ve bu örnekte, aynı değer döndürülür.

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>Hataları İşleme

### <a name="try-catch-statements"></a>Try-catch deyimleri

Kodunuzda, denetiminizin dışındaki nedenlerle başarısız olabilecek deyimler vardır. Örneğin:

- Kodunuz bir dosya oluşturmayı veya bir dosyayı erişmeyi denediğinde, tüm hata sıralamaları meydana gelebilir. İstediğiniz dosya mevcut olmayabilir, kilitli olabilir, kod izinlere sahip olmayabilir ve bu şekilde devam eder.
- Benzer şekilde, kodunuz bir veritabanındaki kayıtları güncelleştirmeye çalışırsa, izin sorunları olabilir, veritabanı bağlantısı bırakılmış olabilir, kaydedilecek veriler geçersiz olabilir ve bu şekilde devam eder.

Programlama koşullarında, bu durumlara *özel durumlar*denir. Kodunuz bir özel durumla karşılaşırsa, en iyi şekilde kullanıcılara sinir bozucu bir hata iletisi üretir (atar):

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

Kodunuzun özel durumlarla karşılaşmasına ve bu türden hata iletilerinden kaçınmak için `try/catch` deyimlerini kullanabilirsiniz. `try` bildiriminde, kontrol ettiğiniz kodu çalıştırırsınız. Bir veya daha fazla `catch` deyiminde, oluşmuş olabilecek belirli hatalara (özel durum türleri) bakabilirsiniz. Benimsemeyi bekleme olduğunuz hatalara bakmak için gereken sayıda `catch` deyimi ekleyebilirsiniz.

> [!NOTE]
> `try/catch` deyimlerde `Response.Redirect` yöntemini kullanmaktan kaçınmanızı öneririz, çünkü sayfanızda bir özel duruma neden olabilir.

Aşağıdaki örnek, ilk istekte bir metin dosyası oluşturan ve sonra kullanıcının dosyayı açmasına olanak tanıyan bir düğme görüntüleyen bir sayfa gösterir. Örnek, bir özel duruma neden olacak şekilde hatalı bir dosya adı kullanır. Kod, olası iki özel durum için `catch` deyimlerini içerir: dosya adı bozuksa oluşan `FileNotFoundException`ve ASP.NET bile klasörü bulamazsa oluşan `DirectoryNotFoundException`. (Her şey düzgün şekilde çalıştığında nasıl çalıştığını görmek için örnekteki bir deyimin açıklamasını değiştirebilirsiniz.)

Kodunuz özel durumu işlemediyse, önceki ekran görüntüsündeki gibi bir hata sayfası görürsünüz. Ancak, `try/catch` bölümü kullanıcının bu hata türlerini görmesini önlemeye yardımcı olur.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

**Visual Basic ile programlama**

[Ek: Visual Basic dil ve sözdizimi](https://go.microsoft.com/fwlink/?LinkId=202908)

**Başvuru belgeleri**

[ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)

[C#Dildir](https://msdn.microsoft.com/library/kx37x362.aspx)
