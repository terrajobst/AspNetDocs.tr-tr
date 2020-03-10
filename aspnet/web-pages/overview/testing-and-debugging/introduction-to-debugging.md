---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: ASP.NET Web Pages (Razor) sitelerinde hata ayıklamaya giriş | Microsoft Docs
author: Rick-Anderson
description: Hata ayıklama, kod sayfalarınızdaki hataları bulma ve düzeltme işlemidir. Bu bölümde, hata ayıklamak ve analiz etmek için kullanabileceğiniz bazı araçlar ve teknikler gösterilmektedir...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624371"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerinde hata ayıklamaya giriş

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) Web sitesinde sayfalarda hata ayıklamanın çeşitli yolları açıklanmaktadır. Hata ayıklama, kod sayfalarınızdaki hataları bulma ve düzeltme işlemidir.
>
> **Şunları öğreneceksiniz:**
>
> - Sayfaların çözümlenmesine ve hata ayıklamasına yardımcı olan bilgileri görüntüleme.
> - Visual Studio 'da hata ayıklama araçlarını kullanma.
>
>
> Makalesinde sunulan ASP.NET özellikleri şunlardır:
>
> - `ServerInfo` Yardımcısı.
> - `ObjectInfo` Yardımcısı.
>
>
> ## <a name="software-versions"></a>Yazılım sürümleri
>
>
> - ASP.NET Web sayfaları (Razor) 3
> - Visual Studio 2013
>
>
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir. WebMatrix 3 ' ü kullanabilirsiniz, ancak tümleşik hata ayıklayıcı desteklenmez.

Kodunuzdaki hataların ve sorunların giderilmesi için önemli bir en önemli nokta, bunları ilk yerde kullanmaktan kaçınmaktır. Bu, kodunuzun `try/catch` bloklarında hatalara neden olması olası bölümlerini yerleştirerek yapabilirsiniz. Daha fazla bilgi için, [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkId=202890)konusundaki hataları işleme bölümüne bakın.

`ServerInfo` Yardımcısı, sayfanızı barındıran Web sunucusu ortamı hakkındaki bilgilere genel bakış sunan bir tanılama aracıdır. Ayrıca, bir tarayıcı sayfayı istediğinde gönderilen HTTP isteği bilgilerini gösterir. `ServerInfo` Yardımcısı geçerli kullanıcı kimliğini, isteği yapan tarayıcının türünü ve bu şekilde devam eder. Bu tür bilgiler, yaygın sorunları gidermenize yardımcı olabilir.

1. *ServerInfo. cshtml*adlı yeni bir Web sayfası oluşturun.
2. Sayfanın sonunda, kapatma `</body>` etiketinden hemen önce, `@ServerInfo.GetHtml()`ekleyin:

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    `ServerInfo` kodunu sayfada herhangi bir yere ekleyebilirsiniz. Ancak sonuna eklemek, çıktısını diğer sayfa İçeriğinizden ayrı tutar, bu da daha kolay okunabilir hale gelir.

    > [!NOTE]
    >
    > **Önemli** Web sayfalarını bir üretim sunucusuna taşımadan önce Web sayfalarınızdaki tüm tanılama kodlarını kaldırmanız gerekir. Bu, `ServerInfo` Yardımcısı ve bir sayfaya kod eklemeyi kapsayan diğer tanılama teknikleri için de geçerlidir. Web sitesi ziyaretçilerinizin, sunucunuzun adı, Kullanıcı adları, sunucunuzdaki yollarınız ve benzer ayrıntılarla ilgili bilgileri görmesini istemezsiniz, çünkü bu tür bilgiler kötü amaçlı olan kişiler için yararlı olabilir.
