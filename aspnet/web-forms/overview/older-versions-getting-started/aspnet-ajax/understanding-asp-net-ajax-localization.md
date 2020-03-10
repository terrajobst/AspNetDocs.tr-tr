---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: ASP.NET AJAX yerelleştirmesini anlama | Microsoft Docs
author: scottcate
description: Yerelleştirme, belirli bir dil ve kültür için bir uygulama veya uygulama bileşeni için destek tasarlama ve tümleştirme işlemidir. MIC...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566222"
---
# <a name="understanding-aspnet-ajax-localization"></a>ASP.NET AJAX Yerelleştirmesini Anlama

[Scott](https://github.com/scottcate) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> Yerelleştirme, belirli bir dil ve kültür için bir uygulama veya uygulama bileşeni için destek tasarlama ve tümleştirme işlemidir. Microsoft ASP.NET platformu standart .NET yerelleştirme modelini tümleştirerek standart ASP.NET uygulamalarına yönelik kapsamlı destek sağlar; Microsoft AJAX Framework, yerelleştirmenin gerçekleştirilebileceği farklı senaryoları desteklemek için tümleşik modeli kullanır.

## <a name="introduction"></a>Giriş

Microsoft 'un ASP.NET teknolojisi, nesne odaklı ve olay odaklı bir programlama modeli sağlar ve derlenmiş kodun avantajları ile birleştirir. Ancak, sunucu tarafı işleme modeli teknolojide bulunan birçok dezavantaja sahiptir ve birçok, Microsoft AJAX hizmetlerini .NET Framework kapsülleyen System. Web. Extensions Ad alanında yer alan yeni özellikler tarafından çözülebilir. 3,5. Bu uzantılar, daha önce ASP.NET 2,0 AJAX uzantılarının bir parçası olarak sunulan birçok zengin istemci özelliğini etkinleştirir, ancak artık Framework temel sınıf kitaplığı 'nın bir parçasıdır. Bu ad alanındaki denetimler ve özellikler tam sayfa yenileme gerektirmeden sayfaların kısmen işlenmesini, istemci betiği (ASP.NET profil oluşturma API 'SI dahil) aracılığıyla Web hizmetlerine erişme özelliği ve birçok bir tane yansıtması için tasarlanan kapsamlı bir istemci tarafı API ASP.NET sunucu tarafı denetim kümesinde görülen denetim şemaları.

Bu Teknik İnceleme, Microsoft AJAX Framework ve Microsoft AJAX betik kitaplığı 'nda bulunan yerelleştirme özelliklerini inceleyerek, yerelleştirme desteği için iş ihtiyacı ve Web 'de yerelleştirme için zaten tümleşik desteği gözden geçirme .NET Framework tarafından sunulan uygulamalar. Microsoft AJAX betik kitaplığı, .NET uygulamaları tarafından zaten kullanılan. resx dosya biçimini kullanır; bu, tümleşik IDE desteği ve paylaşılabilir bir kaynak türü sağlar.

Bu Teknik İnceleme Microsoft Visual Studio 2008 Beta 2 sürümünü temel alır. Bu Teknik İnceleme, Visual Studio 2008, Visual Web Developer Express ile birlikte çalıştığın ve Visual Studio 'nun Kullanıcı arabirimine göre izlenecek yollar sağlayacak olduğunu varsaymaktadır. Bazı kod örnekleri, Visual Web Developer Express 'te kullanılamayan proje şablonlarını kullanır.

## <a name="the-need-for-localization"></a>*Yerelleştirme gereksinimi*

Özellikle, kurumsal uygulama geliştiricileri ve bileşen geliştiricileri için, kültürler ve diller arasındaki farklılıklardan haberdar olabilecek araçlar oluşturma özelliği giderek daha da gerekli hale geldi. İstemci yerel ayarına uyum yeteneği olan bileşenleri tasarlamak, geliştirici üretkenliğini artırır ve bir bileşenin uyarlaması için gereken çalışma miktarını azaltır.

Yerelleştirme, belirli bir dil ve kültür için bir uygulama veya uygulama bileşeni için destek tasarlama ve tümleştirme işlemidir. Microsoft ASP.NET platformu standart .NET yerelleştirme modelini tümleştirerek standart ASP.NET uygulamalarına yönelik kapsamlı destek sağlar; Microsoft AJAX Framework, yerelleştirmenin gerçekleştirilebileceği farklı senaryoları desteklemek için tümleşik modeli kullanır. Microsoft AJAX Framework ile betikler, uydu derlemelerine dağıtılarak veya statik bir dosya sistemi yapısı kullanılarak yerelleştirilir.

## <a name="embedding-scripts-with-satellite-assemblies"></a>*Uydu Derlemeleriyle betikleri katıştırma*

Standart .NET Framework yerelleştirme stratejisi ile tutarlı, kaynak uydu derlemelerine dahil edilebilir. Uydu derlemeleri, ikili dosyalar dahil olmak üzere geleneksel kaynak içerme konusunda çeşitli avantajlar sağlar. herhangi bir yerelleştirme daha büyük görüntü güncelleştirilmeden güncelleştirilebildiği için, ek yerelleştirmeler yalnızca ' a uydu derlemeleri yüklenerek dağıtılabilir. Proje klasörü ve uydu derlemeleri ana proje derlemesinin yeniden yüklemesine neden olmadan dağıtılabilir. Özellikle ASP.NET projelerinde, bu faydalıdır çünkü artımlı güncelleştirmeler tarafından kullanılan sistem kaynakları miktarını önemli ölçüde azaltabilir ve üretim web sitesi kullanımını en düşük düzeyde kesintiye uğratabilirler.

Betikler derleme zamanında derleme sırasında bulunan yönetilen. resx (veya derlenmiş. resources) dosyalarına dahil ederek derlemelere katıştırılır. Daha sonra kaynakları, derleme düzeyi öznitelikler aracılığıyla AJAX çalışma zamanı tarafından oluşturulan kod aracılığıyla betik uygulaması için kullanılabilir hale getirilir

*Katıştırılmış betik dosyaları için adlandırma kuralları*

Microsoft AJAX Framework betik yönetimi, betikleri dağıtmak ve test etmek için kullanabileceğiniz çeşitli seçenekleri destekler ve bu seçenekleri kolaylaştırmak için yönergeler sağlanır.

*Hata ayıklamayı kolaylaştırmak için:*

Yayın (üretim) betikleri dosya adında `.debug` niteleyicisi içermemelidir. Hata ayıklama için tasarlanan betikler dosya adında `.debug` içermelidir.

*Yerelleştirmeyi kolaylaştırmak için:*

Nötr kültür betikleri, dosyanın adında hiçbir kültür tanımlayıcısı içermemelidir. Yerelleştirilmiş kaynaklar içeren betikler için, dosya adında ISO dil kodu belirtilmelidir. Örneğin, `es-CO` Ispanyolca, Kolumbiyası için temsil eder.

Aşağıdaki tablo, dosya adlandırma kurallarını örneklerle özetler:

| Kısaltın | Açıklama |
| --- | --- |
| Script. js | Sürüm-kültür bağımsız betiği. |
| Script.debug.js | Hata ayıklama-sürüm kültürü-bağımsız betiği. |
| Script.en-US.js | Bir sürüm Ingilizce, Birleşik Devletler betiği. |
| Script.debug.es-CO.js | Hata ayıklama-sürüm Ispanyolca, Kolumbiyası betiği. |

## <a name="walkthrough-create-an-localized-embedded-script"></a>İzlenecek yol: yerelleştirilmiş, katıştırılmış betik oluşturma

*Lütfen unutmayın: Visual Web Developer Express, sınıf kitaplığı projeleri için bir proje şablonu içermediğinden, Bu izlenecek yol Visual Studio 2008 ' un kullanılmasını gerektirir.*

1. ASP.NET AJAX Uzantıları ile tümleşik yeni bir Web sitesi projesi oluşturun. LocalizingResources adlı çözüm içindeki bir sınıf kitaplığı projesi olan başka bir proje oluşturun.
2. LocalizingResources projesine Verifysilmenin. js adlı bir JScript dosyası ve ayrıca, DeletionResources. resx ve DeletionResources. es. resx adlı. resx kaynak dosyaları ekleyin. İlki, kültürün bağımsız kaynaklarını içerir; İkincisi, Ispanyolca-Dil kaynakları içerecektir.
3. Verifysilinmeye. js ' ye aşağıdaki kodu ekleyin:

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

JavaScript Regex sözdizimi, tek eğik çizgi (önceki örnekte/dosyaadı/bir örnektir) içindeki metinler, RegExp nesnesini gösterir. MSDN Kitaplığı kapsamlı bir JavaScript başvurusu içerir ve JavaScript yerel nesnelerindeki kaynaklar çevrimiçi olarak bulunabilir.

1. Aşağıdaki kaynak dizelerini DeletionResources. resx öğesine ekleyin: 

    **Verifydelete**: dosya adını silmek istediğinizden emin misiniz?

    **Silindi**: dosya adı silindi.

1. Aşağıdaki kaynak dizelerini DeletionResources. es. resx öğesine ekleyin: 

    **Verifydelete**: EST Seguro que desee TITAR FILENAME?

    **Silindi**: FILENAME se ha titado.
2. Aşağıdaki kod satırlarını AssemblyInfo dosyasına ekleyin:

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. LocalizingResources projesine System. Web ve System. Web. Extensions başvuruları ekleyin.
2. Web sitesi projesinden LocalizingResources projesine bir başvuru ekleyin.
3. Varsayılan. aspx dosyasında, Web sitesi projesi altında, ScriptManager denetimini aşağıdaki ek işaretlerle güncelleştirin:

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. Varsayılan. aspx dosyasında, sayfanın herhangi bir yerinde şu biçimlendirmeyi ekleyin:

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. F5 tuşuna basın. İstenirse, hata ayıklamayı etkinleştirin. Sayfa yüklendiğinde Sil düğmesine basın. Onay için, Ingilizce (Bilgisayarınız varsayılan olarak Ispanyolca-Dil kaynaklarını tercih etmek üzere ayarlanmamışsa) sorulur.
2. Tarayıcı penceresini kapatın ve default. aspx ' e geri dönün. @Page Header yönergesinde Auto ve UICulture için Auto-ES ile değiştirin. Web uygulamasını tarayıcıda yeniden başlatmak için F5 tuşuna basın. Bu kez, dosyayı Ispanyolca olarak silmeniz istenir:

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-localization/_static/image3.png))

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

