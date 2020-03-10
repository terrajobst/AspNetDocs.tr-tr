---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
title: Ayrıntıları ve silme yöntemlerini geliştirme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: c5c14ef0-c128-4dc1-8c01-7f0fdb09e411
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 08d80cac071907e927bb30df53c6f84a28f53156
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599955"
---
# <a name="improving-the-details-and-delete-methods-vb"></a>Details ve Delete Metotlarını Geliştirme (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur. [Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/improving-the-details-and-delete-methods.md) geçin.

Öğreticinin bu bölümünde otomatik olarak oluşturulan `Details` ve `Delete` yöntemlerinde bazı geliştirmeler yaparsınız. Bu değişiklikler gerekli değildir, ancak yalnızca birkaç küçük bit kod ile uygulamayı kolayca geliştirebilirsiniz.

## <a name="improving-the-details-and-delete-methods"></a>Ayrıntıları ve silme yöntemlerini geliştirme

`Movie` denetleyiciyi iskele aldığınızda, ASP.NET MVC tarafından üretilen ve harika çalışan, ancak yalnızca birkaç küçük değişiklikle daha sağlam hale getirilebilir olan kod.

`Movie` denetleyiciyi açın ve bir film bulunamadığında `HttpNotFound` döndürerek `Details` yöntemini değiştirin. Ayrıca, kendisine geçirilen KIMLIĞI için varsayılan bir değer ayarlamak üzere `Details` metodunu değiştirmelisiniz. (Bu öğreticinin [6. bölümünde](examining-the-edit-methods-and-edit-view.md) `Edit` yönteminde benzer değişiklikler yaptınız.) Ancak, `HttpNotFound` yöntemi bir `ViewResult` nesnesi döndürmediği için `ViewResult` `Details` yönteminin dönüş türünü `ActionResult`olarak değiştirmeniz gerekir. Aşağıdaki örnekte, değiştirilmiş `Details` yöntemi gösterilmektedir.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample1.vb)]

Code First, `Find` yöntemini kullanarak verileri aramanızı kolaylaştırır. Yönteminde derlediğimiz önemli bir güvenlik özelliği, kodun, kod ile herhangi bir şey yapmayı denemeden önce `Find` yönteminin bir filmi buldığını doğrulamaktır. Örneğin, bir korsan `http://localhost:xxxx/Movies/Details/1` bağlantıları tarafından oluşturulan URL 'yi `http://localhost:xxxx/Movies/Details/12345` (veya gerçek bir filmi temsil eden başka bir değer) gibi bir şeye değiştirerek siteye hata verebilir. Null bir filmi denetmezseniz, bu bir veritabanı hatasına neden olabilir.

Benzer şekilde, `Delete` ve `DeleteConfirmed` yöntemlerini, ID parametresi için varsayılan bir değer belirtmek ve bir film bulunamadığında `HttpNotFound` döndürmek için değiştirin. `Movie` denetleyicisindeki güncelleştirilmiş `Delete` yöntemleri aşağıda gösterilmiştir.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample2.vb)]

`Delete` yönteminin verileri silmediğini unutmayın. Bir GET isteğine yanıt olarak silme işlemi gerçekleştirme (veya bu konuyla ilgili olarak, düzenleme işlemi gerçekleştirme, oluşturma işlemi yapma veya verileri değiştiren başka bir işlem) bir güvenlik deliği açılır. Bunun hakkında daha fazla bilgi için bkz. Stephen Walther Web günlüğü girdisi [ASP.NET MVC ipucu #46 — güvenlik delikleri oluşturdıklarından, silme bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

Verileri silen `HttpPost` yöntemi, HTTP POST yöntemine benzersiz bir imza veya ad vermek için `DeleteConfirmed` olarak adlandırılır. İki yöntem imzası aşağıda gösterilmiştir:

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample3.vb)]

Ortak dil çalışma zamanı (CLR), aşırı yüklenmiş yöntemlerin benzersiz bir imzaya sahip olmasını gerektirir (aynı adı, farklı parametre listesini). Bununla birlikte, her ikisi de aynı imzayı gerektiren iki Delete yöntemi (GET için bir tane) ve diğeri için de gereklidir. (Her ikisi de parametre olarak tek bir tamsayıyı kabul etmelidir.)

