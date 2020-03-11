---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
title: Modelleri, görünümleri ve denetleyicileri anlama (VB) | Microsoft Docs
author: StephenWalther
description: Modeller, görünümler ve denetleyiciler hakkında kafa karıştırılır Bu öğreticide, Stephen Walther, sizi bir ASP.NET MVC uygulamasının farklı bölümlerine tanıtır.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: a106374a-5e74-4fd0-9ac0-1a32280e5d0d
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
msc.type: authoredcontent
ms.openlocfilehash: cc7988e0c9802e8cd376396eb5da15b5393d6088
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600452"
---
# <a name="understanding-models-views-and-controllers-vb"></a>Modelleri, Görünümleri ve Denetleyicileri Anlama (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> Modeller, görünümler ve denetleyiciler hakkında kafa karıştırılır Bu öğreticide, Stephen Walther, sizi bir ASP.NET MVC uygulamasının farklı bölümlerine tanıtır.

Bu öğreticide, ASP.NET MVC modellerine, görünümlerine ve denetleyicilerine yönelik yüksek düzey bir genel bakış sunulmaktadır. Diğer bir deyişle, ASP.NET MVC 'de M ', V ' ve C ' de açıklanmaktadır.

Bu öğreticiyi okuduktan sonra, bir ASP.NET MVC uygulamasının farklı bölümlerinin birlikte nasıl çalıştığını anlamanız gerekir. Ayrıca, bir ASP.NET MVC uygulamasının mimarisinin ASP.NET Web Forms uygulamasından veya Active Server Pages uygulamasından nasıl farklı olduğunu anlamanız gerekir.

## <a name="the-sample-aspnet-mvc-application"></a>Örnek ASP.NET MVC uygulaması

ASP.NET MVC web uygulamaları oluşturmaya yönelik varsayılan Visual Studio şablonu, bir ASP.NET MVC uygulamasının farklı parçalarını anlamak için kullanılabilecek son derece basit bir örnek uygulama içerir. Bu öğreticide bu basit uygulamadan faydalanabilir.

Visual Studio 2008 ' i başlatarak ve menü seçenek dosyası, yeni proje ' yi seçerek MVC şablonuyla yeni bir ASP.NET MVC uygulaması oluşturursunuz (bkz. Şekil 1). Yeni proje iletişim kutusunda, proje türleri altında sık kullandığınız programlama dilini seçin (Visual Basic veya C#) ve şablonlar altında **ASP.NET MVC web uygulaması** ' nı seçin. Tamam düğmesine tıklayın.

[Yeni proje Iletişim kutusunu ![](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)

**Şekil 01**: yeni proje iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-models-views-and-controllers-vb/_static/image2.png))

Yeni bir ASP.NET MVC uygulaması oluşturduğunuzda, **birim test projesi oluştur** iletişim kutusu görüntülenir (bkz. Şekil 2). Bu iletişim kutusu, çözümünüzde ASP.NET MVC uygulamanızı test etmek için ayrı bir proje oluşturmanıza olanak sağlar. Hayır seçeneğini belirleyin **, birim testi projesi oluşturmayın** ve **Tamam** düğmesine tıklayın.

[![birim testi oluştur Iletişim kutusu](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)

**Şekil 02**: birim testi iletişim kutusu oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-models-views-and-controllers-vb/_static/image4.png))

Yeni ASP.NET MVC uygulaması oluşturulduktan sonra. Çözüm Gezgini penceresinde birkaç klasör ve dosya görürsünüz. Özellikle, modeller, görünümler ve denetleyiciler adlı üç klasör görürsünüz. Klasör adlarından tahmin edebilmeniz için, bu klasörler modeller, görünümler ve denetleyiciler uygulamak için dosyaları içerir.

