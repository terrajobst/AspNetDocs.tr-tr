---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: Görünüm ana sayfalarıyla sayfa düzenleri oluşturma (C#) | Microsoft Docs
author: microsoft
description: Bu öğreticide, ana sayfaların görünüm özelliğinden yararlanarak uygulamanızda birden çok sayfa için ortak bir sayfa düzeni oluşturmayı öğreneceksiniz. Bir... kullanabilirsiniz
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 026e3efb4ebf84016aa0f6a5fda4af549fdadfcb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594117"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a>Görünüm Ana Sayfalarıyla Sayfa Düzenleri Oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> Bu öğreticide, ana sayfaların görünüm özelliğinden yararlanarak uygulamanızda birden çok sayfa için ortak bir sayfa düzeni oluşturmayı öğreneceksiniz. Bir görünüm ana sayfasını, örneğin, iki sütunlu bir sayfa düzeni tanımlamak ve Web uygulamanızdaki tüm sayfalar için iki sütunlu düzeni kullanmak için kullanabilirsiniz.

## <a name="creating-page-layouts-with-view-master-pages"></a>Görünüm ana sayfalarıyla sayfa düzenleri oluşturma

Bu öğreticide, ana sayfaların görünüm özelliğinden yararlanarak uygulamanızda birden çok sayfa için ortak bir sayfa düzeni oluşturmayı öğreneceksiniz. Bir görünüm ana sayfasını, örneğin, iki sütunlu bir sayfa düzeni tanımlamak ve Web uygulamanızdaki tüm sayfalar için iki sütunlu düzeni kullanmak için kullanabilirsiniz.

Ayrıca, uygulamanızda birden çok sayfada ortak içerikleri paylaşmak için ana sayfaların görünüm özelliğinden yararlanabilirsiniz. Örneğin, Web sitesi logonuzu, gezinti bağlantılarınızı ve başlık reklamlarınızı bir görünüm ana sayfasına yerleştirebilirsiniz. Bu şekilde, uygulamanızdaki her sayfada bu içerik otomatik olarak görüntülenir.

Bu öğreticide, yeni bir görünüm ana sayfası oluşturmayı ve ana sayfayı temel alan yeni bir görünüm içeriği sayfası oluşturmayı öğreneceksiniz.

### <a name="creating-a-view-master-page"></a>Bir görünüm ana sayfası oluşturma

İki sütunlu bir düzeni tanımlayan bir görünüm ana sayfası oluşturarak başlayalım. Views\Shared klasörüne sağ tıklayıp, **Add, New Item**menü seçeneğini belirleyerek ve **MVC görünüm ana sayfa** şablonunu seçerek MVC projesine yeni bir görünüm ana sayfası eklersiniz (bkz. Şekil 1).

[bir görünüm ana sayfası ekleme ![](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)

**Şekil 01**: bir görünüm ana sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))

Bir uygulamada birden fazla görünüm ana sayfası oluşturabilirsiniz. Her görünüm ana sayfası, farklı bir sayfa düzeni tanımlayabilir. Örneğin, belirli sayfaların iki sütunlu bir düzen ve diğer sayfaların üç sütunlu bir düzene sahip olmasını isteyebilirsiniz.

Bir görünüm ana sayfası, standart ASP.NET MVC görünümü gibi çok daha fazla görünür. Ancak, normal bir görünümün aksine, bir görünüm ana sayfası bir veya daha fazla `<asp:ContentPlaceHolder>` etiketi içerir. `<contentplaceholder>` etiketleri, ana sayfanın tek bir içerik sayfasında geçersiz kılınabilen bölgelerini işaretlemek için kullanılır.

Örneğin, liste 1 ' deki ana görünüm sayfası, iki sütunlu bir düzeni tanımlar. İki `<contentplaceholder>` etiketi içerir. Her sütun için bir `<ContentPlaceHolder>`.

