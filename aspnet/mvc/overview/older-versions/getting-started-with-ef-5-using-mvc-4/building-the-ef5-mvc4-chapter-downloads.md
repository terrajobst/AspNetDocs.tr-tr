---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: EF 5 MVC 4 öğreticileri için bölüm Indirmeleri oluşturma | Microsoft Docs
author: Rick-Anderson
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599465"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>EF 5 MVC 4 öğreticileri için bölüm Indirmeleri oluşturma

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın.

## <a name="building-the-chapter-downloads"></a>Bölüm İndirmeleri Oluşturma

1. Proje örnek ZIP dosyasını indirip sıkıştırmasını açın. Sıkıştırılmış indirme paketinde, her bölümün tamamlanması için bir tane olmak üzere ek ZIP dosyaları bulacaksınız.
2. İstenen ZIP dosyasına sağ tıklayın, **Özellikler**' e tıklayın ve **Engellemeyi kaldır** düğmesine tıklayın.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. Dosyayı sıkıştırmayı açın.
4. Visual Studio 'Yu başlatmak için *cux. sln* dosyasına çift tıklayın.
5. **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. Paket Yöneticisi konsolunda (PMC) **geri yükle**' ye tıklayın.  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. Visual Studio 'dan çıkın.
8. Yukarıdaki adımda kapattığınız çözüm dosyasını açarak Visual Studio 'Yu yeniden başlatın.
9. Paket Yöneticisi konsolunda (PMC) `Update-Database` komutunu girin:  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > Aşağıdaki hatayı alırsanız:  
    >   
    >  *' Update-Database ' terimi bir cmdlet, işlev, betik dosyası veya çalıştırılabilir programının adı olarak tanınmıyor. Adın yazımını denetleyin veya bir yol içerilip yolun doğru olduğundan emin olun ve yeniden deneyin.*  
    > Çıkın ve Visual Studio 'Yu yeniden başlatın.

    Her geçiş çalışır ve ardından çekirdek yöntemi çalışacaktır. Artık uygulamayı çalıştırabilirsiniz.

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [Öncekini](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
