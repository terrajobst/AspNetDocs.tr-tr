---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: ASP.NET Web Pages (Razor) sitelerinde tutarlı bir düzen oluşturma | Microsoft Docs
author: Rick-Anderson
description: Siteniz için Web sayfaları oluşturmayı daha verimli hale getirmek için, Web siteniz için yeniden kullanılabilir içerik blokları (üstbilgiler ve altbilgiler gibi) oluşturabilir ve c...
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627451"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerinde tutarlı bir düzen oluşturma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde düzen sayfalarını kullanarak, yeniden kullanılabilir içerik blokları (üstbilgiler ve altbilgiler gibi) oluşturma ve sitedeki tüm sayfalar için tutarlı bir görünüm oluşturma işlemleri açıklanmaktadır.
> 
> **Şunları öğreneceksiniz:** 
> 
> - Üst bilgiler ve altbilgiler gibi yeniden kullanılabilir içerik blokları oluşturma.
> - Bir düzen kullanarak sitenizdeki tüm sayfalar için tutarlı bir görünüm oluşturma.
> - Çalışma zamanında verileri bir düzen sayfasına geçirme.
> 
> Makalesinde sunulan ASP.NET özellikleri şunlardır:
> 
> - Birden çok sayfaya eklenecek HTML biçimli içerik içeren dosyalar olan içerik blokları.
> - Web sitesindeki sayfalarla paylaşılabilen, HTML biçimli içerik içeren sayfalar olan düzen sayfaları.
> - `RenderPage`, `RenderBody`ve `RenderSection` yöntemleri, bu da sayfa öğelerinin nereye ekleneceği ASP.NET bildirir.
> - İçerik blokları ve düzen sayfaları arasında veri paylaşmanıza olanak sağlayan `PageData` sözlüğü.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

## <a name="about-layout-pages"></a>Düzen sayfaları hakkında

Birçok Web sitesinde, bir üst bilgi ve altbilgi gibi her sayfada görüntülenen içerik veya kullanıcılara oturum açtığı kullanıcılara söyleyen bir kutu vardır. ASP.NET, yalnızca normal bir Web sayfası gibi metin, biçimlendirme ve kod içerebilen bir içerik bloğu ile ayrı bir dosya oluşturmanıza olanak sağlar. Daha sonra içerik bloğunu, bilgilerin görünmesini istediğiniz sitede diğer sayfalara ekleyebilirsiniz. Bu şekilde, aynı içeriği her sayfaya kopyalayıp yapıştırmanıza gerek kalmaz. Bu gibi yaygın içerik oluşturmak sitenizin güncelleştirilmesini de kolaylaştırır. İçeriği değiştirmeniz gerekiyorsa yalnızca tek bir dosyayı güncelleştirebilir ve değişiklikler içeriğin eklendiği her yerde yansıtılır.

Aşağıdaki diyagramda, içerik bloklarının nasıl çalıştığı gösterilmektedir. Bir tarayıcı web sunucusundan bir sayfa istediğinde, ASP.NET, ana sayfada `RenderPage` yönteminin çağrıldığı noktaya içerik blokları ekler. Tamamlandı (birleştirilmiş) sayfası tarayıcıya gönderilir.

![RenderPage yönteminin geçerli sayfaya başvurulan bir sayfa ekleme şeklini gösteren kavramsal diyagram.](3-creating-a-consistent-look/_static/image1.jpg)

Bu yordamda, ayrı dosyalarda bulunan iki içerik blobuna (bir üst bilgi ve alt bilgi) başvuran bir sayfa oluşturacaksınız. Aynı içerik bloklarını sitenizdeki herhangi bir sayfada kullanabilirsiniz. İşiniz bittiğinde şöyle bir sayfa alacaksınız:

![Tarayıcıdaki bir sayfayı, RenderPage yöntemine yapılan çağrıları içeren bir sayfanın çalıştırılmasının sonucu gösteren ekran görüntüsü.](3-creating-a-consistent-look/_static/image2.png)

1. Web sitenizin kök klasöründe *Index. cshtml*adlı bir dosya oluşturun.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. Kök klasörde, *paylaşılan*adlı bir klasör oluşturun.

    > [!NOTE]
    > *Paylaşılan*adlı bir klasörde Web sayfaları arasında paylaşılan dosyaları depolamak yaygın bir uygulamadır.
