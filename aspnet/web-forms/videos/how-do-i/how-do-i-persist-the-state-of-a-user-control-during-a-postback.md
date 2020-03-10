---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: Bu videoda, bir kullanıcı denetimindeki bir veya daha fazla nesnenin durumunun kalıcı hale getirilmesi gösterilmektedir. İlk olarak, şunu temsil eden bir kullanıcı denetimi oluşturulur...
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635823"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a>[Nasıl Yapılır?]: geri gönderme sırasında Kullanıcı denetiminin durumunu kalıcı hale getirme
[How Do I]: Persist the State of a User Control During a Postback

<span data-ttu-id="3b97f-104">[Chris](https://twitter.com/chrispels) 'e göre</span><span class="sxs-lookup"><span data-stu-id="3b97f-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="3b97f-105">Bu videoda, bir kullanıcı denetimindeki bir veya daha fazla nesnenin durumunun kalıcı hale getirilmesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3b97f-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="3b97f-106">İlk olarak, bir kullanıcının arama için filtre ölçütü belirtme yeteneğini temsil eden bir kullanıcı denetimi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3b97f-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="3b97f-107">Ayrıca, filtre bilgilerini depolamak için bir yardımcı filtre sınıfı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3b97f-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="3b97f-108">Filtre denetimine çeşitli kullanıcı arabirimi öğeleri, filtre sınıfı örneğinde geçerli filtre bilgilerini depolamak için bazı yöntemler ve özelliklerle birlikte eklenir.</span><span class="sxs-lookup"><span data-stu-id="3b97f-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="3b97f-109">Sonra, Kullanıcı denetimi kalıcılığı RegisterRequiresControlState yöntemi ve ilişkili Save/restore yöntemleri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3b97f-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="3b97f-110">Bu yöntemler, sayfanın geri göndermeler sırasında filtre sınıfının ve verilerinin örneğini depolar.</span><span class="sxs-lookup"><span data-stu-id="3b97f-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="3b97f-111">Son olarak, denetim durumu uygulamasında birden çok nesneyi depolamanın bir tartışması vardır.</span><span class="sxs-lookup"><span data-stu-id="3b97f-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="3b97f-112">&#9654;Videoyu izleyin (23 dakika)</span><span class="sxs-lookup"><span data-stu-id="3b97f-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
