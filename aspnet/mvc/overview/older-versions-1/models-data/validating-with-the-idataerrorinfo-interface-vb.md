---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: IDataErrorInfo arabirimi ile doğrulama (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther, bir model sınıfında IDataErrorInfo arabirimini uygulayarak özel doğrulama hata iletilerinin nasıl görüntüleneceğini gösterir.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542506"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a>IDataErrorInfo Arabirimi ile Doğrulama (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther, bir model sınıfında IDataErrorInfo arabirimini uygulayarak özel doğrulama hata iletilerinin nasıl görüntüleneceğini gösterir.

Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirmeye yönelik bir yaklaşımı açıklamaktır. Bir kişinin gerekli form alanları için değer sağlamadan bir HTML formu göndermesini nasıl önleyeceğinizi öğrenirsiniz. Bu öğreticide, ıerrordataınfo arabirimini kullanarak doğrulamanın nasıl gerçekleştirileceğini öğreneceksiniz.

## <a name="assumptions"></a>Varsayımlar

Bu öğreticide, MoviesDB veritabanı ve filmler veritabanı tablosunu kullanacağız. Bu tabloda aşağıdaki sütunlar bulunur:

<a id="0.6_table01"></a>

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Başlık | Nvarchar (100) | False |
| Direktörü | Nvarchar (100) | False |
| Davterekiralık | DateTime | False |

Bu öğreticide, veritabanı modeli sınıflarımı oluşturmak için Microsoft Entity Framework kullanıyorum. Entity Framework tarafından üretilen film sınıfı Şekil 1 ' de görüntülenir.

[Film varlığını ![](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)

**Şekil 01**: film varlığı ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))

> [!NOTE] 
> 
> Veritabanı modeli sınıflarınızı oluşturmak için Entity Framework kullanma hakkında daha fazla bilgi edinmek için, Entity Framework ile model sınıfları oluşturma adlı öğreticiye bakın.

## <a name="the-controller-class"></a>Denetleyici sınıfı

Filmleri listelemek ve yeni filmler oluşturmak için giriş denetleyicisini kullanıyoruz. Bu sınıfın kodu, liste 1 ' de yer alır.

**Listeleme 1-Controllers\homecontroller.exe**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

Liste 1 ' deki giriş denetleyicisi sınıfı iki oluşturma () eylemi içerir. İlk eylem, yeni bir filmi oluşturmak için HTML formunu görüntüler. İkinci Create () eylemi, yeni filmin gerçek ekleme işlemini veritabanına uygular. İkinci Create () eylemi, ilk oluşturma () eylemi tarafından görüntülenecek form sunucuya gönderildiğinde çağrılır.

İkinci oluşturma () eyleminin aşağıdaki kod satırlarını içerdiğine dikkat edin:

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

IsValid özelliği bir doğrulama hatası olduğunda false döndürür. Bu durumda, bir filmi oluşturmak için HTML formunu içeren oluştur görünümü yeniden görüntülenir.

## <a name="creating-a-partial-class"></a>Kısmi sınıf oluşturma

Film sınıfı Entity Framework tarafından oluşturulur. Çözüm Gezgini penceresinde MoviesDBModel. edmx dosyasını genişletirseniz ve kod düzenleyicisinde MoviesDBModel. Designer. vb dosyasını açarsanız film sınıfının kodunu görebilirsiniz (bkz. Şekil 2).

[Film varlığı için kodu ![](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)

**Şekil 02**: film varlığının kodu ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))

Film sınıfı, kısmi bir sınıftır. Diğer bir deyişle, film sınıfının işlevlerini genişletmek için aynı ada sahip başka bir kısmi sınıf ekleyebiliriz. Yeni kısmi sınıfa doğrulama mantığımızı ekleyeceğiz.

Liste 2 ' deki sınıfı modeller klasörüne ekleyin.

**Listeleme 2-Models\Movie.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

Kod 2 ' deki sınıfın *kısmi* değiştirici içerdiğine dikkat edin. Bu sınıfa eklediğiniz tüm yöntemler veya özellikler, Entity Framework tarafından oluşturulan film sınıfının bir parçası haline gelir.

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>OnChanging ve OnChanged kısmi yöntemleri ekleme

Entity Framework bir varlık sınıfı oluşturduğunda Entity Framework otomatik olarak sınıfa kısmi Yöntemler ekler. Entity Framework, sınıfın her özelliğine karşılık gelen OnChanging ve OnChanged kısmi yöntemleri oluşturur.

Film sınıfı söz konusu olduğunda Entity Framework aşağıdaki yöntemleri oluşturur:

- Onıdchanging
- Onıdchanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

OnChanging yöntemi, ilgili özellik değiştirilmeden önce hemen çağrılır. OnChanged yöntemi, özellik değiştirildikten hemen sonra çağrılır.

Film sınıfına doğrulama mantığı eklemek için bu kısmi yöntemlerin avantajlarından yararlanabilirsiniz. Listeleme 3 ' teki filmi Güncelleştir sınıfı, başlık ve yönetmen özelliklerinin boş olmayan değerler atandığını doğrular.

