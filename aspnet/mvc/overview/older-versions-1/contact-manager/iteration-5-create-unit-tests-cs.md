---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: 'Yineleme #5 – birim testleri oluşturma (C#) | Microsoft Docs'
author: microsoft
description: Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. O için veri modeli sınıflarınızı ve derleme birimi testlerimizi modelliyoruz...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: 32e81cce34a0e0b1f6b01934334e1b66dce89651
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544305"
---
# <a name="iteration-5--create-unit-tests-c"></a>Yineleme #5 – birim testleri oluşturma (C#)

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. Denetleyicilerimizin ve doğrulama mantığımız için veri modeli Sınıflarımızı ve derleme birimi testlerini modelliyoruz.

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

Contact Manager uygulamasının önceki yinelemesinde, uygulamanın daha gevşek bir şekilde bağlanmış yeniden düzenlenmiş. Uygulamayı ayrı denetleyicide, hizmette ve depo katmanlarında ayırdık. Her katman, arabirimler aracılığıyla bunun altındaki katmanla etkileşime girer.

Uygulamayı, uygulamayı daha kolay hale getirmek ve değiştirmek için yeniden düzenlenmiş. Örneğin, yeni bir veri erişim teknolojisi kullanmanız gerekiyorsa, yalnızca denetleyiciye veya hizmet katmanına dokunmadan depo katmanını değiştirebiliriz. Iletişim yöneticisini gevşek olarak kaydederek uygulamanın değiştirilmesini daha dayanıklı hale getirdik.

Ancak, Contact Manager uygulamasına yeni bir özellik eklememiz gerektiğinde ne olur? Ya da bir hatayı düzelttiğimiz zaman ne olur? Bir üzgün, ancak iyi kanıtlanmış, kod yazma, yeni hatalara giriş riskini her seferinde oluşturduğunuz zaman, kod yazmanın gerçeği.

Örneğin, bir gün boyunca yöneticiniz, Contact Manager 'a yeni bir özellik eklemenizi isteyebilir. Kişi grupları için destek eklemenizi istiyor. Kullanıcıların kendi kişilerini arkadaşlar, Iş ve benzeri gruplar halinde düzenlemesini olanaklı hale etkinleştirmenizi istiyor.

Bu yeni özelliği uygulamak için, Contact Manager uygulamasının üç katmanını de değiştirmeniz gerekir. Denetleyicilere, hizmet katmanına ve depoya yeni işlevsellik eklemeniz gerekir. Kodu değiştirmeye başladığınızda, daha önce çalışan işlevselliği bozun.

Uygulamamızı, önceki yinelemede yaptığımız gibi ayrı katmanlara yeniden düzenleme işlemi iyi bir şeydir. Uygulamanın geri kalanına dokunmadan tüm katmanlarda değişiklik yapmamızı sağladığından, bu iyi bir şeydir. Ancak, bir katmandaki kodun bakım ve değiştirme işlemlerini daha kolay hale getirmek istiyorsanız, kod için birim testleri oluşturmanız gerekir.

Tek bir kod birimini test etmek için bir birim testi kullanırsınız. Bu kod birimleri tüm uygulama katmanlarından daha küçüktür. Genellikle, kodunuzda belirli bir yöntemin istediğiniz şekilde davranıp davranmadığını doğrulamak için bir birim testi kullanırsınız. Örneğin, ContactManagerService sınıfı tarafından kullanıma sunulan CreateContact () yöntemi için bir birim testi oluşturacaksınız.

Bir uygulama için birim testleri, tıpkı bir güvenlik ağı gibi çalışır. Bir uygulamadaki kodu değiştirdiğinizde, değişikliğin var olan işlevleri kesip bölmediğini denetlemek için bir birim testleri kümesi çalıştırabilirsiniz. Birim testleri, kodunuzun değişiklik yapmasını güvenli hale getirir. Birim testleri, uygulamanızdaki tüm kodun değiştirilmesini daha dayanıklı hale getirir.

Bu yinelemede, Ilgili kişi Yöneticisi uygulamamıza birim testleri ekleyeceğiz. Bu şekilde, bir sonraki yinelemede, mevcut işlevselliği bozmadan uygulamamıza kişi grupları ekleyebiliriz.

