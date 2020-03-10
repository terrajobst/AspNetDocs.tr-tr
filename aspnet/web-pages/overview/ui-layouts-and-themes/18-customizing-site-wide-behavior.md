---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: ASP.NET Web Pages (Razor) siteleri için site genelinde davranışı özelleştirme | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, yalnızca bir sayfa yerine tüm Web sitenizde veya bir klasörün tamamına yönelik ayarların nasıl yapılacağı açıklanmaktadır.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634626"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) siteleri için site genelinde davranışı özelleştirme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, ASP.NET Web Pages (Razor) Web sitesinde sayfalar için site tarafı ayarlarının nasıl yapılacağı açıklanır.
> 
> Öğrenecekleriniz:
> 
> - Bir sitedeki tüm sayfalar için değerleri (genel değerler veya Yardım ayarları) ayarlamanıza olanak tanıyan kodu çalıştırma.
> - Bir klasördeki tüm sayfalar için değerleri ayarlamanıza olanak tanıyan kodu çalıştırma.
> - Bir sayfa yüklenmeden önce ve sonra kodu çalıştırma.
> - Merkezi hata sayfasına hata gönderme.
> - Bir klasördeki tüm sayfalara kimlik doğrulaması ekleme.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 3
> - ASP.NET Web yardımcıları kitaplığı (NuGet paketi)
>   
> 
> Bu öğretici, ASP.NET Web yardımcıları kitaplığını kullanana ASP.NET Web sayfaları 3 ve Visual Studio 2013 (Visual Studio Express veya Web için 2013) ile de kullanılabilir.

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>ASP.NET Web sayfaları için Web sitesi başlangıç kodu ekleme

ASP.NET Web sayfalarına yazdığınız kodun büyük bölümü için, tek bir sayfa, Bu sayfa için gereken tüm kodu içerebilir. Örneğin, bir sayfa bir e-posta iletisi gönderirse, bu işlem için tüm kodu tek bir sayfada yerleştirmek mümkündür. Bu, e-posta gönderme (SMTP sunucusu için) ve e-posta iletisini gönderme ayarlarını başlatacak kodu içerebilir.

Ancak bazı durumlarda, sitedeki herhangi bir sayfanın çalıştırılmadan önce bazı kodlar çalıştırmak isteyebilirsiniz. Bu, sitede herhangi bir yerde kullanılabilecek değerleri ayarlamak için yararlıdır ( *genel değerler*olarak adlandırılır.) Örneğin, bazı yardımcılar e-posta ayarları veya hesap anahtarları gibi değerler sağlamanızı gerektirir. Bu ayarları genel değerlerde tutmak yararlı olabilir.

