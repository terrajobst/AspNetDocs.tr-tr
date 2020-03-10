---
uid: web-pages/overview/api-reference/asp-net-web-pages-api-reference
title: ASP.NET Web Pages (Razor) API 'SI hızlı başvurusu | Microsoft Docs
author: Rick-Anderson
description: Bu sayfa, en yaygın kullanılan nesneler, Özellikler ve Razor söz dizimi ile ASP.NET Web sayfalarını programlama yöntemlerine ilişkin kısa örnekler içeren bir liste içerir.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 4001cb9b-3bfd-4ace-8a89-1561d8421e2c
msc.legacyurl: /web-pages/overview/api-reference/asp-net-web-pages-api-reference
msc.type: authoredcontent
ms.openlocfilehash: e010307fc0576e8b003fbfe665cae77618d9c9a5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574335"
---
# <a name="aspnet-web-pages-razor-api-quick-reference"></a>ASP.NET Web Pages (Razor) API 'SI hızlı başvurusu

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu sayfa, en yaygın kullanılan nesneler, Özellikler ve Razor söz dizimi ile ASP.NET Web sayfalarını programlama yöntemlerine ilişkin kısa örnekler içeren bir liste içerir.
> 
> "(V2)" ile işaretlenen açıklamalar ASP.NET Web Pages sürüm 2 ' de tanıtılmıştır.
> 
> API başvuru belgeleri için MSDN 'deki [ASP.NET Web sayfaları başvuru belgelerine](https://go.microsoft.com/fwlink/?LinkId=208659) bakın.
> 
> ## <a name="software-versions"></a>Yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici Ayrıca ASP.NET Web Pages 2 ve ASP.NET Web Pages 1,0 (v2 olarak işaretlenmiş Özellikler hariç) ile de kullanılabilir.

Bu sayfa, aşağıdakiler için başvuru bilgileri içerir:

- [Sınıflar](#Classes)
- [Veri](#Data)
- [Yardımcı](#Helpers)
- [Doğrulama](#Validation)

<a id="Classes"></a>
## <a name="classes"></a>Sınıflar

### `AppState[key], AppState[index],App`

Uygulamadaki herhangi bir sayfa tarafından paylaşılabilecek verileri içerir. Aşağıdaki örnekteki gibi, aynı verilere erişmek için dinamik `App` özelliğini kullanabilirsiniz:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample1.html)]

### `AsBool(), AsBool(true|false)`

Bir dize değerini bir Boole değerine dönüştürür (true/false). Dize doğru/yanlış temsil ediyorsa, false veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample2.cs)]

### `AsDateTime(), AsDateTime(value)`

Bir dize değerini Tarih/saate dönüştürür. Dize bir tarih/saat temsil etmediği zaman `DateTime.MinValue` veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample3.cs)]

### `AsDecimal(), AsDecimal(value)`

Bir dize değerini ondalık bir değere dönüştürür. Dize bir ondalık değeri temsil ediyorsa 0,0 veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample4.cs)]

### `AsFloat(), AsFloat(value)`

Bir dize değerini bir float öğesine dönüştürür. Dize bir ondalık değeri temsil ediyorsa 0,0 veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample5.cs)]

### `AsInt(), AsInt(value)`

Bir dize değerini bir tamsayıya dönüştürür. Dize bir tamsayıyı temsil ediyorsa 0 veya belirtilen değeri döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample6.cs)]

### `Href(path [, param1 [, param2]])`

İsteğe bağlı ek yol parçalarıyla, yerel bir dosya yolundan tarayıcı ile uyumlu bir URL oluşturur.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample7.cshtml)]

### `Html.Raw(value)`

*Değeri* HTML kodlu çıktı olarak IŞLEMEK yerine HTML biçimlendirmesi olarak işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample8.cshtml)]

### `IsBool(), IsDateTime(), IsDecimal(), IsFloat(), IsInt()`

Değer bir dizeden belirtilen türe dönüştürülebiliyorsa, true döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample9.cs)]

### `IsEmpty()`

Nesnenin veya değişkenin değeri yoksa true döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample10.cs)]

### `IsPost`