([Tam boyutlu görüntüyü görüntülemek Için tıklayın](understanding-asp-net-ajax-localization/_static/image6.png))

Bu izlenecek yol için çeşitli Çeşitlemeler olduğunu unutmayın. Örneğin, betikler sayfa yükleme sırasında program aracılığıyla ScriptManager denetimine kaydedilebilir.

## <a name="including-a-static-script-file-structure"></a>*Statik betik dosyası yapısını dahil etme*

Dağıtım için statik betik dosyaları kullanıldığında, devralınan .NET yerelleştirme şemasını kullanmanın avantajlarından bazılarını kaybedersiniz. Birincil olarak görünür, komut dosyası kaynak dosyalarını dahil ederek oluşturulan otomatik türü kaybedersiniz; Yukarıdaki yönergede, örneğin, kaynaklar ScriptManager denetiminden Ileti adlı otomatik olarak oluşturulan bir tür tarafından kullanıma sunuldu.

Ancak, statik betik dosya yapısını kullanmanın bazı avantajları vardır. Güncelleştirme, uydu derlemelerini yeniden derleme ve yeniden dağıtmaya gerek kalmadan gerçekleştirilebilir ve bir bileşen ile birlikte sunulmayan küçük bir işlev parçasını bütünleştirmek için, gömülü betiği geçersiz kılmak üzere bir statik dosya yapısının kullanılması da yapılabilir.

