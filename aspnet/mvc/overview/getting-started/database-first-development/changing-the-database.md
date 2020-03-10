---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'Öğretici: EF Database First için veritabanını ASP.NET MVC uygulamasıyla değiştirme'
description: Bu öğretici, veritabanı yapısına bir güncelleştirme yapma ve bu değişikliği Web uygulaması genelinde yayma konusunda odaklanır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616265"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a>Öğretici: EF Database First için veritabanını ASP.NET MVC uygulamasıyla değiştirme

MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz. Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir. Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.

Bu öğretici, veritabanı yapısına bir güncelleştirme yapma ve bu değişikliği Web uygulaması genelinde yayma konusunda odaklanır.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Sütun ekleme
> * Özelliği görünümlere ekleyin

## <a name="prerequisites"></a>Önkoşullar

* [Görünümler üretiliyor](generating-views.md)

## <a name="add-a-column"></a>Sütun ekleme

Veritabanınızdaki bir tablonun yapısını güncelleştirirseniz, yaptığınız değişikliğin veri modeline, görünümlere ve denetleyiciye yayıldığından emin olmanız gerekir.

Bu öğretici için öğrencinin orta adını kaydetmek üzere öğrenci tablosuna yeni bir sütun ekleyeceksiniz. Bu sütunu eklemek için veritabanı projesini açın ve öğrenci. SQL dosyasını açın. Tasarımcı ya da T-SQL kodu aracılığıyla, NVARCHAR (50) olan **MiddleName** adlı bir sütun ekleyın ve null değerlere izin verir.

Veritabanı projenizi (veya F5) başlatarak bu değişikliği yerel veritabanınıza dağıtın. Yeni alan tabloya eklenir. SQL Server Nesne Gezgini görmüyorsanız, bölmedeki Yenile düğmesine tıklayın.

![Yeni sütun göster](changing-the-database/_static/image2.png)

Yeni sütun veritabanı tablosunda var, ancak şu anda veri modeli sınıfında mevcut değil. Modeli yeni sütununuzu içerecek şekilde güncelleştirmeniz gerekir. **Modeller** klasöründe, model diyagramını göstermek Için **contosomodel. edmx** dosyasını açın. Öğrenci modelinin MiddleName özelliğini içermediğinden emin olun. Tasarım yüzeyinde herhangi bir yere sağ tıklayın ve **modeli veritabanından Güncelleştir**' i seçin.

Güncelleştirme sihirbazında **Yenile** sekmesini seçin ve ardından **tablo** > **dbo** > **öğrenci**' yi seçin. **Son**'a tıklayın.

Güncelleştirme işlemi tamamlandıktan sonra, veritabanı diyagramı yeni **MiddleName** özelliğini içerir. **Contosomodel. edmx** dosyasını kaydedin. Bu dosyayı, **Student.cs** sınıfına yayılacağı yeni özellik için kaydetmeniz gerekir. Artık veritabanını ve modeli güncelleştirmiş oldunuz.

Çözümü derleyin.

## <a name="add-the-property-to-the-views"></a>Özelliği görünümlere ekleyin

Ne yazık ki, görünümler yine de yeni özelliği içermiyor. Görünümleri güncelleştirmek için iki seçeneğiniz vardır. bir kez daha, öğrenci sınıfı için yapı iskelesi ekleyerek görünümleri yeniden oluşturabilir ya da yeni özelliği mevcut görünümlerinize el ile ekleyebilirsiniz. Bu öğreticide, otomatik olarak oluşturulan görünümlerde özelleştirilmiş bir değişiklik yapmadığından, yapı iskelesi 'ni yeniden ekleyeceksiniz. Görünümlerde değişiklikler yaptığınızda ve bu değişiklikleri kaybetmek istemediğinizde özelliği el ile eklemeyi düşünebilirsiniz.

Görünümlerin yeniden oluşturulduğundan emin olmak için, **Görünümler**altındaki **öğrenciler** klasörünü silin ve **studentscontroller**öğesini silin. Ardından, **denetleyiciler** klasörüne sağ tıklayın ve **öğrenci** modeli için yapı iskelesi ekleyin. Yine, denetleyiciyi **Studentscontroller**olarak adlandırın. **Add (Ekle)** seçeneğini belirleyin.

Çözümü yeniden oluşturun. Görünümler artık MiddleName özelliğini içerir.

![İkinci adı göster](changing-the-database/_static/image5.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Sütun eklendi
> * Özellik görünümlere eklendi

Bir öğrenci kaydıyla ilgili ayrıntıları göstermek için görünümü özelleştirmeyi öğrenmek üzere sonraki öğreticiye ilerleyin.
> [!div class="nextstepaction"]
> [Görünümü özelleştirme](customizing-a-view.md)