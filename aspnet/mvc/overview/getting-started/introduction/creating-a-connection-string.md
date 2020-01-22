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
ms.openlocfilehash: d3c6e736c5dcf4a3615e3c72cfc033effc7cc8e6
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519316"
---
# <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

[!INCLUDE [Tutorial Note](index.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Bağlantı Dizesi Oluşturma ve SQL Server LocalDB ile Çalışma

Oluşturduğunuz `MovieDBContext` sınıf veritabanına bağlanma ve `Movie` nesneleri veritabanı kayıtlarına eşleme görevini işler. Tek bir soru sorabilirsiniz, ancak hangi veritabanının bağlanacağı de bu şekilde belirlenir. Gerçekten hangi veritabanını kullanacağınızı belirtmeniz gerekmez, Entity Framework varsayılan olarak [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)'yi kullanmaktır. Bu bölümde, uygulamanın *Web. config* dosyasına açıkça bir bağlantı dizesi ekleyeceğiz.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) , kullanıcı modunda isteğe bağlı ve çalışır durumda başlayan SQL Server Express veritabanı altyapısının hafif bir sürümüdür. LocalDB, veritabanlarıyla *. mdf* dosyaları olarak çalışmanıza olanak sağlayan SQL Server Express özel bir yürütme modunda çalışır. Genellikle, LocalDB veritabanı dosyaları bir Web projesinin *App\_Data* klasöründe tutulur.

SQL Server Express üretim Web uygulamalarında kullanılması önerilmez. LocalDB, IIS ile çalışmak üzere tasarlanmadığı için bir Web uygulamasıyla üretim için kullanılmamalıdır. Ancak, bir LocalDB veritabanı SQL Server veya SQL Azure kolayca geçirilebilir.

Visual Studio 2017 ' de, LocalDB, Visual Studio ile varsayılan olarak yüklenir.

Varsayılan olarak Entity Framework, nesne bağlamı sınıfıyla aynı adlı bir bağlantı dizesi arar (Bu proje için`MovieDBContext`). Daha fazla bilgi için bkz. [ASP.NET Web uygulamaları Için bağlantı dizeleri SQL Server](https://msdn.microsoft.com/library/jj653752.aspx).

Aşağıda gösterilen uygulama kök *Web. config* dosyasını açın. ( *Görünümler* klasöründeki *Web. config* dosyası değil.)

![](creating-a-connection-string/_static/image1.png)

`<connectionStrings>` öğeyi bul:

![](creating-a-connection-string/_static/image2.png)

Aşağıdaki bağlantı dizesini *Web. config* dosyasındaki `<connectionStrings>` öğesine ekleyin.

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

Aşağıdaki örnek, *Web. config* dosyasının yeni bağlantı dizesi eklenmiş bir bölümünü gösterir:

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

İki bağlantı dizesi çok benzerdir. İlk bağlantı dizesi `DefaultConnection` olarak adlandırılır ve uygulamaya kimlerin erişebileceğini denetlemek için üyelik veritabanı için kullanılır. Eklediğiniz bağlantı dizesi, *App\_Data* klasöründe bulunan *Movie. mdf* adlı bir LocalDB veritabanını belirtir. Bu öğreticide üyelik veritabanını kullanmayacağız, üyelik, kimlik doğrulama ve güvenlik hakkında daha fazla bilgi için bkz. öğreticimin [kimlik doğrulama ve SQL DB ile ASP.NET MVC uygulaması oluşturma ve Azure App Service için dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

Bağlantı dizesinin adı [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) sınıfının adıyla eşleşmelidir.

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

Gerçekten `MovieDBContext` bağlantı dizesi eklemeniz gerekmez. Bir bağlantı dizesi belirtmezseniz, Entity Framework [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) sınıfının tam adı ile Users dizininde bir LocalDB veritabanı oluşturur (bu durumda `MvcMovie.Models.MovieDBContext`). Veritabanına sahip olduğu sürece, istediğiniz herhangi bir şey için bir ad verebilirsiniz *. MDF* soneki. Örneğin, *MyFilms. mdf*veritabanına ad vereceğiz.

Daha sonra, film verilerini göstermek ve kullanıcıların yeni film listeleri oluşturmasına izin vermek için kullanabileceğiniz yeni bir `MoviesController` sınıfı oluşturacaksınız.

> [!div class="step-by-step"]
> [Önceki](adding-a-model.md)
> [İleri](accessing-your-models-data-from-a-controller.md)
