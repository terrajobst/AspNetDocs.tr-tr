---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Katana 'da Windows kimlik doğrulamasını etkinleştirme | Microsoft Docs
author: MikeWasson
description: "Bu makalede, Katana 'da Windows kimlik doğrulamasının nasıl etkinleştirileceği gösterilmektedir. İki senaryo vardır: IIS kullanarak Katana barındırmak ve HttpListener 'ı Self-Host kat 'a kullanma..."
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617182"
---
# <a name="enabling-windows-authentication-in-katana"></a>Katana’da Windows Kimlik Doğrulamasını Etkinleştirme

, [Mike te son](https://github.com/MikeWasson)

> Bu makalede, Katana 'da Windows kimlik doğrulamasının nasıl etkinleştirileceği gösterilmektedir. İki senaryo ele alınmaktadır: Katana barındırmak için IIS kullanma ve özel bir işlemde bağımsız olarak kendi kendine konak Katana eklemek için HttpListener kullanma. Bu makaleyi gözden geçirmek için Barry Dorrans, David Matson ve Chris 'e teşekkür ederiz.

Katana, Microsoft 'un .NET için açık Web arabirimi olan [Owin](http://owin.org/)uygulamasıdır. OWıN ve Katana 'ya giriş bilgilerini [burada](an-overview-of-project-katana.md)bulabilirsiniz. OWIN mimarisi birçok katmana sahiptir:

- Ana bilgisayar: OWıN ardışık düzeninin çalıştırıldığı işlemi yönetir.
- Sunucu: bir ağ yuvası açar ve istekleri dinler.
- Ara yazılım: HTTP isteğini ve yanıtını Işler.

Katana Şu anda iki sunucu sağladığından, her ikisi de Windows tümleşik kimlik doğrulamasını destekler:

- **Microsoft. Owin. Host. SystemWeb**. ASP.NET işlem hattı ile IIS 'yi kullanır.
- **Microsoft. Owin. Host. HttpListener**. [System .net. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)kullanır. Bu sunucu şu anda kendi kendine barındırma Katana olduğunda varsayılan seçenektir.

> [!NOTE]
> Bu işlevsellik sunucuda zaten mevcut olduğundan Katana, şu anda Windows kimlik doğrulaması için OWıN ara yazılımı sağlamıyor.

## <a name="windows-authentication-in-iis"></a>IIS 'de Windows kimlik doğrulaması

Microsoft. Owin. Host. SystemWeb kullanarak IIS 'de Windows kimlik doğrulamasını etkinleştirebilirsiniz.

"ASP.NET Empty Web Application" proje şablonunu kullanarak yeni bir ASP.NET uygulaması oluşturarak başlayalım.

![](enabling-windows-authentication-in-katana/_static/image1.png)

Sonra NuGet paketlerini ekleyin. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

Şimdi aşağıdaki kodla `Startup` adlı bir sınıf ekleyin:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

Bu, IIS üzerinde çalışan OWIN için bir "Hello World" uygulaması oluşturmanız gerekir. Uygulamada hata ayıklamak için F5 tuşuna basın. "Merhaba Dünya!" görmeniz gerekir tarayıcı penceresinde.

![](enabling-windows-authentication-in-katana/_static/image2.png)

Daha sonra, IIS Express Windows kimlik doğrulamasını etkinleştireceğiz. **Görünüm** menüsünden **Özellikler**' i seçin. Proje özelliklerini görüntülemek için Çözüm Gezgini içindeki proje adına tıklayın.

**Özellikler** penceresinde, **anonim kimlik doğrulamasını** **devre dışı** olarak ayarlayın ve **Windows kimlik doğrulamasını** **etkin**olarak ayarlayın.

![](enabling-windows-authentication-in-katana/_static/image3.png)

Uygulamayı Visual Studio 'dan çalıştırdığınızda IIS Express kullanıcının Windows kimlik bilgilerini gerektirir. Bu, [Fiddler](http://fiddler2.com/home) veya başka bir http hata ayıklama aracı kullanarak bunu görebilirsiniz. Örnek bir HTTP yanıtı aşağıda verilmiştir:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

Bu yanıttaki WWW-kimlik doğrulama üst bilgileri, sunucunun Kerberos veya NTLM kullanan [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protokolünü desteklediğini gösterir.

Daha sonra, uygulamayı bir sunucusuna dağıttığınızda, bu sunucudaki IIS 'de Windows kimlik doğrulamasını etkinleştirmek için [Bu adımları](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) izleyin.

## <a name="windows-authentication-in-httplistener"></a>HttpListener 'da Windows kimlik doğrulaması

Self-Host Katana için Microsoft. Owin. Host. HttpListener kullanıyorsanız, doğrudan **HttpListener** örneğinde Windows kimlik doğrulamasını etkinleştirebilirsiniz.

İlk olarak yeni bir konsol uygulaması oluşturun. Sonra NuGet paketlerini ekleyin. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

Şimdi aşağıdaki kodla `Startup` adlı bir sınıf ekleyin:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

Bu sınıf, öncesinde aynı "Hello World" örneğini uygular, ancak Windows kimlik doğrulamasını da kimlik doğrulama düzeni olarak ayarlar.

`Main` işlevinin içinde OWıN ardışık düzenini başlatın:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

Uygulamanın Windows kimlik doğrulamasını kullandığını onaylamak için Fiddler 'da bir istek gönderebilirsiniz:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>İlgili Konular

[Project Katana’ya Genel Bakış](an-overview-of-project-katana.md)

[System .net. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[MVC 5 ' te OWıN Forms kimlik doğrulamasını anlama](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
