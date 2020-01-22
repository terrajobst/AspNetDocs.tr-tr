---
uid: overview
title: ASP.NET genel bakış | Microsoft Docs
author: rick-anderson
description: Web siteleri, Web uygulamaları ve Web API 'Leri oluşturmaya yönelik ücretsiz bir çatı olan ASP.NET 'e giriş.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: aa4f627bca99f0a7ffbbb53ea45ebdcf0850fd89
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519368"
---
# <a name="aspnet-overview"></a>ASP.NET’e genel bakış

ASP.NET, HTML, CSS ve JavaScript kullanarak harika web siteleri ve Web uygulamaları oluşturmaya yönelik ücretsiz bir Web çerçevesidir. Web API 'Leri de oluşturabilir ve Web Yuvaları gibi gerçek zamanlı teknolojileri kullanabilirsiniz.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) , ASP.NET için bir alternatiftir.  [ASP.net ve ASP.NET Core arasından nasıl seçim yapılacağı hakkındaki kılavuza](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework)bakın.

## <a name="get-started"></a>Kullanmaya başlayın

Windows üzerinde ASP.NET için ücretsiz bir IDE olan [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019) Community Edition 'ı yükleyin.

## <a name="websites-and-web-applications"></a>Web siteleri ve Web uygulamaları

 ASP.NET, Web uygulamaları oluşturmak için üç çerçeve sunar: Web Forms, ASP.NET MVC ve ASP.NET Web Pages. Üç çerçeve de kararlı ve olgun ve bunlarla harika web uygulamaları oluşturabilirsiniz. Seçtiğiniz çerçeve ne olduğuna bakılmaksızın, ASP.NET her yerde tüm avantajları ve özellikleri elde edersiniz.

Her çerçeve, farklı bir geliştirme stilini hedefler. Seçtiğiniz bir, programlama varlıklarınızın birleşimine (bilgi, beceriler ve geliştirme deneyimi), oluşturmakta olduğunuz uygulamanın türüne ve rahat bir geliştirme yaklaşımına göre farklılık gösterir.

