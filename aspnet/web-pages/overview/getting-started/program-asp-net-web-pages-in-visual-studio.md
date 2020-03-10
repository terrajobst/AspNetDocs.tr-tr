---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Visual Studio kullanarak ASP.NET Web Pages (Razor) programlama | Microsoft Docs
author: Rick-Anderson
description: Bu ekte, Razor söz dizimi ile Web sayfalarını ASP.NET programlamak için Visual Studio 2010 veya Visual Web Developer 2010 Express 'i nasıl kullanabileceğiniz açıklanır.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633513"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>Visual Studio kullanarak ASP.NET Web Pages (Razor) programlama

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) Web sitelerini programlamak için Visual Studio veya Visual Web Developer Express 'i nasıl kullanabileceğiniz açıklanır.
>
> Öğrenecekleriniz
>
> - Visual Studio sürümünüzde ASP.NET Web sayfalarıyla çalışmak için (varsa) yüklemeniz gerekenler.
> - Visual Web Developer 2010 Express 'e ASP.NET Web sayfaları için destek ekleme.
> - IntelliSense ve hata ayıklayıcı dahil olmak üzere ASP.NET Razor sayfalarıyla çalışmak için Visual Studio 'daki özellikleri kullanma.
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - ASP.NET Web sayfaları (Razor) 3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> Bu öğretici Ayrıca ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010 ve WebMatrix 2 ile de kullanılabilir.

Razor söz dizimi Web sayfalarını WebMatrix veya diğer birçok kod Düzenleyicisi kullanarak ASP.NET programlayabilirsiniz. Ayrıca, çok sayıda uygulama (yalnızca Web siteleri değil) oluşturmak için güçlü bir araç kümesi sağlayan, tam özellikli bir tümleşik geliştirme ortamı (IDE) olan Microsoft Visual Studio de kullanabilirsiniz. ASP.NET Razor sayfalarıyla çalışmak için [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)' i kullanabilirsiniz.

Visual Studio 'nun ASP.NET Razor Web sayfalarıyla programlama için sağladığı, özellikle yararlı olan iki özellik şunlardır:

- *IntelliSense*. Visual Studio 'da yerleşik olarak bulunan IntelliSense özelliği, WebMatrix 'teki IntelliSense 'ten daha kapsamlıdır.
- *Hata ayıklayıcı*. Hata ayıklayıcı, çalışırken bir programı durdurup, değişkenleri inceleyerek ve satıra göre kod satırı üzerinden adımlayarak kodunuzun sorunlarını gidermenize olanak sağlar.

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>Visual Studio 'Yu ASP.NET Web sayfalarının farklı sürümleriyle kullanma

Visual Studio 2017 ' de ASP.NET Web uygulamaları geliştirmek için, **ASP.net ve Web geliştirme** iş yükünü yüklemek.

