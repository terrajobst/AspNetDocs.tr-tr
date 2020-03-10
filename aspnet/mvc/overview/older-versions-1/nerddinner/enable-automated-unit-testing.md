---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: Otomatik birim testini etkinleştir | Microsoft Docs
author: microsoft
description: 12. adım, Nerdakşam yemeği işlevselümüzü doğrulayan ve değişiklik yapma güvencesine izin veren bir otomatik birim testleri paketinin nasıl geliştirileceği gösterilmektedir...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541680"
---
# <a name="enable-automated-unit-testing"></a>Otomatik Birim Testini Etkinleştirme

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 12. adımından oluşur.
> 
> 12. adım, Nerdakşam yemeği işlevselümüzü doğrulayan bir otomatik birim testi paketinin nasıl geliştirileceği ve gelecekte uygulamada değişiklik ve iyileştirmeler yapma güvencesine sahip olduğunu gösterir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-12-unit-testing"></a>Nerdakşam yemeği adım 12: birim testi

Nerdakşam yemeği işlevselümüzü doğrulayan ve gelecekte uygulamada değişiklik ve iyileştirmeler yapma güvencesine izin veren bir otomatik birim testleri paketi geliştiriyorum.

### <a name="why-unit-test"></a>Birim testi neden?

Sürücüde bir sabah iş üzerinde çalıştığınız bir uygulamayla ilgili ani bir flaş vardır. Uygulamayı önemli ölçüde daha iyi hale getirmek için uygulayabileceğiniz bir değişiklik olduğunu fark edersiniz. Kodu temizliyor, yeni bir özellik ekleyen veya bir hatayı düzelten bir yeniden düzenleme olabilir.

Bilgisayarınıza ulaşan bir sorun var: "Bu geliştirmeyi yapmak için güvenli hale getirme mi?" Değişikliğin yan etkileri varsa veya bir şeyi bozarsa ne olacak? Değişikliğin uygulanması basit olabilir ve yalnızca birkaç dakika sürer, ancak tüm uygulama senaryolarını el ile test etmek için saat alırsa ne olur? Bir senaryoyu ele almayı unutursanız ve bozuk bir uygulama üretime gidiyor mi? Bu geliştirmeyi tamamen tüm çabalara getirsin mi?

Otomatik birim testleri, uygulamalarınızı sürekli olarak geliştirmenize ve üzerinde çalıştığınız kodun bir RAID 'den kaçınmanızı sağlayan bir güvenlik ağı sağlayabilir. İşlevselliği hızlı bir şekilde doğrulayan otomatikleştirilmiş testlerin olması, güvenle kod sağlamanıza olanak sağlar ve sizin de rahat bir şekilde yapamamanıza izin vermeyebilirsiniz. Ayrıca, daha fazla sürdürülebilir çözüm oluşturmaya yardımcı olur ve daha uzun bir süre boyunca yatırım getirisi daha yüksektir.

ASP.NET MVC Framework, birim testi uygulaması işlevselliğini kolaylaştırır ve doğal hale getirir. Ayrıca, test ilk tabanlı geliştirmeyi sağlayan test odaklı geliştirme (TDD) iş akışını da mümkün kılar.

### <a name="nerddinnertests-project"></a>Nerdakşam yemeği. Tests projesi

Bu öğreticinin başlangıcında Nerdakşam yemeği uygulamamızı oluşturduğumuzda, uygulama projesiyle birlikte olmak üzere bir birim testi projesi oluşturmak isteyip istemediğinizi soran bir iletişim kutusu sorulduk:

![](enable-automated-unit-testing/_static/image1.png)

Çözümünüze "Nerdakşam. Tests" projesinin eklenmesinden kaynaklanan "Evet, birim test projesi oluştur" radyo düğmesinin seçili olduğunu tutduk:

![](enable-automated-unit-testing/_static/image2.png)

Nerdakşam yemeği. Tests projesi, Nerdakşam yemeği uygulaması proje derlemesine başvurur ve uygulama işlevselliğini doğrulayan buna kolayca otomatikleştirilmiş testler ekleyebilmenizi sağlar.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Akşam yemeği model sınıfımız için birim testleri oluşturma

Şimdi, model katmanımızı oluştururken oluşturduğumuz akşam yemeği sınıfını doğrulayan Nerdakşam yemeği. test projemize bazı testler ekleyelim.