Aşağıda, her bir çerçeve ve aralarında nasıl seçim yapılacağı hakkında bazı fikirler hakkında genel bir bakış verilmiştir. Video girişini tercih ediyorsanız bkz. [ASP.net Ile web siteleri yapma](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) ve [Web araçları nedir?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | Ortamında deneyiminiz varsa | Geliştirme stili | Uzmanlık |
|-----------|----------------------|-----------------------------------------------------|----------------|
| Web Forms | Win Forms, WPF, .NET | HTML işaretlemesini kapsülleyen bir zengin denetim kitaplığı kullanarak hızlı geliştirme | Orta düzey, gelişmiş RAD |
| MVC       | Ruby on rayın, .NET  | HTML işaretleme, kod ve biçimlendirme ayrımı ve kolayca yazma testleri üzerinde tam denetim. Mobil ve tek sayfalı uygulamalar (SPA) için en iyi seçenektir. | Orta düzey, gelişmiş |
| Web Sayfaları  | Klasik ASP, PHP     | Aynı dosyada HTML biçimlendirme ve kodunuz birlikte | Yeni, orta düzey |

### <a name="web-forms"></a>Web Forms

ASP.NET Web Forms ile, tanıdık bir sürükle ve bırak, olay odaklı model kullanarak dinamik Web siteleri oluşturabilirsiniz. Tasarım yüzeyi ve yüzlerce denetim ve bileşen, veri erişimi ile hızlı bir şekilde gelişmiş, güçlü Kullanıcı arabirimi odaklı siteleri oluşturmanızı sağlar.

[Web Forms hakkında daha fazla bilgi edinin](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC, ilgilenilecek alanların temiz bir biçimde ayrılmasını sağlayan ve keyifli, kıvrak bir geliştirme deneyimi için size işaretleme üzerinde tam denetim imkanı sağlayan dinamik web siteler oluşturmak için kullanabileceğiniz güçlü, alışkanlık tabanlı bir yöntem sunar. ASP.NET MVC, en son web standartlarını kullanan gelişmiş uygulamalar oluşturmak için hızlı, TDD kullanımı kolay geliştirmeyi etkinleştiren birçok özellik içerir.

[MVC hakkında daha fazla bilgi edinin](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET Web Sayfaları

ASP.NET Web sayfaları ve Razor söz dizimi, dinamik Web içeriği oluşturmak için sunucu kodunu HTML ile birleştirmenin hızlı, ulaşılabilir ve hafif bir yolunu sağlar. Veritabanlarına bağlanın, video ekleyin, sosyal ağ sitelerine bağlanın ve en son web standartlarına uygun harika siteler oluşturmanıza yardımcı olan birçok daha fazla özelliği ekleyin.

[Web sayfaları hakkında daha fazla bilgi](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Web Forms, MVC ve Web sayfaları hakkında notlar

Üç ASP.NET Framework 'ün tamamı, .NET ve ASP.NET temel işlevlerini .NET Framework ve paylaşırlar. Örneğin, üç çerçeve, üyeliği temel alan bir oturum açma güvenlik modeli sunar ve her üç, isteği yönetmek, oturumları işlemek ve çekirdek ASP.NET işlevselliğinin bir parçası olan aynı tesislerin tümünü paylaşır.

Bunlara ek olarak, üç çerçeve tamamen bağımsızdır ve birini seçmek başka bir tane kullanmaz. Çerçeveler aynı Web uygulamasında bir arada olabildiğinden, farklı çerçeveler kullanılarak yazılmış uygulamaların ayrı ayrı bileşenlerini görmek yaygın olmayan bir durumdur. Örneğin, bir uygulamanın müşteriye yönelik bölümleri, biçimlendirmeyi iyileştirmek için MVC 'de geliştirildiğinde, veri erişimi ve yönetim bölümleri veri denetimlerinden ve basit veri erişimlerinden yararlanmak için Web Forms geliştirilmiştir.

## <a name="web-apis"></a>Web API'leri

ASP.NET Web API; tarayıcılar ve mobil cihazlar dahil olmak üzere, geniş bir yelpazedeki istemcilere erişen HTTP hizmetlerini oluşturmayı kolaylaştıran bir çerçevedir. ASP.NET Web API; .NET Framework üzerinde RESTful uygulamaları geliştirmek için ideal bir platformdur.

[Web API 'SI hakkında daha fazla bilgi](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>Gerçek zamanlı teknolojiler

ASP.NET SignalR, gerçek zamanlı web işlevlerinin geliştirilmesine daha kolay bir ASP.NET geliştiricileri için yeni bir kitaplıktır. SignalR sunucu ve istemci arasında çift yönlü iletişime olanak sağlar. Sunucular, kullanılabilir hale geldiğinde içerikleri anında bağlantılı istemcilere gönderebilir. SignalR, Web yuvalarını destekler ve eski tarayıcılar için diğer uyumlu tekniklere geri döner. SignalR bağlantı yönetimine yönelik API 'Leri (örneğin, bağlanma ve bağlantı kesme olayları), gruplandırma bağlantılarını ve yetkilendirmeyi içerir.

[SignalR hakkında daha fazla bilgi](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>Mobil uygulamalar ve siteler

ASP.NET, bir Web API arka ucu ile yerel mobil uygulamaları ve Twitter önyüklemesi gibi yanıt veren tasarım çerçevelerini kullanarak mobil web sitelerini de güçlendirin. Yerel bir mobil uygulama oluşturuyorsanız, uygulamanız için veri erişimi, kimlik doğrulama ve anında iletme bildirimlerini işlemek üzere JSON tabanlı bir Web API 'SI oluşturmak kolaydır. Yanıt veren bir mobil site oluşturuyorsanız, istediğiniz CSS çerçevesini veya açık kılavuz sistemini kullanabilir veya jQuery Mobile veya Sencha gibi güçlü bir mobil sistem ve PhoneGap ile harika mobil uygulamalar seçebilirsiniz.

[Mobil uygulama ve site geliştirme hakkında daha fazla bilgi edinin](mobile/overview.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>Tek sayfalı uygulamalar

ASP.NET tek sayfalı uygulama (SPA), HTML 5, CSS 3 ve JavaScript kullanarak önemli istemci tarafı etkileşimleri içeren uygulamalar oluşturmanıza yardımcı olur. Visual Studio, altını gizleme. js ve ASP.NET Web API 'SI kullanarak tek sayfalı uygulamalar oluşturmaya yönelik bir şablon içerir. Yerleşik SPA şablonuna ek olarak, topluluk tarafından oluşturulan SPA şablonları da indirilebilir.

[Tek sayfalı uygulama geliştirme hakkında daha fazla bilgi edinin](single-page-application/index.md)

## <a name="webhooks"></a>Web Kancaları

Web kancaları, Web API 'Leri ve SaaS hizmetlerini birbirine bağlama için basit bir yayın/alt model sağlayan hafif bir HTTP modelidir. Bir hizmette bir olay gerçekleştiğinde, kayıtlı abonelere HTTP POST isteği biçiminde bir bildirim gönderilir. POST isteği, alıcının uygun şekilde davranmasına olanak sağlayan olayla ilgili bilgiler içerir.

Web kancaları; Dropbox, GitHub, Instagram, MailChimp, PayPal, bolluk, Trello ve çok daha fazlası dahil olmak üzere çok sayıda hizmet tarafından sunulur. Örneğin, bir Web kancası bir dosyanın Dropbox 'ta değiştiğini veya bir kod değişikliğinin GitHub 'da kaydedilmiş olduğunu veya bir ödemenin PayPal 'de başlatıldığını ya da Trello 'da bir kartın oluşturulduğunu gösterebilir.

[Web kancaları hakkında daha fazla bilgi](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->
