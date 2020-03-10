---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: Modeller ve denetleyiciler ekleme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557542"
---
# <a name="add-models-and-controllers"></a>Model ve Denetleyici Ekleme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

Bu bölümde, veritabanı varlıklarını tanımlayan model sınıfları ekleyeceksiniz. Daha sonra, bu varlıklarda CRUD işlemlerini gerçekleştiren Web API denetleyicileri ekleyeceksiniz.

## <a name="add-model-classes"></a>Model sınıfları Ekle

Bu öğreticide, Entity Framework (EF) için "Code First" yaklaşımını kullanarak veritabanını oluşturacağız. Code First, veritabanı tablolarına karşılık C# gelen SıNıFLARı yazdığınızda EF veritabanını oluşturur. (Daha fazla bilgi için bkz. [Entity Framework geliştirme yaklaşımları](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)

Etki alanı nesnelerimizi POCOs (düz eski CLR nesneleri) olarak tanımlayarak başladık. Aşağıdaki POCOs 'ları oluşturacağız:

- Yazar
- Book

Çözüm Gezgini, modeller klasörüne sağ tıklayın. **Ekle**' yi ve ardından **sınıf**' ı seçin. `Author`sınıfı adlandırın.

![](part-2/_static/image1.png)

Author.cs içindeki tüm ortak kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](part-2/samples/sample1.cs)]

Aşağıdaki kodla `Book`adlı başka bir sınıf ekleyin.

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework, veritabanı tabloları oluşturmak için bu modelleri kullanır. Her model için `Id` özelliği, veritabanı tablosunun birincil anahtar sütunu olur.

Kitap sınıfında `AuthorId`, `Author` tabloya bir yabancı anahtar tanımlar. (Basitlik için, her kitabın tek bir yazarı olduğunu kabul ediyorum.) Kitap sınıfı ayrıca ilgili `Author`bir gezinti özelliği içerir. Koddaki ilgili `Author` erişmek için gezinti özelliğini kullanabilirsiniz. Bölüm 4 ' te gezinti özellikleri hakkında daha fazla bilgi alıyorum ve [varlık Ilişkilerini işliyor](part-4.md).

## <a name="add-web-api-controllers"></a>Web API denetleyicileri ekleme

Bu bölümde, CRUD işlemlerini (oluşturma, okuma, güncelleştirme ve silme) destekleyen Web API denetleyicileri ekleyeceğiz. Denetleyiciler veritabanı katmanıyla iletişim kurmak için Entity Framework kullanacaktır.

Önce dosya denetleyicilerini/ValuesController. cs dosyasını silebilirsiniz. Bu dosya, örnek bir Web API denetleyicisi içerir, ancak bu öğretici için gerekli değildir.

![](part-2/_static/image2.png)

Sonra, projeyi derleyin. Web API 'SI yapı iskelesi, model sınıflarını bulmak için yansıma kullanır, bu nedenle derlenen derlemeye ihtiyaç duyuyor.

Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın. **Ekle**' yi ve ardından **Denetleyici**' yi seçin.

![](part-2/_static/image3.png)

**Yapı Iskelesi Ekle** iletişim kutusunda, "Entity Framework kullanarak eylemler Ile Web API 2 denetleyicisi" ni seçin. **Ekle**'yi tıklatın.

![](part-2/_static/image4.png)

**Denetleyici Ekle** iletişim kutusunda aşağıdakileri yapın:

1. **Model sınıfı** açılan menüsünde `Author` sınıfını seçin. (Açılan listede görmüyorsanız, projeyi derlediğinizden emin olun.)
2. "Zaman uyumsuz denetleyici eylemlerini kullan" öğesini işaretleyin.
3. Denetleyici adını &quot;AuthorsController&quot;olarak bırakın.
4. **Veri bağlam sınıfının**yanındaki artı (+) düğmesine tıklayın.

![](part-2/_static/image5.png)

**Yeni veri bağlamı** iletişim kutusunda varsayılan adı bırakın ve **Ekle**' ye tıklayın.

![](part-2/_static/image6.png)

**Denetleyici Ekle** iletişim kutusunu doldurmak için **Ekle** ' ye tıklayın. İletişim kutusu projenize iki sınıf ekler:

- `AuthorsController` bir Web API denetleyicisi tanımlar. Denetleyici, istemcilerin yazar listesinde CRUD işlemleri gerçekleştirmek için kullandığı REST API uygular.
- `BookServiceContext`, çalışma zamanında nesne nesnelerini yönetir, bu da nesneleri bir veritabanından verilerle doldurmayı, değişiklik izlemeyi ve kalıcı verileri veritabanına getirmeyi içerir. `DbContext`devralır.

![](part-2/_static/image7.png)

Bu noktada, projeyi yeniden derleyin. Artık `Book` varlıkları için bir API denetleyicisi eklemek üzere aynı adımları izleyin. Bu kez, model sınıfı için `Book` ' ı seçin ve veri bağlamı sınıfı için mevcut `BookServiceContext` sınıfını seçin. (Yeni bir veri bağlamı oluşturmayın.) Denetleyiciyi eklemek için **Ekle** ' ye tıklayın.

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [Önceki](part-1.md)
> [İleri](part-3.md)