Controllers klasörünü genişletirseniz AccountController. vb adlı bir dosya ve HomeController. vb adlı bir dosya görmeniz gerekir. Görünümler klasörünü genişletirseniz, hesap, giriş ve paylaşılan adlı üç alt klasör görmeniz gerekir. Giriş klasörünü genişletirseniz,. aspx ve Index. aspx adlı iki ek dosya görürsünüz (bkz. Şekil 3). Bu dosyalar, varsayılan ASP.NET MVC şablonuna eklenen örnek uygulamayı yapar.

[Çözüm Gezgini pencereyi ![](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)

**Şekil 03**: Çözüm Gezgini penceresi ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-models-views-and-controllers-vb/_static/image6.png))

**Hata Ayıkla, hata ayıklamayı Başlat**menü seçeneğini belirleyerek örnek uygulamayı çalıştırabilirsiniz. Alternatif olarak F5 tuşuna da basabilirsiniz.

Bir ASP.NET uygulamasını ilk kez çalıştırdığınızda, Şekil 4 ' te iletişim kutusu, hata ayıklama modunu etkinleştirmenizi öneren görünür. Tamam düğmesine tıklayın ve uygulama çalışacaktır.

[![hata ayıklama etkin değil iletişim kutusu](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)

**Şekil 04**: hata ayıklama etkin değil iletişim kutusu ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-models-views-and-controllers-vb/_static/image8.png))

Bir ASP.NET MVC uygulaması çalıştırdığınızda, Visual Studio uygulamayı Web tarayıcınızda başlatır. Örnek uygulama yalnızca iki sayfadan oluşur: Dizin sayfası ve hakkında sayfası. Uygulama ilk kez başladığında Dizin sayfası görünür (bkz. Şekil 5). Uygulamanın sağ üst köşesindeki menü bağlantısına tıklayarak hakkında sayfasına gidebilirsiniz.

[Dizin sayfasını ![](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)

**Şekil 05**: Dizin sayfası ([tam boyutlu görüntüyü görüntülemek için tıklayın](understanding-models-views-and-controllers-vb/_static/image10.png))

Tarayıcınızın adres çubuğundaki URL 'Lere dikkat edin. Örneğin, hakkında menüsü bağlantısına tıkladığınızda, tarayıcı adres çubuğundaki URL, **/Home/about**olarak değişir.

Tarayıcı penceresini kapatır ve Visual Studio 'ya dönerseniz, giriş/hakkında yolunda bir dosya bulamayabileceksiniz. Dosyalar yok. Nasıl bu mümkün mü?

## <a name="a-url-does-not-equal-a-page"></a>Bir URL bir sayfaya eşit değil

Geleneksel bir ASP.NET Web Forms uygulaması veya Active Server Pages uygulaması oluşturduğunuzda, URL ve sayfa arasında bire bir yazışmalar vardır. Sunucudan SomePage. aspx adlı bir sayfa istemeniz halinde, disk üzerinde SomePage. aspx adlı bir sayfa daha iyidir. SomePage. aspx dosyası yoksa, bir **404 sayfa bulunamadı** hatası alırsınız.

Bir ASP.NET MVC uygulaması oluştururken, tarayıcınızın adres çubuğuna yazdığınız URL ile uygulamanızda bulduğunuz dosyalar arasında bir yazışmalar yoktur. Bir ASP.NET MVC uygulamasında, URL, disk üzerindeki bir sayfa yerine bir denetleyici eylemine karşılık gelir.

Geleneksel bir ASP.NET veya ASP uygulamasında, tarayıcı istekleri sayfalarla eşleştirilir. Bir ASP.NET MVC uygulamasında, buna karşılık tarayıcı istekleri denetleyici eylemlerine eşlenir. Bir ASP.NET Web Forms uygulaması içerik merkezli bir uygulamadır. Aksine, uygulama mantığı merkezli bir ASP.NET MVC uygulaması.

## <a name="understanding-aspnet-routing"></a>ASP.NET yönlendirmeyi anlama

Bir tarayıcı isteği, *ASP.net yönlendirme*adlı ASP.NET çerçevesinin bir özelliği aracılığıyla bir denetleyici eylemine eşlenir. ASP.NET yönlendirme, gelen istekleri denetleyici eylemlerine *yönlendirmek* IÇIN ASP.NET MVC çerçevesi tarafından kullanılır.

ASP.NET yönlendirme, gelen istekleri işlemek için bir yol tablosu kullanır. Bu yol tablosu, Web uygulamanız ilk kez başladığında oluşturulur. Yol tablosu, Global. asax dosyasında ayarlanır. Varsayılan MVC Global. asax dosyası listeleme 1 ' de bulunur.

**Listeleme 1-Global. asax**

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample1.vb)]