Test projemizde, modellerle ilgili testlerinizi yerleştireceğiniz "modeller" adlı yeni bir klasör oluşturarak başlayacağız. Ardından, klasöre sağ tıklayıp **&gt;yeni test Ekle** menü komutunu seçmelisiniz. Bu, "yeni test Ekle" iletişim kutusunu getirir.

"Birim testi" oluşturup "DinnerTest.cs" olarak adlandırın:

![](enable-automated-unit-testing/_static/image3.png)

"Tamam" düğmesine tıkladığımızda, Visual Studio projeye bir DinnerTest.cs dosyası ekler (ve açar):

![](enable-automated-unit-testing/_static/image4.png)

Varsayılan Visual Studio birim testi şablonu, küçük bir Messy buldum. Yalnızca aşağıdaki kodu içerecek şekilde temizleyelim:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

Yukarıdaki DinnerTest sınıfındaki [TestClass] özniteliği, testleri içerecek bir sınıf olarak ve isteğe bağlı test başlatma ve tearı kodu tanımlar. Üzerinde [TestMethod] özniteliğine sahip ortak yöntemler ekleyerek, içindeki testleri tanımlayabiliriz.

Aşağıda akşam yemeği sınıfınızı sunduğumuz iki testten ilki verilmiştir. İlk test, tüm özellikler doğru şekilde ayarlanmaksızın yeni bir akşam yemeği oluşturulduysa, akşam yemeği 'nin geçersiz olduğunu doğrular. İkinci test, bir akşam yemeği 'nin geçerli değerlerle ayarlanmış tüm özellikleri olduğunda akşam yemeği 'nin geçerli olduğunu doğrular:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

Test adlarımızın çok açık (ve biraz ayrıntılı) olduğunu fark edeceksiniz. Yüzlerce veya binlerce küçük test oluşturduğumuz için bunu yapıyoruz ve bunların her birinin amacını ve davranışını hızlı bir şekilde belirlemeyi kolaylaştırmak istiyoruz (özellikle bir Test Çalıştırıcısı içindeki hataların bir listesini aradığımızda). Test adları, test ettikleri işlevlerden sonra adlandırılmalıdır. Yukarıdaki bir "ad\_\_fiil" adlandırma deseninin kullanılması gerekir.

"Düzenle, davran, onaylama" anlamına gelir ve "AAA" test modelini kullanarak testleri oluşturacağız:

- Düzenle: test edilmekte olan birimi ayarla
- Davran: birimi test ve yakalama sonuçları altında yapın
- Onaylama: davranışı doğrulama

Testleri yazarken, bireysel testlerin çok fazla olmasına engel olmak istiyoruz. Bunun yerine her testin yalnızca tek bir kavram doğrulaması gerekir (Bu, hataların nedenlerini saptamak çok daha kolay hale getirir). Her test için, denemek ve yalnızca tek bir onay bildirimine sahip olmak iyi bir uygulamadır. Bir test yönteminde birden fazla onay deyiminiz varsa, bunların aynı kavramı test etmek için kullanıldığından emin olun. Şüpheli olduğunda başka bir test oluşturun.

### <a name="running-tests"></a>Testleri Çalıştırma

Visual Studio 2008 Professional (ve üzeri sürümler), IDE içinde Visual Studio birim testi projelerini çalıştırmak için kullanılabilen yerleşik bir Test Çalıştırıcısı içerir. Tüm birim testlerimizi çalıştırmak için **&gt;test-&gt;tüm testleri çözüm** menü komutunda (veya CTRL R, A) seçebilirsiniz. Ya da alternatif olarak, imleimizi belirli bir test sınıfı veya test yöntemi içinde konumlandırabiliriz ve birim testlerinin bir alt kümesini çalıştırmak için **geçerli bağlam menü komutunda test&gt;Run-&gt;testlerini** (veya CTRL R, t) kullanabilirsiniz.

Şimdi, yeni tanımladığımız iki testi çalıştırmak için imlecinizi DinnerTest sınıfı içinde konumlandıralım ve "CTRL R, T" yazın. Bunu yaptığımızda, Visual Studio içinde bir "Test Sonuçları" penceresi görünür ve test çalıştırdığımız sonuçları onun içinde listelenmiş olarak görebiliriz:

![](enable-automated-unit-testing/_static/image5.png)

