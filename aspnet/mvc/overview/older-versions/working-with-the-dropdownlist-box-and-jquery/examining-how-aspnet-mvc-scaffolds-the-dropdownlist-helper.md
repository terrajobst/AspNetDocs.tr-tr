---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: ASP.NET MVC 'nin DropDownList yardımcısını nasıl kullandığını İnceleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457615"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>ASP.NET MVC tarafından DropDownList yardımcısı için nasıl iskele oluşturulduğunu inceleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

**Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Denetleyici Ekle**' yi seçin. Denetleyiciyi **Storemanagercontroller**olarak adlandırın. Aşağıdaki görüntüde gösterildiği gibi **Denetleyici Ekle** iletişim kutusu seçeneklerini ayarlayın.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

*Storemanager\ındex.cshtml* görünümünü düzenleyin ve `AlbumArtUrl`kaldırın. `AlbumArtUrl` kaldırıldığında sunum daha okunabilir hale alınacaktır. Tamamlanan kodu aşağıda gösterilmiştir.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

*Controllers\storemanagercontroller.cs* dosyasını açın ve `Index` yöntemi bulun. Albümler fiyata göre sıralanabilmesi için `OrderBy` yan tümcesini ekleyin. Kodun tamamı aşağıda gösterilmiştir.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

Fiyata göre sıralama, değişiklikleri veritabanında test etmek için daha kolay hale gelir. Düzenleme ve oluşturma yöntemlerini test ederken, önce kaydedilmiş verilerin görünmesi için düşük bir fiyat kullanabilirsiniz.

*Storemanager\edit.exe* dosyasını açın. Gösterge etiketinden hemen sonra aşağıdaki satırı ekleyin.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

Aşağıdaki kod bu değişikliğin bağlamını gösterir:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

Bir albüm kaydında değişiklik yapmak için `AlbumId` gereklidir.

Uygulamayı çalıştırmak için CTRL+F5'e basın. **Yönetici** bağlantısını seçin ve yeni bir albüm oluşturmak Için **Yeni oluştur** bağlantısını seçin. Albüm bilgilerinin kaydedildiğini doğrulayın. Bir albümü düzenleyin ve yaptığınız değişikliklerin kalıcı olduğunu doğrulayın.

### <a name="the-album-schema"></a>Albüm şeması

MVC yapı iskelesi mekanizması tarafından oluşturulan `StoreManager` denetleyicisi, yolculuk (oluşturma, okuma, güncelleştirme, silme) ile müzik mağazası veritabanındaki albümlere erişim sağlar. Albüm bilgileri şeması aşağıda gösterilmiştir:

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums` tablosu, albüm tarzı ve açıklamasını depolamaz, `Genres` tabloya bir yabancı anahtar depolar. `Genres` tablosu, tarz adını ve açıklamasını içerir. Benzer şekilde, `Albums` tablo, albüm sanatçıları adını, `Artists` tablosuna yabancı bir anahtarı içermez. `Artists` tablosu, sanatçının adını içerir. `Albums` tablosundaki verileri incelerseniz, her bir satırın `Genres` tabloya yabancı anahtar ve `Artists` tabloya yabancı anahtar içerdiğini görebilirsiniz. Aşağıdaki görüntüde `Albums` tablosundan bazı tablo verileri gösterilmektedir.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML seçme etiketi

HTML `<select>` öğesi (HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) Yardımcısı tarafından oluşturulan), değerlerin tüm listesini (örneğin, tarzlar listesi) göstermek için kullanılır. Form düzenleme için, geçerli değer bilindiğinde, seçim listesinde geçerli değer görüntülenebilir. Bu, daha önce seçili değeri **komedi**olarak belirlediğimiz zaman gördük. Seçim listesi Kategori veya yabancı anahtar verilerini görüntülemek için idealdir. Tarzı yabancı anahtar için `<select>` öğesi, olası tarz adlarının listesini görüntüler, ancak formu kaydettiğinizde, tarz özelliği, görüntülenen tarz adı değil, tarzı yabancı anahtar değeri ile güncelleştirilir. Aşağıdaki görüntüde, seçilen tarz **disco** ve sanatçı **Donna yazın**.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>ASP.NET MVC Scafkatlama kodunu inceleme

*Controllers\storemanagercontroller.cs* dosyasını açın ve `HTTP GET Create` yöntemi bulun.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` yöntemi `ViewBag`iki [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) nesnesi ekler, biri tarz bilgilerini içerecek şekilde, diğeri de sanatçı bilgilerini içermelidir. Yukarıda kullanılan [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) Oluşturucu aşırı yüklemesi üç bağımsız değişken alır:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *Items*: listedeki öğeleri Içeren bir [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) . Yukarıdaki örnekte, `db.Genres`tarafından döndürülen tarzın listesi.
2. *DataValueField*: anahtar değerini içeren **IEnumerable** listesindeki özelliğin adı. Yukarıdaki örnekte, `GenreId` ve `ArtistId`.
3. *DataTextField*: görüntülenecek bilgileri içeren **IEnumerable** listesindeki özelliğin adı. Sanatçı ve tarz tablosunda, `name` alanı kullanılır.