İstek bir GÖNDERISE, true döndürür. (Başlangıç istekleri genellikle bir GET olur.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample11.cs)]

### `Layout`

Bu sayfaya uygulanacak bir düzen sayfasının yolunu belirtir.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample12.html)]

### `PageData[key], PageData[index],Page`

Geçerli istekteki sayfa, düzen sayfaları ve kısmi sayfalar arasında paylaşılan verileri içerir. Aşağıdaki örnekteki gibi, aynı verilere erişmek için dinamik `Page` özelliğini kullanabilirsiniz:

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample13.html)]

### `RenderBody()`

(Düzen sayfaları) Herhangi bir adlandırılmış bölümde olmayan bir içerik sayfasının içeriğini işler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample14.cs)]

### `RenderPage(path, values)`  
`RenderPage(path[,param1 [, param2]])`

Belirtilen yolu ve isteğe bağlı ek verileri kullanarak bir içerik sayfası oluşturur. `PageData` konuma (örnek 1) veya anahtara göre ek parametrelerin değerlerini alabilirsiniz (örnek 2).

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample15.js)]

### `RenderSection(sectionName [, required = true|false])`

(Düzen sayfaları) Adında bir içerik bölümü oluşturur. Bir bölümü isteğe bağlı *yapmak için false olarak ayarlayın.*

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample16.js)]

### `Request.Cookies[key]`

HTTP tanımlama bilgisinin değerini alır veya ayarlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample17.cs)]

### `Request.Files[key]`

Geçerli istekte karşıya yüklenen dosyaları alır.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample18.js)]

### `Request.Form[key]`

Bir formda (dizeler olarak) gönderilen verileri alır. `Request[key]` hem `Request.Form` hem de `Request.QueryString` koleksiyonlarını denetler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample19.cs)]

### `Request.QueryString[key]`

URL sorgu dizesinde belirtilen verileri alır. `Request[key]` hem `Request.Form` hem de `Request.QueryString` koleksiyonlarını denetler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample20.cs)]

### `Request.Unvalidated(key)`  
`Request.Unvalidated().QueryString|Form|Cookies|Headers[key]`

Form öğesi, sorgu dizesi değeri, tanımlama bilgisi veya üst bilgi değeri için istek doğrulamayı seçmeli olarak devre dışı bırakır. İstek doğrulaması varsayılan olarak etkindir ve kullanıcıların biçimlendirme veya diğer potansiyel tehlikeli içerik almasını engeller.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample21.cs)]

### `Response.AddHeader(name, value)`

Yanıta bir HTTP sunucusu üst bilgisi ekler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample22.cs)]

### `Response.OutputCache(seconds [, sliding] [, varyByParams])`

Sayfa çıkışını belirli bir süre için önbelleğe alır. İsteğe bağlı olarak, her sayfa erişiminde zaman aşımını sıfırlamak için *kayan* , sayfa isteğindeki her farklı sorgu dizesi için sayfanın farklı sürümlerini önbelleğe almak için *varyByParams* ayarlayın.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample23.js)]

### `Response.Redirect(path)`

Tarayıcı isteğini yeni bir konuma yönlendirir.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample24.js)]

### `Response.SetStatus(httpStatusCode)`

Tarayıcıya gönderilen HTTP durum kodunu ayarlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample25.cs)]

### `Response.WriteBinary(data [, mimetype])`

*Verilerin* içeriğini isteğe bağlı bir MIME türü ile yanıta yazar.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample26.js)]

### `Response.WriteFile(file)`

Bir dosyanın içeriğini yanıta yazar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample27.cs)]

### `@section(sectionName) {content }`

(Düzen sayfaları) Bir ada sahip bir içerik bölümü tanımlar.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample28.cshtml)]

### `Server.HtmlDecode(htmlText)`

HTML kodlamalı bir dizenin kodunu çözer.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample29.cs)]

### `Server.HtmlEncode(text)`

HTML biçimlendirmesinde işleme için bir dizeyi kodlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample30.cs)]

### `Server.MapPath(virtualPath)`

Belirtilen sanal yol için sunucu fiziksel yolunu döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample31.cs)]

### `Server.UrlDecode(urlText)`