4. *Paylaşılan* klasörde, *\_Header. cshtml*adlı bir dosya oluşturun.
5. Var olan tüm içerikleri aşağıdakiler ile değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    Dosya adının üst çizgi (\_) bir ön ek olarak *\_Header. cshtml*olduğuna dikkat edin. ASP.NET, adı bir alt çizgiyle başlıyorsa tarayıcıya sayfa göndermez. Bu, kullanıcıların bu sayfaları doğrudan istememelerini (farkında veya başka şekilde) engeller. Kullanıcıların bu sayfaları &#8212; yalnızca diğer sayfalara eklenmesine izin vermek istemediğiniz için, bir alt çizgi kullanarak bunlarda içerik blokları olan sayfaları da kullanabilirsiniz.
6. *Paylaşılan* klasörde, *\_footer. cshtml* adlı bir dosya oluşturun ve içeriği aşağıdaki ile değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. *Index. cshtml* sayfasında, `RenderPage` yöntemine aşağıda gösterildiği gibi iki çağrı ekleyin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    Bu, bir Web sayfasına içerik bloğunun nasıl ekleneceğini gösterir. `RenderPage` yöntemini çağırır ve bu noktada içeriğini eklemek istediğiniz dosyanın adını geçirin. Burada, *\_Header. cshtml* ve *\_footer. cshtml* dosyalarının içeriğini *Index. cshtml* dosyasına yerleştiriyoruz.
8. *Index. cshtml* sayfasını bir tarayıcıda çalıştırın. (WebMatrix 'te **dosyalar** çalışma alanında, dosyaya sağ tıklayın ve ardından **tarayıcıda Başlat**' ı seçin.)
9. Tarayıcıda, sayfa kaynağını görüntüleyin. (Örneğin, Internet Explorer 'da, sayfaya sağ tıklayın ve **kaynağı görüntüle**' ye tıklayın.)

    Bu, Dizin sayfası işaretlemesini içerik bloklarıyla birleştiren tarayıcıya gönderilen Web sayfası işaretlemesini görmenizi sağlar. Aşağıdaki örnek, *Index. cshtml*için işlenen sayfa kaynağını gösterir. *Index. cshtml* içine eklediğiniz `RenderPage` çağrıları, üst bilgi ve altbilgi dosyalarının gerçek içeriğiyle değiştirilmiştir.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>Düzen sayfaları kullanarak tutarlı bir görünüm oluşturma

Şimdiye kadar, aynı içeriği birden çok sayfaya eklemek kolay olduğunu gördünüz. Bir site için tutarlı bir görünüm oluşturmaya yönelik daha yapılandırılmış bir yaklaşım, düzen sayfalarını kullanmaktır. Düzen sayfası bir Web sayfasının yapısını tanımlar, ancak hiçbir gerçek içeriği içermez. Bir düzen sayfası oluşturduktan sonra içeriği içeren Web sayfaları oluşturabilir ve ardından bunları düzen sayfasına bağlayabilirsiniz. Bu sayfalar görüntülendiğinde, düzen sayfasına göre biçimlendirilir. (Bu anlamda, Düzen sayfası diğer sayfalarda tanımlanmış içerik için şablon türü olarak davranır.)

Düzen sayfası, her HTML sayfası gibi olduğundan, `RenderBody` yöntemine bir çağrı içerir. Düzen sayfasındaki `RenderBody` yönteminin konumu, içerik sayfasındaki bilgilerin nereye ekleneceğini belirler.

Aşağıdaki diyagramda, tamamlanmış Web sayfasını oluşturmak için içerik sayfaları ve düzen sayfalarının çalışma zamanında nasıl birleştirileceği gösterilmektedir. Tarayıcı bir içerik sayfası ister. İçerik sayfasında, sayfanın yapısı için kullanılacak düzen sayfasını belirten kod bulunur. Düzen sayfasında, içerik `RenderBody` yönteminin çağrıldığı noktaya eklenir. İçerik blokları, önceki bölümde yaptığınız şekilde `RenderPage` yöntemi çağırarak düzen sayfasına da eklenebilir. Web sayfası tamamlandığında tarayıcıya gönderilir.

