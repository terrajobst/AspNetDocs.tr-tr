---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET Web sayfalarına giriş-Programlama Temelleri | Microsoft Docs
author: Rick-Anderson
description: "Bu öğreticide, ASP.NET Web sayfalarındaki programın Razor söz dizimi ile nasıl kullanılacağına ilişkin bir genel bakış sunulmaktadır. Öğrenirsiniz: çekme isteği için kullandığınız temel ' Razor ' söz dizimi..."
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 474de7671ac2931e5ba9ff635d77385403644521
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628480"
---
# <a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET Web sayfalarına giriş-Programlama Temelleri

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, ASP.NET Web sayfalarındaki programın Razor söz dizimi ile nasıl kullanılacağına ilişkin bir genel bakış sunulmaktadır.
> 
> Öğrenecekleriniz:
> 
> - ASP.NET Web sayfalarında programlama için kullandığınız temel "Razor" söz dizimi.
> - Kullanacağınız programlama C#dili olan bazı temel.
> - Web sayfaları için bazı temel programlama kavramları.
> - Sitenizde kullanmak için paketleri (önceden oluşturulmuş kod içeren bileşenler) yüklemek.
> - Ortak programlama görevlerini gerçekleştirmek için *yardımcıları* kullanma.
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - NuGet ve Paket Yöneticisi.
> - `Gravatar` Yardımcısı.

Bu öğretici, birincil olarak ASP.NET Web sayfaları için kullanacağınız programlama söz dizimini size tanıtan bir uygulamadır. *Razor söz dizimi* ve C# programlama dilinde yazılmış kod hakkında bilgi edineceksiniz. Önceki öğreticide bu söz dizimi hakkında bir göz aldınız; Bu öğreticide söz dizimini daha fazla açıklayacağız.

Bu öğreticinin, tek bir öğreticide göreceğiniz ve *yalnızca* programlama ile ilgili tek öğreticinin bulunduğu birçok programı gerektirdiğini taahhüt ediyoruz. Bu küme içindeki diğer öğreticilerde aslında ilginç şeyler yapan sayfalar oluşturacaksınız.

Ayrıca, *yardımcılar*hakkında bilgi edineceksiniz. Yardımcı, bir sayfaya ekleyebileceğiniz, paketlenmiş bir kod parçası olan bir bileşendir. Yardımcı, sizin tarafınızdan sizin için sıkıcı veya karmaşık olabilecek bir şekilde iş gerçekleştirir.

## <a name="creating-a-page-to-play-with-razor"></a>Razor ile oynatmak için bir sayfa oluşturma

Bu bölümde, temel söz dizimi hakkında fikir sahibi olmak için Razor ile bir bit oynayacağız.

Zaten çalışmıyorsa WebMatrix 'i başlatın. Önceki öğreticide oluşturduğunuz Web sitesini ([Web sayfalarına Başlarken](https://go.microsoft.com/fwlink/?LinkId=251578)) kullanacaksınız. Yeniden açmak için **Sitelerim** ' e tıklayın ve **webpagefilmler**' i seçin:

![WebMatrix başlangıç ekranı açık site seçeneklerini ve Sitelerim vurgulanmış](intro-to-web-pages-programming/_static/image1.png)

**Dosyalar** çalışma alanını seçin.

Şeritte **Yeni** ' ye tıklayarak bir sayfa oluşturun. **Cshtml** 'yi seçin ve yeni *testrazor. cshtml*sayfasını adlandırın.

**Tamam**’a tıklayın.

Aşağıdakileri dosyaya kopyalamak için, zaten mevcut olanları tamamen değiştirin.

> [!NOTE]
> Örneklerden bir sayfaya kod veya biçimlendirme kopyaladığınızda, girintileme ve hizalama öğreticiyle aynı olmayabilir. Girintileme ve hizalama kodun nasıl çalıştığını etkilemez, ancak.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>Örnek sayfayı İnceleme

Gördiklerinizi çoğu sıradan HTML 'dir. Ancak, en üstte bu kod bloğu vardır:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

Bu kod bloğu hakkında aşağıdaki noktalara dikkat edin:

- @ Karakteri, ASP.NET 'in, nasıl HTML değil Razor kodu olduğunu söyler. ASP.NET, @ karakterinden sonraki her şeyi, bazı HTML yeniden çalıştırana kadar kod olarak değerlendirir. (Bu durumda &lt;! DOCTYPE&gt; öğesi.
- Kod ayraçları ({ve}), kodun birden fazla satırı varsa Razor kodu bloğunu kapsar. Küme ayraçları, bu bloğun kodunun başladığı ve bittiği ASP.NET bildirir.
- //Karakterleri bir açıklamayı (yani, yürütümeyecek kodun bir parçasını) işaretler.
- Her deyimin sonunda noktalı virgül (;) vardır. (Ancak açıklama değil)
- Değerlerini, var olan (*Declare*) anahtar sözcüğü ile oluşturduğunuz *değişkenlerde*saklayabilirsiniz. Bir değişken oluşturduğunuzda, bu ada harfler, rakamlar ve alt çizgi (\_) içerebilen bir ad verirsiniz. Değişken adları bir sayıyla başlayamaz ve bir programlama anahtar sözcüğünün adını (var gibi) kullanamaz.
- Karakter dizelerini ("ASP.NET" ve "Web Pages" gibi) tırnak işaretleri içine alın. (Çift tırnak işareti olmalıdır.) Sayılar tırnak işaretleri içinde değil.
- Tırnak işaretlerinin dışındaki boşluklar önemli değildir. Satır sonları çoğunlukla büyük değildir; özel durum, bir dizeyi satırlarda tırnak işaretleriyle bölemiyorum. Girintileme ve hizalama önemi yoktur.

Bu örnekte belirgin olmayan bir şey, tüm kodun büyük/küçük harfe duyarlıdır. Bu, değişken, değişken ya da Deum adında olabilecek değişkenlerden farklı bir değişken olduğu anlamına gelir. Benzer şekilde, var bir anahtar sözcüktür, ancak var değildir.

### <a name="objects-and-properties-and-methods"></a>Nesneler ve Özellikler ve Yöntemler

Ardından DateTime. Now ifadesi. Basit koşullarda, DateTime bir *nesnedir*. Bir nesne, bir sayfa, metin kutusu, dosya, görüntü, Web isteği, e-posta iletisi, müşteri kaydı vb. ile programlama yapamayacağınız bir şeydir. Nesneler, özelliklerini tanımlayan bir veya daha fazla *özelliğe* sahiptir. Metin kutusu nesnesi bir metin özelliğine sahiptir (diğerleri arasında), bir istek nesnesinin bir URL özelliği (ve diğerleri), bir e-posta iletisinin Kimden özelliği ve bir to özelliği vardır ve bu şekilde devam eder. Nesneler, gerçekleştirebilecekleri "fiiller" olan *yöntemlere* de sahiptir. Nesnelerle çok büyük bir şekilde çalışıyorsunuz.

Örnekte görebileceğiniz gibi, TarihSaat tarih ve saat programlamanızı sağlayan bir nesnedir. Şu anda geçerli tarih ve saati döndüren adlı bir özelliği vardır.

### <a name="using-code-to-render-markup-in-the-page"></a>Sayfadaki biçimlendirmeyi işlemek için kodu kullanma

Sayfanın gövdesinde, aşağıdakilere dikkat edin:

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

Yine, @ karakteri, ASP.NET 'in HTML değil kodun ne olduğunu söyler. Biçimlendirme içinde @ arkasından bir kod ifadesi ve ASP.NET bu ifadenin değerini bu noktada işleyecek şekilde işleyebilir. Örnekte, @a değeri bir olan değişkenin ne olduğunu, @product ürün adlı değişkende olduğunu ve bu şekilde devam eder.

Ancak değişkenlerle sınırlı değilsiniz. Burada birkaç örnekte @ karakteri bir ifadeden önce gelir:

- @ (a\*b), a ve b değişkenlerinde her türlü ürünü işler. (\* işleci çarpma anlamına gelir.)
- @ (teknoloji + "" + ürün), değişken teknolojideki ve üründeki değerleri, bunları birleştirerek ve arasına boşluk ekleyerek işler. Dizeleri bitiştirme işleci (+), sayı eklemek için olan işleçle aynıdır. ASP.NET, genellikle sayılarla veya dizeler ile çalışıp çalışmadığını ve + işleciyle doğru şeyi yapıp yapamadığını söyleyebilir.
- @Request.Url, Istek nesnesinin URL özelliğini işler. Istek nesnesi, tarayıcıdan gelen geçerli istek hakkında bilgiler içerir ve kuşkusuz URL özelliği o anki isteğin URL 'sini içerir.

