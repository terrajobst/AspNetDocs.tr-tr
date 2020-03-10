---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Razor ve unobtrusive JavaScript ile MVC 3 uygulaması oluşturma | Microsoft Docs
author: microsoft
description: Kullanıcı listesi örnek Web uygulaması, Razor görünüm altyapısını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar kolay olduğunu gösterir. Örnek uygulama s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540987"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="615f6-104">Razor ve Unobtrusive JavaScript ile MVC 3 Uygulaması Oluşturma</span><span class="sxs-lookup"><span data-stu-id="615f6-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="615f6-105">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="615f6-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="615f6-106">Kullanıcı listesi örnek Web uygulaması, Razor görünüm altyapısını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="615f6-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="615f6-107">Örnek uygulama, Kullanıcı oluşturma, görüntüleme, görüntüleme ve silme gibi işlevleri içeren bir kurgusal Kullanıcı listesi Web sitesi oluşturmak için ASP.NET MVC sürüm 3 ve Visual Studio 2010 ile yeni Razor görünümü altyapısının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="615f6-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="615f6-108">Bu öğreticide, kullanıcı listesi örnek ASP.NET MVC 3 uygulaması oluşturmak için uygulanan adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="615f6-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="615f6-109">Ve VB kaynak kodu içeren C# bir Visual Studio projesi, bu konuya eşlik eden bir şekilde kullanılabilir: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="615f6-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="615f6-110">Bu öğreticiyle ilgili sorularınız varsa, lütfen bunları [MVC forumuna](https://forums.asp.net/1146.aspx)gönderin.</span><span class="sxs-lookup"><span data-stu-id="615f6-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="615f6-111">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="615f6-111">Overview</span></span>

<span data-ttu-id="615f6-112">Oluşturmakta olduğunuz uygulama basit bir kullanıcı listesi Web sitesidir.</span><span class="sxs-lookup"><span data-stu-id="615f6-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="615f6-113">Kullanıcılar Kullanıcı bilgilerini girebilir, görüntüleyebilir ve güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="615f6-113">Users can enter, view, and update user information.</span></span>

