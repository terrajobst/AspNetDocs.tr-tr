---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET Web sayfalarına giriş-veritabanı verilerini silme | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, tek bir veritabanı girişinin nasıl silineceği gösterilir. ASP.NET Web PA 'de veritabanı verilerini güncelleştirerek seriyi tamamladığınız varsayılmaktadır...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629040"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="43d08-104">ASP.NET Web sayfalarına giriş-veritabanı verilerini silme</span><span class="sxs-lookup"><span data-stu-id="43d08-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="43d08-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="43d08-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="43d08-106">Bu öğreticide, tek bir veritabanı girişinin nasıl silineceği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="43d08-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="43d08-107">[ASP.NET Web sayfalarındaki veritabanı verilerini güncelleştirerek](updating-data.md)seriyi tamamladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="43d08-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="43d08-108">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="43d08-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="43d08-109">Kayıt listesinden tek bir kayıt seçme.</span><span class="sxs-lookup"><span data-stu-id="43d08-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="43d08-110">Veritabanından tek bir kaydı silme.</span><span class="sxs-lookup"><span data-stu-id="43d08-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="43d08-111">Bir formda belirli bir düğmenin tıklandığını denetleme.</span><span class="sxs-lookup"><span data-stu-id="43d08-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="43d08-112">Ele alınan özellikler/teknolojiler:</span><span class="sxs-lookup"><span data-stu-id="43d08-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="43d08-113">`WebGrid` Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="43d08-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="43d08-114">SQL `Delete` komutu.</span><span class="sxs-lookup"><span data-stu-id="43d08-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="43d08-115">Bir SQL `Delete` komutu çalıştırmak için `Database.Execute` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="43d08-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="43d08-116">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="43d08-116">What You'll Build</span></span>

<span data-ttu-id="43d08-117">Önceki öğreticide, var olan bir veritabanı kaydını güncelleştirmeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="43d08-118">Bu öğretici benzerdir, çünkü kaydı güncelleştirmek yerine onu silersiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="43d08-119">Süreçler çok daha basit olduğundan, bu öğretici bu öğreticiyi bir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="43d08-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="43d08-120">*Filmler* sayfasında, daha önce eklediğiniz **düzenleme** bağlantısına eşlik etmek için `WebGrid` yardımcısını her filmin yanında bir **silme** bağlantısı görüntüleyecek şekilde güncelleştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![Her film için silme bağlantısı gösteren filmler sayfası](deleting-data/_static/image1.png)

<span data-ttu-id="43d08-122">Düzenlemede olduğu gibi, **Sil** bağlantısına tıkladığınızda, sizi film bilgisinin zaten bir biçimde olduğu farklı bir sayfaya götürür:</span><span class="sxs-lookup"><span data-stu-id="43d08-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![Bir film görüntülenirken film sayfasını Sil](deleting-data/_static/image2.png)

<span data-ttu-id="43d08-124">Ardından, kaydı kalıcı olarak silmek için düğmeye tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="43d08-125">Film listesine silme bağlantısı ekleme</span><span class="sxs-lookup"><span data-stu-id="43d08-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="43d08-126">`WebGrid` Yardımcısı 'na **silme** bağlantısı ekleyerek başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="43d08-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="43d08-127">Bu bağlantı, önceki bir öğreticide eklediğiniz **düzenleme** bağlantısına benzer.</span><span class="sxs-lookup"><span data-stu-id="43d08-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="43d08-128">*Filmler. cshtml* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="43d08-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="43d08-129">Sütun ekleyerek sayfanın gövdesindeki `WebGrid` işaretlemesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="43d08-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="43d08-130">Değiştirilen biçimlendirme şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="43d08-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="43d08-131">Yeni sütun budur:</span><span class="sxs-lookup"><span data-stu-id="43d08-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="43d08-132">Kılavuzun yapılandırıldığı şekilde, **düzenleme** sütunu kılavuzda en solda, **silme** sütunu ise en sağdaki bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="43d08-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="43d08-133">(Bunu fark etmediğiniz durumlarda `Year` sütundan sonra bir virgül vardır.) Bu bağlantı sütunlarının nereye gittiğine ilişkin hiçbir şey yoktur ve bunların yanına kolayca yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="43d08-134">Bu durumda, karışık bir şekilde yararlanmak daha zor hale getirmek için ayrıdır.</span><span class="sxs-lookup"><span data-stu-id="43d08-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![Düzenleme ve ayrıntı bağlantıları içeren filmler sayfası, birbirini ileri bir yanından gösterme](deleting-data/_static/image3.png)