Örnek ayrıca, farklı yollarla iş yapabileceğinizi göstermek için de tasarlanmıştır. Üstteki kod bloğunda hesaplamalar yapabilir, sonuçları bir değişkene yerleştirebilir ve sonra değişkeni biçimlendirme içinde işleyebilirsiniz. Alternatif olarak, İşaretlemede bir ifadede hesaplamalar yapabilirsiniz. Kullandığınız yaklaşım, yaptığınız işe ve bir ölçüde kendi tercihlerinize göre değişir.

### <a name="seeing-the-code-in-action"></a>Kodu eylemde görüntüleme

Dosyanın adına sağ tıklayın ve ardından **tarayıcıda Başlat**' ı seçin. Sayfada, sayfada çözümlenen tüm değerler ve ifadeler ile tarayıcıda görüntülenir.

![' TestRazor ' sayfası tarayıcıda çalışıyor](intro-to-web-pages-programming/_static/image2.png)

Tarayıcıdaki kaynağa bakın.

![Tarayıcıdaki ' test Razor ' sayfası kaynağı](intro-to-web-pages-programming/_static/image3.png)

Önceki öğreticide deneyiminizden beklemediğiniz gibi, Razor kodundan hiçbiri sayfada değildir. Tüm gördüğünüz gerçek görüntü değerleridir. Bir sayfa çalıştırdığınızda, aslında WebMatrix 'te yerleşik olarak bulunan Web sunucusuna bir istek oluşturursunuz. İstek alındığında, ASP.NET tüm değerleri ve ifadeleri çözer ve değerlerini sayfada oluşturur. Daha sonra sayfayı tarayıcıya gönderir.

> [!TIP] 
> 
> **Razor veC#**
> 
> Şimdi Razor söz dizimi çalıştığınızı söyledik. Bu doğru, ancak tamamen hikaye değildir. Kullanmakta olduğunuz gerçek programlama dili çağırılır *C#* . C#, Microsoft tarafından bir yılda bir süre önce oluşturulmuştur ve Windows uygulamaları oluşturmaya yönelik birincil programlama dillerinden biri haline geldi. Bir değişkeni adlandırma ve deyimleri oluşturma hakkında gördüğünüz tüm kurallar gerçekte C# dilin tüm kurallarıdır.
> 
> Razor, bu kodu sayfaya nasıl katıştırabileceğinizi gösteren küçük bir kural kümesine daha fazla başvurur. Örneğin, sayfadaki kodu işaretlemek için @ kullanma ve bir kod bloğunu eklemek için @ {} kullanma kuralı sayfanın Razor yönüdür. Yardımcılar da Razor 'nin bir parçası olarak kabul edilir. Razor söz dizimi, tıpkı ASP.NET Web sayfalarından daha fazla yerde kullanılır. (Örneğin, ASP.NET MVC görünümlerinde de kullanılır.)
> 
> Bunun yerine, ASP.NET Web sayfalarını programlama hakkında bilgi aradığınız için Razor 'ye çok sayıda başvuru bulacaksınız. Ancak, bu başvuruların çoğu yaptığınız şey için uygulanmaz ve bu nedenle kafa karıştırıcı olabilir. Aslında, programlama sorularınızın birçoğu, ASP.NET ile çalışmaya C# veya bunlarla çalışmaya yönelik olarak olacaktır. Bu nedenle, Razor hakkında daha fazla bilgi için gereken yanıtları bulamadıysanız.

## <a name="adding-some-conditional-logic"></a>Koşullu mantık ekleme

Bir sayfada kod kullanmayla ilgili harika özelliklerden biri, çeşitli koşullara göre ne olacağını değiştirebilmesidir. Öğreticinin bu bölümünde, sayfada görüntülendiklerinizi değiştirmek için bazı yollarla gezinirsiniz.

Örnek, koşullu mantığa odaklanabilmeniz için basit ve biraz contrived olacaktır. Oluşturacağınız sayfa şu şekilde yapılır:

- Sayfada, sayfanın ilk kez görüntülenmediğine veya sayfayı göndermek için bir düğmeye tıklandığınıza bağlı olarak farklı bir metin gösterin. Bu, ilk koşullu test olacaktır.
- İletiyi yalnızca URL 'nin sorgu dizesinde belirli bir değer geçirildiğinde görüntüleyin (http://...? Show = true). Bu, ikinci koşullu test olacaktır.

