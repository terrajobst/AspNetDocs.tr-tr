---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
title: 'Yineleme #4 – uygulamayı gevşek olarak (VB) yapın | Microsoft Docs'
author: microsoft
description: Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. İçin...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 92c70297-4430-4e4e-919a-9c2333a8d09a
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-vb
msc.type: authoredcontent
ms.openlocfilehash: 422c75406d9c08279d0c2224ee4b6db3a71eb1b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582084"
---
# <a name="iteration-4--make-the-application-loosely-coupled-vb"></a>Yineleme #4 – uygulamayı gevşek olarak bağlanmış hale getirme (VB)

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-4-make-the-application-loosely-coupled-vb/_static/contactmanager_4_vb1.zip)

> Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. Örneğin, uygulamamız depo deseninin ve bağımlılık ekleme düzeninin kullanılması için yeniden düzenliyoruz.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Kişi yönetimi ASP.NET MVC uygulaması oluşturma (VB)

Bu öğretici dizisinde, başlangıçtan sonuna kadar bir Iletişim yönetimi uygulaması oluşturacaksınız. Ilgili kişi Yöneticisi uygulaması, kişi listesi için kişi bilgilerini, telefon numaralarını ve e-posta adreslerini depolamanıza olanak sağlar.

Uygulamayı birden çok yineleme üzerinde oluşturacağız. Her yinelemede, uygulamayı kademeli olarak geliştirdik. Bu birden çok yineleme yaklaşımının hedefi, her bir değişikliğin nedenini anlamanıza olanak sağlamaktır.

- Yineleme #1-uygulamayı oluşturun. İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve silme (CRUD).

- Yineleme #2-uygulamanın iyi görünmesini sağlayın. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.

- Yineleme #3-form doğrulaması ekleme. Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğruladık.

- Yineleme #4-uygulamayı gevşek olarak bağlanmış hale getirin. Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. Örneğin, uygulamamız depo deseninin ve bağımlılık ekleme düzeninin kullanılması için yeniden düzenliyoruz.

- Yineleme #5-birim testleri oluşturun. Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. Denetleyicilerimizin ve doğrulama mantığımız için veri modeli Sınıflarımızı ve derleme birimi testlerini modelliyoruz.

- Yineleme #6-test odaklı geliştirme kullanın. Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede kişi grupları ekleyeceğiz.

- Yineleme #7-Ajax işlevselliği ekleme. Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.

## <a name="this-iteration"></a>Bu yineleme

Contact Manager uygulamasının bu dördüncü yinelemesinde, uygulamayı daha gevşek bir şekilde bağlanmış hale getirmek için uygulamayı yeniden tasarlıyoruz. Bir uygulama gevşek olarak birleştirildiğinde, uygulamanın diğer bölümlerinde kodu değiştirmeye gerek kalmadan kodu uygulamanın bir bölümünde değiştirebilirsiniz. Gevşek olarak bağlanmış uygulamaların değiştirilmesi daha esnektir.

Şu anda, Contact Manager uygulaması tarafından kullanılan tüm veri erişimi ve doğrulama mantığı denetleyici sınıflarında yer alır. Bu kötü bir fikir. Uygulamanızın bir bölümünü değiştirmeniz gerektiğinde, uygulamanızın başka bir bölümüne hata getirriskten etkilenir. Örneğin, doğrulama mantığınızı değiştirirseniz, veri erişiminize veya denetleyici mantığınıza yeni hatalar sunuyoruz.

> [!NOTE] 
> 
> (SRP), bir sınıf asla değiştirmek için birden fazla neden olmamalıdır. Denetleyici, doğrulama ve veritabanı mantığını karıştırma, tek sorumluluk Ilkesinin büyük bir ihlaline neden olur.

Uygulamanızı değiştirmeniz gerekebilecek birkaç neden vardır. Uygulamanıza yeni bir özellik eklemeniz gerekebilir, uygulamanızdaki bir hatayı çözmeniz gerekebilir veya uygulamanızın bir özelliğinin nasıl uygulandığını değiştirmeniz gerekebilir. Uygulamalar nadiren statiktir. Zaman içinde büyüme ve bulunmamalıdır 'e eğilimlidir.

Örneğin, veri erişim katmanınızı nasıl uygulayacağınızı değiştirmeye karar verirsiniz. Şimdi, Contact Manager uygulaması veritabanına erişmek için Microsoft Entity Framework kullanır. Ancak, ADO.NET veri Hizmetleri veya Nhazırda bekleme gibi yeni veya alternatif bir veri erişim teknolojisine geçirmeye karar verebilirsiniz. Ancak, veri erişim kodu doğrulama ve denetleyici kodundan ayrı olmadığı için, veri erişimiyle doğrudan ilgili olmayan diğer kodları değiştirmeden uygulamanızdaki veri erişim kodunu değiştirmenin bir yolu yoktur.

