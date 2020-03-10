---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümü özelleştirme'
description: Bu öğretici, sunuyu iyileştirmek için otomatik olarak oluşturulan görünümlerin değiştirilmesine odaklanmaktadır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583596"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="bd086-103">Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümü özelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd086-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="bd086-104">MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd086-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="bd086-105">Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bd086-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="bd086-106">Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="bd086-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="bd086-107">Bu öğretici, sunuyu iyileştirmek için otomatik olarak oluşturulan görünümlerin değiştirilmesine odaklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bd086-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="bd086-108">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="bd086-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd086-109">Öğrenci ayrıntısı sayfasına kurslar ekleme</span><span class="sxs-lookup"><span data-stu-id="bd086-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="bd086-110">Kurslar sayfasına eklendiğini onaylayın</span><span class="sxs-lookup"><span data-stu-id="bd086-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd086-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bd086-111">Prerequisites</span></span>

* [<span data-ttu-id="bd086-112">Veritabanını değiştirme</span><span class="sxs-lookup"><span data-stu-id="bd086-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="bd086-113">Öğrenci ayrıntılarına kurslar ekleyin</span><span class="sxs-lookup"><span data-stu-id="bd086-113">Add courses to student detail</span></span>

<span data-ttu-id="bd086-114">Oluşturulan kod, uygulamanız için iyi bir başlangıç noktası sağlar, ancak uygulamanızda ihtiyaç duyduğunuz tüm işlevleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="bd086-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="bd086-115">Kodu uygulamanızın belirli gereksinimlerini karşılayacak şekilde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd086-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="bd086-116">Şu anda, uygulamanız seçili öğrenci için kayıtlı kursları görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="bd086-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="bd086-117">Bu bölümde, her öğrencinin kayıtlı kurslarını öğrenciye ait **Ayrıntılar** görünümüne ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="bd086-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="bd086-118">**Görünümler** > **öğrenciler** > *details. cshtml*dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bd086-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="bd086-119">Son &lt;/DL&gt; etiketinin altında, ancak kapanış &lt;/div&gt; etiketiyle önce aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd086-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="bd086-120">Bu kod, seçili öğrenci için kayıt tablosundaki her bir kayıt için bir satır görüntüleyen bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd086-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="bd086-121">**Görüntüleme** yöntemi, ifadeyi temsil eden nesne (Modelıdıtem) için HTML 'i işler.</span><span class="sxs-lookup"><span data-stu-id="bd086-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="bd086-122">Değerin türüne ve bu türün şablonuna göre doğru biçimlendirildiğinden emin olmak için, görüntüleme yöntemini (kodda özellik değerini katıştırmak yerine) kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd086-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="bd086-123">Bu örnekte, her bir ifade döngüdeki geçerli kayıttan tek bir özellik döndürür ve değerler metin olarak işlenen ilkel türlerdir.</span><span class="sxs-lookup"><span data-stu-id="bd086-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="bd086-124">Kurslar eklendiğini Onayla</span><span class="sxs-lookup"><span data-stu-id="bd086-124">Confirm courses are added</span></span>

<span data-ttu-id="bd086-125">Çözümü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bd086-125">Run the solution.</span></span> <span data-ttu-id="bd086-126">**Öğrenciler listesi** ' ne tıklayın ve öğrencilerden biri için **Ayrıntılar** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd086-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="bd086-127">Kayıtlı kurslar görünüme dahil edildiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bd086-127">You will see the enrolled courses have been included in the view.</span></span>

![kayıt ile öğrenci](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="bd086-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd086-129">Next steps</span></span>
<span data-ttu-id="bd086-130">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="bd086-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bd086-131">Öğrenci ayrıntısı sayfasına kurslar eklendi</span><span class="sxs-lookup"><span data-stu-id="bd086-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="bd086-132">Kurslar sayfasına eklendiğine onaylandı</span><span class="sxs-lookup"><span data-stu-id="bd086-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="bd086-133">Doğrulama gereksinimlerini belirtmek ve biçimlendirmeyi göstermek için veri ek açıklamaları ekleme hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="bd086-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bd086-134">Veri doğrulamayı geliştirme</span><span class="sxs-lookup"><span data-stu-id="bd086-134">Enhance data validation</span></span>](enhancing-data-validation.md)