Bir ASP.NET uygulaması ilk kez başlatıldığında, uygulama\_Start () yöntemi çağrılır. Bu yöntem, liste 1 ' de RegisterRoutes () yöntemini çağırır ve RegisterRoutes () yöntemi varsayılan yol tablosunu oluşturur.

Varsayılan yol tablosu bir rotadan oluşur. Bu varsayılan yol, tüm gelen istekleri üç parçaya ayırır (bir URL segmenti, eğik çizgiler arasındaki herhangi bir şeydir). İlk kesim bir denetleyici adına eşlenir, ikinci segment bir eylem adıyla eşlenir ve son segment ID adlı eyleme geçirilen bir parametreye eşlenir.

Örneğin, aşağıdaki URL 'YI göz önünde bulundurun:

/Product/Details/3

Bu URL, aşağıdaki gibi üç parametreye ayrıştırılır:

Controller = ürün

Eylem = Ayrıntılar

kimlik = 3

Global. asax dosyasında tanımlanan varsayılan yol, üç parametre için varsayılan değerleri içerir. Varsayılan denetleyici ana, varsayılan eylem dizindir ve varsayılan kimlik boş bir dizedir. Bu varsayılan varsayılanlar göz önünde bulundurularak aşağıdaki URL 'nin nasıl ayrıştırılabileceğini düşünün:

/Employee

Bu URL, aşağıdaki gibi üç parametreye ayrıştırılır:

Denetleyici = çalışan

eylem = Dizin

Kimlik =

Son olarak, herhangi bir URL (örneğin, `http://localhost`) vermeden bir ASP.NET MVC uygulaması açarsanız, URL şöyle ayrıştırılır:

denetleyici = ana

eylem = Dizin

Kimlik =

İstek, HomeController sınıfında dizin () eylemine yönlendirilir.

## <a name="understanding-controllers"></a>Denetleyicileri anlama

Bir denetleyici, bir kullanıcının MVC uygulamasıyla etkileşim kurma şeklini denetmaktan sorumludur. Bir denetleyici, bir ASP.NET MVC uygulaması için akış denetim mantığını içerir. Bir denetleyici, bir Kullanıcı bir tarayıcı isteği yaptığında kullanıcıya hangi yanıtın geri gönderileceğini belirler.

Denetleyici yalnızca bir sınıf (örneğin, bir Visual Basic veya C# sınıf). Örnek ASP.NET MVC uygulaması, denetleyiciler klasöründe bulunan HomeController. vb adlı bir denetleyici içerir. HomeController. vb dosyasının içeriği, liste 2 ' de yeniden oluşturulur.

**Listeleme 2-HomeController.cs**

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample2.vb)]

HomeController 'ın Index () ve About () adlı iki yöntemi olduğuna dikkat edin. Bu iki yöntem, denetleyicinin açığa çıkarılan iki eyleme karşılık gelir. /Home/Index URL 'SI HomeController. Index () yöntemini ve/Home/About URL 'sini, HomeController. About () yöntemini çağırır.

Denetleyicideki herhangi bir genel yöntem bir denetleyici eylemi olarak sunulur. Bunun için dikkatli olmanız gerekir. Bu, bir denetleyicide yer alan herhangi bir genel yöntemin, bir tarayıcıya doğru URL 'yi girerek Internet erişimi olan herkes tarafından çağrılabileceği anlamına gelir.

