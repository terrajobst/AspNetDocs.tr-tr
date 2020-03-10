---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6\. Bölüm: model doğrulaması için veri ek açıklamalarını kullanma | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 6\. bölüm, model V için veri ek açıklamalarını kullanmayı içerir...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539279"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a>6\. Bölüm: Model Doğrulama için Veri Ek Açıklamalarını Kullanma

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 6\. bölüm, model doğrulaması için veri ek açıklamalarını kullanmayı içerir.

Oluşturma ve düzenleme formlarımızla ilgili önemli bir sorun var: herhangi bir doğrulama yapmadık. Gerekli alanları boş bırakma veya fiyat alanında harfler yazma gibi işlemleri yapabiliriz ve göreceğiniz ilk hata veritabanından.

Model sınıflarımıza veri ek açıklamaları ekleyerek uygulamamıza kolayca doğrulama ekleyebiliriz. Veri ek açıklamaları, model özelliklerine uygulanmasını istediğimiz kuralları açıklamanıza olanak sağlar ve ASP.NET MVC bunları zorlamaya ve kullanıcılarımıza uygun iletileri görüntülemeye yönelik bir işlem gerçekleştirir.

## <a name="adding-validation-to-our-album-forms"></a>Albüm formlarımıza doğrulama ekleme

Aşağıdaki veri ek açıklaması özniteliklerini kullanacağız:

- **Gerekli** – özelliğin gerekli bir alan olduğunu belirtir
- **DisplayName** : form alanlarında ve doğrulama iletilerinde kullanmak istediğimiz metni tanımlar
- **StringLength** : bir dize alanı için en fazla uzunluğu tanımlar
- **Range** : sayısal bir alan için en yüksek ve en küçük değeri verir
- **Bind** : parametre veya form değerlerini model özelliklerine bağlamada hariç tutulacak veya dahil edilecek alanları listeler
- **ScaffoldColumn** – alanları düzenleyici formlarından gizlemeyi sağlar

*Not: veri ek açıklaması özniteliklerini kullanarak model doğrulama hakkında daha fazla bilgi için`https://go.microsoft.com/fwlink/?LinkId=159063`ADRESINDEKI MSDN belgelerine bakın.* [ ](https://go.microsoft.com/fwlink/?LinkId=159063)

Albüm sınıfını açın ve aşağıdaki *using* deyimlerini en üste ekleyin.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

Ardından, aşağıda gösterildiği gibi, görüntüleme ve doğrulama öznitelikleri eklemek için özellikleri güncelleştirin.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

Biz de var olsa da, tarzı ve sanatçıya sanal özelliklere de değiştirdik. Bu, Entity Framework gerektiği gibi yavaş yüklenmesine izin verir.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

Bu öznitelikleri albüm modelimize ekledikten sonra, oluşturma ve düzenleme ekranımız alanları doğrulamaya başlar ve seçtiğiniz görünen adları (örn. albümle değil, albüm sanat URL 'Si) kullanın. Uygulamayı çalıştırın ve/Storemanager/createadresine gidin.

![](mvc-music-store-part-6/_static/image1.png)

Daha sonra bazı doğrulama kurallarını bozacağız. 0 ' ın bir fiyatını girin ve başlığı boş bırakın. Oluştur düğmesine tıkladığımızda, tanımlamış olduğumuz doğrulama kurallarına uymayan alanları gösteren doğrulama hata iletileriyle birlikte görüntülenecek formu görüyoruz.

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>Istemci tarafı doğrulamayı test etme

Sunucu tarafı doğrulaması bir uygulama perspektifinden çok önemlidir, çünkü kullanıcılar istemci tarafı doğrulamayı atlayabilirler. Ancak, yalnızca sunucu tarafı doğrulama uygulayan Web sayfası formları üç önemli sorun sergiler.

1. Kullanıcının, formun gönderilmesini, sunucuda doğrulanmasını ve yanıtın tarayıcıya gönderilmesi için beklemesi gerekir.
2. Kullanıcı artık doğrulama kurallarını geçirmeden bir alanı düzelttiklerinde anında geri bildirim almaz.
3. Sunucu kaynaklarını kullanıcının tarayıcısına göre değil, doğrulama mantığını gerçekleştirecek şekilde harcadık.

Neyse ki, ASP.NET MVC 3 iskele şablonlarının içinde yerleşik olarak bulunan ve başka hiçbir iş gerektirmeyen istemci tarafı doğrulaması vardır.

Başlık alanına tek bir harf yazmak doğrulama gereksinimlerini karşılar, bu nedenle doğrulama iletisi hemen kaldırılır.

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-5.md)
> [İleri](mvc-music-store-part-7.md)
