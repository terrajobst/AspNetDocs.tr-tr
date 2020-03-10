---
uid: single-page-application/overview/templates/breezeangular-template
title: Breeze/angular şablonu | Microsoft Docs
author: madskristensen
description: Breeze/angular tek sayfalı uygulama şablonu
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578542"
---
# <a name="breezeangular-template"></a>Breeze/Angular şablonu

[Mads Kristensen](https://github.com/madskristensen) tarafından

> Breeze/angular MVC şablonu Ward tarafından yazılmıştır
> 
> [Breeze/angular MVC şablonunu indirin](https://go.microsoft.com/fwlink/?LinkId=286437)

[AngularJS](http://angularjs.org) , tek sayfa uygulamaları (maça 'lar) oluşturmak için Google 'dan alınan açık kaynaklı bir kitaplıktır. Veri bağlama, bağımlılık ekleme ve ekran yönetimi sağlar. Bunu [Breezejs](http://www.breezejs.com/?utm_source=ms-spa)ile birleştirin, veri modelleme ve veri yönetimi için başka bir açık kaynak kitaplık ve harıka bir HTML/JavaScript istemci uygulaması için önemli malzemeler vardır.

Breeze/angular SPA şablonu, ASP.NET and Web Tools 2012,2 güncelleştirmesine dahil olan [altını gizleme Koutjs Spa şablonunda](../introduction/knockoutjs-template.md) bulunan bir çeşitçdır. Visual Studio 'Yu aldıysanız, 60 saniyeden az bir süre içinde çalışır durumda bir örnek SPA görürsünüz.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

Outwardly, uygulama altını gizleme Koutjs SPA şablonuna benzer şekilde görünür. Ancak bu, aynı şekilde oldukça farklıdır. Altını gizleme şablonu veri bağlama ve veri erişimi için ham AJAX için gizleme kullanır. Breeze/angular şablonu veri bağlama için angular kullanır ve veri erişimi için Breeze kullanır. Bu kitaplıklar, sayfa gezintisi ve geçmişi de dahil olmak üzere ek yetenekler sağlar.

Uygulamanın hakkında sayfası aşağıda verilmiştir:

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

Bu sayfa, geçerli kullanıcı oturumu sırasında aşağıdakiler de dahil olmak üzere olayların bir günlüğünü görüntüler:

- Sayfalamayı. #2 ve #7 'de Todo denetleyicisi oluşturmayı aklınızda edin.
- Uzak sorgular (#3) ve yerel önbellek sorguları (#7).
- New (#5, #6) ve Modified (#4) varlıklarını kaydetme.
- Değişiklikler istemcide (#9) onaylanır, böylece Kullanıcı, değişiklikleri veritabanına kaydetmeden önce hataları düzeltebilir.

Bu şablonda araştırılacak, şunlar dahil olmak üzere daha fazla bilgi vardır:

- HTML görünüm şablonlarının dinamik yüklemesi.
- Angular aracılığıyla özel veri bağlama "yönergeler"
- Modülerlik ve bağımlılık ekleme.
- Sorgu filtreleri, sıralar, sayfalama, tahminler ve ilgili varlıkların dahil edilmesi.
- Birden çok ekranda veri paylaşma.
- Birden çok değişiklik tek bir işlem olarak kaydediliyor.
- Doğrulama kuralları sunucudan JavaScript istemcisine otomatik olarak yayılır.

Başlayalım.

## <a name="create-a-breezeangular-template-project"></a>Breeze/angular şablonu projesi oluşturma

Yukarıdaki Indir düğmesine tıklayarak şablonu indirip yükleyin. Şablon, Visual Studio uzantısı (VSıX) dosyası olarak paketlenmiştir. Visual Studio 'Yu yeniden başlatmanız gerekebilir.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi adlandırın ve **Tamam**' a tıklayın.

**Yeni proje** sihirbazında **Breeze angular Spa**' yı seçin.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

Hata ayıklama olmadan uygulamayı derlemek ve çalıştırmak için CTRL-F5 tuşlarına basın ya da hata ayıklama ile çalıştırmak için F5 'e basın.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

Uygulama ilk kez çalıştırıldığında, oturum açma ekranını görüntüler. "Kaydolun" bağlantısına ve yeni bir sayfaya göz atmak için bir Kullanıcı adı ve parola girebileceğiniz Görünüm ' e tıklayın. (Oturum açma ve kayıt sayfaları ASP.NET MVC kullanılarak oluşturulur.) Kayıt formunu gönderdiğinizde sunucu, hesabınız için iki öğeyle bir TodoList oluşturur. Daha sonra bunları bir sarı notta size gösterir.

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

Artık SPA 'nın aratada olursunuz. Todos işleme sırasında gördüğünüz ve deneyimle ilgili her şey, altını gizleme ve Breeze yardımıyla istemcisinde işlenir ve yönetilir. Uygulamayı kullanıcı olarak keşfet... Ancak geliştirici gözle. Ağ trafiğini yakalamak için tarayıcınızda geliştirici araçlarını kullanın. (Internet Explorer 'da: F12 tuşuna basın, ağ sekmesini seçin ve **Yakalamayı Başlat**' **a** tıklayın.) Şimdi şunları deneyin:

- Yeni bir Todo öğesi ekleyin.
- Etikete tıklayın ve Todo öğesi başlığını düzenleyin
- Öğenin yapıldığını işaretlemek için bir onay kutusu işaretleyin. TextBox 'ın devre dışı bırakıldığına dikkat edin, böylece başlık artık düzenlenebilir olmaz.
- Etiketin sağındaki ' x ' öğesine tıklayın. Öğe kaybolur ve veritabanından silinir.
- Başka bir öğe seçin ve başlığını temizleyin. Başlığın gerekli olduğu bir doğrulama hatası alırsınız. Kısa bir duraklama sonrasında, önceki başlık geri yüklenir.
- Daha dikkatli bir uzun başlık yazın. Başlığın çok uzun olduğu farklı bir doğrulama hatası alırsınız.
- "Yapılacaklar listesi ekle" düğmesine tıklayın. Önceki listenin solunda yeni bir liste görüntülenir.
- Gerekli ve uzunluk doğrulamaları tetikleyerek TodoList başlığıyla yürütün.
- Hata iletisini temizlemek için title metin kutusuna tıklayın.
- TodoList ve Todos ' ı silmek için sağ üst köşedeki daire içinde "x" simgesine tıklayın.
- Bu etkinliklerin günlüğünü görmek için sağ üstteki "hakkında" bağlantısına tıklayın.

Doğrulama mantığı, istemci tarafında Breeze tarafından gerçekleştirilir. Sunucu modeli sınıflarında doğrulama öznitelikleri istemciye yayılır ve istemci sunucu ile iletişim kurmadan önce otomatik olarak yürütülür.

Ağ trafiğini gözden geçirin. Breeze bir hata algıladığında sunucuya hiçbir çağrı olmadığına dikkat edin. Her geçerli değişiklik, "/api/Todo/SaveChanges" için bir POST isteğiyle sonuçlandı. Breeze, değişiklikleri paketleyip Web API denetleyicisinin `SaveChanges` yöntemine tek bir istek olarak gönderir. Bu, her öğe için ayrı ayrı PUT, POST ve DELETE istekleri yapan altını gizleme Koutjs SPA şablonundan farklıdır.

Ayrıca, TodoList ve hakkında sayfalar arasında geçiş yaparken ağ trafiği olmadığına dikkat edin. Bunun nedeni, sorgunun yerel Breeze önbelleğiyle kısıtlandığı anlamına gelir.

## <a name="peek-inside"></a>İçine göz atın

Bu uygulamanın bir istemci tarafı ve sunucu tarafı vardır. İstemci tarafı yığını, bir HTML ve uygulama JavaScript modüllerinin ("uygulama" klasöründe) yanı sıra üçüncü taraf JavaScript kitaplıklarının ("betikler" klasöründe) bir birleşiminden oluşur.

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

Kullanıcı arabirimi mimarisi, görünümlerin HTML pencere öğelerini denetleyicilerde bulunan destekleyici sunum kodundan ayırır. Angular veri bağlama sistemi, her birinin işini intimate bilgisi olmadan yapabilmesi için görünümleri ve denetleyicileri düzenler.

Denetleyici, veri bağlamını Model varlıklarını elde etmek ve kaydetmek için sorar. Veri bağlamı, iş öğesinin çoğunu, JSON sorgu sonuçlarından kendi kendine izleme modeli nesneleri oluşturan Breeze olarak destekler.

Sunucu tarafı yığını bazı geliştirici kodları ve üç prensibi .NET kitaplıklarından oluşur: Web API, Entity Framework ve Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

Temel mimari, altını gizleme Koutjs SPA şablonuyla aynıdır. Ancak, uygulama çok daha basittir: DTOs silinmişse ve Entity Framework ayrıntılarının çoğu Breeze.NET için temsilci olarak kaldırılmıştır.

## <a name="next-steps"></a>Sonraki Adımlar

Breeze Web sitesinde hem istemci hem de sunucu yığınları hakkında [kapsamlı tartışmayla](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) Kılavuzlu kodu araştırmanızı öneririz.

İstemci tarafı sorgusuyla Breeze ile yürütmeyi deneyebilirsiniz; bazı filtreler ve sıralamalar ekleyin. Uçtan uca SPA geliştirmesi için daha iyi bir fikir almak üzere daha fazla model özelliği ve daha varlık ekleyebilirsiniz. Tasarımın bir sahibiyseniz, Todo özelliklerini ve bunları kendi kendinize yerleştirebilirsiniz.

Kodlarım kutlu olsun!