<span data-ttu-id="43d08-136">Yeni sütun, metni "Sil" ifadesini içeren bir bağlantıyı (`<a>` öğesi) gösterir.</span><span class="sxs-lookup"><span data-stu-id="43d08-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="43d08-137">Bağlantının hedefi (`href` özniteliği), son olarak, her film için `id` değeri farklı olan bu URL gibi bir şekilde çözümlenen koddur:</span><span class="sxs-lookup"><span data-stu-id="43d08-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="43d08-138">Bu bağlantı, *deletefilm* adlı bir sayfayı çağırır ve SEÇTIĞINIZ filmin kimliğini iletmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="43d08-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="43d08-139">Bu öğretici, önceki öğreticideki **düzenleme** bağlantısı ile neredeyse özdeş olduğundan ([ASP.NET Web sayfalarındaki veritabanı verilerini güncelleştirme](updating-data.md)) Bu bağlantının nasıl oluşturulduğu hakkında ayrıntı vermez.</span><span class="sxs-lookup"><span data-stu-id="43d08-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="43d08-140">Silme sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="43d08-140">Creating the Delete Page</span></span>

<span data-ttu-id="43d08-141">Artık kılavuzdaki **Delete** bağlantısının hedefi olacak sayfayı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="43d08-142">**Önemli** İlk olarak silmek için bir kayıt seçme ve sonra ayrı bir sayfa ve düğme kullanarak işlemin güvenlik açısından çok önemli olduğunu belirleme tekniği.</span><span class="sxs-lookup"><span data-stu-id="43d08-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="43d08-143">Önceki öğreticilerde okuduğunuzdan, Web sitenizde *herhangi* bir değişiklik yapmak *her zaman* bir HTTP POST işlemi kullanılarak &mdash; bir form kullanılarak yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="43d08-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="43d08-144">Yalnızca bir bağlantıya tıklayarak (yani, bir GET işlemi kullanarak) siteyi değiştirmeyi mümkün kıldıysanız, kişiler sitenize basit istekler yapabilir ve verilerinizi silebilir.</span><span class="sxs-lookup"><span data-stu-id="43d08-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="43d08-145">Sitenizi dizine alan bir arama motoru Gezgini bile, verileri yanlışlıkla izleyen bağlantıları yanlışlıkla silebilir.</span><span class="sxs-lookup"><span data-stu-id="43d08-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="43d08-146">Uygulamanız kişilerin bir kaydı değiştirmesine izin veriyorsun, kaydı kullanıcıya yine de düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="43d08-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="43d08-147">Ancak bir kaydı silmek için bu adımı atlamayı düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="43d08-148">Bu adımı atlayın, ancak.</span><span class="sxs-lookup"><span data-stu-id="43d08-148">Don't skip that step, though.</span></span> <span data-ttu-id="43d08-149">(Kullanıcıların kaydı görmesini ve hedeflediğiniz kaydı sildiklerini onaylamasını de yararlı olur.)</span><span class="sxs-lookup"><span data-stu-id="43d08-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="43d08-150">Sonraki bir öğretici kümesinde, kullanıcının bir kaydı silmeden önce oturum açması için oturum açma işlevselliği ekleme hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="43d08-151">*Deletemovie. cshtml* adlı bir sayfa oluşturun ve dosyadaki nelerin aşağıdaki biçimlendirmeyle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="43d08-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="43d08-152">Bu biçimlendirme *Editmovie* sayfaları gibi olduğundan, metin kutuları (`<input type="text">`) kullanmak yerine, biçimlendirme `<span>` öğelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="43d08-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="43d08-153">Burada düzenlemek için bir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="43d08-153">There's nothing here to edit.</span></span> <span data-ttu-id="43d08-154">Tüm yapmanız gereken, kullanıcıların doğru filmi sildiklerinden emin olmak için film ayrıntılarını görüntüleriz.</span><span class="sxs-lookup"><span data-stu-id="43d08-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="43d08-155">Biçimlendirme zaten kullanıcının film listesi sayfasına dönüşmesine izin veren bir bağlantı içeriyor.</span><span class="sxs-lookup"><span data-stu-id="43d08-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="43d08-156">*Editmovie* sayfasında, SEÇILI filmin kimliği gizli bir alanda saklanır.</span><span class="sxs-lookup"><span data-stu-id="43d08-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="43d08-157">(Bu, ilk yerde bir sorgu dizesi değeri olarak sayfaya geçirilir.) Doğrulama hatalarını görüntüleyen bir `Html.ValidationSummary` çağrısı vardır.</span><span class="sxs-lookup"><span data-stu-id="43d08-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="43d08-158">Bu durumda hata, sayfaya hiçbir film KIMLIĞI geçirilmemişse veya film KIMLIĞI geçersiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="43d08-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="43d08-159">Bu durum, birisi önce *filmler* sayfasında bir filmi seçmeden bu sayfayı çalıştırmışsa meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="43d08-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="43d08-160">Düğme başlığı **filmi siler**ve ad özniteliği `buttonDelete`olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="43d08-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="43d08-161">`name` özniteliği, formu gönderen düğmeyi tanımlamak için kodda kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="43d08-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="43d08-162">1 ' e kod yazmanız gerekir) sayfa ilk görüntülendiğinde film ayrıntılarını okumak ve 2) aslında Kullanıcı düğmeye tıkladığında filmi silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="43d08-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="43d08-163">Tek bir filmi okumak için kod ekleme</span><span class="sxs-lookup"><span data-stu-id="43d08-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="43d08-164">*Deletemovie. cshtml* sayfasının en üstünde aşağıdaki kod bloğunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="43d08-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="43d08-165">Bu biçimlendirme, *Editmovie* sayfasındaki karşılık gelen kodla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="43d08-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="43d08-166">Film KIMLIĞINI sorgu dizesinden alır ve veritabanından bir kaydı okumak için KIMLIĞI kullanır.</span><span class="sxs-lookup"><span data-stu-id="43d08-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="43d08-167">Kod, sayfaya geçirilen film KIMLIĞININ geçerli olduğundan emin olmak için doğrulama testini (`IsInt()` ve `row != null`) içerir.</span><span class="sxs-lookup"><span data-stu-id="43d08-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="43d08-168">Bu kodun yalnızca sayfa ilk kez çalıştığında çalışacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="43d08-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="43d08-169">Kullanıcı **filmi Sil** düğmesine tıkladığında film kaydını veritabanından yeniden okumak istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="43d08-170">Bu nedenle, filmi okuma kodu, *istek bir POST işlemi değilse (form gönderimi)* `if(!IsPost)` &mdash; belirten bir test içindedir.</span><span class="sxs-lookup"><span data-stu-id="43d08-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="43d08-171">Seçili filmi silmek için kod ekleme</span><span class="sxs-lookup"><span data-stu-id="43d08-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="43d08-172">Kullanıcı düğmeye tıkladığında filmi silmek için, `@` bloğunun kapanış ayracın içine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="43d08-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="43d08-173">Bu kod, var olan bir kaydın güncelleştirilmesine yönelik koda benzerdir, ancak daha basittir.</span><span class="sxs-lookup"><span data-stu-id="43d08-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="43d08-174">Kod temelde bir SQL `Delete` ifadesini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="43d08-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="43d08-175">*Editmovie* sayfasında olduğu gibi, kod `if(IsPost)` bloğudur.</span><span class="sxs-lookup"><span data-stu-id="43d08-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="43d08-176">Bu kez `if()` koşulu biraz daha karmaşıktır:</span><span class="sxs-lookup"><span data-stu-id="43d08-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="43d08-177">Burada iki koşul vardır.</span><span class="sxs-lookup"><span data-stu-id="43d08-177">There are two conditions here.</span></span> <span data-ttu-id="43d08-178">Birincisi, &mdash; `if(IsPost)`önce gördüğünüz gibi sayfanın gönderilme sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="43d08-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="43d08-179">İkinci koşul `!Request["buttonDelete"].IsEmpty()`, isteğin `buttonDelete`adlı bir nesneye sahip olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="43d08-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="43d08-180">Admitetki, formu hangi düğmenin gönderdiğine yönelik dolaylı bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="43d08-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="43d08-181">Form birden çok Gönder düğmesi içeriyorsa, istekte yalnızca tıklanan düğmenin adı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="43d08-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="43d08-182">Bu nedenle, mantıksal olarak, belirli bir düğmenin adı istek &mdash; veya kodda belirtilen şekilde görünüyorsa, bu düğme boş değilse formu gönderen düğmedir &mdash;.</span><span class="sxs-lookup"><span data-stu-id="43d08-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="43d08-183">`&&` işleci "and" (Logical ve) anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="43d08-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="43d08-184">Bu nedenle `if` koşulu tamamen...</span><span class="sxs-lookup"><span data-stu-id="43d08-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="43d08-185">*Bu istek bir gönderi (ilk kez istek değil)*</span><span class="sxs-lookup"><span data-stu-id="43d08-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="43d08-186">AND</span><span class="sxs-lookup"><span data-stu-id="43d08-186">AND</span></span>  
  