> [!NOTE] 
> 
> Kısmi Yöntem, uygulamanız için gerekli olmayan bir sınıfta tanımlanan bir yöntemdir. Kısmi bir yöntem gerçekleştirmezseniz, derleyici yöntem imzasını ve yönteme tüm çağrıları kaldırır, böylece kısmi yöntemle ilişkili bir çalışma zamanı maliyeti yoktur. Visual Studio Code düzenleyicide, *bir kısmı, sonra da* uygulanacak partileri bir listesini görüntülemek için bir boşluk gelen anahtar sözcüğünü yazarak kısmen bir yöntem ekleyebilirsiniz.

**Listeleme 3-Models\Movie.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

Örneğin, title özelliğine boş bir dize atamayı denerseniz, \_hatalar adlı bir sözlüğe bir hata mesajı atanır.

Bu noktada, başlık özelliğine boş bir dize atadığınızda ve özel \_hataları alanına bir hata eklendiğinde hiçbir şey olmaz. Bu doğrulama hatalarını ASP.NET MVC çerçevesine göstermek için IDataErrorInfo arabirimini uygulamamız gerekir.

## <a name="implementing-the-idataerrorinfo-interface"></a>IDataErrorInfo arabirimini uygulama

IDataErrorInfo arabirimi, .NET Framework 'ün ilk sürümden bu yana bir parçasıdır. Bu arabirim çok basit bir arabirimdir:

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

Bir sınıf, IDataErrorInfo arabirimini uyguluyorsa, sınıfın bir örneğini oluştururken ASP.NET MVC çerçevesi bu arabirimi kullanır. Örneğin, giriş denetleyicisi oluşturma () eylemi, film sınıfının bir örneğini kabul eder:

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

ASP.NET MVC Framework, bir model Ciltçi (Defaultmodelciltçi) kullanarak Create () eylemine geçirilen filmin örneğini oluşturur. Model Ciltçi, HTML form alanlarını bir film nesnesinin örneğine bağlayarak film nesnesinin bir örneğini oluşturmaktan sorumludur.

Defaultmodelciltçi, bir sınıfın IDataErrorInfo arabirimini uygulayıp uygulamadığını algılar. Bir sınıf bu arabirimi uyguluyorsa model Bağlayıcısı, sınıfının her özelliği için IDataErrorInfo. bu dizin oluşturucuyu çağırır. Dizin Oluşturucu bir hata iletisi döndürürse, model Ciltçi bu hata iletisini model durumuna otomatik olarak ekler.

Defaultmodelciltçi, IDataErrorInfo. Error özelliğini de denetler. Bu özellik, sınıfla ilişkili, özelliğe özgü olmayan doğrulama hatalarını temsil etmek için tasarlanmıştır. Örneğin, film sınıfının birden çok özelliklerinin değerlerine bağlı olan bir doğrulama kuralını zorlamak isteyebilirsiniz. Bu durumda, hata özelliğinden bir doğrulama hatası döndürürsınız.

Liste 4 ' teki güncelleştirilmiş film sınıfı, IDataErrorInfo arabirimini uygular.

**Listeleme 4-Models\Movie.vb (IDataErrorInfo uygular)**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

4\. listede, Indexer özelliği, dizin oluşturucuya geçirilen özellik adına karşılık gelen bir anahtar içerip içermediğini görmek için \_hataları koleksiyonunu denetler. Özelliği ile ilişkili doğrulama hatası yoksa boş bir dize döndürülür.

Değiştirilen film sınıfını kullanmak için giriş denetleyicisini herhangi bir şekilde değiştirmeniz gerekmez. Şekil 3 ' te görünen sayfa, başlık veya yönetmen formu alanları için hiçbir değer girilmediğinde ne olacağını gösterir.

[eylem yöntemlerini otomatik olarak oluşturma ![](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)

**Şekil 03**: eksik değerlere sahip bir form ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))

Dadlanmış değerin otomatik olarak doğrulanacağını unutmayın. Dadterekiralık özelliği NULL değerleri kabul etmediğinden, Defaultmodelciltçi bir değere sahip olmadığında bu özellik için otomatik olarak bir doğrulama hatası oluşturur. Bu özellik için bir hata iletisi değiştirmek istiyorsanız, özel bir model Bağlayıcısı oluşturmanız gerekir.

## <a name="summary"></a>Özet

Bu öğreticide, IDataErrorInfo arabirimini kullanarak doğrulama hata iletileri oluşturma hakkında bilgi edindiniz. İlk olarak, Entity Framework tarafından oluşturulan kısmi film sınıfının işlevselliğini genişleten kısmi bir film sınıfı oluşturduk. Daha sonra, OnTitleChanging () ve OnDirectorChanging () kısmi yöntemlerine yönelik olarak doğrulama mantığı ekledik. Son olarak, bu doğrulama iletilerini ASP.NET MVC çerçevesine göstermek için IDataErrorInfo arabirimini uyguladık.

> [!div class="step-by-step"]
> [Önceki](performing-simple-validation-vb.md)
> [İleri](validating-with-a-service-layer-vb.md)