![Tarayıcıdaki bir sayfayı, RenderBody metoduna yapılan çağrıları içeren bir sayfanın çalıştırılmasının sonucu gösteren ekran görüntüsü.](3-creating-a-consistent-look/_static/image3.jpg)

Aşağıdaki yordamda, bir düzen sayfası oluşturma ve içerik sayfalarını buna bağlama gösterilmektedir.

1. Web sitenizin *paylaşılan* klasöründe, *\_layout1. cshtml*adlı bir dosya oluşturun.
2. Var olan tüm içerikleri aşağıdakiler ile değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    İçerik blokları eklemek için bir düzen sayfasında `RenderPage` yöntemini kullanırsınız. Düzen sayfası `RenderBody` metoduna yalnızca bir çağrı içerebilir.
3. *Paylaşılan* klasörde, *\_Header2. cshtml* adlı bir dosya oluşturun ve var olan tüm içerikleri şu şekilde değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. Kök klasörde yeni bir klasör oluşturun ve bu klasöre göre *stilleri*adlandırın.
5. *Stiller* klasöründe, *site. css* adlı bir dosya oluşturun ve aşağıdaki stil tanımlarını ekleyin:

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    Bu stil tanımları yalnızca, düzen sayfalarıyla birlikte stil sayfalarının nasıl kullanılabileceğini göstermek için geçerlidir. İsterseniz, bu öğeler için kendi stillerinizi tanımlayabilirsiniz.
6. Kök klasörde, *Content1. cshtml* adlı bir dosya oluşturun ve var olan tüm içerikleri şu şekilde değiştirin:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    Bu, Düzen sayfası kullanacak bir sayfasıdır. Sayfanın üst kısmındaki kod bloğu, bu içeriği biçimlendirmek için hangi düzen sayfasının kullanılacağını gösterir.
7. Tarayıcıda *Content1. cshtml* dosyasını çalıştırın. İşlenmiş sayfa, *\_layout1. cshtml* içinde tanımlanan biçim ve stil sayfasını ve *Content1. cshtml*dosyasında tanımlanan metni (içerik) kullanır.

    ![görüntüyle](3-creating-a-consistent-look/_static/image4.png)

    Daha sonra aynı düzen sayfasını paylaşabilen ek içerik sayfaları oluşturmak için 6. adımı tekrarlayabilirsiniz.

    > [!NOTE]
    > Sitenizi, bir klasördeki tüm içerik sayfaları için otomatik olarak aynı düzen sayfasını kullanabilmeniz için ayarlayabilirsiniz. Ayrıntılar için bkz. [ASP.NET Web Pages Için site genelinde davranışı özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906).

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>Birden çok Içerik bölümü olan düzen sayfaları tasarlama

