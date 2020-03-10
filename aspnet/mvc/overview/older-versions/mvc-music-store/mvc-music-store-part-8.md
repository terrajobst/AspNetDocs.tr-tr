---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8\. kısım: Ajax güncelleştirmeleriyle alışveriş sepeti | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, Ajax güncelleştirmeleriyle alışveriş sepetini içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539258"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a>8\. Bölüm: Ajax Güncelleştirmeleriyle Alışveriş Sepeti

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.  
>   
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, Ajax güncelleştirmeleriyle alışveriş sepetini içerir.

Kullanıcıların, kayıt yaptırmadan albümleri sepetlerine yerleştirmelerini sağlar, ancak kullanıma alma işlemini tamamlaması için konuk olarak kaydolmaları gerekir. Alışveriş ve kullanıma alma işlemi iki denetleyicide ayrılacaktır: bir alışveriş sepeti denetleyicisi ve bu, kullanıma alma işlemini işleyen bir kullanıma alma denetleyicisi. Bu bölümdeki alışveriş sepetini kullanmaya başlayacağız, ardından aşağıdaki bölümde kullanıma alma işlemini oluşturacağız.

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>Sepet, sipariş ve OrderDetail model sınıfları ekleme

Alışveriş sepetimiz ve kullanıma alma işlemlerimiz bazı yeni sınıfların kullanımını sağlayacak. Modeller klasörüne sağ tıklayın ve aşağıdaki kodla bir sepet sınıfı (Cart.cs) ekleyin.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

Bu sınıf, şu ana kadar kullandığımız diğerlerine, recordID özelliği için [key] özniteliği dışında oldukça benzer. Sepet öğelerimiz, adsız alışverişe izin vermek için CartId adlı bir dize tanımlayıcısına sahip olacaktır, ancak tablo, recordID adlı bir tamsayı birincil anahtar içerir. Kural gereği, Entity Framework kodu-önce sepet adlı bir tablonun birincil anahtarının CartId veya ID olacağını bekler, ancak bunu yapmak isterseniz ek açıklamalar veya kod aracılığıyla kolayca geçersiz kılabiliriz. Bu, Entity Framework kodda basit kuralları nasıl kullanabileceğimizi gösteren bir örnektir, ancak bu, ne zaman bir kez karşılaştıklarında bunlarla sınırlandırılıyoruz.

Ardından, aşağıdaki kodla bir order class (Order.cs) ekleyin.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

Bu sınıf, bir sipariş için Özet ve teslim bilgilerini izler. Henüz oluşturulamadığımız bir sınıfa bağlı olan bir OrderDetails gezinti özelliği olduğundan, **henüz derlenmez**. Şimdi, aşağıdaki kodu ekleyerek OrderDetail.cs adlı bir sınıf ekleyerek bunu düzeldelim.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

Bir DbSet&lt;sanatçı&gt;de dahil olmak üzere, bu yeni model sınıflarını sunan DbSets 'leri dahil etmek için MusicStoreEntities sınıfımız son bir güncelleştirme yapacağız. Güncelleştirilmiş MusicStoreEntities sınıfı aşağıda gösterildiği gibi görünür.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>Alışveriş sepetini iş mantığını yönetme

Daha sonra, modeller klasöründe ShoppingCart sınıfını oluşturacağız. ShoppingCart modeli, sepet tablosuna veri erişimini işler. Ayrıca, alışveriş sepetinden öğe ekleme ve kaldırma için iş mantığını işleymeyecektir.

Kullanıcıların alışveriş sepetine öğe eklemek için bir hesaba kaydolmaları gerektirmek istediğimiz için, alışveriş sepetine erişirken kullanıcılara geçici bir benzersiz tanımlayıcı (GUID veya genel benzersiz tanımlayıcı kullanarak) atayacağız. Bu KIMLIĞI ASP.NET oturum sınıfını kullanarak depolayacağız.

*Note: ASP.NET oturumu, siteye ayrıldıktan sonra sona ereceği kullanıcıya özgü bilgileri depolamak için uygun bir yerdir. Oturum durumunun kötüye kullanımı daha büyük sitelerde performans etkilerine sahip olsa da, hafif kullanım, tanıtım amacıyla iyi bir şekilde çalışacaktır.*

ShoppingCart sınıfı aşağıdaki yöntemleri kullanıma sunar:

