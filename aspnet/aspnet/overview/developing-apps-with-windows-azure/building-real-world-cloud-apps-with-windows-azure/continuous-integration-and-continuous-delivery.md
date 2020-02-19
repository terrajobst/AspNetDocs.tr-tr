---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: Sürekli tümleştirme ve sürekli teslim (Azure ile gerçek dünyada bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: cf3c65ef95528173eed3fb08984035b2512861c4
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457043"
---
# <a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>Sürekli tümleştirme ve sürekli teslim (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Önerilen ilk iki geliştirme işlemi deseni her şeyi ve [kaynak denetimi](source-control.md) [otomatikleştirin](automate-everything.md) ve üçüncü işlem deseni bunları birleştirir. Sürekli tümleştirme (CI), bir geliştiricinin kaynak depoya kod iade ettiğinde otomatik olarak tetiklendiği anlamına gelir. Sürekli teslim (CD) bu adımı bir adım ileri alır: derleme ve otomatik birim testleri başarılı olduktan sonra, uygulamayı otomatik olarak daha ayrıntılı test yapabileceğiniz bir ortama dağıtırsınız.

Bulut, yalnızca kullandığınız sürece ortam kaynakları için ödeme yaptığınız için bir test ortamının bakım maliyetini en aza indirmenize olanak sağlar. CD işleminiz, ihtiyacınız olduğunda test ortamını ayarlayabilir ve testi tamamladıktan sonra ortamı azaltabilirsiniz.

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>Sürekli tümleştirme ve sürekli teslim iş akışı

Genellikle geliştirme ve hazırlama ortamlarınıza sürekli teslim etmenizi öneririz. Çoğu ekip, Microsoft 'ta bile üretim dağıtımı için el ile gözden geçirme ve onay süreci gerektirir. Bir üretim dağıtımı için, geliştirme ekibinizdeki önemli kişilerin destek için kullanılabilir olduğu veya düşük trafikli dönemler sırasında olduğundan emin olmak isteyebilirsiniz. Ancak, geliştirme ve test ortamlarınızı tamamen otomatikleştirerek, tüm geliştiricinin yapması gereken bir değişikliği iade etme ve bir ortamın kabul testi için ayarlanmış olması gibi bir şey yoktur.

[Sürekli teslim hakkındaki bir Microsoft desenlerinden ve uygulamalardan](https://aka.ms/ReleasePipeline) oluşan aşağıdaki diyagramda tipik bir iş akışı gösterilmektedir. Özgün bağlamında tam boyuta bakmak için resme tıklayın.

[Sürekli teslim iş akışı ![](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>Bulut, uygun maliyetli CI ve CD 'yi nasıl sunar

Bu işlemlerin Azure 'da otomatikleştirilmesi kolaydır. Buluttaki her şeyi çalıştırdığınız için, derlemelerinizi veya test ortamlarınız için sunucu satın almanız veya yönetmeniz gerekmez. Ve testinizi üzerinde bir sunucunun kullanılabilir olmasını beklemeniz gerekmez. Yaptığınız her derleme sayesinde, otomasyon komut dosyanızı kullanarak Azure 'da bir test ortamı çalıştırabilir, kabul testleri veya daha ayrıntılı testler çalıştırabilir ve sonra da bunu koparın. Ayrıca, bu sunucuyu yalnızca 2 saat veya 8 saat veya bir gün boyunca çalıştırırsanız, yalnızca bir makinenin gerçekten çalıştığı zaman için ödeme yaptığınız için, bunun için ödeme yapmak zorunda olduğunuz para miktarı en az olur. Örneğin, BT uygulamasını onarmak için gereken ortam, ücretsiz düzeyden bir katmana giderseniz, saat başına yaklaşık 1 San maliyetindedir. Bir ay boyunca yalnızca bir saatte bir saat çalıştırırsanız, test ortamınız büyük olasılıkla başlangıçlarından satın aldığınız bir gözden daha düşük maliyetli olacaktır.

## <a name="azure-devops-services"></a>Azure DevOps Services 

Azure DevOps Services, dağıtıma planlamadan uygulama geliştirmeye yardımcı olacak birçok özellik sağlar.

- Hem git (dağıtılmış) hem de TFVC (Merkezi) kaynak denetimini destekler.
- Elastik derleme hizmeti sunar; bu, gerektiğinde dinamik olarak yapı sunucuları oluşturur ve bu işlem bittiğinde onları aşağı doğru alır. Birisi kaynak kodu değişikliklerini iade ettiğinde bir derlemeyi otomatik olarak başlatabilir ve çoğu zaman boşta olan kendi yapı sunucularınız için tahsis ve ödeme yapmanız gerekmez. Derleme hizmeti, belirli sayıda yapıyı aşmadığı sürece ücretsizdir. Yüksek hacimli derlemeler yapmayı düşünüyorsanız, ayrılmış derleme sunucuları için biraz daha fazla ödeme yapabilirsiniz.
- Azure 'a sürekli teslimi destekler.
- Otomatikleştirilmiş yük testini destekler. Yük testi bir bulut uygulaması için kritiktir ancak çok geç olana kadar genellikle ihmal edilir. Yük testi, uygulamayı üretime bırakmadan önce binlerce kullanıcı tarafından bir uygulamanın yoğun kullanımını taklit ederek, performans sorunlarını saptamanıza ve verimlilik iyileştirmenize olanak tanır.
- Bu, küçük Çevik takımlar için gerçek zamanlı iletişim ve işbirliği sağlayan takım odası işbirliğini destekler.
- Çevik proje yönetimini destekler.

Azure DevOps Services sürekli tümleştirme ve teslim özellikleri hakkında daha fazla bilgi için bkz. [Azure DevOps belgeleri](/azure/devops/index).

Bir aç-anahtar proje yönetimi, ekip işbirliği ve kaynak denetimi çözümü arıyorsanız, Azure DevOps Services kullanıma alma. [Azure DevOps Services](https://dev.azure.com/)kaydolun.

## <a name="summary"></a>Özet

İlk üç bulut geliştirme deseni, düşük zaman süresi ile tekrarlanabilir, güvenilir ve öngörülebilir bir geliştirme sürecinin nasıl uygulanacağı hakkında. [Sonraki bölümde](web-development-best-practices.md) mimari ve kodlama desenlerine bakmamız için başladık.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için bkz. [Azure App Service Web uygulaması dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-deploy/).

Ayrıca aşağıdaki kaynaklara bakın:

- [Team Foundation Server 2012 Ile yayın Işlem hattı oluşturuluyor](https://aka.ms/ReleasePipeline). E-kitap, uygulamalı laboratuvarlar ve Microsoft desenlerine ve uygulamalarına göre örnek kod, sürekli teslime yönelik ayrıntılı bir giriş sağlar. Visual Studio Laboratuvar Yönetimi ve Visual Studio Release Management kullanımını içerir.
- [ALM Ranger DevOps araçları ve Kılavuzu](https://aka.ms/vsarsolutions/). ALM derecelendirmeleri, TFS 2012 ' de DevOps &amp; Release Management kavramlarını öğrenmeye başlamak ve Tires 'yi başlatmak için harika bir yöntem olarak, *tfs 2012 ile*birlikte çalışma Işlem hattı oluşturma adlı &amp; modellerle Işbirliği Için DevOps ve örnek yardımcı çözümü ve pratik rehberlik 'yi kullanıma sunmuştur. Kılavuzda bir kez nasıl derleme yapılacağı ve birden çok ortama nasıl dağıtılacağı gösterilmektedir.
- [Visual Studio 2012 Ile sürekli teslim Için test etme](https://msdn.microsoft.com/library/jj159345.aspx). Microsoft düzenleri ve uygulamalarına göre E-kitap, otomatikleştirilmiş testlerin sürekli teslim ile nasıl tümleştirileceğini açıklar.
- [Windowsazuredeploymenttracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker). TFS 'den bir derlemeyi yakalamak, oluşturmak, paketlemek, DevOps rolündeki birisinin belirli yönlerini yapılandırmasına izin vermek ve Azure 'a göndermek için tasarlanan bir aracın kaynak kodu. Araç, işlemleri daha önce dağıtılan bir sürüme "geri alma" olanağı sağlamak için dağıtım sürecini izler. Araç, dış bağımlılıklara sahip değildir ve TFS API 'Leri ile Azure SDK kullanarak tek başına işlev görebilir.
- [Sürekli teslim: derleme, test ve Dağıtım Otomasyonu aracılığıyla güvenilir yazılım yayınları](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361). Jez ınsanla kitap.
- [Yayınlayın! üretime yönelik kullanıma yönelik yazılımları tasarlayın ve dağıtın](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213). Michael T. Nygard tarafından kitap.

> [!div class="step-by-step"]
> [Önceki](source-control.md)
> [İleri](web-development-best-practices.md)
