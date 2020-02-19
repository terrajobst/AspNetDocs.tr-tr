---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 4 | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvimini bir ASP.NET MV içinde nasıl çalışabileceğiniz hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457498"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 4

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, bir ASP.NET MVC web uygulamasında düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvim ile çalışma hakkında temel bilgiler verilir.

### <a name="adding-a-template-for-editing-dates"></a>Tarihleri düzenlemede şablon ekleme

Bu bölümde, ASP.NET MVC 'nin [veri türü](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliğinin **Tarih** numaralandırması ile işaretlenmiş model özelliklerini düzenlemesi için Kullanıcı arabirimini görüntülediği zaman, uygulanacak tarihleri düzenlemeniz için bir şablon oluşturacaksınız. Şablon yalnızca tarihi işler; zaman gösterilmez. Şablonda, tarihleri düzenlemek için bir yol sağlamak üzere [jQuery UI DatePicker](http://jqueryui.com/demos/datepicker/) açılan takvimini kullanacaksınız.

Başlamak için, *Movie.cs* dosyasını açın ve aşağıdaki kodda gösterildiği gibi, **Tarih** numaralandırması olan [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliğini `ReleaseDate` özelliğine ekleyin:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

Bu kod, `ReleaseDate` alanının her iki görüntüleme şablonu ve düzenleme şablonlarında zaman olmadan görüntülenmesine neden olur. Uygulamanız *Views\shared\editortemplates* klasöründe veya *Views\Movies\EditorTemplates* klasöründe bir *date. cshtml* şablonu içeriyorsa, bu şablon, düzenlenirken herhangi bir `DateTime` özelliğini işlemek için kullanılacaktır. Aksi takdirde, yerleşik ASP.NET şablon oluşturma sistemi bu özelliği bir tarih olarak görüntüler.

Uygulamayı çalıştırmak için CTRL+F5'e basın. Yayın tarihi için giriş alanının yalnızca tarihi göstermesini doğrulamak için bir düzenleme bağlantısı seçin.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

**Çözüm Gezgini**, *Görünümler* klasörünü genişletin, *paylaşılan* klasörünü genişletin ve ardından *Views\Shared\EditorTemplates* klasörüne sağ tıklayın.

**Ekle**' ye tıklayın ve ardından **görüntüle**' ye tıklayın. **Görünüm Ekle** iletişim kutusu görüntülenir.

**Görünüm adı** kutusuna &quot;Tarih&quot;yazın.

**Kısmi görünüm olarak oluştur** onay kutusunu seçin. **Düzen veya ana sayfa kullan** ve **kesin türü belirtilmiş bir görünüm oluştur** onay kutularının seçili olmadığından emin olun.

**Ekle**'ye tıklayın. *Views\shared\editortemplates\date.exe* şablonu oluşturulur.

Aşağıdaki kodu *Views\shared\editortemplates\date.exe* şablonuna ekleyin.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

İlk satır, modeli `DateTime` bir tür olacak şekilde bildirir. Düzenleme ve görüntüleme şablonlarında model türünü bildirmenize gerek olmasa da, görünümün geçirildiği modelin derleme zamanı denetimini elde etmeniz için en iyi uygulamadır. (Diğer bir deyişle, daha sonra Visual Studio görünümünde model için IntelliSense elde edersiniz.) Model türü bildirilmemiş ise, ASP.NET MVC onu [dinamik](https://msdn.microsoft.com/library/dd264741.aspx) bir tür olarak değerlendirir ve derleme zamanı tür denetimi yoktur. Modeli `DateTime` bir tür olacak şekilde bildirirseniz, türü kesin olarak belirlenmiş olur.

İkinci satır yalnızca bir Tarih alanından önce&quot; Tarih şablonu kullanarak &quot;görüntüleyen yalnızca sabit bir HTML biçimlemedir. Bu tarih şablonunun kullanıldığını doğrulamak için bu satırı geçici olarak kullanacaksınız.

Sonraki satır, bir metin kutusu olan `input` alanı işleyen bir [HTML. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) yardımcıdır. Yardımcının üçüncü parametresi, metin kutusu için sınıfını `datefield` ve `date`türüne ayarlamak için anonim bir tür kullanır. (`class` ' de C#ayrılmış olduğundan, C# ayrıştırıcıdaki `class` özniteliğini atlamak için `@` karakterini kullanmanız gerekir.)

`date` türü, HTML5 'e duyarlı tarayıcıların HTML5 Takvim denetimini işlemesini sağlayan HTML5 giriş türüdür. Daha sonra, `datefield` sınıfını kullanarak jQuery DatePicker `Html.TextBox` öğesine bağlamak için bazı JavaScript ekleyeceğiz.

Uygulamayı çalıştırmak için CTRL+F5'e basın. Şablon, bu görüntüde gösterildiği gibi, `ReleaseDate` metin girişi kutusundan hemen önceki&quot; Tarih şablonu kullanarak &quot;görüntülediğinden, düzenleme görünümündeki `ReleaseDate` özelliğinin düzenleme şablonunu kullandığını doğrulayabilirsiniz:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

Tarayıcınızda sayfanın kaynağını görüntüleyin. (Örneğin, sayfaya sağ tıklayın ve **kaynağı görüntüle**' yi seçin.) Aşağıdaki örnek, işlenen HTML 'deki `class` ve `type` özniteliklerini gösteren sayfanın bazı işaretlemesini gösterir.

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

*Views\shared\editortemplates\date.exe* şablonuna dönün ve tarih şablonu&quot; işaretlemesini kullanarak &quot;kaldırın. Artık tamamlanan şablon şöyle görünür:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>NuGet kullanarak jQuery kullanıcı arabirimi DatePicker açılan takvimi ekleme

Bu bölümde, [jQuery UI DatePicker](http://jqueryui.com/demos/datepicker/) açılan takvimini tarih-Düzenle şablonuna ekleyeceksiniz. [JQuery kullanıcı arabirimi](http://jqueryui.com/) kitaplığı, animasyon, gelişmiş etkiler ve özelleştirilebilir pencere öğeleri için destek sağlar. JQuery JavaScript kitaplığının üzerine kurulmuştur. DatePicker açılır penceresi, bir dize girmek yerine bir takvim kullanarak tarihleri kolay ve doğal olarak girmeye olanak sağlar. Açılan takvim Ayrıca kullanıcıları yasal tarihlerle sınırlar — bir tarih için normal metin girişi, `2/33/1999` (33rd, 1999) gibi bir değer girmenizi sağlar, ancak [jQuery UI DatePicker](http://jqueryui.com/demos/datepicker/) açılan takvim buna izin vermez.

İlk olarak, jQuery kullanıcı arabirimi kitaplıklarını yüklemeniz gerekir. Bunu yapmak için, Visual Studio 2010 ve Visual Web Developer 'ın SP1 sürümlerinde bulunan bir paket yöneticisi olan NuGet ' i kullanacaksınız.

Visual Web Developer 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi** ' ni seçin ve ardından **NuGet Paketlerini Yönet**' i seçin.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

Note: **Araçlar** menüsünde NuGet **Paket Yöneticisi** komutu görünmezse NuGet Web sitesinin [NuGet yükleme](http://docs.nuget.org/docs/start-here/installing-nuget) sayfasındaki yönergeleri izleyerek NuGet 'i yüklemeniz gerekir.   
  
Visual Web Developer yerine Visual Studio kullanıyorsanız, **Araçlar** menüsünden **NuGet Paket Yöneticisi** ' ni seçin ve ardından **kitaplık paketi başvurusu Ekle**' yi seçin.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

**Mvcmovie-NuGet Paketlerini Yönet** iletişim kutusunda, sol taraftaki **çevrimiçi** sekmesine tıklayın ve sonra arama kutusuna jQuery. UI&quot; &quot;girin. J **Query UI pencere öğeleri: DatePicker**öğesini seçin, sonra da **Install** düğmesini seçin.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet, bu hata ayıklama sürümlerini ve jQuery UI Core 'un küçültülmüş sürümlerini ve jQuery kullanıcı arabirimi Tarih seçicisini projenize ekler:

- *jQuery. UI. Core. js*
- *jQuery. UI. Core. min. js*
- *jQuery. UI. DatePicker. js*
- *jQuery. UI. DatePicker. min. js*

Note: hata ayıklama sürümleri ( *. min. js* uzantısı olmayan dosyalar) hata ayıklama için yararlıdır, ancak bir üretim sitesinde yalnızca küçültülmüş sürümleri dahil edersiniz.

JQuery tarih seçiciyi gerçekten kullanmak için, takvim pencere öğesini düzenleme şablonuna bağlayan bir jQuery betiği oluşturmanız gerekir. **Çözüm Gezgini**, *betikler* klasörüne sağ tıklayın ve **Ekle**, **Yeni öğe**ve ardından **JScript dosyası**' nı seçin. *Datepickerready. js*dosyasını adlandırın.

Aşağıdaki kodu *Datepickerready. js* dosyasına ekleyin:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

JQuery hakkında bilgi sahibi değilseniz, bu işlemin kısa bir açıklaması aşağıda verilmiştir: ilk satır, bir sayfadaki tüm DOM öğeleri yüklendiğinde çağrılan &quot;jQuery Ready&quot; işlevidir. İkinci satır `datefield`sınıf adına sahip tüm DOM öğelerini seçer, ardından her biri için `datepicker` işlevini çağırır. (`datefield` sınıfını, öğreticinin önceki kısımlarında yer alan *Views\shared\editortemplates\date.exe* şablonuna eklendiğini unutmayın.)

Sonra, *Views\shared\\_Layout. cshtml* dosyasını açın. Tarih seçiciyi kullanabilmeniz için tüm gerekli olan aşağıdaki dosyalara başvurular eklemeniz gerekir:

- *İçerik/Temalar/Base/jQuery. UI. Core. css*
- *İçerik/Temalar/Base/jQuery. UI. DatePicker. css*
- *İçerik/Temalar/Base/jQuery. UI. theme. css*
- *jQuery. UI. Core. min. js*
- *jQuery. UI. DatePicker. min. js*
- *DatePickerReady. js*

Aşağıdaki örnek, *Views\shared\\_Layout. cshtml* dosyasında `head` öğesinin altına eklemeniz gereken gerçek kodu gösterir.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

Tüm `head` bölümü burada gösterilmektedir:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL içerik Yardımcısı](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) yöntemi, kaynak yolunu mutlak bir yola dönüştürür. Uygulama IIS üzerinde çalışırken bu kaynaklara doğru başvurmak için `@URL.Content` kullanmanız gerekir.

Uygulamayı çalıştırmak için CTRL+F5'e basın. Bir düzenleme bağlantısı seçin ve ekleme noktasını **ReleaseDate** alanına yerleştirin. JQuery kullanıcı arabirimi açılır Takvimi görüntülenir.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

Çoğu jQuery denetimi gibi, DatePicker ise bunları kapsamlı şekilde özelleştirmenize olanak tanır. Bilgi için bkz. görsel özelleştirme: [jQuery kullanıcı arabirimi](http://learn.jquery.com/jquery-ui/getting-started/) sitesinde [jQuery kullanıcı arabirimi teması tasarlama](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) .

### <a name="supporting-the-html5-date-input-control"></a>HTML5 tarih girişi denetimini destekleme

Daha fazla tarayıcı HTML5 'i destekledikleri için, `date` Input öğesi gibi yerel HTML5 girişini kullanmak ve jQuery kullanıcı arabirimi takvimini kullanmak istemezsiniz. Tarayıcı tarafından destekliyorsa HTML5 denetimlerini otomatik olarak kullanmak için uygulamanıza Logic ekleyebilirsiniz. Bunu yapmak için, *Datepickerready. js* dosyasının içeriğini aşağıdakiler ile değiştirin:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

Bu betiğin ilk satırı HTML5 Tarih girişinin desteklendiğini doğrulamak için Modernizr kullanır. Desteklenmiyorsa, bunun yerine jQuery kullanıcı arabirimi tarih seçici kullanıma açılır. ([Modernizr](http://www.modernizr.com/docs/) , HTML5 ve CSS3 'ın yerel uygulamalarının kullanılabilirliğini algılayan açık kaynaklı bir JavaScript kitaplığıdır. Modernizr, oluşturduğunuz tüm yeni ASP.NET MVC projelerine dahil edilmiştir.)

Bu değişikliği yaptıktan sonra, Opera 'yı destekleyen bir tarayıcı kullanarak (Opera 11 gibi) test edebilirsiniz. HTML5 uyumlu bir tarayıcı kullanarak uygulamayı çalıştırın ve bir film girişini düzenleyin. JQuery kullanıcı arabirimi açılır takvimi yerine HTML5 tarih denetimi kullanılır:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

Tarayıcıların yeni sürümleri daha artımlı olarak çalıştığından, Web sitenize çok sayıda HTML5 desteği sunan kod eklemektir. Örneğin, daha güçlü bir *Datepickerready. js* betiği aşağıda verilmiştir ve bu da sitenizin HTML5 Tarih denetimini yalnızca kısmen desteklediği tarayıcıları destekliyor.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

Bu betik, HTML5 Tarih denetimini tam olarak desteklemeyen `date` türündeki HTML5 `input` öğeleri seçer. Bu öğeler için, jQuery kullanıcı arabirimi açılan takvimini takar ve `date` `type` özniteliğini `text`olarak değiştirir. `type` özniteliğini `date` `text`olarak değiştirerek kısmi HTML5 Tarih desteği ortadan kalkar. Daha sağlam bir *Datepickerready. js* betiğinin [JSFIDDLE](http://jsfiddle.net/XSTK8/15/)adresinde bulabilirsiniz.

### <a name="adding-nullable-dates-to-the-templates"></a>Şablonlara null yapılabilir tarihler ekleme

Mevcut tarih şablonlarından birini kullanırsanız ve null bir tarih geçirirseniz, bir çalışma zamanı hatası alırsınız. Tarih şablonlarını daha sağlam hale getirmek için bunları null değerleri işleyecek şekilde değiştirirsiniz. Null yapılabilir tarihleri desteklemek için *Views\shared\displaytemplates\datetime.exe. cshtml* içindeki kodu aşağıdaki şekilde değiştirin:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

Model **null**olduğunda kod boş bir dize döndürür.

*Views\shared\editortemplates\date.exe* dosyasındaki kodu aşağıdaki şekilde değiştirin:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

Bu kod çalıştığında, model null değilse modelin `DateTime` değeri kullanılır. Model null ise, bunun yerine geçerli tarih kullanılır.

### <a name="wrapup"></a>Wrapup

Bu öğreticide ASP.NET şablonlu yardımcıların temelleri ele alınmıştır ve bir ASP.NET MVC uygulamasında jQuery UI DatePicker açılan takviminin nasıl kullanılacağı gösterilir. Daha fazla bilgi için şu kaynakları deneyin:

- Yerelleştirme hakkında daha fazla bilgi için bkz. [ASP.NET MVC 'de Rampacqueryuı DatePicker](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).
- JQuery kullanıcı arabirimi hakkında daha fazla bilgi için bkz. [jQuery kullanıcı arabirimi](http://docs.jquery.com/UI).
- DatePicker denetimini yerelleştirmek hakkında daha fazla bilgi için bkz. [UI/DatePicker/yerelleştirme](http://docs.jquery.com/UI/Datepicker/Localization).
- ASP.NET MVC şablonları hakkında daha fazla bilgi için bkz. [ASP.NET MVC 2 şablonlarında](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)atacan solson 'ın blog serisi. Serinin ASP.NET MVC 2 için yazılmış olmasına karşın, bu malzeme geçerli ASP.NET MVC sürümü için de geçerlidir.

> [!div class="step-by-step"]
> [Öncekini](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
