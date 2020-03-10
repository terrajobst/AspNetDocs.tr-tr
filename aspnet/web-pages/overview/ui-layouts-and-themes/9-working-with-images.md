---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: ASP.NET Web Pages (Razor) sitesindeki görüntülerle çalışma | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, Web sitenizde resimleri ekleme, görüntüleme ve işleme (filigranları yeniden boyutlandırma, çevirme ve ekleme) gösterilmektedir.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 53514b3c314fc182a43c82974ffcfa8158a636a1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631861"
---
# <a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web Pages (Razor) sitesindeki görüntülerle çalışma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde görüntüleri ekleme, görüntüleme ve işleme (filigranları yeniden boyutlandırma, çevirme ve ekleme) gösterilmektedir.
> 
> Öğrenecekleriniz:
> 
> - Sayfaya dinamik olarak görüntü ekleme.
> - Kullanıcıların bir görüntüyü karşıya yüklemesine izin verin.
> - Görüntüyü yeniden boyutlandırma.
> - Bir görüntüyü çevirme veya döndürme.
> - Görüntüye filigran ekleme.
> - Bir görüntüyü filigran olarak kullanma.
> 
> Makalesinde sunulan ASP.NET programlama özellikleri şunlardır:
> 
> - `WebImage` Yardımcısı.
> - Yolu ve dosya adlarını değiştirmenize olanak sağlayan yöntemler sağlayan `Path` nesnesi.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 2
>   
> 
> Bu öğretici WebMatrix 3 ile de kullanılabilir.

<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>Bir Web sayfasına dinamik olarak görüntü ekleme

Web sitenizi geliştirirken, Web sitenize ve tek tek sayfalara görüntü ekleyebilirsiniz. Ayrıca, kullanıcıların bir profil fotoğrafı eklemesine izin veren görevler için yararlı olabilecek resimleri karşıya yüklemesine izin verebilirsiniz.

Sitenizde zaten bir görüntü varsa ve yalnızca bir sayfada göstermek istiyorsanız, şöyle bir HTML `<img>` öğesi kullanın:

[!code-html[Main](9-working-with-images/samples/sample1.html)]

Bazen, görüntüleri dinamik olarak &#8212; görüntülemenin yanı, sayfa çalışmadığı sürece hangi görüntünün görüntüleneceğini bilemezsiniz.

Bu bölümdeki yordamda, kullanıcıların görüntü adı listesinden görüntü dosyası adını belirtmesi durumunda bir görüntünün nasıl görüntüleneceği gösterilmektedir. Bu kişiler, açılan listeden görüntünün adını seçer ve sayfayı gönderdiğinde, seçtiğiniz resim görüntülenir.

![görüntüyle](9-working-with-images/_static/image1.jpg "ch9images-1. jpg")

1. WebMatrix 'te yeni bir Web sitesi oluşturun.
2. *Dynamicımage. cshtml*adlı yeni bir sayfa ekleyin.
3. Web sitesinin kök klasöründe yeni bir klasör ekleyin ve *resim*olarak adlandırın.
4. Az önce oluşturduğunuz *görüntüler* klasörüne dört görüntü ekleyin. (Kullanışlı olan tüm görüntüler olur, ancak bir sayfaya sığması gerekir.) *Photo1. jpg*, *Photo2. jpg*, *Photo3. jpg*ve *Photo4. jpg*görüntülerini yeniden adlandırın. (Bu yordamda *Photo4. jpg* kullanamazsınız, ancak makalenin ilerleyen kısımlarında kullanacaksınız.)
5. Dört görüntünün salt okunurdur olarak işaretlenmediğini doğrulayın.
6. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin:

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    Sayfanın gövdesinde `photoChoice`adlı bir açılan liste (bir `<select>` öğesi) bulunur. Listede üç seçenek vardır ve her liste seçeneğinin `value` özniteliği, *görüntüler* klasörüne yerleştirdiğiniz görüntülerden birinin adını içerir. Temelde, liste kullanıcının &quot;fotoğraf 1&quot;gibi kolay bir ad seçmesini sağlar ve ardından sayfa gönderildiğinde *. jpg* dosya adını geçirir.

    Kodda, kullanıcının seçimini (diğer bir deyişle, görüntü dosyası adı) `Request["photoChoice"]`okuyarak listeden alabilirsiniz. Önce bir seçim olup olmadığını görürsünüz. Varsa, görüntü için resimlerin ve kullanıcının görüntü dosyası adının adını içeren bir yol oluşturursunuz. (Bir yol oluşturmaya çalıştıysanız, ancak `Request["photoChoice"]`hiçbir şey olmadıysa bir hata alırsınız.) Bunun gibi göreli bir yol oluşur:

    *Images/Photo1. jpg*

    Yol, sayfada daha sonra ihtiyacınız olacak `imagePath` adlı değişkende saklanır.

    Gövdede, kullanıcının çekileceği görüntüyü göstermek için kullanılan bir `<img>` öğesi de vardır. `src` özniteliği bir dosya adına veya URL 'ye ayarlı değil, bir statik öğeyi göstermek için yaptığınız gibi. Bunun yerine, `@imagePath`olarak ayarlanır, yani bu değer kodda ayarladığınız yoldan değerini alır.

    Sayfa ilk kez çalıştığında, Kullanıcı hiçbir şey seçmediği için görüntülenecek görüntü yok. Bu, normalde `src` özniteliğinin boş olacağı ve görüntünün kırmızı &quot;x&quot; olarak (veya bir görüntü bulamadığında tarayıcı tarafından ne zaman işlediğini) göstereceği anlamına gelir. Bunu engellemek için, `imagePath` değişkeninin içinde herhangi bir şey olup olmadığını görmek üzere test eden bir `if` bloğuna `<img>` öğesini yerleştirebilirsiniz. Kullanıcı bir seçim yaptıysanız `imagePath` yolu içerir. Kullanıcı bir görüntü seçmediyse veya sayfa ilk kez görüntülendiğinde `<img>` öğesi bile işlenmez.