<span data-ttu-id="43d08-187">*`buttonDelete`* *düğmesi formu gönderen düğmedir.*</span><span class="sxs-lookup"><span data-stu-id="43d08-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="43d08-188">Bu form (Aslında, Bu sayfa) yalnızca bir düğme içerir, bu nedenle `buttonDelete` ek testi Teknik olarak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="43d08-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="43d08-189">Hala, verileri kalıcı olarak kaldıracak bir işlem gerçekleştirmeye çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="43d08-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="43d08-190">Bu nedenle, işlemi yalnızca kullanıcı açıkça talep edildiğinde gerçekleştirdiğinizden emin olmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="43d08-191">Örneğin, bu sayfayı daha sonra genişletdiğinizi ve diğer düğmeleri daha sonra eklediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="43d08-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="43d08-192">Daha sonra bile, filmi silen kod yalnızca `buttonDelete` düğmesi tıklandıysa çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="43d08-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="43d08-193">*Editmovie* sayfasında, gızlı alandan kimliği alır ve sonra SQL komutunu çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="43d08-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="43d08-194">`Delete` deyimin sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="43d08-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="43d08-195">`WHERE` yan tümcesini ve KIMLIĞINI eklemek çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="43d08-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="43d08-196">WHERE yan tümcesini bıraktığınızda, *tablodaki tüm kayıtlar silinir*.</span><span class="sxs-lookup"><span data-stu-id="43d08-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="43d08-197">Gördüğünüz gibi, bir yer tutucu kullanarak KIMLIK değerini SQL komutuna geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="43d08-198">Film silme Işlemini test etme</span><span class="sxs-lookup"><span data-stu-id="43d08-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="43d08-199">Artık test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-199">Now you can test.</span></span> <span data-ttu-id="43d08-200">*Filmler* sayfasını çalıştırın ve filmin yanındaki **Sil** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43d08-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="43d08-201">*Deletemovie* sayfası göründüğünde **filmi Sil**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43d08-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![Filmi Sil düğmesinin vurgulandığı film sayfasını Sil](deleting-data/_static/image4.png)