URL 'deki metnin kodunu çözer.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample32.cs)]

### `Server.UrlEncode(text)`

Bir URL 'ye konacak metni kodlar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample33.cs)]

### `Session[key]`

Kullanıcı Tarayıcıyı kapatana kadar var olan bir değeri alır veya ayarlar.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample34.css)]

### `ToString()`

Nesnenin değerinin dize gösterimini görüntüler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample35.html)]

### `UrlData[index]`

URL 'den ek verileri alır (örneğin, */MyPage/ExtraData*).

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample36.cs)]

### `WebSecurity.ChangePassword(userName,currentPassword,newPassword)`

Belirtilen kullanıcının parolasını değiştirir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample37.cs)]

### `WebSecurity.ConfirmAccount(accountConfirmationToken)`

Hesap onaylama belirtecini kullanarak bir hesabı onaylar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample38.cs)]

### `WebSecurity.CreateAccount(userName, password`  
 `[, requireConfirmationToken = true|false])`

Belirtilen Kullanıcı adı ve parolayla yeni bir kullanıcı hesabı oluşturur. Bir onay belirteci gerektirmek için, RequireConfirmationToken için doğru geçirin *.*

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample39.cs)]

### `WebSecurity.CurrentUserId`

Şu anda oturum açmış olan kullanıcının tamsayı tanımlayıcısını alır.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample40.cs)]

### `WebSecurity.CurrentUserName`

Şu anda oturum açmış olan kullanıcının adını alır.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample41.cs)]

### `WebSecurity.GeneratePasswordResetToken(username`  
 `[, tokenExpirationInMinutesFromNow])`

Kullanıcının parolayı sıfırlayabilmesi için kullanıcıya e-posta ile gönderilebilecek bir parola sıfırlama belirteci üretir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample42.cs)]

### `WebSecurity.GetUserId(userName)`

Kullanıcı adından kullanıcı KIMLIĞINI döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample43.cs)]

### `WebSecurity.IsAuthenticated`

Geçerli Kullanıcı oturum açtıysa, doğru döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample44.cs)]

### `WebSecurity.IsConfirmed(userName)`

Kullanıcı onaylanmışsa (örneğin, bir onay e-postası aracılığıyla) true döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample45.cs)]

### `WebSecurity.IsCurrentUser(userName)`

Geçerli kullanıcının adı belirtilen kullanıcı adıyla eşleşiyorsa, doğru değerini döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample46.cs)]

### `WebSecurity.Login(userName,password[, persistCookie])`

Tanımlama bilgisinde bir kimlik doğrulama belirteci ayarlayarak kullanıcıyı ' de günlüğe kaydeder.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample47.cs)]

### `WebSecurity.Logout()`

Kimlik doğrulama belirteci tanımlama bilgisini kaldırarak kullanıcıyı günlüğe kaydeder.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample48.css)]

### `WebSecurity.RequireAuthenticatedUser()`

Kullanıcının kimliği doğrulanmazsa, HTTP durumunu 401 (Yetkisiz) olarak ayarlar.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample49.css)]

### `WebSecurity.RequireRoles(roles)`

Geçerli Kullanıcı belirtilen rollerden birinin üyesi değilse, HTTP durumunu 401 (yetkisiz) olarak ayarlar.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample50.html)]

### `WebSecurity.RequireUser(userId)`  
`WebSecurity.RequireUser(userName)`

Geçerli Kullanıcı Kullanıcı *adı*tarafından belirtilen kullanıcı DEĞILSE, HTTP durumunu 401 (yetkisiz) olarak ayarlar.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample51.css)]

### `WebSecurity.ResetPassword(passwordResetToken,newPassword)`

Parola sıfırlama belirteci geçerliyse, kullanıcının parolasını yeni parola olarak değiştirir.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample52.css)]

<a id="Data"></a>
## <a name="data"></a>Veri

### `Database.Execute(SQLstatement [,parameters]`

INSERT, DELETE veya UPDATE gibi bir *SQLstatement* (isteğe bağlı parametrelerle) çalıştırır ve etkilenen kayıtların sayısını döndürür.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample53.sql)]

### `Database.GetLastInsertId()`