7. Dosyayı kaydedin ve sayfayı bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.)
8. Aşağı açılan listeden bir görüntü seçin ve ardından **örnek görüntü**' e tıklayın. Farklı seçimler için farklı görüntüler görtığınızdan emin olun.

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>Görüntü karşıya yükleme

Önceki örnekte bir görüntünün dinamik olarak nasıl görüntüleneceği, ancak yalnızca Web sitenizde zaten bulunan görüntülerle çalışmakta olduğunuz gösteriliyordu. Bu yordamda, kullanıcıların bir görüntüyü karşıya yüklemesine nasıl izin ver, daha sonra sayfada görüntülenme gösterilmektedir. ASP.NET ' de resimleri oluşturma, işleme ve kaydetmenizi sağlayan yöntemler içeren `WebImage` Yardımcısı 'nı kullanarak anında görüntüleri yönetebilirsiniz. `WebImage` Yardımcısı, *. jpg*, *. png*ve *. bmp*dahil tüm ortak Web görüntüsü dosya türlerini destekler. Bu makale boyunca *. jpg* görüntülerini kullanacaksınız, ancak herhangi bir görüntü türünü kullanabilirsiniz.

![görüntüyle](9-working-with-images/_static/image2.jpg "ch9images-2. jpg")

1. Yeni bir sayfa ekleyin ve bu sayfayı *Uploadımage. cshtml*olarak adlandırın.
2. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin: 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    Metnin gövdesinde, kullanıcıların karşıya yüklenecek dosyayı seçmesini sağlayan bir `<input type="file">` öğesi vardır. **Gönder**' e tıkladıklarında, çekildikleri dosya formla birlikte gönderilir.

    Karşıya yüklenen görüntüyü almak için, görüntülerle çalışmak üzere tüm kullanışlı Yöntemler içeren `WebImage` yardımcısını kullanırsınız. Özellikle, karşıya yüklenen görüntüyü (varsa) almak ve `photo`adlı bir değişkende depolamak için `WebImage.GetImageFromRequest` kullanırsınız.

    Bu örnekteki çalışmanın çok fazla olması, dosya ve yol adlarını almayı ve ayarlamayı içerir. Sorun, kullanıcının karşıya yüklediği görüntünün adını (ve yalnızca adını) almak ve ardından görüntüyü depolayacağınız yere yeni bir yol oluşturmak istemiştir. Kullanıcılar, aynı ada sahip birden çok görüntüyü karşıya yükleyebildiğinden, benzersiz adlar oluşturmak ve kullanıcıların var olan resimlerin üzerine yazmadığından emin olmak için ek kod kullanın.

    Bir görüntü gerçekten karşıya yüklenmişse (test `if (photo != null)`) görüntünün adını görüntünün `FileName` özelliğinden alırsınız. Kullanıcı görüntüyü karşıya yüklediğinde, `FileName` kullanıcının bilgisayarından yolunu içeren özgün adını içerir. Şöyle görünebilir:

    *C:\users\joe\resim\samplephoto1.jpg*

    Tüm bu yol bilgilerini istemezsiniz ancak &#8212; gerçek dosya adını (*SamplePhoto1. jpg*) istediğiniz gibi istemezsiniz. `Path.GetFileName` yöntemini kullanarak yalnızca bir yoldan dosya açabilirsiniz, örneğin:

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    Ardından, özgün ada bir GUID ekleyerek yeni bir benzersiz dosya adı oluşturursunuz. (GUID 'Ler hakkında daha fazla bilgi için bu makaledeki [GUID 'Ler hakkında](#SB_AboutGUIDs) bölümüne bakın.) Ardından, görüntüyü kaydetmek için kullanabileceğiniz bir bütün yol oluşturursunuz. Kayıt yolu, yeni dosya adından, klasörden (görüntülerden) ve geçerli Web sitesi konumundan oluşur.

    > [!NOTE]
    > Kodunuzun *resimler* klasöründeki dosyaları kaydetmesi için, uygulamanın bu klasör için okuma-yazma izinlerine sahip olması gerekir. Geliştirme bilgisayarınızda bu genellikle bir sorun değildir. Ancak, sitenizi bir barındırma sağlayıcısının Web sunucusunda yayımladığınızda, bu izinleri açıkça ayarlamanız gerekebilir. Bu kodu bir barındırma sağlayıcısının sunucusunda çalıştırırsanız ve hata alırsanız, bu izinleri nasıl ayarlayacağınızı öğrenmek için barındırma sağlayıcısına başvurun.

    Son olarak, kayıt yolunu `WebImage` Yardımcısı 'nın `Save` yöntemine geçitirsiniz. Bu, karşıya yüklenen görüntüyü yeni adının altına depolar. Save yöntemi şöyle görünür: `photo.Save(@"~\" + imagePath)`. Tüm yol, geçerli Web sitesi konumu olan `@"~\"`eklenir. (`~` işleci hakkında daha fazla bilgi için bkz. [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)

    Önceki örnekte olduğu gibi, sayfanın gövdesi görüntünün görüntüleneceği bir `<img>` öğesi içerir. `imagePath` ayarlandıysa, `<img>` öğesi işlenir ve `src` özniteliği `imagePath` değere ayarlanır.
3. Sayfayı bir tarayıcıda çalıştırın.
4. Bir görüntüyü karşıya yükleyin ve sayfada görüntülendiğinden emin olun.
5. Sitenizde *görüntüler* klasörünü açın. Dosya adının şuna benzer bir şekilde göründüğünü yeni bir dosya eklendiğini görürsünüz: 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto. png*

    Bu, adının önekli bir GUID ile karşıya yüklediğiniz görüntüdür. (Kendi dosyanız farklı bir GUID 'e sahip olur ve muhtemelen *myphoto. png*'den farklı bir şey olarak adlandırılır.)

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>GUID 'Ler hakkında
> 
> GUID (Global-Unique ID), genellikle şöyle bir biçimde işlenen bir tanıtıcıdır: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`. Sayılar ve harfler (A-F) Her GUID için farklılık gösterir, ancak hepsi 8-4-4-4-12 karakterlik grupları kullanma düzenlerini izler. (Teknik olarak, bir GUID 16 baytlık/128 bit bir sayıdır.) Bir GUID gerekiyorsa, sizin için bir GUID üreten özelleştirilmiş kodu çağırabilirsiniz. GUID 'lerin arkasındaki düşünce, sayının çok büyük boyutu (3,4 x 10<sup>38</sup>) ve oluşturma algoritması arasında, sonuçta elde edilen sayının bir türden biri olması durumunda neredeyse garanti edilir. Bu nedenle, her iki kez de aynı adı kullanmayacağından emin olmanız gerektiğinde, nesnelerin adlarını oluşturmak için iyi bir yoldur. Tabii ki, bu, GUID 'lerin özellikle Kullanıcı dostu olmadığı için, ad yalnızca kodda kullanıldığında kullanılır.

<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>Görüntüyü Yeniden Boyutlandırma

Web siteniz bir kullanıcıdan görüntüleri kabul ediyorsa, görüntüleri görüntülemeden veya kaydetmeden önce yeniden boyutlandırmak isteyebilirsiniz. Bunun için `WebImage` yardımcısını kullanabilirsiniz.

Bu yordamda karşıya yüklenen görüntünün bir küçük resim oluşturmak için yeniden boyutlandırılması ve sonra küçük resim ve özgün görüntünün Web sitesine kaydedilmesi gösterilmektedir. Sayfada küçük resmi görüntüler ve bir köprü kullanarak kullanıcıları tam boyutlu görüntüye yönlendirebilirsiniz.

![görüntüyle](9-working-with-images/_static/image3.jpg "ch9images-3. jpg")

1. *Thumbnail. cshtml*adlı yeni bir sayfa ekleyin.
2. *Görüntüler* klasöründe, *thumbs*adında bir alt klasör oluşturun.
3. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin: 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    Bu kod, önceki örnekteki koda benzerdir. Bu fark, görüntünün küçük bir kopyasını oluşturduktan sonra, bu kodun görüntüyü normal bir kez ve bir kez kaydetmektedir. Önce karşıya yüklenen görüntüyü alın ve *görüntüler* klasörüne kaydedin. Ardından küçük resim görüntüsü için yeni bir yol oluşturursunuz. Küçük resmi oluşturmak için, `WebImage` yardımcının `Resize` yöntemini çağırarak, 60 piksellik bir görüntüye göre 60 piksellik bir görüntü oluşturabilirsiniz. Örnek, en boy oranını nasıl koruyabileceğinizi ve görüntünün genişletilmesini nasıl önleyebileceğinizi gösterir (yeni boyut aslında görüntüyü daha büyük hale getirir). Yeniden boyutlandırılmış resim daha sonra *thumbs* alt klasörüne kaydedilir.

    Biçimlendirmenin sonunda, görüntüyü koşullu olarak göstermek için önceki örneklerde gördüğünüz dinamik `src` özniteliğiyle aynı `<img>` öğesini kullanırsınız. Bu durumda, küçük resmi görüntüleriz. Ayrıca, görüntünün büyük sürümüne köprü oluşturmak için bir `<a>` öğesi kullanırsınız. `<img>` öğesinin `src` özniteliğinde olduğu gibi, `<a>` öğenin `href` özniteliğini dinamik olarak `imagePath`olarak ayarlarsınız. Yolun URL olarak çalıştığından emin olmak için `imagePath` `Html.AttributeEncode` yöntemine geçitirsiniz ve bu, yoldaki ayrılmış karakterleri bir URL 'de tamam olan karakterlere dönüştürür.
4. Sayfayı bir tarayıcıda çalıştırın.
5. Fotoğrafı karşıya yükleyin ve küçük resmin gösterildiğini doğrulayın.
6. Tam boyutlu görüntüyü görmek için küçük resme tıklayın.
7. *Resimlerde* ve *resimlerde/thumbs*'da yeni dosyaların eklendiğini unutmayın.

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>Bir görüntüyü döndürme ve çevirme

`WebImage` Yardımcısı, görüntüleri çevirmenize ve döndürmenize de olanak tanır. Bu yordamda, sunucudan bir görüntünün nasıl alınacağı, görüntünün baş aşağı ters çevrilme (dikey), nasıl kaydedileceği ve sonra çevrilmiş görüntüyü sayfada görüntülemesi gösterilmektedir. Bu örnekte, yalnızca sunucuda zaten sahip olduğunuz bir dosyayı kullanıyorsunuz (*Photo2. jpg*). Gerçek bir uygulamada, büyük olasılıkla adı, önceki örneklerde yaptığınız gibi, dinamik olarak aldığınız bir görüntüyü çevirirsiniz.

![görüntüyle](9-working-with-images/_static/image4.jpg "ch9images-4. jpg")

1. *FlipImage. cshtml*adlı yeni bir sayfa ekleyin.
2. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin: 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    Kod, sunucudan bir görüntü almak için `WebImage` yardımcısını kullanır. Görüntü yolunu, daha önceki örneklerde görüntü kaydetme için kullandığınız tekniği kullanarak oluşturursunuz ve `WebImage`kullanarak bir görüntü oluşturduğunuzda bu yolu geçirirsiniz:

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    Bir görüntü bulunursa, daha önceki örneklerde yaptığınız gibi yeni bir yol ve dosya adı oluşturursunuz. Görüntüyü çevirmek için `FlipVertical` yöntemini çağırır ve sonra görüntüyü yeniden kaydetmelisiniz.

    Görüntü, `src` özniteliği `imagePath`olarak ayarlanan `<img>` öğesi kullanılarak sayfada görüntülenir.
3. Sayfayı bir tarayıcıda çalıştırın. *Photo2. jpg* görüntüsü baş aşağı gösterilir.
4. Görüntüyü yenilemek için sayfayı yenileyin veya sayfayı tekrar isteyin.

Bir görüntüyü döndürmek için, `FlipVertical` veya `FlipHorizontal`çağırmak yerine, `RotateLeft` veya `RotateRight`çağırmanız dışında aynı kodu kullanırsınız.

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>Görüntüye filigran ekleme

Web sitenize görüntü eklediğinizde, kaydetmeden önce görüntüye bir filigran eklemek veya bir sayfada göstermek isteyebilirsiniz. İnsanlar bir görüntüye telif hakkı bilgileri eklemek veya iş adlarını tanıtmak için genellikle filigranlar kullanır.

![görüntüyle](9-working-with-images/_static/image5.jpg "ch9images-5. jpg")

1. *Filigran. cshtml*adlı yeni bir sayfa ekleyin.
2. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin: 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    Bu kod, *flipImage. cshtml* sayfasında daha erken kod gibidir (Bu kez *Photo3. jpg* dosyasını kullanır). Filigranı eklemek için, görüntüyü kaydetmeden önce `WebImage` yardımcının `AddTextWatermark` yöntemini çağırın. `AddTextWatermark`çağrısında, metni Filigranım &quot;geçirin&quot;, yazı tipi rengini sarı olarak ayarlarsınız ve yazı tipi ailesini Arial olarak ayarlarsınız. (Burada gösterilmese de `WebImage` Yardımcısı, opaklık, yazı tipi ailesi ve yazı tipi boyutu ile filigran metninin konumunu belirtmenizi sağlar.) Görüntüyü kaydettiğinizde, salt okuma olmaması gerekir.

    Daha önce gördüğünüz gibi görüntü, `@imagePath`olarak ayarlanmış src özniteliği ile `<img>` öğesi kullanılarak sayfada görüntülenir.
3. Sayfayı bir tarayıcıda çalıştırın. Resmin sağ alt köşesindeki "Filigranım" metnini görürsünüz.

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>Bir görüntüyü filigran olarak kullanma

Bir filigran için metin kullanmak yerine, başka bir görüntü kullanabilirsiniz. İnsanlar bazen bir şirket logosu gibi görüntüleri bir filigran olarak veya telif hakkı bilgileri için metin yerine bir filigran görüntüsü kullanır.

![görüntüyle](9-working-with-images/_static/image6.jpg "ch9images-6. jpg")

1. *Imagefiligran. cshtml*adlı yeni bir sayfa ekleyin.
2. *Resimler* klasörüne logo olarak kullanabileceğiniz bir görüntü ekleyin ve *mycompanylogo. jpg*görüntüsünü yeniden adlandırın. Bu görüntü, 80 piksel genişliğinde ve 20 piksel yüksekliğinde olarak ayarlandığında açıkça görebileceğiniz bir görüntü olmalıdır.
3. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin: 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    Bu, önceki örneklerden kod üzerindeki başka bir çeşitçdır. Bu durumda, görüntüyü kaydetmeden önce, hedef görüntüye (*Photo3. jpg*) filigran görüntüsünü eklemek için `AddImageWatermark` çağırın. `AddImageWatermark`çağırdığınızda, genişliğini 80 piksel ve yüksekliği 20 piksel olarak ayarlarsınız. *Mycompanylogo. jpg* görüntüsü ortasında yatay olarak hizalanır ve hedef görüntünün en altında dikey olarak hizalanmıştır. Opaklık %100 olarak ayarlanır ve doldurma 10 piksel olarak ayarlanır. Filigran görüntüsü hedef görüntüden büyükse, hiçbir şey olmaz. Filigran görüntüsü hedef görüntüden büyükse ve resim filigranı için doldurmayı sıfıra ayarlarsanız, filigran yoksayılır.

    Daha önce olduğu gibi, `<img>` öğesini ve dinamik `src` özniteliğini kullanarak görüntüyü görüntüleriz.
4. Sayfayı bir tarayıcıda çalıştırın. Filigran resminin ana görüntünün altında göründüğünü unutmayın.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[Bir ASP.NET Web sayfaları sitesinde dosyalarla çalışma](https://go.microsoft.com/fwlink/?LinkId=202896)

[Razor söz dizimini kullanarak ASP.NET Web sayfaları programlamasına giriş](https://go.microsoft.com/fwlink/?LinkID=251587)