WebMatrix 'te bir sayfa oluşturun ve *TestRazorPart2. cshtml*olarak adlandırın. (Şeritte **Yeni**' ye tıklayın, **cshtml**'yi seçin, dosyayı adlandırın ve ardından **Tamam**' a tıklayın.)

Bu sayfanın içeriğini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

Üstteki kod bloğu, ileti adlı bir değişkeni bir metin ile başlatır. Sayfanın gövdesinde, ileti değişkeninin içeriği &lt;p&gt; öğesinin içinde görüntülenir. Biçimlendirme Ayrıca bir **Gönder** düğmesi oluşturmak için bir &lt;Input&gt; öğesi içerir.

Nasıl çalıştığını görmek için sayfayı çalıştırın. Şimdilik, **Gönder** düğmesine tıklasanız bile, bu, temelde statik bir sayfasıdır.

WebMatrix 'e geri dönün. Kod bloğunun içinde, iletiyi Başlatan satırdan *sonra* aşağıdaki vurgulanmış kodu ekleyin:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} bloğu

Yeni eklediğiniz bir If koşulunuz. Kodda, If koşulu şöyle bir yapıya sahiptir:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

Sınanacak koşul parantez içinde. True veya false döndüren bir değer veya ifade olmalıdır. Koşul doğru ise, ASP.NET, küme ayraçları içinde olan deyimi veya deyimleri çalıştırır. (Bunlar *daha sonra* *if-then* mantığının parçasıdır.) Koşul yanlış ise, kod bloğu atlanır.

Aşağıda, bir if ifadesinde test verebilmeniz için birkaç koşul örneği verilmiştir:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

Bir *mantıksal işleç* veya *karşılaştırma işleci*kullanarak değişkenleri değerlere veya ifadelerde test edebilirsiniz: eşittir (= =), büyüktür (&gt;), küçüktür (&lt;), büyüktür veya eşittir (&gt;=) ve küçüktür veya eşittir (&lt;=). ! = İşleci şuna eşit değildir — Örneğin, (bir! = 0), *a 'nın 0 değerine eşit olmaması*anlamına gelir.

> [!NOTE]
> Eşittir (= =) karşılaştırma işlecinin = ile aynı olmadığını fark ettiğinizden emin olun. = İşleci yalnızca değer atamak için kullanılır (var a = 2). Bu işleçleri karıştırırsanız bir hata alırsınız veya bazı garip sonuçlar elde edersiniz.

Bir şeyin doğru olup olmadığını test etmek için, tüm sözdizimi (Isdone = = true) olur. Ancak (Isdone) kısayolunu da kullanabilirsiniz. Karşılaştırma operatörü yoksa, ASP.NET doğru test olduğunuzu varsayar.

İçin! tek başına işleci mantıksal DEĞILDIR anlamına gelir. Örneğin, (! Ispost), *ıspost doğru değilse*anlamına gelir.

Bir mantıksal ve (&amp;&amp; işleci) veya mantıksal veya (| | işleç) kullanarak koşulları birleştirebilirsiniz. Örneğin, Yukarıdaki örneklerde en son koşullar, *Fileprocessingısdone değeri true olarak AYARLANMAMıŞSA ve displayMessage false olarak ayarlandığında*anlamına gelir.

### <a name="the-else-block"></a>Else bloğu

If bloklarıyla ilgili son bir şey: If bloğu, Else bloğu tarafından izlenebilir. Else bloğu, koşul yanlış olduğunda farklı kod yürütmeniz gerekir. İşte basit bir örnek:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

Bu serinin sonraki öğreticilerde, Else bloğunun kullanılması yararlı olan bazı örnekler görürsünüz.

### <a name="testing-whether-the-request-is-a-submit-post"></a>İsteğin bir gönderme (gönderi) olup olmadığını test etme

Daha fazla, ancak (ıspost) {...} koşulunu içeren örneğe geri bakalım. Ispost aslında geçerli sayfanın bir özelliğidir. Sayfa istendiğinde, ıspost yanlış döndürür. Ancak, bir düğmeye tıkladığınızda veya sayfayı gönderirseniz — Yani, gönderirseniz, ıspost doğru döndürür. Bu nedenle, ıspost, form gönderme işlemiyle ilgili olup olmadığınızı belirlemenizi sağlar. (HTTP fiilleri açısından, istek bir GET işlemi ise, ıspost yanlış değerini döndürür. İstek bir POST işlemi ise, ıspost doğru döndürür.) Daha sonraki bir öğreticide, bu testin özellikle yararlı olacağı giriş formlarıyla çalışırsınız.

