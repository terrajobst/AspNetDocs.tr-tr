---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'Öğretici: ASP.NET MVC uygulamasıyla EF Database First için veri doğrulamayı geliştirin'
description: Bu öğretici, doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri modeline veri ek açıklamaları eklenmesine odaklanmaktadır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616279"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>Öğretici: ASP.NET MVC uygulamasıyla EF Database First için veri doğrulamayı geliştirin

MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz. Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir. Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.

Bu öğretici, doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri modeline veri ek açıklamaları eklenmesine odaklanmaktadır. Yorumlar bölümünde kullanıcılardan gelen geri bildirimlere göre geliştirilmiştir.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Veri ek açıklamaları Ekle
> * Meta veri sınıfları Ekle

## <a name="prerequisites"></a>Önkoşullar

* [Görünümü özelleştirme](customizing-a-view.md)

## <a name="add-data-annotations"></a>Veri ek açıklamaları Ekle

Daha önceki bir konu başlığında gördüğünüz gibi, bazı veri doğrulama kuralları Kullanıcı girişine otomatik olarak uygulanır. Örneğin, sınıf özelliği için yalnızca bir sayı sağlayabilirsiniz. Daha fazla veri doğrulama kuralı belirtmek için model sınıfınıza veri ek açıklamaları ekleyebilirsiniz. Bu ek açıklamalar, belirtilen özellik için Web uygulamanız genelinde uygulanır. Özelliklerin nasıl görüntülendiğini değiştiren biçimlendirme öznitelikleri de uygulayabilirsiniz. Örneğin, metin etiketleri için kullanılan değeri değiştirme.

Bu öğreticide, FirstName, LastName ve MiddleName özellikleri için belirtilen değerlerin uzunluğunu kısıtlamak üzere veri ek açıklamaları ekleyeceksiniz. Veritabanında, bu değerler 50 karakterle sınırlıdır; Ancak, Web uygulamanızda karakter sınırının Şu anda zorlanmadığını unutmayın. Bir Kullanıcı bu değerlerden biri için 50 ' den fazla karakter sağlıyorsa, bu değer veritabanına kaydedilmeye çalışıldığında sayfa kilitlenir. Ayrıca, 0 ile 4 arasındaki değerleri de sınırlayabilirsiniz.

 > **Contosomodel. edmx** > **ContosoModel.tt** **modellerini** seçin ve *Student.cs* dosyasını açın. Aşağıdaki Vurgulanan kodu sınıfına ekleyin.

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

*Enrollment.cs* açın ve aşağıdaki vurgulanmış kodu ekleyin.

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

Çözümü derleyin.

**Öğrenciler listesi** ' ne tıklayın ve **Düzenle**' yi seçin. 50 'den fazla karakter girmeye çalışırsanız bir hata iletisi görüntülenir.

![hata iletisini göster](enhancing-data-validation/_static/image1.png)

Giriş sayfasına geri dönün. Kayıt **listesi** ' ne tıklayın ve **Düzenle**' yi seçin. 4 ' ün üzerinde bir sınıf sağlamayı deneyin. Bu hatayı alırsınız: *alan sınıfı 0 ile 4 arasında olmalıdır.*

## <a name="add-metadata-classes"></a>Meta veri sınıfları Ekle

Doğrulama özniteliklerini doğrudan model sınıfına eklemek, veritabanının değiştirilmesini beklemediğinde işe yarar; Ancak, veritabanınız değişirse ve model sınıfını yeniden oluşturmanız gerekiyorsa, model sınıfına uyguladığınız tüm öznitelikleri kaybedersiniz. Bu yaklaşım çok verimsiz olabilir ve önemli doğrulama kurallarının kaybolması olabilir.

Bu sorundan kaçınmak için, özniteliklerini içeren bir meta veri sınıfı ekleyebilirsiniz. Model sınıfını meta veri sınıfıyla ilişkilendirdiğinizde, bu öznitelikler modele uygulanır. Bu yaklaşımda model sınıfı, meta veri sınıfına uygulanan tüm öznitelikleri kaybetmeden yeniden oluşturulabilir.