## <a name="understanding-views"></a>Görünümleri anlama

HomeController sınıfı, Index () ve About () tarafından kullanıma sunulan iki denetleyici eylemi, her ikisi de bir görünüm döndürür. Bir görünüm, tarayıcıya gönderilen HTML işaretlemesini ve içeriğini içerir. Bir görünüm, bir ASP.NET MVC uygulamasıyla çalışırken bir sayfanın eşdeğeridir.

Görünümlerinizi doğru yerde oluşturmanız gerekir. HomeController. Index () eylemi aşağıdaki yolda bulunan bir görünüm döndürür:

\Views\Home\Index.aspx

HomeController. About () eylemi aşağıdaki yolda bulunan bir görünüm döndürür:

\Views\Home\About.aspx

Genel olarak, bir denetleyici eylemi için bir görünüm döndürmek istiyorsanız, denetleyicinize aynı adı taşıyan görünümler klasöründe bir alt klasör oluşturmanız gerekir. Alt klasör içinde, denetleyici eylemiyle aynı ada sahip bir. aspx dosyası oluşturmanız gerekir.

Listeleme 3 ' teki dosya about. aspx görünümünü içerir.

**Listeleme 3-hakkında. aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-vb/samples/sample3.aspx)]

Liste 3 ' teki ilk satırı yoksayabilirsiniz, görünümün geri kalanının çoğu standart HTML 'den oluşur. Burada istediğiniz HTML 'yi girerek görünümün içeriğini değiştirebilirsiniz.

Bir görünüm, Active Server sayfalarındaki veya ASP.NET Web Forms bir sayfaya çok benzer. Bir görünüm, HTML içeriği ve betikleri içerebilir. Betikleri, en sevdiğiniz .NET programlama dilinde (örneğin, C# veya Visual Basic .net) yazabilirsiniz. Veritabanı verileri gibi dinamik içerikleri göstermek için betikleri kullanın.

## <a name="understanding-models"></a>Modelleri anlama

Denetleyiciler tartışıyoruz ve görünümleri tartıştık. Tartışımız gereken son konu modelleridir. MVC modeli nedir?

MVC modeli, bir görünümde veya denetleyicide bulunmayan tüm uygulama mantığınızı içerir. Model tüm uygulamanızın iş mantığı, doğrulama mantığı ve veritabanı erişim mantığınızı içermelidir. Örneğin, veritabanınıza erişmek için Microsoft Entity Framework kullanıyorsanız, modeller klasöründe Entity Framework sınıflarınızı (. edmx dosyanız) oluşturursunuz.

Bir görünüm yalnızca Kullanıcı arabirimini oluşturmak için ilgili mantığı içermelidir. Denetleyici, doğru görünümü döndürmek veya kullanıcıyı başka bir eyleme (akış denetimi) yönlendirmek için gereken en az mantığı içermelidir. Başka her şey modelde bulunmalıdır.

Genel olarak, FAT modelleri ve Skinny denetleyicileri için çaba göstermelisiniz. Denetleyici yöntemleriniz yalnızca birkaç satır kod içermelidir. Bir denetleyici eylemi çok FAT alırsa, mantığı modeller klasöründeki yeni bir sınıfa taşımayı göz önünde bulundurmanız gerekir.

## <a name="summary"></a>Özet

Bu öğreticide, ASP.NET MVC web uygulamasının farklı bölümlerine yüksek düzeyde bir genel bakış sunulmaktadır. ASP.NET yönlendirme 'nin gelen tarayıcı isteklerini belirli denetleyici eylemlerine nasıl eşlediğini öğrendiniz. Denetleyicilerin, görünümlerin tarayıcıya nasıl döndürüldüğünü nasıl düzenleyeceğinizi öğrendiniz. Son olarak, modellerin uygulama iş, doğrulama ve veritabanı erişim mantığını nasıl içerdiğini öğrenirsiniz.
