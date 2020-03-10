---
uid: web-forms/videos/how-do-i/how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list
title: '[Nasıl yapılır:] Dağıtım listesine e-posta göndermek için yeniden kullanılabilir bir bileşen oluştur | Microsoft Docs'
author: rick-anderson
description: Bu videoda, bir alıcı listesine e-posta gönderen birden çok Web sayfasında ve Web sitesinde kullanılabilen bir bileşenin nasıl oluşturulacağı gösterilmektedir. Firmalar...
ms.author: riande
ms.date: 12/04/2008
ms.assetid: 13dd3a26-c210-432e-91fe-355c979060b3
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list
msc.type: video
ms.openlocfilehash: 6a117d0bf029245c4929e903e0c0494f6ba2b072
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523466"
---
# <a name="how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list"></a><span data-ttu-id="23b69-104">[Nasıl yapılır:] Dağıtım listesine e-posta göndermek için yeniden kullanılabilir bir bileşen oluşturma</span><span class="sxs-lookup"><span data-stu-id="23b69-104">[How Do I:] Create a Reusable Component for Sending Email to a Distribution List</span></span>

<span data-ttu-id="23b69-105">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="23b69-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="23b69-106">Bu videoda, bir alıcı listesine e-posta gönderen birden çok Web sayfasında ve Web sitesinde kullanılabilen bir bileşenin nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="23b69-106">In this video Chris Pels shows how to create a component that can be used on multiple web pages and web sites that sends emails to a list of recipients.</span></span> <span data-ttu-id="23b69-107">İlk olarak, ASP.NET Web sitesi, Web. config dosyasındaki &lt;mailSettings&gt; kullanarak e-posta gönderecek şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="23b69-107">First, the ASP.NET web site will be configured to send email using the &lt;mailSettings&gt; in the web.config file.</span></span> <span data-ttu-id="23b69-108">Daha sonra bir veri kaynağından (DB, XML, vb.) alıcıların listesini okumak ve sistem .net. Mail sınıflarını kullanarak alıcıların her birine bir e-posta iletisi göndermek için bir sınıf ve çeşitli yöntemler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="23b69-108">Then a class and several methods are created to read a list of recipients from a data source (DB, XML, etc.) and send an email message to each of the recipients using the System.Net.Mail classes.</span></span> <span data-ttu-id="23b69-109">Bu işlemin bir parçası olarak, özel durum işleme dahildir.</span><span class="sxs-lookup"><span data-stu-id="23b69-109">As part of this process exception handling is included.</span></span> <span data-ttu-id="23b69-110">Ayrıca, kullanıcının Kimden adresi, konu, ek ekleme, vb. gibi öğeleri belirtmesini sağlamak için bir kullanıcı arabirimi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="23b69-110">In addition, a user interface is created to allow the user to specify items such as the From address, Subject, add an attachment, etc.</span></span>

[<span data-ttu-id="23b69-111">&#9654;Videoyu izleyin (35 dakika)</span><span class="sxs-lookup"><span data-stu-id="23b69-111">&#9654; Watch video (35 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-reusable-component-for-sending-email-to-a-distribution-list)
