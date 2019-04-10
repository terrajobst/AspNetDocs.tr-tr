---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: "ASP.NET Web API'de HTML Form verileri gönderme: Karşıya dosya yükleme ve çok parçalı MIME - ASP.NET 4.x"
author: MikeWasson
description: Bu öğreticide, bir web API'sine dosyaları karşıya yükleme işlemi gösterilmektedir. Ayrıca, çok parçalı MIME verilerin nasıl işleneceğini açıklar.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 70e150a32f208cf75086f959d484d86e8501c6bd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419931"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="c508e-104">ASP.NET Web API'de HTML Form verileri gönderme: Karşıya Dosya Yükleme ve Çok Parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="c508e-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="c508e-105">tarafından [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c508e-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="c508e-106">Bölüm 2: Karşıya Dosya Yükleme ve Çok Parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="c508e-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="c508e-107">Bu öğreticide, bir web API'sine dosyaları karşıya yükleme işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c508e-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="c508e-108">Ayrıca, çok parçalı MIME verilerin nasıl işleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="c508e-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="c508e-109">[Tamamlanmış projeyi indirmek](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span><span class="sxs-lookup"><span data-stu-id="c508e-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="c508e-110">Bir dosyayı yüklemek için bir HTML formuna bir örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c508e-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="c508e-111">Bu form, metin girişi denetimi ve dosya giriş denetimi içerir.</span><span class="sxs-lookup"><span data-stu-id="c508e-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="c508e-112">Bir formu bir dosya giriş denetimini içerdiğinde **Notenctype** özniteliği uymanız gereken &quot;multipart/form-data&quot;, belirten form çok parçalı MIME ileti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c508e-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="c508e-113">Çok parçalı MIME ileti biçimi bir örnek isteğiyle bakarak anlamak oldukça kolaydır:</span><span class="sxs-lookup"><span data-stu-id="c508e-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="c508e-114">Bu ileti ikiye bölünür *bölümleri*, her form denetimi için bir tane.</span><span class="sxs-lookup"><span data-stu-id="c508e-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="c508e-115">Bölüm sınırları, kısa çizgi ile başlayan satırları tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="c508e-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="c508e-116">Bölüm sınırının rastgele bir bileşeni içerir (&quot;41184676334&quot;) sınır dize yanlışlıkla bir ileti bölümü içinde görünmüyor emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="c508e-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="c508e-117">Bölüm içeriğine göre ve ardından bir veya daha fazla üst bilgileri, her ileti bölümü içerir.</span><span class="sxs-lookup"><span data-stu-id="c508e-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="c508e-118">İçerik düzeni üstbilgisini denetimin adını içerir.</span><span class="sxs-lookup"><span data-stu-id="c508e-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="c508e-119">Dosyalar için dosya adı da içerir.</span><span class="sxs-lookup"><span data-stu-id="c508e-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="c508e-120">Content-Type üstbilgisi veri bölümünde açıklanır.</span><span class="sxs-lookup"><span data-stu-id="c508e-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="c508e-121">Bu üst bilgisi çıkarılırsa, metin/düz varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="c508e-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="c508e-122">Önceki örnekte, kullanıcı GrandCanyon.jpg, içerik türü görüntü/jpeg ile adlı bir dosya karşıya; ve metin girişi değerini &quot;Yaz tatil&quot;.</span><span class="sxs-lookup"><span data-stu-id="c508e-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="c508e-123">Karşıya dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="c508e-123">File Upload</span></span>

