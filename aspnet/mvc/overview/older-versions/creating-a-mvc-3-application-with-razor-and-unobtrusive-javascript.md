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
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a>Razor ve Unobtrusive JavaScript ile MVC 3 Uygulaması Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

> Kullanıcı listesi örnek Web uygulaması, Razor görünüm altyapısını kullanarak ASP.NET MVC 3 uygulamaları oluşturmanın ne kadar kolay olduğunu gösterir. Örnek uygulama, Kullanıcı oluşturma, görüntüleme, görüntüleme ve silme gibi işlevleri içeren bir kurgusal Kullanıcı listesi Web sitesi oluşturmak için ASP.NET MVC sürüm 3 ve Visual Studio 2010 ile yeni Razor görünümü altyapısının nasıl kullanılacağını gösterir.
> 
> Bu öğreticide, kullanıcı listesi örnek ASP.NET MVC 3 uygulaması oluşturmak için uygulanan adımlar açıklanmaktadır. Ve VB kaynak kodu içeren C# bir Visual Studio projesi, bu konuya eşlik eden bir şekilde kullanılabilir: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114). Bu öğreticiyle ilgili sorularınız varsa, lütfen bunları [MVC forumuna](https://forums.asp.net/1146.aspx)gönderin.

## <a name="overview"></a>Genel bakış

Oluşturmakta olduğunuz uygulama basit bir kullanıcı listesi Web sitesidir. Kullanıcılar Kullanıcı bilgilerini girebilir, görüntüleyebilir ve güncelleştirebilir.

