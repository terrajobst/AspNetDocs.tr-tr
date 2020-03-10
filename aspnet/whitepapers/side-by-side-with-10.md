---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1,0 ve 1,1 ' nin yan yana yürütülmesi | Microsoft Docs
author: rick-anderson
description: Bu Teknik İnceleme, makinenizde hem .NET 1,0 hem de .NET 1,1 ' nin nasıl yükleneceğini ve bir ASP.NET Web uygulamasının her iki sürümünde de çalışmasına izin verir...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632974"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>ASP.NET .NET Framework 1.0 ve 1.1 Sürümlerini Yan Yana Yürütme

> Bu Teknik İnceleme, makinenizde hem .NET 1,0 hem de .NET 1,1 ' nin nasıl yükleneceğini ve bir ASP.NET Web uygulamasının Framework 'ün herhangi bir sürümünde çalışmasına izin verir.
> 
> ASP.NET 1,0 ve ASP.NET 1,1 için geçerlidir.

ASP.NET ' de, uygulamalar aynı bilgisayara yüklendiklerinde yan yana çalışıyor olarak kabul edilir, ancak .NET Framework farklı sürümlerini kullanır. Aşağıdaki konu, yan yana yürütme için ASP.NET uygulamalarının nasıl yapılandırılacağını açıklar ve aşağıdakiler için ayrıntılı adımlar sağlar:

- [Yükleme sırasında Web uygulamanızın .NET Framework sürüm 1,0 ' e eşlenmesini koruyun](#1)
- [Bir Web uygulamasını .NET Framework belirli bir sürümüne eşleyin](#2)
- [Bir Web sitesinin kullandığı .NET Framework sürümünü bulma](#3)

Geleneksel olarak, bir bilgisayarda bir bileşen veya uygulama güncelleştirildiği zaman, eski sürüm kaldırılır ve daha yeni bir sürümle değiştirilmiştir. Yeni sürüm önceki sürümle uyumlu değilse, bu genellikle bileşeni veya uygulamayı kullanan diğer uygulamaları keser. .NET Framework, bir derleme veya uygulamanın birden çok sürümünün aynı anda aynı bilgisayara yüklenmesine izin veren yan yana yürütme desteği sağlar. Aynı anda birden çok sürüm yüklenebildiğinden, yönetilen uygulamalar farklı bir sürüm kullanan uygulamaları etkilemeden hangi sürümün kullanılacağını seçebilir.

Varsayılan olarak, .NET Framework sürüm 1,1 yüklemesi sırasında, tüm mevcut ASP.NET uygulamaları .NET Framework en son sürümünü kullanacak şekilde otomatik olarak yeniden yapılandırılır. ASP.NET uygulamalarınızın varsayılan .NET Framework 1,1 ' i kullanmasını istemiyorsanız, yükleme sırasında bunu nasıl önleyeceğinizi öğrenmek için [buraya](#1) tıklayın.

Web sunucunuzu 1,1 .NET Framework ve bir veya daha fazla Web uygulamasının .NET Framework 1,0 ' i çalıştırmak istiyorsanız, Internet Information Services (IIS) betik eşlemesini güncelleştirmeniz gerekir. Betik eşleme, belirli bir Web uygulaması için. aspx dosya uzantısını .NET Framework bir sürümüne eşlemek için bir mekanizmadır. Bir Web uygulamasını .NET Framework belirli bir sürümüne nasıl eşleyeceğinizi öğrenmek için [buraya](#2) tıklayın.

Belirli bir Web uygulamasını hangi .NET Framework sürümünün çalıştırmakta olduğunu bulmak için Internet Information Manager veya ASP.NET IIS kayıt aracı 'nı (ASPNET\_regııs. exe) kullanabilirsiniz. Bir Web sitesinin kullandığı .NET Framework sürümünü bulma hakkında bilgi edinmek için [buraya](#3) tıklayın.

.NET Framework 1,1 ' e geçiş yaparken bir içeri aktarma işlemi, .NET Framework her bir sürümünün kendi Machine. config dosyasını kullanmalarından biridir. Sonuç olarak, bir Web Yöneticisi Machine. config dosyasında değişiklik yaptıysanız, bu değişikliklerin .NET Framework 1,1 Machine. config dosyasına geçirilmesi gerekir.

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>Web uygulamanızın yükleme sırasında .NET Framework 1,0 ' e eşlenmesini koruma

Varsayılan olarak, tüm mevcut ASP.NET uygulamaları yükleme sırasında .NET Framework 'in daha yeni bir sürümünü kullanmak üzere otomatik olarak yeniden yapılandırılır. .NET Framework daha yeni sürümünü kullanarak uygulamalar, yeni sürümde sunulan geliştirmelerden ve yeni özelliklerden tam olarak faydalanabilir. Aynı zamanda, hangi uygulamaların güncelleştirildiği üzerinde ayrıntılı denetim yapmak isteyebileceğiniz Web Yöneticisi, .NET Framework yüklemesi sırasında var olan tüm ASP.NET uygulamalarının otomatik yeniden eşleştirmasını önleyebilir.

Tüm ASP.NET uygulamasının .NET Framework yeni sürümüne otomatik olarak yeniden eşleştirmeyi engellemek için Web Yöneticisi, Dotnetfx. exe Kurulum programı ile/noaspupgrade komut satırı seçeneğini kullanabilir.

**ASP.NET uygulamasının toplam yeniden eşleştirmasını daha yeni bir sürüme engellemek için**

1. **Başlat**'a gidin.
2. **Çalıştır**' a tıklayın.
3. **Cmd**yazın.
4. **Tamam**’a tıklayın.  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. Komut isteminde, .NET Framework: **Dotnetfx. exe/c: "/noaspupgrade yüklensin mi?** . yüklemesini başlatmak için aşağıdaki satırı yazın.  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. Microsoft .NET Framework 1,1 kurulumunda **Evet** ' e tıklayın. Bu işlem 1,1 .NET Framework kurulum işlemini başlatacak.  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>Bir Web uygulamasını .NET Framework belirli bir sürümüne eşleyin

.NET Framework her sürümü, ASP.NET IIS kayıt aracı 'nın (ASPNET\_regııs. exe) bir sürümünü içerir. Bu araç, yöneticilerin bir Web uygulamasının .NET Framework belirli bir sürümü altında çalıştırıldığını belirtmesini sağlar. Bu, bir Web uygulamasını .NET Framework bir sürümüne eşleme olarak adlandırılır. Yöneticiler, Web uygulamasıyla ilişkilendirilecek .NET Framework sürümüne karşılık gelen ASPNET\_regııs. exe ' yi seçmelidir. Örneğin, bir Web sitesinin 1,1 .NET Framework kullanmasını belirtmek isteyen bir yöneticinin .NET Framework 1,1 ile birlikte gelen ASPNET\_regııs. exe ' yi kullanması gerekir.

Sürüm 1,0 için ASPNET\_regııs. exe şu konumda bulunur:

- C:\WINDOWS\Microsoft.NET\Framework\\**v 1.0.3705**\aspnet\_regııs

Sürüm 1 için regııs. exe\_ASPNET, şu konumda bulunur:

- C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\aspnet\_regııs

ASPNET\_regııs. exe, bir Web uygulamasını betik eşleme için iki seçenek sunar:

- **-s** , yol içindeki ve alt dizinlerinde betik eşlemesini ayarlar.
- **-sn** yalnızca yoldaki betik eşlemesini ayarlar.

Yol, W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} biçiminde tanımlanan Web uygulaması IIS meta veri yolunu tanımlar. Örneğin, varsayılan Web sitesi altında bulunan Portal adlı bir Web uygulaması için, metatabanı yolu W3SVC/1/ROOT/Portal olur.

![](side-by-side-with-10/_static/image4.gif)

Ayrıca, metatabanı yolunu almak için metatabanı düzenleyicisi olarak adlandırılan bir araç da kullanabilirsiniz. Bu aracı, [https://support.microsoft.com/default.aspx?scid=kb, en-US; 232068](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068) konumundaki Microsoft desteği sitesinden indirebilirsiniz.

- Portal IIS betik eşlemesini ve alt öğesini güncelleştirmek için ASPNET\_regııs. exe-s W3SVC/1/ROOT/Portal çalıştırın.  
  
    ![](side-by-side-with-10/_static/image5.gif)

- Portaldaki uygulamaları etkilemeden Portal IIS betik eşlemesini güncelleştirmek için ASPNET\_regııs. exe-sn W3SVC/1/ROOT/Portal çalıştırın.  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>Bir Web uygulamasının kullandığı .NET Framework sürümünü bulma

Yönetici, .NET Framework bir Web sitesi hangi sürümünün çalıştığını bulmak için Internet Service Manager kullanabilir. Farklı işletim sistemi sürümleri Internet Service Manager farklı şekilde başlatır. Service Manager 'ı başlatmak için aşağıda listelenen adımları izleyin.

**Internet Service Manager başlatmak için**

1. **Başlat**'a gidin.
2. **Çalıştır**' a tıklayın.
3. **İnetmgr**yazın.  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. Internet Service Manager, .NET Framework sürümünü kullanmak istediğiniz Web uygulamasını seçin.  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. Web uygulamasına sağ tıklayın ve Özellikler ' e tıklayın **.**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. Özellik penceresinde yapılandırma ' yı seçin **.**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. Uygulama eşleme tablosundan **. aspx**' i seçin ve **Düzenle**' ye tıklayın.  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. **Yürütülebilir** metin kutusundan, kaydırma yoluyla sürüm dizinine bakın. Sürüm dizini v. 1.1.4322 ise, uygulama .NET Framework 1,1 ile eşleştirilir. Buna karşılık, sürüm dizini v 1.0.3705 ise, uygulama .NET Framework 1,0 ile eşleştirilir.  
  
    ![](side-by-side-with-10/_static/image12.gif)
