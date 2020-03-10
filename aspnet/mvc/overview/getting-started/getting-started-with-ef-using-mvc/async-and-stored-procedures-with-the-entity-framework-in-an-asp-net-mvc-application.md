---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC uygulamasında EF ile zaman uyumsuz ve saklı yordamlar kullanın'
description: Bu öğreticide, zaman uyumsuz programlama modelini uygulamayı ve saklı yordamları nasıl kullanacağınızı öğreneceksiniz.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583442"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a>Öğretici: bir ASP.NET MVC uygulamasında EF ile zaman uyumsuz ve saklı yordamlar kullanın

Önceki öğreticilerde, zaman uyumlu programlama modelini kullanarak verileri okuma ve güncelleştirme hakkında bilgi edinirsiniz. Bu öğreticide, zaman uyumsuz programlama modelinin nasıl uygulanacağını görürsünüz. Zaman uyumsuz kod, sunucu kaynaklarını daha iyi kullandığından, uygulamanın daha iyi performans sağlanmasına yardımcı olabilir.

Bu öğreticide, bir varlıkta ekleme, güncelleştirme ve silme işlemleri için saklı yordamları nasıl kullanacağınızı da görürsünüz.

Son olarak, uygulamayı Azure 'a yeniden dağıtırsınız ve ilk kez dağıttığınız zamandan beri uyguladığınız tüm veritabanı değişiklikleri vardır.

Aşağıdaki çizimlerde, üzerinde çalıştığınız sayfaların bazıları gösterilmektedir.

