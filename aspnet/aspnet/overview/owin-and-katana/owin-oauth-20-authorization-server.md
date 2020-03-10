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
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617112"
---
# <a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 Yetkilendirme Sunucusu

[OAuth 2,0 çerçevesi](http://tools.ietf.org/html/rfc6749) , bir üçüncü taraf UYGULAMANıN bir HTTP hizmetine sınırlı erişim elde etmesini sağlar. İstemci, korunan bir kaynağa erişmek için kaynak sahibinin kimlik bilgilerini kullanmak yerine, bir erişim belirteci alır (belirli bir kapsam, ömür ve diğer erişim özniteliklerini belirten bir dizedir). Erişim belirteçleri, üçüncü taraf istemcilere, kaynak sahibinin onayına sahip bir yetkilendirme sunucusu tarafından verilir.

OWIN, .NET Web sunucuları ile Web uygulamaları arasında standart bir arabirim tanımlar. OWIN arabiriminin hedefi, sunucu ve uygulamayı ayırmak, .NET Web geliştirme için basit modüllerin geliştirilmesini teşvik etmek ve açık bir standart hale getirerek .NET Web geliştirme araçlarının açık kaynak ekosistemini temel hale getirmenize yöneliktir.

Daha fazla bilgi için bkz. [Owin](http://owin.org/)