**Listeleme 1 – `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

Liste 1 ' deki ana görünüm sayfası gövdesi iki sütuna karşılık gelen iki `<div>` etiketi içerir. Geçişli stil sayfası sütun sınıfı, hem `<div>` etiketlerine uygulanır. Bu sınıf, ana sayfanın en üstünde belirtilen stil sayfasında tanımlanmıştır. Tasarım görünümü ' ye geçerek görünüm ana sayfasının nasıl işleneceğini önizleyebilirsiniz. Kaynak kodu düzenleyicisinin sol alt kısmındaki Tasarım sekmesine tıklayın (bkz. Şekil 2).

[Tasarımcıda ana sayfanın önizlemesini ![](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)

**Şekil 02**: Tasarımcıda bir ana sayfanın önizlemesini[görüntüleme (tam boyutlu görüntüyü görüntülemek için tıklayın](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))

### <a name="creating-a-view-content-page"></a>Içerik görüntüleme sayfası oluşturma

Bir görünüm ana sayfası oluşturduktan sonra ana görünüm sayfasını temel alarak bir veya daha fazla içerik sayfası oluşturabilirsiniz. Örneğin, Views\Home klasörüne sağ tıklayıp, **Ekle, yeni öğe**' yi seçerek, **MVC görünüm içeriği sayfa** şablonunu seçerek, Index. aspx adını girerek ve **Ekle** düğmesine tıklayarak (bkz. Şekil 3), giriş denetleyicisi için bir dizin görünümü içerik sayfası oluşturabilirsiniz.

[içerik görüntüleme sayfası ekleme ![](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)

**Şekil 03**: içerik görüntüleme sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))

Ekle düğmesine tıkladıktan sonra içeriği görüntüle sayfasıyla ilişkilendirilecek bir görünüm ana sayfası seçmenizi sağlayan yeni bir iletişim kutusu görünür (bkz. Şekil 4). Önceki bölümde oluşturduğumuz site. Master görünüm ana sayfasına gidebilirsiniz.

[Ana sayfa seçme ![](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)

**Şekil 04**: Ana sayfa seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))

Site. Master ana sayfasına dayalı yeni bir görünüm içeriği sayfası oluşturduktan sonra, dosyayı liste 2 ' de alırsınız.

**Listeleme 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

Bu görünümün ana görünüm ana sayfasındaki `<asp:ContentPlaceHolder>` etiketlerinin her birine karşılık gelen bir `<asp:Content>` etiketi içerdiğine dikkat edin. Her `<asp:Content>` etiketi, geçersiz kıldığını belirten belirli `<asp:ContentPlaceHolder>` işaret eden bir ContentPlaceHolderID özniteliği içerir.

Ayrıca, liste 2 ' deki içerik görünümü sayfasının normal açma ve kapatma HTML etiketlerinin hiçbirini içermediğini fark edebilirsiniz. Örneğin, açma ve kapatma `<html>` veya `<head>` etiketleri içermez. Normal açılış ve kapanış etiketlerinin hepsi görünüm ana sayfasında bulunur.

İçeriği görüntüle sayfasında görüntülemek istediğiniz içerikler bir `<asp:Content>` etiketi içine yerleştirilmelidir. Bu etiketlerin dışına herhangi bir HTML veya diğer içerik yerleştirirseniz, sayfayı görüntülemeyi denediğinizde bir hata alırsınız.

Bir içerik görünümü sayfasındaki ana sayfadan her `<asp:ContentPlaceHolder>` etiketini geçersiz kılmanız gerekmez. Etiketi belirli içerikle değiştirmek istediğinizde yalnızca bir `<asp:ContentPlaceHolder>` etiketini geçersiz kılmanız gerekir.

Örneğin, kod 3 ' teki değiştirilen dizin görünümü yalnızca iki `<asp:Content>` etiketi içerir. `<asp:Content>` etiketlerinin her biri, bazı metinleri içerir.

**Listeleme 3 – `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