En son eklenen satırdaki kimlik sütununu döndürür.

[!code-sql[Main](asp-net-web-pages-api-reference/samples/sample54.sql)]

### `Database.Open(filename)`  
`Database.Open(connectionStringName)`

Belirtilen veritabanı dosyasını veya *Web. config* dosyasından adlandırılmış bir bağlantı dizesi kullanılarak belirtilen veritabanını açar.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample55.cs)]

### `Database.OpenConnectionString(connectionString)`

Bağlantı dizesini kullanarak bir veritabanı açar. (Bu, bir bağlantı dizesi adı kullanan `Database.Open`karşıttır.)

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample56.cs)]

### `Database.Query(SQLstatement[,parameters])`

*SQLstatement* (isteğe bağlı olarak parametreleri geçirme) kullanarak veritabanını sorgular ve sonuçları bir koleksiyon olarak döndürür.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample57.html)]

### `Database.QuerySingle(SQLstatement [, parameters])`

*SQLstatement* (isteğe bağlı parametrelerle) yürütür ve tek bir kayıt döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample58.cs)]

### `Database.QueryValue(SQLstatement [, parameters])`

*SQLstatement* (isteğe bağlı parametrelerle) yürütür ve tek bir değer döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample59.cs)]

<a id="Helpers"></a>
## <a name="helpers"></a>Yardımcı

### `Analytics.GetGoogleHtml(webPropertyId)`

Belirtilen KIMLIK için Google Analytics JavaScript kodunu işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample60.js)]

### `Analytics.GetStatCounterHtml(project,security)`

Belirtilen proje için StatCounter Analytics JavaScript kodunu işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample61.css)]

### `Analytics.GetYahooHtml(account)`

Belirtilen hesap için Yahoo Analytics JavaScript kodunu işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample62.js)]

### `Bing.SearchBox([boxWidth])`

Bir aramayı Bing 'e geçirir. Aranacak siteyi ve arama kutusu için bir başlığı belirtmek üzere `Bing.SiteUrl` ve `Bing.SiteTitle` özelliklerini ayarlayabilirsiniz. Normalde bu özellikleri *\_AppStart* sayfasında ayarlarsınız.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample63.html)]

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample64.cshtml)]

### `Chart(width,height [, template] [, templatePath])`

Bir grafiği başlatır.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample65.cshtml)]

### `Chart.AddLegend([title] [, name])`

Grafiğe bir açıklama ekler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample66.cshtml)]

### `Chart.AddSeries([name] [, chartType] [, chartArea]`  
 `[, axisLabel] [, legend] [, markerStep] [, xValue]`  
 `[, xField] [, yValues] [, yFields] [, options])`

Grafiğe bir dizi değer ekler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample67.cshtml)]

### `Crypto.Hash(string [, algorithm])`  
`Crypto.Hash(bytes [, algorithm])`

Belirtilen veriler için bir karma döndürür. Varsayılan algoritma `sha256`.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample68.html)]

### `Facebook.LikeButton(href [, buttonLayout] [, showFaces] [, width] [, height]`   
 `[, action] [, font] [, colorScheme] [, refLabel])`

Facebook kullanıcılarının sayfalarla bağlantı yapmasını sağlar.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample69.js)]

### `FileUpload.GetHtml([initialNumberOfFiles] [, allowMoreFilesToBeAdded]`  
 `[, includeFormTag] [, addText] [, uploadText])`

Dosyaları karşıya yüklemek için Kullanıcı arabirimini işler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample70.html)]

### `GamerCard.GetHtml(gamerTag)`

Belirtilen Xbox oyuncu etiketini işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample71.js)]

### `Gravatar.GetHtml(email [, imageSize] [, defaultImage] [, rating]`  
 `[, imageExtension] [, attributes])`

Belirtilen e-posta adresi için Gravatar görüntüsünü işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample72.css)]

### `Json.Encode(object)`

Veri nesnesini JavaScript Nesne Gösterimi (JSON) biçimindeki bir dizeye dönüştürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample73.cs)]

### `Json.Decode(string)`

JSON kodlu bir giriş dizesini, yinelemek veya veritabanına eklemek için bir veri nesnesine dönüştürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample74.cs)]

