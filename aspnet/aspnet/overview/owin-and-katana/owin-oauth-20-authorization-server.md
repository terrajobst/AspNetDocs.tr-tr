---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWıN OAuth 2,0 yetkilendirme sunucusu | Microsoft Docs
author: hongyes
description: Bu öğretici, OWıN OAuth ara yazılımını kullanarak bir OAuth 2,0 yetkilendirme sunucusunu nasıl uygulayacağınızı size kılavuzluk eder. Bu, yalnızca bir çıktı olan gelişmiş bir öğreticidir...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000679"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="2233a-104">OWIN OAuth 2.0 Yetkilendirme Sunucusu</span><span class="sxs-lookup"><span data-stu-id="2233a-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="2233a-105">[OAuth 2,0 çerçevesi](http://tools.ietf.org/html/rfc6749) , bir üçüncü taraf UYGULAMANıN bir HTTP hizmetine sınırlı erişim elde etmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2233a-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="2233a-106">İstemci, korunan bir kaynağa erişmek için kaynak sahibinin kimlik bilgilerini kullanmak yerine, bir erişim belirteci alır (belirli bir kapsam, ömür ve diğer erişim özniteliklerini belirten bir dizedir).</span><span class="sxs-lookup"><span data-stu-id="2233a-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="2233a-107">Erişim belirteçleri, üçüncü taraf istemcilere, kaynak sahibinin onayına sahip bir yetkilendirme sunucusu tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="2233a-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="2233a-108">OWIN, .NET Web sunucuları ile Web uygulamaları arasında standart bir arabirim tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2233a-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="2233a-109">OWIN arabiriminin hedefi, sunucu ve uygulamayı ayırmak, .NET Web geliştirme için basit modüllerin geliştirilmesini teşvik etmek ve açık bir standart hale getirerek .NET Web geliştirme araçlarının açık kaynak ekosistemini temel hale getirmenize yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="2233a-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="2233a-110">Daha fazla bilgi için bkz. [Owin](http://owin.org/)</span><span class="sxs-lookup"><span data-stu-id="2233a-110">For more information, see [OWIN](http://owin.org/)</span></span>