Bunu sıralamak için birkaç şey yapabilirsiniz. Bunlardan biri, yöntemlere farklı adlar vermektir. Bu, önceki örnekte yaptığımız şeydir. Ancak, bu küçük bir sorun ortaya çıkarır: ASP.NET bir URL 'nin segmentlerini ada göre eylem yöntemlerine eşler ve bir yöntemi yeniden adlandırırsanız, yönlendirme normalde bu yöntemi bulamaz. Çözüm, örnekte gördüğünüz şeydir. Bu, `DeleteConfirmed` yöntemine `ActionName("Delete")` özniteliğini eklemektir. Bu, bir POST isteği için <em>/Delete/</em>IÇEREN bir URL 'nin `DeleteConfirmed` yöntemini bulabilmesi için yönlendirme sistemi için eşlemeyi etkili bir şekilde gerçekleştirir.

Özdeş adlara ve imzalara sahip Yöntemler ile ilgili bir sorunu önlemenin bir diğer yolu da, yapay, POST yönteminin imzasını kullanılmayan bir parametre içerecek şekilde değiştirir. Örneğin, bazı geliştiriciler POST yöntemine geçirilen `FormCollection` bir parametre türü ekler ve sonra yalnızca parametresini kullanmaz:

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample4.vb)]

## <a name="wrapping-up"></a>Yukarı kaydırma

Artık SQL Server Compact bir veritabanında veri depolayan bir tamamen ASP.NET MVC uygulamanız var. Film oluşturabilir, okuyabilir, güncelleştirebilir, silebilir ve arayabilirsiniz.

![](improving-the-details-and-delete-methods/_static/image1.png)

Bu temel öğretici, denetleyiciler oluşturma, bunları görünümlerle ilişkilendirme ve sabit kodlanmış verileri geçirme ile çalışmaya başladım. Daha sonra bir veri modeli oluşturdunuz ve tasarlamış olursunuz. Entity Framework Code First anında veri modelinden bir veritabanı oluşturdu ve ASP.NET MVC scafkatlama sistemi, temel CRUD işlemleri için eylem yöntemleri ve görünümleri otomatik olarak oluşturdu. Daha sonra kullanıcıların veritabanını aramasına izin veren bir arama formu eklediniz. Veritabanını yeni bir veri sütunu içerecek şekilde değiştirdiniz ve sonra bu yeni verileri oluşturmak ve göstermek için iki sayfa güncelleştirmiş olursunuz. Veri modelini `DataAnnotations` ad alanındaki özniteliklerle işaretleyerek doğrulama eklediniz. Elde edilen doğrulama, istemci ve sunucuda çalışır.

Uygulamanızı dağıtmak istiyorsanız, öncelikle uygulamayı yerel IIS 7 sunucunuzda test etmek yararlı olur. Bu [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) bağlantısını, ASP.net UYGULAMALARı için IIS ayarını etkinleştirmek üzere kullanabilirsiniz. Aşağıdaki dağıtım bağlantılarına bakın:

- [ASP.NET dağıtım Içerik Haritası](https://msdn.microsoft.com/library/dd394698.aspx)
- [IIS 7. x etkinleştiriliyor](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [Web uygulaması projeleri dağıtımı](https://msdn.microsoft.com/library/dd394698.aspx)

Artık ASP.NET MVC uygulaması ve [MVC müzik deposu](../../mvc-music-store/mvc-music-store-part-1.md) öğreticileri [Için Entity Framework veri MODELI oluşturma](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) , [MSDN 'deki ASP.net makalelerini](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)araştırmak ve ASP.NET MVC hakkında daha fazla bilgi edinmek için [https://asp.net/mvc](https://asp.net/mvc) birçok video ve kaynağa göz atın! [ASP.NET MVC forumları](https://forums.asp.net/1146.aspx) , soru sormak için harika bir yerdir.

Keyfini çıkarın!

— Scott Hanselman ([http://hanselman.com](http://hanselman.com) ve Twitter 'da [@shanselman](http://twitter.com/shanselman) ) ve Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [Öncekini](adding-validation-to-the-model.md)