*Views\storemanager\create5cshtml* dosyasını açın ve tarz alanı için `Html.DropDownList` yardımcı işaretlemesini inceleyin.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

İlk satır, oluşturma görünümünün `Album` model aldığını gösterir. Yukarıda gösterilen `Create` yönteminde hiçbir model iletilmemiştir, bu nedenle Görünüm **null** `Album` modeli alır. Bu noktada yeni bir albüm oluşturuyoruz. bu nedenle, bunun için `Album` veri yok.

Yukarıda gösterilen [HTML. DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) aşırı yüklemesi, modele bağlanacak alanın adını alır. Ayrıca, [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) nesnesi Içeren bir **ViewBag** nesnesini aramak için bu adı kullanır. Bu aşırı yüklemeyi kullanarak, **ViewBag SelectList** nesnesinin `GenreId`adını yazmanız gerekir. İkinci parametre (`String.Empty`), hiçbir öğe seçilne zaman seçili olmadığında görüntülenecek metindir. Bu, yeni bir albüm oluştururken tam olarak istediğiniz şeydir. İkinci parametreyi kaldırdıysanız ve aşağıdaki kodu kullandıysanız:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

Seçim listesi varsayılan olarak ilk öğe veya örneğimizde rock olur.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

`HTTP POST Create` yöntemi inceleniyor.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

`Create` yönteminin bu aşırı yüklemesi, gönderilen form değerlerinden ASP.NET MVC model bağlama sistemi tarafından oluşturulan bir `album` nesnesi alır. Yeni bir albüm gönderdiğinizde, model durumu geçerliyse ve veritabanı hatası yoksa, yeni albüm veritabanına eklenir. Aşağıdaki görüntüde yeni bir albümün oluşturulması gösterilmektedir.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

