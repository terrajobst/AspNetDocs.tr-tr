---
uid: mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
title: Düzenleme yöntemleri ve düzenleme görünümü inceleniyor | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/06/2019
ms.assetid: 52a4d5fe-aa31-4471-b3cb-a064f82cb791
msc.legacyurl: /mvc/overview/getting-started/introduction/examining-the-edit-methods-and-edit-view
msc.type: authoredcontent
ms.openlocfilehash: 6cef963910b957e8b4ad7c7909385f6dbdff95c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582441"
---
# <a name="examining-the-edit-methods-and-edit-view"></a>Düzenleme Metotlarını ve Düzenleme Görünümünü İnceleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [Tutorial Note](index.md)]

Bu bölümde, film denetleyicisi için oluşturulan `Edit` eylem yöntemlerini ve görünümlerini inceleyeceksiniz. Ancak ilk olarak yayın tarihinin daha iyi görünmesini sağlamak için kısa bir göz atalım. *Models\movie.cs* dosyasını açın ve vurgulanan satırları aşağıda gösterildiği gibi ekleyin:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample1.cs?highlight=2,12-14)]

Ayrıca, tarih kültürünü aşağıdakine benzer hale getirebilirsiniz:

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample2.cs?highlight=3)]

Sonraki öğreticide [veri ek açıklamalarını](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ele alacağız. [Display](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayattribute.aspx) özniteliği bir alanın adı için (Bu durumda "ReleaseDate" yerine "Yayın tarihi") görüntüleneceğini belirtir. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği verilerin türünü belirtir, bu durumda bir tarih olur, bu nedenle alanda depolanan zaman bilgileri görüntülenmez. Chrome tarayıcısında, tarih biçimlerini yanlış işleyen bir hata için [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliği gereklidir.

Uygulamayı çalıştırın ve `Movies` denetleyicisine gidin. Bağlantı yaptığı URL 'yi görmek için fare işaretçisini bir **düzenleme** bağlantısı üzerine tutun.

![EditLink_sm](examining-the-edit-methods-and-edit-view/_static/image1.png)

**Düzenleme** bağlantısı, *Views\Movies\Index.cshtml* görünümündeki `Html.ActionLink` yöntemi tarafından oluşturulmuştur:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample3.cshtml)]

![HTML. ActionLink](examining-the-edit-methods-and-edit-view/_static/image2.png)

`Html` nesnesi, [System. Web. Mvc. WebViewPage](https://msdn.microsoft.com/library/gg402107(VS.98).aspx) temel sınıfında özelliği kullanılarak ortaya çıkarılan bir yardımcıdır. Yardımcı 'nın `ActionLink` yöntemi, denetleyicilerde eylem yöntemlerine bağlantı sağlayan HTML köprülerini dinamik olarak oluşturmayı kolaylaştırır. `ActionLink` yönteminin ilk bağımsız değişkeni işlenecek bağlantı metindir (örneğin, `<a>Edit Me</a>`). İkinci bağımsız değişken çağrılacak eylem yönteminin adıdır (Bu durumda `Edit` eylemi). Son bağımsız değişken, yol verilerini üreten [anonim bir nesnedir](https://weblogs.asp.net/scottgu/archive/2007/05/15/new-orcas-language-feature-anonymous-types.aspx) (Bu durumda, 4 ' ün kimliği).

Önceki görüntüde gösterilen oluşturulan bağlantı `http://localhost:1234/Movies/Edit/4`. Varsayılan yol ( *\_Start\RouteConfig.cs*konumunda kurulan), URL deseninin `{controller}/{action}/{id}`alır. Bu nedenle, ASP.NET `http://localhost:1234/Movies/Edit/4` `Movies` denetleyicinin `Edit` Action yöntemine bir isteğe çevirir. bu `ID` eşittir 4. *\_Start\RouteConfig.cs dosyasını uygulamadan* aşağıdaki kodu inceleyin. [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) YÖNTEMI, http isteklerini doğru denetleyiciye ve eylem yöntemine yönlendirmek ve Isteğe bağlı ID parametresini sağlamak için kullanılır. [MapRoute](../../older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs.md) yöntemi, denetleyici, eylem yöntemi ve rota verileri verilen URL 'leri oluşturmak için `ActionLink` gibi [htmlyardımcılar](https://msdn.microsoft.com/library/system.web.mvc.htmlhelper(v=vs.108).aspx) tarafından da kullanılır.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample4.cs?highlight=7)]

Ayrıca, bir sorgu dizesi kullanarak eylem yöntemi parametrelerini geçirebilirsiniz. Örneğin, URL `http://localhost:1234/Movies/Edit?ID=3` Ayrıca 3 `ID` parametresini `Movies` denetleyicisinin `Edit` Action yöntemine geçirir.

![EditQueryString](examining-the-edit-methods-and-edit-view/_static/image3.png)

`Movies` denetleyiciyi açın. İki `Edit` eylemi yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample5.cs?highlight=19-21)]

