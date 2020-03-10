---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: 'Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 3. Bölüm: sıralama ve filtreleme | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, Entity Framework 4,0 öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 603120864528b9a5ff81214270eb9a7f1b68b347
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631672"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a>Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 3. Bölüm: sıralama ve filtreleme

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu öğretici serisi, [Entity Framework 4,0 öğretici serisi Ile çalışmaya](https://asp.net/entity-framework/tutorials#Getting%20Started) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) . Öğreticiler hakkında sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx)gönderebilirsiniz.

Önceki öğreticide, Entity Framework ve `ObjectDataSource` denetimini kullanan n katmanlı bir Web uygulamasına depo modelini uyguladık. Bu öğreticide, sıralama ve filtreleme ve ana ayrıntı senaryolarını işleme işlemlerinin nasıl yapılacağı gösterilmektedir. Aşağıdaki geliştirmeleri *Departmanlar. aspx* sayfasına ekleyeceksiniz:

- Kullanıcıların departmanları ada göre seçmesine izin veren bir metin kutusu.
- Kılavuzda gösterilen her departman için kurslar listesi.
- Sütun başlıklarına tıklayarak sıralama özelliği.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)

## <a name="adding-the-ability-to-sort-gridview-columns"></a>GridView sütunlarını sıralama özelliği ekleme

*Departmanlar. aspx* sayfasını açın ve `DepartmentsObjectDataSource`adlı `ObjectDataSource` denetimine bir `SortParameterName="sortExpression"` özniteliği ekleyin. (Daha sonra, `sortExpression`adlı bir parametre alan `GetDepartments` yöntemi oluşturacaksınız.) Denetimin açılış etiketiyle ilgili biçimlendirme şimdi aşağıdaki örneğe benzer.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

`GridView` denetiminin açılış etiketine `AllowSorting="true"` özniteliğini ekleyin. Denetimin açılış etiketiyle ilgili biçimlendirme şimdi aşağıdaki örneğe benzer.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

*Departments.aspx.cs*' de, `Page_Load` yönteminden `GridView` denetiminin `Sort` yöntemini çağırarak varsayılan sıralama düzenini ayarlayın:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

İş mantığı sınıfında veya depo sınıfında sıralama ya da filtre uygulayan bir kod ekleyebilirsiniz. İş mantığı sınıfında bunu yaparsanız sıralama veya filtreleme işi, veri veritabanından alındıktan sonra yapılır, çünkü iş mantığı sınıfı depo tarafından döndürülen bir `IEnumerable` nesnesiyle çalışır. Depo sınıfına sıralama ve filtreleme kodu ekler ve bunu bir LINQ ifadesi veya nesne sorgusu `IEnumerable` nesnesine dönüştürüldükten sonra yaparsanız, komutlarınız işlenmek üzere veritabanına geçirilir, bu da genellikle daha etkilidir. Bu öğreticide, sıralama ve filtrelemeyi, işleme veritabanı tarafından (yani depodaki) yapılmasına neden olacak şekilde uygulayacaksınız.

Sıralama yeteneği eklemek için depo arabirimine ve depo sınıflarına ek olarak, iş mantığı sınıfına yeni bir yöntem eklemeniz gerekir. *ISchoolRepository.cs* dosyasında, döndürülen departmanlar listesini sıralamak için kullanılacak bir `sortExpression` parametresi alan yeni bir `GetDepartments` yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

`sortExpression` parametresi, sıralanacak sütunu ve sıralama yönünü belirler.

Yeni yöntemin kodunu *SchoolRepository.cs* dosyasına ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

Yeni yöntemi çağırmak için mevcut parametresiz `GetDepartments` yöntemini değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

Test projesinde, *MockSchoolRepository.cs*öğesine aşağıdaki yeni yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

Bu yönteme bağımlı olan herhangi bir birim testini, sıralanmış bir liste döndüleyecekseniz, listeyi döndürmeden önce sıralamalısınız. Bu öğreticide olduğu gibi test oluşturmayacağız, bu nedenle yöntem yalnızca sıralanmamış departmanlar listesini döndürebilir.

*SchoolBL.cs* dosyasında, iş mantığı sınıfına aşağıdaki yeni yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

Bu kod, sıralama parametresini depo yöntemine geçirir.

*Departmanlar. aspx* sayfasını çalıştırın.

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)

Artık herhangi bir sütun başlığına tıklayarak bu sütuna göre sıralama yapabilirsiniz. Sütun zaten sırlanmışsa, başlığa tıklamak sıralama yönünü tersine çevirir.