ASP.NET MVC model bağlamasının albüm nesnesini oluşturmak için kullandığı postalanmış form değerlerini incelemek için [Fiddler aracını](http://www.fiddler2.com/fiddler2/) kullanabilirsiniz.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).

### <a name="refactoring-the-viewbag-selectlist-creation"></a>ViewBag SelectList oluşturmayı yeniden düzenleme

`Edit` yöntemlerinin ve `HTTP POST Create` yönteminin her ikisi de **ViewBag**Içinde **SelectList** öğesini ayarlamak için aynı koda sahiptir. Bu [durumda, bu](http://en.wikipedia.org/wiki/Don't_repeat_yourself)kodu yeniden düzenlemelisiniz. Bu yeniden düzenlenmiş kodundan daha sonra bir kullanım yapacağız.

**ViewBag**'e bir tarz ve sanatçı **SelectList** eklemek için yeni bir yöntem oluşturun.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

İki satırı, `Create` ve `Edit` yöntemlerinin her biri içindeki `ViewBag`, `SetGenreArtistViewBag` yöntemine yönelik bir çağrıda olacak şekilde değiştirin. Tamamlanan kodu aşağıda gösterilmiştir.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

Değişikliklerin çalıştığını doğrulamak için yeni bir albüm oluşturun ve bir albümü düzenleyin.

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>SelectList öğesini DropDownList 'e açık bir şekilde geçirme

ASP.NET MVC yapı iskelesi tarafından oluşturulan oluşturma ve düzenleme görünümleri aşağıdaki **DropDownList** aşırı yüklemesini kullanır:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

Oluşturma görünümü için `DropDownList` biçimlendirmesi aşağıda gösterilmiştir.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

`SelectList` için `ViewBag` özelliği `GenreId`olarak adlandırıldığından, **DropDownList** Yardımcısı **viewbag**içindeki `GenreId`**SelectList** ' i kullanacaktır. Aşağıdaki **DropDownList** Aşırı yükte, `SelectList` açıkça geçirilir.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

*Views\storemanager\edit.exe* dosyasını açın ve **DropDownList** çağrısını, yukarıdaki aşırı yüklemeyi kullanarak **SelectList**içinde açıkça geçirilecek şekilde değiştirin. Bunu tarz kategorisi için yapın. Tamamlanan kod aşağıda gösterilmektedir:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

Uygulamayı çalıştırın ve **yönetici** bağlantısına tıklayın, ardından bir CAE albümüne gidin ve **Düzenle** bağlantısını seçin.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

Şu anda seçili olan tarz olarak CAAS göstermek yerine rock görüntülenir. Dize bağımsız değişkeni (bağlanacak özellik) ve **SelectList** nesnesi aynı ada sahip olduğunda, seçilen değer kullanılmaz. Seçili değer yoksa, tarayıcılar varsayılan olarak **SelectList**içindeki ilk öğeye (Yukarıdaki örnekte **rock** olur) sahiptir. Bu, **DropDownList** Yardımcısı 'nın bilinen bir sınırlamasıdır.

*Controllers\storemanagercontroller.cs* dosyasını açın ve **SelectList** nesne adlarını `Genres` ve `Artists`olarak değiştirin. Tamamlanan kod aşağıda gösterilmektedir:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

Her bir kategorinin KIMLIĞI daha fazlasını içerdiğinden, tarzlar ve sanatçı adları kategoriler için daha iyi adlardır. Daha önce ödediğimiz yeniden düzenleme. Dört yöntemde **ViewBag** 'i değiştirmek yerine, değişiklikler `SetGenreArtistViewBag` yöntemi ile yalıtılmış.

Yeni **SelectList** adlarını kullanmak için oluşturma ve düzenleme görünümlerindeki **DropDownList** çağrısını değiştirin. Düzenleme görünümü için yeni biçimlendirme aşağıda gösterilmiştir:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Oluşturma görünümü, SelectList içindeki ilk öğenin görüntülenmesini engellemek için boş bir dize gerektirir.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

Değişikliklerin çalıştığını doğrulamak için yeni bir albüm oluşturun ve bir albümü düzenleyin. Rock dışında bir tarz bir albüm seçerek düzenleme kodunu test edin.

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>DropDownList Yardımcısı ile bir görünüm modeli kullanma

`AlbumSelectListViewModel`adlı Viewmodeller klasöründe yeni bir sınıf oluşturun. `AlbumSelectListViewModel` sınıfındaki kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel` Oluşturucu, sanatçı ve tarzların listesini, albüm ve tarzlar ve sanatçılar için bir `SelectList` içeren bir nesne oluşturur.

Bir sonraki adımda bir görünüm oluşturduğumuz zaman `AlbumSelectListViewModel` için projeyi derleyin.

`StoreManagerController`bir `EditVM` yöntemi ekleyin. Tamamlanan kodu aşağıda gösterilmiştir.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

`AlbumSelectListViewModel`sağ tıklayın, **Çözümle**' yi ve ardından **MvcMusicStore. viewmodeller;** öğesini seçin.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

Alternatif olarak, aşağıdaki using ifadesini de ekleyebilirsiniz:

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

`EditVM` sağ tıklayın ve **Görünüm Ekle**' yi seçin. Aşağıda gösterilen seçenekleri kullanın.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

**Ekle**' yi seçin, ardından *Views\storemanager\editvm.exe* dosyasının içeriğini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM` biçimlendirmesi, özgün `Edit` biçimlendirmesine aşağıdaki özel durumlarla çok benzer.

- `Edit` görünümündeki model özellikleri `model.property`form (örneğin, `model.Title`). `EditVm` görünümündeki model özellikleri `model.Album.property`form (örneğin, `model.Album.Title`). Çünkü `EditVM` görünümü `Edit` görünümünde olduğu gibi bir `Album` değil `Album`için bir kapsayıcı geçirmez.
- **DropDownList** Second parametresi, **ViewBag**değil, görünüm modelinden gelir.
- `EditVM` görünümündeki **BeginForm** Yardımcısı `Edit` eylem yöntemine açıkça geri gönderiler. `Edit` eyleme geri döndüğünüzde, `HTTP POST EditVM` eylemi yazmak zorunda kalmaz ve `HTTP POST` `Edit` eylemini yeniden kullanabilir.

Uygulamayı çalıştırın ve bir albümü düzenleyin. `EditVM`kullanılacak URL 'YI değiştirin. Bir alanı değiştirin ve kodun çalıştığını doğrulamak için **Kaydet** düğmesine basın.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>Hangi yaklaşımı kullanmalısınız?

Gösterilen üç yaklaşımdan bazıları kabul edilebilir. Birçok geliştirici, `ViewBag`kullanarak `DropDownList` `SelectList` açıkça geçirmeye tercih eder. Bu yaklaşım, koleksiyon için daha uygun bir ad kullanma esnekliği sağlayan ek avantajına sahiptir. Bir desteklenmediği uyarısıyla, `ViewBag SelectList` nesnesine model özelliği ile aynı adı verebilir.

Bazı geliştiriciler ViewModel yaklaşımını tercih eder. Diğerleri daha ayrıntılı biçimlendirme ve ViewModel tarafından oluşturulan HTML 'nin bir dezavantajı olduğunu düşünsün.

Bu bölümde, kategori verileriyle **DropDownList** 'i kullanmanın üç yaklaşımını öğrendik. Sonraki bölümde, yeni bir kategorinin nasıl ekleneceğini göstereceğiz.

> [!div class="step-by-step"]
> [Önceki](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [İleri](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
