---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: "ASP.NET Web API 'sinde HTML form verileri gönderme: dosya yükleme ve çok parçalı MIME-ASP.NET 4. x"
author: MikeWasson
description: Bu öğreticide, bir Web API 'sine dosya yükleme işleminin nasıl yapılacağı gösterilmektedir. Ayrıca, çok parçalı MIME verilerinin nasıl işlenmesi açıklanmaktadır.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557570"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="89b24-104">ASP.NET Web API 'sinde HTML form verileri gönderme: dosya yükleme ve çok parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="89b24-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="89b24-105">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="89b24-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="89b24-106">Bölüm 2: dosya yükleme ve çok parçalı MIME</span><span class="sxs-lookup"><span data-stu-id="89b24-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="89b24-107">Bu öğreticide, bir Web API 'sine dosya yükleme işleminin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="89b24-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="89b24-108">Ayrıca, çok parçalı MIME verilerinin nasıl işlenmesi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89b24-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="89b24-109">[Tamamlanmış projeyi indirin](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span><span class="sxs-lookup"><span data-stu-id="89b24-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="89b24-110">Bir dosyayı karşıya yüklemek için bir HTML formu örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="89b24-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="89b24-111">Bu form bir metin girişi denetimi ve bir dosya girişi denetimi içerir.</span><span class="sxs-lookup"><span data-stu-id="89b24-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="89b24-112">Form bir dosya girişi denetimi içerdiğinde, **Enctype** özniteliği her zaman &quot;multipart/form-Data&quot;olmalıdır ve bu, formun çok PARÇALı bir MIME iletisi olarak gönderileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="89b24-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="89b24-113">Bir çok parçalı MIME iletisinin biçimi, örnek bir isteğe bakarak anlaşılması en kolay yoldur:</span><span class="sxs-lookup"><span data-stu-id="89b24-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="89b24-114">Bu ileti, her form denetimi için bir tane olmak üzere iki *parçaya*bölünür.</span><span class="sxs-lookup"><span data-stu-id="89b24-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="89b24-115">Bölüm sınırları, tireler ile başlayan satırlar ile belirtilir.</span><span class="sxs-lookup"><span data-stu-id="89b24-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="89b24-116">Bölüm sınırı, sınır dizesinin yanlışlıkla bir ileti bölümü içinde görünmemesini sağlamak için rastgele bir bileşen (&quot;41184676334&quot;) içerir.</span><span class="sxs-lookup"><span data-stu-id="89b24-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="89b24-117">Her ileti parçası bir veya daha fazla üst bilgi içerir ve ardından bölüm içerikleri gelir.</span><span class="sxs-lookup"><span data-stu-id="89b24-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="89b24-118">Content-Disposition üst bilgisi, denetimin adını içerir.</span><span class="sxs-lookup"><span data-stu-id="89b24-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="89b24-119">Dosyalar için dosya adını da içerir.</span><span class="sxs-lookup"><span data-stu-id="89b24-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="89b24-120">Content-Type üst bilgisi, bölümündeki verileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="89b24-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="89b24-121">Bu üst bilgi atlanırsa, varsayılan metin/düz ' dır.</span><span class="sxs-lookup"><span data-stu-id="89b24-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="89b24-122">Önceki örnekte, Kullanıcı, Type Image/JPEG; içerik türü ile birlikte bir dosya olarak belirtilen bir dosyayı karşıya yükledi. ve metin girişinin değeri &quot;yaz tatili&quot;.</span><span class="sxs-lookup"><span data-stu-id="89b24-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="89b24-123">Karşıya dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="89b24-123">File Upload</span></span>

<span data-ttu-id="89b24-124">Şimdi çok parçalı bir MIME iletisinden dosyaları okuyan bir Web API denetleyicisine göz atalım.</span><span class="sxs-lookup"><span data-stu-id="89b24-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="89b24-125">Denetleyici dosyaları zaman uyumsuz olarak okur.</span><span class="sxs-lookup"><span data-stu-id="89b24-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="89b24-126">Web API 'SI, [görev tabanlı programlama modelini](https://msdn.microsoft.com/library/dd460693.aspx)kullanarak zaman uyumsuz eylemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="89b24-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="89b24-127">İlk olarak, **Async** ve **await** anahtar sözcüklerini destekleyen .NET Framework 4,5 ' i hedefliyorsanız, bu kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="89b24-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="89b24-128">Denetleyici eyleminin hiçbir parametre almaz.</span><span class="sxs-lookup"><span data-stu-id="89b24-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="89b24-129">Bunun nedeni, bir medya türü biçimlendirici çağırmadan, işlem içindeki istek gövdesini işletireceğiz.</span><span class="sxs-lookup"><span data-stu-id="89b24-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="89b24-130">**Imultipartcontent** yöntemi, isteğin çok PARÇALı bir MIME iletisi içerip içermediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="89b24-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="89b24-131">Aksi takdirde, denetleyici HTTP durum kodu 415 (desteklenmeyen medya türü) döndürür.</span><span class="sxs-lookup"><span data-stu-id="89b24-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="89b24-132">**Multipartformdatastreamprovider** sınıfı, karşıya yüklenen dosyalar için dosya akışlarını ayıran bir yardımcı nesnedir.</span><span class="sxs-lookup"><span data-stu-id="89b24-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="89b24-133">Çok parçalı MIME iletisini okumak için, **Readasmultipartasync** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="89b24-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="89b24-134">Bu yöntem, tüm ileti parçalarını ayıklar ve bunları **Multipartformdatastreamprovider**tarafından sunulan akışlara yazar.</span><span class="sxs-lookup"><span data-stu-id="89b24-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="89b24-135">Yöntem tamamlandığında, **çok partfiledata** nesnelerinin bir koleksiyonu olan **Filedata** özelliğinden dosyalar hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89b24-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="89b24-136">**Multipartfiledata. FileName** , sunucuda dosyanın kaydedildiği yerel dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="89b24-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="89b24-137">**Multipartfiledata. Headers** , bölüm üst bilgisini (istek üst bilgisini*değil* ) içerir.</span><span class="sxs-lookup"><span data-stu-id="89b24-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="89b24-138">Bunu, Içerik\_eğilimi ve Içerik türü üst bilgilerine erişmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89b24-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="89b24-139">Adından da anlaşılacağı gibi, **Readasmultipartasync** zaman uyumsuz bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="89b24-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="89b24-140">Yöntem tamamlandıktan sonra iş gerçekleştirmek için bir [devamlılık görevi](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4,0) veya **await** anahtar sözcüğünü (.NET 4,5) kullanın.</span><span class="sxs-lookup"><span data-stu-id="89b24-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="89b24-141">Önceki kodun .NET Framework 4,0 sürümü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="89b24-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="89b24-142">Form denetimi verilerini okuma</span><span class="sxs-lookup"><span data-stu-id="89b24-142">Reading Form Control Data</span></span>

<span data-ttu-id="89b24-143">Daha önce gösterilen HTML formu metin girişi denetimine sahipti.</span><span class="sxs-lookup"><span data-stu-id="89b24-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="89b24-144">**Multipartformdatastreamprovider**'ın **FormData** özelliğinden denetimin değerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89b24-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="89b24-145">**FormData** , form denetimleri için ad/değer çiftlerini Içeren bir **NameValueCollection** .</span><span class="sxs-lookup"><span data-stu-id="89b24-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="89b24-146">Koleksiyonda yinelenen anahtarlar bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="89b24-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="89b24-147">Şu formu göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="89b24-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="89b24-148">İstek gövdesi şöyle görünebilir:</span><span class="sxs-lookup"><span data-stu-id="89b24-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="89b24-149">Bu durumda, **FormData** koleksiyonu aşağıdaki anahtar/değer çiftlerini içerir:</span><span class="sxs-lookup"><span data-stu-id="89b24-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="89b24-150">seyahat: gidiş dönüş</span><span class="sxs-lookup"><span data-stu-id="89b24-150">trip: round-trip</span></span>
- <span data-ttu-id="89b24-151">Seçenekler: nonstop</span><span class="sxs-lookup"><span data-stu-id="89b24-151">options: nonstop</span></span>
- <span data-ttu-id="89b24-152">Seçenekler: tarihler</span><span class="sxs-lookup"><span data-stu-id="89b24-152">options: dates</span></span>
- <span data-ttu-id="89b24-153">koltuk: pencere</span><span class="sxs-lookup"><span data-stu-id="89b24-153">seat: window</span></span>