Bir içerik sayfasında birden fazla bölüm olabilir. Bu, değiştirilebilir içeriğe sahip birden fazla alana sahip olan düzenleri kullanmak istiyorsanız yararlıdır. İçerik sayfasında, her bölüme benzersiz bir ad verirsiniz. (Varsayılan bölüm, adlandırılmamış ' dır.) Düzen sayfasında, adlandırılmamış (varsayılan) bölümün nerede görüneceğini belirtmek için bir `RenderBody` yöntemi eklersiniz. Daha sonra adlandırılmış bölümleri tek tek işlemek için ayrı `RenderSection` Yöntemler eklersiniz.

Aşağıdaki diyagramda, ASP.NET 'in birden çok bölüme bölünen içeriği nasıl işleyeceği gösterilmektedir. Her bir adlandırılmış bölüm, içerik sayfasındaki bir bölüm bloğunda bulunur. (`Header` adlandırılırsınız ve örnekteki `List`.) Çerçeve, `RenderSection` yönteminin çağrıldığı noktada düzen sayfasına içerik bölümü ekler. Adlandırılmamış (varsayılan) bölüm, daha önce gördüğünüz gibi `RenderBody` yönteminin çağrıldığı noktaya eklenir.

![RenderSection yönteminin geçerli sayfaya nasıl başvuru bölümleri eklediğini gösteren kavramsal diyagram.](3-creating-a-consistent-look/_static/image5.jpg)

Bu yordamda, birden fazla içerik bölümüne sahip bir içerik sayfasının nasıl oluşturulacağı ve birden çok içerik bölümünü destekleyen bir düzen sayfası kullanılarak nasıl işlenmesi gösterilmektedir.

1. *Paylaşılan* klasörde, *\_layout2. cshtml*adlı bir dosya oluşturun.
2. Var olan tüm içerikleri aşağıdakiler ile değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    Hem üstbilgi hem de liste bölümlerini işlemek için `RenderSection` yöntemini kullanırsınız.
3. Kök klasörde, *Content2. cshtml* adlı bir dosya oluşturun ve var olan tüm içerikleri şu şekilde değiştirin:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    Bu içerik sayfası sayfanın üst kısmında bir kod bloğu içerir. Her bir adlandırılmış bölüm bir bölüm bloğunda bulunur. Sayfanın geri kalanı varsayılan (adlandırılmamış) içerik bölümünü içerir.
4. Tarayıcıda *Content2. cshtml* dosyasını çalıştırın.

    ![Tarayıcıda, RenderSection metoduna çağrılar içeren bir sayfanın çalıştırılmasının sonucu olan bir sayfayı gösteren ekran görüntüsü.](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a>Içerik bölümlerini Isteğe bağlı hale getirme

Normalde, bir içerik sayfasında oluşturduğunuz bölümlerin, Düzen sayfasında tanımlanan bölümleri eşleşmesi gerekir. Aşağıdakilerden biri gerçekleşirse hata alabilirsiniz:

- İçerik sayfası, Düzen sayfasında karşılık gelen bir bölümü olmayan bir bölümü içerir.
- Düzen sayfası, içeriği olmayan bir bölüm içerir.
- Düzen sayfası, aynı bölümü birden çok kez işlemeye çalışır Yöntem çağrılarını içerir.

Ancak, Bölüm Düzen sayfasında isteğe bağlı olarak bildirerek adlandırılmış bir bölüm için bu davranışı geçersiz kılabilirsiniz. Bu, bir düzen sayfasını paylaşabilen ancak belirli bir bölüm için içeriğe sahip olabilecek veya olmayan birden çok içerik sayfası tanımlamanızı sağlar.

1. *Content2. cshtml* dosyasını açın ve aşağıdaki bölümü kaldırın:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. Sayfayı kaydedin ve bir tarayıcıda çalıştırın. İçerik sayfası Düzen sayfasında tanımlanan bir bölüm için içerik sağlamadığından başlık bölümü olarak bir hata mesajı görüntülenir.

    ![RenderSection yöntemini çağıran bir sayfa çalıştırırsanız, ancak karşılık gelen bölüm sağlanmadığında oluşan hatayı gösteren ekran görüntüsü.](3-creating-a-consistent-look/_static/image7.png)
3. *Paylaşılan* klasörde, *\_layout2. cshtml* sayfasını açın ve şu satırı değiştirin:

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    aşağıdaki kodla:

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    Alternatif olarak, önceki kod satırını, aynı sonuçları üreten aşağıdaki kod bloğu ile değiştirebilirsiniz:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. *Content2. cshtml* sayfasını bir tarayıcıda yeniden çalıştırın. (Bu sayfa hala tarayıcıda açıksa, yalnızca yenilemeniz yeterlidir.) Bu kez, üst bilgisi olmasa bile sayfada hata olmadan görüntülenir.

## <a name="passing-data-to-layout-pages"></a>Düzen sayfalarına veri geçirme

İçerik sayfasında, bir düzen sayfasında başvurmanız gereken verileriniz olabilir. Bu durumda, içerik sayfasından düzen sayfasına veri geçirmeniz gerekir. Örneğin, bir kullanıcının oturum açma durumunu görüntülemek veya kullanıcı girdisine göre içerik alanını göstermek ya da gizlemek isteyebilirsiniz.

Bir içerik sayfasından bir düzen sayfasına veri geçirmek için, içerik sayfasının `PageData` özelliğine değer yerleştirebilirsiniz. `PageData` özelliği, sayfalar arasında geçiş yapmak istediğiniz verileri tutan ad/değer çiftleri koleksiyonudur. Düzen sayfasında, `PageData` özelliğinden dışarı değer okuyabilirsiniz.

Başka bir diyagram. Bu, ASP.NET 'in bir içerik sayfasından düzen sayfasına değer geçirmek için `PageData` özelliğini nasıl kullanabileceğinizi gösterir. ASP.NET, Web sayfasını oluşturmaya başladığında `PageData` koleksiyonunu oluşturur. İçerik sayfasında, `PageData` koleksiyonuna veri koymak için kod yazarsınız. `PageData` koleksiyonundaki değerlere, içerik sayfasındaki diğer bölümler veya ek içerik blokları tarafından da erişilebilir.

![Bir içerik sayfasının bir PageData sözlüğünü nasıl dolduramayacağı ve bu bilgileri düzen sayfasına geçeme şeklini gösteren kavramsal diyagram.](3-creating-a-consistent-look/_static/image8.jpg)

Aşağıdaki yordamda bir içerik sayfasından bir düzen sayfasına nasıl veri geçirünün yapılacağı gösterilmektedir. Sayfa çalıştırıldığında, kullanıcının Düzen sayfasında tanımlanmış bir listeyi gizlemesini veya göstermesini sağlayan bir düğme görüntüler. Kullanıcılar düğmeye tıkladığınızda, `PageData` özelliğinde bir true/false (Boolean) değeri ayarlar. Düzen sayfası bu değeri okur ve false ise listeyi gizler. Bu değer Ayrıca, **liste Gizle** düğmesinin mi yoksa **Listeyi göster** düğmesinin mi görüntüleneceğini anlamak için içerik sayfasında de kullanılır.

![görüntüyle](3-creating-a-consistent-look/_static/image9.jpg)

1. Kök klasörde, *Content3. cshtml* adlı bir dosya oluşturun ve var olan tüm içerikleri şu şekilde değiştirin:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    Kod, `PageData` özelliğindeki &#8212; iki veri parçasını Web sayfasının başlığını, doğru ya da bir listenin görüntülenip görüntülenmeyeceğini belirtmek için true veya false olarak depolar.

    ASP.NET, bir kod bloğu kullanarak HTML işaretlemesini sayfaya koşullu olarak koymanızı sağlar. Örneğin, sayfanın gövdesinde `if/else` bloğu, `PageData["ShowList"]` doğru olarak ayarlanmış olmasına bağlı olarak hangi formun görüntüleneceğini belirler.
2. *Paylaşılan* klasörde, *\_Layout3. cshtml* adlı bir dosya oluşturun ve var olan tüm içerikleri şu şekilde değiştirin:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    Düzen sayfası, `PageData` özelliğinden başlık değerini alan `<title>` öğesinde bir ifade içerir. Ayrıca, liste içerik bloğunun görüntülenip görüntülenmeyeceğini anlamak için `PageData` özelliğinin `ShowList` değerini kullanır.
3. *Paylaşılan* klasörde, *\_List. cshtml* adlı bir dosya oluşturun ve var olan tüm içerikleri şu şekilde değiştirin:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. *Content3. cshtml* sayfasını bir tarayıcıda çalıştırın. Sayfa, sayfanın sol tarafında görünür liste ve alt kısımdaki **liste Gizle** düğmesi görüntülenir.

    ![Listeyi ve ' listeyi Gizle 'yi belirten bir düğmeyi içeren sayfayı gösteren ekran görüntüsü.](3-creating-a-consistent-look/_static/image10.png)
5. **Listeyi Gizle**' ye tıklayın. Liste kaybolur ve düğme **Listeyi göster**olarak değişir.

    ![Liste ve ' liste göster ' yazan bir düğme içermeyen sayfayı gösteren ekran görüntüsü.](3-creating-a-consistent-look/_static/image11.png)
6. **Listeyi göster** düğmesine tıklayın ve liste yeniden görüntülenir.

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web sayfaları için site genelinde davranışı özelleştirme](https://go.microsoft.com/fwlink/?LinkId=202906)