Sayfayı çalıştırın. Sayfayı ilk kez istemiş olduğunuzdan, "sayfayı ilk kez istemiş olursunuz" görürsünüz. Bu dize, ileti değişkenini seçtiğiniz değerdir. Bir if (ıspost) testi vardır ancak bu, şu anda false değerini döndürürse, IF bloğunun içindeki kod çalıştırılmaz.

**Gönder** düğmesine tıklayın. Sayfa yeniden istendi. Daha önce olduğu gibi, ileti değişkeni "Bu ilk kez..." olarak ayarlanır. Ancak, bu kez (ıspost) testi true değerini döndürürse, IF bloğu içindeki kod çalışır. Kod, ileti değişkeninin değerini, biçimlendirmede işlenen farklı bir değer olarak değiştirir.

Şimdi, İşaretlemede bir If koşulu ekleyin. **Gönder** düğmesini içeren &lt;p&gt; öğesinin altında aşağıdaki biçimlendirmeyi ekleyin:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

Biçimlendirme içine kod ekleyecekseniz @başlatmanız gerekir. Daha sonra kod bloğunda daha önce eklendiğine benzer bir if testi vardır. Küme ayraçları içinde, normal HTML ekliyorsanız, en azından, @DateTime.Nowgelene kadar sıradan olur. Bu, başka bir Razor kodu biraz daha olduğundan, bu nedenle yine de önüne @ eklemeniz gerekir.

Buradaki nokta, hem kod bloğunda hem de İşaretlemede koşul ekleyebilmeniz için kullanılır. Sayfanın gövdesinde bir If koşulu kullanırsanız, bloktaki satırlar biçimlendirme veya kod olabilir. Bu durumda, her zaman biçimlendirmeyi ve kodu karıştırabilmeniz için @ kullanmanız gerekir ve kodun nerede olduğu ASP.NET açık olması için @ kullanmalısınız.

Sayfayı çalıştırın ve **Gönder**' e tıklayın. Bu kez gönderdiğinizde ("Şimdi gönderdiniz...") farklı bir ileti görmezsiniz, ancak tarih ve saati listeleyen yeni bir ileti görürsünüz.

