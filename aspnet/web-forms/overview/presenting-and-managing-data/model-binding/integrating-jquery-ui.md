---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: JQuery UI DatePicker model bağlama ve Web formlarıyla tümleştirme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642480"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>JQuery UI DatePicker model bağlama ve Web formlarıyla tümleştirme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir. Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.
> 
> Bu öğretici, JQuery UI [DatePicker pencere](http://jqueryui.com/datepicker/) öğesinin bir Web formuna nasıl ekleneceğini ve veritabanını seçili değerle güncellemek için model bağlamayı nasıl kullanacağınızı gösterir.
> 
> Bu öğreticide, serinin [Birinci](retrieving-data.md) ve [ikinci](updating-deleting-and-creating-data.md) bölümlerinde oluşturulan projede derleme yapılır.
> 
> Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz. İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir. Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğreticide şunları yapmanız gerekir:

1. Öğrencinin kayıt tarihini kaydetmek için modelinize bir özellik ekleyin
2. Kullanıcının JQuery Kullanıcı arabirimi DatePicker pencere öğesini kullanarak kayıt tarihini seçmesini sağlama
3. Kayıt tarihi için doğrulama kurallarını zorla

JQuery kullanıcı ARABIRIMI DatePicker pencere öğesi, kullanıcıların alanla etkileşime geçtiğinde bir takvimden bir tarihi kolayca seçmesini sağlar. Bu pencere öğesinin kullanılması, kullanıcıların el ile tarih yazmakla daha kullanışlı olabilir. DatePicker pencere öğesini, veri işlemleri için model bağlama kullanan bir sayfayla tümleştirmek yalnızca az miktarda ek iş gerektirir.

## <a name="add-a-new-property-to-the-model"></a>Modele yeni bir özellik ekleyin

İlk olarak, öğrenci modelinize bir **DateTime** özelliği ekleyecek ve bu değişikliği veritabanına geçirecaksınız. **UniversityModels.cs**' yi açın ve vurgulanan kodu öğrenci modeline ekleyin.

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

**RangeAttribute** , özelliği için doğrulama kurallarını zorlamak için eklenmiştir. Bu öğreticide, Contoso University 'in 1 Ocak 2013 ' de yer aldığı ve bu nedenle daha önceki kayıt tarihlerinin geçerli olmadığı varsayıyoruz.

Paket Yönetimi penceresinde, **Add-Migration AddEnrollmentDate**komutunu çalıştırarak bir geçiş ekleyin. Geçiş kodunun yeni tarih saat sütununu öğrenci tablosuna eklediğine dikkat edin. RangeAttribute içinde belirttiğiniz değeri eşleştirmek için, aşağıdaki vurgulanan kodda gösterildiği gibi yeni sütun için varsayılan bir değer ekleyin.

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

Değişiklerinizi geçiş dosyasına kaydedin.

Verileri yeniden temel almanız gerekmez. Bu nedenle, geçişler klasöründe **Configuration.cs** açın ve **çekirdek** yöntemindeki kodu kaldırın veya not edin. Dosyayı kaydedin ve kapatın.

Şimdi, **Update-Database**komutunu çalıştırın. Sütunun artık veritabanında var olduğunu ve var olan tüm kayıtların kayıt tarihi için varsayılan değere sahip olduğuna dikkat edin.

## <a name="add-dynamic-controls-for-enrollment-date"></a>Kayıt tarihi için dinamik denetimler ekleme

Şimdi kayıt tarihini görüntüleme ve düzenlemeyle ilgili denetimler ekleyeceksiniz. Bu noktada, değer bir metin kutusuyla düzenlenir. Öğreticide daha sonra, metin kutusunu JQuery DatePicker pencere öğesi olarak değiştirirsiniz.

İlk olarak, **Addstudent. aspx** dosyasında herhangi bir değişiklik yapmanız gerekmediğini unutmayın. DynamicEntity denetimi, yeni özelliği otomatik olarak işler.

**Öğrenciler. aspx**' i açın ve aşağıdaki vurgulanmış kodu ekleyin.

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

Uygulamayı çalıştırın ve bir tarih yazarak kayıt tarihinin değerini ayarlayabildiğinize dikkat edin. Yeni öğrenci eklerken:

![tarihi ayarla](integrating-jquery-ui/_static/image1.png)

Ya da varolan bir değeri düzenleyebilirsiniz:

![tarihi Düzenle](integrating-jquery-ui/_static/image2.png)

Çalışma tarihi yazılması, ancak sağlamak istediğiniz müşteri deneyimi olmayabilir. Sonraki bölümde, bir takvim üzerinden tarih seçmeyi etkinleştirecektir.

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>JQuery Kullanıcı arabirimi ile çalışmak için NuGet paketini yükler

Bu **Kullanıcı arabirimi** NuGet paketi, jQuery kullanıcı arabirimi Pencere öğelerinin Web uygulamanıza kolay bir şekilde tümleştirilmesini sunar. Bu paketi kullanmak için NuGet aracılığıyla yükleyemezsiniz.

![SBU Kullanıcı arabirimi Ekle](integrating-jquery-ui/_static/image3.png)

Yüklediğiniz bu kullanıcı arabirimi sürümü uygulamanızdaki JQuery sürümü ile çakışabilir. Bu öğreticiye devam etmeden önce, uygulamanızı çalıştırmayı deneyin. JavaScript hatasıyla karşılaşırsanız, JQuery sürümünü bağdaştırmanız gerekir. JQuery 'in beklenen sürümünü Scripts klasörünüze (Bu öğreticiyi yazma sırasında sürüm 1.8.2) veya sitesinde ekleyebilirsiniz. Master JQuery dosyasının yolunu belirtin.

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>DateTime şablonunu DatePicker pencere öğesini içerecek şekilde özelleştirme

DatePicker pencere öğesini dinamik veri şablonuna ekleyerek bir tarih saat değerini düzenleyebilirsiniz. Pencere öğesini şablona ekleyerek, otomatik olarak yeni öğrenci ekleme ve öğrencilerin düzenlenmesine yönelik kılavuz görünümünde otomatik olarak işlenir. **Tarih/saat\_açın. ascx**' i düzenleyin ve aşağıdaki vurgulanmış kodu ekleyin.

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

Arka plan kod dosyasında, DatePicker için en düşük ve en büyük tarihleri ayarlayacaksınız. Bu değerleri ayarlayarak, kullanıcıların geçersiz tarihlere gitmesini önleyecaksınız. Tarih saat özelliğindeki en düşük ve en yüksek değerleri, varsa DateTime özelliğinde elde edersiniz. **DateTime\_Edit.ascx.cs**açın ve sayfa\_Load yöntemine aşağıdaki vurgulanmış kodu ekleyin.

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

Web uygulamasını çalıştırın ve Addöğrenci sayfasına gidin. Alanlar için değerler sağlayın ve kayıt tarihi için metin kutusuna tıkladığınızda takvimin görüntülendiğini unutmayın.

![Tarih Seçici](integrating-jquery-ui/_static/image4.png)

Bir tarih seçin ve **Ekle**' ye tıklayın. RangeAttribute, sunucuda doğrulamayı zorlar. DatePicker üzerinde minDate özelliğini ayarlayarak, istemciye doğrulama de uygularsınız. Takvim, kullanıcının minDate değerinden önceki bir tarihe gitmasına izin vermez.

Kılavuz görünümünde bir kayıt düzenlediğinizde, takvim de görüntülenir.

![GridView 'da DatePicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>Sonuç

Bu öğreticide, bir JQuery pencere öğesini model bağlama kullanan bir Web formuna nasıl ekleyeceğinizi öğrendiniz.

Sonraki [öğreticide](using-query-string-values-to-retrieve-data.md), veri seçerken bir sorgu dizesi değeri kullanacaksınız.

> [!div class="step-by-step"]
> [Önceki](sorting-paging-and-filtering-data.md)
> [İleri](using-query-string-values-to-retrieve-data.md)
