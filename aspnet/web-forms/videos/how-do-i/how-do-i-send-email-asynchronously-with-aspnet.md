---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[Nasıl yapılır:] ASP.NET ile e-posta zaman uyumsuz Gönder | Microsoft Docs'
author: rick-anderson
description: Bu videoda, Chris pron, zaman uyumsuz bir e-posta iletisi göndermek için ASP.NET içindeki System .net. Mail sınıflarının nasıl kullanılacağını gösterir. İlk olarak bkz. Web 'i yapılandırma...
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: ea29823446cc1339003160bd3e945bde1af42473
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635704"
---
# <a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="c063d-104">[Nasıl yapılır:] ASP.NET ile e-posta zaman uyumsuz olarak gönderin</span><span class="sxs-lookup"><span data-stu-id="c063d-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>

<span data-ttu-id="c063d-105">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="c063d-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="c063d-106">Bu videoda, Chris pron, zaman uyumsuz bir e-posta iletisi göndermek için ASP.NET içindeki System .net. Mail sınıflarının nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c063d-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="c063d-107">İlk olarak, Web. config dosyasındaki &lt;mailSettings&gt; öğesini kullanarak e-posta göndermek üzere Web sitesini nasıl yapılandıracağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c063d-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="c063d-108">Sonra, e-posta bilgilerini girmek için basit bir kullanıcı arabirimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c063d-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="c063d-109">Ardından, sayfanın arkasındaki kodda bir e-posta iletisi oluşturmak için MailMessage sınıfını nasıl kullanacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c063d-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="c063d-110">Bu işlemin bir parçası olarak, e-postanın gönderilmesini izleyen zaman uyumsuz geri çağırma için bir olay işleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c063d-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="c063d-111">Olay işleyicisinde, e-posta gönderme işlemi hakkında bilgi sağlayan AsynchCompletedEventArgs sınıfının örneğini nasıl kullanacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c063d-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="c063d-112">Son olarak, hata ayıklama modundaki adımları izleyerek bir test e-postası zaman uyumsuz olarak gönderin ve işlemden alınan gerçek e-postayı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="c063d-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="c063d-113">&#9654;Videoyu izleyin (18 dakika)</span><span class="sxs-lookup"><span data-stu-id="c063d-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)
