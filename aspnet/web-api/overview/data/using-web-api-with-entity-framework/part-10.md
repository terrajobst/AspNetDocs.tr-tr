---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Uygulamayı Azure 'da yayımlayın Azure App Service | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622390"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>Uygulamayı Azure 'da yayımlayın Azure App Service

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Son adım olarak, uygulamayı Azure 'da yayımlayacaksınız. Çözüm Gezgini, projeye sağ tıklayın ve **Yayımla**' yı seçin.

![](part-10/_static/image1.png)

**Yayımla** ' ya tıklamak **Web 'i Yayımla** iletişim kutusunu çağırır. Projeyi ilk oluşturduğunuz sırada **bulutta konak** denetlediyseniz, bağlantı ve ayarlar zaten yapılandırılmıştır. Bu durumda, yalnızca **Ayarlar** sekmesine tıkladıktan sonra Code First Migrations&quot;&quot;Yürüt ' ü kontrol edin. (Başlangıçta **Konağı bulutta** denetmediyseniz, [sonraki bölümdeki](#new-website)adımları izleyin.)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

Uygulamayı dağıtmak için **Yayımla**' ya tıklayın. Yayımlama ilerlemesini **Web yayımlama etkinliği** penceresinde görebilirsiniz. ( **Görünüm** menüsünde **diğer pencereler**' i seçin ve ardından **Web yayımlama etkinliği**' ni seçin.)

![](part-10/_static/image4.png)

Visual Studio uygulamayı dağıtırken, varsayılan tarayıcı otomatik olarak dağıtılan Web sitesinin URL 'SI olarak açılır ve oluşturduğunuz uygulama artık bulutta çalışmaktadır. Tarayıcı adres çubuğundaki URL, sitenin Internet 'ten yüklenmekte olduğunu gösterir.

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>Yeni bir Web sitesine dağıtma

Projeyi ilk oluşturduğunuzda **bulutta konak** denetmediyseniz, şimdi yeni bir Web uygulaması yapılandırabilirsiniz. Çözüm Gezgini, projeye sağ tıklayın ve **Yayımla**' yı seçin. **Profil** sekmesini seçin ve **Microsoft Azure Web siteleri**' ne tıklayın. Şu anda Azure 'da oturum açmadıysanız, oturum açmanız istenir.

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

**Mevcut Web siteleri** Iletişim kutusunda **Yeni**' ye tıklayın.

![](part-10/_static/image9.png)

Bir site adı girin. Azure aboneliğinizi ve bölgeyi seçin. **Veritabanı sunucusu**altında **Yeni sunucu oluştur**' u seçin veya var olan bir sunucuyu seçin. **Oluştur**'u tıklatın.

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

**Ayarlar** sekmesine tıklayın ve Code First Migrations&quot;&quot;yürütün ' i işaretleyin. Ardından **Yayımla**' ya tıklayın.

> [!div class="step-by-step"]
> [Öncekini](part-9.md)