![Departmanlar sayfası](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Departman oluşturma](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Zaman uyumsuz kod hakkında bilgi edinin
> * Departman denetleyicisi oluşturma
> * Saklı yordamları kullanma
> * Azure’a dağıtma

## <a name="prerequisites"></a>Önkoşullar

* [İlgili Verileri Güncelleştirme](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a>Neden zaman uyumsuz kod kullanılmalıdır?

Sınırlı sayıda iş parçacığı kullanılabilir bir web sunucusuna sahip ve yüksek yük durumlarda tüm kullanılabilir iş parçacıklarının kullanımda olabilir. Bu durum oluştuğunda, sunucunun iş parçacıklarının serbest bırakılana kadar yeni istekleri işleyemiyor. G/ç tamamlanması bekleniyor çünkü bunlar herhangi bir iş gerçekten yapmamanız sırasında eş zamanlı kod ile birçok iş parçacığı bağlanması. İşlemi tamamlamak, g/ç için beklerken zaman uyumsuz kod ile diğer istekleri işlemek için kullanılacak sunucuyu için kendi iş parçacığı serbest bırakılır. Sonuç olarak, zaman uyumsuz kod sunucu kaynaklarının daha verimli bir şekilde kullanılmasını ve sunucunun gecikmeler olmadan daha fazla trafiği işlemesini sağlar.

.NET 'in önceki sürümlerinde, zaman uyumsuz kodu yazma ve test etme karmaşık, hataya açık ve hata ayıklama zor idi. .NET 4,5 ' de, zaman uyumsuz kodu yazma, test etme ve hata ayıklama gibi bir nedeniniz olmadığı takdirde genellikle zaman uyumsuz kod yazmanız çok daha kolay olur. Zaman uyumsuz kod, az miktarda yük getirir, ancak düşük trafik durumlarında performans artışı göz ardı edilebilir, ancak yüksek trafik durumları için olası performans iyileştirmesi oldukça önemlidir.

Zaman uyumsuz programlama hakkında daha fazla bilgi için bkz. [çağrı engellemeyi önlemek için .NET 4.5 'in zaman uyumsuz desteğini kullanma](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).

## <a name="create-department-controller"></a>Departman denetleyicisi oluşturma

Daha önceki denetleyicilerle aynı şekilde bir departman denetleyicisi oluşturun, bu süre dışında **zaman uyumsuz denetleyici eylemlerini kullan** onay kutusunu seçin.

Aşağıdaki önemli noktalar, zaman uyumsuz hale getirmek için `Index` yöntemi için zaman uyumlu koda nelerin eklendiğini gösterir:

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

Entity Framework veritabanı sorgusunun zaman uyumsuz olarak yürütülmesine olanak tanımak için dört değişiklik uygulandı:

- Yöntemi, derleyicinin Yöntem gövdesinin bölümlerine geri çağrılar oluşturmasını ve döndürülen `Task<ActionResult>` nesnesini otomatik olarak oluşturmasını bildiren `async` anahtar sözcüğüyle işaretlenir.
- Dönüş türü, `ActionResult` `Task<ActionResult>`olarak değiştirildi. `Task<T>` türü, `T`türünde bir sonuçla devam eden işi temsil eder.
- `await` anahtar sözcüğü Web hizmeti çağrısına uygulandı. Derleyici bu anahtar sözcüğü gördüğünde, arka planda yöntemi iki parçaya böler. İlk bölüm, zaman uyumsuz olarak başlatılan işlemle biter. İkinci bölüm, işlem tamamlandığında çağrılan bir geri çağırma yöntemine konur.
- `ToList` uzantısı yönteminin zaman uyumsuz sürümü çağrıldı.

`departments.ToList` deyimleri neden değiştirildi, ancak `departments = db.Departments` deyimleri değil mi? Bu nedenle, yalnızca sorgu veya komutların veritabanına gönderilmesine neden olan deyimler zaman uyumsuz olarak yürütülür. `departments = db.Departments` ifade bir sorgu ayarlıyor, ancak `ToList` yöntemi çağrılana kadar sorgu yürütülmez. Bu nedenle, yalnızca `ToList` yöntemi zaman uyumsuz olarak yürütülür.

`Details` yönteminde ve `HttpGet` `Edit` ve `Delete` yöntemlerinde, `Find` yöntemi bir sorgunun veritabanına gönderilmesine neden olan bir yöntemdir, böylece zaman uyumsuz olarak yürütülen yöntem olur:

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

`Create`, `HttpPost Edit`ve `DeleteConfirmed` yöntemlerinde, bu, yalnızca bellekte bulunan varlıkların değiştirilmesine neden olan `db.Departments.Add(department)` gibi deyimler değil, bir komutun yürütülmesine neden olan `SaveChanges` yöntem çağrıdır.

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

*Views\Department\Index.cshtml*'i açın ve şablon kodunu şu kodla değiştirin:

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

Bu kod, başlığı dizinden departmanlar olarak değiştirir, yönetici adını sağa taşımakta ve yöneticinin tam adını sağlar.

Oluşturma, silme, Ayrıntılar ve düzenleme görünümlerinde, `InstructorID` alanının başlığını, Bölüm adı alanını kurs görünümlerinde "Departman" olarak değiştirdiğiniz şekilde "Yönetici" olarak değiştirin.

Oluşturma ve düzenleme görünümlerinde aşağıdaki kodu kullanın:

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

Silme ve Ayrıntılar görünümlerinde aşağıdaki kodu kullanın:

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

Uygulamayı çalıştırın ve **Departmanlar** sekmesine tıklayın.

Her şey diğer denetleyicilerle aynı şekilde çalışıyor, ancak bu denetleyicide tüm SQL sorguları zaman uyumsuz olarak yürütülüyor.

Entity Framework zaman uyumsuz programlama kullanırken dikkat etmeniz gereken bazı şeyler:

- Zaman uyumsuz kod iş parçacığı güvenli değildir. Diğer bir deyişle, diğer bir deyişle, aynı bağlam örneğini kullanarak paralel olarak birden çok işlem yapmayı denemeyin.
- Zaman uyumsuz kodun performans avantajlarından yararlanmak isterseniz, kullanmakta olduğunuz tüm kitaplık paketlerinin (örneğin, sayfalama için), sorguların veritabanına gönderilmesine neden olan herhangi bir Entity Framework yöntemini çağırıyorsa, zaman uyumsuz olarak da kullanılmasını sağlayın.

## <a name="use-stored-procedures"></a>Saklı yordamları kullanma

Bazı geliştiriciler ve DBAs, veritabanı erişimi için saklı yordamları kullanmayı tercih eder. Entity Framework önceki sürümlerinde, [Ham BIR SQL sorgusu yürüterek](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)saklı yordam kullanarak verileri alabilirsiniz, ancak güncelleştirme işlemlerine yönelik saklı yordamları kullanmak için EF 'e talimat verebilirsiniz. EF 6 ' da, saklı yordamları kullanmak için Code First yapılandırmak kolaydır.

1. *DAL\SchoolContext.cs*' de, vurgulanan kodu `OnModelCreating` yöntemine ekleyin.

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    Bu kod, `Department` varlığındaki ekleme, güncelleştirme ve silme işlemleri için saklı yordamları kullanmayı Entity Framework söyler.
2. Paket Yönetimi Konsolu ' nda, aşağıdaki komutu girin:

    `add-migration DepartmentSP`

    *\\&lt;zaman damgası&gt;\_* , ekleme, güncelleştirme ve silme saklı yordamlarını oluşturan `Up` yönteminde kodu görmek için zaman damgası ' nı açın:

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. Paket Yönetimi Konsolu ' nda, aşağıdaki komutu girin:

     `update-database`
4. Uygulamayı hata ayıklama modunda çalıştırın, **Departmanlar** sekmesine tıklayın ve ardından **Yeni oluştur**' a tıklayın.
5. Yeni bir departman için veri girin ve ardından **Oluştur**' a tıklayın.

6. Visual Studio 'da, yeni departman satırını eklemek için bir saklı yordamın kullanıldığını görmek için **Çıkış** penceresindeki günlüklere bakın.

     ![Bölüm ekleme SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Code First varsayılan saklı yordam adlarını oluşturur. Var olan bir veritabanını kullanıyorsanız, veritabanında önceden tanımlanmış saklı yordamları kullanabilmeniz için saklı yordam adlarını özelleştirmeniz gerekebilir. Bunun nasıl yapılacağı hakkında bilgi için, bkz. [Entity Framework Code First saklı yordamları ekleme/güncelleştirme/silme](https://msdn.microsoft.com/data/dn468673).

Oluşturulan saklı yordamları özelleştirmek istiyorsanız, saklı yordamı oluşturan geçişler `Up` yöntemi için yapı iskelesi kodunu düzenleyebilirsiniz. Bu şekilde, geçiş her çalıştırıldığında yaptığınız değişiklikler yansıtılır ve dağıtımdan sonra geçişler otomatik olarak çalıştırıldığında üretim veritabanınıza uygulanır.

Önceki bir geçişte oluşturulmuş mevcut bir saklı yordamı değiştirmek istiyorsanız, bir boş geçiş oluşturmak için Add-Migration komutunu kullanabilir ve ardından [Alterstoredprocedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) metodunu çağıran kodu el ile yazabilirsiniz.

## <a name="deploy-to-azure"></a>Azure’a dağıtma

Bu bölüm, bu serinin [geçişler ve dağıtım](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde **uygulamayı Azure 'a** isteğe bağlı olarak dağıtma bölümünü tamamladığınıza gerek duyar. Yerel projenizde veritabanını silerek çözümladığınız hataları geçirseniz, bu bölümü atlayın.

1. Visual Studio 'da **Çözüm Gezgini** projeye sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.
2. **Yayımla**’ta tıklayın.

    Visual Studio uygulamayı Azure 'a dağıtır ve uygulama, Azure 'da çalışan varsayılan tarayıcınızda açılır.
3. Çalışıp çalışmadığını doğrulamak için uygulamayı test edin.

    Veritabanına erişen bir sayfayı ilk kez çalıştırdığınızda Entity Framework, geçerli veri modeliyle veritabanını güncel hale getirmek için gereken tüm geçişleri `Up` yöntemlerini çalıştırır. Artık bu öğreticide eklediğiniz departman sayfaları dahil olmak üzere, son dağıttığınız zamandan sonra eklediğiniz tüm Web sayfalarını kullanabilirsiniz.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indirin](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Zaman uyumsuz kod hakkında öğrenildi
> * Bir departman denetleyicisi oluşturuldu
> * Kullanılan saklı yordamlar
> * Azure 'a dağıtıldı

Aynı anda birden çok kullanıcı aynı varlığı güncelleştirilişinde çakışmaların nasıl işleneceğini öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Eşzamanlılık işleme](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