**Modeller** klasöründe, *Metadata.cs*adlı bir sınıf ekleyin.

*Metadata.cs* içindeki kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

Bu meta veri sınıfları, daha önce model sınıflarına uyguladığınız tüm doğrulama özniteliklerini içerir. **Görüntü** özniteliği, metin etiketleri için kullanılan değeri değiştirmek için kullanılır.

Şimdi, model sınıflarını meta veri sınıflarıyla ilişkilendirmeniz gerekir.

**Modeller** klasöründe, *PartialClasses.cs*adlı bir sınıf ekleyin.

Dosyanın içeriğini aşağıdaki kodla değiştirin.

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

Her sınıfın bir `partial` sınıfı olarak işaretlendiğinden ve her birinin otomatik olarak oluşturulan sınıf ile ad ve ad alanıyla eşleştiğini unutmayın. Meta veri özniteliğini kısmi sınıfa uygulayarak, veri doğrulama özniteliklerinin otomatik olarak oluşturulan sınıfa uygulandığından emin olursunuz. Meta veri özniteliği yeniden üretilmediği kısmi sınıflarda uygulandığından, model sınıflarını yeniden oluşturduğunuzda bu öznitelikler kaybolmaz.

Otomatik olarak oluşturulan sınıfları yeniden oluşturmak için *Contosomodel. edmx* dosyasını açın. Bir kez daha, tasarım yüzeyine sağ tıklayın ve **modeli veritabanından Güncelleştir**' i seçin. Veritabanını değiştirmeseniz bile, bu işlem sınıfları yeniden oluşturacak. **Yenile** sekmesinde **Tablolar** ve **son**' u seçin.

Değişiklikleri uygulamak için *Contosomodel. edmx* dosyasını kaydedin.

*Student.cs* dosyasını veya *enrollment.cs* dosyasını açın ve daha önce uyguladığınız veri doğrulama özniteliklerinin artık dosyada bulunmadığından emin olun. Ancak, uygulamayı çalıştırın ve veri girerken doğrulama kurallarının hala uygulanmış olduğuna dikkat edin.

## <a name="conclusion"></a>Sonuç

Bu seri, kullanıcıların verileri düzenlemesini, güncelleştirmesini, oluşturmasını ve silmesini sağlayan mevcut bir veritabanından kod oluşturmaya yönelik basit bir örnek sağlamıştır. Projeyi oluşturmak için ASP.NET MVC 5, Entity Framework ve ASP.NET Scafkatlesi kullandı. 

Code First geliştirmenin açıklayıcı bir örneği için bkz. [ASP.NET MVC 5 Ile çalışmaya](../introduction/getting-started.md)başlama. 

Daha gelişmiş bir örnek için bkz. [ASP.NET MVC 4 uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Database First verileriyle çalışırken kullandığınız DbContext API 'sinin, Code First verilerle çalışırken kullandığınız API ile aynı olduğunu unutmayın. Database First kullanmayı amaçlasanız bile, ilgili verileri okuma ve güncelleştirme, eşzamanlılık çakışmalarını işleme gibi daha karmaşık senaryoları nasıl işleyeceğinizi ve bir Code First öğreticiden yapmayı öğrenebilirsiniz. Tek fark, veritabanının, bağlam sınıfının ve varlık sınıflarının oluşturulma biçiminde olur.

## <a name="additional-resources"></a>Ek kaynaklar

Veri doğrulama ek açıklamalarının tam listesi için, Özellikler ve sınıflar için uygulayabileceğiniz, bkz. [System. ComponentModel. Dataaçıklamalarda](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Eklenen veri açıklamaları
> * Meta veri sınıfları eklendi

Azure App Service için bir Web uygulaması ve SQL veritabanı dağıtmayı öğrenmek için şu öğreticiye bakın:
> [!div class="nextstepaction"]
> [Azure App Service için bir .NET uygulaması dağıtma](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
