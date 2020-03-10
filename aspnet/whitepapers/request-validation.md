---
uid: whitepapers/request-validation
title: İstek doğrulaması-betik saldırılarını önler | Microsoft Docs
author: rick-anderson
description: Bu belgede, varsayılan olarak uygulamanın, kodlanmamış HTML içerik göndermesinin yerine, varsayılan olarak, ASP.NET ' nin istek doğrulama özelliği açıklanmaktadır...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640849"
---
# <a name="request-validation---preventing-script-attacks"></a>İstek Doğrulama - Betik Saldırılarını Önleme

> Bu sayfa, varsayılan olarak uygulamanın sunucuya gönderilen kodlanmamış HTML içeriğini işlemesini engellediği ASP.NET 'in istek doğrulama özelliğini açıklar. Bu istek doğrulama özelliği, uygulama HTML verilerini güvenle işlemek üzere tasarlandıysa devre dışı bırakılabilir.
> 
> ASP.NET 1,1 ve ASP.NET 2,0 için geçerlidir.

Sürüm 1,1 ' den bu yana bir ASP.NET özelliği olan istek doğrulaması, sunucunun kodlanmamış HTML içeren içeriği kabul etmesini engeller. Bu özellik, istemci betik kodu veya HTML 'nin bir sunucuya geri gönderilebildiği, depolandığı ve daha sonra diğer kullanıcılara sunulabildiği bazı betik ekleme saldırılarını önlemeye yardımcı olmak için tasarlanmıştır. Ayrıca, uygun olduğunda tüm giriş verilerini doğrulamanızı ve HTML 'in kodlanmasını kesinlikle öneririz.

Örneğin, bir kullanıcının e-posta adresini isteyen bir Web sayfası oluşturur ve bu e-posta adresini bir veritabanında depolar. Kullanıcı, geçerli bir e-posta adresi yerine bir &lt;komut dosyası&gt;Uyarısı ("betikten Merhaba") girerse&lt;/SCRIPT&gt;, bu veriler sunulursa, içerik düzgün şekilde kodlanmışsa bu betik yürütülebilir. ASP.NET öğesinin istek doğrulama özelliği, bunun oluşmasını engeller.

## <a name="why-this-feature-is-useful"></a>Bu özelliğin neden yararlı olduğu

Birçok site basit betik ekleme saldırılarına açık olduğunu bilmez. Bu saldırıların amacı, HTML 'yi görüntüleyerek siteyi erteleyerek veya kullanıcıyı bir korsanın sitesine yönlendirmek için büyük olasılıkla istemci komut dosyasını yürütmeye yönelik bir sorun olsun, komut dosyası ekleme saldırıları Web geliştiricilerinin ile devam etmelidir.

Betik ekleme saldırıları, ASP.NET, ASP veya diğer web geliştirme teknolojileri kullanıp kullandıklarından bağımsız olarak tüm Web geliştiricilerinin bir kaygıdır.

ASP.NET istek doğrulama özelliği, geliştirici bu içeriğe izin vermeye karar vermediği takdirde, bu saldırıların, kodlanamayan HTML içeriğinin sunucu tarafından işlenmesine izin vermez.

## <a name="what-to-expect-error-page"></a>Bekleneceğiniz: hata sayfası

Aşağıdaki ekran görüntüsünde örnek ASP.NET kodu gösterilmektedir:

![](request-validation/_static/image1.png)

Bu kodun çalıştırılması, metin kutusuna bir metin girmenize izin veren basit bir sayfa ile sonuçlanır, düğmeye tıklayın ve metni etiket denetiminde görüntüleyebilirsiniz:

![](request-validation/_static/image2.png)

Ancak, girilecek ve gönderilecek `<script>alert("hello!")</script>` özel bir durum alırız gibi JavaScript vardı:

![](request-validation/_static/image3.png)

Hata iletisinde ' potansiyel olarak tehlikeli bir Istek. form değeri algılandı ' belirtilir ve açıklamada tam olarak ne olduğu ve davranışın nasıl değiştirileceği hakkında daha fazla ayrıntı sağlar. Örneğin:

İstek doğrulaması potansiyel olarak tehlikeli bir istemci giriş değeri algıladı ve isteğin işlenmesi durduruldu. Bu değer, bir siteler arası betik saldırısı gibi uygulamanızın güvenliğini tehlikeye atabilir. Sayfa yönergesinde veya yapılandırma bölümünde `validateRequest=false` ayarlayarak istek doğrulamayı devre dışı bırakabilirsiniz. Ancak, uygulamanızın bu durumda tüm girdileri açıkça denetlemesi önemle önerilir.

## <a name="disabling-request-validation-on-a-page"></a>Sayfada istek doğrulamayı devre dışı bırakma

Bir sayfada istek doğrulamayı devre dışı bırakmak için, sayfa yönergesinin `validateRequest` özniteliğini `false`olarak ayarlamanız gerekir:

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> İstek doğrulaması devre dışı bırakıldığında, içerik bir sayfaya gönderilebilir; Bu, içeriğin düzgün şekilde kodlandığından veya işlendiğinden emin olmak için sayfa geliştiricisinin sorumluluğundadır.

## <a name="disabling-request-validation-for-your-application"></a>Uygulamanız için istek doğrulamasını devre dışı bırakma

Uygulamanız için istek doğrulamayı devre dışı bırakmak için, uygulamanız için bir Web. config dosyası değiştirmeniz veya oluşturmanız ve `<pages />` bölümünün validateRequest özniteliğini `false`olarak ayarlamanız gerekir:

[!code-xml[Main](request-validation/samples/sample2.xml)]

Sunucunuzdaki tüm uygulamalar için istek doğrulamayı devre dışı bırakmak istiyorsanız, bu değişikliği Machine. config dosyanızda yapabilirsiniz.

> [!CAUTION]
> İstek doğrulaması devre dışı bırakıldığında, uygulamanıza içerik gönderilebilir; içeriğin doğru şekilde kodlandığından veya işlendiğinden emin olmak için uygulama geliştiricisinin sorumluluğundadır.

Aşağıdaki kod, istek doğrulamasını devre dışı bırakmak için değiştirilmiştir:

![](request-validation/_static/image4.png)

Şimdi aşağıdaki JavaScript metin kutusuna girilmişse `<script>alert("hello!")</script>` sonuç şöyle olur:

![](request-validation/_static/image5.png)

Bunun oluşmasını engellemek için, istek doğrulama kapalıyken, içeriği HTML olarak kodlamamız gerekir.

## <a name="how-to-html-encode-content"></a>HTML kodlama içeriği

İstek doğrulamayı devre dışı bırakırsanız, daha sonra kullanılmak üzere depolanacak olan HTML kodlaması içerik için iyi bir uygulamadır. HTML kodlaması, karşılık gelen HTML kodlu gösterimle birlikte otomatik olarak '&lt;' veya '&gt;' (diğer simgelerle birlikte) değiştirir. Örneğin, '&lt;', '&amp;lt; ' ile değiştirilmiştir ve '&gt;', '&amp;gt; ' ile değiştirilmiştir. Tarayıcılar tarayıcıda '&lt;' veya '&gt;' görüntülenmesini sağlamak için bu özel kodları kullanır.

İçerik, `Server.HtmlEncode(string)` API kullanılarak sunucu üzerinde kolayca HTML kodlanabilir. İçerik ayrıca HTML kodu çözülemiyor, diğer bir deyişle `Server.HtmlDecode(string)` yöntemi kullanılarak standart HTML 'ye geri döndürülebilir.

![](request-validation/_static/image6.png)

Sonuç:

![](request-validation/_static/image7.png)