![Örnek site](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

VB ve C# tamamlanmış projeyi [buradan](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)indirebilirsiniz.

## <a name="creating-the-web-application"></a>Web uygulaması oluşturma

Öğreticiyi başlatmak için Visual Studio 2010 ' i açın ve *ASP.NET MVC 3 Web uygulaması* şablonunu kullanarak yeni bir proje oluşturun. Uygulamayı &quot;Mvc3Razor&quot;olarak adlandırın.

[Yeni MVC 3 projesi ![](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)

**Yeni ASP.NET MVC 3 projesi** Iletişim kutusunda **Internet uygulaması**' nı seçin, Razor görünüm altyapısını seçin ve ardından **Tamam**' a tıklayın.

![Yeni ASP.NET MVC 3 proje iletişim kutusu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

Bu öğreticide, ASP.NET üyelik sağlayıcısını kullanmayacak ve bu sayede oturum açma ve üyelikle ilişkili tüm dosyaları silebilirsiniz. **Çözüm Gezgini**, aşağıdaki dosya ve dizinleri kaldırın:

- *Controllers\AccountController*
- *Models\accountmodellerini*
- *Views\Shared\\_LogOnPartial*
- *Views\account* (ve bu dizindeki tüm dosyalar)

![Soln exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<em>\_Layout. cshtml</em> dosyasını düzenleyin ve `logindisplay` adlı `<div>` öğesi içindeki biçimlendirmeyi <em>&quot;</em>oturum açma devre dışı&quot;iletisiyle değiştirin. Aşağıdaki örnekte yeni biçimlendirme gösterilmektedir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a>Model ekleme

**Çözüm Gezgini**, *modeller* klasörüne sağ tıklayın, **Ekle**' yi ve ardından **sınıf**' ı seçin.

![Yeni Kullanıcı MDL sınıfı](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

`UserModel`sınıfı adlandırın. *UserModel* dosyasının içeriğini aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

`UserModel` sınıfı kullanıcıları temsil eder. Sınıfın her üyesine, [Dataaçıklamalarda](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki [gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelikle açıklama eklenir. [Dataaçıklamalarda](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki öznitelikler, Web uygulamaları için otomatik istemci ve sunucu tarafı doğrulaması sağlar.

`UserModel` ve `Users` sınıflarına erişebilmek için `HomeController` sınıfını açın ve bir `using` yönergesi ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

`HomeController` bildiriminden hemen sonra, aşağıdaki yorumu ve başvuruyu bir `Users` sınıfına ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

`Users` sınıfı, bu öğreticide kullanacağınız Basitleştirilmiş, bellek içi bir veri deposudur. Gerçek bir uygulamada, Kullanıcı bilgilerini depolamak için bir veritabanı kullanırsınız. `HomeController` dosyanın ilk birkaç satırı aşağıdaki örnekte gösterilmiştir:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

Bir sonraki adımda Kullanıcı modelinin scafkatlama Sihirbazı tarafından kullanılabilmesi için uygulamayı oluşturun.

## <a name="creating-the-default-view"></a>Varsayılan görünüm oluşturma

Sonraki adım, kullanıcıları görüntülemek için bir eylem yöntemi ve görünümü eklemektir.

Var olan *Views\home\ındex* dosyasını silin. Kullanıcıları göstermek için yeni bir *Dizin* dosyası oluşturacaksınız.

`HomeController` sınıfında, `Index` yönteminin içeriğini aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

`Index` yönteminin içine sağ tıklayın ve ardından **Görünüm Ekle**' ye tıklayın.

![Görünüm Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

Kesin olarak **belirlenmiş görünüm oluştur** seçeneğini belirleyin. **Görünüm verileri sınıfı**için **Mvc3Razor. modeller. userModel**öğesini seçin. ( **Veri sınıfı görüntüle** kutusunda **Mvc3Razor. modeller. userModel** görmüyorsanız projeyi derlemeniz gerekir.) Görünüm altyapısının **Razor**olarak ayarlandığından emin olun. İçeriği **listeye** **görüntüle** ' yi belirleyin ve ardından **Ekle**' ye tıklayın.

![Dizin görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

Yeni görünüm, `Index` görünümüne geçirilen kullanıcı verilerini otomatik olarak yapı haline getiriliyor. Yeni oluşturulan *Views\home\ındex* dosyasını inceleyin. **Yeni oluştur**, **Düzenle**, **Ayrıntılar**ve **Sil** bağlantıları çalışmıyor, ancak sayfanın geri kalanı işlevsel. Sayfayı çalıştırın. Kullanıcıların listesini görürsünüz.

![Dizin sayfası](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

*Index. cshtml* dosyasını açın ve **Düzenle**, **Ayrıntılar**ve **Sil** `ActionLink` işaretlemesini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

Kullanıcı adı, **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarında seçili kaydı bulmak için kimlik olarak kullanılır.

## <a name="creating-the-details-view"></a>Ayrıntılar görünümü oluşturuluyor

Sonraki adım, Kullanıcı ayrıntılarını görüntülemek için bir `Details` eylem yöntemi ve görünümü eklemektir.

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

Aşağıdaki `Details` yöntemini giriş denetleyicisine ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

`Details` yönteminin içine sağ tıklayın ve ardından <strong>Görünüm Ekle</strong>' yi seçin. <strong>Görünüm verileri sınıf</strong> kutusunun <strong>Mvc3Razor. modeller. userModel</strong>içerdiğini doğrulayın<em>.</em> Ayrıntıları <strong>görüntüle</strong> ' yi seçin ve ardından <strong>Ekle</strong>' ye tıklayın.

![Ayrıntı görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

Uygulamayı çalıştırın ve bir ayrıntılar bağlantısı seçin. Otomatik yapı iskelesi modeldeki her bir özelliği gösterir.

![Ayrıntılar](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a>Düzenleme görünümü oluşturuluyor

Aşağıdaki `Edit` yöntemini giriş denetleyicisine ekleyin.

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

Önceki adımlarda olduğu gibi bir görünüm ekleyin, ancak **düzenleme**Için **içerik görüntüle** seçeneğini belirleyin.

![Düzenleme görünümü Ekle](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

Uygulamayı çalıştırın ve kullanıcılardan birinin adını ve soyadını düzenleyin. `UserModel` sınıfına uygulanan `DataAnnotation` kısıtlamalarını ihlal ederseniz, formu gönderdiğinizde, sunucu kodu tarafından üretilen doğrulama hatalarını görürsünüz. Örneğin, &quot;Ann&quot; adını&quot;&quot;olarak değiştirirseniz, formu gönderdiğinizde şu hata görüntülenir:

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

Bu öğreticide, Kullanıcı adını birincil anahtar olarak değerlendiriyorsunuz. Bu nedenle, Kullanıcı adı özelliği değiştirilemez. *Edit. cshtml* dosyasında, `Html.BeginForm` deyimden hemen sonra, Kullanıcı adını gizli bir alan olarak ayarlayın. Bu, özelliğin modele geçirilmesine neden olur. Aşağıdaki kod parçası `Hidden` deyimin yerleşimini gösterir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

Kullanıcı adının `TextBoxFor` ve `ValidationMessageFor` işaretlemesini bir `DisplayFor` çağrısıyla değiştirin. `DisplayFor` yöntemi, özelliği salt okunurdur bir öğe olarak görüntüler. Aşağıdaki örnekte, tamamlanan biçimlendirme gösterilmektedir. Özgün `TextBoxFor` ve `ValidationMessageFor` çağrıları, Razor başlangıç-açıklama ve son açıklama karakterleriyle (`@* *@`) yorum yapılır

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a>Istemci tarafı doğrulamayı etkinleştirme

ASP.NET MVC 3 ' te istemci tarafı doğrulamasını etkinleştirmek için iki bayrak ayarlamanız ve üç JavaScript dosyası eklemeniz gerekir.

Uygulamanın *Web. config* dosyasını açın. Uygulama ayarlarında `that ClientValidationEnabled` ve `UnobtrusiveJavaScriptEnabled` true olarak ayarlandığını doğrulayın. Kök *Web. config* dosyasındaki aşağıdaki parça doğru ayarları gösterir:

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

`UnobtrusiveJavaScriptEnabled` true olarak ayarlamak, untrusive Ajax ve unobtrusive istemci doğrulamasını sağlar. Unobtrusive doğrulaması kullandığınızda, doğrulama kuralları HTML5 özniteliklerine açıktır. HTML5 öznitelik adları yalnızca küçük harf, sayı ve kısa çizgi içerebilir.

`ClientValidationEnabled` true olarak ayarlamak, istemci tarafı doğrulamayı sağlar. Bu anahtarları uygulama *Web. config* dosyasında ayarlayarak, istemci doğrulaması ve uygulamanın tamamı Için JavaScript 'i devre altına al özelliğini etkinleştirirsiniz. Ayrıca, aşağıdaki kodu kullanarak bu ayarları ayrı görünümlerde veya denetleyici yöntemlerinde etkinleştirebilir veya devre dışı bırakabilirsiniz:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

Ayrıca, çeşitli JavaScript dosyalarını işlenmiş görünümde de eklemeniz gerekir. Tüm görünümlere JavaScript eklemenin kolay bir yolu, bunları *Views\shared\\_Layout. cshtml* dosyasına eklemektir. *\_Layout. cshtml* dosyasının `<head>` öğesini şu kodla değiştirin:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

İlk iki jQuery komut dosyası Microsoft Ajax Content Delivery Network (CDN) tarafından barındırılır. Microsoft Ajax CDN 'nin avantajlarından yararlanarak uygulamalarınızın ilk isabet performansını önemli ölçüde artırabilirsiniz.

Uygulamayı çalıştırın ve bir düzenleme bağlantısına tıklayın. Sayfanın kaynağını tarayıcıda görüntüleyin. Tarayıcı kaynağı `data-val` formun birçok özniteliğini gösterir (veri doğrulaması için). İstemci doğrulaması ve unobtrusive JavaScript etkinleştirildiğinde, istemci doğrulama kuralına sahip giriş alanları, engellemeyen istemci doğrulamasını tetiklemek için `data-val="true"` özniteliğini içerir. Örneğin, modeldeki `City` alanı [gerekli](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) öznitelikle tasarlanmıştı ve bu, aşağıdaki örnekte gösterilen HTML ile sonuçlanır:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

Her istemci doğrulama kuralı için, `data-val-rulename="message"`form içeren bir öznitelik eklenir. Daha önce gösterilen `City` alan örneğini kullanarak, gerekli istemci doğrulama kuralı `data-val-required` özniteliğini ve &quot;City alanı gereklidir&quot;ileti üretir. Uygulamayı çalıştırın, kullanıcılardan birini düzenleyin ve `City` alanını temizleyin. Alanı kapattığınızda, bir istemci tarafı doğrulama hata iletisi görürsünüz.

![Şehir gerekli](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

Benzer şekilde, istemci doğrulama kuralındaki her bir parametre için `data-val-rulename-paramname=paramvalue`form olan bir öznitelik eklenir. Örneğin, `FirstName` özelliğine [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliğiyle açıklama eklenir ve en az 3 ve en fazla 8 uzunluğunda bir değer belirtir. `length` adlı veri doğrulama kuralının parametre adı `max` ve 8 parametre değeri vardır. Aşağıda, kullanıcılardan birini düzenlerken `FirstName` alanı için oluşturulan HTML gösterilmektedir:

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

Engellenemeyen istemci doğrulaması hakkında daha fazla bilgi için bkz. [ASP.NET MVC 3 ' te](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) atacan solson bloguna yönelik Istemci doğrulamasını kaldırma.

> [!NOTE]
> ASP.NET MVC 3 Beta sürümünde, bazen istemci tarafı doğrulamayı başlatmak için formu göndermeniz gerekir. Bu, son sürüm için değişebilir.

## <a name="creating-the-create-view"></a>Oluşturma görünümü oluşturuluyor

Sonraki adım, kullanıcının yeni bir Kullanıcı oluşturmasını sağlamak için bir `Create` eylem yöntemi ve görünümü eklemektir. Aşağıdaki `Create` yöntemini giriş denetleyicisine ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

Önceki adımlarda olduğu gibi bir görünüm ekleyin, ancak **oluşturulacak** **görünümü içerik** olarak ayarlayın.

![Görünüm Oluşturma](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

Uygulamayı çalıştırın, **Oluştur** bağlantısını seçin ve yeni bir kullanıcı ekleyin. `Create` yöntemi, istemci tarafı ve sunucu tarafı doğrulamasından otomatik olarak yararlanır. &quot;ben X&quot;gibi boşluk içeren bir Kullanıcı adı girmeyi deneyin. Kullanıcı adı alanından kaldırdığınızda, bir istemci tarafı doğrulama hatası (`White space is not allowed`) görüntülenir.

## <a name="add-the-delete-method"></a>Delete metodunu ekleyin

Öğreticiyi tamamlayabilmeniz için aşağıdaki `Delete` yöntemini giriş denetleyicisine ekleyin:

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

Önceki adımlarda olduğu gibi `Delete` bir görünüm ekleyin ve **Silinecek** **içeriği görüntüle** olarak ayarlar.

![Görünümü Sil](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

Artık doğrulama ile basit ancak tamamen işlevsel ASP.NET MVC 3 uygulamanız vardır.