Liste 3 ' teki görünüm istendiğinde, sayfayı Şekil 5 ' te işler. Görünümün iki sütunlu bir sayfa işlediğini unutmayın. Ayrıca, içeriği görüntüle sayfasındaki içeriğin görünüm ana sayfasındaki içerikle birleştirildiğine dikkat edin.

[Dizin görünümü içerik sayfasını ![](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)

**Şekil 05**: Dizin görünümü içerik sayfası ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))

### <a name="modifying-view-master-page-content"></a>Görünüm ana sayfası Içeriğini değiştirme

Görünüm ana sayfalarıyla çalışırken neredeyse hemen karşılaştığınız bir sorun, farklı görünüm içerik sayfaları istendiğinde görünüm ana sayfa içeriğini değiştirme sorunudur. Örneğin, Web uygulamanızdaki her sayfanın benzersiz bir başlığa sahip olmasını istiyorsunuz. Ancak, başlık görünüm ana sayfasında belirtilir ve içeriği görüntüleme sayfasında değildir. Bu nedenle, her içerik görüntüleme sayfası için sayfa başlığını nasıl özelleştireceğiniz?

Görünümü içerik sayfası ile görüntülenen başlığı değiştirmek için iki yol vardır. İlk olarak, bir görünüm içeriği sayfasının en üstünde belirtilen `<%@ page %>` yönergesinin title özniteliğine bir sayfa başlığı atayabilirsiniz. Örneğin, "süper harika web sitesi" sayfa başlığını dizin görünümüne atamak istiyorsanız, Dizin görünümünün en üstüne aşağıdaki yönergeyi dahil edebilirsiniz:

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

Dizin görünümü tarayıcıya işlendiğinde, istenen başlık tarayıcı başlık çubuğunda görünür:

[![tarayıcısı başlık çubuğu](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)

Başlık özniteliğinin çalışması için bir ana görünüm sayfasının karşılaması gereken önemli bir gereksinim vardır. Görünüm ana sayfası, üst bilgisi için normal bir `<head>` etiketi yerine bir `<head runat="server">` etiketi içermelidir. `<head>` etiketi runat = "Server" özniteliğini içermiyorsa başlık görünmez. Varsayılan görünüm ana sayfası, gerekli `<head runat="server">` etiketini içerir.

Tek bir görünüm içeriği sayfasından ana sayfa içeriğini değiştirmeye yönelik alternatif bir yaklaşım, değiştirmek istediğiniz bölgeyi `<asp:ContentPlaceHolder>` etiketinde sarmalıdır. Örneğin, yalnızca başlığı değil, bir ana görünüm sayfası tarafından oluşturulan meta etiketlerini de değiştirmek istediğinizi düşünün. Liste 4 ' teki ana görünüm sayfası, `<head>` etiketi içinde bir `<asp:ContentPlaceHolder>` etiketi içerir.

**Listeleme 4 – `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

Liste 4 ' teki `<asp:ContentPlaceHolder>` etiketinin varsayılan içeriği içerdiğine dikkat edin: varsayılan bir başlık ve varsayılan meta etiketler. Tek bir görünüm içeriği sayfasında bu `<asp:ContentPlaceHolder>` etiketini geçersiz kılamazsanız, varsayılan içerik görüntülenir.

Listeleme 5 ' teki içerik görünümü sayfası, özel bir başlık ve özel meta etiketler görüntülemek için `<asp:ContentPlaceHolder>` etiketini geçersiz kılar.

**Listeleme 5 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a>Özet

Bu öğreticide, ana sayfaları görüntüleme ve içerik sayfalarını görüntüleme konusunda temel bir giriş sunulmaktadır. Yeni görünüm ana sayfaları oluşturmayı ve bunlara göre içerik sayfaları oluşturmayı öğrendiniz. Ayrıca, belirli bir görünüm içeriği sayfasından bir görünüm ana sayfasının içeriğini nasıl değiştirebileceğiniz de incelendik.

> [!div class="step-by-step"]
> [Önceki](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [İleri](passing-data-to-view-master-pages-cs.md)