*Not: VS test sonuçları penceresi sınıf adı sütununu varsayılan olarak göstermez. Test Sonuçları penceresinin içine sağ tıklayıp sütunları ekle/kaldır menü komutunu kullanarak bunu ekleyebilirsiniz.*

İki sınamamız yalnızca saniyenin bir kısmını çalıştırtık ve her ikisini de görebilecekleri gibi. Artık, belirli kural doğrulamaları doğrulayan ek sınamalar oluşturarak bunları artırabilir ve bu, akşam yemeği sınıfına eklediğimiz iki yardımcı yöntemi (ısuserhost () ve ıuserregistered ()) kapsar. Dinner Now sınıfı için tüm bu testlerin yerinde olması, gelecekte buna yeni iş kuralları ve doğrulamalar eklemek çok daha kolay ve güvenli hale getirir. Yeni kural mantığımızı akşam yemeği 'ya ekleyebiliriz ve saniyeler içinde önceki Logic işlevlerinden hiçbirini bozmadığını doğrulıyoruz.

Açıklayıcı bir test adı kullanmanın, her sınamanın ne olduğunu hızla öğrenmesini nasıl kolaylaştırdığını unutmayın. **Araçlar-&gt;seçenekler** menü komutunu, test araçları-&gt;test yürütme yapılandırma ekranını açmak ve "başarısız veya sonuçlanmamış birim test sonucunu çift tıklatmak, testteki hata noktasını görüntüler" onay kutusunu işaretleyerek. Bu, test sonuçları penceresinde bir hataya çift tıklamasına ve onaylama hatasına hemen geçebilmenizi sağlar.

### <a name="creating-dinnerscontroller-unit-tests"></a>DinnersController birim testleri oluşturma

Şimdi DinnersController işlevselümüzü doğrulayan bazı birim testleri oluşturalım. Test projemizdeki "denetleyiciler" klasörüne sağ tıklayıp ardından **&gt;yeni test Ekle** menü komutunu seçerek başlayacağız. "Birim testi" oluşturacağız ve "DinnersControllerTest.cs" olarak adlandırın.

DinnersController üzerinde details () eylem yöntemini doğrulayan iki test yöntemi oluşturacağız. Birincisi, var olan bir akşam yemeği istendiğinde bir görünümün döndürüleceğini doğrular. İkincisi, var olmayan bir akşam yemeği istendiğinde "NotFound" görünümünün döndürüldüğünü doğrular:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

Yukarıdaki kod, temizlemeyi derler. Testleri çalıştırdığımızda, her ikisi de başarısız olur:

![](enable-automated-unit-testing/_static/image6.png)

Hata iletilerine baktığımızda, DinnersRepository sınıfımız bir veritabanına bağlanamadığı için testin başarısız olmasının nedenini görüyoruz. Nerdakşam yemeği uygulamamız, Nerdakşam yemeği uygulama projesinin \app\_veri dizininde bulunan bir yerel SQL Server Express dosyasına bağlantı dizesi kullanıyor. Nerdakşam yemeği. Tests projesi farklı bir dizinde derlendiğinden ve çalıştırıldığı için, bağlantı dizemizin göreli yol konumu yanlış.

Bunu, SQL Express veritabanı dosyasını test projemiz olarak kopyalayarak ve ardından test projemizin App. config dosyasında buna uygun bir test bağlantısı dizesi *ekleyerek giderebiliriz* . Bu, yukarıdaki testlerin engeli kaldırılmış ve çalışır durumda olur.

Gerçek bir veritabanı kullanan birim testi kodu, bununla birlikte bir dizi zorluk gösterir. Daha ayrıntılı şekilde belirtmek gerekirse:

- Birim testlerinin yürütme süresini önemli ölçüde yavaşlatır. Testleri çalıştırmak daha uzun sürer, bu da sık sık yürütülecektir. İdeal olarak, birim testlerinizin Saniyeler içinde çalıştırılmasını ve projeyi derlemek için doğal olarak yaptığınız bir şey olmasını istersiniz.
- Testler içindeki kurulum ve Temizleme mantığını karmaşıklaştırır. Her birim testinin diğerlerinden (yan etkileri veya bağımlılıklar olmadan) yalıtılmış ve bağımsız olmasını istiyorsunuz. Gerçek bir veritabanına karşı çalışırken, eyalet olması ve testler arasında sıfırlanması gerekir.