Bir uygulama gevşek olarak birleştirildiğinde, diğer yandan uygulamanın diğer bölümlerine dokunmadan uygulamanın bir bölümünde değişiklik yapabilirsiniz. Örneğin, doğrulama veya denetleyici mantığınızı değiştirmeden veri erişim teknolojilerini geçirebilirsiniz.

Bu yinelemede, Contact Manager uygulamamızı daha gevşek olarak bağlanmış bir uygulamayla yeniden düzenleme olanağı sağlayan çeşitli yazılım tasarımı desenlerinden faydalanır. İşiniz bittiğinde, Ilgili kişi Yöneticisi, daha önce yapmadığı herhangi bir şey gerçekleştirmedik. Ancak, gelecekte uygulamayı daha kolay değiştirebileceksiniz.

> [!NOTE] 
> 
> Yeniden düzenleme, bir uygulamayı var olan herhangi bir işlevi kaybedecek şekilde yeniden yazma işlemidir.

## <a name="using-the-repository-software-design-pattern"></a>Depo yazılımı tasarım modelini kullanma

İlk değiştirimiz, depo deseninin adı verilen bir yazılım tasarımı deseninin avantajlarından faydalanır. Veri erişim kodumuzu uygulamamızda geri kalanından yalıtmak için depo düzenlerini kullanacağız.

Depo deseninin uygulanması için aşağıdaki iki adımı tamamlaması gerekir:

1. Arabirim oluşturma
2. Arabirimi uygulayan somut bir sınıf oluşturun

İlk olarak, gerçekleştirmeleri gereken tüm veri erişim yöntemlerini açıklayan bir arabirim oluşturuyoruz. Itactmanagerrepository arabirimi, Listeleme 1 ' de yer alır. Bu arabirim beş yöntemi açıklar: CreateContact (), DeleteContact (), EditContact (), GetContact ve ListContacts ().

**Listeleme 1-Models\icontactmanagerdepotory.exe**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample1.vb)]

Bundan sonra, ıtactmanagerrepository arabirimini uygulayan somut bir sınıf oluşturuyoruz. Veritabanına erişmek için Microsoft Entity Framework kullandığımızda EntityContactManagerRepository adlı yeni bir sınıf oluşturacağız. Bu sınıf, Listeleme 2 ' de bulunur.

**Listeleme 2-Models\entitycontactmanagerdepotory.exe**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample2.vb)]

EntityContactManagerRepository sınıfının ıtactmanagerrepository arabirimini uyguladığına dikkat edin. Sınıfı, bu arabirim tarafından tanımlanan tüm yöntemlerin beş birini uygular.

Neden bir arabirimle botelemiz gerektiğini merak ediyor olabilirsiniz. Neden hem bir arabirim hem de onu uygulayan bir sınıf oluşturuyoruz?

Tek bir istisna ile, uygulamamız geri kalanı somut sınıfla değil arabirimiyle etkileşime girecektir. EntityContactManagerRepository sınıfı tarafından kullanıma sunulan yöntemleri çağırmak yerine, ıtactmanagerrepository arabirimi tarafından kullanıma sunulan yöntemleri çağıracağız.

Bu şekilde, uygulamanın geri kalanını değiştirmeye gerek kalmadan arabirimi yeni bir sınıfla uygulayabiliriz. Örneğin, bir sonraki tarihte IContactManagerRepository arabirimini uygulayan bir DataServicesContactManagerRepository sınıfı uygulamak isteyebilirsiniz. DataServicesContactManagerRepository sınıfı, Microsoft Entity Framework yerine bir veritabanına erişmek için ADO.NET veri hizmetlerini kullanabilir.

Uygulama kodumuz somut EntityContactManagerRepository sınıfı yerine ıtactmanagerrepository arabirimine göre programlanmışsa, kodunuzun geri kalanının hiçbirini değiştirmeden somut sınıfları değiştirebilirsiniz. Örneğin, veri erişimimizi veya doğrulama mantığımızı değiştirmeden EntityContactManagerRepository sınıfından DataServicesContactManagerRepository sınıfına geçiş yapabilirsiniz.

Somut sınıflar yerine arabirimlere (soyutlamalar) programlama, uygulamamızı daha dayanıklı hale getirir.

> [!NOTE] 
> 
> Visual Studio içindeki somut bir sınıftan hızlı bir şekilde bir arabirim oluşturarak yeniden düzenleme, Arabirimi Ayıkla ' yı seçebilirsiniz. Örneğin, önce EntityContactManagerRepository sınıfını oluşturabilir ve sonra ıtactmanagerrepository arabirimini otomatik olarak oluşturmak için ayıklama arabirimini kullanabilirsiniz.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Bağımlılık ekleme yazılımı tasarım deseninin kullanımı