3. Sayfayı kaydedin ve bir tarayıcıda çalıştırın.

    ![Hata ayıklama-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo` Yardımcısı, sayfada dört bilgi tablosu görüntüler:

   - Sunucu yapılandırması. Bu bölümde bilgisayar adı, çalıştırdığınız ASP.NET sürümü, etki alanı adı ve sunucu saati dahil olmak üzere barındırma Web sunucusu hakkında bilgi sağlanır.
   - ASP.NET sunucu değişkenleri. Bu bölüm, birçok HTTP protokol ayrıntıları (HTTP değişkenleri adı verilir) ve her bir Web sayfası isteğinin parçası olan değerler hakkında ayrıntılar sağlar.
   - HTTP çalışma zamanı bilgileri. Bu bölüm, Web sayfanızın altında çalıştığı Microsoft .NET Framework sürümü, yol, önbellek hakkındaki ayrıntılar vb. hakkında ayrıntılar sağlar. ( [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkId=202890)konusunda öğrendiğiniz gibi, Razor söz dizimi kullanan ASP.NET Web sayfaları Microsoft 'un kendi ASP.NET Web sunucusu teknolojisine kurulmuştur ve bu, .NET Framework adlı kapsamlı bir yazılım geliştirme kitaplığı üzerine kurulmuştur.)
   - Ortam değişkenleri. Bu bölüm, Web sunucusundaki tüm yerel ortam değişkenlerinin ve bunların değerlerinin bir listesini sağlar.

     Tüm sunucu ve istek bilgilerinin tam açıklaması Bu makalenin kapsamı dışındadır, ancak `ServerInfo` Yardımcısı 'nın çok sayıda tanılama bilgisi döndürdüğünden emin olabilirsiniz. `ServerInfo` döndürdüğü değerler hakkında daha fazla bilgi için, MSDN Web sitesindeki Microsoft TechNet Web sitesindeki ve [IIS sunucu değişkenlerinde](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) [tanınan ortam değişkenlerine](https://technet.microsoft.com/library/dd560744(WS.10).aspx) bakın.

## <a name="embedding-output-expressions-to-display-page-values"></a>Sayfa değerlerini göstermek için çıkış Ifadeleri katıştırma

Kodunuzda neler olduğunu görmenin bir diğer yolu da sayfada çıkış ifadelerini katıştırmaya yönelik bir yoldur. Bildiğiniz gibi, sayfaya `@myVariable` veya `@(subTotal * 12)` gibi bir şey ekleyerek bir değişkenin değerini doğrudan çıktısını alabilirsiniz. Hata ayıklama için, bu çıktı ifadelerini kodunuzda stratejik noktalara yerleştirebilirsiniz. Bu, sayfanız çalıştırıldığında anahtar değişkenlerinin veya hesaplamaların sonucunun değerini görmenizi sağlar. Hata ayıklamayı tamamladıktan sonra ifadeleri kaldırabilir veya açıklamaları dışarı yerleştirebilirsiniz. Bu yordam, bir sayfada hata ayıklamaya yardımcı olmak için katıştırılmış ifadeleri kullanmanın tipik bir yolunu gösterir.

1. *Outputexpression. cshtml*adlı yeni bir WebMatrix sayfası oluşturun.
2. Sayfa içeriğini aşağıdaki kodla değiştirin:

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    Örnek, `weekday` değişkeninin değerini denetlemek için bir `switch` ifadesini kullanır ve sonra haftanın hangi gününe bağlı olarak farklı bir çıkış iletisi görüntüler. Örnekte, ilk kod bloğunun içindeki `if` bloğu, geçerli iş günü değerine bir gün ekleyerek haftanın gününü rasgele değiştirir. Bu, çizim amacıyla sunulan bir hatadır.
3. Sayfayı kaydedin ve bir tarayıcıda çalıştırın.

    Sayfada, bu ileti, haftanın yanlış günü için görüntülenir. Haftanın hangi gününde olduğu, bir gün daha sonra mesajı görürsünüz. Bu durumda, iletinin neden yanlış gün değerini kasıtlı olarak ayarladığından emin olmak için, gerçekte kodda yanlış olan yerleri öğreniyor. Hata ayıklamak için, `weekday`gibi anahtar nesne ve değişkenlerin değerde neler olduğunu bulmanız gerekir.
4. Koddaki yorumlarla belirtilen iki yerde gösterildiği gibi `@weekday` ekleyerek çıkış ifadeleri ekleyin. Bu çıkış ifadeleri, kod yürütmesindeki bu noktada değişkenin değerlerini görüntüler.

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. Sayfayı bir tarayıcıda kaydedin ve çalıştırın.

    Bu sayfa, haftanın gerçek gününü, ardından bir gün eklemek ve sonra da `switch` deyimindeki sonuç iletisini görüntüler. Çıkışa herhangi bir HTML `<p>` etiketi eklemediğiniz için, iki değişken ifadesinin (`@weekday`) çıktısında günler arasında boşluk yok; ifadeler yalnızca test içindir.

    ![Hata ayıklama-2](introduction-to-debugging/_static/image2.jpg)

    Artık hatanın nerede olduğunu görebilirsiniz. Kodda `weekday` değişkenini ilk kez görüntülediğinizde, doğru günü gösterir. İkinci kez görüntülediğinizde, koddaki `if` bloğundan sonra, gün bir olur. Bu nedenle, haftanın günü değişkeninin birinci ve ikinci görünümü arasında bir şeyin gerçekleştiğini öğrenmiş olursunuz. Bu gerçek bir hatasa, bu tür bir yaklaşım soruna neden olan kodun konumunu daraltmanıza yardımcı olur.
6. Eklediğiniz iki çıkış ifadesini kaldırarak ve haftanın gününü değiştiren kodu kaldırarak sayfadaki kodu onarın. Geri kalan ve tamamen kod bloğu aşağıdaki örneğe benzer şekilde görünür:

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. Sayfayı bir tarayıcıda çalıştırın. Bu kez, haftanın gerçek günü için doğru ileti görüntülendiğini görürsünüz.

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>Nesne değerlerini göstermek için ObjectInfo Yardımcısını kullanma

`ObjectInfo` Yardımcısı, kendisine geçirdiğiniz her nesnenin türünü ve değerini görüntüler. Kodunuzda değişkenlerin ve nesnelerin değerini görüntülemek için kullanabilirsiniz (önceki örnekteki çıkış ifadeleriyle yaptığınız gibi), Ayrıca, nesneyle ilgili veri türü bilgilerini görebilirsiniz.

1. Daha önce oluşturduğunuz *Outputexpression. cshtml* adlı dosyayı açın.
2. Sayfadaki tüm kodu aşağıdaki kod bloğuna değiştirin:

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. Sayfayı bir tarayıcıda kaydedin ve çalıştırın.

    ![Hata ayıklama-4](introduction-to-debugging/_static/image3.jpg)

    Bu örnekte `ObjectInfo` Yardımcısı iki öğe görüntüler:

   - Tür. İlk değişken için tür `DayOfWeek`. İkinci değişken için tür `String`.
   - Değer. Bu durumda, tebrik değişkeninin değerini sayfada zaten görüntülen için, değişkeni `ObjectInfo`geçirdiğinizde değer yeniden görüntülenir.

     Daha karmaşık nesneler için `ObjectInfo` Yardımcısı temel olarak daha fazla bilgi &#8212; görüntüleyebilir. Bu, bir nesnenin tüm özelliklerinin türlerini ve değerlerini görüntüleyebilir.

## <a name="using-debugging-tools-in-visual-studio"></a>Visual Studio 'da hata ayıklama araçları kullanma

Daha kapsamlı bir hata ayıklama deneyimi için [Visual Studio 'yu](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)kullanın. Visual Studio ile kodunuzda, incelemek istediğiniz satıra bir kesme noktası ayarlayabilirsiniz.

![Kesme noktası ayarla](introduction-to-debugging/_static/image1.png)

Web sitesini test ettiğinizde yürütülen kod kesme noktasında durur.

![kesme noktasına ulaşma](introduction-to-debugging/_static/image2.png)

Değişkenlerin geçerli değerlerini inceleyebilir ve kod satırı satır içinde ilerleyerek adımları izleyebilirsiniz.

![değerleri gör](introduction-to-debugging/_static/image3.png)

ASP.NET Razor sayfalarında hata ayıklamak için Visual Studio 'da tümleşik hata ayıklayıcı kullanma hakkında bilgi için bkz. [Visual Studio kullanarak ASP.NET Web Pages (Razor) programlama](https://go.microsoft.com/fwlink/?LinkId=205854).

## <a name="additional-resources"></a>Ek Kaynaklar

- [Visual Studio kullanarak ASP.NET Web Pages (Razor) programlama](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS sunucu değişkenleri](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)
- [Tanınan ortam değişkenleri](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)