Microsoft, proje derlemesi sırasında betik kaynaklarınızı otomatik olarak oluşturarak bir sürüm denetimi sorununa karşı kaçınmanızı önerir. Kapsamlı bir betik kodu tabanı korunarak, kod değişikliklerinin her bir yerelleştirilmiş betiğe yansıtıldığından emin olmak giderek daha zor hale gelebilir. Alternatif olarak, proje derlerken dosyaları birleştirerek yalnızca bir mantık betiği ve birden çok yerelleştirme betiği tutabilirsiniz.

Bildirimli olarak dahil edilecek kaynaklar olmadığından, statik betik dosyalarına ScriptManager denetiminin `<Scripts>` etiketinin alt öğesi olarak `<asp:ScriptElement>` öğeleri eklenerek ya da çalışma zamanında sayfadaki `ScriptManager` denetiminin `Scripts` özelliğine program aracılığıyla `ScriptReference` nesneleri ekleyerek başvurulmalıdır.

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager ve yerelleştirme rolü*

ScriptManager, yerelleştirilmiş uygulamalar için birkaç otomatik davranışa izin vermez:

- Ayarları ve adlandırma kurallarını temel alarak betik dosyalarını otomatik olarak bulur; Örneğin, hata ayıklama modundayken hata ayıklama özellikli betikleri yükler ve tarayıcının kullanıcı arabirimi seçimine göre yerelleştirilmiş betikleri yükler.
- Özel kültürler dahil olmak üzere kültürlerin tanımını sunar.
- HTTP üzerinden betik dosyalarını sıkıştırmaya izin vermez.
- Birçok isteği verimli bir şekilde yönetmek için betikleri önbelleğe alır.
- Bu kod, şifrelenmiş bir URL aracılığıyla bir yöneltme katmanını bir yöneltmeye ekler.

