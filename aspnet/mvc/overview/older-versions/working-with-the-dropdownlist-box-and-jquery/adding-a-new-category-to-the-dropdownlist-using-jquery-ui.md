---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery kullanıcı arabirimini kullanarak DropDownList 'e yeni bir kategori ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538838"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="522ef-102">jQuery kullanıcı arabirimini kullanarak DropDownList’e Yeni Kategori ekleme</span><span class="sxs-lookup"><span data-stu-id="522ef-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="522ef-103">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="522ef-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="522ef-104">HTML `Select` etiketi, sabit kategori verilerinin bir listesini sunmak için idealdir, ancak genellikle yeni bir kategori eklemeniz gereken zamanlar.</span><span class="sxs-lookup"><span data-stu-id="522ef-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="522ef-105">"Opera" tarzımızı veritabanımız kategorilere eklemek istediğimizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="522ef-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="522ef-106">Bu bölümde, yeni bir kategori eklemek için kullanılabilecek bir iletişim kutusu eklemek için jQuery kullanıcı arabirimini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="522ef-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="522ef-107">Aşağıdaki görüntüde, Kullanıcı arabiriminin tarayıcıda nasıl bulunduğu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="522ef-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="522ef-108">Bir Kullanıcı **yeni tarz Ekle** bağlantısını seçtiğinde, bir açılan iletişim kutusu kullanıcıdan yeni bir tarz adı (ve isteğe bağlı olarak bir açıklama) ister.</span><span class="sxs-lookup"><span data-stu-id="522ef-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="522ef-109">Aşağıdaki görüntüde **tarzı Ekle** açılır iletişim kutusu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="522ef-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="522ef-110">Yeni bir tarz adı girildiğinde ve **Kaydet** düğmesi gönderildiğinde, şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="522ef-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="522ef-111">AJAX çağrısı, verileri yeni tarzı veritabanına kaydeden ve yeni tarz bilgilerini (tarz adı ve KIMLIĞI) JSON olarak döndüren tarzı denetleyicinin oluşturma yöntemine gönderir.</span><span class="sxs-lookup"><span data-stu-id="522ef-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="522ef-112">JavaScript yeni tarz verilerini seçim listesine ekler.</span><span class="sxs-lookup"><span data-stu-id="522ef-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="522ef-113">JavaScript yeni tarzı seçili öğe yapar.</span><span class="sxs-lookup"><span data-stu-id="522ef-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="522ef-114">Aşağıdaki görüntüde, **Opera** veritabanına eklendi ve **tarz** açılan listesinde seçildi.</span><span class="sxs-lookup"><span data-stu-id="522ef-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="522ef-115">*Views\storemanager\create5cshtml* dosyasını açın ve tarz işaretlemesini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="522ef-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="522ef-116">`_ChooseGenre` kısmi görünümü, yeni tarz Ekle özelliğini uygulamak için kullanılan JavaScript ve jQuery 'i bağlamak için tüm mantığı içerir.</span><span class="sxs-lookup"><span data-stu-id="522ef-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="522ef-117">Kodu tamamladıktan sonra, sanatçı Kullanıcı arabirimi ile aynı yapmak basit olacaktır.</span><span class="sxs-lookup"><span data-stu-id="522ef-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="522ef-118">Çözüm Gezgini, *Views\storemanager* klasörüne sağ tıklayın ve **Ekle**' yi ve ardından **görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="522ef-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="522ef-119">**Görünüm adı** girişinde `_ChooseGenre` girin ve ardından **Ekle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="522ef-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="522ef-120">*Views\storemanager\\_ChooseGenre. cshtml* dosyasındaki biçimlendirmeyi aşağıdakiler ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="522ef-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="522ef-121">İlk satır, modelimiz olarak bir `Album` geçirdiğimiz ve oluşturma görünümünde tam olarak aynı model bildiriminin bulunduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="522ef-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="522ef-122">Sonraki birkaç satır **etiket** Yardımcısı işaretlemedir.</span><span class="sxs-lookup"><span data-stu-id="522ef-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="522ef-123">Sonraki satır, özgün oluşturma görünümündeki ile tam olarak aynı olan **DropDownList** yardımcı çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="522ef-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="522ef-124">Sonraki satır, `Add New Genre`adıyla bir bağlantı ekler ve bir düğme gibi stillerdir.</span><span class="sxs-lookup"><span data-stu-id="522ef-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="522ef-125">`ValidationMessageFor` içeren çizgi doğrudan oluştur görünümünden kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="522ef-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="522ef-126">Aşağıdaki satırlar:</span><span class="sxs-lookup"><span data-stu-id="522ef-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="522ef-127">`genreDialog`KIMLIKLI gizli bir div oluşturur.</span><span class="sxs-lookup"><span data-stu-id="522ef-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="522ef-128">Bu div içindeki ID `genreDialog` **tarz Ekle** iletişim kutusumuzu bağlamak için jQuery kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="522ef-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="522ef-129">Son iki betik etiketi, yeni tarz Ekle özelliğini uygulamak için kullanacağız JavaScript dosyalarının bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="522ef-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="522ef-130">*/Scripts/chooseGenre.js* dosyası projede sizin için verilmiştir. bu işlemi öğreticide daha sonra inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="522ef-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="522ef-131">Uygulamayı çalıştırın ve **yeni tarz Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="522ef-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="522ef-132">**Tarz Ekle** Iletişim kutusunda **ad** giriş kutusuna **Opera** girin.</span><span class="sxs-lookup"><span data-stu-id="522ef-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="522ef-133">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="522ef-133">Click the **Save** button.</span></span> <span data-ttu-id="522ef-134">AJAX çağrısı Opera kategorisini oluşturur ve ardından açılan listeyi Opera ile doldurur ve Opera 'yı seçili tarz olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="522ef-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="522ef-135">Bir sanatçı, başlık ve fiyat girin, ardından **Oluştur** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="522ef-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="522ef-136">$8,99 'den düşük bir fiyat girerseniz, yeni albüm Dizin görünümünün en üstünde görünür.</span><span class="sxs-lookup"><span data-stu-id="522ef-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="522ef-137">Yeni albüm girişinin veritabanına kaydedildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="522ef-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="522ef-138">Yalnızca bir harfle yeni bir tarz oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="522ef-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="522ef-139">*Models\genre.cs* dosyasında bulunan aşağıdaki kod, tarz adının minimum ve maksimum uzunluğunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="522ef-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="522ef-140">İstemci tarafı doğrulama raporları 2 ila 20 karakter arasında bir dize girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="522ef-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="522ef-141">Veritabanına ve seçim listesine yeni bir tarz eklendiğini İnceleme.</span><span class="sxs-lookup"><span data-stu-id="522ef-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="522ef-142">*Scripts\chooseGenre.js* dosyasını açın ve kodu inceleyin.</span><span class="sxs-lookup"><span data-stu-id="522ef-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="522ef-143">İkinci satır, *Views\storemanager\\_ChooseGenre. cshtml* dosyasındaki div etiketinde bir iletişim kutusu oluşturmak için kimlik `genreDialog` kullanır.</span><span class="sxs-lookup"><span data-stu-id="522ef-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="522ef-144">Adlandırılmış parametrelerin çoğu kendi kendine açıklayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="522ef-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="522ef-145">`autoOpen` parametresi false olarak ayarlanır, **tarz oluştur** düğmesi seçildiğinde iletişim kutusu açıkça açılır (Bu, ikinci üzerinde açıklanmıştır).</span><span class="sxs-lookup"><span data-stu-id="522ef-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="522ef-146">İletişim kutusunda iki düğme bulunur, **Kaydet** ve **iptal et**.</span><span class="sxs-lookup"><span data-stu-id="522ef-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="522ef-147">**İptal** düğmesi iletişim kutusunu kapatır.</span><span class="sxs-lookup"><span data-stu-id="522ef-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="522ef-148">Aşağıdaki kodda **Kaydet** düğmesi işlevi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="522ef-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="522ef-149">`var createGenreForm` `createGenreForm` KIMLIĞINDEN seçilir.</span><span class="sxs-lookup"><span data-stu-id="522ef-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="522ef-150">`createGenreForm` KIMLIĞI, *Views\tarz\\_CreateGenre. cshtml* dosyasında bulunan aşağıdaki kodda ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="522ef-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="522ef-151">*Views\tarz\\_CreateGenre. cshtml* dosyasında kullanılan [HTML. BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) yardımcı aşırı yüklemesi, formu göndermek için URL 'yi IÇEREN bir Action özniteliğiyle HTML oluşturur.</span><span class="sxs-lookup"><span data-stu-id="522ef-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="522ef-152">Bu bunu, bir tarayıcıda albüm oluştur sayfasını görüntüleyerek ve kaynağı tarayıcıda göster ' i seçerek görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="522ef-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="522ef-153">Aşağıdaki biçimlendirme form etiketini içeren oluşturulan HTML 'yi gösterir.</span><span class="sxs-lookup"><span data-stu-id="522ef-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="522ef-154">JQuery `$.post` satırı eylem özniteliğine (`/StoreManager/Create`) bir AJAX çağrısı yapar ve **tarz oluştur** iletişim kutusundan verileri geçirir.</span><span class="sxs-lookup"><span data-stu-id="522ef-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="522ef-155">Veriler, yeni tarz için ad ve isteğe bağlı bir açıklama içerir.</span><span class="sxs-lookup"><span data-stu-id="522ef-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="522ef-156">AJAX çağrısı başarılı olursa, yeni tarz adı ve değeri seçim biçimlendirmesine eklenir ve yeni tarz seçili değere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="522ef-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="522ef-157">Bu, dinamik olarak oluşturulan biçimlendirme olduğundan, kaynağı tarayıcıda görüntüleyerek yeni seçim seçeneğini göremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="522ef-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="522ef-158">IE 9 F12 geliştirici araçlarıyla yeni HTML 'yi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="522ef-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="522ef-159">Yeni seçim seçeneğini görüntülemek için, Internet Explorer 9 ' da F12 Geliştirici Araçları ' nı başlatmak için F12 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="522ef-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="522ef-160">Oluştur sayfasına gidin ve yeni bir tarz ekleyin, bu nedenle tarz seçim listesinde yeni tarz seçilir.</span><span class="sxs-lookup"><span data-stu-id="522ef-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="522ef-161">F12 geliştirici araçlarında:</span><span class="sxs-lookup"><span data-stu-id="522ef-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="522ef-162">HTML sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="522ef-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="522ef-163">Yenile simgesine basın.</span><span class="sxs-lookup"><span data-stu-id="522ef-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="522ef-164">Arama kutusuna Genreıd girin.</span><span class="sxs-lookup"><span data-stu-id="522ef-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="522ef-165">İleri simgesini kullanarak,</span><span class="sxs-lookup"><span data-stu-id="522ef-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="522ef-166">Şu seçme etiketine gidin:</span><span class="sxs-lookup"><span data-stu-id="522ef-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="522ef-167">Son seçenek değerini genişletin.</span><span class="sxs-lookup"><span data-stu-id="522ef-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="522ef-168">*Scripts\chooseGenre.js* dosyasında aşağıdaki kod, **yeni tarz Ekle** düğmesinin tıklama olayına nasıl bağlandığını ve **yeni tarz Ekle** iletişim kutusunun nasıl oluşturulduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="522ef-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="522ef-169">İlk satır, **yeni tarz Ekle** düğmesine iliştirilmiş bir tıklama işlevi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="522ef-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="522ef-170">Views\StoreManager\\_ChooseGenre. cshtml dosyasından aşağıdaki biçimlendirme, **yeni tarz Ekle** düğmesinin nasıl oluşturulduğunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="522ef-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="522ef-171">Load yöntemi, tarz Ekle iletişim kutusunu oluşturup açar ve jQuery `parse` yöntemini çağırarak, iletişim kutusunda girilen verilerde istemci doğrulaması gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="522ef-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="522ef-172">Bu bölümde, bir seçim listesine yeni kategori verileri eklemek için kullanılabilecek bir iletişim kutusu oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="522ef-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="522ef-173">Sanatçı seçim listesine yeni bir sanatçı eklemek için Kullanıcı arabirimi oluşturmak üzere aynı yordamı izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="522ef-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="522ef-174">Bu öğreticide, ASP.NET MVC HTML Yardımcısı **DropDownList**ile çalışmaya genel bakış verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="522ef-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="522ef-175">**DropDownList**ile çalışma hakkında daha fazla bilgi için, aşağıdaki başvuruları ekleme bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="522ef-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="522ef-176">Lütfen Bu öğreticinin yararlı olup olmadığını bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="522ef-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="522ef-177">Rick. Anderson [at] Microsoft. com</span><span class="sxs-lookup"><span data-stu-id="522ef-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="522ef-178">Ek başvurular</span><span class="sxs-lookup"><span data-stu-id="522ef-178">Additional References</span></span>

