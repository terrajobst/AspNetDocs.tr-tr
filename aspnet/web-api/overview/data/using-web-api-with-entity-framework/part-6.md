---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript Istemcisini oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622348"
---
# <a name="create-the-javascript-client"></a>JavaScript İstemcisini Oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, HTML, JavaScript ve [altını gizleme. js](http://knockoutjs.com/) kitaplığı kullanarak uygulama için istemcisini oluşturacaksınız. İstemci uygulamasını aşamalar halinde oluşturacağız:

- Kitap listesi gösteriliyor.
- Bir kitap ayrıntısı gösteriliyor.
- Yeni kitap ekleniyor.

Altını gizleme kitaplığı Model-View-ViewModel (MVVM) modelini kullanır:

- **Model** , iş etki alanındaki verilerin sunucu tarafı gösterimidir (bizim örneğimizde, kitaplarımızda ve yazarlarımız).
- **Görünüm** sunum katmanıdır (HTML).
- **Görünüm modeli** , modelleri tutan bir JavaScript nesnesidir. Görünüm modeli, Kullanıcı arabiriminin kod soyutlamasıdır. HTML temsili bilgisine sahip değildir. Bunun yerine, görünümün Özet özelliklerini temsil eder, örneğin kitap&quot;listesini &quot;.

Görünüm, görünüm modeline veri ile bağlanır. Görünüm modeli güncelleştirmeleri otomatik olarak görünüme yansıtılır. Görünüm modeli, düğme tıklamaları gibi görünümden de olayları alır.

![](part-6/_static/image1.png)

Bu yaklaşım, herhangi bir kodu yeniden yazmadan bağlamaları değiştirebildiğinden uygulamanızın düzen ve Kullanıcı arabirimini değiştirmeyi kolaylaştırır. Örneğin, öğelerin bir listesini `<ul>`olarak gösterip daha sonra bir tablo olarak değiştirebilirsiniz.

## <a name="add-the-knockout-library"></a>Altını gizleme kitaplığını ekleme

Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni seçin. Ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](part-6/samples/sample1.cmd)]

Bu komut, altını gizleme dosyalarını betikler klasörüne ekler.

## <a name="create-the-view-model"></a>Görünüm modeli oluşturma

Scripts klasörüne App. js adlı bir JavaScript dosyası ekleyin. (Çözüm Gezgini, betikler klasörüne sağ tıklayın, **Ekle**' yi ve ardından **JavaScript dosyası**' nı seçin.) Aşağıdaki kodu yapıştırın:

[!code-javascript[Main](part-6/samples/sample2.js)]

Altını gizleme bölümünde, `observable` sınıfı veri bağlamayı mümkün bir şekilde sunar. Bir observable 'ın içeriği değiştiğinde, observable her türlü veri bağlantılı denetimi kendileri tarafından güncelleştirebilecekleri şekilde bilgilendirir. (`observableArray` sınıfı, *observable*'ın dizi sürümüdür.) İle başlamak için, görünüm modelimizin iki gözlemlenenler vardır:

- `books`, kitap listesini tutar.
- `error` bir AJAX çağrısı başarısız olursa bir hata iletisi içerir.

`getAllBooks` yöntemi, kitap listesini almak için bir AJAX çağrısı yapar. Sonra, sonucu `books` dizisine iter.

`ko.applyBindings` yöntemi, altını gizleme kitaplığının bir parçasıdır. Görünüm modelini bir parametre olarak alır ve veri bağlamayı ayarlar.

## <a name="add-a-script-bundle"></a>Betik paketi ekleme

Paketleme, ASP.NET 4,5 ' de birden çok dosyayı tek bir dosyada birleştirmeyi veya paketlemeyi kolaylaştıran bir özelliktir. Paketleme, sunucuya yapılan istek sayısını azaltır ve bu da sayfa yükleme süresini iyileştirebilirler.

Start/paketleme Liconfig. cs\_dosya uygulamasını açın. Aşağıdaki kodu Registerdemeti yöntemine ekleyin.

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [Önceki](part-5.md)
> [İleri](part-7.md)