**AddToCart** bir albümü parametre olarak alır ve kullanıcının sepetine ekler. Sepet tablosu her bir albümün miktarını izlediğinden, gerektiğinde yeni bir satır oluşturma veya Kullanıcı zaten bir albümün kopyasını sipariş eden miktarı artırma mantığını içerir.

**Removefromcart** BIR albüm kimliği alır ve kullanıcının sepetinden kaldırır. Kullanıcının sepetine yalnızca bir albümün kopyası varsa, satır kaldırılır.

**Emptycart** bir kullanıcının alışveriş sepetinden tüm öğeleri kaldırır.

**Getcartıtems** , ekran veya Işleme Için cartıtems listesini alır.

**GetCount** , bir kullanıcının alışveriş sepetindeki toplam albüm sayısını alır.

**Gettotal** , sepetteki tüm öğelerin toplam maliyetini hesaplar.

**CreateOrder** , alışveriş sepetini, kullanıma alma aşamasında bir sıraya dönüştürür.

**Getcart** , denetleyicilerimizin bir sepet nesnesi elde etmesine olanak tanıyan statik bir yöntemdir. Kullanıcının oturumundan CartId 'yi okumayı işlemek için **Getcartıd** yöntemini kullanır. Getcartıd yöntemi, kullanıcının oturumunun kullanıcı oturumundan okuyabilmesi için HttpContextBase 'i gerektirir.

Aşağıda, tüm **ShoppingCart sınıfı**verilmiştir:

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModel 'lar

Alışveriş sepeti denetleyicinizin, bazı karmaşık bilgileri, model nesnelerimize düzgün bir şekilde eşlenmeyen görünümlerimize iletmelerini gerekecektir. Modellerimizi görünümlerimize uyacak şekilde değiştirmek istemiyorum; Model sınıfları kullanıcı arabirimini değil, etki alanını temsil etmelidir. Tek bir çözüm, mağaza yöneticisi açılan bilgileriyle yaptığımız gibi, ViewBag sınıfını kullanarak bu bilgileri görünümlerimize geçirmektir, ancak ViewBag aracılığıyla çok fazla bilgi geçirilerek yönetimi zor olur.

Bu, *ViewModel* deseninin kullanıldığı bir çözümdür. Bu model kullanılırken, belirli görünüm senaryolarımız için optimize edilmiş ve görünüm şablonlarımız tarafından gerek duyulan dinamik değerler/içerik özelliklerini sunan kesin türü belirtilmiş sınıflar oluşturuyoruz. Denetleyici sınıflarımız daha sonra bu görünümün en iyi duruma getirilmiş sınıflarını, kullanılacak görünüm şablonumuza yerleştirebilir ve geçirebilir. Bu, Görünüm şablonları içinde tür güvenliği, derleme zamanı denetimi ve düzenleyici IntelliSense 'i sunar.

Alışveriş sepeti denetleyicimizde kullanılmak üzere iki görünüm modeli oluşturacağız: ShoppingCartViewModel kullanıcının alışveriş sepetinin içeriğini tutacağından, bir Kullanıcı bir şeyi kaldırdığında bir sorun çıkardığında, ShoppingCartRemoveViewModel, onay bilgilerini görüntülemek için kullanılacaktır , sepetlerinden.

İşleri düzenli tutmak için projemizin ' ın kökünde yeni bir Viewmodeller klasörü oluşturalım. Projeye sağ tıklayın, Ekle/yeni klasör ' ü seçin.

![](mvc-music-store-part-8/_static/image1.jpg)

Klasör Viewmodellerini adlandırın.

![](mvc-music-store-part-8/_static/image1.png)

Ardından, Viewmodeller klasörüne ShoppingCartViewModel sınıfını ekleyin. İki özelliğe sahiptir: sepet öğelerinin listesi ve sepetteki tüm öğelerin toplam fiyatını tutacak bir ondalık değer.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

Şimdi, aşağıdaki dört özellik ile ShoppingCartRemoveViewModel ' i Viewmodeller klasörüne ekleyin.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>Alışveriş sepeti denetleyicisi

Alışveriş sepeti denetleyicisi üç ana amaca sahiptir: bir sepete öğe ekleme, sepetten öğe kaldırma ve sepetteki öğeleri görüntüleme. Yeni oluşturduğumuz üç sınıfı kullanacaktır: ShoppingCartViewModel, ShoppingCartRemoveViewModel ve ShoppingCart. StoreController ve StoreManagerController 'da olduğu gibi, MusicStoreEntities 'in bir örneğini tutmak için bir alan ekleyeceğiz.

