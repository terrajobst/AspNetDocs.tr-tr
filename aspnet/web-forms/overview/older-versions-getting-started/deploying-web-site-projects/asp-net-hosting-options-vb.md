---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-vb
title: ASP.NET barındırma seçenekleri (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET Web uygulamaları, genellikle yerel bir geliştirme ortamında tasarlanır, oluşturulur ve test edilir ve bir üretim ortamına dağıtılması gerekir...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 492f5ae2-bad7-4107-89a9-f04a9525dee7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-vb
msc.type: authoredcontent
ms.openlocfilehash: 4293114002aee15ddace1a3f19c240f35e6065f5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620754"
---
# <a name="aspnet-hosting-options-vb"></a>ASP.NET Barındırma Seçenekleri (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_vb.pdf)

> ASP.NET Web uygulamaları, genellikle yerel bir geliştirme ortamında tasarlanır, oluşturulur ve test edilir ve piyasaya çıkdıktan sonra bir üretim ortamına dağıtılması gerekir. Bu öğretici, dağıtım işlemine ilişkin üst düzey bir genel bakış sağlar ve bu öğretici serisine giriş görevi görür.

## <a name="introduction"></a>Giriş

Web uygulamaları tipik olarak yalnızca sitede çalışan programcılar tarafından erişilebilen bir geliştirme ortamında tasarlanır, oluşturulur ve test edilir. Uygulama yayınlanmaya hazırsa, siteye Internet 'teki herkes tarafından erişilebilen bir üretim ortamına taşınır. Bu dağıtım işlemi çeşitli güçlükleri tanıtır:

- Bir ASP.NET uygulamasının dağıtılabilmesi için bir üretim ortamının mevcut ve düzgün şekilde kurulması gerekir; Üstelik, üretim ortamının en son güvenlik düzeltme ekleriyle güncel tutulması gerekir.
- Doğru biçimlendirme dosyaları kümesi, kod dosyaları ve destek dosyaları geliştirme ortamından üretim ortamına kopyalanmalıdır. Veri odaklı uygulamalar için bu, veritabanı şemasının ve/veya verilerinin kopyalanmasını gerektirebilir.
- İki ortam arasında yapılandırma farklılıkları olabilir. Geliştirme ortamında kullanılan veritabanı bağlantı dizesi veya e-posta sunucusu büyük olasılıkla üretim ortamından farklı olacaktır. Ne kadar çok, uygulamanın davranışı ortama bağlı olabilir. Örneğin, geliştirmede bir hata oluştuğunda hatanın ayrıntıları ekranda görüntülenebilir, ancak üretimde bir hata oluştuğunda, bunun yerine Kullanıcı dostu bir hata sayfası görüntülenmelidir ve hata ayrıntıları geliştiricilere e-postayla gönderilebilir.

İlk sınamayı obviate için-üretim ortamını ayarlama ve sürdürme-birçok kişi ve işletme, üretim ortamlarını *Web barındırma sağlayıcılarına*dış olarak anlar. Web barındırma sağlayıcısı, sizin adınıza üretim ortamını yöneten bir şirkettir. Her biri değişen fiyatlar ve hizmet düzeylerine sahip olan sayaçsuz Web ana bilgisayarı sağlayıcıları vardır; Bu tür bir hizmet sağlayıcısını bulmaya yönelik ipuçları için "Web ana bilgisayar sağlayıcısı bulma" bölümüne bakın.

Bu, bir Web ana bilgisayar sağlayıcısı tarafından yönetilen bir üretim ortamına bir ASP.NET Web uygulaması dağıtmaya dahil olan adımlara bakamakta olan bir öğretici serisinin ilkisidir. Bu öğreticilerin kursunda, şunları inceleyeceğiz:

- Web ana bilgisayar sağlayıcısına dağıtılması gereken dosyalar.
- Dağıtım sürecini hızlandırma araçları.
- Bir veritabanını dağıtma.
- [SQL tabanlı üyelik ve rol sağlayıcısı](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)kullanan bir veritabanını dağıtmaya yönelik Ipuçları ve Web sitesi yönetim aracı 'nı bir üretim ortamında taklit etmenin yolları.
- Geliştirme sırasında yapılan değişikliklerle üretimde veritabanını sorunsuzca güncelleştirme stratejileri.
- Üretim sırasında oluşan hataları günlüğe kaydetme teknikleri ve bir hata oluştuğunda geliştiricilere bildirme yolları.

Bu öğreticilerin kısa olması ve işlem boyunca görsel olarak size yol göstermek için çok sayıda ekran görüntüsü ile adım adım yönergeler sağlaması gerekir. Bu ınaugural öğreticisi, ASP.NET dağıtım sürecine genel bir bakış ve bir Web barındırma sağlayıcısı bulma önerisi sağlar. Haydi başlayın!

## <a name="an-overview-of-the-aspnet-deployment-process"></a>ASP.NET dağıtım Işlemine genel bakış

Bir Nutshell 'de, bir ASP.NET uygulaması dağıtmak aşağıdaki üç adımdan oluşur:

1. Web uygulamasını, Web sunucusunu ve veritabanını üretim ortamında yapılandırın.
2. ASP.NET sayfalarını, kod dosyalarını, `Bin` klasöründeki derlemeleri ve CSS ve JavaScript dosyaları gibi HTML ile ilgili destek dosyalarını eşitler.
3. Veritabanı şemasını ve/veya verilerini eşitler.

Bir Web uygulamasının yapılandırma bilgileri genellikle `Web.config` dosyasında bulunur ve veritabanı bağlantı dizelerini, hata işleme ölçütlerini, URL yeniden yazma kurallarını ve e-posta sunucusu bilgilerini içerir. Bu bilgilerin geliştirilme aşamasındaki bir uygulama ve üretimde aynı uygulamaya göre farklı olması. Örneğin, bir uygulama geliştirirken, üretim veritabanına karşı test etmediğiniz için bir geliştirme veritabanını kullanmak en iyisidir. Sonuç olarak, veritabanı bağlantı dizeleri genellikle geliştirme ve üretim uygulamaları arasında farklılık gösterir. Bu farklılıklar nedeniyle, dağıtımın bir parçası Web uygulamasının yapılandırma bilgilerinde değişiklik yapmayı içerir.

Web uygulaması yapılandırma değişikliklerinin yanı sıra, 1. adım, Web sunucusu ve veritabanı için de yapılandırmayı sıraya alabilir. Örneğin, bir ASP.NET sayfası Web sunucusundaki bir dizinden dosya oluşturduğunda veya silerse, bu dosya sistemi değişikliklerine izin vermek için Web sunucusunun yapılandırılması gerekir. Benzer şekilde, veritabanına yapılması gereken izin veya kimlik doğrulama ayarları olabilir.

2\. adım, geliştirme ve üretim ortamları arasında temel ASP.NET sayfaları ve destek dosyaları kümesini eşitlemeyi içerir. İki ortam arasında eşitlenmesi gereken ASP.NET ile ilgili belirli dosyalar kümesi, Visual Studio 'da oluşturduğunuz projenin türüne bağlıdır ve bir sonraki öğreticide, <em>[hangi dosyaların dağıtılması gerektiğini belirleyen](determining-what-files-need-to-be-deployed-vb.md)</em>tartışmadır. Üçüncü ve dördüncü öğreticiler- <em>[SITENIZI FTP kullanarak dağıtma](deploying-your-site-using-an-ftp-client-vb.md)</em>ve <em>[sitenizi Visual Studio kullanarak dağıtma](deploying-your-site-using-visual-studio-vb.md)</em> -bu dosyaları eşitlemeye yönelik farklı araçları ve teknikleri inceleyin.

Veri tabanlı uygulamalar oluştururken genellikle iki veritabanı kullanılır: bir geliştirme ve diğeri üretimde. Geliştirme sırasında, geliştirme veritabanının şeması yeni tabloları, sütunları, saklı yordamları ve Tetikleyicileri içerecek şekilde değiştirilebilir veya var olan veritabanı nesnelerini kaldırmak veya yeniden adlandırmak için değiştirilebilir. Bu değişikliklerin yapıldığı zaman ve uygulamanın üretime dağıtıldığı zaman arasında geliştirme ve üretim veritabanları eşitlenmemiş olur. Dağıtım işlemi sırasında bu eşitleme işleminin düzeltilmesi gerekir. Bu sorunlar gelecekteki öğreticilerde incelenmeyecektir.

## <a name="finding-a-web-host-provider"></a>Web ana bilgisayar sağlayıcısı bulma

ASP.NET uygulamaları, .NET Framework ve Internet Information Services (IIS) yüklü olan herhangi bir Web sunucusuna dağıtılabilir. Internet 'e bir geniş bant bağlantınız olduğunu varsayarak ve gelen Web isteklerine izin vermek için yönlendiricinizin nasıl yapılandırılacağını öğrenmek için kişisel bilgisayarınızdan bir siteyi barındırabilirsiniz. Ayrıca, aynı zamanda intranetteki bir bilgisayardan bir site barındırabilirsiniz. Ancak, Bu öğreticilerin odaklanılması, Web sitesini bir Web ana bilgisayar sağlayıcısıyla barındırıyor.

> [!NOTE]
> [IIS](https://www.iis.net/) , Microsoft 'un kurumsal sınıf Web sunucusudur. Windows Server 2008 ve belirli Windows Vista sürümleri gibi Windows 'un ana olmayan sürümleriyle birlikte gelir. Visual Studio ASP.NET Development Web sunucusunu içerdiğinden, ASP.NET uygulamalarını bir geliştirme ortamında sunacak şekilde IIS yüklemeniz gerekmez. Ancak, ASP.NET Development Web sunucusu yalnızca yerel bağlantıları kabul eder ve bu nedenle üretim ortamında kullanılamaz.

Sitenizi bir Web ana bilgisayar sağlayıcısına dağıtabilmeniz için önce hangi şirkete iş yapacağına karar vermelisiniz. Market 'te sayaçsuz Web barındırma şirketleri vardır; "Web barındırma şirketi" araması 5.000.000 'den fazla sonuç döndürüyor. Sizin için doğru olanı nasıl bulabilirim? En sevdiğiniz arama altyapınız, [Tophosts](http://www.tophosts.com/) ve [Hostcritique](http://www.hostcritique.net/)gibi çeşitli barındırma hizmetlerini karşılaştıran ve kontrast sağlayan Web siteleri olduğu gibi iyi bir başlangıç olarak gerçekleşir. Ayrıca iş arkadaşlarınız ve iş arkadaşlarınız için herhangi bir öneri istenir; Ayrıca, [ASP.net forumlarında](https://forums.asp.net/) [barındırma açık forumundaki](https://forums.asp.net/158.aspx) önerileri de isteyebilirsiniz.

Web barındırma şirketleri, genellikle paylaşılan barındırma planları ve adanmış barındırma planları sunar. Paylaşılan barındırma ile tek bir Web sunucusu yüzlerce farklı Web sitesi değilse düzinelerce barındırır. Adanmış barındırma sayesinde, Şirket içinden sitenize ve sitenize hizmet veren bir bilgisayar kiralayın. Paylaşılan barındırma planı, ASP.NET sayfaları, Microsoft Access veritabanları, 5 GB disk alanı ve 100 GB aylık bant genişliği $9,95 trafiği için destek içerebilir. Başka bir paylaşılan barındırma planı, ASP.NET sayfaları için destek, Microsoft SQL Server 2008 veritabanı sunucusuna erişim, 10 GB disk alanı ve 250 GB aylık bant genişliği trafiği ile ayda $19,95. Adanmış barındırma planları genellikle ayda birkaç yüz doları maliyetlidir, ancak paylaşılan barındırma seçenekleriyle daha iyi performans ve daha fazla denetim sunar. Seçtiğiniz plan, bütçenize, Web sitenizin ne kadar trafik alacağını ve size tahmin ettiğiniz özellikleri bağlıdır.

Müşteri hizmeti ve hizmet kalitesi olan bir Web ana bilgisayar sağlayıcısı seçerken dikkat etmeniz gereken iki önemli nokta. Bir sorunuz veya yapılandırma sorununuz varsa, yanıt alınana kadar sorununuzun Web barındırma yardım masasına gönderilmesi ne kadar sürer? Şirketin Hizmetleri ne kadar güvenilir? Genellikle veritabanı kesintileri mı var? E-posta sunucusu ne sıklıkla çevrimdışı çalışıyor? Bir şirketten her zaman çalışma süresi ve müşteri hizmetleri ilkeleri hakkında sorgu bilgilerini sağlamasını isteyebilirsiniz, ancak çevrimiçi forumlar, haber grupları ve e-posta listesiları aracılığıyla yapabileceğiniz geçerli ve geçmiş müşterilerin geri bildirimini istemek daha fazla zor bir yoldur. .

> [!NOTE]
> Bazı Web barındırma şirketleri, işletmelerini .NET veya [lamba](http://en.wikipedia.org/wiki/LAMP_stack) (**L** ınux, **bir** Pache, **m** -SQL ve **P** Hp) gibi belirli bir teknoloji yığınına odakladığında, seçtiğiniz şirketin ASP.NET uygulamalarını barındırdığından emin olun. Ayrıca, uygulamanızı oluşturmak için kullandığınız ASP.NET sürümünü desteklediklerinden emin olmak için kontrol edin. Veri tabanlı bir uygulama oluşturuyorsanız, Web konağının kullandığınız veritabanı sunucusunu ve sürümü sağladığından emin olun.

## <a name="summary"></a>Özet

ASP.NET Web uygulamaları, genellikle yerel bir geliştirme ortamında tasarlanır, oluşturulur ve test edilmiştir. Sürüm yayın için hazırsa, bir üretim ortamına taşınır. ASP.NET Web sitelerini kişisel bilgisayarınızda veya şirketinizin içindeki sunucularda barındırmak mümkün olsa da birçok işletme ve kişi, barındırmayı bir Web ana bilgisayar sağlayıcısına aktarmak üzere tercih edilir.

Bu öğretici serisi, bir ASP.NET uygulamasını bir Web ana bilgisayar sağlayıcısına dağıtmaya yönelik adımları inceleyerek yaygın güçlükleri inceler. Bu öğreticide, ASP.NET dağıtım işlemine yönelik yüksek düzeyde bir genel bakış sunulmakta ve uygun bir Web ana bilgisayar sağlayıcısını bulmaya yönelik ipuçları sunulmuştur. Sonraki öğreticide, Web siteniz dağıtıldığında ASP.NET ile ilgili dosyaların üretim ortamına kopyalanması gerekir.

Programlamanın kutlu olsun!

### <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni bir Murphy idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](users-and-roles-on-the-production-website-cs.md)
> [İleri](determining-what-files-need-to-be-deployed-vb.md)