> [!NOTE] 
> 
> NUnit, xUnit.net ve MbUnit dahil olmak üzere çeşitli birim testi çerçeveleri vardır. Bu öğreticide, Visual Studio ile birlikte gelen birim testi çerçevesini kullanırız. Ancak, bu alternatif çerçevelerden yalnızca birini kolayca kullanabilirsiniz.

## <a name="what-gets-tested"></a>Nelerin test edileceği

Kusursuz dünyada tüm kodunuzun birim testleri kapsamına alınır. Mükemmel dünyada, mükemmel bir güvenlik ağı vardır. Uygulamanızdaki herhangi bir kod satırını değiştirebilir ve değişiklik, birim testlerinizi yürüterek anında, bu değişikliğin var olan işlevleri değiştirip edemeyeceğini görebilir.

Ancak, mükemmel bir dünyada yaşıyoruz. Uygulamada, birim testlerini yazarken iş mantığınızı (örneğin, doğrulama mantığı) yazmaya odaklanabilirsiniz. Özellikle, veri erişim mantığınızın veya görünüm mantığınızın birim *testlerini yazmayın* .

Yararlı olması için birim testlerinin çok çabuk yürütülmesi gerekir. Bir uygulama için yüzlerce (veya hatta binlerce) birim testlerini kolayca birikmesini sağlayabilirsiniz. Birim testlerinin çalışması uzun zaman alıyorsa, bunları yürütmemeye özen gösterin. Diğer bir deyişle, uzun süre çalışan birim testleri gün-gün kodlama amaçları için yararsızdır.

Bu nedenle, genellikle bir veritabanıyla etkileşim kuran kod için birim testleri yazmayın. Canlı bir veritabanına karşı yüzlerce birim testi çalıştırmak çok yavaş olur. Bunun yerine, veritabanınızı modellemekte ve sahte veritabanıyla etkileşim kuran kodu yazarsınız (aşağıdaki bir veritabanının bir listesini ele aldık).

Benzer bir nedenden dolayı, genellikle görünümler için birim testleri yazmayın. Bir görünümü test etmek için bir Web sunucusu başlatmalısınız. Bir Web sunucusunu kurmak görece yavaş bir işlem olduğundan, Görünümleriniz için birim testleri oluşturmanız önerilmez.

Görünümleriniz karmaşık mantık içeriyorsa, mantığı yardımcı yöntemlere taşımayı göz önünde bulundurmanız gerekir. Bir Web sunucusu koymadan yürütülen yardımcı yöntemler için birim testleri yazabilirsiniz.

> [!NOTE] 
> 
> Veri erişim mantığı veya görüntüleme mantığı için testler yazılırken, birim testlerini yazarken iyi bir fikir değildir. Bu testler, işlevsel veya tümleştirme testleri oluşturulurken çok değerli olabilir.

> [!NOTE] 
> 
> ASP.NET MVC Web Forms görünüm altyapısıdır. Web Forms Görünüm altyapısı bir Web sunucusuna bağımlı olsa da, diğer görünüm motorları olmayabilir.

## <a name="using-a-mock-object-framework"></a>Bir sahte nesne çerçevesi kullanma

Birim testlerini oluştururken neredeyse her zaman bir sahte nesne çerçevesinin avantajlarından faydalanabilirsiniz. Bir sahte nesne çerçevesi, uygulamanızdaki sınıflar için molar ve saplamalar oluşturmanızı sağlar.

Örneğin, bir sahte nesne çerçevesini kullanarak depo sınıfınızın bir sahte sürümünü oluşturabilirsiniz. Bu şekilde, birim testlerinizde gerçek depo sınıfı yerine sahte depo sınıfını kullanabilirsiniz. Sahte deponun kullanılması, birim testini yürütürken veritabanı kodu yürütmeyi önlemenize olanak sağlar.

Visual Studio, bir sahte nesne çerçevesi içermez. Ancak, .NET Framework için kullanılabilen çeşitli ticari ve açık kaynaklı sahte nesne çerçeveleri vardır:

1. Moq-bu çerçeve, açık kaynak BSD lisansı altında bulunabilir. [https://code.google.com/p/moq/](https://code.google.com/p/moq/)'Den moq indirebilirsiniz.
2. Rhino mol 'ler-bu çerçeve, açık kaynak BSD lisansı altında bulunur. [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)Rhino moaltını indirebilirsiniz.
3. Typesahte ısotor-bu ticari bir çerçevedir. [http://www.typemock.com/](http://www.typemock.com/)bir deneme sürümü indirebilirsiniz.

Bu öğreticide moq kullanmaya karar verdim. Ancak, Iletişim Yöneticisi uygulaması için sahte nesneler oluşturmak üzere Rhino Molılar veya Typelıl ısotor 'ı kolayca kullanabilirsiniz.

Moq 'yi kullanabilmeniz için aşağıdaki adımları gerçekleştirmeniz gerekir:

1. arasında yetersiz alanla karşılaştı.
2. İndirmeyi sıkıştırmayı açmadan önce, dosyaya sağ tıklayın ve **Engellemeyi kaldır** etiketli düğmeye tıklayın (bkz. Şekil 1).
3. İndirmeyi sıkıştırmayı açın.
4. ContactManager ' daki başvurular klasörüne sağ tıklayarak moq derlemesine bir başvuru ekleyin. test projesi ve **Başvuru Ekle**' yi seçin. Gözden geçirme sekmesinde, moq 'yi sıkıştırmamışın ve moq. dll derlemesini seçin. **Tamam** düğmesine tıklayın.
5. Bu adımları tamamladıktan sonra, başvurular klasörünüz Şekil 2 gibi görünmelidir.

[Moq engellemesini ![](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**Şekil 01**: MOQ engellemesini kaldırma ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-5-create-unit-tests-cs/_static/image2.png))

[Moq eklendikten sonra başvuruları ![](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**Şekil 02**: MOQ eklendikten sonra başvurular ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-5-create-unit-tests-cs/_static/image4.png))

## <a name="creating-unit-tests-for-the-service-layer"></a>Hizmet katmanı için birim testleri oluşturma

, Contact Manager uygulama s hizmet katmanımız için bir birim testleri kümesi oluşturarak başlayalım. Doğrulama mantığımızı doğrulamak için bu testleri kullanacağız.

ContactManager. Tests projesinde modeller adlı yeni bir klasör oluşturun. Ardından modeller klasörüne sağ tıklayın ve **Ekle, yeni test**' i seçin. Şekil 3 ' te gösterilen **Yeni Test Ekle** iletişim kutusu görünür. **Birim testi** şablonunu seçin ve yeni test ContactManagerServiceTest.cs olarak adlandırın. Yeni testinizi test projenize eklemek için **Tamam** düğmesine tıklayın.

> [!NOTE] 
> 
> Genel olarak, test projenizin klasör yapısını ASP.NET MVC projenizin klasör yapısıyla eşleşecek şekilde istersiniz. Örneğin, denetleyici testlerini bir denetleyiciler klasörüne yerleştirirken, bir modeller klasöründeki testleri modelleyebilir ve bu şekilde devam edersiniz.

[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**Şekil 03**: Models\contactmanagerservicetest.cs ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-5-create-unit-tests-cs/_static/image6.png))

Başlangıçta, ContactManagerService sınıfı tarafından kullanıma sunulan CreateContact () yöntemini test etmek istiyoruz. Aşağıdaki beş testi oluşturacağız:

- CreateContact ()-yöntemi, geçerli bir kişi yöntemine geçirildiğinde, CreateContact () tarafından true değeri döndüren testler.
- CreateContactRequiredFirstName ()-adı eksik olan bir kişi CreateContact () yöntemine geçirildiğinde model durumuna bir hata iletisi eklendiğini sınar.
- CreateContactRequiredLastName ()-eksik bir son ada sahip bir kişi CreateContact () yöntemine geçirildiğinde, model durumuna bir hata iletisi eklendiğini sınar.
- Createcontactınvalidphone ()-geçersiz telefon numarası olan bir kişi CreateContact () yöntemine geçirildiğinde model durumuna bir hata iletisi eklendiğini sınar.
- Createcontactınvalidemail ()-geçersiz bir e-posta adresine sahip bir kişi CreateContact () yöntemine geçirildiğinde model durumuna bir hata iletisi eklendiğini sınar.

İlk test geçerli bir kişinin doğrulama hatası üretmadığını doğrular. Kalan sınamalar, doğrulama kurallarının her birini denetler.

Bu testlerin kodu, liste 1 ' de yer alır.

**Listeleme 1-Models\ContactManagerServiceTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]