Boş denetleyici şablonunu kullanarak projeye yeni bir alışveriş sepeti denetleyicisi ekleyin.

![](mvc-music-store-part-8/_static/image2.png)

İşte bu, tüm ShoppingCart denetleyicisi. Dizin ve ekleme denetleyicisi eylemleri çok tanıdık görünmelidir. Remove ve CartSummary denetleyici eylemleri, aşağıdaki bölümde ele alacağız iki özel durumu ele alır.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>JQuery ile Ajax güncelleştirmeleri

Daha sonra, ShoppingCartViewModel için kesin olarak belirlenmiş bir alışveriş sepeti Dizin sayfası oluşturacak ve daha önce ile aynı yöntemi kullanarak liste görünümü şablonunu kullanıyor olacaksınız.

![](mvc-music-store-part-8/_static/image3.png)

Ancak, sepetten öğeleri kaldırmak için bir HTML. ActionLink kullanmak yerine, bu görünümdeki HTML sınıfı RemoveLink 'e sahip tüm bağlantılar için tıklama olayını "kullanıma almak" amacıyla jQuery kullanacağız. Formu deftere nakletmek yerine, bu tıklama olayı işleyicisi yalnızca RemoveFromCart Controller eylemmiz için bir AJAX geri araması yapar. RemoveFromCart, jQuery geri çağırduğumuz, daha sonra jQuery kullanarak sayfada dört hızlı güncelleştirme gerçekleştiren JSON serileştirilmiş sonucunu döndürür.

- 1. Silinen albümü listeden kaldırır
- 2. Başlıktaki sepet sayısını güncelleştirir
- 3. Kullanıcıya bir güncelleştirme iletisi görüntüler
- 4. Sepet toplam fiyatını güncelleştirir

Kaldırma senaryosu dizin görünümü içinde bir AJAX geri çağırması tarafından işlendiğinden, RemoveFromCart Action için ek bir görünüm gerekmez. /ShoppingCart/Index görünümü için kodun tamamı aşağıda verilmiştir:

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

Bunu test etmek için, alışveriş sepetimize öğe ekleyebilmemiz gerekiyor. **Mağaza ayrıntıları** görünümümüzü "sepetin Ekle" düğmesi içerecek şekilde güncelleştireceğiz. Bu noktada, bu görünümü son güncelleştirdiğimiz zamandan sonra eklediğimiz bazı albüm ek bilgilerini de dahil eteceğiz: tarz, sanatçı, Fiyat ve albüm resmi. Güncelleştirilmiş mağaza Ayrıntıları görünümü kodu aşağıda gösterildiği gibi görüntülenir.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

Şimdi mağazaya tıklayabilir ve alışveriş sepetimize ve ' ye Albümler ekleme ve kaldırma testi yapabilirsiniz. Uygulamayı çalıştırın ve mağaza dizinine gidin.

![](mvc-music-store-part-8/_static/image4.png)

Ardından, albümler listesini görüntülemek için bir tarz üzerine tıklayın.

![](mvc-music-store-part-8/_static/image5.png)

Bir albüm başlığına tıkladığınızda, "Sepete Ekle" düğmesi de dahil olmak üzere güncelleştirilmiş Albüm Ayrıntıları görünümü görüntülenir.

![](mvc-music-store-part-8/_static/image6.png)

"Sepete Ekle" düğmesine tıklamak, alışveriş sepeti özet listesi ile alışveriş sepeti Dizin görünümümüzü gösterir.

![](mvc-music-store-part-8/_static/image7.png)

Alışveriş sepetinizi yükledikten sonra, alışveriş sepetinize yönelik Ajax güncelleştirmesini görmek için sepeden Kaldır bağlantısına tıklayabilirsiniz.

![](mvc-music-store-part-8/_static/image8.png)

Kayıtsız kullanıcıların sepetlerinde öğe eklemesine izin veren bir çalışan alışveriş sepeti oluşturduk. Aşağıdaki bölümde, kullanıma alma işleminin kaydolmasını ve tamamlanmasına izin vereceğiz.

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-7.md)
> [İleri](mvc-music-store-part-9.md)