Bu sorunları çözmek için "bağımlılık ekleme" adlı bir tasarım düzenine göz atalım ve testlerimizde gerçek bir veritabanı kullanma gereksinimini ortadan kaldırabilirsiniz.

### <a name="dependency-injection"></a>Bağımlılık Ekleme

Hemen DinnersController, DinnerRepository sınıfına sıkı bir şekilde "bağlanmış". "Kuponu" bir sınıfın çalışması için açıkça başka bir sınıfa bağlı olduğu bir durum anlamına gelir:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

DinnerRepository sınıfı bir veritabanına erişim gerektirdiğinden, DinnersController sınıfının sıkı şekilde bağlanmış bağımlılığı, DinnersController eylem yöntemlerinin test edilmesi için bir veritabanının olmasını gerektirmemizi gerektirir.

Bu sorunu çözmek için "bağımlılık ekleme" adlı bir tasarım deseninin kullanıldığı bir yaklaşım olan, bağımlılıklar (veri erişimi sağlayan depo sınıfları gibi) bunları kullanan sınıflarda artık örtük olarak oluşturulmayacak. Bunun yerine, bağımlılıklar, Oluşturucu bağımsız değişkenleri kullanarak bunları kullanan sınıfa açıkça geçirilebilir. Bağımlılıklar arabirimler kullanılarak tanımlanmışsa, birim testi senaryoları için "sahte" bağımlılık uygulamalarında geçiş esnekliği elde ediyoruz. Bu, gerçekte bir veritabanına erişim gerektirmeyen, teste özel bağımlılık uygulamaları oluşturmamızı sağlar.

Bunu eylemde görmek için DinnersController ile bağımlılık ekleme işlemi uygulayalim.

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository arabirimini ayıklama

İlk adımımız, denetleyicilerimizin Dinerleri almak ve güncelleştirmek için gereken depo sözleşmesini kapsülleyen yeni bir IDinnerRepository arabirimi oluşturmaktır.

Bu arabirim sözleşmesini \Modeller klasörüne sağ tıklayıp ardından **&gt;yeni öğe Ekle** menü komutunu seçerek ve IDinnerRepository.cs adlı yeni bir arabirim oluşturarak el ile tanımlayabiliriz.

Alternatif olarak, var olan DinnerRepository sınıfımızın bir arabirimini otomatik olarak ayıklamak ve oluşturmak için yerleşik Visual Studio Professional (ve sonraki sürümler) yeniden düzenleme araçlarını kullanabiliriz. VS kullanarak bu arabirimi ayıklamak için, imleci DinnerRepository sınıfındaki metin düzenleyicisinde konumlandırın ve sonra sağ tıklayıp yeniden **Düzenle-&gt;ayıklamayı Ayıkla** menü komutunu seçin:

![](enable-automated-unit-testing/_static/image7.png)

Bu, "Arabirimi Ayıkla" iletişim kutusunu başlatacaktır ve oluşturulacak arabirimin adı için bizi ister. IDinnerRepository varsayılan olarak, arabirime eklemek için var olan DinnerRepository sınıfındaki tüm ortak yöntemleri otomatik olarak seçer:

![](enable-automated-unit-testing/_static/image8.png)

"Tamam" düğmesine tıkladığımızda, Visual Studio uygulamamıza yeni bir IDinnerRepository arabirimi ekleyecek:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

Ve var olan DinnerRepository sınıfımız, arabirimini uygulayan şekilde güncelleştirilecektir:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>DinnersController 'i Oluşturucu ekleme işlemini destekleyecek şekilde güncelleştirme

Şimdi, yeni arabirimi kullanmak için DinnersController sınıfını güncelleştireceğiz.

Şu anda DinnersController, "dinnerRepository" alanı her zaman bir DinnerRepository sınıfı olacak şekilde sabit kodludur:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

Bunu, "dinnerRepository" alanı DinnerRepository yerine IDinnerRepository türünde olacak şekilde değiştireceksiniz. Daha sonra iki genel DinnersController Oluşturucusu ekleyeceğiz. Oluşturuculardan biri, bir IDinnerRepository bağımsız değişken olarak geçirilmesine izin verir. Diğeri, var olan DinnerRepository uygulamamızı kullanan varsayılan bir oluşturucudur:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