![Örnek site](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="615f6-115">VB ve C# tamamlanmış projeyi [buradan](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="615f6-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="615f6-116">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="615f6-116">Creating the Web Application</span></span>

<span data-ttu-id="615f6-117">Öğreticiyi başlatmak için Visual Studio 2010 ' i açın ve *ASP.NET MVC 3 Web uygulaması* şablonunu kullanarak yeni bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="615f6-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="615f6-118">Uygulamayı &quot;Mvc3Razor&quot;olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="615f6-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="615f6-119">[Yeni MVC 3 projesi ![](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="615f6-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="615f6-120">**Yeni ASP.NET MVC 3 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin, Razor görünüm altyapısını seçin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Yeni ASP.NET MVC 3 proje iletişim kutusu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="615f6-122">Bu öğreticide, ASP.NET üyelik sağlayıcısını kullanmayacak ve bu sayede oturum açma ve üyelikle ilişkili tüm dosyaları silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="615f6-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="615f6-123">**Çözüm Gezgini**, aşağıdaki dosya ve dizinleri kaldırın:</span><span class="sxs-lookup"><span data-stu-id="615f6-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="615f6-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="615f6-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="615f6-125">*Models\accountmodellerini*</span><span class="sxs-lookup"><span data-stu-id="615f6-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="615f6-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="615f6-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="615f6-127">*Views\account* (ve bu dizindeki tüm dosyalar)</span><span class="sxs-lookup"><span data-stu-id="615f6-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="615f6-129"><em>\_Layout. cshtml</em> dosyasını düzenleyin ve `logindisplay` adlı `<div>` öğesi içindeki biçimlendirmeyi <em>&quot;</em>oturum açma devre dışı&quot;iletisiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="615f6-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="615f6-130">Aşağıdaki örnekte yeni biçimlendirme gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="615f6-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="615f6-131">Model ekleme</span><span class="sxs-lookup"><span data-stu-id="615f6-131">Adding the Model</span></span>

<span data-ttu-id="615f6-132">**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="615f6-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Yeni Kullanıcı MDL sınıfı](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="615f6-134">`UserModel`sınıfı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="615f6-134">Name the class `UserModel`.</span></span> <span data-ttu-id="615f6-135">*UserModel* dosyasının içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="615f6-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="615f6-136">`UserModel` sınıfı kullanıcıları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="615f6-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="615f6-137">Sınıfın her üyesine, [Dataaçıklamalarda](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki [gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelikle açıklama eklenir.</span><span class="sxs-lookup"><span data-stu-id="615f6-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="615f6-138">[Dataaçıklamalarda](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki öznitelikler, Web uygulamaları için otomatik istemci ve sunucu tarafı doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="615f6-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="615f6-139">`UserModel` ve `Users` sınıflarına erişebilmek için `HomeController` sınıfını açın ve bir `using` yönergesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="615f6-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="615f6-140">`HomeController` bildiriminden hemen sonra, aşağıdaki yorumu ve başvuruyu bir `Users` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="615f6-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="615f6-141">`Users` sınıfı, bu öğreticide kullanacağınız Basitleştirilmiş, bellek içi bir veri deposudur.</span><span class="sxs-lookup"><span data-stu-id="615f6-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="615f6-142">Gerçek bir uygulamada, Kullanıcı bilgilerini depolamak için bir veritabanı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="615f6-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="615f6-143">`HomeController` dosyanın ilk birkaç satırı aşağıdaki örnekte gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="615f6-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="615f6-144">Bir sonraki adımda Kullanıcı modelinin scafkatlama Sihirbazı tarafından kullanılabilmesi için uygulamayı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="615f6-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="615f6-145">Varsayılan görünüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="615f6-145">Creating the Default View</span></span>

<span data-ttu-id="615f6-146">Sonraki adım, kullanıcıları görüntülemek için bir eylem yöntemi ve görünümü eklemektir.</span><span class="sxs-lookup"><span data-stu-id="615f6-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="615f6-147">Var olan *Views\home\ındex* dosyasını silin.</span><span class="sxs-lookup"><span data-stu-id="615f6-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="615f6-148">Kullanıcıları göstermek için yeni bir *Dizin* dosyası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="615f6-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="615f6-149">`HomeController` sınıfında, `Index` yönteminin içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="615f6-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="615f6-150">`Index` yönteminin içine sağ tıklayın ve ardından **Görünüm Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Görünüm Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="615f6-152">Kesin olarak **belirlenmiş görünüm oluştur** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="615f6-153">**Görünüm verileri sınıfı**için **Mvc3Razor. modeller. userModel**öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="615f6-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="615f6-154">( **Veri sınıfı görüntüle** kutusunda **Mvc3Razor. modeller. userModel** görmüyorsanız projeyi derlemeniz gerekir.) Görünüm altyapısının **Razor**olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="615f6-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="615f6-155">İçeriği **listeye** **görüntüle** ' yi belirleyin ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-155">Set **View content** to **List** and then click **Add**.</span></span>

![Dizin görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="615f6-157">Yeni görünüm, `Index` görünümüne geçirilen kullanıcı verilerini otomatik olarak yapı haline getiriliyor.</span><span class="sxs-lookup"><span data-stu-id="615f6-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="615f6-158">Yeni oluşturulan *Views\home\ındex* dosyasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="615f6-159">**Yeni oluştur**, **Düzenle**, **Ayrıntılar**ve **Sil** bağlantıları çalışmıyor, ancak sayfanın geri kalanı işlevsel.</span><span class="sxs-lookup"><span data-stu-id="615f6-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="615f6-160">Sayfayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="615f6-160">Run the page.</span></span> <span data-ttu-id="615f6-161">Kullanıcıların listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="615f6-161">You see a list of users.</span></span>

![Dizin sayfası](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="615f6-163">*Index. cshtml* dosyasını açın ve **Düzenle**, **Ayrıntılar**ve **Sil** `ActionLink` işaretlemesini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="615f6-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="615f6-164">Kullanıcı adı, **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarında seçili kaydı bulmak için kimlik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="615f6-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="615f6-165">Ayrıntılar görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="615f6-165">Creating the Details View</span></span>

<span data-ttu-id="615f6-166">Sonraki adım, Kullanıcı ayrıntılarını görüntülemek için bir `Details` eylem yöntemi ve görünümü eklemektir.</span><span class="sxs-lookup"><span data-stu-id="615f6-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="615f6-168">Aşağıdaki `Details` yöntemini giriş denetleyicisine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="615f6-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="615f6-169">`Details` yönteminin içine sağ tıklayın ve ardından <strong>Görünüm Ekle</strong>' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="615f6-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="615f6-170"><strong>Görünüm verileri sınıf</strong> kutusunun <strong>Mvc3Razor. modeller. userModel</strong>içerdiğini doğrulayın<em>.</em></span><span class="sxs-lookup"><span data-stu-id="615f6-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="615f6-171">Ayrıntıları <strong>görüntüle</strong> ' yi seçin ve ardından <strong>Ekle</strong>' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Ayrıntı görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="615f6-173">Uygulamayı çalıştırın ve bir ayrıntılar bağlantısı seçin.</span><span class="sxs-lookup"><span data-stu-id="615f6-173">Run the application and select a details link.</span></span> <span data-ttu-id="615f6-174">Otomatik yapı iskelesi modeldeki her bir özelliği gösterir.</span><span class="sxs-lookup"><span data-stu-id="615f6-174">The automatic scaffolding shows each property in the model.</span></span>

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="615f6-176">Düzenleme görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="615f6-176">Creating the Edit View</span></span>

<span data-ttu-id="615f6-177">Aşağıdaki `Edit` yöntemini giriş denetleyicisine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="615f6-178">Önceki adımlarda olduğu gibi bir görünüm ekleyin, ancak **düzenleme**Için **içerik görüntüle** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Düzenleme görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="615f6-180">Uygulamayı çalıştırın ve kullanıcılardan birinin adını ve soyadını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="615f6-181">`UserModel` sınıfına uygulanan `DataAnnotation` kısıtlamalarını ihlal ederseniz, formu gönderdiğinizde, sunucu kodu tarafından üretilen doğrulama hatalarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="615f6-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="615f6-182">Örneğin, &quot;Ann&quot; adını&quot;&quot;olarak değiştirirseniz, formu gönderdiğinizde şu hata görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="615f6-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="615f6-183">Bu öğreticide, Kullanıcı adını birincil anahtar olarak değerlendiriyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="615f6-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="615f6-184">Bu nedenle, Kullanıcı adı özelliği değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="615f6-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="615f6-185">*Edit. cshtml* dosyasında, `Html.BeginForm` deyimden hemen sonra, Kullanıcı adını gizli bir alan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="615f6-186">Bu, özelliğin modele geçirilmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="615f6-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="615f6-187">Aşağıdaki kod parçası `Hidden` deyimin yerleşimini gösterir:</span><span class="sxs-lookup"><span data-stu-id="615f6-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="615f6-188">Kullanıcı adının `TextBoxFor` ve `ValidationMessageFor` işaretlemesini bir `DisplayFor` çağrısıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="615f6-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="615f6-189">`DisplayFor` yöntemi, özelliği salt okunurdur bir öğe olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="615f6-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="615f6-190">Aşağıdaki örnekte, tamamlanan biçimlendirme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="615f6-190">The following example shows the completed markup.</span></span> <span data-ttu-id="615f6-191">Özgün `TextBoxFor` ve `ValidationMessageFor` çağrıları, Razor başlangıç-açıklama ve son açıklama karakterleriyle (`@* *@`) yorum yapılır</span><span class="sxs-lookup"><span data-stu-id="615f6-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="615f6-192">Istemci tarafı doğrulamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="615f6-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="615f6-193">ASP.NET MVC 3 ' te istemci tarafı doğrulamasını etkinleştirmek için iki bayrak ayarlamanız ve üç JavaScript dosyası eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="615f6-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="615f6-194">Uygulamanın *Web. config* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="615f6-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="615f6-195">Uygulama ayarlarında `that ClientValidationEnabled` ve `UnobtrusiveJavaScriptEnabled` true olarak ayarlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="615f6-196">Kök *Web. config* dosyasındaki aşağıdaki parça doğru ayarları gösterir:</span><span class="sxs-lookup"><span data-stu-id="615f6-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="615f6-197">`UnobtrusiveJavaScriptEnabled` true olarak ayarlamak, untrusive Ajax ve unobtrusive istemci doğrulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="615f6-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="615f6-198">Unobtrusive doğrulaması kullandığınızda, doğrulama kuralları HTML5 özniteliklerine açıktır.</span><span class="sxs-lookup"><span data-stu-id="615f6-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="615f6-199">HTML5 öznitelik adları yalnızca küçük harf, sayı ve kısa çizgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="615f6-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="615f6-200">`ClientValidationEnabled` true olarak ayarlamak, istemci tarafı doğrulamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="615f6-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="615f6-201">Bu anahtarları uygulama *Web. config* dosyasında ayarlayarak, istemci doğrulaması ve uygulamanın tamamı Için JavaScript 'i devre altına al özelliğini etkinleştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="615f6-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="615f6-202">Ayrıca, aşağıdaki kodu kullanarak bu ayarları ayrı görünümlerde veya denetleyici yöntemlerinde etkinleştirebilir veya devre dışı bırakabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="615f6-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="615f6-203">Ayrıca, çeşitli JavaScript dosyalarını işlenmiş görünümde de eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="615f6-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="615f6-204">Tüm görünümlere JavaScript eklemenin kolay bir yolu, bunları *Views\shared\\_Layout. cshtml* dosyasına eklemektir.</span><span class="sxs-lookup"><span data-stu-id="615f6-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="615f6-205">*\_Layout. cshtml* dosyasının `<head>` öğesini şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="615f6-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="615f6-206">İlk iki jQuery komut dosyası Microsoft Ajax Content Delivery Network (CDN) tarafından barındırılır.</span><span class="sxs-lookup"><span data-stu-id="615f6-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="615f6-207">Microsoft Ajax CDN 'nin avantajlarından yararlanarak uygulamalarınızın ilk isabet performansını önemli ölçüde artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="615f6-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="615f6-208">Uygulamayı çalıştırın ve bir düzenleme bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-208">Run the application and click an edit link.</span></span> <span data-ttu-id="615f6-209">Sayfanın kaynağını tarayıcıda görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-209">View the page's source in the browser.</span></span> <span data-ttu-id="615f6-210">Tarayıcı kaynağı `data-val` formun birçok özniteliğini gösterir (veri doğrulaması için).</span><span class="sxs-lookup"><span data-stu-id="615f6-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="615f6-211">İstemci doğrulaması ve unobtrusive JavaScript etkinleştirildiğinde, istemci doğrulama kuralına sahip giriş alanları, engellemeyen istemci doğrulamasını tetiklemek için `data-val="true"` özniteliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="615f6-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="615f6-212">Örneğin, modeldeki `City` alanı [gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelikle tasarlanmıştı ve bu, aşağıdaki örnekte gösterilen HTML ile sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="615f6-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="615f6-213">Her istemci doğrulama kuralı için, `data-val-rulename="message"`form içeren bir öznitelik eklenir.</span><span class="sxs-lookup"><span data-stu-id="615f6-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="615f6-214">Daha önce gösterilen `City` alan örneğini kullanarak, gerekli istemci doğrulama kuralı `data-val-required` özniteliğini ve &quot;City alanı gereklidir&quot;ileti üretir.</span><span class="sxs-lookup"><span data-stu-id="615f6-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="615f6-215">Uygulamayı çalıştırın, kullanıcılardan birini düzenleyin ve `City` alanını temizleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="615f6-216">Alanı kapattığınızda, bir istemci tarafı doğrulama hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="615f6-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Şehir gerekli](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="615f6-218">Benzer şekilde, istemci doğrulama kuralındaki her bir parametre için `data-val-rulename-paramname=paramvalue`form olan bir öznitelik eklenir.</span><span class="sxs-lookup"><span data-stu-id="615f6-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="615f6-219">Örneğin, `FirstName` özelliğine [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliğiyle açıklama eklenir ve en az 3 ve en fazla 8 uzunluğunda bir değer belirtir.</span><span class="sxs-lookup"><span data-stu-id="615f6-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="615f6-220">`length` adlı veri doğrulama kuralının parametre adı `max` ve 8 parametre değeri vardır.</span><span class="sxs-lookup"><span data-stu-id="615f6-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="615f6-221">Aşağıda, kullanıcılardan birini düzenlerken `FirstName` alanı için oluşturulan HTML gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="615f6-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="615f6-222">Engellenemeyen istemci doğrulaması hakkında daha fazla bilgi için bkz. [ASP.NET MVC 3 ' te](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) atacan solson bloguna yönelik Istemci doğrulamasını kaldırma.</span><span class="sxs-lookup"><span data-stu-id="615f6-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="615f6-223">ASP.NET MVC 3 Beta sürümünde, bazen istemci tarafı doğrulamayı başlatmak için formu göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="615f6-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="615f6-224">Bu, son sürüm için değişebilir.</span><span class="sxs-lookup"><span data-stu-id="615f6-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="615f6-225">Oluşturma görünümü oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="615f6-225">Creating the Create View</span></span>

<span data-ttu-id="615f6-226">Sonraki adım, kullanıcının yeni bir Kullanıcı oluşturmasını sağlamak için bir `Create` eylem yöntemi ve görünümü eklemektir.</span><span class="sxs-lookup"><span data-stu-id="615f6-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="615f6-227">Aşağıdaki `Create` yöntemini giriş denetleyicisine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="615f6-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="615f6-228">Önceki adımlarda olduğu gibi bir görünüm ekleyin, ancak **oluşturulacak** **görünümü içerik** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="615f6-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Görünüm Oluşturma](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="615f6-230">Uygulamayı çalıştırın, **Oluştur** bağlantısını seçin ve yeni bir kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="615f6-231">`Create` yöntemi, istemci tarafı ve sunucu tarafı doğrulamasından otomatik olarak yararlanır.</span><span class="sxs-lookup"><span data-stu-id="615f6-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="615f6-232">&quot;ben X&quot;gibi boşluk içeren bir Kullanıcı adı girmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="615f6-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="615f6-233">Kullanıcı adı alanından kaldırdığınızda, bir istemci tarafı doğrulama hatası (`White space is not allowed`) görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="615f6-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="615f6-234">Delete metodunu ekleyin</span><span class="sxs-lookup"><span data-stu-id="615f6-234">Add the Delete method</span></span>

<span data-ttu-id="615f6-235">Öğreticiyi tamamlayabilmeniz için aşağıdaki `Delete` yöntemini giriş denetleyicisine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="615f6-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="615f6-236">Önceki adımlarda olduğu gibi `Delete` bir görünüm ekleyin ve **Silinecek** **içeriği görüntüle** olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="615f6-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Görünümü Sil](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="615f6-238">Artık doğrulama ile basit ancak tamamen işlevsel ASP.NET MVC 3 uygulamanız vardır.</span><span class="sxs-lookup"><span data-stu-id="615f6-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
