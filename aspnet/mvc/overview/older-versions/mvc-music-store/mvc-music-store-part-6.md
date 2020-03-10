---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6\. Bölüm: model doğrulaması için veri ek açıklamalarını kullanma | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 6\. bölüm, model V için veri ek açıklamalarını kullanmayı içerir...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539279"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="ae7b8-104">6\. Bölüm: Model Doğrulama için Veri Ek Açıklamalarını Kullanma</span><span class="sxs-lookup"><span data-stu-id="ae7b8-104">Part 6: Using Data Annotations for Model Validation</span></span>

<span data-ttu-id="ae7b8-105">[Jon Galloway](https://github.com/jongalloway) tarafından</span><span class="sxs-lookup"><span data-stu-id="ae7b8-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="ae7b8-106">MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="ae7b8-107">MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="ae7b8-108">Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="ae7b8-109">6\. bölüm, model doğrulaması için veri ek açıklamalarını kullanmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>

<span data-ttu-id="ae7b8-110">Oluşturma ve düzenleme formlarımızla ilgili önemli bir sorun var: herhangi bir doğrulama yapmadık.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="ae7b8-111">Gerekli alanları boş bırakma veya fiyat alanında harfler yazma gibi işlemleri yapabiliriz ve göreceğiniz ilk hata veritabanından.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="ae7b8-112">Model sınıflarımıza veri ek açıklamaları ekleyerek uygulamamıza kolayca doğrulama ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="ae7b8-113">Veri ek açıklamaları, model özelliklerine uygulanmasını istediğimiz kuralları açıklamanıza olanak sağlar ve ASP.NET MVC bunları zorlamaya ve kullanıcılarımıza uygun iletileri görüntülemeye yönelik bir işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="ae7b8-114">Albüm formlarımıza doğrulama ekleme</span><span class="sxs-lookup"><span data-stu-id="ae7b8-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="ae7b8-115">Aşağıdaki veri ek açıklaması özniteliklerini kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="ae7b8-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="ae7b8-116">**Gerekli** – özelliğin gerekli bir alan olduğunu belirtir</span><span class="sxs-lookup"><span data-stu-id="ae7b8-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="ae7b8-117">**DisplayName** : form alanlarında ve doğrulama iletilerinde kullanmak istediğimiz metni tanımlar</span><span class="sxs-lookup"><span data-stu-id="ae7b8-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="ae7b8-118">**StringLength** : bir dize alanı için en fazla uzunluğu tanımlar</span><span class="sxs-lookup"><span data-stu-id="ae7b8-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="ae7b8-119">**Range** : sayısal bir alan için en yüksek ve en küçük değeri verir</span><span class="sxs-lookup"><span data-stu-id="ae7b8-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="ae7b8-120">**Bind** : parametre veya form değerlerini model özelliklerine bağlamada hariç tutulacak veya dahil edilecek alanları listeler</span><span class="sxs-lookup"><span data-stu-id="ae7b8-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="ae7b8-121">**ScaffoldColumn** – alanları düzenleyici formlarından gizlemeyi sağlar</span><span class="sxs-lookup"><span data-stu-id="ae7b8-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="ae7b8-122">*Not: veri ek açıklaması özniteliklerini kullanarak model doğrulama hakkında daha fazla bilgi için`https://go.microsoft.com/fwlink/?LinkId=159063`ADRESINDEKI MSDN belgelerine bakın.* [ ](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="ae7b8-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="ae7b8-123">Albüm sınıfını açın ve aşağıdaki *using* deyimlerini en üste ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="ae7b8-124">Ardından, aşağıda gösterildiği gibi, görüntüleme ve doğrulama öznitelikleri eklemek için özellikleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="ae7b8-125">Biz de var olsa da, tarzı ve sanatçıya sanal özelliklere de değiştirdik.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="ae7b8-126">Bu, Entity Framework gerektiği gibi yavaş yüklenmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="ae7b8-127">Bu öznitelikleri albüm modelimize ekledikten sonra, oluşturma ve düzenleme ekranımız alanları doğrulamaya başlar ve seçtiğiniz görünen adları (örn. albümle değil, albüm sanat URL 'Si) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="ae7b8-128">Uygulamayı çalıştırın ve/Storemanager/createadresine gidin.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="ae7b8-129">Daha sonra bazı doğrulama kurallarını bozacağız.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="ae7b8-130">0 ' ın bir fiyatını girin ve başlığı boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="ae7b8-131">Oluştur düğmesine tıkladığımızda, tanımlamış olduğumuz doğrulama kurallarına uymayan alanları gösteren doğrulama hata iletileriyle birlikte görüntülenecek formu görüyoruz.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="ae7b8-132">Istemci tarafı doğrulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="ae7b8-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="ae7b8-133">Sunucu tarafı doğrulaması bir uygulama perspektifinden çok önemlidir, çünkü kullanıcılar istemci tarafı doğrulamayı atlayabilirler.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="ae7b8-134">Ancak, yalnızca sunucu tarafı doğrulama uygulayan Web sayfası formları üç önemli sorun sergiler.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="ae7b8-135">Kullanıcının, formun gönderilmesini, sunucuda doğrulanmasını ve yanıtın tarayıcıya gönderilmesi için beklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="ae7b8-136">Kullanıcı artık doğrulama kurallarını geçirmeden bir alanı düzelttiklerinde anında geri bildirim almaz.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="ae7b8-137">Sunucu kaynaklarını kullanıcının tarayıcısına göre değil, doğrulama mantığını gerçekleştirecek şekilde harcadık.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="ae7b8-138">Neyse ki, ASP.NET MVC 3 iskele şablonlarının içinde yerleşik olarak bulunan ve başka hiçbir iş gerektirmeyen istemci tarafı doğrulaması vardır.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="ae7b8-139">Başlık alanına tek bir harf yazmak doğrulama gereksinimlerini karşılar, bu nedenle doğrulama iletisi hemen kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="ae7b8-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> <span data-ttu-id="ae7b8-140">[Önceki](mvc-music-store-part-5.md)
> [İleri](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="ae7b8-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