ASP.NET MVC Varsayılan oluşturucuları kullanarak denetleyici sınıfları oluşturduğundan, çalışma zamanındaki DinnersController, veri erişimi gerçekleştirmek için DinnerRepository sınıfını kullanmaya devam edecektir.

Artık birim testlerimizi güncelleştirebiliriz, ancak parametre oluşturucusunu kullanarak "sahte" bir akşam yemeği depo uygulamasını geçirmek için. Bu "sahte" akşam yemeği deposu gerçek bir veritabanına erişim gerektirmez ve bunun yerine bellek içi örnek verileri kullanır.

#### <a name="creating-the-fakedinnerrepository-class"></a>FakeDinnerRepository sınıfı oluşturma

Bir FakeDinnerRepository sınıfı oluşturalım.

Nerdakşam yemeği. Tests projemizdeki bir "Fakes" dizini oluşturup buna yeni bir FakeDinnerRepository sınıfı ekleyerek başlayacağız (klasöre sağ tıklayıp **Add-&gt;New Class**) ' i seçin:

![](enable-automated-unit-testing/_static/image9.png)

Kodu FakeDinnerRepository sınıfının IDinnerRepository arabirimini uyguladığı şekilde güncelleştireceğiz. Daha sonra, üzerine sağ tıklayıp "arabirim IDinnerRepository Uygula" bağlam menüsü komutunu seçebilirsiniz:

![](enable-automated-unit-testing/_static/image10.png)

Bu, Visual Studio 'nun tüm IDinnerRepository arabirimi üyelerini varsayılan "saplama çıkış" uygulamalarıyla FakeDinnerRepository sınıfımızda otomatik olarak eklemesine neden olur:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

Daha sonra FakeDinnerRepository uygulamasını, bir Oluşturucu bağımsız değişkeni olarak kendisine geçirilen akşam yemeği&gt; koleksiyonu&lt;bir bellek içi listede çalışmak üzere güncelleştirebiliriz:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

Artık bir veritabanı gerektirmeyen sahte bir IDinnerRepository uygulamasıdır ve bunun yerine akşam yemeği nesnelerinin bellek içi bir listesini çalıştırabilirsiniz.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>Birim testleriyle FakeDinnerRepository kullanma

Veritabanı kullanılamadığından daha önce başarısız olan DinnersController birim testlerine geri dönelim. Test yöntemlerini aşağıdaki kodu kullanarak örnek bellek içi akşam yemeği verileriyle birlikte DinnersController ile doldurulmuş bir FakeDinnerRepository kullanacak şekilde güncelleştirebiliriz:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

Şimdi de bu testleri çalıştırdığımızda her iki geçiş de yapılır:

![](enable-automated-unit-testing/_static/image11.png)

En iyisi, yalnızca saniyenin bir kısmını çalıştırırlar ve karmaşık kurulum/Temizleme mantığı gerektirmez. Artık gerçek bir veritabanına bağlanmak zorunda kalmadan tüm DinnersController eylem yöntemi kodumuzu (listeleme, sayfalama, ayrıntılar, oluşturma, güncelleştirme ve silme dahil) test edebilirsiniz.

| **Kenar konusu: bağımlılık ekleme çerçeveleri** |
| --- |
| El ile bağımlılık ekleme (yukarıda yaptığımız gibi) gerçekleştiriyoruz, ancak bir uygulamadaki bağımlılıkların ve bileşenlerin sayısı arttıkça devam etmek daha zor hale gelir. .NET için birçok bağımlılık ekleme çerçevesi, daha da fazla bağımlılık yönetimi esnekliği sağlamaya yardımcı olabilir. Ayrıca, bazen "Control of Control" (IOC) kapsayıcıları olarak da adlandırılan bu çerçeveler, çalışma zamanında nesnelere bağımlılıklar belirtme ve geçirme için ek yapılandırma desteğinin sağlanmasına olanak tanıyan mekanizmalar sağlar (çoğunlukla Oluşturucu Ekleme kullanarak). ). .NET 'teki daha popüler OSS bağımlılığı ekleme/ıOC çerçevelerinden bazıları şunlardır: AutoFac, Neklemesine, Spring.NET, StructureMap ve Wınossor. ASP.NET MVC, geliştiricilerin çözüme ve örneklemesine katılmasını sağlayan ve bağımlılık ekleme/IOC çerçevelerinin bu işlem dahilinde düzgün bir şekilde tümleştirilebilmesi için genişletilebilirlik API 'Leri sunar. Bir dı/ıOC çerçevesinin kullanılması Ayrıca, DinnersController ' dan varsayılan oluşturucuyu kaldırmamızı sağlar; Bu, ile DinnerRepository arasındaki kuponu tamamen kaldırır. Nerdakşam yemeği uygulamamız ile bir bağımlılık ekleme/ıOC çerçevesi kullanmayacağız. Ancak, Nerdakşam yemeği kod tabanı ve özellikleri grew ise gelecek için göz önünde bulundurduğumuz bir şeydir. |

