---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: '5\. Bölüm: Iş mantığı | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm bazı iş mantığını ekler.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630307"
---
# <a name="part-5-business-logic"></a>5\. Bölüm: İş Mantığı

[ali Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir. Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.
> 
> Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm bazı iş mantığını ekler.

## <a id="_Toc260221671"></a>Iş mantığı ekleme

Her biri web sitemizi ziyaret ettiğinde alışveriş deneyimimizin kullanılabilir olmasını istiyoruz. Ziyaretçiler, kayıtlı veya oturum açmış olmasalar bile alışveriş sepetini ziyaret edebilir ve bunlara öğe ekleyebilir. Kullanıma hazır olduklarında, kimlik doğrulama seçeneği verilir ve henüz üye değilse, hesap oluşturabileceksiniz.

Bu, alışveriş sepetini anonim bir durumdan "kayıtlı Kullanıcı" durumuna dönüştürmek için mantığı uygulamamız gereken anlamına gelir.

"Classes" adlı bir dizin oluşturalım ve sonra klasöre sağ tıklayıp MyShoppingCart.cs adlı yeni bir "sınıf" dosyası oluşturma

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

Daha önce belirtildiği gibi, MyShoppingCart. aspx sayfasını uygulayan sınıfı genişletireceğiz ve bunu kullanarak yapacağız. NET ' in güçlü "kısmi sınıf" yapısı.

MyShoppingCart.aspx.cf dosyası için oluşturulan çağrı şuna benzer.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

"Partial" anahtar sözcüğünün kullanımını aklınızda edin.

Yeni oluşturduğumuz sınıf dosyası şuna benzer.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

Bu dosyaya kısmi anahtar sözcük ekleyerek uygulamalarımızı birleştiriyoruz.

Yeni sınıf dosyanız artık şuna benzer.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

Sınıfmıza ekleyeceğiniz ilk yöntem "Addidıtem" yöntemidir. Bu, Kullanıcı ürün listesi ve ürün ayrıntıları sayfalarındaki "resimlere Ekle" bağlantılarına tıkladığında sonunda çağrılacaktır.

Aşağıdaki, sayfanın en üstündeki using deyimlerine ekleyin.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

Ve bu yöntemi MyShoppingCart sınıfına ekleyin.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

Öğenin zaten sepette olup olmadığını görmek için LINQ to Entities kullandık. Bu durumda, öğenin sipariş miktarını güncelleştiririz, aksi takdirde seçili öğe için yeni bir giriş oluşturuyoruz

Bu yöntemi çağırmak için, yalnızca bu yöntemi sınıftan olmayan bir AddToCart. aspx sayfası uygulayacağız, sonra da öğe eklendikten sonra geçerli alışverişe bir = sepet görüntülendi.

Çözüm Gezgini ' nde çözüm adına sağ tıklayın ve daha önce yaptığımız gibi AddToCart. aspx adlı yeni bir sayfa ekleyin.

Bu sayfayı, düşük stok sorunları gibi ara sonuçları görüntülemek için kullanabiliriz, ancak uygulamamızda, sayfa aslında işlenmeyecektir, ancak "Ekle" mantığını ve yeniden yönlendirmeyi çağırır.

Bunu gerçekleştirmek için, sayfa\_Load olayına aşağıdaki kodu ekleyeceğiz.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

Bir QueryString parametresinden alışveriş sepetine eklemek ve sınıfınızın AddItem yöntemini çağırmak için ürünü aldığımızdan emin olmanız gerektiğini unutmayın.

Bir hata ile karşılaşılmayan bir şekilde, bir sonraki adımda uygulayacağız olan SHoppingCart. aspx sayfasına geçirilen hiçbir hatayla karşılaşıyoruz. Bir hata olması halinde bir özel durum oluşturuyoruz.

Şu anda genel bir hata işleyicisini uyguladık, bu özel durum uygulamamız tarafından işlenmemiş olacak ancak kısa süre içinde devam edeceğiz.

Ayrıca, hata ayıklama. Fail () ifadesinin kullanımı (`using System.Diagnostics;)` aracılığıyla kullanılabilir)

Uygulamanın hata ayıklayıcı içinde çalışıyor olması, bu yöntemin, uygulama durumu hakkında bilgiler içeren ayrıntılı bir iletişim kutusu görüntüler ve bu durum, belirlediğimiz hata iletisiyle birlikte, uygulamalar durumu hakkında bilgi gösterir.

Üretimde çalışırken Debug. Fail () bildirisi yok sayılır.

"Getshoppingcartıd" alışveriş sepeti sınıfımızda bir yönteme yapılan çağrının üzerine bir çağrı yukarıdaki kodu görürsünüz.

Yöntemi aşağıdaki şekilde uygulamak için kodu ekleyin.

Ayrıca, "Toplam" sepetini görüntüleyebilmemiz için güncelleştirme ve kullanıma alma düğmelerini ve bir etiketi ekledik.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

Şimdi alışveriş sepetimize öğe ekleyebiliriz, ancak bir ürün eklendikten sonra sepeti görüntüleme mantığını uygulamadık.

Bu nedenle, MyShoppingCart. aspx sayfasında, aşağıdaki gibi bir EntityDataSource denetimi ve GridVire denetimi ekleyeceğiz.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

Tasarımcı 'yı Güncelleştir düğmesine çift tıklayarak ve İşaretlemede bildirimde belirtilen Click olay işleyicisini oluşturabilmeniz için formu tasarımcıda çağırın.

Ayrıntıları daha sonra uygulayacağız, ancak bunu yaptığınızda uygulamamızı hatasız olarak derleyip çalıştıralım.

Uygulamayı çalıştırıp alışveriş sepetine bir öğe eklediğinizde bunu görürsünüz.

![](tailspin-spyworks-part-5/_static/image2.jpg)

Üç özel sütun uygulayarak "varsayılan" kılavuz görüntüününden sapdık.

Birincisi, miktar için düzenlenebilir, "bağlantılı" bir alandır:

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

Bir sonraki, satır öğe toplamı (sipariş edilecek miktar) gösteren "hesaplanan" bir sütundur:

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

Son olarak, kullanıcının öğenin alışveriş grafiğinden kaldırılması gerektiğini belirtmek için kullanacağı CheckBox denetimini içeren özel bir sütunu vardır.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

Görebileceğiniz gibi, Order Total satırı boş olduğundan, sipariş toplamını hesaplamak için bir mantık ekleyelim.

Önce MyShoppingCart sınıfımızda bir "GetTotal" yöntemi uygulayacağız.

MyShoppingCart.cs dosyasında aşağıdaki kodu ekleyin.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

Daha sonra sayfa\_Load olay işleyicisine GetTotal yönteminizi çağırabiliriz. Aynı zamanda, alışveriş sepetinin boş olup olmadığını görmek için bir test ekleyeceğiz.

Şimdi alışveriş sepeti boşsa şunu ediniyoruz:

![](tailspin-spyworks-part-5/_static/image4.jpg)

Aksi takdirde, bizim toplamımızı görüyoruz.

![](tailspin-spyworks-part-5/_static/image5.jpg)

Ancak, Bu sayfa henüz tamamlanmadı.

Kaldırma için işaretlenen öğeleri kaldırarak ve yeni miktar değerlerini belirleyerek, Kullanıcı tarafından kılavuzda değiştirilmiş olabileceğinden, alışveriş sepetini yeniden hesaplamak için ek mantığa ihtiyacımız olacak.

Bir Kullanıcı bir öğeyi kaldırmak üzere işaretlediğinde durumu işlemek için MyShoppingCart.cs içindeki alışveriş sepeti sınıfımızın "RemoveItem" yöntemini eklemesini sağlar.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

Şimdi, bir Kullanıcı bir kaliteyi GridView 'da sipariş olacak şekilde değiştirdiğinde, bu, bir yöntemi ele alalım.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

Temel kaldırma ve güncelleştirme özellikleriyle birlikte, veritabanındaki alışveriş sepetini gerçekten güncelleştiren mantığı uygulayabiliriz. (MyShoppingCart.cs)

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

Bu yöntemin iki parametre beklediğini unutmayın. Bunlardan biri, alışveriş sepeti kimliğidir ve diğeri Kullanıcı tanımlı türdeki nesnelerin bir dizisidir.

Bu nedenle, Kullanıcı arabirimi özellikleri üzerinde mantığımız bağımlılığı en aza indirmek için, GridView denetimine doğrudan erişme gereksinimi olmadan, alışveriş sepeti öğelerini kodumuza iletmek üzere kullandığımız bir veri yapısı tanımladık.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

MyShoppingCart.aspx.cs dosyanızda, bu yapıyı Güncelleştir düğümüzde olay işleyicisi ' ne tıklayarak aşağıda bulabilirsiniz. Sepet güncelleştirmesinin yanı sıra sepet toplamı da güncelleştirilecektir.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

Bu kod satırıyla ilgili belirli bir ilgi olduğunu aklınızda edin:

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues (), MyShoppingCart.aspx.cs içinde aşağıdaki gibi uygulayacağız özel bir yardımcı işlevdir.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

Bu, GridView denetimizdeki bağlantılı öğelerin değerlerine erişmenin temiz bir yolunu sağlar. "Öğe kaldır" onay kutusu denetimi bağlanmadı çünkü bu, FindControl () yöntemiyle erişeceğiz.

Projenizin geliştirmesinde bu aşamada, kullanıma alma işlemini uygulamaya hazırız.

Bunu yapmadan önce, üyelik veritabanını oluşturmak ve üyelik deposuna bir kullanıcı eklemek için Visual Studio 'Yu kullanalım.

> [!div class="step-by-step"]
> [Önceki](tailspin-spyworks-part-4.md)
> [İleri](tailspin-spyworks-part-6.md)
