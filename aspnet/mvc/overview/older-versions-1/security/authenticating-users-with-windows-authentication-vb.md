---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: Windows kimlik doğrulaması ile kullanıcıların kimliğini doğrulama (VB) | Microsoft Docs
author: microsoft
description: Windows kimlik doğrulamasını bir MVC uygulaması bağlamında nasıl kullanacağınızı öğrenin. Uygulamanızın Web Co 'inizdeki Windows kimlik doğrulamasını etkinleştirmeyi öğrenirsiniz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: aa64b1f9ef6461a81611ca066310dca2d545baa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624119"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>Windows Kimlik Doğrulaması ile Kullanıcıların Kimliğini Doğrulama (VB)

[Microsoft](https://github.com/microsoft) tarafından

> Windows kimlik doğrulamasını bir MVC uygulaması bağlamında nasıl kullanacağınızı öğrenin. Uygulamanızın Web yapılandırma dosyasında Windows kimlik doğrulamasını etkinleştirmeyi ve IIS ile kimlik doğrulamanın nasıl yapılandırılacağını öğrenirsiniz. Son olarak, denetleyici eylemlerine erişimi belirli Windows kullanıcılarına veya gruplarına kısıtlamak için [Yetkilendir] özniteliğini nasıl kullanacağınızı öğrenirsiniz.

Bu öğreticinin amacı, MVC uygulamalarınızda görünümleri korumak için Internet Information Services yerleşik olarak bulunan güvenlik özelliklerinden nasıl yararlanabilmenizi açıklamaktır. Denetleyici eylemlerinin yalnızca belirli Windows kullanıcıları veya belirli Windows gruplarının üyesi olan kullanıcılar tarafından nasıl çağrılacağını öğrenirsiniz.

Windows kimlik doğrulamasının kullanılması, dahili bir şirket web sitesi (intranet sitesi) oluştururken ve kullanıcılarınızın Web sitesine erişirken standart Windows Kullanıcı adlarını ve parolalarını kullanmasını istediğinizde anlamlı hale gelir. Bir dış Web sitesi (Internet Web sitesi) oluşturuyorsanız bunun yerine Forms kimlik doğrulaması kullanmayı düşünün.

#### <a name="enabling-windows-authentication"></a>Windows kimlik doğrulamasını etkinleştirme

Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, Windows kimlik doğrulaması varsayılan olarak etkinleştirilmemiştir. Forms kimlik doğrulaması, MVC uygulamaları için etkinleştirilen varsayılan kimlik doğrulama türüdür. MVC uygulamanızın Web yapılandırma (Web. config) dosyasını değiştirerek Windows kimlik doğrulamasını etkinleştirmeniz gerekir. &lt;kimlik doğrulaması&gt; bölümünü bulun ve bunun gibi Forms kimlik doğrulaması yerine Windows kullanacak şekilde değiştirin:

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

Windows kimlik doğrulamasını etkinleştirdiğinizde, Web sunucunuz kullanıcıların kimliğini doğrulamak için sorumlu olur. Genellikle, bir ASP.NET MVC uygulaması oluştururken ve dağıttığınızda kullandığınız iki farklı Web sunucusu türü vardır.

İlk olarak, bir MVC uygulaması geliştirirken, Visual Studio ile birlikte gelen ASP.NET Development Web sunucusunu kullanırsınız. Varsayılan olarak, ASP.NET Development Web sunucusu tüm sayfaları geçerli Windows hesabı bağlamında yürütür (Windows 'da oturum açmak için kullandığınız hesap).

ASP.NET Development Web sunucusu, NTLM kimlik doğrulamasını da destekler. Çözüm Gezgini penceresinde projenizin adına sağ tıklayıp Özellikler ' i seçerek NTLM kimlik doğrulamasını etkinleştirebilirsiniz. Sonra, Web sekmesini seçin ve NTLM onay kutusunu işaretleyin (bkz. Şekil 1).

**Şekil 1: ASP.NET Development Web sunucusu için NTLM kimlik doğrulamasını etkinleştirme**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

Bir üretim Web uygulaması için, el ile IIS 'yi Web sunucunuz olarak kullanırsınız. IIS aşağıdakiler dahil çeşitli kimlik doğrulama türlerini destekler:

- Temel kimlik doğrulaması – HTTP 1,0 protokolünün bir parçası olarak tanımlanır. Kullanıcı adlarını ve parolaları Internet üzerinden şifresiz metin (Base64 kodlamalı) olarak gönderir. -Özet kimlik doğrulaması – internet üzerinden parolanın kendisi yerine bir parolanın karmasını gönderir. -Tümleşik Windows (NTLM) kimlik doğrulaması: Windows kullanarak intranet ortamlarında kullanılacak en iyi kimlik doğrulama türüdür. -Sertifika kimlik doğrulaması: istemci tarafı bir sertifika kullanarak kimlik doğrulaması etkinleştirilir. Sertifika bir Windows kullanıcı hesabıyla eşlenir.

> [!NOTE] 
> 
> Bu farklı kimlik doğrulama türleri hakkında daha ayrıntılı bir genel bakış için bkz. [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).

Belirli bir kimlik doğrulama türünü etkinleştirmek için Internet Information Services Manager 'ı kullanabilirsiniz. Her işletim sisteminde her bir kimlik doğrulama türünün mevcut olmadığından emin olun. Ayrıca, Windows Vista ile IIS 7,0 kullanıyorsanız, Internet Information Services Manager 'da görüntülenmeden önce farklı türlerdeki Windows kimlik doğrulamasını etkinleştirmeniz gerekir. **Denetim Masası, programlar, programlar ve Özellikler ' i açın, Windows özelliklerini açın veya kapatın**ve Internet Information Services düğümünü genişletin (bkz. Şekil 2).

**Şekil 2 – Windows IIS özelliklerini etkinleştirme**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

Internet Information Services kullanarak farklı kimlik doğrulama türlerini etkinleştirebilir veya devre dışı bırakabilirsiniz. Örneğin, Şekil 3 ' te anonim kimlik doğrulamasını devre dışı bırakma ve IIS 7,0 kullanırken tümleşik Windows (NTLM) kimlik doğrulamasını etkinleştirme gösterilmektedir.

**Şekil 3 – tümleşik Windows kimlik doğrulamasını etkinleştirme**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows kullanıcılarını ve gruplarını yetkilendirme

Windows kimlik doğrulamasını etkinleştirdikten sonra, denetleyicilere veya denetleyici eylemlerine erişimi denetlemek için &lt;Yetkilendir&gt; özniteliğini kullanabilirsiniz. Bu öznitelik, MVC denetleyicisinin tamamına veya belirli bir denetleyici eylemine uygulanabilir.

Örneğin, liste 1 ' deki giriş denetleyicisi dizin (), Companygizlilikler () ve StephenSecrets () adlı üç eylemi ortaya koyar. Herkes dizin () eylemini çağırabilir. Ancak, yalnızca Windows yerel Yöneticiler grubunun üyeleri Companygizlilikler () eylemini çağırabilir. Son olarak, yalnızca Stephen (Redmond etki alanında) adlı Windows etki alanı kullanıcısı StephenSecrets () eylemini çağırabilir.

**Listeleme 1 – Controllers\homecontroller.exe**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> Windows Kullanıcı hesabı denetimi (UAC) nedeniyle, Windows Vista veya Windows Server 2008 ile çalışırken, yerel Yöneticiler grubu diğer gruplardan farklı davranır. &lt;yetkilendirme&gt; özniteliği, bilgisayarınızın UAC ayarlarını değiştirmediğiniz takdirde yerel Yöneticiler grubunun bir üyesini doğru şekilde tanımaz.

Doğru izinler olmadan bir denetleyici eylemini çağırmaya çalıştığınızda, kimlik doğrulamanın etkin olması için gereken kimlik doğrulama türüne bağlı olarak ne olur? Varsayılan olarak, ASP.NET geliştirme sunucusunu kullandığınızda yalnızca boş bir sayfa alırsınız. Sayfa, **401 yetkili olmayan** bir http yanıt durumuyla birlikte sunulur.

Diğer taraftan, anonim kimlik doğrulaması devre dışı ve temel kimlik doğrulaması etkin IIS kullanıyorsanız, korumalı sayfayı her istediğinizde bir oturum açma iletişim kutusu istemi almaya devam edersiniz (bkz. Şekil 4).

**Şekil 4 – temel kimlik doğrulaması oturum açma iletişim kutusu**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>Özet

Bu öğreticide, Windows kimlik doğrulamasını bir ASP.NET MVC uygulaması bağlamında nasıl kullanabileceğiniz açıklanmaktadır. Uygulamanızın Web yapılandırma dosyasında Windows kimlik doğrulamasının nasıl etkinleştirileceğini ve IIS ile kimlik doğrulamanın nasıl yapılandırılacağını öğrendiniz. Son olarak, denetleyici eylemlerine erişimi belirli Windows kullanıcılarına veya gruplarına kısıtlamak için &lt;Yetkilendir&gt; özniteliğini nasıl kullanacağınızı öğrendiniz.

> [!div class="step-by-step"]
> [Önceki](authenticating-users-with-forms-authentication-vb.md)
> [İleri](preventing-javascript-injection-attacks-vb.md)