### `LinkShare.GetHtml(pageTitle[, pageLinkBack] [, twitterUserName]`  
 `[, additionalTweetText] [, linkSites])`

Belirtilen başlığı ve isteğe bağlı URL 'YI kullanarak sosyal ağ bağlantılarını işler.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample75.xml)]

### `ModelStateDictionary.AddError(key, errorMessage)`

Bir hata iletisini form alanıyla ilişkilendirir. Bu üyeye erişmek için `ModelState` yardımcısını kullanın.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample76.cs)]

### `ModelStateDictionary.AddFormError(errorMessage)`

Bir hata iletisini bir formla ilişkilendirir. Bu üyeye erişmek için `ModelState` yardımcısını kullanın.

[!code-powershell[Main](asp-net-web-pages-api-reference/samples/sample77.ps1)]

### `ModelStateDictionary.IsValid`

Doğrulama hatası yoksa true döndürür. Bu üyeye erişmek için `ModelState` yardımcısını kullanın.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample78.cs)]

### `ObjectInfo.Print(value [, depth] [, enumerationLength])`

Bir nesnenin özelliklerini ve değerlerini ve tüm alt nesneleri işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample79.css)]

### `Recaptcha.GetHtml([, publicKey] [, theme] [, language] [, tabIndex])`

ReCAPTCHA doğrulama testini işler.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample80.css)]

### `ReCaptcha.PublicKey`  
 `ReCaptcha.PrivateKey`

ReCAPTCHA hizmeti için ortak ve özel anahtarları ayarlar. Normalde bu özellikleri *\_AppStart* sayfasında ayarlarsınız.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample81.css)]

### `ReCaptcha.Validate([, privateKey])`

ReCAPTCHA testinin sonucunu döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample82.cs)]

### `ServerInfo.GetHtml()`

ASP.NET Web sayfaları hakkında durum bilgilerini işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample83.cshtml)]

### `Twitter.Profile(twitterUserName)`

Belirtilen kullanıcı için Twitter akışı işler.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample84.js)]

### `Twitter.Search(searchQuery)`

Belirtilen arama metni için bir Twitter akışı işler.

[!code-xml[Main](asp-net-web-pages-api-reference/samples/sample85.xml)]

### `Video.Flash(filename [, width, height])`

Belirtilen dosya için isteğe bağlı genişlik ve yükseklik içeren bir Flash video oynatıcı oluşturur.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample86.cshtml)]

### `Video.MediaPlayer(filename [, width, height])`

Belirtilen dosya için bir Windows Media Player 'ı isteğe bağlı genişlik ve yükseklik ile işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample87.cshtml)]

### `Video.Silverlight(filename, width, height)`

Belirtilen *. xap* dosyası için gerekli genişlik ve yüksekliğe sahip bir Silverlight oynatıcı oluşturur.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample88.cshtml)]

### `WebCache.Get(key)`

*Anahtar*tarafından belirtilen nesneyi veya nesne bulunamazsa null değerini döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample89.cs)]

### `WebCache.Remove(key)`

*Anahtar* tarafından belirtilen nesneyi önbellekten kaldırır.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample90.cs)]

### `WebCache.Set(key, value [, minutesToCache] [, slidingExpiration])`

*Değeri* , *anahtar*tarafından belirtilen ad altında önbelleğe koyar.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample91.html)]

### `WebGrid(data)`

Bir sorgudaki verileri kullanarak yeni bir `WebGrid` nesnesi oluşturur.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample92.cs)]

### `WebGrid.GetHtml()`

HTML tablosunda verileri göstermek için biçimlendirmeyi işler.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample93.html)]

### `WebGrid.Pager()`

`WebGrid` nesnesi için bir sayfalayıcı oluşturur.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample94.html)]

### `WebImage(path)`

Belirtilen yoldan bir görüntü yükler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample95.cs)]

### `WebImage.AddImagesWatermark(image)`

Belirtilen görüntüyü bir filigran olarak ekler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample96.cs)]

### `WebImage.AddTextWatermark(text)`

Görüntüye belirtilen metni ekler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample97.cs)]