Liste 1 ' de Iletişim sınıfını kullandığımız için, test projemizdeki Microsoft Entity Framework bir başvuru eklememiz gerekiyor. System. Data. Entity derlemesine bir başvuru ekleyin.

Listeleme 1, [TestInitialize] özniteliğiyle donatılmış Initialize () adlı bir yöntem içerir. Bu yöntem, birim testlerinin her biri çalıştırılmadan önce otomatik olarak çağrılır (birim testlerinin her biri 5 kez doğru olarak adlandırılır). Initialize () yöntemi aşağıdaki kod satırıyla bir sahte depo oluşturur:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

Bu kod satırı IContactManagerRepository arabiriminden bir sahte depo oluşturmak için moq çerçevesini kullanır. Her birim testi çalıştırıldığında veritabanına erişmeyi önlemek için gerçek EntityContactManagerRepository yerine sahte depo kullanılır. Sahte depo, ıtactmanagerrepository arabiriminin yöntemlerini uygular, ancak Yöntemler aslında hiçbir şey yapmaz.

> [!NOTE] 
> 
> Moq çerçevesini kullanırken, \_mockRepository ve \_mockRepository. Object arasında bir ayrım vardır. İlki, sahte deponun nasıl davrandığını belirtmeye yönelik yöntemleri içeren ıtactmanagerrepository&gt; sınıfına&lt;başvurur. İkincisi, ıtactmanagerrepository arabirimini uygulayan gerçek sahte depoyu ifade eder.

Sahte depo, ContactManagerService sınıfının bir örneği oluşturulurken Initialize () yönteminde kullanılır. Bireysel birim testlerinin tümü, ContactManagerService sınıfının bu örneğini kullanır.

Listeleme 1, birim testlerinin her birine karşılık gelen beş yöntem içerir. Bu yöntemlerin her biri [TestMethod] özniteliğiyle donatılmıştır. Birim testlerini çalıştırdığınızda, bu özniteliğe sahip herhangi bir yöntem çağrılır. Diğer bir deyişle, [TestMethod] özniteliğiyle donatılmış herhangi bir yöntem bir birim sınamadır.

CreateContact () adlı ilk birim testi, bir kişi sınıfının geçerli bir örneği yöntemine geçirildiğinde true değerini döndürür. Test, Contact sınıfının bir örneğini oluşturur, CreateContact () yöntemini çağırır ve CreateContact () öğesinin true değerini döndürdüğünü doğrular.

Kalan sınamalar, CreateContact () yöntemi geçersiz bir kişi ile çağrıldığında yöntemin false döndüğü ve model durumuna beklenen doğrulama hatası iletisinin eklendiği doğrular. Örneğin, CreateContactRequiredFirstName () testi, FirstName özelliği için boş bir dize ile birlikte kişi sınıfının bir örneğini oluşturur. Ardından, CreateContact () yöntemi geçersiz kişi ile çağırılır. Son olarak, test CreateContact () işlevinin yanlış döndürdüğünü ve model durumunun beklenen doğrulama hatası iletisini içerdiğini doğrular "Ilk ad gereklidir."

**Test, Çalıştır, Çözümdeki tüm testler (CTRL + R, A)** menü seçeneğini belirleyerek, liste 1 ' de birim testlerini çalıştırabilirsiniz. Testlerin sonuçları Test Sonuçları penceresinde görüntülenir (bkz. Şekil 4).

