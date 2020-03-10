---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: ASP.NET Web Pages (Razor) sitelerindeki kullanıcı girişini doğrulama | Microsoft Docs
author: Rick-Anderson
description: Bu makalede, kullanıcıların HTML formlarında bir AS... içinde geçerli bilgiler girdiğinizden emin olmak için &mdash;, kullanıcılardan aldığınız bilgilerin nasıl doğrulanacağı açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563506"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerindeki kullanıcı girişini doğrulama

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, kullanıcıların bir ASP.NET Web Pages (Razor) sitesinde HTML formlarında geçerli bilgiler girdiğinizden emin olmak için &mdash;, kullanıcılardan aldığınız bilgilerin nasıl doğrulanacağı anlatılmaktadır.
> 
> Öğrenecekleriniz:
> 
> - Kullanıcı girişinin tanımladığınız doğrulama ölçütleriyle eşleşip eşleşmediğini denetleme.
> - Tüm doğrulama testlerinin başarılı olup olmadığını belirleme.
> - Doğrulama hatalarını görüntüleme (ve bunları biçimlendirme).
> - Doğrudan kullanıcılardan gelmeyen verileri doğrulama.
> 
> Makalesinde sunulan ASP.NET programlama kavramları şunlardır:
> 
> - `Validation` Yardımcısı.
> - `Html.ValidationSummary` ve `Html.ValidationMessage` yöntemleri.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

Bu makale aşağıdaki bölümleri içerir:

- [Kullanıcı girişi doğrulamasına genel bakış](#Overview_of_User_Input_Validation)
- [Kullanıcı girişini doğrulama](#Validating_User_Input)
- [Istemci tarafı doğrulama ekleme](#Adding_Client-Side_Validation)
- [Doğrulama hatalarını biçimlendirme](#Formatting_Validation_Errors)
- [Doğrudan kullanıcılardan gelmeyen verileri doğrulama](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>Kullanıcı girişi doğrulamasına genel bakış

Kullanıcılardan bir sayfaya bilgi girmesini isteme (örneğin, bir forma), girdikleri değerlerin geçerli olduğundan emin olmak önemlidir. Örneğin, kritik bilgileri eksik olan bir formu işlemek istemezsiniz.

Kullanıcılar bir HTML biçimine değer girerken, girdikleri değerler dizelerdir. Çoğu durumda, ihtiyacınız olan değerler, tamsayılar veya tarihler gibi bazı diğer veri türleridir. Bu nedenle, kullanıcıların girebileceği değerlerin uygun veri türlerine doğru şekilde dönüştürülebileceğinden de emin olmanız gerekir.

Ayrıca, değerler üzerinde belirli kısıtlamalara de sahip olabilirsiniz. Kullanıcılar, örneğin, doğru bir tamsayı girse bile, değerin belirli bir aralık dahilinde olduğundan emin olmanız gerekebilir.

![CSS stil sınıflarını kullanan doğrulama hataları](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **Önemli** Güvenlik için Kullanıcı girişinin doğrulanması da önemlidir. Kullanıcıların formlara girebilen değerleri kısıtladığınızda, birisinin sitenizin güvenliğini tehlikeye atabilecek bir değer girebilme olasılığını azaltırsınız.

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>Kullanıcı girişini doğrulama

ASP.NET Web Pages 2 ' de, Kullanıcı girişini sınamak için `Validator` yardımcısını kullanabilirsiniz. Temel yaklaşım şunlardır:

1. Hangi giriş öğelerinin (alanları) doğrulamak istediğinizi saptayın.

    Genellikle bir formdaki `<input>` öğelerdeki değerleri doğrularsınız. Ancak, `<select>` listesi gibi kısıtlanmış bir öğeden gelen tüm giriş, hatta girişi doğrulamak iyi bir uygulamadır. Bu, kullanıcıların bir sayfadaki denetimleri atlayıp form gönderemeyeceği konusunda emin olmanıza yardımcı olur.
2. Sayfa kodunda, `Validation` Yardımcısı yöntemlerini kullanarak her giriş öğesi için ayrı doğrulama denetimleri ekleyin.

    Gerekli alanları denetlemek için `Validation.RequireField(field, [error message])` (tek bir alan için) veya `Validation.RequireFields(field1, field2, ...))` (alanların listesi için) kullanın. Diğer doğrulama türleri için `Validation.Add(field, ValidationType)`kullanın. `ValidationType`için aşağıdaki seçenekleri kullanabilirsiniz:

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. Sayfa gönderildiğinde doğrulamanın `Validation.IsValid`denetleyerek başarılı olup olmadığını denetleyin:

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    Herhangi bir doğrulama hatası varsa, normal sayfa işlemeyi atlayabilirsiniz. Örneğin, sayfanın amacı bir veritabanını güncelleştirmediğinde, tüm doğrulama hataları düzeltilene kadar bunu yapmayın.
4. Doğrulama hataları varsa, `Html.ValidationSummary` veya `Html.ValidationMessage`veya her ikisini de kullanarak sayfa biçimlendirmesinde hata iletilerini görüntüleyin.

Aşağıdaki örnekte, bu adımları gösteren bir sayfa gösterilmektedir.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

Doğrulamanın nasıl çalıştığını görmek için bu sayfayı çalıştırın ve bilinçli olarak hata oluşturun. Örneğin, bir kurs adı girmeyi unuttuğunuzda, bir, girdiğinizde ve geçersiz bir tarih girerseniz, sayfa şöyle görünür:

![İşlenmiş sayfada doğrulama hataları](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>Istemci tarafı doğrulama ekleme

Varsayılan olarak, Kullanıcı girişi, kullanıcılar sayfayı gönderdikten sonra onaylanır — diğer bir deyişle, doğrulama sunucu kodunda gerçekleştirilir. Bu yaklaşımın bir dezavantajı, kullanıcıların sayfayı gönderdikten sonra bir hata yaptığını bilmez. Bir form uzun veya karmaşık ise, yalnızca sayfa gönderildikten sonra hataları bildirmek Kullanıcı için kullanışlı olabilir.

İstemci betiği içinde doğrulama gerçekleştirmek için destek ekleyebilirsiniz. Bu durumda, kullanıcı tarayıcıda çalıştığı için doğrulama gerçekleştirilir. Örneğin, bir değerin tamsayı olması gerektiğini varsayalım. Kullanıcı tamsayı olmayan bir değer girerse, Kullanıcı giriş alanından ayrıldığında hata bildirilir. Kullanıcılar, bunlar için uygun olan anında geri bildirim alırlar. İstemci tabanlı doğrulama, kullanıcının birden çok hatayı düzeltmek için formu kaç kez göndermesi gerektiğini de azaltabilir.

> [!NOTE]
> İstemci tarafı doğrulaması kullanıyor olsanız bile, doğrulama her zaman sunucu kodunda da gerçekleştirilir. Sunucu kodunda doğrulamanın gerçekleştirilmesi, kullanıcıların istemci tabanlı doğrulamayı atlaması durumunda bir güvenlik ölçümüdür.

1. Aşağıdaki JavaScript kitaplıklarını sayfaya kaydedin:  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   Kütüphanelerin ikisi bir Content Delivery Network (CDN) ile yüklenebilir, bu nedenle bilgisayarınızda veya sunucunuzda olması gerekmez. Ancak, *jQuery. Validate. unobtrusive. js*' nin yerel kopyasına sahip olmanız gerekir. Kitaplığı içeren bir WebMatrix şablonuyla ( **Başlatıcı site** gibi) çalışmıyorsanız, **Başlatıcı siteyi**temel alan bir Web sayfaları sitesi oluşturun. Sonra *. js* dosyasını geçerli sitenize kopyalayın.
2. Biçimlendirme ' de, doğruladığınızı her öğe için `Validation.For(field)`bir çağrı ekleyin. Bu yöntem, istemci tarafı doğrulama tarafından kullanılan öznitelikleri yayar. (Gerçek JavaScript kodunu yayma yerine, yöntem `data-val-...`gibi öznitelikleri yayar. Bu öznitelikler, işi yapmak için jQuery kullanan istemci doğrulamasını destekler.)

Aşağıdaki sayfada, daha önce gösterilen örneğe istemci doğrulama özelliklerinin nasıl ekleneceği gösterilmektedir.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

İstemci üzerinde tüm doğrulama denetimleri çalıştırılmadı. Özellikle, veri türü doğrulama (tamsayı, tarih vb.) istemcide çalıştırılmayın. Aşağıdaki denetimler hem istemci hem de sunucu üzerinde çalışır:

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

Bu örnekte, geçerli bir tarih testi istemci kodunda çalışmayacaktır. Ancak, test sunucu kodunda gerçekleştirilir.

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>Doğrulama hatalarını biçimlendirme

Aşağıdaki ayrılmış adlara sahip CSS sınıfları tanımlayarak, doğrulama hatalarının nasıl görüntülendiğini denetleyebilirsiniz:

- `field-validation-error`. Bir hata görüntülenirken `Html.ValidationMessage` yönteminin çıkışını tanımlar.
- `field-validation-valid`. Hata olmadığında `Html.ValidationMessage` yönteminin çıkışını tanımlar.
- `input-validation-error`. Bir hata olduğunda `<input>` öğelerinin nasıl işleneceğini tanımlar. (Örneğin, bir &lt;girişi&gt; öğesinin arka plan rengini, değeri geçersizse farklı bir renge ayarlamak için bu sınıfı kullanabilirsiniz.) Bu CSS sınıfı yalnızca istemci doğrulaması sırasında kullanılır (ASP.NET Web Pages 2).
- `input-validation-valid`. Hata olmadığında `<input>` öğelerinin görünümünü tanımlar.
- `validation-summary-errors`. `Html.ValidationSummary` yönteminin çıkışını tanımlar ve bu, hataların bir listesini görüntüler.
- `validation-summary-valid`. Hata olmadığında `Html.ValidationSummary` yönteminin çıkışını tanımlar.

Aşağıdaki `<style>` bloğu hata koşulları kurallarını gösterir.

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

Bu stil bloğunu, makalenin önceki kısımlarında bulunan örnek sayfalara dahil ederseniz, hata görünümü aşağıdaki çizimde gösterildiği gibi görünür:

![CSS stil sınıflarını kullanan doğrulama hataları](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> ASP.NET Web Pages 2 ' de istemci doğrulaması kullanmıyorsanız, `<input>` öğeleri için CSS sınıfları (`input-validation-error` ve `input-validation-valid` hiçbir etkiye sahip olmaz.

### <a name="static-and-dynamic-error-display"></a>Statik ve dinamik hata görüntüleme

CSS kuralları `validation-summary-errors` ve `validation-summary-valid`gibi çiftler halinde gelir. Bu çiftler her iki koşul için kurallar tanımlamanızı sağlar: bir hata durumu ve "normal" (hata olmayan) koşulu. Hata olmadan biçimlendirmenin her zaman bir hata olmasa bile, her zaman işlenip işlenmeyeceğini anlamak önemlidir. Örneğin, bir sayfada biçimlendirme içinde bir `Html.ValidationSummary` yöntemi varsa, sayfa kaynağı ilk kez istendiği zaman bile aşağıdaki biçimlendirmeyi içerecektir:

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

Diğer bir deyişle, `Html.ValidationSummary` yöntemi her zaman bir `<div>` öğesi ve bir liste oluşturur, bu da hata listesi boş olsa bile. Benzer şekilde, `Html.ValidationMessage` yöntemi her zaman bir alan hatası için bir yer tutucu olarak bir `<span>` öğesi oluşturur, aksi halde bir hata yoktur.

Bazı durumlarda, bir hata iletisi görüntülenirken sayfanın yeniden akıtılmasına neden olabilir ve sayfadaki öğelerin etrafında hareket olmasına neden olabilir. `-valid` biten CSS kuralları, bu sorunu önlemeye yardımcı olabilecek bir düzen tanımlamanızı sağlar. Örneğin, `field-validation-error` tanımlayabilir ve `field-validation-valid` her ikisi de aynı sabit boyuta sahip olabilir. Bu şekilde, alanın görüntüleme alanı statiktir ve bir hata iletisi görüntülenirse sayfa akışını değiştirmez.

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>Doğrudan kullanıcılardan gelmeyen verileri doğrulama

Bazen bir HTML formundan doğrudan gelmeyen bilgileri doğrulamanız gerekebilir. Tipik bir örnek, aşağıdaki örnekte olduğu gibi bir sorgu dizesinde bir değerin geçirildiği bir sayfasıdır:

`http://server/myapp/EditClassInformation?classid=1022`

Bu durumda, sayfaya geçirilen değerin (burada, `classid`değeri için 1022) geçerli olduğundan emin olmak istersiniz. Bu doğrulamayı gerçekleştirmek için `Validation` yardımcısını doğrudan kullanamazsınız. Bununla birlikte, doğrulama sisteminin, doğrulama hatası iletilerini görüntüleme özelliği gibi diğer özelliklerini de kullanabilirsiniz.

> [!NOTE] 
> 
> **Önemli** Form alanı değerleri, sorgu dizesi değerleri ve tanımlama bilgisi değerleri de dahil olmak üzere *herhangi bir* kaynaktan aldığınız değerleri her zaman doğrulayın. Kişilerin bu değerleri değiştirmesi oldukça kolaydır (Belki de kötü amaçlı amaçlar için). Bu nedenle, uygulamanızı korumak için bu değerleri denetlemeniz gerekir.

Aşağıdaki örnek, bir sorgu dizesinde iletilen bir değeri nasıl doğrulayacağınızı gösterir. Kod, değerin boş ve tamsayı olduğunu sınar.

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

İstek bir form gönderimi olmadığında testin gerçekleştirildiğinden (`if(!IsPost)`) dikkat edin. Bu test sayfa istendiğinde ilk kez geçer, ancak istek bir form gönderimi olduğunda bunu yapmayabilir.

Bu hatayı göstermek için `Validation.AddFormError("message")`çağırarak doğrulama hataları listesine hatayı ekleyebilirsiniz. Sayfa `Html.ValidationSummary` yöntemine bir çağrı içeriyorsa, hata bir kullanıcı girişi doğrulama hatası gibi görüntülenir.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web Pages sitelerinde HTML formlarıyla çalışma](https://go.microsoft.com/fwlink/?LinkID=202892)
