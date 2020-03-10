---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: '2\. Bölüm: veri erişim katmanı | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 2\. bölüm, veri erişim katmanını eklemeyi içerir.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573250"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="8577e-104">2\. Bölüm: Veri Erişim Katmanı</span><span class="sxs-lookup"><span data-stu-id="8577e-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="8577e-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="8577e-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="8577e-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8577e-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="8577e-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8577e-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="8577e-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="8577e-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="8577e-109">2\. bölüm, veri erişim katmanını eklemeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="8577e-109">Part 2 covers adding the data access layer.</span></span>

## <a id="_Toc260221668"></a><span data-ttu-id="8577e-110">Veri erişim katmanını ekleme</span><span class="sxs-lookup"><span data-stu-id="8577e-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="8577e-111">Eticaret uygulamamız iki veritabanına bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8577e-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="8577e-112">Müşteri bilgileri için standart ASP.NET üyelik veritabanını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="8577e-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="8577e-113">Alışveriş sepetimiz ve Ürün kataloğumuz için aşağıdaki şekilde bir SQL Express veritabanı uygulayacağız.</span><span class="sxs-lookup"><span data-stu-id="8577e-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="8577e-114">Uygulamanın uygulama\_veri klasöründe veritabanını (Commerce. mdf) oluşturdunuz, .NET Entity Framework kullanarak veri erişim katmanımızı oluşturmaya devam edebiliriz.</span><span class="sxs-lookup"><span data-stu-id="8577e-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="8577e-115">"Data\_Access" adlı bir klasör oluşturacağız ve bu klasöre sağ tıklayıp "yeni öğe Ekle" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8577e-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="8577e-116">"Yüklü şablonlar" öğesinde "ADO.NET Varlık Veri Modeli" öğesini seçin ve ad olarak EDM\_Commerce. edmx girin ve "Ekle" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8577e-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="8577e-117">"Veritabanından üret" seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8577e-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="8577e-118">Kaydet ve oluştur.</span><span class="sxs-lookup"><span data-stu-id="8577e-118">Save and build.</span></span>

<span data-ttu-id="8577e-119">Şimdi birinci özelliğimizi eklemeye hazırız: bir ürün kategorisi menüsü.</span><span class="sxs-lookup"><span data-stu-id="8577e-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8577e-120">[Önceki](tailspin-spyworks-part-1.md)
> [İleri](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="8577e-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