Betik başvuruları, program aracılığıyla ya da bildirime dayalı biçimlendirme yoluyla ScriptManager denetimine eklenebilir. Bildirim temelli biçimlendirme özellikle, Web sitesi projesi dışındaki derlemelere gömülü betiklerle çalışırken yararlı olur, çünkü kod adı, düzeltmelerin gönderildiği şekilde değişmeme olasılığı yüksektir.

## <a name="summary"></a>Özet

Daha büyük bir hedef kitleye ulaşmak için Web uygulamalarının büyümesi arttıkça, daha geniş kültürlere ulaşabilme ve toplulukların bir iş modeli için temel hale gelmesi gerekir; e-ticaret Web uygulamalarının yabancı para birimleriyle uğraşmak zorunda olması gerekir, içerik yönetim sistemleri yalnızca içeriğini sunamayacak ve ayrıca diğer dillerdeki gezinme ipuçlarını ve form alanlarını ve şirketlerin bu ihtiyacı olduğunu bilmeleri gerekir. eriþ.

.NET Framework doğası gereği, uydu derlemelerini ve XML kaynak (. resx) dosyalarını kullanarak kaynak dizeleri ve görüntüleri aramak için tek bir yol sunmak üzere zengin bir yerelleştirme çerçevesini destekler. Microsoft AJAX Framework ve Microsoft AJAX betik kitaplığı dahil olmak üzere ASP.NET AJAX Uzantıları, istemci tarafı koda bu programlama modeli için destek sağlar ve bu sayede kolay kaynak dize aramalarını etkinleştirir. Uydu derlemeleri, dosya adları belirli bir adlandırma şemasını izlediği sürece ScriptResource. axd aracılığıyla betik kaynaklarının (gerçek. js dosyaları) otomatik olarak eklenmesini destekler. Bu destek sayesinde, ASP.NET AJAX Uzantıları, betiklerin yerelleştirilmesini ve uygulamaların Genelleştirme işlemini basitleştirir.

## <a name="bio"></a>*Biyografisi*

Scott, 1997 tarihinden itibaren Microsoft Web teknolojileriyle çalışmaktadır ve Bilgi Bankası yazılım çözümlerine odaklanmış ASP.NET tabanlı uygulamalar yazma konusunda uzmanımız myKB.com ([www.myKB.com](http://www.myKB.com)) Başkan Yardımcısı. Scott 'da e-posta ile [scott.cate@myKB.com](mailto:scott.cate@myKB.com) veya blogundan [ScottCate.com](http://ScottCate.com) adresinden iletişim kurulabilirler

> [!div class="step-by-step"]
> [Önceki](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [İleri](understanding-asp-net-ajax-web-services.md)
