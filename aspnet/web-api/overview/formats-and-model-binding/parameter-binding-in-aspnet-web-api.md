---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4. x içinde parametre bağlama
author: MikeWasson
description: Web API 'sinin parametreleri nasıl bağlatlarının ve ASP.NET 4. x içinde bağlama işleminin nasıl özelleştirileceğini açıklar.
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 464cb9b45dc0b62c4da38b7cf612934808854d32
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074910"
---
# <a name="parameter-binding-in-aspnet-web-api"></a>ASP.NET Web API 'sinde parametre bağlama

, [Mike te son](https://github.com/MikeWasson)

[!INCLUDE[](~/includes/coreWebAPI.md)]

Bu makale, Web API 'sinin parametreleri nasıl bağlamakta olduğunu ve bağlama işlemini nasıl özelleştirebileceğinizi açıklamaktadır. Web API 'SI bir denetleyicide bir yöntemi çağırdığında,, *bağlama*adlı bir işlem olan parametrelerin değerlerini ayarlaması gerekir.

Varsayılan olarak, Web API parametreleri bağlamak için aşağıdaki kuralları kullanır:

- Parametre "basit" bir tür ise, Web API 'SI URI 'den değeri almaya çalışır. Basit türler, .NET [ilkel türlerini](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **Double**, vb.), artı **TimeSpan**, **DateTime**, **Guid**, **Decimal**, ve **String**ve bir dizeden dönüştürebileceğiniz tür dönüştürücüsü *olan herhangi bir* türü içerir. (Daha sonra tür dönüştürücüler hakkında daha fazla bilgi.)
- Karmaşık türler için Web API 'SI, bir [medya türü biçimlendirici](media-formatters.md)kullanarak ileti gövdesinden değeri okumaya çalışır.

Örneğin, tipik bir Web API denetleyici yöntemi aşağıda verilmiştir:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

*ID* parametresi &quot;basit bir&quot; türüdür, bu nedenle Web API 'SI istek URI 'sinden değeri almaya çalışır. *Öğe* parametresi karmaşık bir türdür, bu nedenle Web API 'si, istek gövdesinden değeri okumak için bir medya türü biçimlendirici kullanır.

URI 'den bir değer almak için Web API 'si yol verilerine ve URI sorgu dizesine bakar. Yönlendirme sistemi URI 'yi ayrıştırdığında ve bir rota ile eşleştiğinde rota verileri doldurulur. Daha fazla bilgi için bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md).

Bu makalenin geri kalanında, model bağlama işlemini nasıl özelleştirebileceğinizi göstereceğiz. Ancak karmaşık türler için, mümkün olduğunda medya türü formatlayıcıları kullanmayı düşünün. HTTP 'nin önemli prensibi, kaynak gösterimini belirtmek için içerik görüşmesi kullanılarak ileti gövdesinde kaynakların gönderilmektir. Medya türü formatlayıcıları tam olarak bu amaçla tasarlanmıştı.

## <a name="using-fromuri"></a>[FromUri] kullanma

Web API 'sini URI 'den karmaşık bir tür okuyacak şekilde zorlamak için, parametresine **[Fromuri]** özniteliğini ekleyin. Aşağıdaki örnek, URI 'den `GeoPoint` alan bir denetleyici yöntemiyle birlikte `GeoPoint` türünü tanımlar.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

İstemci, enlem ve boylam değerlerini sorgu dizesine yerleştirebilir ve Web API 'SI bunları bir `GeoPoint`oluşturmak için kullanır. Örneğin:

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a>[FromBody] kullanma

Web API 'sini istek gövdesinden basit bir tür okuyacak şekilde zorlamak için, **[Frombody]** özniteliğini parametresine ekleyin:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

Bu örnekte, Web API 'SI, istek gövdesinden *adı* değerini okumak için bir medya türü biçimlendirici kullanacaktır. Örnek bir istemci isteği aşağıda verilmiştir.

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

Bir parametre [FromBody] olduğunda, Web API 'SI bir biçimlendirici seçmek için Content-Type üst bilgisini kullanır. Bu örnekte, içerik türü &quot;Application/JSON&quot; ve istek gövdesi ham JSON dizesidir (JSON nesnesi değil).

İleti gövdesinden en fazla bir parametrenin okumasına izin verilir. Bu nedenle, bu çalışmaz:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

Bu kuralın nedeni, istek gövdesinin yalnızca bir kez okunabilecek, arabelleğe alınmamış bir akışa depolanabileceği bir akışdır.

## <a name="type-converters"></a>Tür dönüştürücüler

Bir **TypeConverter** 'ı oluşturarak ve bir dize dönüştürmesi sağlayarak Web API 'sinin bir sınıfı basit bir tür olarak (Web API 'sini URI 'den bağlamaya çalışacak şekilde) görmesini sağlayabilirsiniz.

Aşağıdaki kod, bir coğrafi noktayı temsil eden bir `GeoPoint` sınıfını ve dizelerden `GeoPoint` örneklerine dönüştüren bir **TypeConverter** 'ı gösterir. `GeoPoint` sınıfı, tür dönüştürücüsünü belirtmek için bir **[TypeConverter]** özniteliğiyle donatılmalıdır. (Bu örnek, Mike Stall 'ın Web günlüğü gönderisini [MVC/WebAPI içindeki eylem imzalarındaki özel nesnelere bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

Şimdi Web API 'SI `GeoPoint` basit bir tür olarak değerlendirir, yani `GeoPoint` parametrelerini URI 'den bağlamaya çalışacaktır. Parametreye **[Fromuri]** eklemeniz gerekmez.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

İstemci, yöntemi aşağıdaki gibi bir URI ile çağırabilir:

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a>Model ciltleri

Tür dönüştürücüden daha esnek bir seçenek, özel model Bağlayıcısı oluşturmaktır. Model Ciltçi ile HTTP isteği, eylem açıklaması ve rota verilerinden ham değerler gibi şeylere erişebilirsiniz.

Bir model Bağlayıcısı oluşturmak için **ımodelciltçi** arabirimini uygulayın. Bu arabirim tek bir yöntemi tanımlar, **BindModel**:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

`GeoPoint` nesneler için bir model Bağlayıcısı aşağıda verilmiştir.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

Model Ciltçi, bir *değer sağlayıcısından*ham giriş değerleri alır. Bu tasarım iki ayrı işlevi ayırır:

- Değer sağlayıcısı, HTTP isteğini alır ve anahtar-değer çiftlerinin bir sözlüğünü doldurur.
- Model Ciltçi, modeli doldurmak için bu sözlüğü kullanır.

Web API 'sindeki varsayılan değer sağlayıcısı, rota verilerinden ve sorgu dizesinden değerleri alır. Örneğin, URI `http://localhost/api/values/1?location=48,-122`ise, değer sağlayıcı aşağıdaki anahtar-değer çiftlerini oluşturur:

- kimlik = &quot;1&quot;
- Konum = &quot;48.122&quot;

(&quot;API/{Controller}/{ID}&quot;varsayılan yol şablonunu kabul ediyorum.)

Bağlanacak parametrenin adı, **ModelBindingContext. ModelName** özelliğinde depolanır. Model Ciltçi, sözlükte bu değere sahip bir anahtar arar. Değer varsa ve bir `GeoPoint`dönüştürülebiliyorsanız model Ciltçi, bağlantılı değeri **ModelBindingContext. model** özelliğine atar.

Model cildin basit bir tür dönüştürmesi ile sınırlı olmadığına dikkat edin. Bu örnekte, model cildi ilk olarak bilinen konumların bir tablosuna bakar ve bu başarısız olursa, tür dönüştürme kullanır.

**Model cildi ayarlama**

Model cildi ayarlamak için çeşitli yollar vardır. İlk olarak, parametresine bir **[Modelciltçi]** özniteliği ekleyebilirsiniz.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

Ayrıca, türüne bir **[Modelciltçi]** özniteliği ekleyebilirsiniz. Web API 'SI, bu türün tüm parametreleri için belirtilen model cildi kullanır.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

Son olarak, bir model Ciltçi sağlayıcısını **HttpConfiguration**'a ekleyebilirsiniz. Model Ciltçi sağlayıcısı, model cildi oluşturan bir fabrika sınıfıdır. [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) sınıfından türeterek bir sağlayıcı oluşturabilirsiniz. Ancak, model Ciltçi tek bir tür işlediğinde, bu amaçla tasarlanan yerleşik **SimpleModelBinderProvider**kullanımı daha kolay olur. Aşağıdaki kod bunun nasıl yapılacağını gösterir.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

Model bağlama sağlayıcısıyla, Web API 'sini bir medya türü biçimlendirici değil, model cildi kullanması gerektiğini söylemek için, **[modelciltçi]** özniteliğini parametreye eklemeniz gerekir. Ancak şimdi özniteliğinde model cildin türünü belirtmeniz gerekmez:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a>Değer sağlayıcıları

Model cildin bir değer sağlayıcısından değerler aldığından bahsetdim. Özel bir değer sağlayıcısı yazmak için **IValueProvider** arabirimini uygulayın. İşte, istekteki tanımlama bilgilerinden değer çeken bir örnek:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

Ayrıca, **ValueProviderFactory** sınıfından türeterek bir değer sağlayıcısı fabrikası oluşturmanız gerekir.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

Değer sağlayıcısı fabrikasını **HttpConfiguration** öğesine aşağıdaki şekilde ekleyin.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

Web API 'SI, tüm değer sağlayıcılarını oluşturur, bu nedenle model Ciltçi **ValueProvider. GetValue**' yi çağırdığında, model cildi onu üretebilecek ilk değer sağlayıcısından değeri alır.

Alternatif olarak, değer sağlayıcı fabrikasını parametre düzeyinde, **ValueProvider** özniteliğini kullanarak aşağıdaki gibi ayarlayabilirsiniz:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

Bu, Web API 'sinin belirtilen değer sağlayıcı fabrikası ile model bağlamayı kullanmasını söyler ve diğer kayıtlı değer sağlayıcılarının hiçbirini kullanmaz.

## <a name="httpparameterbinding"></a>HttpParameterBinding

Model ciltleri, daha genel bir mekanizmanın belirli bir örneğidir. **[Modelciltçi]** özniteliğine bakarsanız, onun soyut **ParameterBindingAttribute** sınıfından türetildiğinden emin olursunuz. Bu sınıf, bir **Httpparameterbinding** nesnesi döndüren **GetBinding**tek bir yöntemini tanımlar:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

Bir **Httpparameterbinding** , bir parametreyi bir değere bağlamaktan sorumludur. **[Modelciltçi]** söz konusu olduğunda, öznitelik gerçek bağlamayı gerçekleştirmek Için **ımodelciltçi** kullanan bir **httpparameterbinding** uygulaması döndürür. Ayrıca kendi **Httpparameterbinding**'nizi de uygulayabilirsiniz.

Örneğin, istekteki `if-match` ve `if-none-match` üst bilgilerden ETags almak istediğinizi varsayalım. ETags temsil eden bir sınıf tanımlayarak başlayacağız.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

Ayrıca, `if-match` üst bilgisinden veya `if-none-match` üst bilgisinden ETag 'in mi alınacağını göstermek için bir sabit listesi tanımlayacağız.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

Burada, istenen üst bilgiden ETag 'i alan ve ETag türü bir parametreye bağlayan bir **Httpparameterbinding** yer alır:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

**Executebindingasync** yöntemi bağlamayı yapar. Bu yöntemde, bir bağlama parametre değerini **Httpactioncontext**Içindeki **actionargument** sözlüğüne ekleyin.

> [!NOTE]
> **Executebindingasync** yönteminiz istek iletisinin gövdesini okuyorsa, true döndürecek şekilde **willreadbody** özelliğini geçersiz kılın. İstek gövdesi, yalnızca bir kez okunabilecek, arabelleğe alınmamış bir akış olabilir, bu nedenle Web API 'SI en çok bir bağlamanın ileti gövdesini okuyabilecek bir kuralı zorlar.

Özel bir **Httpparameterbinding**uygulamak Için **ParameterBindingAttribute**öğesinden türetilen bir öznitelik tanımlayabilirsiniz. `ETagParameterBinding`için biri `if-match` üst bilgileri ve bir `if-none-match` üst bilgisi için olmak üzere iki öznitelik tanımlayacağız. Her ikisi de soyut bir temel sınıftan türetir.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

`[IfNoneMatch]` özniteliğini kullanan bir Controller yöntemi aşağıda verilmiştir.

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

**ParameterBindingAttribute**'un yanı sıra özel bir **httpparameterbinding**eklemek için başka bir kanca vardır. **HttpConfiguration** nesnesinde **parameterbindingrules** özelliği, (**HttpParameterDescriptor** -&gt; **httpparameterbinding**) türündeki anonim işlevlerin bir koleksiyonudur. Örneğin, GET yöntemindeki herhangi bir ETag parametresinin `if-none-match``ETagParameterBinding` kullandığı bir kural ekleyebilirsiniz:

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

İşlev, bağlamanın geçerli olmadığı parametreler için `null` döndürmelidir.

## <a name="iactionvaluebinder"></a>Iactionvalueciltçi

Tüm parametre bağlama işlemi takılabilir bir hizmet olan **ıactionvalueciltçi**tarafından denetlenir. **Iactionvalueciltçi** 'nin varsayılan uygulaması aşağıdakileri yapar:

1. Parametresinde bir **ParameterBindingAttribute** bulun. Buna **[Frombody]** , **[fromuri]** ve **[modelciltçi]** ya da özel öznitelikler dahildir.
2. Aksi halde, null olmayan bir **Httpparameterbinding**döndüren bir Işlev Için **HttpConfiguration. parameterbindingrules** bölümüne bakın.
3. Aksi takdirde, daha önce açıklananlardan varsayılan kuralları kullanın. 

    - Parametre türü "basittir" ise veya tür dönüştürücüsüyle, URI 'den bağlayın. Bu, **[Fromuri]** özniteliğini parametreye koymaya eşdeğerdir.
    - Aksi takdirde, ileti gövdesinden parametresini okumayı deneyin. Bu parametre üzerine **[Frombody]** koymaya eşdeğerdir.

İsterseniz, tüm **ıactionvalueciltçi** hizmetini özel bir uygulamayla değiştirebilirsiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

[Özel parametre bağlama örneği](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

Mike Stall, Web API parametresi bağlaması hakkında iyi bir blog gönderisi serisi yazdı:

- [Web API parametre bağlamayı nasıl yapar](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [Web API 'SI için MVC stil parametresi bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [MVC/web API 'de eylem imzalarında özel nesnelere bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [Web API 'de özel değer sağlayıcısı oluşturma](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [Altyapı altında Web API parametresi bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
