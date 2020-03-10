---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: Denetleyici ekleme | Microsoft Docs
author: shanselman
description: Bu öğreticiyi Visual Studio 2013 kullanarak burada kullanılabilirse, güncelleştirilmiş bir sürüm. Yeni öğretici, t üzerinde birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır...
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543983"
---
# <a name="adding-a-controller"></a>Denetleyici Ekleme

[Scott Hanselman](https://github.com/shanselman) tarafından

> > [!NOTE]
> > Bu öğreticiyi [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)kullanarak [burada](../../getting-started/introduction/getting-started.md) kullanılabilirse, güncelleştirilmiş bir sürüm. Yeni öğretici, bu öğreticide birçok geliştirme sağlayan ASP.NET MVC 5 ' i kullanır.
>
>
> Bu, ASP.NET MVC 'nin temellerini tanıtan bir başlangıç öğreticisidir. Bir veritabanından okuyan ve yazan basit bir Web uygulaması oluşturacaksınız. Diğer ASP.NET MVC öğreticileri ve örneklerini bulmak için [ASP.NET MVC öğrenme merkezini](../../../index.md) ziyaret edin.

MVC model, görünüm, denetleyici için temsil eder. MVC, her parçanın diğerinden farklı bir sorumluluğu olması gibi uygulamalar geliştirmeye yönelik bir modeldir.

- Model: uygulamanızın verileri
- Görünümler: uygulamanızın, dinamik olarak HTML yanıtları oluşturmak için kullanacağı şablon dosyaları.
- Denetleyiciler: uygulamaya gelen URL isteklerini işleyen sınıflar, model verilerini alır ve ardından istemciye bir yanıt işleyen görünüm şablonlarını belirtir

Bu öğreticide bu kavramların tümünü ele alacağız ve bir uygulama oluşturmak için bunları nasıl kullanacağınızı göstereceğiz.

Çözüm Gezgini ' nde denetleyiciler klasörüne sağ tıklayıp denetleyici Ekle ' yi seçerek yeni bir denetleyici oluşturalım.

[![Addcontrollerbir tıklatma](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

Yeni denetleyicinizi "Merhaba Dünya denetleyicisi" olarak adlandırın ve Ekle ' ye tıklayın.

[![denetleyicisi Ekle Iletişim kutusu](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

Sağdaki Çözüm Gezgini, HelloWorldController.cs adlı ve bu dosya artık **IDE**'de açılan bir yeni dosya oluşturulduğunu fark edin.

[Merhaba Dünya Controllercode ![](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

Yeni genel sınıfınızın Merhaba Dünya denetleyicinizin içinde olduğu gibi iki yeni yöntem oluşturun. Bir örnek olarak denetleyicimizin doğrudan bir HTML dizesini döneceğiz.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

Denetleyicinizde HelloWorldController adı verilir ve yeni yönteminiz dizin olarak adlandırılır. Uygulamanızı daha önce olduğu gibi yeniden çalıştırın (yürütme düğmesine tıklayın veya F5 tuşuna basarak bunu yapın). Tarayıcınız başladıktan sonra adres çubuğundaki yolu, xx ' in bilgisayarınızın seçtiği sayı olduğu `http://localhost:xx/HelloWorld` olarak değiştirin. Artık tarayıcınız aşağıdaki ekran görüntüsüne benzer şekilde görünmelidir. Yukarıdaki yöntemde, "Içerik" adlı bir yönteme geçirilen bir dize döndürüldü. Sisteme yalnızca birkaç HTML döndüğünü söyliyoruz ve!

ASP.NET MVC, gelen URL 'ye bağlı olarak farklı denetleyici sınıflarını (ve bunların içinde farklı eylem yöntemlerini) çağırır. ASP.NET MVC tarafından kullanılan varsayılan eşleme mantığı, hangi kodun çalıştırılacağını denetlemek için şöyle bir biçim kullanır:

/[Controller]/[ActionName]/[parametreler]

URL 'nin ilk bölümü yürütülecek denetleyici sınıfını belirler. Bu nedenle/HelloWorld, Merhaba Dünya denetleyicisi sınıfıyla eşlenir. URL 'nin ikinci bölümü, yürütülecek sınıftaki Action metodunu belirler. Bu nedenle/HelloWorld/Index, HelloWorldController sınıfının Index () yönteminin yürütülmesine neden olur. Yukarıda yalnızca/HelloWorld ' i ziyaret ettiğimiz ve Yöntem dizininin kullanılmış olduğuna dikkat edin. Bunun nedeni, "Index" adlı bir yöntemin, açıkça belirtilmemişse bir denetleyicide çağrılacak varsayılan yöntemdir.

[Bu, varsayılan eylemm ![](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

Şimdi, şimdi de hoş geldiniz Yöntetimiz `http://localhost:xx/HelloWorld/Welcome.` ve kendi HTML dizesini döndürdüğünden şimdi ziyaret edelim.

Yeniden,/[Controller]/[ActionName]/[Parameters] Bu nedenle Controller, bu durumda bir. Henüz parametre yapmadık.

[![, hoş geldiniz eylemi yöntemidir](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

URL 'den denetleyicimize bazı bilgiler geçirebilmemiz için bizim örneğimizi biraz daha değiştirelim. Örneğin, şu şekilde:/HelloWorld/Welcome? Name = Scott&amp;numtimes = 4. Welcome yönteminizi iki parametre içerecek şekilde değiştirin ve aşağıdaki gibi güncelleştirin. Parametresiz parametre özelliğini, parametre geçirilmemişse, numTimes parametresinin varsayılan değer olan 1 ' i belirtmesi gerektiğini gösterecek şekilde kullandığımızda C# aklınızda olduğunu unutmayın.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

Uygulamanızı çalıştırın ve ad ve numtimes değerlerini istediğiniz şekilde değiştirerek `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` ziyaret edin. Sistem, adres çubuğundaki sorgu dizinizdeki adlandırılmış parametreleri yöntemdeki parametrelere otomatik olarak eşlendi.

Her iki örnekte de denetleyici tüm işleri yapıyor ve doğrudan HTML döndürüyor. Normalde, Denetleyicilerimizin doğrudan HTML döndürmesini istiyoruz. Bu, kod için çok daha fazla. Bunun yerine, genellikle HTML yanıtı oluşturmaya yardımcı olmak için ayrı bir görünüm şablonu dosyası kullanacağız. Bu, bunu nasıl yapabiliriz bakalım. Tarayıcınızı kapatın ve IDE 'ye dönün.

> [!div class="step-by-step"]
> [Önceki](getting-started-with-mvc-part1.md)
> [İleri](getting-started-with-mvc-part3.md)
