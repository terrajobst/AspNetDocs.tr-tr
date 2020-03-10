---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 ASP.NET Scafkatlama | Microsoft Docs
author: Rick-Anderson
description: ASP.NET Scafkatlama, Visual Studio 2013 eklenen yeni bir özelliktir.
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557983"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a>Visual Studio 2013’te ASP.NET İskeleti Oluşturma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> ASP.NET Scafkatlama, Visual Studio 2013 eklenen yeni bir özelliktir.

## <a name="overview"></a>Genel bakış

ASP.NET Scafkatlama, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir. Visual Studio 2013, MVC ve Web API projeleri için önceden yüklenmiş kod oluşturucuları içerir. Veri modelleriyle etkileşim kuran kodu hızlıca eklemek istediğinizde projenize yapı iskelesi eklersiniz. Yapı iskelesi kullanmak, projenizde standart veri işlemlerinin geliştirilmesi için geçen süreyi azaltabilir.

Visual Studio 2013, varsayılan olarak, bir Web Forms projesi için kod oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek veya bir uzantı yükleyerek Web Forms ile yapı iskelesi kullanabilirsiniz. Her iki yaklaşım da aşağıda gösterilmiştir.

Visual Studio 2013 güncelleştirme 2 (Şu anda RC), senaryolarınızın gereksinimlerini karşılamak için ASP.NET Scafkatını genişletme olanağı sunar. Bu işlevle özelleştirilmiş bir yapı iskelesi şablonu oluşturabilir ve bunu yeni Scaffold iletişim kutusu Ekle ' ye ekleyebilirsiniz. Özelleştirilmiş şablon içinde, bir yapı iskelesi öğesi eklenirken oluşturulan kodu belirtirsiniz. Daha fazla bilgi için bkz. [Visual Studio Için özel bir Scaffolder oluşturma](https://go.microsoft.com/fwlink/p/?LinkId=395029).

## <a name="prerequisites"></a>Önkoşullar

ASP.NET Scafkatlamayı kullanmak için, şunları yapmanız gerekir:

- Microsoft Visual Studio 2013
- Web Geliştirici Araçları (varsayılan Visual Studio 2013 yüklemesinin parçası)
- ASP.NET Web çerçeveleri ve Araçları 2013 (varsayılan Visual Studio 2013 yüklemesinin parçası)

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>MVC veya Web API 'sine bir yapı iskelesi öğesi ekleme

Bir yapı iskelesi eklemek için projeye veya proje içindeki bir klasöre sağ tıklayın ve aşağıdaki görüntüde gösterildiği gibi **Ekle** – **Yeni Scafkatlanmış öğe**' yi seçin.

![Yapı iskelesi öğesi Ekle](aspnet-scaffolding-overview/_static/image1.png)

**Yapı Iskelesi Ekle** penceresinde, eklenecek yapı iskelesi türünü seçin.

![Yapı iskelesi türünü seçin](aspnet-scaffolding-overview/_static/image2.png)

**Denetleyici Ekle** penceresi, Entity Framework 6 ' dan yeni zaman uyumsuz özellikleri kullanmak isteyip istemediğiniz da dahil olmak üzere, denetleyiciyi oluşturma seçeneklerini seçmenizi sağlar.

![denetleyici Ekle](aspnet-scaffolding-overview/_static/image3.png)

Senaryonuz için ilgili sınıflar ve sayfalar oluşturulur. Örneğin, aşağıdaki görüntüde, filmler adlı bir model sınıfı için scafkatlama aracılığıyla oluşturulan MVC denetleyicisi ve görünümleri gösterilmektedir.

![Oluşturulan dosyalar](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>Web Forms bir yapı iskelesi öğesi ekleme

Web Forms kod üreten yapı iskelesi eklemek için, Visual Studio 'ya bir uzantı yüklemeli ya da MVC bağımlılıklarını eklemeniz gerekir. Her iki yaklaşım da aşağıda gösterilmektedir, ancak yalnızca bu yaklaşımlardan birini yapmanız gerekir.

### <a name="web-forms-scaffolding-extension"></a>Web Forms yapı Iskelesi uzantısı

Bir Web Forms projesiyle yapı iskelesi kullanmanıza imkan tanıyan bir Visual Studio uzantısı yükleyebilirsiniz. Visual Studio 'da **Araçlar** ve ardından **Uzantılar ve güncelleştirmeler**' i seçin. Bu iletişim kutusunda, **Web Forms yapı iskelesi**Için Visual Studio Galerisi ' ni arayın.

![Web Forms yapı iskelesi yüklemesi](aspnet-scaffolding-overview/_static/image5.png)

Daha fazla bilgi için bkz. [Web Forms Scafkatlaması](https://go.microsoft.com/fwlink/p/?LinkId=396478).

### <a name="mvc-dependencies"></a>MVC bağımlılıkları

MVC bağımlılıklarını eklemek için - **yeni yapı Iskelesi öğesi** **Ekle** ' yi seçin. Yapı Iskelesi Ekle penceresinde, aşağıda gösterildiği gibi **MVC bağımlılıklarını**seçin.

![MVC bağımlılıkları Ekle](aspnet-scaffolding-overview/_static/image6.png)

Yapı iskelesi MVC için iki seçenek vardır; En az ve tam. En az ' ı seçerseniz, projenize yalnızca NuGet paketleri ve ASP.NET MVC başvuruları eklenir. Tam seçeneğini belirlerseniz, en düşük bağımlılıklar ve bir MVC projesi için gerekli içerik dosyaları eklenir. Kolayca yapı iskelesi kullanmak için tam bağımlılıklar ' ı seçin.

![Tam bağımlılıklar seçin](aspnet-scaffolding-overview/_static/image7.png)

Bağımlılıkları ekledikten sonra bir **README. txt** dosyası görürsünüz. Projenizin doğru çalıştığından emin olmak için bu dosyadaki yönergeleri dikkatle izleyin.

Readme. txt dosyasındaki adımları tamamladığınızda, MVC ve Web API 'SI ile ilgili önceki bölümde gösterildiği gibi yeni bir yapı iskelesi öğesi ekleyebilirsiniz. Otomatik olarak oluşturulan görünümler ve denetleyici projeniz içinde doğru şekilde çalışır.

## <a name="tutorials"></a>Öğreticiler

Özelleştirilmiş bir scaffolder oluşturmak için bkz. [Visual Studio Için özel bir Scaffolder oluşturma](https://go.microsoft.com/fwlink/p/?LinkId=395029).

Oluşturulan dosyaları özelleştirmek için, bkz. [oluşturulan dosyaları yeni Scafkatlanmış öğe iletişim kutusundan özelleştirme](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).

**Database First geliştirmeyle**yapı iskelesi kullanmanın bir örneği için bkz. [ASP.NET MVC ile EF Database First](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).

**MVC** projesinde scafkatlamayı kullanmanın bir örneği için bkz. [ASP.NET MVC 5 ile çalışmaya](../../../mvc/overview/getting-started/introduction/getting-started.md)başlama.

**Web API** projesinde yapı iskelesi kullanmanın bir örneği için bkz. [Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).