### <a name="creating-edit-action-unit-tests"></a>Düzenleme eylemi birim testlerini oluşturma

Şimdi, DinnersController 'in düzenleme işlevini doğrulayan bazı birim testleri oluşturalım. Düzenleme eylemimizin HTTP-Al sürümünü test ederek başlayacağız:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

Geçerli bir akşam yemeği istendiğinde, bir DinnerFormViewModel nesnesi tarafından desteklenen bir görünümün geri işlenip işlenmeyeceğini doğrulayan bir test oluşturacağız:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

Testi çalıştırdığımızda, düzenleme yöntemi akşam yemeği. ıshostedby () denetimini gerçekleştirmek üzere User.Identity.Name özelliğine eriştiğinde null başvuru özel durumu atıldığı için başarısız olduğunu öğreniyoruz.

Denetleyici temel sınıfındaki Kullanıcı nesnesi, oturum açmış kullanıcıyla ilgili ayrıntıları kapsüller ve çalışma zamanında denetleyici oluşturduğunda ASP.NET MVC tarafından doldurulur. DinnersController 'i bir Web-Server ortamının dışında test ettiğimiz için, Kullanıcı nesnesi ayarlı değil (Bu nedenle, null başvuru özel durumu).

### <a name="mocking-the-useridentityname-property"></a>User.Identity.Name özelliğini moclama

Mocking çerçeveleri, testlerinizi destekleyen bağımlı nesnelerin sahte sürümlerini dinamik olarak oluşturmamızı sağlayarak testi daha kolay hale getirir. Örneğin, DinnersController 'in sanal bir kullanıcı adını aramak için kullanabileceği bir Kullanıcı nesnesini dinamik olarak oluşturmak için düzenleme eylemi testimizde bir sahte işlem çerçevesi kullanabiliriz. Bu, test çalıştırdığımız zaman bir null başvurusunun oluşmasını önler.

ASP.NET MVC ile kullanılabilen birçok .net sahte işlem çerçevesi vardır (bunların bir listesini burada görebilirsiniz: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)). Nerdakşam yemeği uygulamanızı test etmek için, [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)ücretsiz olarak indirilebilen, "moq" adlı açık kaynaklı bir sahte işlem çerçevesi kullanacağız.

İndirildikten sonra, Nerdakşam. test projemizdeki moq. dll derlemesine bir başvuru ekleyeceğiz:

![](enable-automated-unit-testing/_static/image12.png)

Daha sonra bir parametre olarak Kullanıcı adı alan ve daha sonra DinnersController örneğindeki User.Identity.Name özelliğini "bir" CreateDinnersControllerAs (username) "yardımcı yöntemi ekleyeceğiz:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