![' Test RAZOR 2 ' sayfası, gönderdikten sonra zaman damgasıyla tarayıcıda çalışıyor](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>Sorgu dizesinin değerini test etme

Bir test daha. Bu kez, sorgu dizesine geçirilebilen Show adlı bir değeri sınayan bir If bloğu ekleyeceksiniz. (Şu şekilde: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) Sayfayı, görüntülemekte olduğunuz iletinin ("ilk kez...", vb.) yalnızca show değeri true ise görüntülenecek şekilde değiştirirsiniz.

Sayfanın üst kısmındaki kod bloğunu en altta (ancak içinde) aşağıdakileri ekleyin:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

Tüm kod bloğu şimdi aşağıdaki örneğe benzer şekilde görünür. (Kodu sayfanıza kopyaladığınızda, girintileme farklı görünebileceğini unutmayın. Ancak bu, kodun nasıl çalıştığını etkilemez.)

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

Bloktaki yeni kod, showMessage adlı bir değişkeni false olarak başlatır. Sonra sorgu dizesinde bir değer aramak için bir if testi yapar. Sayfayı ilk kez istediğinizde, şöyle bir URL bulunur:

`http://localhost:43097/TestRazorPart2.cshtml`

Kod, URL 'nin bu sürümü gibi sorgu dizesinde göster adlı bir değişken içerip içermediğini belirler:

`http://localhost:43097/TestRazorPart2.cshtml`? Show = true

Test kendisi Istek nesnesinin QueryString özelliğine bakar. Sorgu dizesi Show adlı bir öğe içeriyorsa ve bu öğe true olarak ayarlanırsa, IF bloğu çalışır ve showMessage değişkenini true olarak ayarlar.

Burada gördüğünüz gibi bir elde bulabilirsiniz. Şöyle ki, sorgu dizesi bir dizedir. Ancak, test ettiğiniz değer bir Boole (true/false) değeri ise yalnızca true ve false için test edebilirsiniz. Sorgu dizesinde Show değişkeninin değerini test etmeden önce, onu bir Boole değerine dönüştürmeniz gerekir. Bu, AsBool yönteminin yaptığı şeydir; girdi olarak bir dize alır ve bir Boolean değere dönüştürür. Açık olarak, dize "true" ise AsBool yöntemi bu değeri true olarak dönüştürür. Dizenin değeri başka bir şeydir, AsBool yanlış döndürür.

> [!TIP] 
> 
> **Veri türleri ve as () yöntemleri**
> 
> Yalnızca bir değişken oluşturduğunuzda, var olan anahtar sözcüğünü kullanırsınız. Bu, ancak tüm hikayenin değil. Değerleri değiştirmek için — sayı eklemek veya dizeleri birleştirmek ya da tarihleri karşılaştırmak ya da doğru/yanlış C# için test olması için, değerin uygun bir iç gösterimi ile çalışması gerekir. C#*genellikle* bu temsilin ne olması gerektiğini (yani, verilerin ne *tür* olduğunu) değerler ile yaptığınız verilere göre anlayabilir. Artık, ancak bunu yapamazlar. Aksi takdirde, verileri nasıl C# temsil ettiğini açıkça belirten bir yardım almanız gerekir. AsBool metodu, "true" veya " C# false" dize değerinin Boole değeri olarak değerlendirilip değerlendirilmeyeceğini söyler. Benzer yöntemler, dizeleri diğer türler (tamsayı olarak değerlendir), AsDateTime (bir tarih/saat olarak işle), AsFloat (kayan noktalı sayı olarak işle) gibi diğer türler olarak temsil etmek için de mevcuttur. Bu as () yöntemlerini kullandığınızda, dize değerini istenen C# şekilde temsil ediyorsanız bir hata görürsünüz.

Sayfanın biçimlendirmesinde, bu öğeyi kaldırın veya açıklamayı kaldırın (burada açıklama gösterilir):

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

Bu metni kaldırdığınız veya daha fazla açıklama eklemek için aşağıdakileri ekleyin:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

Eğer test, showMessage değişkeni true ise, ileti değişkeninin değeri ile bir &lt;p&gt; öğesi işleneceğini belirtir.

### <a name="summary-of-your-conditional-logic"></a>Koşullu mantığınızın Özeti

Az önce yaptığınız şekilde tamamen emin değilseniz, bir özet aşağıda verilmiştir.

- İleti değişkeni varsayılan bir dizeye ("Bu ilk kez...") başlatılır.
- Sayfa isteği bir gönderme (gönderi) sonucunda, ileti değeri "Şimdi gönderdiniz..." olarak değiştirilir.
- ShowMessage değişkeni false olarak başlatılır.
- Sorgu dizesi? Show = true ise showMessage değişkeni true olarak ayarlanır.
- İşaretlemede, showMessage true ise, iletinin değerini gösteren bir &lt;p&gt; öğesi işlenir. (ShowMessage false ise, İşaretlemede o noktada hiçbir şey işlenmez.)
- İşaretlemede, istek bir gönderimdiyse, tarihi ve saati gösteren bir &lt;p&gt; öğesi işlenir.

Sayfayı çalıştırın. Bir ileti yoktur, çünkü showMessage false olduğundan, biçimlendirme (showMessage) testi false değerini döndürür.

**Gönder**'e tıklayın. Tarih ve saati görürsünüz ancak yine de ileti görmezsiniz.

Tarayıcınızda URL kutusuna gidin ve şu URL 'nin sonuna şunu ekleyin:? show = true, sonra ENTER tuşuna basın.

![Sorgu dizesini gösteren tarayıcıda ' test RAZOR 2 ' sayfası](intro-to-web-pages-programming/_static/image5.png)

Sayfa yeniden görüntülenir. (URL 'YI değiştirdiğiniz için, bu yeni bir istek, gönderme değil.) Yeniden **Gönder** ' e tıklayın. İleti, tarih ve saat olduğu gibi yeniden görüntülenir.

![Sorgu dizesi olduğunda gönderdikten sonra ' test RAZOR 2 ' sayfası](intro-to-web-pages-programming/_static/image6.png)

URL 'de, Değiştir? = true ile? göster = false ve ENTER 'a basın. Sayfayı yeniden gönder. Sayfa, ileti olmadan nasıl başlatıladığına geri gönderilir.

Daha önce belirtildiği gibi, bu örneğin mantığı biraz contrived. Ancak, sayfalarınızın birçoğu varsa, burada gördüğünüz formlardan birini veya daha fazlasını alır.

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>Yardımcı yükleme (Gravatar görüntüsünü görüntüleme)

Kullanıcıların genellikle Web sayfalarında yapmak istedikleri bazı görevler çok fazla kod gerektirir veya ek bilgi gerektirir. Örnekler: veriler için bir grafik görüntüleme; Facebook "Beğen" düğmesini sayfaya yerleştirme; Web siteinizden e-posta gönderme; görüntüleri kırpma veya yeniden boyutlandırma; siteniz için PayPal 'yi kullanma. Bu tür şeyleri daha kolay hale getirmek için ASP.NET Web sayfaları, *yardımcıları*kullanmanıza olanak sağlar. Yardımcılar, bir site için yüklediğiniz ve yalnızca birkaç Razor kodu satırını kullanarak tipik görevleri gerçekleştirmenize olanak sağlayan bileşenlerdir.

ASP.NET Web sayfalarının içinde yerleşik olarak bulunan birkaç yardımcıları vardır. Ancak, NuGet Paket Yöneticisi kullanılarak sağlanan paketlerde (eklentiler) birçok yardımcı vardır. NuGet, yüklenecek bir paket seçmenizi sağlar ve yükleme ayrıntılarının tamamını ele alır.

Öğreticinin bu bölümünde, Gravatar ("küresel olarak tanınan Avatar") görüntüsünü görüntülemenize olanak tanıyan bir yardımcı yüklersiniz. İki şey öğreneceksiniz. Bunlardan biri, bir yardımcıyı bulma ve yüklemeyi sağlar. Ayrıca, kendiniz yazmanız gereken çok sayıda kod kullanarak yapmanız gereken bir şeyin nasıl yapılacağını nasıl kolaylaştırdığını öğreneceksiniz.

Kendi Gravaık Web sitesine [http://www.gravatar.com/](http://www.gravatar.com/)de kaydedebilirsiniz, ancak öğreticinin bu bölümünü gerçekleştirmek Için bir Gravatar hesabı oluşturmak gerekli değildir.

WebMatrix 'te **NuGet** düğmesine tıklayın.

![WebMatrix 'te NuGet Galerisi iletişim kutusu](intro-to-web-pages-programming/_static/image7.png)

Bu, NuGet paket yöneticisini başlatır ve kullanılabilir paketleri görüntüler. (Paketlerin hepsi yardımcılar değil; bazı WebMatrix işlevleri, bazı ek şablonlar vb.) Sürüm uyumsuzluğu hakkında bir hata iletisi alabilirsiniz. **Tamam** ' a tıklayıp Bu öğreticiye devam ederek bu hata iletisini yoksayabilirsiniz.

![WebMatrix 'te NuGet Galerisi iletişim kutusu](intro-to-web-pages-programming/_static/image8.png)

Arama kutusuna "asp.net yardımcıları" yazın. NuGet, arama terimleriyle eşleşen paketleri gösterir.

![Paketleri gösteren WebMatrix 'te NuGet Galerisi](intro-to-web-pages-programming/_static/image9.png)

ASP.NET Web yardımcıları kitaplığı, Gravatar görüntülerinin kullanımı dahil olmak üzere birçok ortak görevi basitleştirecek kodu içerir. **ASP.NET Web yardımcıları kitaplığı** paketini seçin ve ardından yükleyiciyi başlatmak için **yükleme** ' ye tıklayın. Paketi yüklemek isteyip istemediğiniz sorulduğunda **Evet** ' i seçin ve yüklemeyi tamamlamaya yönelik koşulları kabul edin.

İşte bu kadar. NuGet, gerekli olabilecek ek bileşenler de dahil olmak üzere her şeyi indirir ve yükler (*Bağımlılıklar*).

Bir yardımcıyı kaldırmanız gerekirse, işlem çok benzerdir. **NuGet** düğmesine tıklayın, **yüklü** sekmesine tıklayın ve kaldırmak istediğiniz paketi seçin.

## <a name="using-a-helper-in-a-page"></a>Sayfada yardımcı kullanma

Şimdi, yeni yüklediğiniz yardımcı ' i kullanacaksınız. Bir sayfaya yardımcı ekleme süreci çoğu Yardımcıda benzerdir.

WebMatrix 'te bir sayfa oluşturun ve *Gravatartest. cshml*olarak adlandırın. (Yardımcı 'yı test etmek için özel bir sayfa oluşturuyorsunuz, ancak sitenizdeki herhangi bir sayfada yardımcıları kullanabilirsiniz.)

&lt;Body&gt; öğesinin içinde, bir &lt;div&gt; öğesi ekleyin. &lt;div&gt; öğesinin içinde şunu yazın:

@Gravatar.

@ Karakteri, Razor kodunu işaretlemek için kullandığınız karakter ile aynıdır. **Gravatar** , üzerinde çalıştığınız yardımcı nesnedir.

Noktayı (.) yazdığınızda, WebMatrix, Gravatar Yardımcısı 'nın kullanılabilir hale getiren *yöntemlerin* (işlevlerin) bir listesini görüntüler.

![Gravatar Yardımcısı IntelliSense açılan listesi](intro-to-web-pages-programming/_static/image10.png)

Bu özellik *IntelliSense*olarak bilinir. Bağlama uygun seçimler sunarak kodmanıza yardımcı olur. IntelliSense, WebMatrix 'te desteklenen HTML, CSS, ASP.NET Code, JavaScript ve diğer diller ile birlikte kullanılabilir. WebMatrix 'te Web sayfaları geliştirmeyi kolaylaştıran başka bir özelliktir.

Klavyede G tuşuna basın ve IntelliSense 'in GetHtml metodunu bulduğunu görürsünüz. Sekme tuşuna basın. IntelliSense, sizin için seçilen yöntemi (GetHtml) ekler. Bir açık parantez yazın ve kapatma parantezinin otomatik olarak eklendiğinden emin olun. E-posta adresinizi iki parantez arasına tırnak işareti içine yazın. Bir Gravatar hesabınız varsa, profil resminiz döndürülür. Gravatar hesabınız yoksa, varsayılan bir görüntü döndürülür. İşiniz bittiğinde, satır şöyle görünür:

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

Şimdi sayfayı bir tarayıcıda görüntüleyin. Gravatar hesabınız olmasına bağlı olarak, resminiz veya varsayılan görüntü görüntülenir.

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![Varsayılan görüntü](intro-to-web-pages-programming/_static/image12.png)

Yardımcı 'nın sizin için yaptığına ilişkin bir fikir edinmek için tarayıcıda sayfanın kaynağını görüntüleyin. Sayfanızda bulunan HTML ile birlikte tanımlayıcı içeren bir görüntü öğesi görürsünüz. Bu, yardımcının @Gravatar.GetHtmlsahip olduğunuz yerde sayfada işlenen koddur. Yardımcı, sağladığınız bilgileri alır ve sağlanan hesap için doğru görüntüyü geri almak üzere doğrudan Gravaık 'ye bağlanan kodu üretti.

GetHtml yöntemi, diğer parametreleri sağlayarak görüntüyü özelleştirmenize de olanak sağlar. Aşağıdaki kod, bir görüntünün 40 piksellik genişlik ve yüksekliğe sahip olduğunu ve belirtilen hesap yoksa **Wavatar** adlı belirtilen bir varsayılan görüntü kullandığını gösterir.

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

Bu kod aşağıdaki sonuca benzer bir şey üretir (varsayılan görüntü rastgele farklılık gösterir).

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>Sonraki adımda

Bu öğreticiyi tutmak için yalnızca birkaç temel bilgilere odaklanıyoruz. Doğal olarak, Razor ve C#için çok daha fazla şey vardır. Bu öğreticilerle giderek daha fazla bilgi edineceksiniz. Razor 'in programlama yönleri ve C# Şu anda daha fazla bilgi edinmek istiyorsanız, daha kapsamlı bir giriş bulabilirsiniz: [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkID=202890).

Sonraki öğreticide bir veritabanıyla çalışmanız tanıtılmaktadır. Bu öğreticide, en sevdiğiniz filmleri listelemenizi sağlayan örnek uygulamayı oluşturmaya başlayacaksınız.

## <a name="complete-listing-for-testrazor-page"></a>TestRazor sayfası listesinin tamamını listeleme

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 sayfası için komple liste

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest sayfası için komple liste

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter Yardımcısı](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [Önceki](getting-started.md)
> [İleri](displaying-data.md)
