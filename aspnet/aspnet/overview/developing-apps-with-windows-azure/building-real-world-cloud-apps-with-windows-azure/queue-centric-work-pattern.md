---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: Kuyruk merkezli çalışma deseninin (Azure ile gerçek dünyada bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: 1177336b25479c06706227e5c8ff4d027cdaebb8
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456991"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>Kuyruk merkezli çalışma deseninin (Azure ile gerçek dünyada bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Daha önce, birden çok hizmet kullanmanın "bileşik" SLA ile sonuçlanabileceğini gördük ve uygulamanın etkin SLA 'Sı her SLA 'nın *ürünüdür* . Örneğin, BT uygulaması, Web sitelerini, depolamayı ve SQL veritabanını kullanır. Bu hizmetlerden herhangi biri başarısız olursa, uygulama kullanıcıya bir hata döndürür.

Önbelleğe alma, salt okuma içeriği için geçici hataların işlenmesi için iyi bir yoldur. Ancak uygulamanızın iş yapması gerekiyorsa ne olacak? Örneğin, Kullanıcı yeni bir çözüm BT görevi gönderdiğinde, uygulama görevi yalnızca önbelleğe ekleyemiyor. Uygulamanın, düzeltilmesi için bu görevi kalıcı bir veri deposuna yazması gerekir, bu nedenle işlenebilir.

Bu, kuyruk merkezli çalışma deseninin geldiği yerdir. Bu model, bir Web katmanı ve arka uç hizmeti arasında gevşek bir bağlayıcı sunar.

Düzenin nasıl çalıştığı aşağıda gösterilmiştir. Uygulama bir istek aldığında bir sıraya bir iş öğesi koyar ve yanıtı hemen döndürür. Sonra ayrı bir arka uç işlemi kuyruktan iş öğeleri çeker ve işi yapar.

Sıra merkezli çalışma deseninin kullanılması için yararlıdır:

- Zaman alan iş (yüksek gecikme süresi).
- Her zaman kullanılabilir olmayabilir bir dış hizmet gerektiren iş.
- Kaynak yoğunluklu (yüksek CPU) iş.
- Ücret dengelemeye (ani yük bursts 'ye tabi) faydalanabilir.

## <a name="reduced-latency"></a>Azaltılan gecikme

Kuyruklar, zaman alan iş yaptığınız her zaman faydalıdır. Bir görev birkaç saniye veya daha uzun sürerse, son kullanıcıyı engellemek yerine iş öğesini bir kuyruğa koyun. "Bu BT üzerinde çalıştık" kullanıcısını söyleyin ve sonra görevi arka planda işlemek için bir kuyruk dinleyicisi kullanın.

Örneğin, bir çevrimiçi satıcıdan bir şey satın aldığınızda, Web sitesi siparişinizi hemen onaylar. Ancak bu, bilgileriniz zaten teslim edilen bir kamyonun içinde olduğu anlamına gelmez. Bir kuyruğa görev yerleştirirler ve arka planda kredi denetimini yapıyor, öğelerinizi teslim için hazırlamakta ve benzeri bir şekilde yapılır.

Kısa gecikme süresine sahip senaryolar için, uçtan uca toplam süre, görevi zaman uyumlu olarak yapmakla karşılaştırıldığında daha uzun bir sıra kullanıyor olabilir. Öte yandan, diğer avantajlar da bu dezavantaja aykırı olabilir.

## <a name="increased-reliability"></a>Daha fazla güvenilirlik

Şimdiye kadar yaptığımız bir çözüm olan sürümde, Web ön ucu SQL veritabanı arka ucu ile sıkı bir şekilde bağlanmış. SQL veritabanı hizmeti kullanılamıyorsa, Kullanıcı bir hata alır. Denemeler işe çalışmadıysanız (yani hata geçicidir), yapabileceğiniz tek şey bir hata gösterir ve kullanıcıdan daha sonra tekrar denemesini ister.

![SQL veritabanı arka ucu başarısız olduğunda Web ön ucunun başarısız olduğunu gösteren diyagram](queue-centric-work-pattern/_static/image1.png)

Kuyrukları kullanarak, bir Kullanıcı bir düzelme görevi gönderdiğinde, uygulama sıraya bir ileti yazar. İleti yükü görevin [JSON](http://json.org/) gösterimidir. İleti sıraya yazıldığı anda, uygulama döndürülür ve anında kullanıcıya başarılı bir ileti gösterir.

SQL veritabanı veya kuyruk dinleyicisi gibi arka uç hizmetlerinden herhangi biri, çevrimdışı çalış, kullanıcılar yeni bir çözüm BT görevi göndermeye devam edebilir. Arka uç hizmetleri yeniden kullanılabilir olana kadar iletiler de sıraya alınır. Bu noktada, arka uç hizmetleri biriktirme listesini yakalar.

![Bir SQL veritabanı hatası olduğunda Web ön ucunun işlevine devam eden diyagram](queue-centric-work-pattern/_static/image2.png)

Üstelik, artık ön ucun dayanıklılığı hakkında endişelenmeden daha fazla arka uç mantığı ekleyebilirsiniz. Örneğin, her yeni bir düzelme atandığında Sahibe bir e-posta veya SMS iletisi göndermek isteyebilirsiniz. E-posta veya SMS hizmeti kullanılamaz hale gelirse, diğer her şeyi işleyebilir ve e-posta/SMS iletileri göndermek için ayrı bir kuyruğa bir ileti koyabilirsiniz.

Daha önce geçerli SLA Web Apps &times; depolama &times; SQL veritabanı =% 99,7 ' dir. (Bkz. devam [etmek Için tasarım](design-to-survive-failures.md).)

Uygulamayı bir kuyruğu kullanacak şekilde değiştirdiğimiz zaman Web ön ucu,% 99,8 bileşik SLA 'Sı için yalnızca Web Apps ve depolamaya bağlıdır. (Kuyrukların Azure depolama hizmeti 'nin bir parçası olduğunu ve bu nedenle BLOB depolama ile aynı SLA 'ya dahil edileceğini unutmayın.)

% 99,8 ' den daha da ihtiyacınız varsa iki farklı bölgede iki kuyruk oluşturabilirsiniz. Birincil, diğeri ise ikincil olarak belirleyin. Birincil sıra kullanılamıyorsa, uygulamanızda ikincil sıraya yük devreder. Her ikisinin de aynı anda kullanılamaz olma olasılığı çok küçüktür.

## <a name="rate-leveling-and-independent-scaling"></a>Hız seviyelendirme ve bağımsız ölçekleme

Kuyruklar Ayrıca *hız seviyelendirme* veya *Yük Dengeleme*adlı bir şey için de kullanışlıdır.

Web Apps genellikle trafikte ani artışlarıyla saldırılarına açıktır. Otomatik ölçeklendirmeyi, artırılmış Web trafiğini işlemek üzere otomatik olarak Web sunucuları eklemek için kullanabilirsiniz, ancak otomatik ölçeklendirme, yükteki ani artış artışlarını işlemek için yeterince hızlı bir şekilde tepki sağlayamayabilir. Web sunucuları bir kuyruğa ileti yazarak yapması gereken bazı işleri devretebilirler, daha fazla trafiği işleyebilir. Ardından arka uç hizmeti kuyruktan iletileri okuyabilir ve bunları işleyebilir. Gelen yük arttıkça kuyruğun derinliği büyür veya küçülecektir.

Zaman tüketen çalışmanın büyük bir bölümü, arka uç hizmetine yüklendiğinde, Web katmanı trafikte ani ani artışlar daha kolay bir şekilde yanıt verebilir. Ve verilen herhangi bir trafik miktarı daha az Web sunucusu tarafından işlenebildiğinden para tasarrufu yapabilirsiniz.

Web katmanı ve arka uç hizmetini bağımsız olarak ölçekleyebilirsiniz. Örneğin, üç Web sunucusuna ihtiyacınız vardır ancak yalnızca bir sunucu işleme kuyruğu iletileri gerekebilir. Veya arka planda yoğun işlem gücü olan bir görev çalıştırıyorsanız, daha fazla arka uç sunucusuna ihtiyacınız vardır.

![](queue-centric-work-pattern/_static/image3.png)

Otomatik ölçeklendirme, arka uç hizmetleriyle ve Web katmanıyla birlikte çalışmaktadır. Arka uç VM 'lerinin CPU kullanımına göre kuyruktaki görevleri işleyen VM 'lerin sayısını ölçeklendirebilir veya azaltabilirsiniz. Ya da bir kuyruktaki öğe sayısına göre otomatik ölçeklendirme yapabilirsiniz. Örneğin, otomatik ölçeklendirmeyi sıraya göre 10 ' dan fazla öğe tutmaya çalışmak üzere söyleyebilirsiniz. Kuyrukta 10 ' dan fazla öğe varsa, otomatik ölçeklendirme VM 'Ler ekler. Bunları yakalarsa, otomatik ölçeklendirme ek VM 'Leri kapatır.

## <a name="adding-queues-to-the-fix-it-application"></a>Onarım BT uygulamasına kuyruklar ekleniyor

Sıra deseninin uygulanması için, çözümü onarma uygulamasında iki değişiklik yapmanız gerekir.

- Bir Kullanıcı yeni bir bu BT BT görevini gönderdiğinde, görevi veritabanına yazmak yerine sıraya koyun.
- Kuyruktaki iletileri işleyen bir arka uç hizmeti oluşturun.

Kuyruk için [Azure kuyruk depolama hizmetini](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/)kullanacağız. Başka bir seçenek [Azure Service Bus](https://docs.microsoft.com/azure/service-bus/)kullanmaktır.

Hangi kuyruk hizmetinin kullanılacağına karar vermek için, uygulamanızın kuyruktaki iletileri nasıl gönderebilmesi ve alabilmesi gerektiğini göz önünde bulundurun:

- Kurduğuna üreticileri ve rekabet Tüketicileriniz varsa, Azure kuyruk depolama hizmeti 'ni kullanmayı düşünün. "Cooperating üreticileri", bir kuyruğa ileti ekleyen birden çok işlem anlamına gelir. "Rekabet tüketicileri", birden çok işlemin onları işlemek için sıraya çekdikleri, ancak verilen tüm iletiler yalnızca bir "tüketici" tarafından işlenebileceği anlamına gelir. Tek bir kuyruk ile alabilmeniz için daha fazla işleme ihtiyacınız varsa, ek sıralar ve/veya ek depolama hesapları kullanın.
- Bir [Yayımlama/abonelik modeline](http://en.wikipedia.org/wiki/Publish/subscribe)ihtiyacınız varsa Azure Service Bus kuyrukları kullanmayı göz önünde bulundurun.

BT BT uygulaması, kurduğuna üreticileri ve rakip tüketiciler modeline uyar.

Uygulamanın kullanılabilirliği başka bir noktadır. Kuyruk depolama hizmeti, BLOB depolama için kullandığımız aynı hizmetin bir parçasıdır, bu nedenle kullanım için SLA 'da hiçbir etkisi olmaz. Azure Service Bus kendi SLA 'Sı olan ayrı bir hizmettir. Service Bus kuyrukları kullandığımızda, ek bir SLA yüzdesi olarak çarpanımızın olması gerekir ve kompozit SLA 'Sı daha düşüktür. Bir kuyruk hizmeti seçerken tercih ettiğiniz uygulamanın kullanılabilirliği üzerinde etkisini anladığınızdan emin olun. Daha fazla bilgi için [kaynaklar](#resources) bölümüne bakın.

## <a name="creating-queue-messages"></a>Sıra Iletileri oluşturma

Bir onarma BT görevini Kuyruğa koymak için Web ön ucu aşağıdaki adımları gerçekleştirir:

1. [Cloudqueueclient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx) örneği oluşturun. `CloudQueueClient` örneği, istekleri kuyruk hizmetine göre yürütmek için kullanılır.
2. Henüz yoksa kuyruğu oluşturun.
3. BT BT görevini serileştirme görevi.
4. İletiyi kuyruğa koymak için [Cloudqueue. AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx) çağrısı yapın.

Bu işi yeni bir `FixItQueueManager` sınıfının Oluşturucusu ve `SendMessageAsync` yönteminde yapacağız.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

Burada, [JSON.net](https://github.com/JamesNK/Newtonsoft.Json) kitaplığını kullanarak FIXIT 'i JSON biçimine serileştiriyoruz. Tercih ettiğiniz serileştirme yaklaşımını kullanabilirsiniz. JSON, XML 'den daha az ayrıntılarken insanlar tarafından okunabilen avantajın avantajlarından yararlanır.

Üretim-kalite kodu hata işleme mantığı ekler, veritabanı kullanılamaz hale gelirse duraklatıp daha temiz bir şekilde işleyebilir, uygulama başlatma üzerinde kuyruğu oluşturabilir ve "[Poison" iletilerini](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx)yönetebilir. (Zararlı bir ileti, bazı nedenlerle işlenemeyen bir iletidir. Çalışan rolünün sürekli olarak onları işlemeye çalıştığı, başarısız, yeniden deneme, başarısız, vb. gibi, zarar iletilerinin sırada oturmasını istemezsiniz.

Ön uç MVC uygulamasında yeni bir görev oluşturan kodu güncelleştirmemiz gerekir. Görevi depoya koymak yerine yukarıda gösterilen `SendMessageAsync` yöntemi çağırın.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>Sıra Iletilerini işleme

Kuyruktaki iletileri işlemek için bir arka uç hizmeti oluşturacağız. Arka uç hizmeti aşağıdaki adımları gerçekleştiren sonsuz bir döngü çalıştırır:

1. Sıradaki bir sonraki iletiyi alın.
2. İletiyi bir onarma görevine serisini kaldırma.
3. Veritabanına düzeltilme görevini yazın.

Arka uç hizmetini barındırmak için *çalışan rolü*Içeren bir Azure bulut hizmeti oluşturacağız. Bir çalışan rolü, arka uç işlemeyi gerçekleştiren bir veya daha fazla VM 'den oluşur. Bu VM 'lerde çalışan kod, kullanılabilir hale geldiğinde kuyruktan ileti çeker. Her ileti için, JSON yükünün serisini çıkardık ve Web katmanında daha önce kullandığımız aynı depoyu kullanarak veritabanına olan bir IT BT görevi varlığının örneğini yazacak.

Aşağıdaki adımlarda, standart bir Web projesi olan bir çözüme bir çalışan rolü projesinin nasıl ekleneceği gösterilmektedir. Bu adımlar, indirebileceğiniz BT BT projesinde zaten yapıldı.

İlk olarak Visual Studio çözümüne bir bulut hizmeti projesi ekleyin. Çözüme sağ tıklayın ve **Ekle**' yi ve ardından **Yeni proje**' yi seçin. Sol bölmede, **görsel C#**  ' i genişletin ve **bulut**' u seçin.

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

**Yeni Azure bulut hizmeti** iletişim kutusunda sol bölmedeki **görsel C#**  düğümünü genişletin. **Çalışan rolü** ' nü seçin ve sağ ok simgesine tıklayın.

![](queue-centric-work-pattern/_static/image6.png)

(Ayrıca, bir *Web rolü*de ekleyebildiğinize dikkat edin. Bu çözümü Azure Web sitesinde çalıştırmak yerine, bu ön ucu aynı bulut hizmetinde çalıştırabiliriz. Bu, ön uç ve arka uç arasında bağlantıları koordine etmek daha kolay hale getirmek için bazı avantajlar içerir. Ancak, bu tanıtımı basit tutmak için ön ucu bir Azure App Service Web uygulamasında tutuyoruz ve yalnızca bir bulut hizmetinde arka ucu çalıştırıyorsunuz.)

Çalışan rolüne varsayılan bir ad atanır. Adı değiştirmek için, fareyi sağ bölmedeki çalışan rolünün üzerine getirin ve ardından kurşun kalem simgesine tıklayın.

![](queue-centric-work-pattern/_static/image7.png)

İletişim kutusunu doldurmak için **Tamam** ' ı tıklatın. Bu, Visual Studio çözümüne iki proje ekler.

- yapılandırma bilgileri de dahil olmak üzere bulut hizmetini tanımlayan bir Azure projesi.
- Çalışan rolünü tanımlayan bir çalışan rolü projesi.

![](queue-centric-work-pattern/_static/image8.png)

Daha fazla bilgi için bkz [. Visual Studio Ile Azure projesi oluşturma.](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)

Çalışan rolü içinde, daha önce görtiğimiz `FixItQueueManager` sınıfının `ProcessMessageAsync` yöntemini çağırarak iletiler için yoklama yaptık.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

`ProcessMessagesAsync` yöntemi, bekleyen bir ileti olup olmadığını denetler. Bir varsa, iletiyi bir `FixItTask` varlığına serileştirir ve varlığı veritabanına kaydeder. Sıra boş olana kadar döngü döngüleri.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

Kuyruk iletilerinin yoklanması küçük bir işlem ücreti doğurur, bu nedenle işlenmek üzere bekleyen bir ileti olmadığında çalışan rolünün `RunAsync` yöntemi, `Task.Delay(1000)`çağırarak tekrar yoklamadan önce bir saniye bekler.

Bir Web projesinde, IIS sınırlı bir iş parçacığı havuzunu yönettiği için zaman uyumsuz kod ekleme performansı otomatik olarak iyileştirebilir. Bu, bir çalışan rolü projesindeki bu durum değildir. Çalışan rolünün ölçeklenebilirliğini geliştirmek için, [paralel programlama](https://msdn.microsoft.com/library/ff963553.aspx)uygulamak için çok iş parçacıklı kod yazabilir veya zaman uyumsuz kod kullanabilirsiniz. Örnek, paralel programlama uygulamaz, ancak paralel programlama uygulayabilmeniz için kodun zaman uyumsuz hale getirme şeklini gösterir.

## <a name="summary"></a>Özet

Bu bölümde, kuyruk merkezli iş modelini uygulayarak uygulamanın yanıt verme hızını, güvenilirliğini ve ölçeklenebilirliğini nasıl geliştirebileceğinizi gördünüz.

Bu, bu e-kitapta açıklanan 13 desenin en son idir, ancak başarılı bulut uygulamaları oluşturmanıza yardımcı olabilecek birçok farklı model ve uygulama vardır. [Son bölüm](more-patterns-and-guidance.md) , bu 13 desenlerinde kapsanmayan konuların kaynaklarına bağlantılar sağlar.

<a id="resources"></a>
## <a name="resources"></a>Kaynaklar

Kuyruklar hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın.

Belgelerle

- [Microsoft Azure depolama kuyrukları Bölüm 1:](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-storage-queues-part-1-getting-started/)Başlarken. Roman Schacherl makalesini okuyun.
- [Arka plan görevleri yürütülüyor](https://msdn.microsoft.com/library/ff803365.aspx), uygulama taşıma 5. bölüm, Microsoft desenlerinden ve uygulamalardan [üçüncü sürüm](https://msdn.microsoft.com/library/ff728592.aspx) . (Özellikle, ["Azure depolama kuyrukları kullanma"](https://msdn.microsoft.com/library/ff803365.aspx#sec7)bölümü.)
- [Azure 'Daki sıra tabanlı mesajlaşma çözümlerinin ölçeklenebilirliğini ve maliyet verimliliğini en üst düzeye çıkarmak Için En Iyi uygulamalar](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx). VaraMizonov 'e göre Teknik İnceleme.
- [Azure kuyruklarını ve Service Bus kuyruklarını karşılaştırma](https://msdn.microsoft.com/magazine/jj159884.aspx). MSDN Magazine makalesi, hangi kuyruk hizmetinin kullanılacağını seçmenize yardımcı olabilecek ek bilgiler sağlar. Makalesinde Service Bus kimlik doğrulaması için ACS 'ye bağımlıdır. Bu makalede, ACS kullanılamadığında SB kuyruklarınızın devre dışı olmayacağı anlamına gelir. Ancak makale yazıldığı için, SB, ACS 'ye alternatif olarak [SAS belirteçlerini](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx) kullanmanızı sağlayacak şekilde değiştirilmiştir.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Zaman uyumsuz mesajlaşma öncü, kanallar ve filtreler düzenine, telafi Işlem düzenine, rekabet tüketicilerinin düzenine, CQRS düzenine bakın.
- [CQRS yolculuğu](https://msdn.microsoft.com/library/jj554200). CQRS hakkında Microsoft düzenleri ve uygulamaları ile ilgili E-kitap.

Video:

- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz parçalı video serisi. , Microsoft Müşteri danışmanlık ekibi (CAT) deneyiminden gerçek müşterilerle çekilen hikayelerle, yüksek düzeyde kavramlar ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. Azure depolama hizmeti ve kuyruklara giriş için, bkz. Bölüm 5, 35:13 adresinden itibaren.

> [!div class="step-by-step"]
> [Önceki](distributed-caching.md)
> [İleri](more-patterns-and-guidance.md)