- <span data-ttu-id="522ef-179">[ASP.NET MVC – geçişli aşağı açılan liste öğreticisini](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [oydu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="522ef-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="522ef-180">[Seçili](https://harvesthq.github.com/chosen/) Çoklu Seçme ve filtrelemeyi destekleyen bir JavaScript eklentisi.</span><span class="sxs-lookup"><span data-stu-id="522ef-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="522ef-181">Katkıda Bulunanlar</span><span class="sxs-lookup"><span data-stu-id="522ef-181">Contributors</span></span>

- [<span data-ttu-id="522ef-182">ÇDU Enuca</span><span class="sxs-lookup"><span data-stu-id="522ef-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="522ef-183">Jean-Sébastien Goupıl</span><span class="sxs-lookup"><span data-stu-id="522ef-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="522ef-184">Atacan Solson</span><span class="sxs-lookup"><span data-stu-id="522ef-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="522ef-185">Gözden Geçirenler</span><span class="sxs-lookup"><span data-stu-id="522ef-185">Reviewers</span></span>

- <span data-ttu-id="522ef-186">Jean-Sébastien Goupıl</span><span class="sxs-lookup"><span data-stu-id="522ef-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="522ef-187">Atacan Solson</span><span class="sxs-lookup"><span data-stu-id="522ef-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="522ef-188">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="522ef-188">Mike Pope</span></span>
- <span data-ttu-id="522ef-189">Tom Dykstra</span><span class="sxs-lookup"><span data-stu-id="522ef-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="522ef-190">Öncekini</span><span class="sxs-lookup"><span data-stu-id="522ef-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
