---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (Visual Basic) | Microsoft Docs
author: Rick-Anderson
description: Bu ekte, Razor söz dizimi kullanarak Visual Basic Web sayfaları ile programlamaya genel bakış sunulmaktadır.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526595"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş (Visual Basic)

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, Razor söz dizimi ve Visual Basic kullanarak ASP.NET Web sayfalarıyla programlama hakkında genel bakış sunulmaktadır. ASP.NET, Microsoft 'un web sunucularında dinamik Web sayfaları çalıştırmaya yönelik teknolojisidir.
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

Razor söz dizimi kullanımı C#Ile ASP.NET Web sayfaları kullanmanın çoğu örneği. Ancak Razor söz dizimi de Visual Basic destekler. Visual Basic bir ASP.NET Web sayfasını programlamak için *. vbhtml* dosya adı uzantısıyla bir Web sayfası oluşturun ve sonra Visual Basic kodu ekleyin. Bu makalede, ASP.NET Web sayfaları oluşturmak için Visual Basic dili ve söz dizimi ile çalışmaya ilişkin bir genel bakış sunulmaktadır.

> [!NOTE]
> Microsoft WebMatrix için varsayılan Web sitesi şablonları (**Bakçılık**, **Fotoğraf Galerisi**ve **Başlangıç sitesi**, vb.), C# ve Visual Basic sürümlerde mevcuttur. Visual Basic şablonlarını NuGet paketleri olarak yükleyebilirsiniz. Web sitesi şablonları, sitenizin kök klasörüne *Microsoft şablonlar*adlı bir klasöre yüklenir.

## <a name="the-top-8-programming-tips"></a>Ilk 8 programlama Ipuçları

Bu bölümde, Razor söz dizimi kullanarak ASP.NET sunucu kodu yazmaya başladığınızda kesinlikle bilmeniz gereken birkaç ipucu listelenmektedir.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. @ karakterini kullanarak bir sayfaya kod eklersiniz

