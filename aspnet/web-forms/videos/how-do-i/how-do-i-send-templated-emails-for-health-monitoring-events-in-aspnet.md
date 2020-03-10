---
uid: web-forms/videos/how-do-i/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet
title: "[Nasıl yapılır:] ASP.NET 'de sistem durumu Izleme olayları için şablonlu e-postalar gönder | Microsoft Docs"
author: rick-anderson
description: Bu videoda, kemal 'in bir şablon kullanan sistem durumu izleme olayları gerçekleştiğinde e-posta göndermek için TemplatedEmailWebEventProvider 'nin nasıl kullanılacağı gösterilmektedir...
ms.author: riande
ms.date: 09/18/2008
ms.assetid: 5c107c6e-9fb7-4206-bd3f-221cb0767f8a
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet
msc.type: video
ms.openlocfilehash: e7b929c6e186e59b43180e8f26cf0f8b4608328f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629068"
---
# <a name="how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet"></a><span data-ttu-id="81999-103">[Nasıl yapılır:] ASP.NET 'de sistem durumu Izleme olayları için şablonlu e-postalar gönderme</span><span class="sxs-lookup"><span data-stu-id="81999-103">[How Do I:] Send Templated Emails for Health Monitoring Events in ASP.NET</span></span>

<span data-ttu-id="81999-104">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="81999-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="81999-105">Bu videoda, kemal 'in e-posta içeriği için bir şablon kullanan sistem durumu izleme olayları gerçekleştiğinde e-posta göndermek için TemplatedEmailWebEventProvider 'nin nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="81999-105">In this video Chris Pels shows how to use the TemplatedEmailWebEventProvider to send emails when health monitoring events occur that utilize a template for the email content.</span></span> <span data-ttu-id="81999-106">İlk olarak, şablonlu e-posta kullanımını uygulamak ve bir sistem durumu izleme olayını şablonlu e-posta sağlayıcısıyla ilişkilendirmek için, Web. config dosyasındaki &lt;sağlayıcısı&gt; ve &lt;&gt; kurallarını yapılandırma konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="81999-106">First, see how to configure the &lt;provider&gt; and &lt;rules&gt; elements in the web.config file to implement the use of templated email and associate a health monitoring event with the templated email provider.</span></span> <span data-ttu-id="81999-107">Şablonlu sağlayıcı yapılandırıldıktan sonra standart. aspx sayfası olarak kullanarak e-posta şablonu oluşturma bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="81999-107">Once the templated provider is configured see how to create the email template using as standard .aspx page.</span></span> <span data-ttu-id="81999-108">TemplatedEmailWebEventProvider tarafından Template. aspx sayfasına geçirilen MailEventNotificaitonInfo sınıfında hangi bilgilerin kullanılabildiğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="81999-108">Learn what information is available in the MailEventNotificaitonInfo class that is passed by the TemplatedEmailWebEventProvider to the template .aspx page.</span></span> <span data-ttu-id="81999-109">E-posta içeriğine uygun bilgileri eklemek için nasıl kullanılabileceğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="81999-109">See how it can be used to include whatever information is appropriate in the email content.</span></span> <span data-ttu-id="81999-110">Son olarak, sistem durumu izleme olaylarına yanıt olarak e-posta gönderen test Web sitesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="81999-110">Finally, view the test web site which sends emails in response to health monitoring events.</span></span> <span data-ttu-id="81999-111">Ardından, şablonu temel alan sistem durumu izleme olay bilgilerini içeren alınan gerçek e-postaları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="81999-111">Then view the actual emails received that contain the health monitoring event information based upon the template.</span></span>

[<span data-ttu-id="81999-112">&#9654;Videoyu izleyin (25 dakika)</span><span class="sxs-lookup"><span data-stu-id="81999-112">&#9654; Watch video (25 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-templated-emails-for-health-monitoring-events-in-aspnet)
