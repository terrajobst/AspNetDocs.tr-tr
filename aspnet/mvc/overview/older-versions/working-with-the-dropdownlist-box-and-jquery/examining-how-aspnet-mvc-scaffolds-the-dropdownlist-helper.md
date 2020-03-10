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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614907"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="66143-102">ASP.NET MVC tarafından DropDownList yardımcısı için nasıl iskele oluşturulduğunu inceleme</span><span class="sxs-lookup"><span data-stu-id="66143-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="66143-103">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="66143-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="66143-104">**Çözüm Gezgini**, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Denetleyici Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="66143-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="66143-105">Denetleyiciyi **Storemanagercontroller**olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="66143-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="66143-106">Aşağıdaki görüntüde gösterildiği gibi **Denetleyici Ekle** iletişim kutusu seçeneklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66143-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="66143-107">*Storemanager\ındex.cshtml* görünümünü düzenleyin ve `AlbumArtUrl`kaldırın.</span><span class="sxs-lookup"><span data-stu-id="66143-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="66143-108">`AlbumArtUrl` kaldırıldığında sunum daha okunabilir hale alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="66143-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="66143-109">Tamamlanan kodu aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66143-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="66143-110">*Controllers\storemanagercontroller.cs* dosyasını açın ve `Index` yöntemi bulun.</span><span class="sxs-lookup"><span data-stu-id="66143-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="66143-111">Albümler fiyata göre sıralanabilmesi için `OrderBy` yan tümcesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="66143-112">Kodun tamamı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66143-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="66143-113">Fiyata göre sıralama, değişiklikleri veritabanında test etmek için daha kolay hale gelir.</span><span class="sxs-lookup"><span data-stu-id="66143-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="66143-114">Düzenleme ve oluşturma yöntemlerini test ederken, önce kaydedilmiş verilerin görünmesi için düşük bir fiyat kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66143-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="66143-115">*Storemanager\edit.exe* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="66143-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="66143-116">Gösterge etiketinden hemen sonra aşağıdaki satırı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="66143-117">Aşağıdaki kod bu değişikliğin bağlamını gösterir:</span><span class="sxs-lookup"><span data-stu-id="66143-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="66143-118">Bir albüm kaydında değişiklik yapmak için `AlbumId` gereklidir.</span><span class="sxs-lookup"><span data-stu-id="66143-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="66143-119">Uygulamayı çalıştırmak için CTRL+F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="66143-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="66143-120">**Yönetici** bağlantısını seçin ve yeni bir albüm oluşturmak Için **Yeni oluştur** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="66143-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="66143-121">Albüm bilgilerinin kaydedildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="66143-121">Verify the album information was saved.</span></span> <span data-ttu-id="66143-122">Bir albümü düzenleyin ve yaptığınız değişikliklerin kalıcı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="66143-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="66143-123">Albüm şeması</span><span class="sxs-lookup"><span data-stu-id="66143-123">The Album Schema</span></span>

<span data-ttu-id="66143-124">MVC yapı iskelesi mekanizması tarafından oluşturulan `StoreManager` denetleyicisi, yolculuk (oluşturma, okuma, güncelleştirme, silme) ile müzik mağazası veritabanındaki albümlere erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="66143-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="66143-125">Albüm bilgileri şeması aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="66143-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="66143-126">`Albums` tablosu, albüm tarzı ve açıklamasını depolamaz, `Genres` tabloya bir yabancı anahtar depolar.</span><span class="sxs-lookup"><span data-stu-id="66143-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="66143-127">`Genres` tablosu, tarz adını ve açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="66143-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="66143-128">Benzer şekilde, `Albums` tablo, albüm sanatçıları adını, `Artists` tablosuna yabancı bir anahtarı içermez.</span><span class="sxs-lookup"><span data-stu-id="66143-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="66143-129">`Artists` tablosu, sanatçının adını içerir.</span><span class="sxs-lookup"><span data-stu-id="66143-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="66143-130">`Albums` tablosundaki verileri incelerseniz, her bir satırın `Genres` tabloya yabancı anahtar ve `Artists` tabloya yabancı anahtar içerdiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66143-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="66143-131">Aşağıdaki görüntüde `Albums` tablosundan bazı tablo verileri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="66143-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="66143-132">HTML seçme etiketi</span><span class="sxs-lookup"><span data-stu-id="66143-132">The HTML Select Tag</span></span>

