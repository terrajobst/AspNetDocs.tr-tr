---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 Web uygulamasında 4,0 Entity Framework eşzamanlılık işleme | Microsoft Docs
author: tdykstra
description: Bu öğretici serisi, Entity Framework 4,0 öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632589"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 Web uygulamasında 4,0 Entity Framework eşzamanlılık işleme

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu öğretici serisi, [Entity Framework 4,0 öğretici serisi Ile çalışmaya](https://asp.net/entity-framework/tutorials#Getting%20Started) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) . Öğreticiler hakkında sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx)gönderebilirsiniz.

Önceki öğreticide, `ObjectDataSource` denetimini ve Entity Framework kullanarak verileri sıralama ve filtreleme hakkında daha fazla öğrenirsiniz. Bu öğreticide, Entity Framework kullanan bir ASP.NET Web uygulamasında eşzamanlılık işleme seçenekleri gösterilmektedir. Eğitmen Office atamalarını güncelleştirmek için ayrılmış yeni bir Web sayfası oluşturacaksınız. Bu sayfada ve daha önce oluşturduğunuz departmanlar sayfasında eşzamanlılık sorunlarını işleyeceksiniz.

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>Eşzamanlılık Çakışmaları

Bir Kullanıcı bir kaydı düzenlediğinde ve başka bir Kullanıcı, ilk kullanıcının değişikliği veritabanına yazılmadan önce aynı kaydı düzenlediğinde eşzamanlılık çakışması oluşur. Bu tür çakışmaları algılamak için Entity Framework ayarlamazsanız, veritabanını güncelleştirme son olarak diğer kullanıcının değişikliklerinin üzerine yazar. Birçok uygulamada, bu risk kabul edilebilir ve uygulamayı olası eşzamanlılık çakışmalarını işleyecek şekilde yapılandırmanız gerekmez. (Birkaç Kullanıcı veya birkaç güncelleştirme varsa veya bazı değişikliklerin üzerine yazılmaması durumunda gerçekten önemli değilse, eşzamanlılık için programlama ücreti avantaja aykırı olabilir.) Eşzamanlılık çakışmaları konusunda endişelenmenize gerek yoksa, bu öğreticiyi atlayabilirsiniz; serideki kalan iki öğretici, bu sayfada oluşturduğunuz herhangi bir şeye bağlı değildir.

### <a name="pessimistic-concurrency-locking"></a>Kötümser eşzamanlılık (kilitleme)

Uygulamanızın eşzamanlılık senaryolarında yanlışlıkla veri kaybını önlemesi gerekiyorsa, bunu yapmanın bir yolu veritabanı kilitlerini kullanmaktır. Bu, *Kötümser eşzamanlılık*olarak adlandırılır. Örneğin, bir veritabanından bir satırı okuyabilmeniz için, salt okunurdur veya güncelleştirme erişimi için bir kilit isteyin. Bir satırı güncelleştirme erişimi için kilitlerseniz, başka hiçbir kullanıcının satırı değiştirme sürecinde olan verilerin bir kopyasını alması için salt okunurdur veya güncelleştirme erişimi için bu satırı kilitlemesine izin verilmez. Bir satırı salt okuma erişimi için kilitlerseniz, diğerleri dosyayı salt okuma erişimi için de kilitleyip güncelleştirme için de kilitleyebilirler.

Kilitleri yönetmek bazı dezavantajlara sahiptir. Program, karmaşık olabilir. Bu, önemli ölçüde veritabanı yönetim kaynakları gerektirir ve bir uygulamanın kullanıcı sayısı arttıkça performans sorunlarına neden olabilir (yani, düzgün ölçeklenmez). Bu nedenlerden dolayı, tüm veritabanı yönetim sistemleri Kötümser eşzamanlılık 'yi desteklemez. Entity Framework, BT için yerleşik destek sağlamaz ve bu öğretici bunu nasıl uygulayacağınızı göstermez.

### <a name="optimistic-concurrency"></a>İyimser Eşzamanlılık

Kötümser eşzamanlılık yerine *iyimser*eşzamanlılık yapılır. İyimser eşzamanlılık, eşzamanlılık çakışmalarının gerçekleşmesine ve sonra uygun şekilde yeniden davranmasını sağlar. Örneğin John, *Department. aspx* sayfasını çalıştırır, geçmiş departmanı için **düzenleme** bağlantısına tıklar ve $1.000.000,00 olan **Bütçe** tutarını $125.000,00 olarak azaltır. (John rekabet departmanı yönetir ve kendi departmanı için para kazanmak istiyor.)

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

John 'ın **Güncelleştir**' i tıklamasından önce kemal aynı sayfayı çalıştırır, geçmiş departmanı için **düzenleme** bağlantısına tıklar ve sonra **Başlangıç tarihi** alanını 1/10/2011 ' den 1/1/1999 ' e değiştirir. (Gamze geçmiş departmanı yönetir ve daha fazla kıdem sağlamak istiyor.)

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

John önce **Güncelleştir** ' i tıklatır, sonra gamze **Güncelleştir**' i tıklatır. Kemal 'in tarayıcısı artık **Bütçe** tutarını $1.000.000,00 olarak listelemektedir, ancak bu, tutar John 'dan $125.000,00 ' e değiştiği için yanlış.

Bu senaryoda gerçekleştirebileceğiniz eylemlerden bazıları şunlardır:

- Bir kullanıcının hangi özelliği değiştirdiği ve yalnızca ilgili sütunları veritabanında güncelleştirdiğinden haberdar olabilirsiniz. Örnek senaryoda, iki kullanıcı tarafından farklı özellikler güncelleştirildiğinden hiçbir veri kaybolmaz. Bir sonraki sefer, bir Kullanıcı geçmiş departmanına gözattığında, 1/1/1999 ve $125.000,00 ' i görür. 

    Bu, Entity Framework varsayılan davranıştır ve veri kaybına neden olabilecek çakışmaların sayısını önemli ölçüde azaltabilir. Bununla birlikte, bir varlığın aynı özelliğinde rekabet değişiklikleri yapılırsa, bu davranış veri kaybını önetmez. Ayrıca, bu davranış her zaman mümkün değildir; saklı yordamları bir varlık türüne eşlediğinizde, varlıkta herhangi bir değişiklik yapıldığında varlığın tüm özellikleri güncelleştirilir.
- Gamze 'nin değişikliğini John 'ın değişikliğini geçersiz kılabilirsiniz. Gamze **Güncelleştir**' i tıkladıktan sonra, **Bütçe** miktarı $1.000.000,00 ' e geri gider. Bu, *Istemci WINS* veya *son WINS* senaryosu olarak adlandırılır. (İstemci değerleri, veri deposundaki değerlere göre önceliklidir.)
- Gamze 'nin değişikliğini veritabanında güncelleştirilmesini engelleyebilirsiniz. Genellikle, bir hata iletisi görüntüler, verilerin geçerli durumunu gösterir ve yine de bunu yapmak istiyorsa, kendi değişikliklerini yeniden girmeye izin verebilirsiniz. Girişi kaydederek işlemi otomatik hale getirebilir ve yeniden girmek zorunda kalmadan uygulamayı yeniden uygulamanız için bir fırsat verirsiniz. Buna *Mağaza WINS* senaryosu denir. (Veri deposu değerlerini istemci tarafından gönderilen değerler önceliklidir.)

### <a name="detecting-concurrency-conflicts"></a>Eşzamanlılık çakışmalarını algılama

Entity Framework, Entity Framework oluşturduğu `OptimisticConcurrencyException` özel durumları işleyerek çakışmaları çözebilirsiniz. Bu özel durumların ne zaman throw hakkında bilgi edinmek için Entity Framework çakışmaları algılayabilmelidir. Bu nedenle, veritabanını ve veri modelini uygun şekilde yapılandırmanız gerekir. Çakışma algılamayı etkinleştirmeye yönelik bazı seçenekler şunlardır:

- Veritabanında, bir satırın ne zaman değiştirildiğini belirlemede kullanılabilecek bir tablo sütunu ekleyin. Daha sonra Entity Framework SQL `Update` veya `Delete` komutlarının `Where` yan tümcesinde bu sütunu içerecek şekilde yapılandırabilirsiniz.

    `OfficeAssignment` tablosundaki `Timestamp` sütununun amacı.

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    `Timestamp` sütunun veri türü de `Timestamp`olarak adlandırılır. Ancak, sütun aslında bir tarih veya saat değeri içermez. Bunun yerine, değer, satır her güncelleştirildiği zaman artılan sıralı bir sayıdır. Bir `Update` veya `Delete` komutunda, `Where` yan tümcesi özgün `Timestamp` değerini içerir. Güncelleştirilmekte olan satır başka bir kullanıcı tarafından değiştirilmişse, `Timestamp` değeri özgün değerden farklıdır, bu nedenle `Where` yan tümcesi güncelleştirilecek bir satır döndürmez. Entity Framework geçerli `Update` veya `Delete` komutu tarafından güncelleştirilmemiş bir satır bulduğunda (yani, etkilenen satırların sayısı sıfır olduğunda), bunu bir eşzamanlılık çakışması olarak yorumlar.
- Entity Framework, `Update` ve `Delete` komutlarının `Where` yan tümcesindeki tablodaki her sütunun özgün değerlerini içerecek şekilde yapılandırın.

    İlk seçenekte olduğu gibi, satırdaki herhangi bir şey satırın ilk okuduğundan beri değiştiyse, `Where` yan tümcesi güncelleştirilecek bir satır döndürmez, bu da Entity Framework eşzamanlılık çakışması olarak yorumlar. Bu yöntem, bir `Timestamp` alanı kullanarak etkilidir, ancak verimsiz olabilir. Çok sayıda sütunu olan veritabanı tablolarında, çok büyük `Where` yan tümceleri ve bir Web uygulamasında büyük miktarlarda durum yaşmasını gerektirebilir. Büyük miktarlarda durum bulundurma, uygulama performansını etkileyebilir çünkü sunucu kaynakları (örneğin, oturum durumu) gerektirir veya Web sayfasının kendisine dahil olması gerekir (örneğin, Görünüm durumu).

Bu öğreticide, izleme özelliği (`Department` varlığı) olmayan bir varlık için ve izleme özelliği (`OfficeAssignment` varlığı) olan bir varlık için iyimser eşzamanlılık çakışmaları için hata işleme ekleyeceksiniz.

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>Izleme özelliği olmadan Iyimser eşzamanlılık işleme

İzleme (`Timestamp`) özelliğine sahip olmayan `Department` varlık için iyimser eşzamanlılık uygulamak için aşağıdaki görevleri tamamlayacaksınız:

- `Department` varlıkları için eşzamanlılık izlemeyi etkinleştirmek üzere veri modelini değiştirin.
- `SchoolRepository` sınıfında, `SaveChanges` yöntemindeki eşzamanlılık özel durumlarını işleyin.
- *Departmanlar. aspx* sayfasında, denenen değişikliklerin başarısız olduğunu kullanıcıya bildiren bir ileti görüntüleyerek eşzamanlılık özel durumlarını işleyin. Kullanıcı daha sonra geçerli değerleri görebilir ve hala gerekliyse değişiklikleri yeniden deneyebilir.

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>Veri modelinde eşzamanlılık Izlemeyi etkinleştirme

Visual Studio 'da, bu serideki önceki öğreticide birlikte çalıştığınız Contoso University Web uygulamasını açın.

*SchoolModel. edmx*' i açın ve veri modeli tasarımcısında, `Department` varlığındaki `Name` özelliğine sağ tıklayın ve ardından **Özellikler**' e tıklayın. **Özellikler** penceresinde `ConcurrencyMode` özelliğini `Fixed`olarak değiştirin.

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

Diğer birincil anahtar olmayan skalar özellikler için aynısını yapın (`Budget`, `StartDate`ve `Administrator`.) (Bunu, gezinti özellikleri için yapamazsınız.) Bu, Entity Framework veritabanındaki `Department` varlığı güncelleştirmek için bir `Update` veya `Delete` SQL komutu oluşturduğunda, bu sütunların (özgün değerlerle birlikte) `Where` yan tümcesine dahil olması gerektiğini belirtir. `Update` veya `Delete` komutu yürütüldüğünde hiçbir satır bulunamazsa Entity Framework iyimser eşzamanlılık özel durumu oluşturur.

Veri modelini kaydedin ve kapatın.

### <a name="handling-concurrency-exceptions-in-the-dal"></a>DAL içindeki eşzamanlılık özel durumlarını işleme

*SchoolRepository.cs* ' i açın ve `System.Data` ad alanı için aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

İyimser eşzamanlılık özel durumlarını işleyen aşağıdaki yeni `SaveChanges` yöntemi ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Bu yöntem çağrıldığında bir eşzamanlılık hatası oluşursa, bellekteki varlığın özellik değerleri, veritabanında Şu anda bulunan değerlerle yerine geçer. Web sayfasının işleyebilmesi için eşzamanlılık özel durumu yeniden oluşturulur.

`DeleteDepartment` ve `UpdateDepartment` yöntemlerinde, yeni yöntemi çağırmak için mevcut çağrıyı `context.SaveChanges()` bir `SaveChanges()` çağrısıyla değiştirin.

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>Sunu katmanındaki eşzamanlılık özel durumlarını işleme

*Departmanlar. aspx* ' i açın ve `DepartmentsObjectDataSource` denetimine bir `OnDeleted="DepartmentsObjectDataSource_Deleted"` özniteliği ekleyin. Denetim için açılış etiketi artık aşağıdaki örneğe benzeyecektir.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

`DepartmentsGridView` denetiminde, aşağıdaki örnekte gösterildiği gibi, `DataKeyNames` özniteliğinde tüm tablo sütunlarını belirtin. Bunun çok büyük bir görünüm durumu alanı oluşturulacağını unutmayın. Bu bir neden, izleme alanı kullanmanın yaygın olarak eşzamanlılık çakışmalarını izlemek için tercih edilen yoldur.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

*Departments.aspx.cs* ' i açın ve `System.Data` ad alanı için aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

Veri kaynağı denetiminin `Updated` çağrınızın yanı sıra eşzamanlılık özel durumlarını işlemek için olay işleyicilerinden `Deleted` aşağıdaki yeni yöntemi ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

Bu kod, özel durum türünü denetler ve bir eşzamanlılık özel durumu ise, kod, `ValidationSummary` denetiminde bir ileti görüntüleyen bir `CustomValidator` denetimi dinamik olarak oluşturur.

Daha önce eklediğiniz `Updated` olay işleyicisinden yeni yöntemi çağırın. Ayrıca, aynı yöntemi çağıran (ancak başka bir şey yapmama) yeni bir `Deleted` olay işleyicisi oluşturun:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>Departmanlar sayfasında Iyimser eşzamanlılık test etme

*Departmanlar. aspx* sayfasını çalıştırın.

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

Bir satırda **Düzenle** ' ye tıklayın ve **Bütçe** sütunundaki değeri değiştirin. (Mevcut `School` veritabanı kayıtları bazı geçersiz veriler içerdiğinden, bu öğretici için yalnızca oluşturduğunuz kayıtları düzenleyedeğiştirebileceğinizi unutmayın. Ekonomikler bölümünün kaydı, deneme için güvenli bir deneyimdir.)

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

Yeni bir tarayıcı penceresi açın ve sayfayı yeniden çalıştırın (URL 'YI ilk tarayıcı penceresinin Adres kutusundan ikinci tarayıcı penceresine kopyalayın).

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

Daha önce düzenlediğiniz satırda **Düzenle** ' ye tıklayın ve **Bütçe** değerini farklı bir şekilde değiştirin.

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

İkinci tarayıcı penceresinde **Güncelleştir**' e tıklayın. **Bütçe** miktarı, bu yeni değere başarıyla değiştirildi.

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

İlk tarayıcı penceresinde **Güncelleştir**' e tıklayın. Güncelleştirme başarısız olur. **Bütçe** miktarı, ikinci tarayıcı penceresinde ayarladığınız değer kullanılarak yeniden görüntülenir ve bir hata iletisi görürsünüz.

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>Izleme özelliği kullanarak Iyimser eşzamanlılık işleme

İzleme özelliğine sahip bir varlık için iyimser eşzamanlılık işlemek üzere aşağıdaki görevleri tamamlayacaksınız:

- `OfficeAssignment` varlıklarını yönetmek için veri modeline saklı yordamlar ekleyin. (İzleme özellikleri ve saklı yordamların birlikte kullanılması gerekmez; çizim için burada yalnızca birlikte gruplandırılır.)
- DAL içindeki iyimser eşzamanlılık özel durumlarını işlemek için kod dahil, DAL ve BLL for `OfficeAssignment` varlıklarına CRUD yöntemleri ekleyin.
- Office atamaları Web sayfası oluşturun.
- Yeni Web sayfasında iyimser eşzamanlılık testi yapın.

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>Veri modeline OfficeAssignment saklı yordamları ekleme

Model tasarımcısında *SchoolModel. edmx* dosyasını açın, tasarım yüzeyine sağ tıklayın ve **modeli Güncelleştir**' e tıklayın. **Veritabanı nesnelerinizi seçin** Iletişim kutusundaki **Ekle** sekmesinde **saklı yordamlar** ' ı genişletin ve üç `OfficeAssignment` saklı yordamını seçin (aşağıdaki ekran görüntüsüne bakın) ve ardından **son**' a tıklayın. (Bu saklı yordamlar bir betiği kullanarak indirdiğiniz veya oluşturduğunuz zaman veritabanında zaten var.)

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

`OfficeAssignment` varlığına sağ tıklayın ve **saklı yordam eşlemesi**' ni seçin.

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

**Insert**, **Update**ve **Delete** işlevlerini ilgili saklı yordamlarını kullanacak şekilde ayarlayın. `Update` işlevinin `OrigTimestamp` parametresi için, **özelliği** `Timestamp` olarak ayarlayın ve **özgün değeri kullan** seçeneğini belirleyin.

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

Entity Framework `UpdateOfficeAssignment` saklı yordamını çağırdığında, `OrigTimestamp` parametresindeki `Timestamp` sütununun özgün değerini geçer. Saklı yordam `Where` yan tümcesinde bu parametreyi kullanır:

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

Saklı yordam ayrıca güncelleştirme sonrasında `Timestamp` sütununun yeni değerini seçer. böylece, Entity Framework, ilgili veritabanı satırıyla eşitlenmiş olan `OfficeAssignment` varlığını devam edebilir.

(Office atamasını silmeye yönelik saklı yordamın `OrigTimestamp` parametreye sahip olmadığına unutmayın. Bu nedenle Entity Framework, bir varlığın silinmeden önce değiştirilmemiş olduğunu doğrulayamaz.)

Veri modelini kaydedin ve kapatın.

### <a name="adding-officeassignment-methods-to-the-dal"></a>OfficeAssignment yöntemlerini DAL 'ya ekleme

*ISchoolRepository.cs* ' i açın ve `OfficeAssignment` varlık kümesi için aşağıdaki CRUD yöntemlerini ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

Aşağıdaki yeni yöntemleri *SchoolRepository.cs*öğesine ekleyin. `UpdateOfficeAssignment` yönteminde, `context.SaveChanges`yerine yerel `SaveChanges` yöntemini çağırın.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

Test projesinde *MockSchoolRepository.cs* öğesini açın ve aşağıdaki `OfficeAssignment` koleksiyonunu ve CRUD yöntemlerini ekleyin. (Sahte depo, depo arabirimini uygulamalıdır veya çözüm derlenmez.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>BLL 'e OfficeAssignment yöntemleri ekleme

Ana projede *SchoolBL.cs* ' ı açın ve `OfficeAssignment` varlık için aşağıdaki CRUD yöntemlerini ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>Officeasbir Web sayfası oluşturma

*Site. Master* ana sayfasını kullanan yeni bir Web sayfası oluşturun ve bunu *officeas,. aspx*olarak adlandırın. Aşağıdaki biçimlendirmeyi `Content2`adlı `Content` denetimine ekleyin:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

`DataKeyNames` özniteliğinde, biçimlendirmenin `Timestamp` özelliğinin yanı sıra kayıt anahtarını (`InstructorID`) belirtir. `DataKeyNames` özniteliğinde özelliklerinin belirtilmesi, denetimin bunları, geri gönderme işlemi sırasında özgün değerlerin kullanılabilmesi için denetim durumunda (durumu görüntüleme gibi) kaydetmesine neden olur.

`Timestamp` değerini kaydetmezseniz, Entity Framework SQL `Update` komutunun `Where` yan tümcesi için bu değere sahip olmaz. Bu nedenle güncelleştirilecek hiçbir şey yok. Sonuç olarak, Entity Framework, bir `OfficeAssignment` varlık her güncelleştirildiği sırada iyimser eşzamanlılık özel durumu oluşturur.

*OfficeAssignments.aspx.cs* ' i açın ve veri erişim katmanı için aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

Dinamik veri işlevselliğine izin veren aşağıdaki `Page_Init` yöntemi ekleyin. Ayrıca eşzamanlılık hatalarını denetlemek için `ObjectDataSource` denetiminin `Updated` olayı için aşağıdaki işleyiciyi ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>Officeaslılılık sayfasında Iyimser eşzamanlılık test etme

*Officeas,. aspx* sayfasını çalıştırın.

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

Bir satırda **Düzenle** ' ye tıklayın ve **konum** sütunundaki değeri değiştirin.

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

Yeni bir tarayıcı penceresi açın ve sayfayı yeniden çalıştırın (URL 'YI ilk tarayıcı penceresinden ikinci tarayıcı penceresine kopyalayın).

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

Daha önce düzenlediğiniz satırda **Düzenle** ' ye tıklayın ve **konum** değerini farklı bir şekilde değiştirin.

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

İkinci tarayıcı penceresinde **Güncelleştir**' e tıklayın.

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

İlk tarayıcı penceresine geçin ve **Güncelleştir**' e tıklayın.

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

Bir hata iletisi görürsünüz ve **konum** değeri ikinci tarayıcı penceresinde olarak değiştirdiğiniz değeri gösterecek şekilde güncelleştirilmiştir.

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>EntityDataSource denetimiyle eşzamanlılık işleme

`EntityDataSource` denetimi, veri modelindeki eşzamanlılık ayarlarını algılayan ve güncelleştirme ve silme işlemlerini uygun şekilde işleyen yerleşik mantığı içerir. Ancak, tüm özel durumlarda olduğu gibi, Kullanıcı dostu bir hata mesajı sağlamak için `OptimisticConcurrencyException` özel durumları kendiniz de işlemeniz gerekir.

Daha sonra, Update ve DELETE işlemlerine izin vermek ve bir eşzamanlılık çakışması oluşursa bir hata mesajı göstermek için *Kurslar. aspx* sayfasını (bir `EntityDataSource` denetimi kullanır) yapılandıracaksınız. `Course` varlık bir eşzamanlılık izleme sütununa sahip olmadığından, `Department` varlık: tüm anahtar olmayan özelliklerin değerlerini takip eden aynı yöntemi kullanacaksınız.

*SchoolModel. edmx* dosyasını açın. `Course` varlığının anahtar olmayan özellikleri (`Title`, `Credits`ve `DepartmentID`) için **eşzamanlılık modu** özelliğini `Fixed`olarak ayarlayın. Ardından veri modelini kaydedip kapatın.

*Kurslar. aspx* sayfasını açın ve aşağıdaki değişiklikleri yapın:

- `CoursesEntityDataSource` denetiminde `EnableUpdate="true"` ve `EnableDelete="true"` özniteliklerini ekleyin. Bu denetim için açılış etiketi şimdi aşağıdaki örneğe benzer:

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- `CoursesGridView` denetiminde, `DataKeyNames` öznitelik değerini `"CourseID,Title,Credits,DepartmentID"`olarak değiştirin. Sonra, **düzenleme** ve **silme** düğmelerini (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`) gösteren `Columns` öğeye bir `CommandField` öğesi ekleyin. `GridView` denetimi artık aşağıdaki örneğe benzer:

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

Sayfayı çalıştırın ve departmanlar sayfasından daha önce yaptığınız gibi bir çakışma durumu oluşturun. Sayfayı iki tarayıcı penceresinde çalıştırın, her pencerede aynı satırda **Düzenle** ' ye tıklayın ve her birinde farklı bir değişiklik yapın. Bir pencerede **Güncelleştir** ' i tıklatın ve ardından diğer penceredeki **Güncelleştir** ' i tıklatın. İkinci kez **Güncelleştir** ' e tıkladığınızda, işlenmemiş bir eşzamanlılık özel durumu sonucu oluşan hata sayfasını görürsünüz.

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

Bu hatayı `ObjectDataSource` denetimi için nasıl işleyeceğine benzer bir şekilde işleyebilirsiniz. *Kurslar. aspx* sayfasını açın ve `CoursesEntityDataSource` denetiminde `Deleted` ve `Updated` olayları için işleyiciler belirtin. Denetimin açılış etiketi şimdi aşağıdaki örneğe benzer:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

`CoursesGridView` denetiminden önce aşağıdaki `ValidationSummary` denetimini ekleyin:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

*Courses.aspx.cs*içinde, `System.Data` ad alanı için `using` bir ifade ekleyin, eşzamanlılık özel durumlarını denetleyen bir yöntem ekleyin ve `EntityDataSource` denetiminin `Updated` ve `Deleted` işleyicileri için işleyiciler ekleyin. Kod aşağıdaki gibi görünür:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

Bu kod ve `ObjectDataSource` denetimi için yaptığınız özellikler arasındaki tek fark, bu durumda eşzamanlılık özel durumunun, bu özel durumun `InnerException` özelliği yerine olay bağımsız değişkenleri nesnesinin `Exception` özelliğinde olması gerektiğidir.

Sayfayı çalıştırın ve bir eşzamanlılık çakışması oluşturun. Bu kez bir hata iletisi görürsünüz:

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

Bu, eşzamanlılık çakışmalarını işlemeye giriş işlemini tamamlar. Sonraki öğreticide, Entity Framework kullanan bir Web uygulamasındaki performansı geliştirme hakkında rehberlik sağlanır.

> [!div class="step-by-step"]
> [Önceki](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [İleri](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
