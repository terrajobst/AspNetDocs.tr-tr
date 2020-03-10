---
uid: visual-studio/overview/2013/using-browser-link
title: Visual Studio 2013 'de tarayıcı bağlantısı kullanılıyor | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622908"
---
# <a name="using-browser-link-in-visual-studio-2013"></a>Visual Studio 2013 'de tarayıcı bağlantısı kullanma

, [Mike te son](https://github.com/MikeWasson)

Tarayıcı bağlantısı, geliştirme ortamı ile bir veya daha fazla Web tarayıcısı arasında bir iletişim kanalı oluşturan Visual Studio 2013 yeni bir özelliktir. Tarayıcı bağlantısını, Web uygulamanızı birden çok tarayıcıda tek seferde yenilemek için kullanabilirsiniz. Bu, tarayıcılar arası testler için kullanışlıdır.

- [Tarayıcı yenileme](#browser-refresh)
- [Tarayıcı bağlantısı panosunu görüntüleme](#dashboard)
- [Statik HTML dosyaları için tarayıcı bağlantısını etkinleştirme](#static-html)
- [Tarayıcı bağlantısı devre dışı bırakılıyor](#disabling)
- [Nasıl çalışır?](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>Tarayıcı yenileme

Tarayıcı yenileme ile, tarayıcı bağlantısı aracılığıyla Visual Studio 'ya bağlı birden çok tarayıcıyı yenileyebilirsiniz.

Tarayıcı yenilemeyi kullanmak için, önce proje şablonlarından birini kullanarak bir ASP.NET uygulaması oluşturun. F5 tuşuna basarak veya araç çubuğundaki ok simgesine tıklayarak uygulamada hata ayıklayın:

![](using-browser-link/_static/image1.png)

Ayrıca, hata ayıklama için belirli bir tarayıcı seçmek üzere açılan menüyü de kullanabilirsiniz.

![](using-browser-link/_static/image2.png)

Birden çok tarayıcıyla hata ayıklamak için, **Ile araştır**' ı seçin. **Ile araştır** iletişim kutusunda, birden fazla tarayıcı seçmek için CTRL tuşunu basılı tutun. Seçili tarayıcılarla hata ayıklamak için, **Gözden** geçirme ' ye tıklayın. Tarayıcı bağlantısı, Visual Studio dışında bir tarayıcı başlattığınızda ve uygulama URL 'sine gittiğinizde da geçerlidir.

![](using-browser-link/_static/image3.png)

Tarayıcı bağlantı denetimleri, dairesel ok simgesiyle açılan listede bulunur. Ok simgesi **Yenile** düğmesidir.

![](using-browser-link/_static/image4.png)

Hangi tarayıcıların bağlı olduğunu görmek için, hata ayıklama sırasında fareyi **Yenile** düğmesinin üzerine getirin. Bağlı tarayıcılar bir araç Ipucu penceresinde gösterilir.

![](using-browser-link/_static/image5.png)

Bağlı tarayıcıları yenilemek için **Yenile** düğmesine tıklayın veya CTRL + ALT + ENTER tuşlarına basın. Örneğin, aşağıdaki ekran görüntüsünde MVC 5 proje şablonunu kullanarak oluşturduğum bir ASP.NET projesi gösterilmektedir. En üstte iki tarayıcıda çalışan uygulamayı görebilirsiniz. En altta, proje Visual Studio 'da açıktır.

![](using-browser-link/_static/image6.png)

Visual Studio 'da ana sayfa için &lt;H1&gt; başlığını değiştirdim:

![](using-browser-link/_static/image7.png)

**Yenile** düğmesine tıkladığımda değişiklik her iki tarayıcı penceresinde de görünüyor:

![](using-browser-link/_static/image8.png)

**Notlar**

- Tarayıcı bağlantısını etkinleştirmek için, projenin Web. config dosyasındaki [&lt;derleme&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) öğesinde `debug=true` ayarlayın.
- Uygulamanın localhost üzerinde çalışıyor olması gerekir.
- Uygulamanın .NET 4,0 veya üstünü hedeflemesi gerekir.

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>Tarayıcı bağlantısı panosunu görüntüleme

Tarayıcı bağlantısı panosu, tarayıcı bağlantısı bağlantıları hakkında bilgi gösterir. Panoyu görüntülemek için tarayıcı bağlantısı açılan menüsünü seçin ( **Yenile** düğmesinin yanındaki küçük ok). Ardından **tarayıcı bağlantısı panosu**' na tıklayın.

![](using-browser-link/_static/image9.png)

Pano, bağlı tarayıcıları ve her tarayıcının gezindiği URL 'YI listeler.

![](using-browser-link/_static/image10.png)

**Önkoşullar** bölümünde, bu proje Için tarayıcı bağlantısını etkinleştirmek üzere gereken adımlar gösterilir. Örneğin, aşağıdaki ekran görüntüsünde, Web. config dosyasında "Debug" false olarak ayarlanmış bir proje gösterilmektedir.

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>Statik HTML dosyaları için tarayıcı bağlantısını etkinleştirme

Statik HTML dosyaları için tarayıcı bağlantısını etkinleştirmek üzere, Web. config dosyanıza aşağıdakileri ekleyin.

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

Performans nedenleriyle, projenizi yayımladığınızda bu ayarı kaldırın.

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>Tarayıcı bağlantısı devre dışı bırakılıyor

Tarayıcı bağlantısı varsayılan olarak etkindir. Devre dışı bırakmak için birkaç yol vardır:

- Tarayıcı bağlantısı açılan menüsünde, **tarayıcı bağlantısını etkinleştir**onay kutusunun işaretini kaldırın. 

    ![](using-browser-link/_static/image12.png)
- Web. config dosyasında, appSettings bölümüne "vs: EnableBrowserLink" adlı bir anahtarı "false" değeri ile ekleyin. 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- Web. config dosyasında, hata ayıkla ' yı false olarak ayarlayın. 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>Nasıl çalışır?

Tarayıcı bağlantısı, Visual Studio ile tarayıcı arasında bir iletişim kanalı oluşturmak için [SignalR](../../../signalr/index.md) kullanır. Tarayıcı bağlantısı etkinleştirildiğinde, Visual Studio birden çok istemcinin (tarayıcının) bağlanabileceği bir SignalR sunucusu işlevi görür. Tarayıcı bağlantısı, ASP.NET ile bir HTTP modülünü de kaydeder. Bu modül, sunucudan her sayfa isteğine özel &lt;betiği&gt; başvurularını çıkarır. Tarayıcıda "kaynağı görüntüle" seçeneğini belirleyerek betik başvurularını görebilirsiniz.

![](using-browser-link/_static/image13.png)

Kaynak dosyalarınız değiştirilmez. HTTP modülü betik başvurularını dinamik olarak çıkarır.

Tarayıcı tarafı kodu tüm JavaScript olduğundan, herhangi bir tarayıcı eklentisi gerekmeden, [SignalR 'nin desteklediği](../../../signalr/overview/getting-started/supported-platforms.md)tüm tarayıcılarda çalışıyor olur.