<span data-ttu-id="66143-133">HTML `<select>` öğesi (HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) Yardımcısı tarafından oluşturulan), değerlerin tüm listesini (örneğin, tarzlar listesi) göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66143-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="66143-134">Form düzenleme için, geçerli değer bilindiğinde, seçim listesinde geçerli değer görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="66143-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="66143-135">Bu, daha önce seçili değeri **komedi**olarak belirlediğimiz zaman gördük.</span><span class="sxs-lookup"><span data-stu-id="66143-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="66143-136">Seçim listesi Kategori veya yabancı anahtar verilerini görüntülemek için idealdir.</span><span class="sxs-lookup"><span data-stu-id="66143-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="66143-137">Tarzı yabancı anahtar için `<select>` öğesi, olası tarz adlarının listesini görüntüler, ancak formu kaydettiğinizde, tarz özelliği, görüntülenen tarz adı değil, tarzı yabancı anahtar değeri ile güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="66143-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="66143-138">Aşağıdaki görüntüde, seçilen tarz **disco** ve sanatçı **Donna yazın**.</span><span class="sxs-lookup"><span data-stu-id="66143-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="66143-139">ASP.NET MVC Scafkatlama kodunu inceleme</span><span class="sxs-lookup"><span data-stu-id="66143-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="66143-140">*Controllers\storemanagercontroller.cs* dosyasını açın ve `HTTP GET Create` yöntemi bulun.</span><span class="sxs-lookup"><span data-stu-id="66143-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="66143-141">`Create` yöntemi `ViewBag`iki [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) nesnesi ekler, biri tarz bilgilerini içerecek şekilde, diğeri de sanatçı bilgilerini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="66143-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="66143-142">Yukarıda kullanılan [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) Oluşturucu aşırı yüklemesi üç bağımsız değişken alır:</span><span class="sxs-lookup"><span data-stu-id="66143-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="66143-143">*Items*: listedeki öğeleri Içeren bir [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) .</span><span class="sxs-lookup"><span data-stu-id="66143-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="66143-144">Yukarıdaki örnekte, `db.Genres`tarafından döndürülen tarzın listesi.</span><span class="sxs-lookup"><span data-stu-id="66143-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="66143-145">*DataValueField*: anahtar değerini içeren **IEnumerable** listesindeki özelliğin adı.</span><span class="sxs-lookup"><span data-stu-id="66143-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="66143-146">Yukarıdaki örnekte, `GenreId` ve `ArtistId`.</span><span class="sxs-lookup"><span data-stu-id="66143-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="66143-147">*DataTextField*: görüntülenecek bilgileri içeren **IEnumerable** listesindeki özelliğin adı.</span><span class="sxs-lookup"><span data-stu-id="66143-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="66143-148">Sanatçı ve tarz tablosunda, `name` alanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66143-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="66143-149">*Views\storemanager\create5cshtml* dosyasını açın ve tarz alanı için `Html.DropDownList` yardımcı işaretlemesini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="66143-150">İlk satır, oluşturma görünümünün `Album` model aldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="66143-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="66143-151">Yukarıda gösterilen `Create` yönteminde hiçbir model iletilmemiştir, bu nedenle Görünüm **null** `Album` modeli alır.</span><span class="sxs-lookup"><span data-stu-id="66143-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="66143-152">Bu noktada yeni bir albüm oluşturuyoruz. bu nedenle, bunun için `Album` veri yok.</span><span class="sxs-lookup"><span data-stu-id="66143-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="66143-153">Yukarıda gösterilen [HTML. DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) aşırı yüklemesi, modele bağlanacak alanın adını alır.</span><span class="sxs-lookup"><span data-stu-id="66143-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="66143-154">Ayrıca, [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) nesnesi Içeren bir **ViewBag** nesnesini aramak için bu adı kullanır.</span><span class="sxs-lookup"><span data-stu-id="66143-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="66143-155">Bu aşırı yüklemeyi kullanarak, **ViewBag SelectList** nesnesinin `GenreId`adını yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66143-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="66143-156">İkinci parametre (`String.Empty`), hiçbir öğe seçilne zaman seçili olmadığında görüntülenecek metindir.</span><span class="sxs-lookup"><span data-stu-id="66143-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="66143-157">Bu, yeni bir albüm oluştururken tam olarak istediğiniz şeydir.</span><span class="sxs-lookup"><span data-stu-id="66143-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="66143-158">İkinci parametreyi kaldırdıysanız ve aşağıdaki kodu kullandıysanız:</span><span class="sxs-lookup"><span data-stu-id="66143-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="66143-159">Seçim listesi varsayılan olarak ilk öğe veya örneğimizde rock olur.</span><span class="sxs-lookup"><span data-stu-id="66143-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="66143-160">`HTTP POST Create` yöntemi inceleniyor.</span><span class="sxs-lookup"><span data-stu-id="66143-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="66143-161">`Create` yönteminin bu aşırı yüklemesi, gönderilen form değerlerinden ASP.NET MVC model bağlama sistemi tarafından oluşturulan bir `album` nesnesi alır.</span><span class="sxs-lookup"><span data-stu-id="66143-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="66143-162">Yeni bir albüm gönderdiğinizde, model durumu geçerliyse ve veritabanı hatası yoksa, yeni albüm veritabanına eklenir.</span><span class="sxs-lookup"><span data-stu-id="66143-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="66143-163">Aşağıdaki görüntüde yeni bir albümün oluşturulması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="66143-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="66143-164">ASP.NET MVC model bağlamasının albüm nesnesini oluşturmak için kullandığı postalanmış form değerlerini incelemek için [Fiddler aracını](http://www.fiddler2.com/fiddler2/) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66143-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="66143-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span><span class="sxs-lookup"><span data-stu-id="66143-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="66143-166">ViewBag SelectList oluşturmayı yeniden düzenleme</span><span class="sxs-lookup"><span data-stu-id="66143-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="66143-167">`Edit` yöntemlerinin ve `HTTP POST Create` yönteminin her ikisi de **ViewBag**Içinde **SelectList** öğesini ayarlamak için aynı koda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="66143-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="66143-168">Bu [durumda, bu](http://en.wikipedia.org/wiki/Don't_repeat_yourself)kodu yeniden düzenlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="66143-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="66143-169">Bu yeniden düzenlenmiş kodundan daha sonra bir kullanım yapacağız.</span><span class="sxs-lookup"><span data-stu-id="66143-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="66143-170">**ViewBag**'e bir tarz ve sanatçı **SelectList** eklemek için yeni bir yöntem oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66143-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="66143-171">İki satırı, `Create` ve `Edit` yöntemlerinin her biri içindeki `ViewBag`, `SetGenreArtistViewBag` yöntemine yönelik bir çağrıda olacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="66143-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="66143-172">Tamamlanan kodu aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66143-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="66143-173">Değişikliklerin çalıştığını doğrulamak için yeni bir albüm oluşturun ve bir albümü düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="66143-174">SelectList öğesini DropDownList 'e açık bir şekilde geçirme</span><span class="sxs-lookup"><span data-stu-id="66143-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="66143-175">ASP.NET MVC yapı iskelesi tarafından oluşturulan oluşturma ve düzenleme görünümleri aşağıdaki **DropDownList** aşırı yüklemesini kullanır:</span><span class="sxs-lookup"><span data-stu-id="66143-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="66143-176">Oluşturma görünümü için `DropDownList` biçimlendirmesi aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66143-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="66143-177">`SelectList` için `ViewBag` özelliği `GenreId`olarak adlandırıldığından, **DropDownList** Yardımcısı **viewbag**içindeki `GenreId`**SelectList** ' i kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="66143-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="66143-178">Aşağıdaki **DropDownList** Aşırı yükte, `SelectList` açıkça geçirilir.</span><span class="sxs-lookup"><span data-stu-id="66143-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="66143-179">*Views\storemanager\edit.exe* dosyasını açın ve **DropDownList** çağrısını, yukarıdaki aşırı yüklemeyi kullanarak **SelectList**içinde açıkça geçirilecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="66143-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="66143-180">Bunu tarz kategorisi için yapın.</span><span class="sxs-lookup"><span data-stu-id="66143-180">Do this for the Genre category.</span></span> <span data-ttu-id="66143-181">Tamamlanan kod aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="66143-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="66143-182">Uygulamayı çalıştırın ve **yönetici** bağlantısına tıklayın, ardından bir CAE albümüne gidin ve **Düzenle** bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="66143-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="66143-183">Şu anda seçili olan tarz olarak CAAS göstermek yerine rock görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="66143-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="66143-184">Dize bağımsız değişkeni (bağlanacak özellik) ve **SelectList** nesnesi aynı ada sahip olduğunda, seçilen değer kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="66143-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="66143-185">Seçili değer yoksa, tarayıcılar varsayılan olarak **SelectList**içindeki ilk öğeye (Yukarıdaki örnekte **rock** olur) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="66143-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="66143-186">Bu, **DropDownList** Yardımcısı 'nın bilinen bir sınırlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="66143-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="66143-187">*Controllers\storemanagercontroller.cs* dosyasını açın ve **SelectList** nesne adlarını `Genres` ve `Artists`olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="66143-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="66143-188">Tamamlanan kod aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="66143-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="66143-189">Her bir kategorinin KIMLIĞI daha fazlasını içerdiğinden, tarzlar ve sanatçı adları kategoriler için daha iyi adlardır.</span><span class="sxs-lookup"><span data-stu-id="66143-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="66143-190">Daha önce ödediğimiz yeniden düzenleme.</span><span class="sxs-lookup"><span data-stu-id="66143-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="66143-191">Dört yöntemde **ViewBag** 'i değiştirmek yerine, değişiklikler `SetGenreArtistViewBag` yöntemi ile yalıtılmış.</span><span class="sxs-lookup"><span data-stu-id="66143-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="66143-192">Yeni **SelectList** adlarını kullanmak için oluşturma ve düzenleme görünümlerindeki **DropDownList** çağrısını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="66143-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="66143-193">Düzenleme görünümü için yeni biçimlendirme aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="66143-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="66143-194">Oluşturma görünümü, SelectList içindeki ilk öğenin görüntülenmesini engellemek için boş bir dize gerektirir.</span><span class="sxs-lookup"><span data-stu-id="66143-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="66143-195">Değişikliklerin çalıştığını doğrulamak için yeni bir albüm oluşturun ve bir albümü düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="66143-196">Rock dışında bir tarz bir albüm seçerek düzenleme kodunu test edin.</span><span class="sxs-lookup"><span data-stu-id="66143-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="66143-197">DropDownList Yardımcısı ile bir görünüm modeli kullanma</span><span class="sxs-lookup"><span data-stu-id="66143-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="66143-198">`AlbumSelectListViewModel`adlı Viewmodeller klasöründe yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66143-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="66143-199">`AlbumSelectListViewModel` sınıfındaki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="66143-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="66143-200">`AlbumSelectListViewModel` Oluşturucu, sanatçı ve tarzların listesini, albüm ve tarzlar ve sanatçılar için bir `SelectList` içeren bir nesne oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66143-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="66143-201">Bir sonraki adımda bir görünüm oluşturduğumuz zaman `AlbumSelectListViewModel` için projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="66143-202">`StoreManagerController`bir `EditVM` yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="66143-203">Tamamlanan kodu aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66143-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="66143-204">`AlbumSelectListViewModel`sağ tıklayın, **Çözümle**' yi ve ardından **MvcMusicStore. viewmodeller;** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="66143-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="66143-205">Alternatif olarak, aşağıdaki using ifadesini de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="66143-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="66143-206">`EditVM` sağ tıklayın ve **Görünüm Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="66143-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="66143-207">Aşağıda gösterilen seçenekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="66143-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="66143-208">**Ekle**' yi seçin, ardından *Views\storemanager\editvm.exe* dosyasının içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="66143-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="66143-209">`EditVM` biçimlendirmesi, özgün `Edit` biçimlendirmesine aşağıdaki özel durumlarla çok benzer.</span><span class="sxs-lookup"><span data-stu-id="66143-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="66143-210">`Edit` görünümündeki model özellikleri `model.property`form (örneğin, `model.Title`).</span><span class="sxs-lookup"><span data-stu-id="66143-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="66143-211">`EditVm` görünümündeki model özellikleri `model.Album.property`form (örneğin, `model.Album.Title`).</span><span class="sxs-lookup"><span data-stu-id="66143-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="66143-212">Çünkü `EditVM` görünümü `Edit` görünümünde olduğu gibi bir `Album` değil `Album`için bir kapsayıcı geçirmez.</span><span class="sxs-lookup"><span data-stu-id="66143-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="66143-213">**DropDownList** Second parametresi, **ViewBag**değil, görünüm modelinden gelir.</span><span class="sxs-lookup"><span data-stu-id="66143-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="66143-214">`EditVM` görünümündeki **BeginForm** Yardımcısı `Edit` eylem yöntemine açıkça geri gönderiler.</span><span class="sxs-lookup"><span data-stu-id="66143-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="66143-215">`Edit` eyleme geri döndüğünüzde, `HTTP POST EditVM` eylemi yazmak zorunda kalmaz ve `HTTP POST` `Edit` eylemini yeniden kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="66143-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="66143-216">Uygulamayı çalıştırın ve bir albümü düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="66143-216">Run the application and edit an album.</span></span> <span data-ttu-id="66143-217">`EditVM`kullanılacak URL 'YI değiştirin.</span><span class="sxs-lookup"><span data-stu-id="66143-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="66143-218">Bir alanı değiştirin ve kodun çalıştığını doğrulamak için **Kaydet** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="66143-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="66143-219">Hangi yaklaşımı kullanmalısınız?</span><span class="sxs-lookup"><span data-stu-id="66143-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="66143-220">Gösterilen üç yaklaşımdan bazıları kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="66143-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="66143-221">Birçok geliştirici, `ViewBag`kullanarak `DropDownList` `SelectList` açıkça geçirmeye tercih eder.</span><span class="sxs-lookup"><span data-stu-id="66143-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="66143-222">Bu yaklaşım, koleksiyon için daha uygun bir ad kullanma esnekliği sağlayan ek avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="66143-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="66143-223">Bir desteklenmediği uyarısıyla, `ViewBag SelectList` nesnesine model özelliği ile aynı adı verebilir.</span><span class="sxs-lookup"><span data-stu-id="66143-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="66143-224">Bazı geliştiriciler ViewModel yaklaşımını tercih eder.</span><span class="sxs-lookup"><span data-stu-id="66143-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="66143-225">Diğerleri daha ayrıntılı biçimlendirme ve ViewModel tarafından oluşturulan HTML 'nin bir dezavantajı olduğunu düşünsün.</span><span class="sxs-lookup"><span data-stu-id="66143-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="66143-226">Bu bölümde, kategori verileriyle **DropDownList** 'i kullanmanın üç yaklaşımını öğrendik.</span><span class="sxs-lookup"><span data-stu-id="66143-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="66143-227">Sonraki bölümde, yeni bir kategorinin nasıl ekleneceğini göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="66143-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="66143-228">[Önceki](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [İleri](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="66143-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>