### `WebImage.FlipHorizontal()`  
`WebImage.FlipVertical()`

Görüntüyü yatay veya dikey olarak çevirir.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample98.css)]

### `WebImage.GetImageFromRequest()`

Karşıya dosya yükleme sırasında bir görüntü gönderildiğinde bir görüntü yükler.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample99.cs)]

### `WebImage.Resize(width,height)`

Görüntüyü yeniden boyutlandırır.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample100.css)]

### `WebImage.RotateLeft()`  
`WebImage.RotateRight()`

Görüntüyü sola veya sağa döndürür.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample101.css)]

### `WebImage.Save(path [, imageFormat])`

Görüntüyü belirtilen yola kaydeder.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample102.js)]

### `WebMail.Password`

SMTP sunucusu için parolayı ayarlar. Normalde bu özelliği *\_AppStart* sayfasında ayarlarsınız.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample103.cs)]

### `WebMail.Send(to, subject, body [, from] [, cc] [, filesToAttach] [, isBodyHtml]`  
 `[, additionalHeaders])`

Bir e-posta iletisi gönderir.

[!code-css[Main](asp-net-web-pages-api-reference/samples/sample104.css)]

### `WebMail.SmtpServer`

SMTP sunucusu adını ayarlar. Normalde bu özelliği *\_AppStart* sayfasında ayarlarsınız.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample105.html)]

### `WebMail.UserName`

SMTP sunucusu için Kullanıcı adını ayarlar. Normalde bu özelliği *\_AppStart* sayfasında ayarlamanız gerekir.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample106.html)]

<a id="Validation"></a>
## <a name="validation"></a>Doğrulama

### `Html.ValidationMessage(field)`

v2 Belirtilen alan için bir doğrulama hata iletisi işler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample107.cshtml)]

### `Html.ValidationSummary([message])`

v2 Tüm doğrulama hatalarının listesini görüntüler.

[!code-cshtml[Main](asp-net-web-pages-api-reference/samples/sample108.cshtml)]

### `Validation.Add(field, validationType)`

v2 Belirtilen doğrulama türü için bir kullanıcı girişi öğesi kaydeder.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample109.js)]

### `Validation.ClassFor(field)`

v2 Doğrulama hata iletilerini biçimlendirmek için, istemci tarafı doğrulama için CSS sınıfı özniteliklerini dinamik olarak işler. (Uygun istemci komut dosyası kitaplıklarına başvurmanız ve CSS sınıfları tanımlamanız gerekir.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample110.html)]

### `Validation.For(field)`

v2 Kullanıcı girişi alanı için istemci tarafı doğrulamayı etkinleştirilir. (Uygun istemci komut dosyası kitaplıklarına başvurmanız gerekir.)

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample111.html)]

### `Validation.IsValid()`

v2 Doğrulama için kayıt defteri \ kırmızı olan tüm Kullanıcı giriş öğeleri geçerli değerler içeriyorsa true döndürür.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample112.cs)]

### `Validation.RequireField(field[, errorMessage])`

v2 Kullanıcıların, Kullanıcı girişi öğesi için bir değer sağlamaları gerektiğini belirtir.

[!code-csharp[Main](asp-net-web-pages-api-reference/samples/sample113.cs)]

### `Validation.RequireFields(field1[, field12, field3, ...])`

v2 Kullanıcıların, Kullanıcı giriş öğelerinin her biri için değer sağlaması gerektiğini belirtir. Bu yöntem özel bir hata iletisi belirtmenize izin vermez.

[!code-html[Main](asp-net-web-pages-api-reference/samples/sample114.html)]

### `Validator.DateTime ([error message])`  
`Validator.Decimal([error message])`  
`Validator.EqualsTo(otherField,[error message])`  
`Validator.Float([error message])`  
`Validator.Integer([error message])`  
`Validator.Range(min,max [, error message])`  
`Validator.RegEx(pattern[, error message])`  
`Validator.Required([error message])`  
`Validator.StringLength(length)`  
`Validator.Url([error message])`

v2 `Validation.Add` yöntemini kullandığınızda bir doğrulama testi belirtir.

[!code-javascript[Main](asp-net-web-pages-api-reference/samples/sample115.js)]
