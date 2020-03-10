---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: ASP.NET Web Pages (Razor) sitesinde yardımcı oluşturma ve kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde nasıl yardımcı oluşturulacağı açıklanır. Yardımcı, kod ve perf için biçimlendirme içeren yeniden kullanılabilir bir bileşendir...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563513"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>ASP.NET Web Pages (Razor) sitesinde yardımcı oluşturma ve kullanma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) Web sitesinde nasıl yardımcı oluşturulacağı açıklanır. *Yardımcı* , sıkıcı veya karmaşık olabilecek bir görevi gerçekleştirmek için kod ve biçimlendirme içeren yeniden kullanılabilir bir bileşendir.
> 
> **Şunları öğreneceksiniz:** 
> 
> - Basit bir yardımcı oluşturma ve kullanma.
> 
> Makalesinde sunulan ASP.NET özellikleri şunlardır:
> 
> - `@helper` sözdizimi.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

## <a name="overview-of-helpers"></a>Yardımcıların Özeti

Sitenizdeki farklı sayfalarda aynı görevleri gerçekleştirmeniz gerekiyorsa, bir yardımcı kullanabilirsiniz. ASP.NET Web sayfaları bir dizi yardımcı içerir ve indirebileceğiniz ve yükleyebileceğiniz pek çok daha vardır. (ASP.NET Web sayfalarındaki yerleşik yardımcılar listesi, [ASP.NET API hızlı başvurusu](https://go.microsoft.com/fwlink/?LinkId=202907)' nda listelenmiştir.) Mevcut yardımcıların hiçbiri gereksinimlerinizi karşılamıyorsa, kendi yardımcınızın oluşturulmasını sağlayabilirsiniz.

Yardımcı, birden çok sayfada ortak bir kod bloğu kullanmanıza olanak sağlar. Sayfanızda genellikle normal paragraflardan ayrı olarak ayarlanan bir dekont öğesi oluşturmak istediğinizi varsayalım. Büyük olasılıkla, bir kenarlık içeren bir kutu olarak stillendirilmiş bir `<div>` öğesi olarak oluşturulur. Her bir notun görüntülenmesini istediğiniz her seferinde aynı biçimlendirmeyi bir sayfaya eklemek yerine, biçimlendirmeyi bir yardımcı olarak paketleyebilir. Daha sonra, tek bir kod satırıyla ihtiyacınız olan her yerde nota ekleyebilirsiniz.

Bunun gibi bir yardımcı kullanmak, sayfalarınızın her birinde kodu daha basit ve daha kolay okunabilir hale getirir. Ayrıca, notlarınızın nasıl görüneceğini değiştirmeniz gerekiyorsa, biçimlendirmeyi tek bir yerde değiştirebilirsiniz, ancak bu da sitenizin korunmasını kolaylaştırır.

## <a name="creating-a-helper"></a>Yardımcı oluşturma

Bu yordam, yalnızca açıklandığı gibi, notun oluşturulduğu yardımcıyı nasıl oluşturacağınız gösterilmektedir. Bu basit bir örnektir ancak özel yardımcı, ihtiyacınız olan herhangi bir biçimlendirme ve ASP.NET kodu içerebilir.

1. Web sitesinin kök klasöründe, *uygulama\_kodu*adlı bir klasör oluşturun. Bu, ASP.NET ' de, yardımcılar gibi bileşenler için kod koyabileceğiniz ayrılmış bir klasör adıdır.
2. *Uygulama\_kodu* klasöründe yeni bir *. cshtml* dosyası oluşturun ve *myyardımcıları. cshtml*olarak adlandırın.
3. Var olan içeriği aşağıdaki ile değiştirin:

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    Kod, `MakeNote`adlı yeni bir yardımcı bildirmek için `@helper` sözdizimini kullanır. Bu belirli yardımcı, metin ve biçimlendirme birleşimini içerebilen `content` adlı bir parametreyi geçirmenize olanak sağlar. Yardımcı, dizeyi `@content` değişkenini kullanarak notun gövdesine ekler.

    Dosyanın *myhelper. cshtml*olarak adlandırıldığına, ancak yardımcının `MakeNote`adlandırıldığına dikkat edin. Birden çok özel yardımcıları tek bir dosyaya yerleştirebilirsiniz.
4. Dosyayı kaydedin ve kapatın.

## <a name="using-the-helper-in-a-page"></a>Bir sayfada yardımcı kullanma

1. Kök klasörde, *TestHelper. cshtml*adlı yeni bir boş dosya oluşturun.
2. Dosyaya aşağıdaki kodu ekleyin:

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    Oluşturduğunuz yardımcı 'yı çağırmak için, `@` ve ardından yardımcı, bir nokta ve ardından yardımcı adı olan dosya adı ' nı kullanın. ( *App\_Code* klasöründe birden çok klasörünüz varsa, yardımcı uygulamanızı herhangi bir iç içe klasör düzeyinde çağırmak için `@FolderName.FileName.HelperName` sözdizimini kullanabilirsiniz. Parantez içinde tırnak işaretleri içine eklediğiniz metin, yardımcının Web sayfasındaki notun bir parçası olarak görüntüleyeceği metindir.
3. Sayfayı kaydedin ve bir tarayıcıda çalıştırın. Yardımcı, iki paragraf arasında Yardımcısı nerede olduğunu doğrudan bir şekilde oluşturur.

    ![Tarayıcıdaki sayfanın yanı sıra, belirtilen metnin etrafına bir kutu yerleştiren nasıl yardımcı olan biçimlendirme gösteren ekran görüntüsü.](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a>Ek Kaynaklar

[Razor Yardımcısı olarak yatay menü](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341). Mike Pope tarafından yapılan bu blog girişi, biçimlendirme, CSS ve kod kullanarak bir yardımcı olarak yatay bir menü oluşturmayı gösterir.

[WebMatrix ve ASP.net mvc3 için ASP.NET Web sayfaları yardımcılarını kullanarak HTML5](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)'yi kullanma. Sam Abkıham tarafından bu blog girdisi HTML5 `Canvas` öğesi işleyen bir yardımcı gösterir.

[WebMatrix 'te @Helpers ve @Functions arasındaki fark](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix). Mike Brind tarafından yapılan bu blog girdisi `@helper` sözdizimini ve `@function` sözdizimini ve ne zaman kullanılacağını açıklar.
