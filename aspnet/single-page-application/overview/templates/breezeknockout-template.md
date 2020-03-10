---
uid: single-page-application/overview/templates/breezeknockout-template
title: Breeze/altını gizleme şablonu | Microsoft Docs
author: madskristensen
description: Breeze/altını gizleme tek sayfalı uygulama şablonu
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 5bb9ee8f758a25afa6baf3ccbaf7d5864754c7df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558193"
---
# <a name="breezeknockout-template"></a>Breeze/Knockout şablonu

[Mads Kristensen](https://github.com/madskristensen) tarafından

> Breeze/altını gizleme MVC şablonu Ward tarafından yazılmıştır
> 
> [Breeze/altını gizleme MVC şablonunu indirin](https://go.microsoft.com/fwlink/?LinkId=282649)

"Tek sayfalı uygulama" (SPA) duydunuz ve ne olduğunu merak etmiş olursunuz. Onunla ilgili bilgi edinebilirsiniz, sizin için bunu sizin için de yaşarsınız. Ancak bir örneği indirmek için zaman zamanı var mı? Visual Studio 'Yu aldıysanız, ASP.NET MVC 4 "Breeze/altını gizleme tek sayfalı uygulama" şablonu ile 60 saniyeden az bir örnek SPA çalıştırıyor ve çalışır.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>Breeze/altını gizleme SPA şablonu nedir?

Çoğu proje şablonu bir uygulama iskelet oluşturur. Kodunuzu ekleyerek ve sonunda çalışan bir uygulama sunarak bu kemiklerin üzerine buorsh koyabilirsiniz. Breeze/altını gizleme SPA şablonu farklı. Çalışmanız için örnek bir uygulama oluşturur. SPA uygulama tasarımını ve SPA oluşturma tekniklerinin çoğunu gösterir.

Breeze/altını gizleme şablonu, ASP.NET and Web Tools 2012,2 güncelleştirmesine dahil olan [altını gizleme Koutjs Spa şablonunda](../introduction/knockoutjs-template.md) bulunan bir çeşitçdır. Breeze SPA şablonu, aynı kullanıcı deneyimine sahip bir uygulama oluşturur, ancak veri yönetimi için Breeze kullanılarak farklı bir uygulamaya sahiptir.

Altını gizleme Koutjs SPA şablonu, bir basit uygulama için yeterli olan ham jQuery AJAX ile hizmet istekleri yapar. Ancak daha karmaşık uygulamalar daha yoğun veri yönetimi gereksinimlerine sahiptir. Örneğin, çoğu uygulama:

- Genişletilmiş bir Kullanıcı oturumu sırasında sunucuyu sorgulayın ve yeniden sorgulayın.
- Sorgu filtreleri, sıralama ve sayfalama ekleyin.
- Aynı verileri birden çok ekranda paylaşabilirsiniz.
- Değişiklikleri birçok nesneye biriktir ve bunları tek bir işlem olarak kaydedin.
- Kullanıcının değişiklikleri veritabanına kaydetmeden önce hataları düzeltebilmesi için istemcideki değişiklikleri doğrulayın.

BreezeJS kitaplığı sizin için bu seçim uygular, en çok bir uygulama mantığı ve Kullanıcı deneyimi geliştirmenize olanak sağlar.

[**Breeze**](http://www.breezejs.com/?utm_source=ms-spa) , JAVASCRIPT ve HTML 'de zengin veri uygulamaları oluşturmaya yönelik açık kaynaklı bir kitaplıktır. Bu, geçmişte tek başına masaüstü uygulamaları olarak teslim edilen uygulamalar türleridir.

Breeze/altını gizleme şablonu, bu ilk önemli adımı daha sağlam bir veri yönetimi altyapısına almanıza yardımcı olur. Outwardly Koutjs SPA şablonuyla özdeş olan örnek bir ToDo uygulaması oluşturur. İçinde, AJAX veri katmanını Breeze ile değiştirir, böylece iki yaklaşımı yan yana karşılaştırabilirsiniz. Tabii ki, bir Breeze uygulamasının potansiyelini çok dokunur. Ancak, Breeze 'ın nasıl çalıştığını ve bu geçişi yapmak için ne kadar küçük bir süre gerektiğini göreceksiniz.

Başlayalım.

## <a name="create-a-breezeknockout-template-project"></a>Kreeze/altını gizleme şablonu projesi oluşturma

Yukarıdaki Indir düğmesine tıklayarak şablonu indirip yükleyin. Şablon, Visual Studio uzantısı (VSıX) dosyası olarak paketlenmiştir. Visual Studio 'Yu yeniden başlatmanız gerekebilir.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi adlandırın ve **Tamam**' a tıklayın.

**Yeni proje** sihirbazında **Breeze gizleme Spa**' yı seçin.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

Hata ayıklama olmadan uygulamayı derlemek ve çalıştırmak için CTRL-F5 tuşlarına basın ya da hata ayıklama ile çalıştırmak için F5 'e basın.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

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

Doğrulama mantığı, istemci tarafında Breeze tarafından gerçekleştirilir. Sunucu modeli sınıflarında doğrulama öznitelikleri istemciye yayılır ve istemci sunucu ile iletişim kurmadan önce otomatik olarak yürütülür.

Ağ trafiğini gözden geçirin. Breeze bir hata algıladığında sunucuya hiçbir çağrı olmadığına dikkat edin. Her geçerli değişiklik, "/api/Todo/SaveChanges" için bir POST isteğiyle sonuçlandı. Breeze, değişiklikleri paketleyip Web API denetleyicisinin `SaveChanges` yöntemine tek bir istek olarak gönderir. Bu, her öğe için ayrı ayrı PUT, POST ve DELETE istekleri yapan altını gizleme Koutjs SPA şablonundan farklıdır.

## <a name="peek-inside"></a>İçine göz atın

Bu uygulamanın bir istemci tarafı ve sunucu tarafı vardır. İstemci tarafı yığını, bir HTML ve uygulama JavaScript modüllerinin ("uygulama" klasöründe) yanı sıra üçüncü taraf JavaScript kitaplıklarının ("betikler" klasöründe) bir birleşiminden oluşur.

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

Altını gizleme Koutjs SPA şablonunu araştırdıysanız bu, çok tanıdık görünmelidir. Mavi kutulara odaklanın. Kullanıcı arabirimi mimarisi, görünümün HTML Pencere öğelerinin görünüm-modelindeki destekleyici sunum kodundan düzgün şekilde ayrıldığı Model-View-ViewModel (MVVM) ' dir. Veri bağlama sistemi (Bu durumda altını gizleme), görünümü ve görünüm modelini koordine eder, böylece her biri intimate bilgisi olmadan işini gerçekleştirebilir.

Model Todo verilerini saklar. Modeldeki varlıklar, altını gizleme observable özellikleriyle Breeze tarafından oluşturulur, bu nedenle doğrudan görünümdeki Pencere öğelerinin içine bağlanabilir. Görünüm modeli, veri bağlamını Model varlıklarını elde etmek ve kaydetmek için sorar. Veri bağlamı çalışmanın çoğunu Breeze olarak devreder.

Sunucu tarafı yığını bazı geliştirici kodları ve üç prensibi .NET kitaplıklarından oluşur: Web API, Entity Framework ve Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

Temel mimari, altını gizleme Koutjs SPA şablonuyla aynıdır. Ancak, uygulama çok daha basittir: DTOs silinmişse ve Entity Framework ayrıntılarının çoğu Breeze.NET için temsilci olarak kaldırılmıştır.

## <a name="next-steps"></a>Sonraki Adımlar

Breeze Web sitesinde hem istemci hem de sunucu yığınları hakkında [kapsamlı tartışmayla](http://www.breezejs.com/spa-template?utm_source=ms-spa) Kılavuzlu kodu araştırmanızı öneririz.

İstemci tarafı sorgusuyla Breeze ile yürütmeyi deneyebilirsiniz; bazı filtreler ve sıralamalar ekleyin. Uçtan uca SPA geliştirmesi için daha iyi bir fikir almak üzere daha fazla model özelliği ve daha varlık ekleyebilirsiniz. Tasarımın bir sahibiyseniz, Todo özelliklerini ve bunları kendi kendinize yerleştirebilirsiniz.

Yakında bir sonraki Big Step: istemci tarafı ekranları ekleme ve bunlar arasında gezinme. Bu SPA şablonunu arka planda bırakarak [John Papa 'nın](https://github.com/johnpapa/HotTowel#readme "Etkin simgesi"), Breeze ve altını gizleme karışımına Durandal ekleyen bir daha fazla spa yığınına geçiş yapabilirsiniz.