Veri erişim kodumuzu ayrı bir depo sınıfına geçirdiğimiz için, bu sınıfı kullanmak üzere Iletişim denetleyicimizi değiştirmemiz gerekiyor. Denetleyicimizde depo sınıfını kullanmak için bağımlılık ekleme adlı bir yazılım tasarımı deseninin avantajlarından faydalanacağız.

Değiştirilen Iletişim denetleyicisi, Listeleme 3 ' te bulunur.

**Listeleme 3-Controllers\contactcontroller.exe**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample3.vb)]

Kod 3 ' teki kişi denetleyicisinin iki Oluşturucusu olduğunu unutmayın. İlk Oluşturucu, ıtactmanagerrepository arabiriminin somut bir örneğini ikinci oluşturucuya geçirir. Kişi denetleyicisi sınıfı, *Oluşturucu bağımlılığı ekleme*işlemini kullanır.

Yalnızca EntityContactManagerRepository sınıfının kullanıldığı bir ve tek yer ilk oluşturucuda. Sınıfın geri kalanı somut EntityContactManagerRepository sınıfı yerine ıtactmanagerrepository arabirimini kullanır.

Bu, gelecekte ıtactmanagerrepository sınıfının uygulamalarına geçiş yapmayı kolaylaştırır. EntityContactManagerRepository sınıfı yerine DataServicesContactRepository sınıfını kullanmak istiyorsanız, yalnızca ilk oluşturucuyu değiştirmelisiniz.

Oluşturucu bağımlılığı ekleme Ayrıca, Iletişim denetleyicisi sınıfını çok kararlı hale getirir. Birim testlerinizde, ıtactmanagerrepository sınıfının bir sahte uygulamasını geçirerek, Iletişim denetleyicisi örneğini oluşturabilirsiniz. Bu bağımlılık ekleme özelliği, Contact Manager uygulaması için birim testleri oluştururken bir sonraki yinelemede bizim için çok önemlidir.

> [!NOTE] 
> 
> Ilgili kişi denetleyicisi sınıfını IContactManagerRepository arabiriminin belirli bir uygulamasından tamamen ayırmak istiyorsanız, StructureMap veya Microsoft gibi bağımlılık ekleme 'yi destekleyen bir çatı avantajlarından yararlanabilirsiniz. Entity Framework (MEF). Bağımlılık ekleme çerçevesinin avantajlarından yararlanarak, kodunuzda somut bir sınıfa başvurmanız gerekmez.

## <a name="creating-a-service-layer"></a>Hizmet katmanı oluşturma

Doğrulama mantığımız, kod 3 ' teki değiştirilen denetleyici sınıfında denetleyici mantığımızda hala karışık olduğunu fark etmiş olabilirsiniz. Veri erişim mantığımızı yalıtmak iyi bir fikir olması nedeniyle, doğrulama mantığımızı yalıtmak iyi bir fikirdir.

Bu sorunu gidermek için ayrı bir [hizmet katmanı](http://martinfowler.com/eaaCatalog/serviceLayer.html)oluşturuyoruz. Hizmet katmanı, denetleyicimiz ve depo sınıflarımız arasında ekleyebilmemiz için ayrı bir katmandır. Hizmet katmanı, tüm doğrulama mantığımız dahil olmak üzere iş mantığımızı içerir.

ContactManagerService, listeleme 4 ' te bulunur. Bu, Ilgili kişi denetleyicisi sınıfından doğrulama mantığını içerir.

**Listeleme 4-Models\contactmanagerservice.exe**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample4.vb)]

ContactManagerService oluşturucusunun bir ValidationDictionary gerektirdiğini unutmayın. Hizmet katmanı bu ValidationDictionary aracılığıyla denetleyici katmanıyla iletişim kurar. Dekoratör modelini tartıştığımız zaman, aşağıdaki bölümde ValidationDictionary 'yi ayrıntılı olarak tartıştık.

Ayrıca, ContactManagerService 'in ıtactmanagerservice arabirimini gerçekleştirdiğinden de dikkat edin. Somut sınıflar yerine, her zaman, program arabirimlerine karşı programlama yapmanız gerekir. Contact Manager uygulamasındaki diğer sınıflar doğrudan ContactManagerService sınıfıyla etkileşime girmiyor. Bunun yerine, bir istisna dışında, Contact Manager uygulamasının geri kalanı IContactManagerService arabirimine göre programlanır.

Itactmanagerservice arabirimi, Listeleme 5 ' te bulunur.

**Listeleme 5-Models\icontactmanagerservice,vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample5.vb)]

Değiştirilen Iletişim denetleyicisi sınıfı, listeleme 6 ' da bulunur. Kişi denetleyicisinin artık ContactManager deposuyla etkileşime girmediğine dikkat edin. Bunun yerine, kişi denetleyicisi ContactManager hizmetiyle etkileşime girer. Her katman diğer katmanlardan mümkün olduğunca yalıtılmıştır.

