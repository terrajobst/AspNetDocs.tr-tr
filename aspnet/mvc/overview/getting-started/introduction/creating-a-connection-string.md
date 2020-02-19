---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: Bağlantı dizesi oluşturma ve SQL Server LocalDB ile çalışma | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 20781ad760d3a0e4559ec4c7e18528f3686dcc02
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456523"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="0a0b7-102">Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma</span><span class="sxs-lookup"><span data-stu-id="0a0b7-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="0a0b7-103">[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından</span><span class="sxs-lookup"><span data-stu-id="0a0b7-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="0a0b7-104">Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma</span><span class="sxs-lookup"><span data-stu-id="0a0b7-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="0a0b7-105">Oluşturduğunuz `MovieDBContext` sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="0a0b7-106">Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="0a0b7-107">Gerçekten hangi veritabanını kullanacağınızı belirtmeniz gerekmez, Entity Framework varsayılan olarak [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)'yi kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="0a0b7-108">Bu bölümde, uygulamanın *Web. config* dosyasına açıkça bir bağlantı dizesi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="0a0b7-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="0a0b7-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="0a0b7-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) , kullanıcı modunda isteğe bağlı ve çalışır durumda başlayan SQL Server Express veritabanı altyapısının hafif bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="0a0b7-111">LocalDB, veritabanlarıyla *. mdf* dosyaları olarak çalışmanıza olanak sağlayan SQL Server Express özel bir yürütme modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="0a0b7-112">Genellikle, LocalDB veritabanı dosyaları bir Web projesinin *App\_Data* klasöründe tutulur.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="0a0b7-113">SQL Server Express üretim Web uygulamalarında kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="0a0b7-114">LocalDB, IIS ile çalışmak üzere tasarlanmadığı için bir Web uygulamasıyla üretim için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="0a0b7-115">Ancak, bir LocalDB veritabanı SQL Server veya SQL Azure kolayca geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="0a0b7-116">Visual Studio 2017 ' de, LocalDB, Visual Studio ile varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="0a0b7-117">Varsayılan olarak Entity Framework, nesne bağlamı sınıfıyla aynı adlı bir bağlantı dizesi arar (Bu proje için`MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="0a0b7-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="0a0b7-118">Daha fazla bilgi için bkz. [ASP.NET Web uygulamaları Için bağlantı dizeleri SQL Server](https://msdn.microsoft.com/library/jj653752.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a0b7-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="0a0b7-119">Aşağıda gösterilen uygulama kök *Web. config* dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="0a0b7-120">( *Görünümler* klasöründeki *Web. config* dosyası değil.)</span><span class="sxs-lookup"><span data-stu-id="0a0b7-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="0a0b7-121">`<connectionStrings>` öğeyi bul:</span><span class="sxs-lookup"><span data-stu-id="0a0b7-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="0a0b7-122">Aşağıdaki bağlantı dizesini *Web. config* dosyasındaki `<connectionStrings>` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="0a0b7-123">Aşağıdaki örnek, *Web. config* dosyasının yeni bağlantı dizesi eklenmiş bir bölümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="0a0b7-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="0a0b7-124">İki bağlantı dizesi çok benzerdir.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-124">The two connection strings are very similar.</span></span> <span data-ttu-id="0a0b7-125">İlk bağlantı dizesi `DefaultConnection` olarak adlandırılır ve uygulamaya kimlerin erişebileceğini denetlemek için üyelik veritabanı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="0a0b7-126">Eklediğiniz bağlantı dizesi, *App\_Data* klasöründe bulunan *Movie. mdf* adlı bir LocalDB veritabanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="0a0b7-127">Bu öğreticide üyelik veritabanını kullanmayacağız, üyelik, kimlik doğrulama ve güvenlik hakkında daha fazla bilgi için bkz. öğreticimin [kimlik doğrulama ve SQL DB ile ASP.NET MVC uygulaması oluşturma ve Azure App Service için dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span><span class="sxs-lookup"><span data-stu-id="0a0b7-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="0a0b7-128">Bağlantı dizesinin adı [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) sınıfının adıyla eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="0a0b7-129">Gerçekten `MovieDBContext` bağlantı dizesi eklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="0a0b7-130">Bir bağlantı dizesi belirtmezseniz, Entity Framework [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) sınıfının tam adı ile Users dizininde bir LocalDB veritabanı oluşturur (bu durumda `MvcMovie.Models.MovieDBContext`).</span><span class="sxs-lookup"><span data-stu-id="0a0b7-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="0a0b7-131">Veritabanına sahip olduğu sürece, istediğiniz herhangi bir şey için bir ad verebilirsiniz *. MDF* soneki.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="0a0b7-132">Örneğin, *MyFilms. mdf*veritabanına ad vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="0a0b7-133">Daha sonra, film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir `MoviesController` sınıfı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0a0b7-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0a0b7-134">[Önceki](adding-a-model.md)
> [İleri](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="0a0b7-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