İkinci `Edit` Action yönteminin önünde `HttpPost` özniteliği olduğuna dikkat edin. Bu öznitelik, `Edit` yönteminin aşırı yüklemesinin yalnızca POST istekleri için çağrılabileceğini belirtir. `HttpGet` özniteliğini ilk düzenleme yöntemine uygulayabilirsiniz, ancak varsayılan değer olduğundan bu gerekli değildir. (`HttpGet` özniteliği `HttpGet` yöntemleri olarak örtük olarak atanmış eylem yöntemlerine başvuracağız.) [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) özniteliği, korsanların modelinize veri gönderme işlemini daha fazla tutan başka önemli bir güvenlik mekanizmasıdır. Yalnızca, değiştirmek istediğiniz bağlama özniteliğinde özellikleri eklemeniz gerekir. Fazla deftere nakil ve bağlama özniteliği hakkında bilgi edinmek için bkz. [fazla nakil güvenlik notum](https://go.microsoft.com/fwlink/?LinkId=317598). Bu öğreticide kullanılan basit modelde, modeldeki tüm verileri bağlamamız gerekir. [Validateantiforgerytoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) özniteliği, bir isteğin kullanımını engellemek için kullanılır ve düzenleme görünüm dosyasında (*Views\Movies\Edit.cshtml*) `@Html.AntiForgeryToken()` ile eşleştirilmiştir, bir bölüm aşağıda gösterilmiştir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample6.cshtml?highlight=9)]

`@Html.AntiForgeryToken()`, `Movies` denetleyicisinin `Edit` yönteminde eşleşmesi gereken gizli form Anti-forma belirteci oluşturur. MVC 'de öğreticide, siteler arası istek (XSRF veya CSRF olarak da bilinir) hakkında daha fazla bilgi edinmek için bkz. [MVC/CSRF önleme](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md).

`HttpGet` `Edit` yöntemi, film KIMLIĞI parametresini alır, Entity Framework `Find` yöntemini kullanarak filmi arar ve seçili filmi düzenleme görünümüne döndürür. Bir film bulunamazsa, [Httpnotfound](https://msdn.microsoft.com/library/gg453938(VS.98).aspx) döndürülür. Scafkatlama sistemi düzenleme görünümü oluştururken, `Movie` sınıfını inceledi ve sınıfın her özelliği için `<label>` ve `<input>` öğelerini işlemek üzere kodu oluşturmuştur. Aşağıdaki örnekte, Visual Studio scafkatlama sistemi tarafından oluşturulan düzenleme görünümü gösterilmektedir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample7.cshtml)]

Görünüm şablonunun dosyanın en üstünde bir `@model MvcMovie.Models.Movie` bildirimine sahip olduğuna dikkat edin; bu, görünümün görünüm şablonunun modelinin `Movie`türünde olmasını beklediğini belirtir.

Scafkatlanmış kod, HTML işaretlemesini kolaylaştırmak için çeşitli *yardımcı yöntemler* kullanır. [`Html.LabelFor`](https://msdn.microsoft.com/library/gg401864(VS.98).aspx) Yardımcısı alanın adını (&quot;başlık&quot;, &quot;releasedate&quot;, &quot;tarz&quot;veya &quot;Price&quot;) görüntüler. [`Html.EditorFor`](https://msdn.microsoft.com/library/system.web.mvc.html.editorextensions.editorfor(VS.98).aspx) Yardımcısı bir HTML `<input>` öğesi işler. [`Html.ValidationMessageFor`](https://msdn.microsoft.com/library/system.web.mvc.html.validationextensions.validationmessagefor(VS.98).aspx) Yardımcısı, bu özellikle ilişkili tüm doğrulama iletilerini görüntüler.

Uygulamayı çalıştırın ve */filmler* URL 'sine gidin. Bir **düzenleme** bağlantısına tıklayın. Tarayıcıda, sayfanın kaynağını görüntüleyin. Form öğesi için HTML aşağıda gösterilmiştir.

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample8.cshtml?highlight=1-2)]

`<input>` öğeleri, `action` özniteliği */movies/Edit* URL 'sine gönderi olarak ayarlanan bir HTML `<form>` öğesidir. **Kaydet** düğmesine tıklandığında form verileri sunucuya gönderilir. İkinci satırda `@Html.AntiForgeryToken()` çağrısı tarafından oluşturulan gizli [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) belirteci gösterilmektedir.

## <a name="processing-the-post-request"></a>POST Isteği işleniyor

Aşağıdaki listede `Edit` eylem yönteminin `HttpPost` sürümü gösterilmektedir.

[!code-csharp[Main](examining-the-edit-methods-and-edit-view/samples/sample9.cs)]

[Validateantiforgeryıtoken](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute(v=vs.108).aspx) özniteliği, görünümdeki `@Html.AntiForgeryToken()` çağrısı tarafından oluşturulan [XSRF](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) belirtecini doğrular.

[ASP.NET MVC model Ciltçi](https://msdn.microsoft.com/library/dd410405.aspx) , postalanan form değerlerini alır ve `movie` parametresi olarak geçirilmiş bir `Movie` nesnesi oluşturur. `ModelState.IsValid`, formda gönderilen verilerin bir `Movie` nesnesini değiştirmek (düzenlemek veya güncelleştirmek) için kullanılabileceğini doğrular. Veriler geçerliyse, film verileri `db`(`MovieDBContext` örneği) `Movies` koleksiyonuna kaydedilir. Yeni film verileri, `MovieDBContext``SaveChanges` metodu çağırarak veritabanına kaydedilir. Veriler kaydedildikten sonra, kod, yeni yapılan değişiklikler de dahil olmak üzere, film koleksiyonunu görüntüleyen `MoviesController` sınıfının `Index` Action metoduna Kullanıcı yönlendirir.

İstemci tarafı doğrulaması bir alanın değerini belirler almaz, bir hata iletisi görüntülenir. JavaScript devre dışıysa, istemci tarafı doğrulaması devre dışı bırakılır. Ancak, sunucu, gönderilen değerleri geçerli değil olarak algılar ve form değerleri hata iletileriyle birlikte görüntülenir.

Doğrulama Öğreticinin ilerleyen kısımlarında daha ayrıntılı olarak incelendi.

*Edit. cshtml* görünüm şablonundaki `Html.ValidationMessageFor` yardımcıları, uygun hata iletilerini görüntülemeyi dikkate alır.

![abcNotValid](examining-the-edit-methods-and-edit-view/_static/image4.png)

Tüm `HttpGet` Yöntemler benzer bir düzene uyar. Bunlar bir film nesnesi (veya `Index`olması durumunda, nesne listesi) alır ve modeli görünüme geçirebilir. `Create` yöntemi, oluşturma görünümüne boş bir film nesnesi geçirir. Verileri oluşturan, düzenleme, silme ya da başka bir şekilde değiştiren tüm yöntemler, yönteminin `HttpPost` aşırı yüküne göre yapılır. HTTP GET yöntemindeki verileri değiştirmek, Web günlüğü gönderi girişi [ASP.NET MVC ipucu #46 – güvenlik delikleri oluşturdukları Için silme bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx). GET yöntemindeki verileri değiştirmek, HTTP en iyi uygulamalarını ve bu GET isteklerinin uygulamanızın [](http://en.wikipedia.org/wiki/Representational_State_Transfer) durumunu değiştirmemelidir. Diğer bir deyişle, bir GET işleminin gerçekleştirilmesi, yan etkileri olmayan ve kalıcı verilerinizi değiştirmeyen bir güvenli işlem olmalıdır.

## <a name="jquery-validation-for-non-english-locales"></a>Ingilizce olmayan yerel ayarlarda jQuery doğrulaması

ABD Ingilizcesi bilgisayar kullanıyorsanız, bu bölümü atlayabilir ve sonraki öğreticiye gidebilirsiniz. Bu öğreticinin globalize sürümünü [buradan](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=16475)indirebilirsiniz. Uluslararası duruma getirme için harika iki bölüm öğreticisi için bkz. [Nadeem 'ın ASP.NET MVC 5 Uluslararası duruma getirme](http://afana.me/post/aspnet-mvc-internationalization.aspx).

> [!NOTE]
> ondalık bir nokta ve ABD Ingilizcesi olmayan tarih biçimleri için virgül (&quot;,&quot;) kullanan Ingilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için, *globalize. js* ve belirli *kültürleri/globalize. kültürleri. js* dosyanızı ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve JavaScript 'i `Globalize.parseFloat`kullanacak şekilde eklemeniz gerekir. NuGet 'ten Ingilizce olmayan jQuery doğrulamasını alabilirsiniz. (Ingilizce yerel ayar kullanıyorsanız globalize ' yi yüklemeyin.)

1. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne tıklayın ve ardından **çözüm için NuGet Paketlerini Yönet**' e tıklayın.

    ![](examining-the-edit-methods-and-edit-view/_static/image5.png)
2. Sol bölmede, Araştır ' ı <strong>seçin *.</strong>*  (Aşağıdaki resme bakın.)
3. Giriş kutusuna * globalize * * yazın.

    `jQuery.Validation.Globalize`![](examining-the-edit-methods-and-edit-view/_static/image6.png) seçip `MvcMovie` ' yı **seçin.** *Scripts\jquery.exe Globalize\globalize.exe* dosyası projenize eklenecek. \* Scripts\jquery.exe Globalize\kültürler\* klasörü birçok kültür JavaScript dosyası içerir. Bu paketin yüklenmesi beş dakika sürebilir.

   Aşağıdaki kod Views\Movies\Edit.cshtml dosyasındaki değişiklikleri gösterir:

[!code-cshtml[Main](examining-the-edit-methods-and-edit-view/samples/sample10.cshtml)]

Her düzenleme görünümünde bu kodun yinelenmesinden kaçınmak için, düzen dosyasına taşıyabilirsiniz. Betik indirmeyi iyileştirmek için bkz. öğretici [paketme ve küçültmeye](../../performance/bundling-and-minification.md)yönelik.

Daha fazla bilgi için bkz. [ASP.NET MVC 3 Uluslararası duruma getirme](http://afana.me/post/aspnet-mvc-internationalization.aspx) ve [ASP.NET MVC 3 Uluslararası duruma getirme-Bölüm 2 (nerdakşam yemeği)](http://afana.me/post/aspnet-mvc-internationalization-part-2.aspx).

Geçici bir düzeltme olarak, doğrulamanız için yerel ayarda çalışmayı alamazsanız bilgisayarınızı ABD Ingilizcesi 'ni kullanmaya zorlayabilir veya tarayıcınızda JavaScript 'ı devre dışı bırakabilirsiniz. Bilgisayarınızı ABD Ingilizcesi kullanmaya zorlamak için, proje kök *Web. config* dosyasına Genelleştirme öğesini ekleyebilirsiniz. Aşağıdaki kod, kültürü Birleşik Devletler Ingilizce olarak ayarlanan Genelleştirme öğesini gösterir.

[!code-xml[Main](examining-the-edit-methods-and-edit-view/samples/sample11.xml)]

<a id="gettingstarted"></a><a id="jQueryAjaxJSON"></a>Sonraki öğreticide, arama işlevi uygulayacağız.

> [!div class="step-by-step"]
> [Önceki](accessing-your-models-data-from-a-controller.md)
> [İleri](adding-search.md)