<span data-ttu-id="43d08-203">Düğmeye tıkladığınızda, kod filmleri siler ve film listesine geri döner.</span><span class="sxs-lookup"><span data-stu-id="43d08-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="43d08-204">Silinen filmi arayabilir ve silindiğini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43d08-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="43d08-205">Sonraki adımda</span><span class="sxs-lookup"><span data-stu-id="43d08-205">Coming Up Next</span></span>

<span data-ttu-id="43d08-206">Sonraki öğreticide, sitenizdeki tüm sayfalara ortak bir görünüm ve düzen verme konusu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="43d08-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="43d08-207">Film sayfası için komple liste (silme bağlantılarıyla güncelleştirildi)</span><span class="sxs-lookup"><span data-stu-id="43d08-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="43d08-208">DeleteMovie sayfası için komple liste</span><span class="sxs-lookup"><span data-stu-id="43d08-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="43d08-209">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="43d08-209">Additional Resources</span></span>

- [<span data-ttu-id="43d08-210">Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş</span><span class="sxs-lookup"><span data-stu-id="43d08-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="43d08-211">W3Schools sitesindeki [SQL DELETE deyimleri](http://www.w3schools.com/sql/sql_delete.asp)</span><span class="sxs-lookup"><span data-stu-id="43d08-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="43d08-212">[Önceki](updating-data.md)
> [İleri](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="43d08-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
