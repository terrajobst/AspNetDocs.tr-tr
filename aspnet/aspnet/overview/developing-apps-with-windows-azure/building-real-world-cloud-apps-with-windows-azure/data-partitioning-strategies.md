---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: Veri bölümleme stratejileri (Azure ile gerçek hayatta bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: 2f79b1f459aff3e81dab7ea7eb4ebf3f71084463
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585812"
---
# <a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a>Veri bölümleme stratejileri (Azure ile gerçek hayatta bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. Seriler hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Daha önce, Web sunucuları ekleyerek ve kaldırarak bir bulut uygulamasının Web katmanını ölçeklendirmenin ne kadar kolay olduğunu gördük. Ancak bunların hepsi aynı veri deposuna geçerse, uygulamanızın performans sorunu ön uca arka uca, veri katmanı da ölçeklenir. Bu bölümde, verileri birden çok ilişkisel veritabanına bölümleyerek veya ilişkisel veritabanı depolamayı diğer veri depolama seçenekleriyle birleştirerek veri katmanınızı ölçeklenebilir hale getirme konusuna bakacağız.

Bölümleme şemasının ayarlanması, daha önce bahsedilen aynı nedene göre en iyi şekilde yapılır: bir uygulama üretim aşamasında olduktan sonra veri depolama stratejinizi değiştirmek çok zordur. Farklı yaklaşımlar hakkında daha fazla bilgi sahibi olmanız durumunda uygulamanızın verileri ve veri erişim kodunu yeniden görüntülerken uygulamanız kilitlenirse veya uzun süre geçtiğinde bir "Twitter" geçirmenize gerek kalmaktan kaçınabilirsiniz.

## <a name="the-three-vs-of-data-storage"></a>Üç veri depolama alanı

Bölümleme stratejisi gerekip gerekmediğini ve ne olması gerektiğini belirlemek için verileriniz hakkında üç soruyu göz önünde bulundurun:

- Hacim: sonunda ne kadar veri depolayacaksınız? Birkaç gigabayt mı? Birkaç yüz gigabayt mı? Terabayt? Petabaytlarca?
- Hız: verilerinizin ne kadar büyüeceği hız nedir? Çok fazla veri oluşturmamayan bir iç uygulama mı? Müşterilerin resimleri ve videoları karşıya yüklemesini sağlayacak bir dış uygulama mı?
- Çeşitli: hangi veri türlerini depolayacaksınız? İlişkisel, görüntüler, anahtar-değer çiftleri, sosyal grafikler?

Çok miktarda hacim, hız veya çeşitli özellikler olacağını düşünüyorsanız, uygulamanızın büyüdükçe ne tür bölümleme şemasının etkili ve etkili bir şekilde ölçeklenebileceğini dikkatlice düşünmeniz ve herhangi bir performans sorunu yaşanmamasını sağlamak zorunda kalmazsınız.

Bölümlemeye yönelik temel olarak üç yaklaşım vardır:

- Dikey bölümleme
- Yatay bölümleme
- Karma bölümlendirme

## <a name="vertical-partitioning"></a>Dikey bölümleme

Dikey bağlantı noktası, tabloyu sütunlara göre bölmek gibidir: bir sütun kümesi bir veri deposuna gider ve başka bir sütun kümesi farklı bir veri deposuna gider.

Örneğin, uygulamamın görüntüler dahil olmak üzere insanlarla veri depoladığını varsayalım:

![Veri tablosu](data-partitioning-strategies/_static/image1.png)

Bu verileri bir tablo olarak temsil ettiğinizde ve verilerin farklı varicilerine baktığımızda, sol taraftaki üç sütunun ilişkisel bir veritabanı tarafından etkili bir şekilde depolanabilecek dize verilerine sahip olduğunu, sağdaki iki sütunun ise c 'nin temel aldığı bayt dizileri olduğunu görebilirsiniz. görüntü dosyalarından ası. İlişkisel bir veritabanındaki depolama görüntü dosyası verileri, verileri dosya sistemine kaydetmek istemediklerinden çok sayıda kişi olabilir. Gerekli veri birimlerini depolayan bir dosya sistemine sahip olmayabilir veya ayrı bir yedekleme ve geri yükleme sistemini yönetmek istemeiyor olabilir. Bu yaklaşım, şirket içi veritabanları ve bulut veritabanlarındaki küçük miktarlarda veri için iyi sonuç verir. Şirket içi ortamda, yalnızca DBA 'nın her şeyi ele geçirmesine olanak daha kolay olabilir.

Ancak, bir bulut veritabanında, depolama görece pahalıdır ve yüksek miktarda görüntü, veritabanının boyutunu verimli bir şekilde çalışabilecek limitlerin ötesinde büyütebilirler. Verileri dikey olarak bölümleyerek bu sorunları ele alabilir. Bu, veri tablonuzdaki her bir sütun için en uygun veri deposunu seçtiğiniz anlamına gelir. Bu örnek için en iyi şekilde çalışmayabilir dize verilerini bir ilişkisel veritabanına ve BLOB depolamadaki görüntülere yerleştirmeye yöneliktir.

![Dikey olarak bölümlenmiş veri tablosu](data-partitioning-strategies/_static/image2.png)

Dosya sunucularını ayarlama veya ilişkisel veritabanının dışında depolanan verilerin yedeklenmesini ve geri yüklenmesini yönetme konusunda endişelenmeniz olmadığından, görüntüleri bir veritabanı yerine blob depolamada depolamak, bulutta daha pratik bir şirket içi ortamdır. Bu, sizin için blob Storage hizmeti tarafından otomatik olarak gerçekleştirilir.

Bu, çözümü gidermeye uygulanan bölümlendirme yaklaşımına sahiptir ve [BLOB depolama](unstructured-blob-storage.md)bölümünde buna ilişkin koda bakacağız. Bu bölümleme şeması olmadan ve ortalama bir görüntü boyutu olan 3 megabayt varsayıldığında, BT uygulamasının yalnızca en fazla 150 gigabayt veritabanı boyutunu vurmadan 40.000 görev depolayabilmesini sağlayabilecektir. Görüntüler kaldırıldıktan sonra, veritabanı birçok görev için 10 kez veri saklayabilir; bir yatay bölümleme şeması uygulamayı düşünmek zorunda bırakmadan önce çok daha uzun bir süre izleyebilirsiniz. Uygulama ölçeklenirken, depolama gereksinimlerinizin toplu olarak çok pahalı BLOB depolama alanına gittiğinden, harcamalar daha yavaş büyütüyor.

## <a name="horizontal-partitioning-sharding"></a>Yatay bölümleme (parçalama)

Yatay bağlantı noktası, tabloyu satırlara göre bölmek gibidir: bir dizi satır bir veri deposuna gider ve başka bir satır kümesi farklı bir veri deposuna gider.

Aynı veri kümesi verildiğinde, farklı veritabanlarındaki farklı müşteri adı aralıklarını depolamak başka bir seçenektir.

![Veri tablosu yatay olarak bölümlenmiş](data-partitioning-strategies/_static/image3.png)

Etkin noktaları önlemek için verilerin eşit bir şekilde dağıtıldığından emin olmak için, parçalara ayırma düzeniniz hakkında çok dikkatli olmak istiyorsunuz. Son adın ilk harfini kullanan bu basit örnek, çok sayıda kişinin belirli ortak harflerle başlayan son adlara sahip olması nedeniyle bu gereksinimi karşılamaz. Tablo boyutu sınırlamalarından daha önceki bir deyişle, bazı veritabanlarının çok büyük olduğu, ancak küçük bir süre içinde kalacağından, bu işlem bekleyebilir.

Yatay bölümlemenin aşağı bir kısmı verilerin tamamında sorgu yapmak zor olabilir. Bu örnekte, uygulama tarafından depolanan tüm verileri almak için bir sorgunun en fazla 26 farklı veritabanından çizimi olması gerekir.

## <a name="hybrid-partitioning"></a>Karma bölümlendirme

Dikey ve yatay bölümleme birleştirebilirsiniz. Örneğin, örnek verilerde görüntüleri BLOB depolama alanında saklayabilir ve dize verilerini yatay olarak bölümleyebilirsiniz.

![Veri tablosu karma bölümlenmiş](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a>Üretim uygulamasını bölümlendirme

Kavramsal olarak, bölümleme şemasının nasıl çalıştığını görmek kolaydır, ancak herhangi bir bölümleme şeması kod karmaşıklığını artırır ve ilgilenmeniz gereken birçok yeni karmaşıklıkları tanıtır. Görüntüleri blob depolamaya taşıyorsanız, depolama hizmeti çalışmıyor ne olur? Blob güvenliğini nasıl işleyirsiniz? Veritabanı ve BLOB depolama eşitlenmemiş olduğunda ne olur? Parçalayorsanız, tüm veritabanlarına ilişkin sorgulamayı nasıl işleyeceğinizi istersiniz?

Bu karmaşıklıklar, üretime geçmeden önce bunları planlarken planlama yaptığınız sürece yönetilebilir. Bunu yapması istemeyen birçok kişi daha sonra sahip olurlar. Müşteri danışmanımız ekibi (CAT) ekibimiz, uygulamaları gerçekten büyük bir şekilde çalıştıkları müşterilerin bir ayda bir kez geçen ve bu planlamayı yapamadığımızdan, bu telefon görüşmelerini alır. Ve şöyle bir şey söyler: "yardım! Her şeyi tek bir veri deposuna yerleştirdim ve 45 gün içinde, boş alan kalmadı! " Veri deponuza nasıl erişileceğiyle ilgili çok sayıda iş mantığı varsa ve uygulamanızı kullanan müşteriler varsa, geçiş sırasında bir gün için uygun bir zaman kalmaz. Müşterinin verilerini bir süre boyunca bir süre boyunca bölümlendirmeye yardımcı olmak için hercuyalın çabalarıyla devam ediyoruz. Bu çok heyecan verici ve çok Kordur, ancak bunu önlemek istediğiniz bir şey değildir! Uygulamanın daha sonra büyümesi durumunda, bu ön ödemeli ve uygulamanızla tümleştirilmesi, yaşamınızı çok daha kolay hale getirir.

## <a name="summary"></a>Özet

Etkili bölümleme şeması, bulut uygulamanızın performans sorunlarını gidermek zorunda kalmadan buluttaki verilerin petabaytlarca ölçeklendirilmesini sağlayabilir. Uygulamayı şirket içi bir veri merkezinde çalıştırıyorsanız, büyük ölçekli makinelere veya kapsamlı altyapıya yönelik ön ödeme yapmak zorunda kalmazsınız. Bulutta, ihtiyacınız olan kapasiteyi artımlı olarak ekleyebilir ve yalnızca kullandığınızda kullandığınız kadar ödeyerek ödeme yaparsınız.

[Sonraki bölümde](unstructured-blob-storage.md) , BT uygulamasının, blob depolamada resimleri depolayarak dikey bölümleme uygulayıp uygulamadığını öğreneceğiz.

## <a name="resources"></a>Kaynaklar

Bölümleme stratejileri hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.

Belgelerle

- [Windows Azure Cloud Services büyük ölçekli hizmetleri tasarlamak Için En Iyi uygulamalar](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx). Simms ve Michael Thomassy ' i Işaretleyen Teknik İnceleme.
- [Microsoft düzenleri ve uygulamalar-bulut tasarım desenleri](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. veri bölümleme kılavuzu, parçalı model.

Videolar:

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz bölümden oluşan seriler. , Microsoft Müşteri danışmanlık ekibi (CAT) deneyiminden gerçek müşterilerle çekilen hikayelerle, yüksek düzeyde kavramlar ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. Bölüm 7 ' de bölümlendirme tartışmasına bakın.
- [Oluşturma büyük: Windows Azure müşterileri-bölüm ı 'den öğrenilen dersler](https://channel9.msdn.com/Events/Build/2012/3-029). Simms 'yi işaretlemek, bölüm düzenlerini, parçalama stratejilerini, parçalara ayırma ve SQL veritabanı federasyonlarını 19:49 adresinden başlayarak anlatmaktadır. Failsafe serisine benzer ancak daha fazla nasıl yapılır ayrıntılarına gider.

Örnek kod:

- [Windows Azure 'Da bulut hizmeti temelleri](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649). Parçalı bir veritabanını içeren örnek uygulama. Parça düzeninin bir açıklaması için, bkz. Windows Azure blogundan [RDBMS 'nin](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) parçaları.

> [!div class="step-by-step"]
> [Önceki](data-storage-options.md)
> [İleri](unstructured-blob-storage.md)
