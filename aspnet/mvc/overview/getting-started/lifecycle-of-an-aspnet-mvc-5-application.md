---
uid: mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
title: ASP.NET MVC 5 uygulamasının yaşam döngüsü | Microsoft Docs
author: cephalin
description: ASP.NET MVC 5 uygulamasının yaşam döngüsünü gösteren bir PDF belgesi indirin. Bu yaşam döngüsü belgesi, MVC yaşam döngüsünün bir üst düzey görünümünü sağlar...
ms.author: riande
ms.date: 02/28/2014
ms.assetid: 9c1e3a75-b644-4480-8326-11300b1ec4b3
msc.legacyurl: /mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application
msc.type: authoredcontent
ms.openlocfilehash: f4a9b3fb61552b070db11fba617b5627fcd71cd5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582203"
---
# <a name="lifecycle-of-an-aspnet-mvc-5-application"></a>Bir ASP.NET MVC 5 Uygulamasının Yaşam Döngüsü

[cepby Ile bağlantılı](https://github.com/cephalin)

[PDF belgesini indir](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf)

Burada her ASP.NET MVC 5 uygulamasının yaşam döngüsünü gösteren bir PDF belgesi indirebilirsiniz, http isteğini istemciye geri göndermeye yönelik HTTP isteğini almasını sağlayabilirsiniz. Bu, ASP.NET MVC 'ye yeni olanlar için eğitim aracı olarak ve ayrıca uygulamanın belirli yönlerine ayrıntısına gitmek zorunda olanlar için bir başvuru olarak tasarlanmıştır. PDF belgesi aşağıdaki özelliklere sahiptir:

- MVC 'nin [ASP.NET uygulama yaşam](https://msdn.microsoft.com/library/bb470252.aspx)döngüsüne tümleştirildiğini anlamanıza yardımcı olacak ilgili [HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) aşamaları.
- Her MVC uygulamasının istek işleme ardışık düzeninde geçtiği önemli aşamaları anlayabildiğiniz MVC uygulama yaşam döngüsünün üst düzey bir görünümü.  
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image1.jpg)
- İstek işleme işlem hattının ayrıntılarına gidilmesini gösteren bir ayrıntı görünümü. Yaşam döngüsü ayrıntılarının çeşitli aşamalara nasıl toplandığını görmek için üst düzey görünümü ve ayrıntı görünümünü karşılaştırabilirsiniz. Daha büyük bir görünümü görmek için [PDF 'Yi indirin](lifecycle-of-an-aspnet-mvc-5-application/_static/lifecycle-of-an-aspnet-mvc-5-application1.pdf) .
    ![](lifecycle-of-an-aspnet-mvc-5-application/_static/image2.jpg)
- İstek işleme ardışık düzeninde [Denetleyici](https://msdn.microsoft.com/library/system.web.mvc.controller.aspx) nesnesindeki tüm geçersiz kılınabilir yöntemlerin yerleştirilmesi ve amacı. Herhangi bir yöntemi geçersiz kılmanız gerekebilir veya olmayabilir, ancak istediğiniz etkiye uygun yaşam döngüsü aşamasında kod yazmak için uygulama yaşam döngüsünde rolünü anlamanız önemlidir.
- Filtre türlerinin (kimlik doğrulama, yetkilendirme, eylem ve sonuç) nasıl çağrılabileceğini gösteren blown-up şemaları.
- Ayrıntı görünümündeki her ilgi noktasından faydalı bir makaleye veya bloga bağlanın.

## <a name="next-steps"></a>Sonraki Adımlar

Bu belge gereksiniminizi karşılar mı? Geri bildiriminiz bizim için teşekkür ederiz. Uygulamanızda ASP.NET MVC yaşam döngüsü üzerinde herhangi bir sorunuz varsa, [StackOverflow](http://stackoverflow.com/help) ve [ASP.NET MVC forumları](https://forums.asp.net/1146.aspx) sormak için harika bir yerdir. En son öğreticilerimde güncelleştirmeleri alabilmeniz için Twitter 'da [beni](https://twitter.com/Cephas_MSFT) izleyin.
