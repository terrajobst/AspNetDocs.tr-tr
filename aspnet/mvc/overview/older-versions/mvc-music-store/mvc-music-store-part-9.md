---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: '9\. Bölüm: kayıt ve kullanıma alma | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 9 ' da kayıt ve kullanıma alma ele alınmaktadır.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559537"
---
# <a name="part-9-registration-and-checkout"></a>9\. Bölüm: Kayıt ve Kasa İşlemleri

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 9 ' da kayıt ve kullanıma alma ele alınmaktadır.

Bu bölümde, alışverişçinin adresini ve ödeme bilgilerini toplayacak bir CheckoutController oluşturacaksınız. Kullanıcıların kullanıma almadan önce sitemizi kaydetmesi gerekir, bu nedenle bu denetleyici yetkilendirme gerektirir.

Kullanıcılar, "kullanıma al" düğmesine tıklayarak alışveriş sepetinden kullanıma alma işlemine gidecektir.

![](mvc-music-store-part-9/_static/image1.jpg)

Kullanıcı oturum açmadıysa, bu kullanıcılara sorulur.

![](mvc-music-store-part-9/_static/image1.png)

Oturum başarıyla tamamlandığında, Kullanıcı Adres ve ödeme görünümü gösterilir.

![](mvc-music-store-part-9/_static/image2.png)

Formu doldurduktan ve siparişi gönderdikten sonra, bu sipariş onay ekranı gösterilir.

![](mvc-music-store-part-9/_static/image3.png)

Varolmayan bir siparişi veya size ait olmayan bir siparişi görüntüleme girişimi hata görünümünü gösterir.

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>Alışveriş sepetini geçirme

Alışveriş süreci anonim olsa da, Kullanıcı kullanıma al düğmesine tıkladığında, kaydolmaları ve oturum açması gerekecektir. Kullanıcılar, alışveriş sepeti bilgilerini ziyaret ettikleri sırada koruduğumuz için, kayıt veya oturum açma bilgilerini tamamladıktan sonra alışveriş sepeti bilgilerini bir kullanıcıyla ilişkilendirmemiz gerekir.

Bu aslında çok basittir çünkü, ShoppingCart sınıfınız zaten geçerli sepetteki tüm öğeleri bir kullanıcı adıyla ilişkilendirecek bir yönteme sahiptir. Bir kullanıcı kayıt veya oturum açma işlemini tamamlarsa bu yöntemi çağıracağız.

Üyelik ve yetkilendirme ayarlamamız sırasında eklediğimiz **accountcontroller** sınıfını açın. MvcMusicStore. modellerine başvuran bir using açıklaması ekleyin ve ardından aşağıdaki MigrateShoppingCart metodunu ekleyin:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

Sonra, aşağıda gösterildiği gibi, Kullanıcı doğrulandıktan sonra MigrateShoppingCart ' ı çağırmak için oturum açma sonrası eylemini değiştirin:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

Kullanıcı hesabı başarıyla oluşturulduktan hemen sonra, kaydı kaydet eyleminde aynı değişikliği yapın:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

Bu, artık başarılı kayıt veya oturum açma işlemi sırasında anonim bir alışveriş sepeti otomatik olarak bir kullanıcı hesabına aktarılır.

## <a name="creating-the-checkoutcontroller"></a>CheckoutController oluşturma

Denetleyiciler klasörüne sağ tıklayın ve boş denetleyici şablonunu kullanarak CheckoutController adlı projeye yeni bir denetleyici ekleyin.

![](mvc-music-store-part-9/_static/image5.png)

İlk olarak, kullanıcıların kullanıma almadan önce kaydolmayı gerektirmek için denetleyici sınıfı bildiriminin üzerine Yetkilendir özniteliğini ekleyin:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*Note: Bu, daha önce StoreManagerController 'a yaptığımız değişikliğe benzerdir, ancak bu durumda Yetkilendir özniteliği kullanıcının yönetici rolünde olması gerekir. Kullanıma alma denetleyicisinde, kullanıcının oturum açmasını ve yöneticiler olmasını gerektirmeyi istiyoruz.*

Kolaylık sağlaması için bu öğreticide ödeme bilgileriyle ilgilenmezsiniz. Bunun yerine, kullanıcıların tanıtım kodu kullanarak kullanıma almalarına izin veririz. Bu promosyon kodunu PromoCode adlı bir sabit kullanarak depolayacağız.

StoreController 'da olduğu gibi, storeDB adlı MusicStoreEntities sınıfının bir örneğini tutmak için bir alan tanımlayacağız. MusicStoreEntities sınıfını kullanabilmeniz için, MvcMusicStore. model ad alanı için bir using ifadesini eklememiz gerekir. Kullanıma alma denetleyicimizin en üstü aşağıda görüntülenir.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController aşağıdaki denetleyici eylemlerine sahip olacaktır:

**Addressandödemeler (get yöntemi)** , kullanıcının bilgilerini girmesine izin veren bir form görüntüler.

**Addressandödemeler (POST yöntemi)** girişi doğrular ve siparişi işler.