`@` karakter, satır içi ifadeler, tek deyim blokları ve çok deyimli bloklar başlatır:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML kodlaması**
> 
> Önceki örneklerde olduğu gibi, `@` karakterini kullanarak bir sayfada içerik görüntülediğinizde, ASP.NET HTML-, çıktıyı kodluyor. Bu, ayrılmış HTML karakterlerinin (`<` ve `>` ve `&`), karakterlerin HTML etiketleri veya varlıklar olarak yorumlanıp bir Web sayfasında karakter olarak görüntülenmesini sağlayan kodlarla değiştirilir. HTML kodlaması olmadan, sunucu kodunuzun çıktısı doğru görüntülenmeyebilir ve güvenlik risklerine karşı bir sayfa sunabilir.
> 
> Amacınız etiketleri biçimlendirme olarak işleyen (örneğin, bir paragraf için `<p></p>` ya da metin vurgulamak için `<em></em>`) HTML işaretlemesinin çıktısını alıyorsa, bu makalenin ilerleyen kısımlarında yer alan [kod bloklarında metin, biçimlendirme ve kod birleştirme](#BM_CombiningTextMarkupAndCode) bölümüne bakın.
> 
> HTML kodlaması hakkında daha fazla bilgi için [ASP.NET Web sayfaları SITELERINDE HTML formlarıyla çalışma](https://go.microsoft.com/fwlink/?LinkId=202892)makalesini okuyun.

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. kod bloklarını kodla çevrele... Son kod

Bir kod bloğu bir veya daha fazla kod deyimi içerir ve `Code` ve `End Code`anahtar sözcükleriyle alınmıştır. Açma `Code` anahtar sözcüğünü `@` karakterden &#8212; hemen sonra yerleştirin, aralarında boşluk olamaz.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. bir blok içinde her bir kod ifadesini satır sonuyla sonlandırın

Visual Basic bir kod bloğunda, her bir ifade bir satır sonuyla biter. (Makalede daha sonra, uzun bir kod ifadesini, gerekirse birden çok satıra sarmanın bir yolunu görürsünüz.)

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. değerleri depolamak için değişkenleri kullanırsınız

Değerleri dizeler, sayılar ve tarihler gibi bir *değişkende*saklayabilirsiniz. `Dim` anahtar sözcüğünü kullanarak yeni bir değişken oluşturursunuz. `@`kullanarak doğrudan bir sayfada değişken değerleri ekleyebilirsiniz.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-IMG3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. sabit dize değerlerini çift tırnak işaretleri içine alın

*Dize* , metin olarak kabul edilen bir karakter dizisidir. Bir dize belirtmek için, bunu çift tırnak işareti içine alın:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

Bir dize değeri içinde çift tırnak işaretleri eklemek için iki çift tırnak işareti karakteri ekleyin. Çift tırnak karakterinin sayfa çıktısında bir kez görünmesini istiyorsanız, tırnak içine alınan dize içinde `""` olarak girin ve iki kez görünmesini istiyorsanız, tırnak içine alınan dize içinde `""""` girin.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic kod büyük/küçük harfe duyarlı değildir

Visual Basic dili, büyük/küçük harfe duyarlı değildir. Programlama anahtar sözcükleri (`Dim`, `If`ve `True`gibi) ve değişken adları (`myString`veya `subTotal`gibi) herhangi bir durumda yazılabilir.

Aşağıdaki kod satırları, küçük harfli bir ad kullanarak `lastname` değişkenine bir değer atar ve ardından değişken değerini büyük bir ad kullanarak sayfaya dönüştürür.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

Bir tarayıcıda gösterilecek Sonuç:

![vb-söz dizimi-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. kodlarınızın büyük bölümü nesnelerle çalışmayı içerir

Bir nesne, bir sayfa, metin kutusu, dosya &#8212; , görüntü, Web isteği, e-posta iletisi, müşteri kaydı (veritabanı satırı) vb. ile programlama yapamayacağınız şeyi temsil eder. Nesneler, özelliklerini &#8212; tanımlayan özellikleri içerir metin kutusu nesnesi bir `Text` özelliğine sahiptir, bir istek nesnesi bir `Url` özelliğine sahiptir, bir e-posta iletisi bir `From` özelliğine sahiptir ve bir müşteri nesnesi bir `FirstName` özelliğine sahiptir. Nesneler, gerçekleştirebilecekleri&quot; &quot;fiiller olan yöntemlere de sahiptir. Bir dosya nesnesinin `Save` yöntemi, bir görüntü nesnesinin `Rotate` yöntemi ve bir e-posta nesnesinin `Send` yöntemi sayılabilir.

Genellikle sayfadaki (metin kutuları, vb.) form alanlarının değerleri, istek ne tür bir tarayıcı, Kullanıcı kimliği, vb. gibi bilgiler sağlayan `Request` nesnesiyle çalışırsınız. Bu örnek, `Request` nesnesinin özelliklerine nasıl erişileceğinin yanı sıra sunucu üzerinde sayfanın mutlak yolunu sağlayan `Request` nesnesinin `MapPath` yönteminin nasıl çağrılacağını gösterir:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. kararları veren kodu yazabilirsiniz

Dinamik Web sayfalarının temel bir özelliği, koşullara göre ne yapılacağını belirleyebileceğinize bağlıdır. Bunu yapmanın en yaygın yolu `If` deyimidir (ve isteğe bağlı `Else` deyimidir).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

`If IsPost` ifade, `If IsPost = True`yazmanın bir Özet yoludur. `If` deyimleriyle birlikte, bu makalenin ilerleyen kısımlarında açıklanan koşulları test etme, kod blokları yineleme ve benzeri birçok yol vardır.

Sonuç tarayıcıda ( **Gönder**'e tıklandıktan sonra) gösterilir:

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET ve POST yöntemleri ve ıspost özelliği**
> 
> Web sayfaları (HTTP) için kullanılan protokol, sunucuya istek yapmak için kullanılan çok sınırlı sayıda yöntemi (&quot;fiiller&quot;) destekler. En yaygın iki tane, bir sayfayı okumak için kullanılan ve bir sayfayı göndermek için kullanılan POST ' dır. Genellikle, Kullanıcı ilk kez bir sayfa istediğinde, sayfa GET kullanılarak istenir. Kullanıcı bir formu doldurduğunda ve **Gönder**' e tıkladığında, tarayıcı sunucuya bir post isteği yapar.
> 
> Web programlamada, sayfayı nasıl işleyeceğini bilmeniz için bir sayfanın GET veya POST olarak istenmekte olduğunu bilmeniz genellikle yararlı olur. ASP.NET Web sayfalarında, bir isteğin bir GET veya POST olup olmadığını görmek için `IsPost` özelliğini kullanabilirsiniz. İstek bir GÖNDERIME ise, `IsPost` özelliği true döndürür ve bir formdaki metin kutularının değerlerini okumak gibi şeyler yapabilirsiniz. Birçok örnek, `IsPost`değerine bağlı olarak sayfayı farklı şekilde nasıl işleyeceğini gösterir.

## <a name="a-simple-code-example"></a>Basit bir kod örneği

Bu yordamda, temel programlama tekniklerini gösteren bir sayfanın nasıl oluşturulacağı gösterilmektedir. Örnekte, kullanıcıların iki sayı girmelerini sağlayan bir sayfa oluşturursunuz, sonra bunları ekler ve sonucu görüntüler.

1. Düzenleyicinizde yeni bir dosya oluşturun ve *AddNumbers. vbhtml*olarak adlandırın.
2. Sayfada bulunan herhangi bir şeyi değiştirerek aşağıdaki kodu ve işaretlemeyi sayfaya kopyalayın.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    Dikkat etmeniz gereken bazı şeyler aşağıda verilmiştir:

    - `@` karakteri sayfadaki ilk kod bloğunu başlatır ve en alta eklenen `totalMessage` değişkeninden önce gelir.
    - Sayfanın üst kısmındaki blok `Code...End Code`alınmıştır.
    - Değişkenler `total`, `num1`, `num2`ve `totalMessage` çeşitli sayıları ve bir dizeyi depolar.
    - `totalMessage` değişkenine atanan sabit dize değeri çift tırnak işaretleri içinde.
    - Visual Basic kod büyük/küçük harfe duyarlı olmadığından, sayfanın alt kısmında `totalMessage` değişkeni kullanıldığında, adının sayfanın en üstündeki değişken bildiriminin yazımla eşleşmesi gerekir. Büyük küçük harf büyük bir önemi yoktur.
    - `num1.AsInt()` + `num2.AsInt()` nesne ve yöntemlerle çalışmayı gösterir. Her bir değişkendeki `AsInt` yöntemi, bir kullanıcı tarafından girilen dizeyi eklenebilen bir tam sayıya (tamsayı) dönüştürür.
    - `<form>` etiketi bir `method="post"` özniteliği içerir. Bu, Kullanıcı **Ekle**' ye tıkladığında, SAYFANıN http post yöntemi kullanılarak sunucuya gönderileceğini belirtir. Sayfa gönderildiğinde, kod `If IsPost` doğru olarak değerlendirilir ve koşullu kod çalışır ve sayı ekleme sonucunu görüntüler.
3. Sayfayı kaydedin ve bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) İki tam sayı girin ve **Ekle** düğmesine tıklayın.

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic dil ve sözdizimi

Daha önce, bir ASP.NET Web sayfası oluşturma ve HTML biçimlendirmesine sunucu kodu ekleme hakkında temel bir örnek gördünüz. Burada, programlama dili kuralları Razor söz dizimi &#8212; kullanarak ASP.NET sunucu kodu yazmak için Visual Basic kullanmanın temellerini öğreneceksiniz.

Programlamayla karşılaşırsanız (özellikle C, C++, C#, Visual Basic veya JavaScript kullandıysanız), burada okuduğunuzdan büyük bir şey tanıdık gelecektir. Muhtemelen yalnızca WebMatrix kodunun *. vbhtml* dosyalarındaki biçimlendirmeye nasıl eklendiği hakkında bilgi almanız gerekir.

### <a id="BM_CombiningTextMarkupAndCode"></a>Kod bloklarında metin, biçimlendirme ve kod birleştirme

Sunucu kod blokları ' nda, genellikle sayfada metin ve biçimlendirmeyi çıkarmak isteyeceksiniz. Bir sunucu kod bloğu kod olmayan ve bunun yerine olarak işlenmesi gereken metin içeriyorsa, ASP.NET bu metni koddan ayırabilmelidir. Bunu yapmak için birkaç yol vardır.

- Metni `<p></p>` veya `<em></em>`gibi bir HTML blok öğesine iliştirin:

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML öğesi metin, ek HTML öğeleri ve sunucu kodu ifadelerini içerebilir. ASP.NET, açılan HTML etiketini (örneğin, `<p>`) gördüğünde, öğe ve içeriğinin her şeyi tarayıcıya olduğu gibi işler (ve sunucu kodu ifadelerini çözümler).

- `@:` işlecini veya `<text>` öğesini kullanın. `@:` düz metin veya eşleşmeyen HTML etiketleri içeren tek bir içerik satırı çıktısı verir; `<text>` öğesi çıktı için birden çok satır barındırır. Bu seçenekler, çıktının bir parçası olarak bir HTML öğesi işlemek istemediğinizde yararlıdır.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    Aşağıdaki örnek, önceki örneği yineler, ancak işlemek için metni içine almak için tek bir `<text>` etiketi kullanır.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    Aşağıdaki örnekte, `<text>` ve `</text>` etiketleri üç satırı kapsar; bunların hepsi, sunucu kodu ve eşleşen HTML etiketleriyle birlikte, bazı metin ve eşleşmeyen HTML etiketlerine (`<br />`) sahiptir. Ayrıca, `@:` işleçle her bir satırdan de tek başına bir kez daha olabilirsiniz; Her iki yöntem de geçerlidir.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > Bu bölümde &#8212; gösterildiği gibi metin yazdığınızda, bir HTML öğesi, `@:` işleci veya `<text>` öğesi &#8212; ASP.net, çıktıyı HTML olarak kodlamaz. (Daha önce belirtildiği gibi, ASP.NET, bu bölümde belirtilen özel durumlar dışında, daha önce `@`sunucu kod ifadelerinin ve sunucu kodu bloklarının çıkışını kodladır.)

### <a name="whitespace"></a>Boşlu

Deyimdeki (ve dize sabit değerinin dışında) fazladan boşluklar, bu ifadeyi etkilemez:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>Uzun deyimleri birden çok satıra ayırma

Her kod satırından sonra `_` alt çizgi karakterini (Visual Basic *devamlılık karakteri*olarak adlandırılır) kullanarak, uzun bir kod ifadesini birden çok satıra kesebilirsiniz. Bir ifadeyi sonraki satıra bölmek için satırın sonunda bir boşluk ve sonra devamlılık karakteri ekleyin. Sonraki satırda ifadeye devam edin. Daha okunaklı olması için deyimlerini gereken sayıda satıra kaydırabilirsiniz. Aşağıdaki deyimler aynıdır:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

Ancak, bir satırı dize sabit değerinin ortasında kaydıramazsınız. Aşağıdaki örnek çalışmıyor:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

Yukarıdaki kod gibi birden çok satıra kaydırılan uzun bir dizeyi birleştirmek için, bu makalede daha sonra göreceğiniz *birleştirme işlecini* (`&`) kullanmanız gerekir.

### <a name="code-comments"></a>Kod açıklamaları

Açıklamalar sizin veya diğerleri için Not bırakmayı sağlar. Razor söz dizimi yorumlara ön ek olarak `@*` ve `*@`ile biter.

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

Kod blokları içinde Razor söz dizimi açıklamalarını kullanabilir veya her satıra ait tek tırnak (`'`) olan sıradan Visual Basic açıklama karakterini kullanabilirsiniz.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>Değişkenler

Değişken, verileri depolamak için kullandığınız adlandırılmış bir nesnedir. Değişkenleri herhangi bir şekilde adlandırın, ancak ad alfabetik bir karakterle başlamalı ve boşluk ya da ayrılmış karakterler içeremez. Visual Basic ' de, daha önce gördüğünüz gibi, bir değişken adındaki harflerin büyük/küçük harf durumu büyük değildir.

### <a name="variables-and-data-types"></a>Değişkenler ve veri türleri

Değişken, değişkende ne tür verilerin depolandığını gösteren belirli bir veri türüne sahip olabilir. Dize değerlerini depolayan dize değişkenleriniz (&quot;Hello World&quot;), tam sayı değerlerini depolayan tamsayı değişkenleri (3 veya 79 gibi) ve tarih değerlerini çeşitli biçimlerde depolayan Tarih değişkenlerini (4/12/2012 veya Mart 2009 gibi) kullanabilirsiniz. Ve kullanabileceğiniz pek çok farklı veri türü vardır.

Ancak, bir değişken için bir tür belirtmeniz gerekmez. Çoğu durumda ASP.NET, değişken içindeki verilerin nasıl kullanıldığını temel alarak türü belirleyebilir. (Bazen bir tür belirtmeniz gerekir; bunun doğru olduğu örnekleri görürsünüz.)

Bir tür belirtmeden bir değişken bildirmek için `Dim` ve değişken adını (örneğin, `Dim myVar`) kullanın. Bir türü olan bir değişken bildirmek için `Dim` ve değişken adını, ardından `As` ve ardından tür adını (örneğin, `Dim myVar As String`) kullanın.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

Aşağıdaki örnek, bir Web sayfasındaki değişkenleri kullanan bazı satır içi ifadeleri gösterir.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

Bir tarayıcıda gösterilecek Sonuç:

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>Veri türlerini dönüştürme ve test etme

ASP.NET genellikle bir veri türünü otomatik olarak belirleyebilse de bazen olamaz. Bu nedenle, açık bir dönüştürme gerçekleştirerek ASP.NET Out 'a yardımcı olmanız gerekebilir. Türleri dönüştürmeniz gerekmese de, ne zaman çalıştığınız veri türlerini görmek için test etmeniz yararlı olur.

En yaygın durum, bir dizeyi tamsayı veya tarih gibi başka bir türe dönüştürmeniz gerekir. Aşağıdaki örnek, bir dizeyi bir sayıya dönüştürmeniz gereken tipik bir durumu gösterir.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

Kural olarak, Kullanıcı girişi size dizeler olarak gelir. Kullanıcıdan bir sayı girmesini isteyip istememiş olsanız bile, bir rakam girse bile, Kullanıcı girişi gönderildiğinde ve kodu kodda okuduğunuzda, veriler dize biçimindedir. Bu nedenle, dizeyi bir sayıya dönüştürmeniz gerekir. Örnekte, değerleri dönüşümlemeden aritmetik gerçekleştirmeye çalışırsanız, ASP.NET iki dize ekleyemediğinden aşağıdaki hata oluşur:

`Cannot implicitly convert type 'string' to 'int'.`

Değerleri tamsayılara dönüştürmek için `AsInt` yöntemini çağırın. Dönüştürme başarılı olursa, sayıları ekleyebilirsiniz.

Aşağıdaki tabloda, değişkenler için bazı ortak dönüştürme ve test yöntemleri listelenmektedir.

:::row:::
    :::column:::
        <strong>Yöntem</strong>
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
        Tam sayıyı temsil eden bir dizeyi (&quot;593&quot;gibi) tamsayıya dönüştürür.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>İşleçler

İşleci, bir ifadede ne tür komutun gerçekleştirileceğini ASP.NET söyleyen bir anahtar sözcüktür veya karakterdir. Visual Basic birçok işleci destekler, ancak ASP.NET Web sayfaları geliştirmeye başlamak için yalnızca birkaçını belirlemeniz yeterlidir. Aşağıdaki tabloda en yaygın operatörler özetlenmektedir.

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
        `+ - * /`
    :::column-end:::
    :::column:::
        Sayısal ifadelerde kullanılan matematik işleçleri.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        Atama ve eşitlik. Bağlama bağlı olarak, bir deyimin sağ tarafındaki değeri, sol taraftaki nesneye atar ya da değerleri eşitlik için denetler.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        Olmama. Değerler eşit değilse `True` döndürür.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        Küçüktür, büyüktür, küçüktür veya eşittir, büyüktür veya eşittir.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        Dizeleri birleştirmek için kullanılan birleştirme.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        Bir değişkenden 1 (sırasıyla) ekleyen ve çıkartacak artırma ve azaltma işleçleri.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        Ayraçlar. İfadeleri gruplandırmak, parametreleri yöntemlere geçirmek ve dizi ve koleksiyonların üyelerine erişmek için kullanılır.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        Başlatılmadı. True değerini false değerine tersine çevirir ve tam tersi de geçerlidir. Genellikle `False` test etmek için (`True`değil) kısayol yöntemi olarak kullanılır.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        Koşulları birbirine bağlamak için kullanılan mantıksal AND ve OR.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

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

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>Sanal köke başvuruluyor: ~ operator ve href yöntemi

Bir *. cshtml* veya *. vbhtml* dosyasında, `~` işlecini kullanarak sanal kök yoluna başvurabilirsiniz. Sayfaları bir sitede bir konuma taşıyabilmeniz ve içerdikleri bağlantıların diğer sayfalara bölünememesi nedeniyle bu çok yararlı olur. Web sitenizi farklı bir konuma taşımanız durumunda da yararlıdır. İşte bazı örnekler:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

Web sitesi `http://myserver/myapp`, sayfa çalışırken ASP.NET bu yolları nasıl değerlendilecektir:

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`

(Bu yolları gerçekten değişkenin değerleri olarak görmezsiniz, ancak ASP.NET, bu gibi yollar gibi davranır.)

`~` işlecini hem sunucu kodunda (yukarıdaki gibi) hem de biçimlendirme ' de şu şekilde kullanabilirsiniz:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

Biçimlendirme ' de, görüntü dosyaları, diğer Web sayfaları ve CSS dosyaları gibi kaynaklara yollar oluşturmak için `~` işlecini kullanırsınız. Sayfa çalıştığında, ASP.NET sayfayı (hem kod hem de biçimlendirme) arar ve tüm `~` başvurularını uygun yola çözümler.

## <a name="conditional-logic-and-loops"></a>Koşullu mantık ve döngüler

ASP.NET sunucu kodu, koşullara göre görevleri gerçekleştirmenize ve deyimleri belirli sayıda kez tekrardan yineleme yapan kodu, yani bir döngüsü çalıştıran kodu yazmanızı sağlar.

### <a name="testing-conditions"></a>Test koşulları

Basit bir koşulu test etmek için, belirttiğiniz bir teste göre `True` veya `False` döndüren `If...Then` ifadesini kullanın:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` anahtar sözcüğü bir blok başlatır. Gerçek test (koşul) `If` anahtar sözcüğünü izler ve true veya false değerini döndürür. `If` deyimin bitişi `Then`. Test true ise çalıştırılacak deyimler `If` ve `End If`tarafından alınmıştır. `If` deyimi, koşul yanlış ise çalıştırılacak deyimleri belirten bir `Else` bloğu içerebilir:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

`If` deyimi bir kod bloğu başlattığında, blokları dahil etmek için normal `Code...End Code` deyimlerini kullanmanız gerekmez. Yalnızca bloğa `@` ekleyebilirsiniz ve bu işlem çalışır. Bu yaklaşım, `For`, `For Each`, `Do While`, vb. dahil olmak üzere kod blokları tarafından izlenen `If` ve diğer Visual Basic programlama anahtar kelimeleriyle birlikte kullanılır.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

Bir veya daha çok `ElseIf` bloğu kullanarak birden çok koşul ekleyebilirsiniz:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

Bu örnekte, `If` bloğundaki ilk koşul doğru değilse, `ElseIf` koşulu denetlenir. Bu koşul karşılanıyorsa, `ElseIf` bloğundaki deyimler yürütülür. Koşulların hiçbiri karşılanmazsa, `Else` bloğundaki deyimler yürütülür. Herhangi bir sayıda `ElseIf` blok ekleyebilir ve sonra &quot;her şeyi&quot; koşulu olarak bir `Else` bloğuyla kapatabilirsiniz.

Çok sayıda koşulu test etmek için `Select Case` bloğunu kullanın:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

Sınanacak değer parantez içinde (örnekte, haftanın günü değişkeni). Her bir test, bir değeri listeleyen `Case` bir ifade kullanır. Bir `Case` deyimin değeri test değeriyle eşleşiyorsa, bu `Case` bloğundaki kod yürütülür.

Bir tarayıcıda görünen son iki koşullu blok sonucu:

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>Döngü kodu

Genellikle aynı deyimleri tekrar tekrar çalıştırmanız gerekir. Bu, döngüye göre yapılır. Örneğin, çoğu kez bir veri koleksiyonundaki her öğe için aynı deyimleri çalıştırırsınız. Kaç kez döngüye almak istediğinizi biliyorsanız `For` döngüsünü kullanabilirsiniz. Bu tür bir döngü, özellikle daha fazla sayım veya sayım için yararlıdır:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

Döngü, `For` anahtar sözcüğüyle başlar ve bunu üç öğe izler:

- `For` deyimden hemen sonra, bir sayaç değişkeni bildirir (`Dim`kullanmanız gerekmez) ve sonra aralığı `i = 10 to 20`gibi belirtmeniz gerekir. Bu, `i` değişkeninin 10 ' da sayımının başlayacağı ve 20 ' ye (dahil) ulaşıncaya kadar devam edecek.
- `For` ve `Next` deyimleri arasında bloğunun içeridir. Bu, her döngüyle yürütülen bir veya daha fazla kod deyimi içerebilir.
- `Next i` deyimin döngüsü sona erer. Sayacı artırır ve döngünün bir sonraki yinelemesini başlatır.

`For` ve `Next` çizgileri arasındaki kod satırı, döngünün her yinelemesi için çalışan kodu içerir. Biçimlendirme, her seferinde yeni bir paragraf (`<p>` öğesi) oluşturur ve t değerini (sayaç) görüntüleyerek çıkışa bir satır ekler. Bu sayfayı çalıştırdığınızda örnek, her satırda öğe numarasını gösteren metinle birlikte çıktıyı görüntüleyen 11 satır oluşturur.

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

Bir koleksiyon veya dizi ile çalışıyorsanız, genellikle bir `For Each` döngüsü kullanırsınız. Bir koleksiyon benzer nesneler grubudur ve `For Each` döngüsü koleksiyondaki her öğe üzerinde bir görevi gerçekleştirmenizi sağlar. Bu tür bir döngü koleksiyonlar için uygundur, çünkü `For` döngüsünün aksine sayacı artırmanız veya bir sınır ayarlamanız gerekmez. Bunun yerine, `For Each` döngü kodu yalnızca, tamamlanana kadar koleksiyon üzerinden ilerler.

Bu örnek, `Request.ServerVariables` koleksiyonundaki öğeleri döndürür (Web sunucunuz hakkında bilgi içerir). HTML madde işaretli listesinde yeni bir `<li>` öğesi oluşturarak her öğenin adını göstermek için `For Each` döngüsünü kullanır.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` anahtar kelimesinin ardından, koleksiyondaki tek bir öğeyi temsil eden bir değişken gelir (örneğin, `myItem`), ardından `In` anahtar sözcüğü ve sonra, içinde döngü uygulamak istediğiniz koleksiyon. `For Each` döngüsünün gövdesinde, daha önce bildirdiğiniz değişkeni kullanarak geçerli öğeye erişebilirsiniz.

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

Daha genel amaçlı bir döngü oluşturmak için `Do While` ifadesini kullanın:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

Bu döngü, `Do While` anahtar sözcüğüyle başlar ve sonra bir koşul gelir ve ardından yineleme, yinelenir. Döngüler genellikle sayma için kullanılan bir değişken veya nesneden artış (ekleme) veya azaltma (çıkarma). Örnekte `+=` işleci, döngü her çalıştığında bir değişkenin değerine 1 ekler. (Bir döngüdeki bir değişkeni azaltmak için, azaltma işlecini `-=`kullanırsınız.)

## <a name="objects-and-collections"></a>Nesneler ve koleksiyonlar

Bir ASP.NET Web sitesindeki neredeyse her şey, Web sayfasının kendisi de dahil olmak üzere bir nesnedir. Bu bölümde, kodunuzda sıkça çalışacağımız bazı önemli nesneler açıklanmaktadır.

### <a name="page-objects"></a>Sayfa nesneleri

ASP.NET ' deki en temel nesne, sayfasıdır. Sayfa nesnesinin özelliklerine, uygun herhangi bir nesne olmadan doğrudan erişebilirsiniz. Aşağıdaki kod, sayfanın `Request` nesnesini kullanarak sayfanın dosya yolunu alır:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

`Page` nesnenin özelliklerini kullanarak çok fazla bilgi alabilirsiniz:

- `Request`. Zaten gördüğünüze göre, bu, istek ne tür bir tarayıcı, sayfanın URL 'SI, Kullanıcı kimliği vb. gibi geçerli istek hakkındaki bilgilerin bir koleksiyonudur.
- `Response`. Bu, sunucu kodunun çalışmayı tamamladığında tarayıcıya gönderilecek yanıt (sayfa) hakkındaki bilgilerin bir koleksiyonudur. Örneğin, yanıta bilgi yazmak için bu özelliği kullanabilirsiniz.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>Koleksiyon nesneleri (diziler ve sözlükler)

Bir koleksiyon, bir veritabanından `Customer` nesneleri koleksiyonu gibi aynı türde bir nesne grubudur. ASP.NET, `Request.Files` koleksiyonu gibi birçok yerleşik koleksiyon içerir.

Genellikle koleksiyonlardaki verilerle çalışırsınız. İki ortak koleksiyon türü *dizi* ve *sözlüktür*. Bir dizi benzer öğeler koleksiyonunu depolamak istediğinizde ancak her bir öğeyi tutacak ayrı bir değişken oluşturmak istemediğinizde yararlıdır:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

Diziler ile, `String`, `Integer`veya `DateTime`gibi belirli bir veri türünü bildirirsiniz. Değişkenin bir dizi içerebileceğini belirtmek için, bildirimdeki değişken adına parantez eklersiniz (örneğin, `Dim myVar() As String`). Bir dizideki öğelere konumlarını (Dizin) veya `For Each` ifadesini kullanarak erişebilirsiniz. Dizi dizinleri sıfır tabanlıdır &#8212; , ilk öğe 0 ' dır, ikinci öğe ise 1 konumunda ve bu şekilde devam eder.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

Bir dizideki öğelerin sayısını `Length` özelliğini alarak belirleyebilirsiniz. Dizideki belirli bir öğenin konumunu almak için (yani, diziyi aramak için) `Array.IndexOf` yöntemini kullanın. Ayrıca, bir dizinin içeriğini ters çevirme (`Array.Reverse` yöntemi) veya içeriği sıralama (`Array.Sort` yöntemi) gibi işlemleri de yapabilirsiniz.

Bir tarayıcıda görünen dize dizisi kodunun çıkışı:

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

Sözlük, anahtar/değer çiftleri koleksiyonudur ve buna karşılık gelen değeri ayarlamak ya da almak için anahtarı (veya adı) sağlarsınız:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

Sözlük oluşturmak için `New` anahtar sözcüğünü kullanarak yeni bir `Dictionary` nesnesi oluşturduğunuz anlamına gelir. `Dim` anahtar sözcüğünü kullanarak bir değişkene bir sözlük atayabilirsiniz. Parantez (`( )`) kullanarak Sözlükteki öğelerin veri türlerini gösterebilirsiniz. Bildirimin sonunda, bu gerçekte yeni bir sözlük oluşturan bir yöntem olduğundan, başka bir parantez çifti eklemelisiniz.

Sözlüğe öğe eklemek için, sözlük değişkeninin (Bu durumda`myScores`) `Add` yöntemini çağırabilir ve sonra bir anahtar ve bir değer belirtebilirsiniz. Alternatif olarak, aşağıdaki örnekte olduğu gibi anahtarı göstermek ve basit bir atama yapmak için parantezleri kullanabilirsiniz:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

Sözlükten bir değer almak için anahtarı parantez içinde belirtirsiniz:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>Yöntemler parametrelerle çağırma

Bu makalede daha önce gördüğünüz gibi, ile programlayabilmeniz gereken nesneler yöntemlerine sahiptir. Örneğin, bir `Database` nesnesi bir `Database.Connect` yöntemine sahip olabilir. Birçok yöntemde de bir veya daha fazla parametre vardır. *Parametresi* , bir yöntemine geçirdiğiniz bir değerdir ve bu yöntem, görevini tamamlamaya yönelik yöntemi etkinleştirir. Örneğin, üç parametre alan `Request.MapPath` yöntemi için bir bildirime bakın:

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

Bu yöntem, belirtilen sanal yola karşılık gelen sunucudaki fiziksel yolu döndürür. Yöntemi için üç parametre `virtualPath`, `baseVirtualDir`ve `allowCrossAppMapping`. (Bildiriminde, parametrelerin kabul edeceği verilerin veri türleriyle listelendiğine dikkat edin.) Bu yöntemi çağırdığınızda, üç parametrenin de değerlerini sağlamanız gerekir.

Razor söz dizimi Visual Basic kullanırken, parametreleri bir yönteme geçirmek için iki seçeneğiniz vardır: *Konumsal parametreler* veya *adlandırılmış parametreler*. Konumsal parametreleri kullanarak bir yöntemi çağırmak için, parametreleri yöntem bildiriminde belirtilen katı bir sıraya geçirin. (Bu sırayı genellikle yöntemi için belgeleri okuyarak bilirsiniz.) Sırayı izlemeniz gerekir ve gerekirse parametrelerden &#8212; hiçbirini atlayamazsınız, bir değeri olmayan Konumsal parametre için boş bir dize (`""`) veya null geçirin.

Aşağıdaki örnek, Web sitenizde *betikler* adında bir klasörünüz olduğunu varsayar. Kod `Request.MapPath` yöntemini çağırır ve üç parametrenin değerlerini doğru sırada geçirir. Ardından, sonuçta elde edilen eşleştirilmiş yolu görüntüler.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

Bir yöntem için çok sayıda parametre olduğunda, adlandırılmış parametreleri kullanarak kodunuzu temizleyicinizi ve daha okunaklı tutabilirsiniz. Adlandırılmış parametreleri kullanarak bir yöntemi çağırmak için, parametre adını ve ardından `:=` belirtip değeri sağlayın. Adlandırılmış parametrelerin avantajı, bunları istediğiniz sırada ekleyebilmeniz. (Bir dezavantajı yöntem çağrısının sıkışık olmaması.)

Aşağıdaki örnek, yukarıdaki gibi aynı yöntemi çağırır, ancak değerleri sağlamak için adlandırılmış parametreleri kullanır:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

Görebileceğiniz gibi, parametreler farklı bir sırayla geçirilir. Ancak, önceki örneği çalıştırırsanız ve bu örnekte, aynı değer döndürülür.

## <a name="handling-errors"></a>Hataları İşleme

### <a name="try-catch-statements"></a>Try-catch deyimleri

Kodunuzda, denetiminizin dışındaki nedenlerle başarısız olabilecek deyimler vardır. Örneğin:

- Kodunuz bir dosyayı açmaya, oluşturmaya, okumaya veya yazmaya çalışırsa, tüm hata sıralamaları meydana gelebilir. İstediğiniz dosya mevcut olmayabilir, kilitli olabilir, kod izinlere sahip olmayabilir ve bu şekilde devam eder.
- Benzer şekilde, kodunuz bir veritabanındaki kayıtları güncelleştirmeye çalışırsa, izin sorunları olabilir, veritabanı bağlantısı bırakılmış olabilir, kaydedilecek veriler geçersiz olabilir ve bu şekilde devam eder.

Programlama koşullarında, bu durumlara *özel durumlar*denir. Kodunuz bir özel durumla karşılaşırsa, en iyi ve rahatsız edici kullanıcılara bir hata mesajı üretir (atar).

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

Kodunuzun özel durumlarla karşılaşmasına ve bu türden hata iletilerinden kaçınmak için `Try/Catch` deyimlerini kullanabilirsiniz. `Try` bildiriminde, kontrol ettiğiniz kodu çalıştırırsınız. Bir veya daha fazla `Catch` deyiminde, oluşmuş olabilecek belirli hatalara (özel durum türleri) bakabilirsiniz. Benimsemeyi bekleme olduğunuz hatalara bakmak için gereken sayıda `Catch` deyimi ekleyebilirsiniz.

> [!NOTE]
> `Try/Catch` deyimlerde `Response.Redirect` yöntemini kullanmaktan kaçınmanızı öneririz, çünkü sayfanızda bir özel duruma neden olabilir.

Aşağıdaki örnek, ilk istekte bir metin dosyası oluşturan ve sonra kullanıcının dosyayı açmasına olanak tanıyan bir düğme görüntüleyen bir sayfa gösterir. Örnek, bir özel duruma neden olacak şekilde hatalı bir dosya adı kullanır. Kod, olası iki özel durum için `Catch` deyimlerini içerir: dosya adı bozuksa oluşan `FileNotFoundException`ve ASP.NET bile klasörü bulamazsa oluşan `DirectoryNotFoundException`. (Her şey düzgün şekilde çalıştığında nasıl çalıştığını görmek için örnekteki bir deyimin açıklamasını değiştirebilirsiniz.)

Kodunuz özel durumu işlemediyse, önceki ekran görüntüsündeki gibi bir hata sayfası görürsünüz. Ancak, `Try/Catch` bölümü kullanıcının bu hata türlerini görmesini önlemeye yardımcı olur.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

### <a name="reference-documentation"></a>Başvuru Belgeleri

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic dili](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
