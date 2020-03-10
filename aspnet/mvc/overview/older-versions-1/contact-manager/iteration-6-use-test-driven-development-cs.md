---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 'Yineleme #6 – test odaklı geliştirme kullanın (C#) | Microsoft Docs'
author: microsoft
description: Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: aee0ff9d8d7f17e8a00dab12467bd3a3457fbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601803"
---
# <a name="iteration-6--use-test-driven-development-c"></a>Yineleme #6 – test odaklı geliştirme (C#) kullanın

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede kişi grupları ekleyeceğiz.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Kişi yönetimi ASP.NET MVC uygulaması (C#) oluşturma

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

Contact Manager uygulamasının önceki yinelemesinde, kodumuza yönelik bir güvenlik ağı sağlamak için birim testleri oluşturduk. Birim testlerini oluşturmaya yönelik mosyon, kodumuzu değiştirmeye daha dayanıklı hale getirmek idi. Birim testleri varken, kodumuza yönelik herhangi bir değişiklik yapabiliriz ve var olan işlevsellikten haberdar olup olmadığını hemen öğreniyoruz.

Bu yinelemede, birim testlerini tamamen farklı bir amaç için kullanırız. Bu yinelemede, *test odaklı geliştirme*adlı bir uygulama tasarımı felseparçası olarak birim testlerini kullanırız. Test odaklı geliştirme alıştırması yaparken, önce testleri yazar ve ardından testlere karşı kod yazarsınız.

Daha kesin olarak, test odaklı geliştirme yaparken, kod oluştururken tamamladığınız üç adım vardır (kırmızı/yeşil/yeniden düzenleme):

1. Başarısız olan bir birim testi yazma (kırmızı)
2. Birim testini geçiren kodu yazma (yeşil)
3. Kodunuzu yeniden düzenleme (yeniden düzenleme)

İlk olarak, birim testini yazarsınız. Birim testi, kodunuzun davranışını nasıl beklediğinizi ifade etmelidir. Birim testini ilk oluşturduğunuzda, birim testinin başarısız olması gerekir. Testi karşılayan herhangi bir uygulama kodunu henüz yazmadıysanız test başarısız olmalıdır.

Ardından, birim testinin geçmesi için yeterli kodu yazın. Amaç, kodu laziest, sloppiest ve en hızlı olası bir şekilde yazmaktır. Uygulamanızın mimarisi hakkında düşünmekten zaman harcanmamalıdır. Bunun yerine, birim testi tarafından ifade edilen amacı karşılamak için gereken minimum kod miktarını yazmaya odaklanmanız gerekir.

Son olarak, yeterli kod yazdıktan sonra geri dönerek uygulamanızın genel mimarisini göz önüne alabilirsiniz. Bu adımda, kodunuzun daha sürdürülebilir olması için depo deseni gibi yazılım tasarımı desenlerinden yararlanarak kodunuzu yeniden yazın (yeniden düzenleyin). Kodunuzun birim testleri kapsamında olduğu için kodunuzu bu adımda sorunsuzca yeniden yazabilirsiniz.

Test odaklı geliştirmeyi uygulamadan kaynaklanan birçok avantaj vardır. İlk olarak, test odaklı geliştirme sizi gerçekten yazılması gereken koda odaklanmaya zorlar. Belirli bir testi geçirmek için yeterli kod yazmak üzere sürekli olarak odaklandığınız için, Wandering ' den, hiçbir şekilde kullanmayacak büyük miktarda kod yazmanız engellenir.

İkinci olarak, "test First" tasarım yöntemi, kodunuzun nasıl kullanılacağına ilişkin perspektiften kod yazmaya zorlar. Diğer bir deyişle, test odaklı geliştirme yaparken, testlerinizi bir Kullanıcı perspektifinden sürekli yazmaya devam edersiniz. Bu nedenle, test odaklı geliştirme, temizleyici ve daha fazla anlaşılabilir API 'Lerle sonuçlanabilir.

Son olarak, test odaklı geliştirme, bir uygulama yazma sürecinin bir parçası olarak birim testlerini yazmaya zorlar. Proje son tarihi yaklaşımlarına göre test, genellikle pencereyi izleyen ilk şeydir. Test odaklı geliştirme yaparken, diğer taraftan, birim testlerini yazma hakkında daha büyük olasılıkla, test odaklı geliştirme birim testlerini bir uygulama oluşturma sürecine göre temel hale getiriyor.

> [!NOTE] 
> 
> Test odaklı geliştirme hakkında daha fazla bilgi edinmek için, **eski kod Ile etkin bir şekilde çalışan**Michael fealer defterini okumanızı öneririz.

Bu yinelemede, Contact Manager uygulamasına yeni bir özellik ekleyeceğiz. Kişi grupları için destek ekledik. Kişilerinizi Iş ve arkadaş grupları gibi kategoriler halinde düzenlemek için kişi grupları ' nı kullanabilirsiniz.

Test odaklı geliştirme sürecini izleyerek bu yeni işlevselliği uygulamamıza ekleyeceğiz. Öncelikle birim testlerimizi yazacağız ve bu testlere yönelik olarak tüm kodumuzu yazacağız.

## <a name="what-gets-tested"></a>Nelerin test edileceği

Önceki yinelemede bahsedildiği gibi, genellikle veri erişim mantığı veya görünüm mantığı için birim testleri yazmayın. Veritabanına erişmek görece yavaş bir işlem olduğundan veri erişim mantığı için birim testleri yazırın. Görüntüleme mantığı için birim testlerini yazmanız gerekmez, çünkü bir görünüme erişmek, görece yavaş bir işlem olan bir Web sunucusunun dönmesini gerektirir. Test tekrar çok hızlı yürütülene kadar bir birim testi yazmamanız gerekir

Test odaklı geliştirme birim testleri tarafından kullanıldığı için, başlangıçta yazma denetleyicisi ve iş mantığı üzerine odaklanıyoruz. Veritabanına veya görünümlere dokunmaktan kaçının. Bu öğreticinin çok sonuna kadar veritabanını değiştirmeyecek veya Görünümlerimizi oluşturmayacağız. Neleri test ettiğimiz ile başlayacağız.

## <a name="creating-user-stories"></a>Kullanıcı hikayeleri oluşturma

Test odaklı geliştirme yaparken her zaman bir test yazmaya başlayabilirsiniz. Bu, hemen bu soruyu ortaya çıkarır: ne öncelikle yazılacak teste nasıl karar verirsiniz? Bu soruyu yanıtlamak için [**Kullanıcı hikayeleri**](http://en.wikipedia.org/wiki/User_stories)kümesi yazmalısınız.

Kullanıcı hikayesi, Yazılım gereksiniminin çok kısa (genellikle bir cümle) açıklamasıdır. Kullanıcı perspektifinden yazılmış bir gereksinimin teknik olmayan bir açıklaması olmalıdır.

Burada, yeni kişi grubu işlevinin gerektirdiği özellikleri tanımlayan Kullanıcı hikayeleri kümesi verilmiştir:

1. Kullanıcı, kişi gruplarının bir listesini görüntüleyebilir.
2. Kullanıcı yeni bir kişi grubu oluşturabilir.
3. Kullanıcı, var olan bir kişi grubunu silebilir.
4. Kullanıcı, yeni bir kişi oluştururken bir kişi grubu seçebilir.
5. Kullanıcı, mevcut bir kişiyi düzenlediğinizde bir kişi grubu seçebilir.
6. Dizin görünümünde kişi gruplarının listesi görüntülenir.
7. Kullanıcı bir kişi grubuna tıkladığında, eşleşen kişilerin listesi görüntülenir.

Bu Kullanıcı hikayeleri listesinin bir müşteri tarafından tamamen anlaşılır olduğunu fark edersiniz. Teknik uygulama ayrıntılarının bahsetmesi yoktur.

Uygulamanızı oluşturma sürecinde, Kullanıcı hikayeleri kümesi daha da görüntülenebilir. Bir kullanıcı hikayesini birden fazla hikaye (gereksinimler) ile kesebilirsiniz. Örneğin, yeni bir kişi grubu oluşturmanın doğrulamayı dahil etmesi gerektiğine karar verebilirsiniz. Bir kişi grubu adı olmadan gönderilmesi bir doğrulama hatası döndürmelidir.

Kullanıcı hikayeleri listesini oluşturduktan sonra, ilk birim testinizi yazmaya hazırlanın. İletişim grupları listesini görüntülemek için bir birim testi oluşturarak başlayacağız.

## <a name="listing-contact-groups"></a>Kişi gruplarını listeleme

İlk Kullanıcı hikayemiz, kullanıcının kişi grupları listesini görüntüleyebilmelidir. Bu hikayeyi bir test ile ifade etmemiz gerekiyor.

ContactManager 'daki Controllers klasörüne sağ tıklayarak yeni bir birim testi oluşturun. test projesi, **Ekle, yeni test**ve **birim testi** şablonunu seçme (bkz. Şekil 1). Yeni birim testi GroupControllerTest.cs adlandırın ve **Tamam** düğmesine tıklayın.

[GroupControllerTest birim testi ekleme ![](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**Şekil 01**: groupcontrollertest birim testi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image2.png))

İlk birim testiniz Listeleme 1 ' de yer alır. Bu test, Grup denetleyicisinin Index () yönteminin bir grup kümesini döndürdüğünü doğrular. Test, görünüm verilerinde bir grup koleksiyonunun döndürüldüğünü doğrular.

**Listeleme 1-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

Kodu Visual Studio 'da liste 1 ' de ilk kez yazdığınızda, kırmızı dalgalı çizgi sayısı çok fazla olacaktır. GroupController veya Group sınıfları oluşturmadınız.

Bu noktada, ilk birim testimizi yürütebilmemiz için uygulamamızı bile derliyoruz. Bu iyi. Bu, başarısız bir test olarak sayılır. Bu nedenle, artık uygulama kodu yazmaya başlama iznimiz var. Testimizi yürütmek için yeterli kod yazmamız gerekiyor.

Liste 2 ' deki Grup denetleyicisi sınıfı, birim testini geçirmek için gereken en düşük kodu içerir. Index () eylemi, statik olarak kodlanmış grupların listesini döndürür (Grup sınıfı, Listeleme 3 ' te tanımlanır).

**Listeleme 2-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**Listeleme 3-Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

Projenize GroupController ve Group sınıfları eklendikten sonra ilk birim testi başarıyla tamamlanır (bkz. Şekil 2). Testi geçirmek için gereken en düşük işi yaptık. Hadi kutlayalım.

[Başarılı ![!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**Şekil 02**: başarılı! ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](iteration-6-use-test-driven-development-cs/_static/image4.png))

## <a name="creating-contact-groups"></a>Kişi grupları oluşturma

Şimdi ikinci kullanıcı hikayesine geçiş yapabilirsiniz. Yeni kişi grupları oluşturabilmemiz gerekiyor. Bu amacı bir test ile ifade etmemiz gerekiyor.

Listeleme 4 ' teki test, Create () yönteminin yeni bir grup ile çağrılmasını doğrular grubu, Index () yöntemi tarafından döndürülen gruplar listesine ekler. Başka bir deyişle, yeni bir grup oluştururum, dizin () yöntemi tarafından döndürülen gruplar listesinden yeni grubu geri gönderebilmelidir.

**Listeleme 4-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

Listeleme 4 ' teki test, Grup denetleyicisi oluştur () yöntemini yeni bir kişi grubuyla çağırır. Daha sonra, test, Grup denetleyicisi dizini () metodunu çağırmanın, görüntüleme verilerinde yeni grubu döndürdüğünü doğrular.

5\. listede değiştirilen grup denetleyicisi, yeni testi geçirmek için gereken en düşük değişiklik sayısını içerir.

**Listeleme 5-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>Listeleme 5 ' teki Grup denetleyicisinde yeni bir Create () eylemi vardır. Bu eylem, gruplar koleksiyonuna bir grup ekler. Dizin () eyleminin grup koleksiyonunun içeriğini döndürecek şekilde değiştirildiğini unutmayın.

Bir kez daha, birim testini geçirmek için gereken en düşük iş miktarını gerçekleştirdik. Grup denetleyicisinde bu değişiklikleri yaptıktan sonra, tüm birim testleriniz geçer.

## <a name="adding-validation"></a>Doğrulama Ekleme

Bu gereksinim, Kullanıcı hikayesine açık olarak belirtilmedi. Ancak, bir grubun bir adı olması gerekir. Aksi takdirde, kişilerin gruplar halinde düzenlenmesi çok faydalı olmaz.

Liste 6, bu amacı ifade eden yeni bir test içerir. Bu test, bir ad vermeden bir grup oluşturmaya çalışan, model durumunda doğrulama hata iletisine neden olur.

**6-Controllers\GroupControllerTest.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

Bu testi karşılamak için Grup sınıfmıza bir ad özelliği eklememiz gerekiyor (bkz. Listeleme 7). Ayrıca, Grup denetleyicisi oluşturma () eylemize (bkz. listeleme 8) çok küçük bir doğrulama mantığı eklememiz gerekiyor.

**Listeleme 7-Models\Group.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**8-Controllers\GroupController.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

Grup denetleyicisi oluşturma () eyleminin artık hem doğrulama hem de veritabanı mantığını içerdiğini unutmayın. Şu anda, Grup denetleyicisi tarafından kullanılan veritabanı, bellek içi bir koleksiyondan daha fazla şey içerir.

## <a name="time-to-refactor"></a>Yeniden düzenleme süresi

Kırmızı/yeşil/yeniden düzenleme içinde üçüncü adım yeniden düzenleme bölümüdür. Bu noktada, kodumuza geri dönüp tasarımını geliştirmek için uygulamamızı nasıl yeniden tasarlayabileceğimizi göz önünde bulundurmanız gerekir. Yeniden düzenleme aşaması, yazılım tasarımı ilkelerini ve düzenlerini kullanmanın en iyi yolu hakkında daha fazla bilgi verdiğimiz aşamasıdır.

Kodunuzun tasarımını geliştirmek için seçtiğimiz her şekilde kodumuzu değiştirmek ücretsizdir. Mevcut işlevselliği bozmamıza engel olan birim testlerinin bir güvenlik ağı vardır.

Şu anda grup denetleyicimiz, iyi yazılım tasarımının perspektifinden bir mesgiydi. Grup denetleyicisi, doğrulama ve veri erişim kodu için bir tanınled iletisi içerir. Tek sorumluluğun ihlal edilmesini önlemek için, bu kaygıları farklı sınıflara ayırdık.

Yeniden düzenlenmiş grup denetleyicisi sınıfınız, liste 9 ' da bulunur. Denetleyici ContactManager hizmet katmanını kullanacak şekilde değiştirilmiştir. Bu, Ilgili kişi denetleyicisiyle birlikte kullandığımız aynı hizmet katmanıdır.

10. liste, ContactManager hizmet katmanına eklenen ve grupların doğrulanması, listelenmesi ve oluşturulmasını destekleyen yeni yöntemler içerir. Itactmanagerservice arabirimi yeni yöntemleri içerecek şekilde güncelleştirildi.

12. liste, ıtactmanagerrepository arabirimini uygulayan yeni bir FakeContactManagerRepository sınıfı içerir. Itactmanagerrepository arabirimini de uygulayan EntityContactManagerRepository sınıfından farklı olarak, yeni FakeContactManagerRepository sınıfınız veritabanıyla iletişim kurmaz. FakeContactManagerRepository sınıfı, veritabanı için bir ara sunucu olarak bellek içi bir koleksiyon kullanır. Bu sınıfı, birim testlerimizde sahte bir depo katmanı olarak kullanacağız.

**9-Controllers\GroupController.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**10-Controllers\ContactManagerService.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**11-Controllers\fakecontactmanagerdepotory.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

Itactmanagerrepository arabirimini değiştirmenin, EntityContactManagerRepository sınıfında CreateGroup () ve ListGroups () yöntemlerini uygulaması için kullanılması gerekir. Bunu yapmanın lazest ve en hızlı yolu şuna benzer bir saplama yöntemi eklemektir:   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

Son olarak, uygulamamız üzerinde yapılan bu değişiklikler birim testlerimizde bazı değişiklikler yapmamızı gerektirir. Artık birim testlerini gerçekleştirirken FakeContactManagerRepository 'yi kullanmanız gerekir. Güncelleştirilmiş GroupControllerTest sınıfı, 12. listede yer alır.

**12-Controllers\GroupControllerTest.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

Bu değişiklikleri bir kez daha yaptıktan sonra, tüm birim testleriniz geçer. Kırmızı/yeşil/yeniden düzenleme döngüsünün tamamını tamamladık. İlk iki kullanıcı hikayesi uyguladık. Artık Kullanıcı hikayeleri için ifade edilen gereksinimlere yönelik birim testlerini destekliyoruz. Kullanıcı hikayelerinin geri kalanını uygulamak, aynı kırmızı/yeşil/yeniden düzenleme döngüsünü tekrarlamayı gerektirir.

## <a name="modifying-our-database"></a>Veritabanımızı değiştirme

Ne yazık ki, birim testlerimiz tarafından ifade edilen tüm gereksinimleri karşıladığımız halde çalışmamız yapılmadı. Hala veritabanımızı değiştirmemiz gerekiyor.

Yeni bir grup veritabanı tablosu oluşturuyoruz. Aşağıdaki adımları uygulayın:

1. Sunucu Gezgini penceresinde tablolar klasörüne sağ tıklayın ve **Yeni Tablo Ekle**menü seçeneğini belirleyin.
2. Tablo Tasarımcısı aşağıda açıklanan iki sütunu girin.
3. Kimlik sütununu birincil anahtar ve kimlik sütunu olarak işaretleyin.
4. Disketin simgesine tıklayarak yeni tabloyu ad gruplarıyla kaydedin.

<a id="0.11_table01"></a>

| **Sütun adı** | **Veri türü** | **Null değerlere izin ver** |
| --- | --- | --- |
| Kimlik | int | False |
| Adı | nvarchar (50) | False |

Ardından, kişiler tablosundan tüm verileri silmemiz gerekir (Aksi takdirde, kişiler ve gruplar tabloları arasında bir ilişki oluşturmayacağız). Aşağıdaki adımları uygulayın:

1. Kişiler tablosuna sağ tıklayın ve **tablo verilerini göster**menü seçeneğini belirleyin.
2. Tüm satırları silin.

Ardından, gruplar veritabanı tablosu ve var olan kişiler veritabanı tablosu arasında bir ilişki tanımlamanız gerekir. Aşağıdaki adımları uygulayın:

1. Tablo Tasarımcısı açmak için Sunucu Gezgini penceresindeki kişiler tablosuna çift tıklayın.
2. GroupID adlı kişiler tablosuna yeni bir tamsayı sütunu ekleyin.
3. Yabancı anahtar Ilişkileri iletişim kutusunu açmak için Ilişki düğmesine tıklayın (bkz. Şekil 3).
4. Ekle düğmesine tıklayın.
5. Tablo ve sütun belirtimi düğmesinin yanında görünen üç nokta düğmesine tıklayın.
6. Tablolar ve sütunlar iletişim kutusunda grupları birincil anahtar tablosu ve kimlik olarak birincil anahtar sütunu olarak seçin. Yabancı anahtar tablosu ve GroupID olarak, yabancı anahtar sütunu olarak Kişiler ' i seçin (bkz. Şekil 4). Tamam düğmesine tıklayın.
7. **Ekle ve Güncelleştir belirtimi**altında, **silme kuralı**için değer **basamakla** ' yı seçin.
8. Yabancı anahtar Ilişkileri iletişim kutusunu kapatmak için Kapat düğmesine tıklayın.
9. Değişiklikleri kişiler tablosuna kaydetmek için Kaydet düğmesine tıklayın.

[veritabanı tablosu ilişkisi oluşturma ![](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**Şekil 03**: veritabanı tablosu ilişkisi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image6.png))

[tablo ilişkilerini belirtme ![](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**Şekil 04**: tablo ilişkilerini belirtme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image8.png))

### <a name="updating-our-data-model"></a>Veri modelimizi güncelleştirme

Ardından, veri modelimizi yeni veritabanı tablosunu gösterecek şekilde güncelleştirmemiz gerekiyor. Aşağıdaki adımları uygulayın:

1. Entity Desisgner açmak için modeller klasöründeki ContactManagerModel. edmx dosyasına çift tıklayın.
2. Tasarımcı yüzeyine sağ tıklayıp **modeli Güncelleştir**menü seçeneğini belirleyin.
3. Güncelleştirme sihirbazında, gruplar tablosunu seçin ve son düğmesine tıklayın (bkz. Şekil 5).
4. Gruplar varlığına sağ tıklayın ve **Yeniden Adlandır**seçeneğini belirleyin. *Gruplar* varlığının adını *Grup* (tekil) olarak değiştirin.
5. Iletişim varlığının altında görünen gruplar gezintisi özelliğine sağ tıklayın. *Gruplar* gezintisi özelliğinin adını *Grup* (tekil) olarak değiştirin.

[bir Entity Framework modelini veritabanından güncelleştirme ![](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**Şekil 05**: veritabanından bir Entity Framework modeli güncelleştirme ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image10.png))

Bu adımları tamamladıktan sonra, veri modeliniz hem kişiler hem de gruplar tablolarını temsil eder. Entity Desisgner her iki varlığı de göstermelidir (bkz. Şekil 6).

[Grup ve Iletişim ![Entity Desisgner görüntüleme](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**Şekil 06**: Grup ve ilgili kişi görüntüleme Entity Desisgner ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image12.png))

### <a name="creating-our-repository-classes"></a>Depo Sınıflarımızı oluşturma

Ardından, depo sınıfınızı uygulamamız gerekir. Bu yineleme sırasında, birim testlerimizi karşılamak için kod yazarken ıtactmanagerrepository arabirimine birkaç yeni yöntem ekledik. Itactmanagerrepository arabiriminin son sürümü, 14. listede yer alır.

**14-Models\icontactmanagerdepotory.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

Kişi gruplarıyla çalışma ile ilgili yöntemlerin gerçekten uygulanmamıştır. Şu anda EntityContactManagerRepository sınıfı, ıtactmanagerrepository arabiriminde listelenen her bir kişi grubu yönteminin saplama yöntemlerine sahiptir. Örneğin, ListGroups () yöntemi şu anda şöyle görünür:

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

Saplama yöntemleri, uygulamamızı derleyip birim testlerini iletmemize olanak sağlar. Ancak, bu yöntemlerin gerçekten uygulanması zaman alabilir. EntityContactManagerRepository sınıfının son sürümü, 13. listede yer alır.

**13-Models\entitycontactmanagerdepotory.cs listeleme**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>Görünümleri oluşturma

Varsayılan ASP.NET View altyapısını kullandığınızda ASP.NET MVC uygulaması. Bu nedenle, belirli bir birim testine yanıt olarak görünümler oluşturdon. Ancak, bir uygulama görünümler olmadan yararsız olacağından, bu yinelemeyi, Contact Manager uygulamasında yer alan görünümleri oluşturmadan ve değiştirmeden tamamlayabiliriz.

Kişi gruplarını yönetmek için aşağıdaki yeni görünümleri oluşturmamız gerekir (bkz. Şekil 7):

- Views\group\ındex.aspx-kişi gruplarının listesini görüntüler
- Views\Group\Delete.aspx-bir kişi grubunu silmeye yönelik onay formunu görüntüler

[Grup dizini görünümünü ![](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**Şekil 07**: Grup dizini görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image14.png))

Aşağıdaki mevcut görünümleri, kişi grupları içerecek şekilde değiştirmemiz gerekiyor:

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

Bu öğreticiye eşlik eden Visual Studio uygulamasına bakarak değiştirilmiş görünümleri görebilirsiniz. Örneğin, Şekil 8 ' de kişi dizini görünümü gösterilmektedir.

[Kişi dizini görünümünü ![](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**Şekil 08**: kişi dizini görünümü ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-6-use-test-driven-development-cs/_static/image16.png))

## <a name="summary"></a>Özet

Bu yinelemede, test odaklı bir geliştirme uygulaması tasarım yöntemi izleyerek, Contact Manager uygulamanıza yeni işlevsellik ekledik. Kullanıcı hikayeleri kümesi oluşturarak başladık. Kullanıcı hikayeleri tarafından ifade edilen gereksinimlere karşılık gelen bir birim testleri kümesi oluşturduk. Son olarak, birim testleriyle ifade edilen gereksinimleri karşılamak için yeterli kod yazdık.

Birim testleriyle ifade edilen gereksinimleri karşılamak için yeterli kod yazmayı bitirdikten sonra veritabanı ve Görünümlerimizi güncelleştirdik. Veritabanınıza yeni bir gruplar tablosu ekledik ve Entity Framework veri modelimizi güncelleştirdik. Ayrıca bir görünüm kümesi oluşturulup değiştirdik.

Sonraki yinelemede--son yineleme--Ajax 'un avantajlarından yararlanmak için uygulamamızı yeniden yazdık. Ajax 'tan yararlanarak, Contact Manager uygulamasının yanıt hızını ve performansını iyileştireceğiz.

> [!div class="step-by-step"]
> [Önceki](iteration-5-create-unit-tests-cs.md)
> [İleri](iteration-7-add-ajax-functionality-cs.md)
