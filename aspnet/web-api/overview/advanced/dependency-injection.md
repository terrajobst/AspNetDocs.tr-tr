---
uid: web-api/overview/advanced/dependency-injection
title: ASP.NET Web API 2-ASP.NET 4. x içinde bağımlılık ekleme
author: MikeWasson
description: Bu öğreticide, ASP.NET 4. x için ASP.NET Web API denetleyicinize bağımlılık ekleme gösterilmektedir.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622607"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de bağımlılık ekleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> Bu öğreticide, ASP.NET Web API denetleyicinize bağımlılık ekleme gösterilmektedir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API 2
> - [Unity uygulama bloğu](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (sürüm 5 de kullanılabilir)

## <a name="what-is-dependency-injection"></a>Bağımlılık ekleme nedir?

*Bağımlılık* , başka bir nesnenin gerektirdiği herhangi bir nesnedir. Örneğin, veri erişimini işleyen bir [Depo](http://martinfowler.com/eaaCatalog/repository.html) tanımlanması yaygındır. Bir örnekle bakalım. İlk olarak, bir etki alanı modeli tanımlayacağız:

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

İşte, Entity Framework kullanarak bir veritabanındaki öğeleri depolayan basit bir depo sınıfı.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

Şimdi `Product` varlıkları için GET isteklerini destekleyen bir Web API denetleyicisi tanımlayalim. (Basitlik için GÖNDERI ve diğer yöntemleri dışarıda bırakıyorum.) İlk deneme aşağıda verilmiştir:

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

Denetleyici sınıfının `ProductRepository`bağlı olduğuna dikkat edin ve denetleyicinin `ProductRepository` örneğini oluşturmasına izin veriyoruz. Bununla birlikte, birkaç nedenden dolayı bağımlılığı bu şekilde sabit olarak kodladığı için kötü bir fikir olabilir.

- `ProductRepository` farklı bir uygulamayla değiştirmek istiyorsanız, denetleyici sınıfını da değiştirmeniz gerekir.
- `ProductRepository` bağımlılıkları varsa, bunları denetleyicinin içinde yapılandırmanız gerekir. Birden çok denetleyici içeren büyük bir proje için yapılandırma kodunuz projenize dağılmış hale gelir.
- Denetleyici, veritabanını sorgulamak için sabit kodlanmış olduğundan, birim testi zordur. Birim testi için, geçerli tasarımla mümkün olmayan bir sahte veya saplama deposu kullanmanız gerekir.

Bu sorunları, depoyu denetleyiciye *ekleme* göre ele alabilir. İlk olarak, `ProductRepository` sınıfını bir arabirim olarak yeniden düzenleyin:

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

Sonra `IProductRepository` Oluşturucu parametresi olarak sağlayın:

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

Bu örnek, [Oluşturucu Ekleme](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)kullanır. Ayrıca, bir ayarlayıcı yöntemi veya özelliği aracılığıyla bağımlılığı ayarladığınız *ayarlayıcı ekleme*özelliğini de kullanabilirsiniz.

Ancak artık, uygulamanız denetleyiciyi doğrudan oluşturmadığından bir sorun oluştu. Web API 'SI isteği yönlendirdiğinizde denetleyiciyi oluşturur ve Web API `IProductRepository`hakkında hiçbir şey bilmez. Bu, Web API bağımlılığı Çözümleyicisinin geldiği yerdir.

## <a name="the-web-api-dependency-resolver"></a>Web API bağımlılığı Çözümleyicisi

Web API 'SI, bağımlılıkları çözümlemek için **ıdependencyresolver** arabirimini tanımlar. Arabirimin tanımı şöyledir:

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

**IDependencyScope** arabirimi iki yönteme sahiptir:

- **GetService** bir türün bir örneğini oluşturur.
- **GetServices** , belirtilen türde nesnelerin bir koleksiyonunu oluşturur.

**Idependencyresolver** yöntemi **IDependencyScope** devralır ve **BeginScope** metodunu ekler. Bu öğreticide daha sonra kapsamlar hakkında konuşacağız.

Web API 'SI bir denetleyici örneği oluşturduğunda, önce denetleyici türünü geçirerek **ıdependencyresolver. GetService**öğesini çağırır. Bu genişletilebilirlik kancasını, denetleyiciyi oluşturmak ve tüm bağımlılıkları çözmek için kullanabilirsiniz. **GetService** null döndürürse, Web API 'si denetleyici sınıfında parametresiz bir oluşturucu arar.

## <a name="dependency-resolution-with-the-unity-container"></a>Unity kapsayıcısı ile bağımlılık çözümlemesi

Sıfırdan tamamlanmış bir **ıdependencyresolver** uygulaması yazabilseniz de, arabirim aslında Web API 'si ve var olan IOC kapsayıcıları arasında köprü olarak çalışacak şekilde tasarlanmıştır.

Bir IOC kapsayıcısı, bağımlılıkları yönetmekten sorumlu bir yazılım bileşenidir. Türleri kapsayıcıya kaydeder ve sonra nesneleri oluşturmak için kapsayıcıyı kullanın. Kapsayıcı, bağımlılık ilişkilerini otomatik olarak belirler. Birçok IOC kapsayıcısı ayrıca nesne ömrü ve kapsamı gibi şeyleri denetlemenize olanak tanır.

> [!NOTE]
> "IoC", bir çerçevenin uygulama koduna çağırdığı genel bir model olan "denetimin INVERSION" anlamına gelir. Bir IOC kapsayıcısı, nesnelerinizi sizin için oluşturur, bu da normal denetim akışını "tersine çevirir".

Bu öğreticide, Microsoft düzenleri &amp; uygulamalarından [Unity](https://msdn.microsoft.com/library/ff647202.aspx) kullanacağız. (Diğer popüler kitaplıklar, [role](http://www.castleproject.org/) [Spring.net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [neklemesine](http://www.ninject.org/)ve [StructureMap](http://structuremap.github.io/documentation/)içerir.) Unity 'yi yüklemek için NuGet paket yöneticisini kullanabilirsiniz. Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde aşağıdaki komutu yazın:

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

Bir Unity kapsayıcısını sarmalayan **ıdependencyresolver** 'ın bir uygulaması aşağıda verilmiştir.

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> **GetService** yöntemi bir türü çözümleyemezse **null**döndürmelidir. **GetServices** yöntemi bir türü çözümleyemezse boş bir koleksiyon nesnesi döndürmelidir. Bilinmeyen türler için özel durumlar oluşturmayın.

## <a name="configuring-the-dependency-resolver"></a>Bağımlılık çözümleyici 'yi yapılandırma

Genel **HttpConfiguration** nesnesinin **dependencyresolver** özelliğinde bağımlılık çözümleyici 'yi ayarlayın.

Aşağıdaki kod `IProductRepository` arabirimini Unity 'ye kaydeder ve sonra bir `UnityResolver`oluşturur.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>Bağımlılık kapsamı ve denetleyici ömrü

Denetleyiciler istek başına oluşturulur. **Idependencyresolver** nesne ömrünü yönetmek için bir *kapsamın*kavramını kullanır.

**HttpConfiguration** nesnesine eklenen bağımlılık Çözümleyicisi genel kapsama sahip. Web API 'SI bir denetleyici oluşturduğunda, **BeginScope**'u çağırır. Bu yöntem, bir alt kapsamı temsil eden bir **IDependencyScope** döndürür.

Daha sonra Web API 'SI, denetleyiciyi oluşturmak için alt kapsamdaki **GetService** 'i çağırır. İstek tamamlandığında, Web API 'SI alt kapsamda **Dispose** çağırır. Denetleyicinin bağımlılıklarını atmak için **Dispose** yöntemini kullanın.

**BeginScope** 'ı nasıl uygulayacağınızı IOC kapsayıcısına göre değişir. Unity için, kapsam bir alt kapsayıcıya karşılık gelir:

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

Çoğu IOC kapsayıcısının benzer eşdeğerleri vardır.