[![Test Sonuçları](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**Şekil 04**: test sonuçları ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-5-create-unit-tests-cs/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>Denetleyiciler için birim testleri oluşturma

ASP. NETMVC uygulaması kullanıcı etkileşiminin akışını denetler. Bir denetleyiciyi sınarken, denetleyicinin doğru eylem sonucunu döndürüp döndürmeyeceğini ve verileri görüntülemesini test etmek istersiniz. Ayrıca, bir denetleyicinin model sınıflarıyla beklenen şekilde etkileşimde bulunup çalışmadığını test etmek isteyebilirsiniz.

Örneğin, liste 2, Iletişim denetleyicisi oluşturma () yöntemi için iki birim testi içerir. İlk birim testi, Create () yöntemine geçerli bir kişi geçirildiğinde, Create () yöntemi dizin eylemine yeniden yönlendirdiğini doğrular. Diğer bir deyişle, geçerli bir kişi geçirildiğinde, Create () yöntemi, Dizin eylemini temsil eden bir RedirectToRouteResult döndürmelidir.

Denetleyici katmanını test ettiğimiz zaman ContactManager hizmet katmanını test etmek istemiyorum. Bu nedenle, hizmet katmanını Initialize yönteminde aşağıdaki kodla geliştirdik:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

CreateValidContact () birim testinde, Service Layer CreateContact () yöntemini aşağıdaki kod satırıyla çağırma davranışını geliştirdik:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

Bu kod satırı,, The The The The The The The The The The The The The The The The The The The The The The The The The Hizmet katmanını düzenleyerek, hizmet katmanında herhangi bir kod yürütmeye gerek kalmadan denetleyicimizin davranışını test edebilirsiniz.

İkinci birim testi, yöntemine geçersiz bir kişi geçirildiğinde Create () eyleminin oluştur görünümünü döndürdüğünü doğrular. Service Layer CreateContact () yönteminin aşağıdaki kod satırıyla false değerini döndürmesine neden olur:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

Eğer Create () yöntemi beklediğimiz gibi davrandığı için, hizmet katmanı false değerini döndürdüğünde oluştur görünümünü döndürmelidir. Bu şekilde, denetleyici, doğrulama hata iletilerini oluştur görünümünde görüntüleyebilir ve Kullanıcı geçersiz Iletişim özelliklerini düzeltme şansı verebilir.

Denetleyicileriniz için birim testleri oluşturmayı planlıyorsanız, denetleyici eylemlerinizden açık görünüm adlarını geri dönebilmeniz gerekir. Örneğin, şöyle bir görünüm döndürmeyin:

dönüş görünümü ();

Bunun yerine, görünümü şöyle döndürün:

dönüş görünümü ("Oluştur");

Bir görünümü döndürürken açık değilseniz ViewResult. ViewName özelliği boş bir dize döndürür.

**Listeleme 2-Controllers\ContactControllerTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>Özet

Bu yinelemede, Contact Manager uygulamamız için birim testleri oluşturduk. Uygulamamızın hala beklediğimiz şekilde davrandığını doğrulamak için, bu birim testlerini dilediğiniz zaman çalıştırabiliriz. Birim testleri uygulamamız için bir güvenlik ağı işlevi görür ve gelecekte uygulamamızı güvenle değiştirmenize imkan tanır.

İki birim testi kümesi oluşturduk. İlk olarak, hizmet katmanımız için birim testleri oluşturarak doğrulama mantığımızı test ediyoruz. Daha sonra, denetleyici katmanımız için birim testleri oluşturarak Flow denetim mantığımızı test ediyoruz. Hizmet katmanımızı test ederken, depo katmanımızı inceleyerek hizmet katmanımız için test etmemiz için, depo katmanımızda bulunan testlerimizi yalıdık. Denetleyici katmanını sınarken, hizmet katmanını düzenleyerek denetleyici katmanımız testlerimizi yalıdık.

Bir sonraki yinelemede, kişi gruplarını desteklemesi için Contact Manager uygulamasını değiştiririz. Bu yeni işlevselliği, test odaklı geliştirme adlı bir yazılım tasarımı işlemini kullanarak uygulamamıza ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](iteration-4-make-the-application-loosely-coupled-cs.md)
> [İleri](iteration-6-use-test-driven-development-cs.md)
