---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4,7 Web Forms ve Visual Studio 2017 ile çalışmaya başlama | Microsoft Docs
author: Erikre
description: Bu adım adım öğretici serisi, ASP.NET 4,7 ve Microsoft Visual Studio kullanarak bir ASP.NET Web Forms uygulaması oluşturmaya ilişkin temel bilgileri öğretir.
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568224"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>ASP.NET 4,5 Web Forms ve Visual Studio 2017 ile çalışmaya başlama

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

Bu öğretici serisinde, ASP.NET 4,5 ve Microsoft Visual Studio 2017 ile bir ASP.NET Web Forms uygulamasının nasıl oluşturulacağı gösterilmektedir. 

## <a name="introduction"></a>Giriş

Bu öğretici serisi, Visual Studio 2017 ve ASP.NET 4,5 kullanarak bir ASP.NET Web Forms uygulaması oluşturma konusunda size rehberlik eder. Çevrimiçi bir storefront Web sitesi olan **Wingtip Toys** adlı bir uygulama oluşturacaksınız. Seriler sırasında yeni ASP.NET 4,5 özellikleri vurgulanır.

### <a name="target-audience"></a>Hedef kitle

ASP.NET Web Forms yeni geliştiriciler, bu öğretici serisi için hedef kitledir.

Aşağıdaki alanlarda bazı bilgilere sahip olmanız gerekir:

- Nesne odaklı programlama (OOP) ve diller
- Web geliştirme (HTML, CSS, JavaScript)
- İlişkisel veritabanları
- N katmanlı mimari

Bu alanı gözden geçirmek için aşağıdaki içeriği kullanmayı göz önünde bulundurun:

- [Görsele BaşlarkenC#](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web geliştirme](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, php, jQuery](http://w3schools.com/)
- [İlişkisel veritabanı](http://en.wikipedia.org/wiki/Relational_database)
- [Çok katmanlı mimari](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>Uygulama özellikleri

Bu dizide sunulan ASP.NET Web form özellikleri şunlardır:

- Web uygulaması projesi (Web sitesi projesi değil)
- Web Forms
- Ana sayfalar, yapılandırma
- Yükleyebilirsiniz
- Entity Framework Code First, LocalDB
- İstek doğrulaması
- Kesin tür belirtilmiş veri denetimleri
- Model bağlama
- Veri Açıklamaları
- Değer sağlayıcıları
- SSL ve OAuth
- ASP.NET Identity, yapılandırma ve yetkilendirme
- Unobtrusive doğrulaması
- Yönlendirme
- ASP.NET Hata İşleme

### <a name="application-scenarios-and-tasks"></a>Uygulama senaryoları ve görevler

Öğretici serisi görevleri şunlardır:

- Yeni bir proje oluşturma, gözden geçirme ve çalıştırma
- Veritabanı yapısı oluşturma
- Veritabanını başlatma ve sağlama
- Kullanıcı arabirimini stillerle, grafiklerle ve ana sayfayla özelleştirme
- Sayfa ve gezinti ekleme
- Menü ayrıntılarını ve ürün verilerini görüntüleme
- Alışveriş sepeti oluşturma
- SSL ve OAuth desteği ekleme
- Ödeme yöntemi ekleme
- Uygulamaya yönetici rolü ve Kullanıcı ekleme
- Belirli sayfalara ve klasöre erişimi sınırlandırma
- Web uygulamasına bir dosya yükleme
- Giriş doğrulaması uygulama
- Web uygulaması için rotalar kaydetme
- Hata işleme ve hata günlüğü uygulama

## <a name="overview"></a>Genel bakış

Bu öğretici serisi, programlama kavramlarını bildiğiniz bir kişiye yöneliktir, ancak yeni ASP.NET Web Forms. Zaten ASP.NET Web Forms hakkında bilginiz varsa, bu seri yeni ASP.NET 4,5 özellikleri hakkında bilgi edinmenize yardımcı olmaya devam edebilir. Programlama kavramları ve ASP.NET Web Forms hakkında bilgi sahibi olan okuyucular için, ASP.NET Web sitesinin [Başlarken bölümünde sunulan](../../../index.md) ek Web Forms öğreticilere bakın.

Bu öğretici serisinde sunulan ASP.NET 4,5 aşağıdaki özellikleri içerir:

- Birçok ASP.NET Çerçevesi (Web Forms, MVC ve Web API) [için destek](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) sunan projeler oluşturmaya yönelik basit bir kullanıcı arabirimi.
- [Önyükleme](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), düzen, tema ve yanıt veren tasarım çerçevesi.
- [ASP.NET Identity](../../../../identity/index.md), tüm ASP.net çerçeveleri ile aynı ve IIS dışında Web barındırma yazılımıyla birlikte çalışarak yeni bir ASP.NET üyelik sistemidir.
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  Entity Framework bir güncelleştirme şunları sağlar:
  - Verileri türü kesin belirlenmiş nesneler olarak alma ve işleme
  - Verilere zaman uyumsuz olarak erişin
  - Geçici bağlantı hatalarını işleme
  - SQL deyimlerini günlüğe kaydet

Tüm ASP.NET 4,5 özellik listesi için, bkz. [Visual Studio 2013 Sürüm notları ASP.NET and Web Tools](../../../../visual-studio/overview/2013/release-notes.md).

### <a name="the-wingtip-toys-sample-application"></a>Wingtip Toys örnek uygulaması

Aşağıdaki ekran görüntüleri, bu öğretici serisinde oluşturduğunuz ASP.NET Web Forms uygulamasıdır. Uygulamayı Visual Studio 'da çalıştırdığınızda, aşağıdaki Web giriş sayfası görüntülenir.

![Wingtip Toys-varsayılan sayfa](introduction-and-overview/_static/image1.png)

Yeni bir kullanıcı olarak kaydedebilir veya var olan bir kullanıcı olarak oturum açabilirsiniz. En üstteki gezinmede, ürün kategorilerinin ve bu kullanıcıların ürünleriyle ilişkili bağlantılar bulunur.

**Ürünler**' i seçerseniz, kullanılabilir tüm ürünler görüntülenir. 

![Wingtip Toys-ürünler](introduction-and-overview/_static/image2.png)

Belirli bir ürünü seçerseniz ürün ayrıntıları görüntülenir.

![Wingtip Toys-ürün ayrıntıları](introduction-and-overview/_static/image3.png)

Bir kullanıcı olarak, Web Forms şablonu varsayılan işlevselliğiyle kaydedebilir ve oturum açabilirsiniz. Bu öğretici Ayrıca, mevcut bir Gmail hesabını kullanarak nasıl oturum bulunacağını açıklar. Ayrıca, veritabanından ürün eklemek ve kaldırmak için yönetici olarak oturum açabilirsiniz.

![Wingtip Toys-oturum aç](introduction-and-overview/_static/image4.png)

Kullanıcı olarak oturum açtıktan sonra, alışveriş sepetine ürün ekleyebilir ve PayPal ile kullanıma alabilirsiniz. Örnek uygulama, PayPal 'in geliştirici korumalı alanında çalışacak şekilde tasarlanmıştır. Gerçek para hareketi gerçekleşmez.

![Wingtip Toys-alışveriş sepeti](introduction-and-overview/_static/image5.png)

PayPal hesabı, siparişi ve ödeme bilgilerinizi onaylar.

![Wingtip Toys-PayPal](introduction-and-overview/_static/image6.png)

PayPal 'den döndükten sonra, siparişinizi gözden geçirebilir ve tamamlayabilirsiniz.

![Wingtip Toys-sipariş Incelemesi](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>Önkoşullar

Başlamadan önce, aşağıdaki yazılımın bilgisayarınızda yüklü olduğundan emin olun:

- [Microsoft Visual Studio 2017 veya Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).

.NET Framework otomatik olarak yüklenir.

Bu öğretici serisi 2017 Microsoft Visual Studio Community kullanır. Bu öğretici serisini tamamlayabilmeniz için ya da Microsoft Visual Studio 2017 kullanabilirsiniz.

Visual Studio hakkında aşağıdakileri göz önünde edin:

* Microsoft Visual Studio 2017 ve Microsoft Visual Studio Community 2017, bu öğretici serisinin tamamında *Visual Studio* olarak adlandırılır.

* Visual Studio 2017, zaten yüklü olan tüm eski sürümlerin yanına yüklenir. Önceki sürümlerde oluşturulan siteler, Visual Studio 2017 ' de açılabilir ve önceki sürümlerde açılmaya devam edebilir.

* Visual Studio 'Yu ilk kez başlattığınızda, *Web geliştirme* ayarlarını seçtiğiniz varsayılır. Daha fazla bilgi için bkz. [nasıl yapılır: Web geliştirme ortamı ayarlarını seçme](https://msdn.microsoft.com/library/ff521558.aspx).

Önkoşulları yükledikten sonra, bu öğretici serisinde sunulan Web projesini oluşturmaya başlamaya hazırsınız demektir.

## <a name="download-the-sample-application"></a>Örnek uygulamayı indirin:

 Tamamlanmış örnek uygulamayı dilediğiniz zaman MSDN örnekleri sitesinden indirebilirsiniz:

[ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) ile çalışmaya başlama 

 Bu indirme aşağıdaki öğelere sahiptir:

- *Wingtiptoys* klasöründeki örnek uygulama.
- *Wingtiptoys* klasöründeki *wingtiptoys-varlıklar* klasöründe örnek uygulamayı oluşturmak için kullanılan kaynaklar.

İndirme bir *. zip* dosyasıdır. Bu öğretici serisinin oluşturduğu tamamlanmış projeyi görmek için. zip dosyasındaki *C#* klasörü bulun ve seçin. Klasörünü, C# Visual Studio projeleriyle çalışmak için kullandığınız klasöre kaydedin. Varsayılan olarak, Visual Studio 2017 Projects klasörü:

<strong>C:\Users&#92;</strong>  <strong><em>&lt;Kullanıcı adı&gt;</em></strong> <strong>\source\repos</strong>

***C#*** Klasörü ***wingtiptoys***olarak yeniden adlandırın.

> [!NOTE]
> Projects klasörünüzde *wingtiptoys* adlı bir klasörünüz zaten varsa, *C#* klasörü *wingtiptoys*olarak yeniden adlandırmadan önce mevcut klasörü geçici olarak yeniden adlandırın.

Tamamlanmış projeyi çalıştırmak için *wingtiptoys* klasörünü açın ve *wingtiptoys. sln* dosyasına çift tıklayın. Visual Studio 2017 projeyi açar. Sonra, **Çözüm Gezgini** ' de *default. aspx* dosyasına sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin.

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>İçeriği gözden geçirmek için ASP.NET Web Forms bir test alın

Öğretici serisini tamamladıktan sonra, bilginizi test etmek ve temel kavramları zorlamak için bir test yapın. Her soru, ek rehberlik için bir açıklama ve bağlantılar sağlar.

* [ASP.NET Web Forms test](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>Öğretici desteği ve açıklamaları

Sorular ve açıklamalar için, [ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) örnek sayfasında yer alan Q ve A bölümünü kullanın.

Bu öğretici serisinin açıklamaları hoş geldiniz. Bu öğretici serisi güncelleniyorsa, iyileştirmeler için her çaba veya iyileştirmeleri göz önünde bulundurun.

Bir hata oluşursa, ilgili hata iletileri kafa çözme konusunda iyi bir açıklama olmadan kafa karıştırıcı olabilir. Yardım için [ASP.net forumlarını](https://forums.asp.net/)kontrol edebilirsiniz. Diğer bir iyi kaynak, [ASP.NET 4,5 Web Forms ve Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) örnek sayfasındaki Q ve bir bölümdür. 

> [!div class="step-by-step"]
> [Next](create-the-project.md)