## <a name="adding-a-search-box"></a>Arama kutusu ekleme

Bu bölümde, bir arama metin kutusu ekleyecek, bir denetim parametresi kullanarak `ObjectDataSource` denetimine bağlayacaksınız ve Filtrelemeyi desteklemek için iş mantığı sınıfına bir yöntem ekleyeceğiz.

*Departmanlar. aspx* sayfasını açın ve başlık ve ilk `ObjectDataSource` denetimi arasına aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

`DepartmentsObjectDataSource`adlı `ObjectDataSource` denetiminde şunları yapın:

- `SearchTextBox` denetiminde girilen değeri alan `nameSearchString` adlı bir parametre için `SelectParameters` öğesi ekleyin.
- `SelectMethod` öznitelik değerini `GetDepartmentsByName`olarak değiştirin. (Bu yöntemi daha sonra oluşturacaksınız.)

`ObjectDataSource` denetimine yönelik biçimlendirme artık aşağıdaki örneğe benzer:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

*ISchoolRepository.cs*' de, hem `sortExpression` hem de `nameSearchString` parametrelerini alan bir `GetDepartmentsByName` yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

*SchoolRepository.cs*' de aşağıdaki yeni yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

Bu kod, arama dizesini içeren öğeleri seçmek için bir `Where` yöntemi kullanır. Arama dizesi boşsa, tüm kayıtlar seçilir. Yöntem çağrılarını bunun gibi bir bildirimde belirttiğinizde (`Include`, sonra `OrderBy`, sonra da `Where`), `Where` yönteminin her zaman en son olması gerektiğini unutmayın.

Yeni yöntemi çağırmak için bir `sortExpression` parametresi alan mevcut `GetDepartments` yöntemini değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

Test projesindeki *MockSchoolRepository.cs* içinde aşağıdaki yeni yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

*SchoolBL.cs*' de aşağıdaki yeni yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

*Departmanlar. aspx* sayfasını çalıştırın ve seçim mantığının çalıştığından emin olmak için bir arama dizesi girin. Metin kutusunu boş bırakın ve tüm kayıtların döndürüldüğünden emin olmak için bir arama deneyin.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)

## <a name="adding-a-details-column-for-each-grid-row"></a>Her kılavuz satırı için ayrıntı sütunu ekleme

Ardından, kılavuzun sağ hücresinde görünen her bir departmanın tüm kurslarını görmek istersiniz. Bunu yapmak için, iç içe geçmiş bir `GridView` denetimini kullanacaksınız ve `Department` varlığının `Courses` gezinti özelliğinden verileri veri yoluyla vereceksiniz.

*Departmanlar. aspx* ' i açın ve `GridView` denetimi için biçimlendirme içinde `RowDataBound` olayı için bir işleyici belirtin. Denetimin açılış etiketiyle ilgili biçimlendirme şimdi aşağıdaki örneğe benzer.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

`Administrator` şablonu alanından sonra yeni bir `TemplateField` öğesi ekleyin:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

Bu biçimlendirme bir kurs listesinin kurs numarasını ve başlığını gösteren bir iç içe `GridView` denetimi oluşturur. `RowDataBound` işleyicisinde kodda bir veri kaynağı oluşturacağından bir veri kaynağı belirtmez.

*Departments.aspx.cs* ' i açın ve `RowDataBound` olayı için aşağıdaki işleyiciyi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

Bu kod, olay bağımsız değişkenlerinden `Department` varlığını alır, `Courses` gezinti özelliğini bir `List` koleksiyonuna dönüştürür ve iç içe `GridView` koleksiyona databinds.

*SchoolRepository.cs* dosyasını açın ve `GetDepartmentsByName` yönteminde oluşturduğunuz nesne sorgusunda `Include` yöntemini çağırarak `Courses` gezinti özelliği için Eager yükleme belirtin. `GetDepartmentsByName` yöntemindeki `return` deyimleri artık aşağıdaki örneğe benzer.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

Sayfayı çalıştırın. Daha önce eklediğiniz sıralama ve filtreleme özelliğine ek olarak, GridView denetimi artık her departman için iç içe geçmiş kurs ayrıntılarını gösterir.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)

Bu, sıralamaya, filtrelemeye ve ana ayrıntı senaryolarına giriş işlemini tamamlar. Sonraki öğreticide eşzamanlılık işleme yöntemini göreceksiniz.

> [!div class="step-by-step"]
> [Önceki](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [İleri](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