Bir Kullanıcı, kullanıma alma işlemini başarıyla tamamladıktan sonra, **tamamlandı** görüntülenir. Bu görünüm kullanıcının sıra numarasını onay olarak içerecektir.

İlk olarak, Dizin denetleyicisi eylemini (denetleyiciyi oluşturduğumuz sırada oluşturulmuştur) adreslemek için yeniden adlandıralım. Bu denetleyici eylemi yalnızca kullanıma alma formunu görüntüler, bu nedenle herhangi bir model bilgisi gerektirmez.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

Addressandödeme POST yöntemi, StoreManagerController 'da kullandığımız aynı düzeni izlemelidir: form gönderimini kabul edip sırayı tamamlamaya çalışır ve başarısız olursa formu yeniden görüntüler.

Form girişi doğrulandıktan sonra bir sipariş için doğrulama gereksinimlerimizi karşılıyorsa, PromoCode form değerini doğrudan denetleriz. Her şeyin doğru olduğu varsayıldığında, güncelleştirilmiş bilgileri sırasıyla kaydedecek, ShoppingCart nesnesine sipariş sürecini tamamlayacak ve tamamlanmış eyleme yönlendireceğiz.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

Kullanıma alma işleminin başarıyla tamamlanmasından sonra, kullanıcılar tüm denetleyiciye yeniden yönlendirilir. Bu eylem, sipariş numarasını onay olarak göstermeden önce siparişin, oturum açmış kullanıcıya ait olduğunu doğrulamak için basit bir denetim gerçekleştirir.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*Note: projeyi başladığımızda, hata görünümü/Views/Shared klasöründe bizim için otomatik olarak oluşturuldu.*

Tüm CheckoutController kodu aşağıdaki gibidir:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>Addressandödeme görünümü ekleme

Şimdi Addressandödeme görünümünü oluşturalım. Addressandödeme denetleyicisi eylemlerinden birine sağ tıklayın ve bir sipariş olarak kesin olarak belirlenmiş olan Addressandödeme adlı bir görünüm ekleyin ve aşağıda gösterildiği gibi düzenleme şablonunu kullanır.

![](mvc-music-store-part-9/_static/image6.png)

Bu görünüm StoreManagerEdit görünümünü oluştururken bakdığımız tekniklerin ikisini de kullanacaktır:

- Sipariş modelinin form alanlarını göstermek için HTML. EditorForModel () kullanacağız
- Doğrulama öznitelikleriyle bir order Class kullanarak doğrulama kurallarından yararlanacağız

Form kodunu, daha sonra promosyon kodu için ek bir TextBox ile HTML. EditorForModel () kullanmak üzere güncelleyerek başlayacağız. Addressandödeme görünümü için kodun tamamı aşağıda gösterilmiştir.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>Sıra için doğrulama kuralları tanımlama

Görünümümüzün ayarlanmış olduğuna göre, daha önce albüm modeliyle yaptığımız için, sipariş modelimiz için doğrulama kurallarını ayarlayacağız. Modeller klasörüne sağ tıklayın ve Order adlı bir sınıf ekleyin. Daha önce albüm için kullandığımız doğrulama özniteliklerine ek olarak, kullanıcının e-posta adresini doğrulamak için de normal bir Ifade kullanacağız.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

Form eksik veya geçersiz bilgilerle gönderilmeye çalışıldığında artık istemci tarafı doğrulaması kullanılarak hata iletisi gösterilecektir.

![](mvc-music-store-part-9/_static/image7.png)

Son olarak, kullanıma alma işlemi için çok fazla iş yaptık. yalnızca birkaç gürültü vardır ve sona erer. İki basit görünüm eklememiz gerekir ve oturum açma işlemi sırasında sepet bilgilerinin iletileden kaynaklanmalıdır.

## <a name="adding-the-checkout-complete-view"></a>Kullanıma alma tamamlanma görünümü ekleniyor

Yalnızca sipariş KIMLIĞINI görüntülemesi gerektiğinden, kullanıma alma tam görünümü oldukça basittir. Tüm denetleyiciyi sağ tıklatın ve tam olarak bir int olarak yazılmış olan adlı bir görünüm ekleyin.

![](mvc-music-store-part-9/_static/image8.png)

Şimdi, aşağıda gösterildiği gibi, sipariş KIMLIĞINI görüntülemek için görünüm kodunu güncelleştireceğiz.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>Hata görünümü güncelleştiriliyor

Varsayılan şablon paylaşılan görünümler klasöründe bir hata görünümü içerir, böylece sitede başka bir yerde yeniden kullanılabilir. Bu hata görünümü çok basit bir hata içeriyor ve site düzenimizi kullanmıyor, bu nedenle güncelleştireceğiz.

Bu genel bir hata sayfası olduğundan, içerik çok basittir. Kullanıcı eylemini yeniden denemek isterse, geçmişteki bir önceki sayfaya gitmek için bir ileti ve bir bağlantı ekleyeceğiz.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-8.md)
> [İleri](mvc-music-store-part-10.md)
