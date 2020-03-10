---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: Varlık Ilişkilerini işleme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557465"
---
# <a name="handling-entity-relations"></a>Varlık İlişkilerini İşleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, EF 'in ilgili varlıkları nasıl yüklediği ve model sınıflarınızda dairesel gezinti özelliklerinin nasıl işleneceği hakkında bazı ayrıntılar açıklanmaktadır. (Bu bölüm, arka plan bilgisi sağlar ve öğreticiyi tamamlaması için gerekli değildir. İsterseniz [Bölüm 5](part-5.md)' e atlayın..)

## <a name="eager-loading-versus-lazy-loading"></a>Ekip yükleme ve geç yükleme karşılaştırması

Bir ilişkisel veritabanıyla EF kullanırken, EF 'in ilgili verileri nasıl yüklediğini anlamak önemlidir.

Ayrıca, EF 'in oluşturduğu SQL sorgularını görmek de yararlı olur. SQL 'i izlemek için aşağıdaki kod satırını `BookServiceContext` oluşturucusuna ekleyin:

[!code-csharp[Main](part-4/samples/sample1.cs)]

/Api/Books 'a bir GET isteği gönderirseniz, aşağıdaki gibi JSON döndürür:

[!code-console[Main](part-4/samples/sample2.cmd)]

Kitap geçerli bir AuthorId içeriyor olsa da, Author özelliğinin null olduğunu görebilirsiniz. Bunun nedeni, EF 'in ilgili yazar varlıklarını yüklememalarıdır. SQL sorgusunun izleme günlüğü şunları doğrular:

[!code-console[Main](part-4/samples/sample3.sql)]

SELECT deyimleri kitaplar tablosundan geçer ve yazar tablosuna başvurmuyor.

Başvuru için, kitap listesini döndüren `BooksController` sınıfında yöntemi aşağıda verilmiştir.

[!code-csharp[Main](part-4/samples/sample4.cs)]

Ayrıca, JSON verilerinin bir parçası olarak yazarın nasıl dönediğimiz hakkında bilgi vereceğiz. Entity Framework içinde ilgili verileri yüklemek için üç yol vardır: Eager yükleme, geç yükleme ve açık yükleme. Her teknikle ilgili denge vardır. bu nedenle, nasıl çalıştığını anlamak önemlidir.

### <a name="eager-loading"></a>Ekip yükleme

Bu *yüklemede*, EF ile ilgili varlıkları ilk veritabanı sorgusunun bir parçası olarak yükler. Eager yükleme işlemini gerçekleştirmek için **System. Data. Entity. Include** genişletme yöntemini kullanın.

[!code-csharp[Main](part-4/samples/sample5.cs)]

Bu, sorguya yazar verilerini ekleme hakkında söyleme söyler. Bu değişikliği yapar ve uygulamayı çalıştırırsanız, şu anda JSON verileri şöyle görünür:

[!code-console[Main](part-4/samples/sample6.cmd)]

İzleme günlüğünde, EF 'in kitap ve yazar tablolarında bir JOIN gerçekleştirdiği gösterilmektedir.

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>Geç yükleme

Yavaş yükleme ile ilgili varlık için gezinti özelliği başvurulduğunu EF, ilgili bir varlığı otomatik olarak yükler. Yavaş yüklemeyi etkinleştirmek için, gezinti özelliğini sanal yapın. Örneğin, Book sınıfında:

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

Şimdi aşağıdaki kodu göz önünde bulundurun:

[!code-csharp[Main](part-4/samples/sample9.cs)]

Yavaş yükleme etkinleştirildiğinde, `books[0]` `Author` özelliğine erişmek, yazma için veritabanını sorgulamak için EF 'e neden olur.

EF, her ilgili varlığı aldığında bir sorgu gönderdiğinden, yavaş yükleme birden çok veritabanı gezilerini gerektirir. Genellikle, seri hale getirmek istediğiniz nesneler için yavaş yüklemeyi devre dışı istersiniz. Seri hale getirici modeldeki tüm özellikleri okumalı ve bu da ilgili varlıkları yüklemeyi tetikler. Örneğin, yavaş yükleme özelliği etkin olan kitaplar listesini seri hale geldiğinde SQL sorguları burada açıklanmıştır. EF 'in üç yazar için üç ayrı sorgu yaptığı hakkında bilgi alabilirsiniz.

[!code-console[Main](part-4/samples/sample10.sql)]

Yavaş yükleme kullanmak isteyebileceğiniz zamanlar hala vardır. Eager yüklemesi, EF 'in çok karmaşık bir birleşme oluşturmasına neden olabilir. Ya da verilerin küçük bir alt kümesi için ilgili varlıklara ihtiyacınız olabilir ve yavaş yükleme daha verimli olacaktır.

Serileştirme sorunlarından kaçınmak için bir yol, varlık nesneleri yerine veri aktarımı nesneleri (DTOs) serileştirilmenin bir yoludur. Bu yaklaşımı makalenin ilerleyen kısımlarında göstereceğiz.

### <a name="explicit-loading"></a>Açık yükleme

Açık yükleme, kod içinde ilgili verileri açıkça almanız dışında, yavaş yüklemeye benzer. bir gezinti özelliğine eriştiğinizde otomatik olarak gerçekleşmez. Açık yükleme, ilgili verilerin ne zaman yükleneceği konusunda daha fazla denetim sağlar, ancak ek kod gerektirir. Açık yükleme hakkında daha fazla bilgi için bkz. [Ilgili varlıkları yükleme](https://msdn.microsoft.com/data/jj574232#explicit).

## <a name="navigation-properties-and-circular-references"></a>Gezinti özellikleri ve döngüsel başvurular

Kitap ve yazar modellerini tanımladığımda, kitap yazarı ilişkisinin `Book` sınıfında bir gezinti özelliği tanımlıyorum, ancak başka bir yönde bir gezinti özelliği tanımlıyorum.

Karşılık gelen gezinti özelliğini `Author` sınıfa eklerseniz ne olur?

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

Ne yazık ki, modelleri seri hale alırken bir sorun oluşturur. İlgili verileri yüklerseniz, döngüsel bir nesne grafiği oluşturur.

![](part-4/_static/image1.png)

JSON veya XML biçimlendiricisi grafiği serileştirmek denediğinde, bir özel durum oluşturur. İki biçimlendirme farklı özel durum iletileri oluşturur. JSON biçimlendiricisi için bir örnek aşağıda verilmiştir:

[!code-console[Main](part-4/samples/sample12.cmd)]

XML biçimlendiricisi aşağıda verilmiştir:

[!code-xml[Main](part-4/samples/sample13.xml)]

Bir çözüm, sonraki bölümde tanımlandığım DTOs 'ı kullanmaktır. Alternatif olarak, JSON ve XML formatlarını grafik döngülerini işleyecek şekilde yapılandırabilirsiniz. Daha fazla bilgi için bkz. [Döngüsel nesne başvurularını işleme](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).

Bu öğreticide, `Author.Book` gezinti özelliğine ihtiyacınız yoktur, bu nedenle bırakabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](part-3.md)
> [İleri](part-5.md)