<span data-ttu-id="c508e-124">Artık dosyaları çok parçalı MIME iletiden okuyan bir Web API denetleyicisi göz atalım.</span><span class="sxs-lookup"><span data-stu-id="c508e-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="c508e-125">Denetleyici dosyaları zaman uyumsuz olarak okur.</span><span class="sxs-lookup"><span data-stu-id="c508e-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="c508e-126">Web API'si kullanarak zaman uyumsuz eylemleri destekleyen [görev-tabanlı programlama modeli](https://msdn.microsoft.com/library/dd460693.aspx).</span><span class="sxs-lookup"><span data-stu-id="c508e-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="c508e-127">İlk olarak, kod aşağıdaki gibidir destekleyen .NET Framework 4.5 hedefliyorsanız **zaman uyumsuz** ve **await** anahtar sözcükleri.</span><span class="sxs-lookup"><span data-stu-id="c508e-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="c508e-128">Denetleyici eylemini herhangi bir parametre almaz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c508e-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="c508e-129">Medya türü biçimlendiricisi çağırmadan biz eylem içinde istek gövdesini işlemek olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c508e-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="c508e-130">**IsMultipartContent** yöntemi isteği çok parçalı MIME ileti içerip içermediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="c508e-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="c508e-131">Aksi durumda, denetleyici, HTTP durum kodu 415 (desteklenmeyen medya türü) döndürür.</span><span class="sxs-lookup"><span data-stu-id="c508e-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="c508e-132">**MultipartFormDataStreamProvider** sınıfı, karşıya yüklenen dosyalar için dosya akışları ayıran bir yardımcı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="c508e-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="c508e-133">MIME çok bölümlü iletinin okumak için çağrı **ReadAsMultipartAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c508e-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="c508e-134">Bu yöntem tüm ileti parçalarını ayıklar ve bunları tarafından sağlanan akışları Yazar **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="c508e-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="c508e-135">Yöntemi tamamlandığında, dosyaları hakkında bilgi edinebilirsiniz **FileData** koleksiyonu özelliğinin, **MultipartFileData** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="c508e-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="c508e-136">**MultipartFileData.FileName** dosyanın kaydedildiği sunucusunda, yerel dosya adı.</span><span class="sxs-lookup"><span data-stu-id="c508e-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="c508e-137">**MultipartFileData.Headers** bölüm başlığı içerir (*değil* istek üst bilgisi).</span><span class="sxs-lookup"><span data-stu-id="c508e-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="c508e-138">Bu içeriğe erişmek için kullanabileceğiniz\_değerlendirme ve Content-Type üst bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c508e-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="c508e-139">Adından da anlaşılacağı gibi **ReadAsMultipartAsync** zaman uyumsuz bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="c508e-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="c508e-140">Yöntemi tamamlandığında iş gerçekleştirmek için bir [devamlılık görevi](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) veya **await** anahtar sözcüğü (.NET 4.5).</span><span class="sxs-lookup"><span data-stu-id="c508e-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="c508e-141">Önceki kod .NET Framework 4.0 sürümünü şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="c508e-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="c508e-142">Form denetimi verileri okuma</span><span class="sxs-lookup"><span data-stu-id="c508e-142">Reading Form Control Data</span></span>

<span data-ttu-id="c508e-143">Daha önce gösterilen HTML formu, bir metin girişi denetimi vardı.</span><span class="sxs-lookup"><span data-stu-id="c508e-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="c508e-144">Denetim değer elde edebileceği **çıkışlardan form verisi** özelliği **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="c508e-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="c508e-145">**Çıkışlardan form verisi** olduğu bir **NameValueCollection** , form denetimleri için ad/değer çiftleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c508e-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="c508e-146">Koleksiyonda yinelenen anahtarlar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c508e-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="c508e-147">Bu formu göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="c508e-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="c508e-148">İstek gövdesi şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="c508e-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="c508e-149">Bu durumda, **çıkışlardan form verisi** aşağıdaki anahtar/değer çiftleri koleksiyonu içerebilir:</span><span class="sxs-lookup"><span data-stu-id="c508e-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="c508e-150">Seyahat: gidiş dönüş</span><span class="sxs-lookup"><span data-stu-id="c508e-150">trip: round-trip</span></span>
- <span data-ttu-id="c508e-151">Seçenekler: nonstop</span><span class="sxs-lookup"><span data-stu-id="c508e-151">options: nonstop</span></span>
- <span data-ttu-id="c508e-152">Seçenekler: tarih</span><span class="sxs-lookup"><span data-stu-id="c508e-152">options: dates</span></span>
- <span data-ttu-id="c508e-153">Lisans: penceresi</span><span class="sxs-lookup"><span data-stu-id="c508e-153">seat: window</span></span>
