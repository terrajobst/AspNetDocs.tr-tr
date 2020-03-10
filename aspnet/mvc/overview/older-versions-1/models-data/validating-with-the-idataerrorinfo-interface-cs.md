---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: IDataErrorInfo arabirimi ile doğrulama (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther, bir model sınıfında IDataErrorInfo arabirimini uygulayarak özel doğrulama hata iletilerinin nasıl görüntüleneceğini gösterir.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542562"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="68d41-103">IDataErrorInfo Arabirimi ile Doğrulama (C#)</span><span class="sxs-lookup"><span data-stu-id="68d41-103">Validating with the IDataErrorInfo Interface (C#)</span></span>

<span data-ttu-id="68d41-104">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="68d41-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="68d41-105">Stephen Walther, bir model sınıfında IDataErrorInfo arabirimini uygulayarak özel doğrulama hata iletilerinin nasıl görüntüleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="68d41-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="68d41-106">Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirmeye yönelik bir yaklaşımı açıklamaktır.</span><span class="sxs-lookup"><span data-stu-id="68d41-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="68d41-107">Bir kişinin gerekli form alanları için değer sağlamadan bir HTML formu göndermesini nasıl önleyeceğinizi öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68d41-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="68d41-108">Bu öğreticide, ıerrordataınfo arabirimini kullanarak doğrulamanın nasıl gerçekleştirileceğini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="68d41-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="68d41-109">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="68d41-109">Assumptions</span></span>

<span data-ttu-id="68d41-110">Bu öğreticide, MoviesDB veritabanı ve filmler veritabanı tablosunu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="68d41-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="68d41-111">Bu tabloda aşağıdaki sütunlar bulunur:</span><span class="sxs-lookup"><span data-stu-id="68d41-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>

| <span data-ttu-id="68d41-112">**Sütun adı**</span><span class="sxs-lookup"><span data-stu-id="68d41-112">**Column Name**</span></span> | <span data-ttu-id="68d41-113">**Veri türü**</span><span class="sxs-lookup"><span data-stu-id="68d41-113">**Data Type**</span></span> | <span data-ttu-id="68d41-114">**Null değerlere izin ver**</span><span class="sxs-lookup"><span data-stu-id="68d41-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="68d41-115">Kimlik</span><span class="sxs-lookup"><span data-stu-id="68d41-115">Id</span></span> | <span data-ttu-id="68d41-116">int</span><span class="sxs-lookup"><span data-stu-id="68d41-116">Int</span></span> | <span data-ttu-id="68d41-117">False</span><span class="sxs-lookup"><span data-stu-id="68d41-117">False</span></span> |
| <span data-ttu-id="68d41-118">Başlık</span><span class="sxs-lookup"><span data-stu-id="68d41-118">Title</span></span> | <span data-ttu-id="68d41-119">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="68d41-119">Nvarchar(100)</span></span> | <span data-ttu-id="68d41-120">False</span><span class="sxs-lookup"><span data-stu-id="68d41-120">False</span></span> |
| <span data-ttu-id="68d41-121">Direktörü</span><span class="sxs-lookup"><span data-stu-id="68d41-121">Director</span></span> | <span data-ttu-id="68d41-122">Nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="68d41-122">Nvarchar(100)</span></span> | <span data-ttu-id="68d41-123">False</span><span class="sxs-lookup"><span data-stu-id="68d41-123">False</span></span> |
| <span data-ttu-id="68d41-124">Davterekiralık</span><span class="sxs-lookup"><span data-stu-id="68d41-124">DateReleased</span></span> | <span data-ttu-id="68d41-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="68d41-125">DateTime</span></span> | <span data-ttu-id="68d41-126">False</span><span class="sxs-lookup"><span data-stu-id="68d41-126">False</span></span> |

<span data-ttu-id="68d41-127">Bu öğreticide, veritabanı modeli sınıflarımı oluşturmak için Microsoft Entity Framework kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="68d41-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="68d41-128">Entity Framework tarafından üretilen film sınıfı Şekil 1 ' de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="68d41-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="68d41-129">[Film varlığını ![](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="68d41-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span></span>

<span data-ttu-id="68d41-130">**Şekil 01**: film varlığı ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="68d41-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="68d41-131">Veritabanı modeli sınıflarınızı oluşturmak için Entity Framework kullanma hakkında daha fazla bilgi edinmek için, Entity Framework ile model sınıfları oluşturma adlı öğreticiye bakın.</span><span class="sxs-lookup"><span data-stu-id="68d41-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="68d41-132">Denetleyici sınıfı</span><span class="sxs-lookup"><span data-stu-id="68d41-132">The Controller Class</span></span>

<span data-ttu-id="68d41-133">Filmleri listelemek ve yeni filmler oluşturmak için giriş denetleyicisini kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="68d41-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="68d41-134">Bu sınıfın kodu, liste 1 ' de yer alır.</span><span class="sxs-lookup"><span data-stu-id="68d41-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="68d41-135">**Listeleme 1-Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="68d41-135">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="68d41-136">Liste 1 ' deki giriş denetleyicisi sınıfı iki oluşturma () eylemi içerir.</span><span class="sxs-lookup"><span data-stu-id="68d41-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="68d41-137">İlk eylem, yeni bir filmi oluşturmak için HTML formunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="68d41-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="68d41-138">İkinci Create () eylemi, yeni filmin gerçek ekleme işlemini veritabanına uygular.</span><span class="sxs-lookup"><span data-stu-id="68d41-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="68d41-139">İkinci Create () eylemi, ilk oluşturma () eylemi tarafından görüntülenecek form sunucuya gönderildiğinde çağrılır.</span><span class="sxs-lookup"><span data-stu-id="68d41-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="68d41-140">İkinci oluşturma () eyleminin aşağıdaki kod satırlarını içerdiğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="68d41-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="68d41-141">IsValid özelliği bir doğrulama hatası olduğunda false döndürür.</span><span class="sxs-lookup"><span data-stu-id="68d41-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="68d41-142">Bu durumda, bir filmi oluşturmak için HTML formunu içeren oluştur görünümü yeniden görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="68d41-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="68d41-143">Kısmi sınıf oluşturma</span><span class="sxs-lookup"><span data-stu-id="68d41-143">Creating a Partial Class</span></span>

<span data-ttu-id="68d41-144">Film sınıfı Entity Framework tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="68d41-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="68d41-145">Çözüm Gezgini penceresinde MoviesDBModel. edmx dosyasını genişlettikten sonra MoviesDBModel.Designer.cs dosyasını kod düzenleyicisinde açarsanız film sınıfının kodunu görebilirsiniz (bkz. Şekil 2).</span><span class="sxs-lookup"><span data-stu-id="68d41-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="68d41-146">[Film varlığı için kodu ![](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="68d41-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span></span>

<span data-ttu-id="68d41-147">**Şekil 02**: film varlığının kodu ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="68d41-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>

<span data-ttu-id="68d41-148">Film sınıfı, kısmi bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="68d41-148">The Movie class is a partial class.</span></span> <span data-ttu-id="68d41-149">Diğer bir deyişle, film sınıfının işlevlerini genişletmek için aynı ada sahip başka bir kısmi sınıf ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="68d41-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="68d41-150">Yeni kısmi sınıfa doğrulama mantığımızı ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="68d41-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="68d41-151">Liste 2 ' deki sınıfı modeller klasörüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="68d41-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="68d41-152">**Listeleme 2-Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="68d41-152">**Listing 2 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="68d41-153">Kod 2 ' deki sınıfın *kısmi* değiştirici içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="68d41-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="68d41-154">Bu sınıfa eklediğiniz tüm yöntemler veya özellikler, Entity Framework tarafından oluşturulan film sınıfının bir parçası haline gelir.</span><span class="sxs-lookup"><span data-stu-id="68d41-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="68d41-155">OnChanging ve OnChanged kısmi yöntemleri ekleme</span><span class="sxs-lookup"><span data-stu-id="68d41-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="68d41-156">Entity Framework bir varlık sınıfı oluşturduğunda Entity Framework otomatik olarak sınıfa kısmi Yöntemler ekler.</span><span class="sxs-lookup"><span data-stu-id="68d41-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="68d41-157">Entity Framework, sınıfın her özelliğine karşılık gelen OnChanging ve OnChanged kısmi yöntemleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="68d41-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="68d41-158">Film sınıfı söz konusu olduğunda Entity Framework aşağıdaki yöntemleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="68d41-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="68d41-159">Onıdchanging</span><span class="sxs-lookup"><span data-stu-id="68d41-159">OnIdChanging</span></span>
- <span data-ttu-id="68d41-160">Onıdchanged</span><span class="sxs-lookup"><span data-stu-id="68d41-160">OnIdChanged</span></span>
- <span data-ttu-id="68d41-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="68d41-161">OnTitleChanging</span></span>
- <span data-ttu-id="68d41-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="68d41-162">OnTitleChanged</span></span>
- <span data-ttu-id="68d41-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="68d41-163">OnDirectorChanging</span></span>
- <span data-ttu-id="68d41-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="68d41-164">OnDirectorChanged</span></span>
- <span data-ttu-id="68d41-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="68d41-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="68d41-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="68d41-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="68d41-167">OnChanging yöntemi, ilgili özellik değiştirilmeden önce hemen çağrılır.</span><span class="sxs-lookup"><span data-stu-id="68d41-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="68d41-168">OnChanged yöntemi, özellik değiştirildikten hemen sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="68d41-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="68d41-169">Film sınıfına doğrulama mantığı eklemek için bu kısmi yöntemlerin avantajlarından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68d41-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="68d41-170">Listeleme 3 ' teki filmi Güncelleştir sınıfı, başlık ve yönetmen özelliklerinin boş olmayan değerler atandığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="68d41-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="68d41-171">Kısmi Yöntem, uygulamanız için gerekli olmayan bir sınıfta tanımlanan bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="68d41-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="68d41-172">Kısmi bir yöntem gerçekleştirmezseniz, derleyici yöntem imzasını ve yönteme tüm çağrıları kaldırır, böylece kısmi yöntemle ilişkili bir çalışma zamanı maliyeti yoktur.</span><span class="sxs-lookup"><span data-stu-id="68d41-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="68d41-173">Visual Studio Code düzenleyicide, *bir kısmı, sonra da* uygulanacak partileri bir listesini görüntülemek için bir boşluk gelen anahtar sözcüğünü yazarak kısmen bir yöntem ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68d41-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="68d41-174">**Listeleme 3-Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="68d41-174">**Listing 3 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="68d41-175">Örneğin, title özelliğine boş bir dize atamayı denerseniz, \_hatalar adlı bir sözlüğe bir hata mesajı atanır.</span><span class="sxs-lookup"><span data-stu-id="68d41-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="68d41-176">Bu noktada, başlık özelliğine boş bir dize atadığınızda ve özel \_hataları alanına bir hata eklendiğinde hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="68d41-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="68d41-177">Bu doğrulama hatalarını ASP.NET MVC çerçevesine göstermek için IDataErrorInfo arabirimini uygulamamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="68d41-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="68d41-178">IDataErrorInfo arabirimini uygulama</span><span class="sxs-lookup"><span data-stu-id="68d41-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="68d41-179">IDataErrorInfo arabirimi, .NET Framework 'ün ilk sürümden bu yana bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="68d41-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="68d41-180">Bu arabirim çok basit bir arabirimdir:</span><span class="sxs-lookup"><span data-stu-id="68d41-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="68d41-181">Bir sınıf, IDataErrorInfo arabirimini uyguluyorsa, sınıfın bir örneğini oluştururken ASP.NET MVC çerçevesi bu arabirimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="68d41-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="68d41-182">Örneğin, giriş denetleyicisi oluşturma () eylemi, film sınıfının bir örneğini kabul eder:</span><span class="sxs-lookup"><span data-stu-id="68d41-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="68d41-183">ASP.NET MVC Framework, bir model Ciltçi (Defaultmodelciltçi) kullanarak Create () eylemine geçirilen filmin örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="68d41-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="68d41-184">Model Ciltçi, HTML form alanlarını bir film nesnesinin örneğine bağlayarak film nesnesinin bir örneğini oluşturmaktan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="68d41-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="68d41-185">Defaultmodelciltçi, bir sınıfın IDataErrorInfo arabirimini uygulayıp uygulamadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="68d41-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="68d41-186">Bir sınıf bu arabirimi uyguluyorsa model Bağlayıcısı, sınıfının her özelliği için IDataErrorInfo. bu dizin oluşturucuyu çağırır.</span><span class="sxs-lookup"><span data-stu-id="68d41-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="68d41-187">Dizin Oluşturucu bir hata iletisi döndürürse, model Ciltçi bu hata iletisini model durumuna otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="68d41-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="68d41-188">Defaultmodelciltçi, IDataErrorInfo. Error özelliğini de denetler.</span><span class="sxs-lookup"><span data-stu-id="68d41-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="68d41-189">Bu özellik, sınıfla ilişkili, özelliğe özgü olmayan doğrulama hatalarını temsil etmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="68d41-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="68d41-190">Örneğin, film sınıfının birden çok özelliklerinin değerlerine bağlı olan bir doğrulama kuralını zorlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68d41-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="68d41-191">Bu durumda, hata özelliğinden bir doğrulama hatası döndürürsınız.</span><span class="sxs-lookup"><span data-stu-id="68d41-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="68d41-192">Liste 4 ' teki güncelleştirilmiş film sınıfı, IDataErrorInfo arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="68d41-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="68d41-193">**Listeleme 4-Models\Movie.cs (IDataErrorInfo uygular)**</span><span class="sxs-lookup"><span data-stu-id="68d41-193">**Listing 4 - Models\Movie.cs (implements IDataErrorInfo)**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="68d41-194">4\. listede, Indexer özelliği, dizin oluşturucuya geçirilen özellik adına karşılık gelen bir anahtar içerip içermediğini görmek için \_hataları koleksiyonunu denetler.</span><span class="sxs-lookup"><span data-stu-id="68d41-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="68d41-195">Özelliği ile ilişkili doğrulama hatası yoksa boş bir dize döndürülür.</span><span class="sxs-lookup"><span data-stu-id="68d41-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="68d41-196">Değiştirilen film sınıfını kullanmak için giriş denetleyicisini herhangi bir şekilde değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="68d41-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="68d41-197">Şekil 3 ' te görünen sayfa, başlık veya yönetmen formu alanları için hiçbir değer girilmediğinde ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="68d41-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="68d41-198">[eylem yöntemlerini otomatik olarak oluşturma ![](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="68d41-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span></span>

<span data-ttu-id="68d41-199">**Şekil 03**: eksik değerlere sahip bir form ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="68d41-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>

<span data-ttu-id="68d41-200">Dadlanmış değerin otomatik olarak doğrulanacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="68d41-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="68d41-201">Dadterekiralık özelliği NULL değerleri kabul etmediğinden, Defaultmodelciltçi bir değere sahip olmadığında bu özellik için otomatik olarak bir doğrulama hatası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="68d41-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="68d41-202">Bu özellik için bir hata iletisi değiştirmek istiyorsanız, özel bir model Bağlayıcısı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="68d41-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="68d41-203">Özet</span><span class="sxs-lookup"><span data-stu-id="68d41-203">Summary</span></span>

<span data-ttu-id="68d41-204">Bu öğreticide, IDataErrorInfo arabirimini kullanarak doğrulama hata iletileri oluşturma hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="68d41-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="68d41-205">İlk olarak, Entity Framework tarafından oluşturulan kısmi film sınıfının işlevselliğini genişleten kısmi bir film sınıfı oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="68d41-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="68d41-206">Daha sonra, OnTitleChanging () ve OnDirectorChanging () kısmi yöntemlerine yönelik olarak doğrulama mantığı ekledik.</span><span class="sxs-lookup"><span data-stu-id="68d41-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="68d41-207">Son olarak, bu doğrulama iletilerini ASP.NET MVC çerçevesine göstermek için IDataErrorInfo arabirimini uyguladık.</span><span class="sxs-lookup"><span data-stu-id="68d41-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="68d41-208">[Önceki](performing-simple-validation-cs.md)
> [İleri](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="68d41-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>