Visual Studio 2012 ve Visual Studio 2013 ASP.NET Web Pages desteğini içerir. (ASP.NET Web sayfalarını desteklemek için gereken paketler, Visual Studio 'Yu yüklediğinizde yüklenir.)

Visual Studio 2010, ASP.NET Web sayfaları için varsayılan olarak desteği içermez. Visual Studio 2010 ile ASP.NET Web sayfalarını kullanmak için ASP.NET MVC paketini yüklemelisiniz. ASP.NET Web sayfaları 2 ' yi almak için ASP.NET MVC 4 ' ü yüklersiniz.

Aşağıdaki tabloda, Visual Studio 'nun farklı sürümlerindeki ASP.NET Web sayfalarına yönelik destek özetlenmektedir.

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET Web sayfaları 2** | ASP.NET MVC 4 ' ü yükler | Verilen | Verilen |
| **ASP.NET Web sayfaları 3** |  | NuGet aracılığıyla ASP.NET Web Pages 3 ' e güncelleştirme | Verilen |

Visual Studio 2010 ile çalışmak için bkz. [Visual studio 2010 ' de ASP.NET Web Pages Için destek yükleme](#vs2010support).

## <a name="launching-visual-studio-from-webmatrix"></a>WebMatrix 'ten Visual Studio 'Yu başlatma

WebMatrix 'te bir proje başlattıysanız ve Visual Studio 'ya geçiş yapmak istiyorsanız, WebMatrix projeyi Visual Studio 'da kolayca açmak için bir düğme sağlar. Bu düğmenin etkinleştirilmesi için bilgisayarınızda Visual Studio yüklü olmalıdır. Aşağıdaki görüntüde WebMatrix içindeki düğme gösterilmektedir.

![Visual Studio 'Yu Başlat](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

Düğmeye tıkladığınızda, proje Visual Studio 'da açılır. Herhangi bir sorun olmadan WebMatrix ve Visual Studio arasında geri ve ileri geçiş yapabilirsiniz. Diğer ortamda herhangi bir dosya değiştiyse ve en son değişiklikleri almak için yeniden yüklenmesi gerekiyorsa size bildirilir.

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>Visual Studio 'da ASP.NET Razor sitesi oluşturma

Visual Studio 'da bir ASP.NET Razor Web sitesi oluşturmak için:

1. Visual Studio'yu açın.
2. **Dosya** menüsünde **Yeni Web sitesi**' ne tıklayın.

    ![Yeni Web sitesi oluştur](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. **Yeni Web sitesi** iletişim kutusunda kullanılacak dili seçin (görsel C# veya Visual Basic).
4. **ASP.NET Web sitesi (Razor)** şablonunu seçin.

    ![Razor sitesi](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. **Tamam**’a tıklayın.

Yeni projeniz var ve kullanmaya başlamanıza yardımcı olacak bazı varsayılan Web sayfalarıyla doldurulmuştur.

### <a name="using-intellisense"></a>IntelliSense Kullanma

Artık bir site oluşturduğunuza göre, IntelliSense 'in Visual Studio 'da nasıl çalıştığını görebilirsiniz.

1. Yeni oluşturduğunuz Web sitesinde *default. cshtml* sayfasını açın.
2. Sayfadaki `<h3>` etiketlerden sonra, `@ServerInfo.` (nokta dahil) yazın. IntelliSense 'in bir açılan listede `ServerInfo` Yardımcısı için kullanılabilir yöntemleri nasıl görüntüleyeceği hakkında dikkat edin.

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. Listeden `GetHtml` yöntemi seçin ve ardından ENTER tuşuna basın. IntelliSense, yöntemi otomatik olarak doldurur. (İçinde C#herhangi bir yöntemde olduğu gibi, yönteminden sonra `()` karakterler eklemeniz gerekir.) `GetHtml` yöntemi için tamamlanan kod aşağıdaki örneğe benzer şekilde görünür:

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. Sayfayı çalıştırmak için CTRL + F5 tuşlarına basın. Bu, sayfanın bir tarayıcıda görüntülenmesiyle benzer şekilde görünür:

    ![tarayıcıda varsayılan sayfa](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. Tarayıcıyı kapatın.

### <a name="using-the-debugger"></a>Hata ayıklayıcıyı kullanma

1. *Default. cshtml* sayfasının en üstünde, `Page.Title`ile başlayan satırdan sonra aşağıdaki kod satırını ekleyin:

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. Düzenleyicinin solundaki düzenleyicinin gri kenar boşluğunda, bir *kesme noktası*eklemek için bu yeni satıra ileri ' ye tıklayın. Kesme noktası, hata ayıklayıcıya programın bu noktada çalışmayı durdurmasını, böylece neler olduğunu görmeniz gerektiğini belirten bir işaretçidir.

    ![Kesme noktası ayarla](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. `ServerInfo.GetHtml` yöntemine yapılan çağrıyı kaldırın ve onun yerine `@myTime` değişkenine bir çağrı ekleyin. Bu çağrı, yeni kod satırıyla döndürülen geçerli saat değerini görüntüler.
4. Hata ayıklayıcıda sayfayı çalıştırmak için F5 tuşuna basın. Sayfa, ayarladığınız kesme noktasında durmaktadır. Aşağıdaki görüntüde, sayfanın kesme noktası (sarı) ile düzenleyicide nasıl göründüğü gösterilmektedir.

    ![hata ayıklama kesme noktası](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. Sonraki kod satırını çalıştırmak için hata ayıklama araç çubuğunda **adımla** düğmesine (veya F11 tuşuna basın) tıklayın. Bu düğmeye tıkladığınızda, yürütmeyi bir sonraki kod satırına ilerletin.

    ![Adımla düğmesi](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. `myTime` değişkenin değerini, fare işaretçinizi bunun üzerinde tutarak veya **Yereller** ve **çağrı yığını** pencerelerinde görünen değerleri inceleyerek inceleyin. Visual Studio, değişkenin değerini görüntüler.

    ![saat değerini göster](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. Değişkeni incelemeyi ve kod içinde adımlamayı tamamladıktan sonra, her satırda durmadan sayfayı çalıştırmaya devam etmek için F5 'e basın. Tüm kodda adımlamayı bitirdiğinizde tarayıcı sayfayı görüntüler.

Hata ayıklayıcı hakkında daha fazla bilgi edinmek ve Visual Studio 'da kod hata ayıklama hakkında daha fazla bilgi için bkz. [Izlenecek yol: Visual Web Developer 'Da Web sayfalarında hata ayıklama](https://msdn.microsoft.com/library/z9e7w6cs.aspx)

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>Visual Studio ile ASP.NET MVC projelerinde Razor kullanma

Razor söz dizimi Ayrıca, ASP.NET MVC projelerinde kapsamlı olarak da kullanılır. MVC, dinamik Web siteleri oluşturmaya yönelik güçlü ve desenlere dayalı bir yoldur. ASP.NET Web sayfaları sitenizin bakımı zor hale gelirse, bunu bir ASP.NET MVC uygulamasına dönüştürmeyi düşünebilirsiniz. MVC uygulaması oluşturma örneği için bkz. [ASP.NET MVC 5 Ile çalışmaya](../../../mvc/overview/getting-started/introduction/getting-started.md)başlama.

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>Visual Studio 2010 ' de ASP.NET Web sayfaları için destek yükleme

Bu bölüm Visual Studio için Visual Web Developer Express 2010 ve ASP.NET Web Pages araçları 'nın nasıl yükleneceğini gösterir.

1. Web Platformu Yükleyicisi yoksa, aşağıdaki URL 'den indirin:

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. Web Platformu Yükleyicisi 'ni çalıştırın.
3. **Ürünler** sekmesine tıklayın.

    ![WebPI ürünleri sekmesi](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. **ASP.NET MVC 4** ' ü arayın (ASP.NET Web sayfaları 2 için) ve ardından **Ekle**' ye tıklayın. Bu ürünler, ASP.NET Razor Web siteleri oluşturmak için Visual Studio araçları içerir.

    ![WebPI yüklemesi seçenekleri](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. Yüklemeyi **gerçekleştirmek için yükleme** ' ye tıklayın.