Yukarıda, bir ControllerContext nesnesini kullanan bir sahte nesne (ASP.NET MVC 'nin Kullanıcı, Istek, yanıt ve oturum gibi çalışma zamanı nesnelerini kullanıma sunmak için denetleyici sınıflarına ne kadar başarılı olduğunu) oluşturmak için moq kullanıyoruz. ControllerContext üzerinde HttpContext.User.Identity.Name özelliğinin yardımcı metoduna geçirdiğimiz Kullanıcı adı dizesini döndürmesi gerektiğini göstermek için, "SetupGet" yöntemini geliştirdik.

Herhangi bir sayıda ControllerContext özelliği ve yöntemi olabilir. Bunu göstermek için, Request. IsAuthenticated özelliği için bir SetupGet () çağrısı ekledik (Bu aslında aşağıdaki testler için gerekli değildir, ancak Istek özelliklerinin nasıl sahte olduğunu göstermeye yardımcı olur). İşiniz bittiğinde, DinnersController yardımcı yöntemimizin döndürdüğü bir ControllerContext 'in bir örneğini atamamız.

Artık, farklı kullanıcılar ile ilgili düzenleme senaryolarını test etmek için bu yardımcı yöntemi kullanan birim testleri yazalım:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

Şimdi, başarılı olan testleri çalıştırdığımızda:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>UpdateModel () senaryolarını test etme

Düzenleme eyleminin HTTP-Al sürümünü kapsayan testler oluşturduk. Şimdi, düzenleme eyleminin HTTP-POST sürümünü doğrulayan bazı sınamalar oluşturalım:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

Bu eylem yöntemiyle desteketmemizi istediğiniz ilginç yeni test senaryosu, denetleyici temel sınıfındaki UpdateModel () yardımcı yönteminin kullanımındır. Bu yardımcı yöntemi, form gönderme değerlerini akşam yemeği nesne örneğimize bağlamak için kullanıyoruz.

Aşağıda, kullanılacak UpdateModel () yardımcı yöntemi için postalanan değerleri nasıl sağlayabiliriz gösteren iki test verilmiştir. Bunu bir FormCollection nesnesi oluşturup doldurarak ve sonra denetleyicideki "ValueProvider" özelliğine atayarak yapacağız.

İlk test, tarayıcıyı başarılı bir şekilde Kaydet ' in Ayrıntılar eylemine yeniden yönlendirildiğini doğrular. İkinci test, geçersiz giriş gönderildiğinde, işlem düzenleme görünümünü bir hata iletisiyle yeniden görüntüler.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>Kaydırmayı test etme

Birim testi denetleyici sınıflarıyla ilgili temel kavramları ele aldık. Uygulamamızın davranışını doğrulayan yüzlerce basit testi kolayca oluşturmak için bu teknikleri kullanabiliriz.

Denetleyicimiz ve model testleriniz gerçek bir veritabanı gerektirmediğinden, bunlar son derece hızlı ve kolay bir şekilde çalışır. Saniyeler içinde yüzlerce otomatik test yürütebilecektir ve yaptığımız bir değişikliğin bir şeyi yapıp yapmadığımızda anında geri bildirim alırsınız. Bu, uygulamamızı sürekli iyileştirme, yeniden düzenleme ve iyileştirmenin güvencesi sağlamasına yardımcı olur.

Testi bu bölümün son konusu olarak ele aldık, ancak test bir geliştirme sürecinin sonunda yapmanız gereken bir şeydir! Aksine, geliştirme sürecinizde otomatik testleri mümkün olduğunca erken yazmanız gerekir. Böylece geliştirme sırasında anında geri bildirimde bulunmanızı sağlar, uygulamanızın kullanım örneği senaryolarınız hakkında daha fazla bilgi almanızı düşünmenize yardımcı olur ve uygulamanızı temiz katmanla ve daha sonra göz önünde bulundurarak tasarlamanıza kılavuzluk eder.

Kitapta daha sonraki bir bölümde test odaklı geliştirme (TDD) ve ASP.NET MVC ile nasıl kullanılacağı ele alınacaktır. TDD, sonuçta elde edilen kodunuzun karşılaacağı testleri ilk yazdığınız yinelemeli bir kodlama uygulamasıdır. TDD ile, uygulamak üzere olduğunuz işlevselliği doğrulayan bir test oluşturarak her bir özelliği başlatın. Öncelikle birim testi yazmak, özelliği net bir şekilde anladığınızdan ve çalışmanın nasıl çalıştığınızdan emin olmanıza yardımcı olur. Yalnızca test yazıldıktan sonra (ve başarısız olduğunu doğruladıktan sonra), test tarafından doğrulanan gerçek işlevselliği uygulayın. Özelliğin nasıl çalışacağından ilgili kullanım durumu hakkında daha fazla zaman harcadığınız için, gereksinimlerin ve ne kadar en iyi şekilde faydalanacağınızı daha iyi anlayabilirsiniz. Uygulama ile işiniz bittiğinde, testi yeniden çalıştırabilir ve özelliğin doğru şekilde çalışıp çalışmadığını anında geri bildirimde bulabilirsiniz. Bölüm 10 ' da TDD daha fazla ele alınacaktır.

### <a name="next-step"></a>Sonraki adım

Bazı son sarmalar açıklamaları.

> [!div class="step-by-step"]
> [Önceki](use-ajax-to-implement-mapping-scenarios.md)
> [İleri](nerddinner-wrap-up.md)