**6-Controllers\contactcontroller.exe listeleme**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample6.vb)]

Uygulamamız artık tek sorumluluğun (SRP) hiç birini çalıştırmayacaktır. Liste 6 ' daki kişi denetleyicisi, uygulama yürütme akışının denetlenmesinden farklı olarak her sorumluluktan çıkarılır. Tüm doğrulama mantığı, kişi denetleyicisinden kaldırılmıştır ve hizmet katmanına gönderilir. Tüm veritabanı mantığı depo katmanına itildi.

## <a name="using-the-decorator-pattern"></a>Dekoratör modelini kullanma

Hizmet katmanımızı denetleyici katmanımızdan tamamen ayrışabilebilmemiz istiyoruz. İlke ' de, MVC uygulamamıza bir başvuru eklemeye gerek kalmadan hizmet katmanımızı denetleyici katmanımız ayrı bir derlemede derleyebilmelidir.

Ancak, hizmet katmanımız doğrulama hata iletilerini denetleyici katmanına geri geçirebilmelidir. Hizmet katmanını, denetleyici ve hizmet katmanıyla eşlenmeden doğrulama hata iletilerini iletmeksizin nasıl etkinleştirebiliriz? [Dekoratör deseninin](http://en.wikipedia.org/wiki/Decorator_pattern)adlı bir yazılım tasarımı deseninin avantajlarından faydalanabiliyoruz.

Denetleyici, doğrulama hatalarını göstermek için ModelState adlı bir ModelStateDictionary kullanır. Bu nedenle, ModelState 'i denetleyici katmanından hizmet katmanına geçirmeye düşünebilirsiniz. Ancak, hizmet katmanında ModelState kullanmak, hizmet katmanınızı ASP.NET MVC çerçevesinin bir özelliğine bağımlı hale getirir. Bu, ASP.NET MVC uygulaması yerine bir WPF uygulamasıyla hizmet katmanını kullanmak isteyebileceğiniz için hatalı olabilir. Bu durumda, ModelStateDictionary sınıfını kullanmak için ASP.NET MVC çerçevesine başvurmak istemezsiniz.

Dekoratör düzeni, bir arabirim uygulamak için yeni bir sınıftaki mevcut bir sınıfı sarmanızı sağlar. Contact Manager projemiz, liste 7 ' de bulunan ModelStateWrapper sınıfını içerir. ModelStateWrapper sınıfı, bir arabirimi liste 8 ' de uygular.

**Listeleme 7-Models\Validation\ModelStateWrapper.vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample7.vb)]

**Listeleme 8 Models\validation\ivalidationdictionary.exe. vb**

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample8.vb)]

Liste 5 ' e yakın bir görünüm alırsanız, ContactManager hizmet katmanının yalnızca ıvalidationdictionary arabirimini kullandığını görürsünüz. ContactManager hizmeti ModelStateDictionary sınıfına bağımlı değil. Kişi denetleyicisi ContactManager hizmetini oluşturduğunda, denetleyici modelleme durumunu şu şekilde sarar:

[!code-vb[Main](iteration-4-make-the-application-loosely-coupled-vb/samples/sample9.vb)]

## <a name="summary"></a>Özet

Bu yinelemede, Contact Manager uygulamasına yeni bir işlev ekliyoruz. Bu yinelemenin hedefi, devam etmek ve değiştirmek daha kolay olacak şekilde Contact Manager uygulamasını yeniden düzenlemek idi.

İlk olarak, depo yazılım tasarımı modelini uyguladık. Tüm veri erişim kodunu ayrı bir ContactManager depo sınıfına geçirdik.

Ayrıca, denetleyici mantığımızda doğrulama mantığımızı yalıdık. Tüm doğrulama kodumuzu içeren ayrı bir hizmet katmanı oluşturduk. Denetleyici katmanı hizmet katmanıyla etkileşime girer ve hizmet katmanı, depo katmanıyla etkileşime girer.

Hizmet katmanını oluşturduğumuzda, modelinden hizmet katmanımızın ayırt etmek için dekoratör düzeninden faydalanır. Hizmet katmanımızda ModelState yerine ıvalidationdictionary arabirimine göre programlıyoruz.

Son olarak, bağımlılık ekleme düzeniyle adlandırılan bir yazılım tasarımı deseninin avantajlarından faydalantık. Bu model somut sınıflar yerine arabirimlerde (soyutlamalar) programmamıza olanak sağlar. Bağımlılık ekleme tasarım deseninin uygulanması, kodumuzu daha da daha kararlı hale getirir. Sonraki yinelemede, projemizdeki birim testlerini ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](iteration-3-add-form-validation-vb.md)
> [İleri](iteration-5-create-unit-tests-vb.md)