Bunu, site kökünde *AppStart. cshtml\_* adlı bir sayfa oluşturarak yapabilirsiniz. Bu sayfa varsa, sitede herhangi bir sayfa istendiğinde ilk kez çalışır. Bu nedenle, genel değerleri ayarlamak için kodu çalıştırmak iyi bir yerdir. ( *\_AppStart. cshtml* 'nin bir alt çizgi öneki olduğundan, ASP.net doğrudan istekte bulunsa bile sayfayı tarayıcıya göndermez.)

Aşağıdaki diyagramda *\_AppStart. cshtml* sayfasının nasıl çalıştığı gösterilmektedir. Bir sayfa için bir istek geldiğinde ve bu, sitedeki herhangi bir sayfa için ilk istek ise, ASP.NET önce *\_AppStart. cshtml* sayfasının var olup olmadığını denetler. Bu durumda, *\_AppStart. cshtml* sayfasındaki tüm kodlar çalışır ve sonra istenen sayfa çalışır.

![görüntüyle](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>Web siteniz için genel değerleri ayarlama

1. WebMatrix Web sitesinin kök klasöründe *\_AppStart. cshtml*adlı bir dosya oluşturun. Dosya, sitenin kökünde olmalıdır.
2. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    Bu kod, sitedeki tüm sayfalar için otomatik olarak kullanılabilen `AppState` sözlüğünde bir değer depolar. *\_AppStart. cshtml* dosyasında hiçbir biçimlendirme olmadığından emin olun. Sayfa kodu çalıştırır ve ardından başlangıçta istenen sayfaya yönlendirilir.

    > [!NOTE]
    > *\_AppStart. cshtml* dosyasına kod yerleştirdiğinizde dikkatli olun. *\_AppStart. cshtml* dosyasındaki kodda herhangi bir hata oluşursa, Web sitesi başlatılmaz.
3. Kök klasörde, *appname. cshtml*adlı yeni bir sayfa oluşturun.
4. Varsayılan biçimlendirmeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    Bu kod, *\_AppStart. cshtml* sayfasında ayarladığınız `AppState` nesnesinden değeri ayıklar.
5. *Appname. cshtml* sayfasını bir tarayıcıda çalıştırın. (Çalıştırmadan önce sayfanın **dosyalar** çalışma alanında seçili olduğundan emin olun.) Sayfa, genel değeri görüntüler. 

    ![görüntüyle](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>Yardımcılar için değerleri ayarlama

*\_AppStart. cshtml* dosyası için iyi bir kullanım, sitenizde kullandığınız ve başlatılması gereken yardımcıların değerlerini ayarlamanıza yöneliktir. Tipik örnekler, `WebMail` Yardımcısı için e-posta ayarları ve `ReCaptcha` Yardımcısı için özel ve genel anahtarlardır. Bunlar gibi durumlarda, değerleri *AppStart. cshtml\_* bir kez ayarlayabilir ve ardından sitenizdeki tüm sayfalar için önceden ayarlanmıştır.

Bu yordamda `WebMail` ayarlarının küresel olarak nasıl ayarlanacağı gösterilmektedir. (`WebMail` Yardımcısını kullanma hakkında daha fazla bilgi için bkz. [ASP.NET Web Pages sitesine e-posta ekleme](../getting-started/11-adding-email-to-your-web-site.md).)

1. ASP.NET Web yardımcıları kitaplığını, daha önce eklemediyseniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)başlığı altında açıklandığı gibi Web sitenize ekleyin.
2. Zaten bir *\_AppStart. cshtml* dosyanız yoksa bir Web sitesinin kök klasöründe *\_AppStart. cshtml*adlı bir dosya oluşturun.
3. Aşağıdaki `WebMail` ayarlarını *\_AppStart. cshtml* dosyasına ekleyin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    Koddaki aşağıdaki e-posta ile ilgili ayarları değiştirin:

   - `your-SMTP-host`, erişiminiz olan SMTP sunucusunun adına ayarlayın.
   - `your-user-name-here`, SMTP sunucusu hesabınızın kullanıcı adına ayarlayın.
   - SMTP sunucusu hesabınızın parolasını `your-account-password` ayarlayın.
   - `your-email-address-here` kendi e-posta adresinizi ayarlayın. Bu, iletinin gönderildiği e-posta adresidir. (Bazı e-posta sağlayıcıları farklı bir `From` adresi belirtmenize izin vermez ve Kullanıcı adınızı `From` adresi olarak kullanır.)

     SMTP ayarları hakkında daha fazla bilgi [için bkz.](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) [ASP.NET Web Pages (Razor) sitesinden e-posta gönderme](https://go.microsoft.com/fwlink/?LinkID=202899) ve [ASP.NET Web Pages (Razor) sorun giderme kılavuzunda](https://go.microsoft.com/fwlink/?LinkId=253001)e [-posta gönderme sorunları](https://go.microsoft.com/fwlink/?LinkId=253001#email) .
4. *\_AppStart. cshtml* dosyasını kaydedin ve kapatın.
5. Bir Web sitesinin kök klasöründe, *TestEmail. cshtml*adlı yeni bir sayfa oluşturun.
6. Var olan içeriği aşağıdaki ile değiştirin: 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. *TestEmail. cshtml* sayfasını bir tarayıcıda çalıştırın.
8. Kendinize bir e-posta iletisi göndermek için alanları doldurup **Gönder**' e tıklayın.
9. İletiyi aldığınızdan emin olmak için e-postanızı kontrol edin.

Bu örneğin önemli bölümü, genellikle değiştirmediğiniz ayarların (SMTP sunucunuzun adı ve e-posta kimlik bilgileriniz gibi) *\_AppStart. cshtml* dosyasında ayarlanır. Bu şekilde, e-posta göndereceğiniz her sayfada bunları tekrar ayarlamanız gerekmez. (Bazı nedenlerle bu ayarları değiştirmeniz gerekiyorsa, bunları bir sayfada ayrı ayrı ayarlayabilirsiniz.) Sayfada yalnızca, alıcı ve e-posta iletisinin gövdesi gibi her seferinde genellikle değişen değerleri ayarlarsınız.

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>Bir klasördeki dosyalardan önce ve sonra kod çalıştırma

Site çalıştırmadan sayfalardan önce kod yazmak üzere *AppStart. cshtml\_* de kullanabilirsiniz. belirli bir klasördeki herhangi bir sayfadan önce (ve sonra) çalışan bir kod yazabilirsiniz. Bu, bir klasördeki tüm sayfalar için aynı düzen sayfasını ayarlama veya bir kullanıcının klasörde bir sayfa çalıştırmadan önce oturum açmış olduğunu denetleme gibi şeyler için yararlıdır.

Belirli klasörlerdeki sayfalar için, *\_PageStart. cshtml*adlı bir dosyada kod oluşturabilirsiniz. Aşağıdaki diyagramda *\_PageStart. cshtml* sayfasının nasıl çalıştığı gösterilmektedir. Bir sayfa için bir istek geldiğinde, ASP.NET önce *\_AppStart. cshtml* sayfasını denetler ve bunu çalıştırır. Ardından ASP.NET bir *\_PageStart. cshtml* sayfası olup olmadığını denetler ve varsa bunu çalıştırır. Ardından istenen sayfayı çalıştırır.

*\_PageStart. cshtml* sayfasında, bir `RunPage` yöntemi ekleyerek istenen sayfanın çalıştırılmasını istediğiniz yeri belirtebilirsiniz. Bu, istenen sayfa çalıştırılmadan önce ve sonra yeniden kod çalıştırmanızı sağlar. `RunPage`eklemezseniz, *\_PageStart. cshtml* dosyasındaki tüm kodlar çalışır ve sonra istenen sayfa otomatik olarak çalışır.

![görüntüyle](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET, *\_PageStart. cshtml* dosyaları hiyerarşisi oluşturmanızı sağlar. Bir *\_PageStart. cshtml* dosyasını sitenin köküne ve herhangi bir alt klasöre koyabilirsiniz. Bir sayfa istendiğinde, en üst düzeydeki *\_PageStart. cshtml* dosyası (site köküne en yakın) çalışır ve ardından sonraki alt klasördeki *\_pagestart.* cshtml dosyası ve bu, istek istenen sayfayı içeren klasöre ulaşıncaya kadar alt klasör yapısını yavaşlatır. Tüm uygulanabilir *\_PageStart. cshtml* dosyaları çalıştıktan sonra, istenen sayfa çalışır.

Örneğin, aşağıdaki *\_PageStart. cshtml* dosyaları ve *default. cshtml* dosyası birleşimine sahip olabilirsiniz:

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

*/MyFolder/default.exe*komutunu çalıştırdığınızda şunları görürsünüz:

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>Bir klasördeki tüm sayfalar için başlatma kodunu çalıştırma

*\_PageStart. cshtml* dosyaları için iyi bir kullanım, tek bir klasördeki tüm dosyalar için aynı düzen sayfasını başlatmaktır.

1. Kök klasörde, *ınitpages*adlı yeni bir klasör oluşturun.
2. Web sitenizin *ınitpages* klasöründe *\_pagestart. cshtml* adlı bir dosya oluşturun ve varsayılan biçimlendirmeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. Web sitesinin kökünde, *paylaşılan*adlı bir klasör oluşturun.
4. *Paylaşılan* klasörde, *\_layout1. cshtml* adlı bir dosya oluşturun ve varsayılan biçimlendirmeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. *Initpages* klasöründe, *Content1. cshtml* adlı bir dosya oluşturun ve var olan içeriği şu şekilde değiştirin: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. *Initpages* klasöründe, *Content2. cshtml* adlı başka bir dosya oluşturun ve varsayılan biçimlendirmeyi aşağıdaki kodla değiştirin: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. Tarayıcıda *Content1. cshtml* dosyasını çalıştırın. 

    ![görüntüyle](18-customizing-site-wide-behavior/_static/image4.jpg)

    *Content1. cshtml* sayfası çalıştırıldığında, *\_pagestart. cshtml* dosyası `Layout` ayarlar ve ayrıca `PageData["MyBackground"]` bir renge ayarlar. *Content1. cshtml*içinde düzen ve renk uygulanır.
8. *Content2. cshtml* 'yi bir tarayıcıda görüntüleyin. 

    Her iki sayfa de *\_PageStart. cshtml*içinde başlatılan aynı düzen sayfasını ve rengini kullandığından, düzen aynıdır.

## <a name="using-_pagestartcshtml-to-handle-errors"></a>Hataları Işlemek için \_PageStart. cshtml kullanma

*\_PageStart. cshtml* dosyası için bir diğer iyi kullanım, bir klasördeki herhangi bir *. cshtml* sayfasında oluşabilen programlama hatalarını (özel durumlar) işlemenin bir yolunu oluşturmaktır. Bu örnek, bunu yapmanın bir yolunu gösterir.

1. Kök klasörde, *ınitcatch*adlı bir klasör oluşturun.
2. Web sitenizin *ınitcatch* klasöründe, *\_pagestart. cshtml* adlı bir dosya oluşturun ve var olan biçimlendirmeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    Bu kodda, bir `try` bloğunun içinde `RunPage` yöntemini çağırarak istenen sayfayı açıkça çalıştırmayı deneyin. İstenen sayfada herhangi bir programlama hatası oluşursa, `catch` bloğu içindeki kod çalışır. Bu durumda, kod bir sayfaya (*Error. cshtml*) yönlendirilir ve hata oluşan DOSYANıN adını URL 'nin bir parçası olarak geçirir. (Sayfayı kısa bir süre içinde oluşturacaksınız.)
3. Web sitenizin *ınitcatch* klasöründe *Exception. cshtml* adlı bir dosya oluşturun ve var olan biçimlendirmeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    Bu örneğin amaçları doğrultusunda, bu sayfada yaptığınız şeyler, mevcut olmayan bir veritabanı dosyasını açmaya çalışırken kasıtlı olarak bir hata oluşturuyor.
4. Kök klasörde, *Error. cshtml* adlı bir dosya oluşturun ve var olan işaretlemeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    Bu sayfada ifade `@Request["source"]`, URL 'den dışarı değeri alır ve görüntüler.
5. Araç çubuğunda **Kaydet**' e tıklayın.
6. *Özel durum. cshtml* 'yi bir tarayıcıda çalıştırın. 

    ![görüntüyle](18-customizing-site-wide-behavior/_static/image5.jpg)

    *Exception. cshtml*dosyasında bir hata oluştuğu için, *\_pagestart. cshtml* sayfası, iletiyi görüntüleyen *Error. cshtml* dosyasına yeniden yönlendirir.

    Özel durumlar hakkında daha fazla bilgi için bkz. [Razor sözdizimini kullanarak ASP.NET Web sayfalarına giriş programlama](https://go.microsoft.com/fwlink/?LinkID=251587).

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a>Klasör erişimini kısıtlamak için \_PageStart. cshtml kullanma

Ayrıca, bir klasördeki tüm dosyalara erişimi kısıtlamak için *\_PageStart. cshtml* dosyasını da kullanabilirsiniz.

1. WebMatrix 'te, **şablondan site** seçeneğini kullanarak yeni bir Web sitesi oluşturun.
2. Kullanılabilir şablonlar ' dan **Başlatıcı site**' yi seçin.
3. Kök klasörde, *kimlik doğrulayan Tedcontent*adlı bir klasör oluşturun.
4. Kimliği *Doğrulatediçerik* klasöründe, *\_pagestart. cshtml* adlı bir dosya oluşturun ve var olan biçimlendirmeyi ve kodu aşağıdaki kodla değiştirin: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    Kod, klasördeki tüm dosyaların önbelleğe alınmasını önleyecek şekilde başlatılır. (Bu, bir kullanıcının önbelleğe alınmış sayfalarının bir sonraki Kullanıcı tarafından kullanılabilmesini istemediğiniz genel bilgisayarlar gibi senaryolar için gereklidir.) Daha sonra, kod, kullanıcının klasördeki sayfalardan hiçbirini görüntüleyebilmek için sitede oturum açmış olup olmadığını belirler. Kullanıcı oturum açmamışsa, kod oturum açma sayfasına yeniden yönlendirilir. Oturum açma sayfası, `ReturnUrl`adlı bir sorgu dizesi değeri eklerseniz, kullanıcıyı başlangıçta istenen sayfaya döndürebilir.
5. *Sayfa. cshtml*adlı *kimlik doğrulayan tedcontent* klasöründe yeni bir sayfa oluşturun.
6. Varsayılan biçimlendirmeyi aşağıdaki kodla değiştirin:  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. *Sayfa. cshtml* 'yi bir tarayıcıda çalıştırın. Kod sizi bir oturum açma sayfasına yönlendirir. Oturum açmadan önce kaydolmanız gerekir. Kaydolduktan ve oturum açtıktan sonra, sayfasına gidebilir ve içeriğini görüntüleyebilirsiniz.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[Razor söz dizimini kullanarak ASP.NET Web sayfaları programlamasına giriş](https://go.microsoft.com/fwlink/?LinkID=251587)
