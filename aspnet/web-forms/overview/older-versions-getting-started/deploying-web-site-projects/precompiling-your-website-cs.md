---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-cs
title: Web sitenizi önceden derleme (C#) | Microsoft Docs
author: rick-anderson
description: "Visual Studio, ASP.NET geliştiricilerin iki tür proje sunar: Web uygulaması projeleri (WAP 'ler) ve Web sitesi projeleri (WSPs). Önemli farklardan biri..."
ms.author: riande
ms.date: 06/09/2009
ms.assetid: ecd5a4de-beb7-4d1d-bbbb-e31003633267
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-cs
msc.type: authoredcontent
ms.openlocfilehash: cb42398f44f3cd16ab83a9976e7b34f132384456
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573509"
---
# <a name="precompiling-your-website-c"></a>Web Sitenizi Önceden Derleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_15_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial15_Precompiling_cs.pdf)

> Visual Studio, ASP.NET geliştiricilerin iki tür proje sunar: Web uygulaması projeleri (WAP 'ler) ve Web sitesi projeleri (WSPs). İki proje türü arasındaki temel farklardan biri, WAP 'nin dağıtımdan önce açıkça derlenmiş olması gerekir, ancak bir WSP içindeki kod Web sunucusunda otomatik olarak derlenebilir. Ancak, dağıtımdan önce bir WSP 'yi önceden derlemek mümkündür. Bu öğretici, ön derleme avantajlarından yararlanır ve Visual Studio içinden ve komut satırından bir Web sitesinin nasıl önleneceğini gösterir.

## <a name="introduction"></a>Giriş

Visual Studio ASP.NET geliştiricileri iki farklı proje türü sunar: Web uygulaması projeleri (WAP) ve Web sitesi projeleri (WSP). Bu proje türleri arasındaki önemli farklılıklardan biri, WAP 'nin varsayılan olarak *otomatik derleme*kullanması için *Açık derleme* gerektirmasıdır. WAP 'lerle, Web uygulamasının kodunu Web sitesinin `Bin` klasöründe oluşturulan tek bir derlemede derleyebilirsiniz. Dağıtım, projedeki biçimlendirme içeriğini (`.aspx.ascx`ve `.master` dosyalarını), `Bin` klasöründeki derlemeden birlikte kopyalamayı gerektirir; arka plan kod dosyasının kendileri için dağıtılması gerekmez. Diğer yandan, hem biçimlendirme sayfalarını hem de karşılık gelen arka plan kod sınıflarını üretim ortamına kopyalayarak WSPs 'yi dağıtırsınız. Arka plan kod sınıfları Web sunucusunda isteğe bağlı olarak derlenir.

> [!NOTE]
> Proje modelleri, açık ve otomatik derleme ve derleme modelinin dağıtımı nasıl etkilediği hakkında daha fazla arka plan için [ *hangi dosyaların dağıtılmasını belirleme* öğreticisindeki](determining-what-files-need-to-be-deployed-cs.md) "açık derleme ve otomatik derlemeye karşılık gelen" bölümüne bakın.

Otomatik derleme seçeneğinin kullanımı basittir. Açık derleme adımı yoktur ve yalnızca değiştirilmiş dosyaların dağıtılması gerekir, ancak açık derleme, değiştirilen biçimlendirme sayfalarını ve yalnızca derlenmiş derlemeyi dağıtmakta olması gerekir. Ancak otomatik dağıtımda iki olası Sakıncaı vardır:

- Sayfaların ilk kez ziyaret edildiğinde otomatik olarak derlenmesi gerektiğinden, bir ASP.NET sayfası dağıtıldıktan sonra ilk kez istendiğinde, kısa ancak belirgin bir gecikme olabilir.
- Otomatik derleme, hem bildirim temelli biçimlendirmenin hem de kaynak kodunun Web sunucusunda mevcut olmasını gerektirir. Web uygulamasını Web sunucularına yükleyecek müşterilere satmaya planlandıysanız bu, etkileyici bir seçenek olabilir.

Yukarıdaki iki eksikle bir ölçü varsa, WAP modeline geçebilir veya dağıtımdan önce WSP 'yi *önceden derleyebilirsiniz* . Bu öğretici, barındırılan bir Web sitesi için en uygun ön derleme seçeneklerini inceler ve önceden derlenmiş bir Web sitesinin ön derleme işlemine ve dağıtımına yol gösterir.

## <a name="an-overview-of-aspnet-code-generation-and-compilation"></a>ASP.NET kod oluşturma ve derlemeye genel bakış

Kullanılabilir ön derleme seçeneklerine bakmadan önce, ilk kez oluşturulduğu veya son güncelleştirildiği için bir ASP.NET sayfası istendiğinde oluşan kod oluşturma ve derleme hakkında konuşalım. Bildiğiniz gibi, ASP.NET sayfaları iki bölümden oluşur: `.aspx` dosyasında bildirim temelli biçimlendirme; ve genellikle ayrı bir arka plan kod sınıfı dosyasında (`.aspx.cs`) bir kaynak kod bölümü. Bir ASP.NET sayfası istendiğinde çalışma zamanı tarafından gerçekleştirilen adımlar, uygulamanın derleme modeline bağlıdır.

WAP 'ler sayesinde sayfaların kaynak kodu, dağıtılmadan önce tek bir derlemeye açıkça derlenmiş olmalıdır. Dağıtım sırasında, bu derleme ve çeşitli biçimlendirme sayfaları üretim ortamına kopyalanır. Bir istek bir ASP.NET sayfası için Web sunucusuna ulaştığında, çalışma zamanı sayfanın arka plan kod sınıfının bir örneğini oluşturur ve sayfa yaşam döngüsünü başlatan `ProcessRequest` yöntemini çağırır ve sonuç olarak, sayfanın istek sahibine döndürülen içeriğini oluşturur. Arka plan kod sınıfı, dağıtımdan önce bir derlemeye zaten derlenmiş olduğundan, çalışma zamanı ASP.NET sayfasının arka plan kod sınıfı ile çalışabilir.

WSPs ve otomatik derleme ile dağıtımdan önce açık bir derleme adımı yoktur. Bunun yerine, dağıtım hem bildirim temelli hem de kaynak kodu içeriğini üretim ortamına kopyalamayı içerir. Sayfanın oluşturulduğu veya son güncelleştirildiği yana bir ASP.NET sayfası için bir istek Web sunucusuna ulaştığında, çalışma zamanının önce kod arkasındaki kodu bir derlemeye derlemesi gerekir. Bu derlenmiş derleme `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`klasöre kaydedilir, ancak bu klasörün konumu, genellikle `Web.config`içinde `<system.web>``<compilation tempDirectory="" />` öğesi aracılığıyla özelleştirilebilir. Derleme diske kaydedildiğinden, sonraki isteklerde aynı sayfaya yeniden derlenmesi gerekmez.

> [!NOTE]
> Tahmin edeceğiniz gibi, otomatik derleme kullanan bir sitede ilk kez (veya değiştirildikten sonra ilk kez) bir sayfa istendiğinde bir gecikme gecikirken, sunucunun sayfa kodunu derlemek ve ortaya çıkan derlemeyi şu şekilde kaydetmesi için bir süre sürer. dis.

Kısacası, açık derleme ile, dağıtımdan önce Web sitesinin kaynak kodunu derlemek, çalışma zamanının bu adımı gerçekleştirmek için sahip olduğu yerden kaydetmeniz gerekir. Otomatik derleme ile çalışma zamanı, sayfaların kaynak kodu derlemesini işler, ancak sayfanın oluşturulduğu veya son güncelleştirildiği bu yana ilk ziyaretine yönelik hafif bir başlatma maliyeti sağlar.

Ancak ASP.NET Pages 'in bildirime dayalı bölümü (`.aspx` dosyası) hakkında ne olacak? Bildirim temelli biçimlendirmede tanımlanan Web denetimlerine kodda erişilebilir olduğu için, `.aspx` dosyaları ve kod arkasında kod arasında bir ilişki olması çok açıktır. Ayrıca, `.aspx` dosyalardaki içeriğin sayfa tarafından oluşturulan işlenmiş biçimlendirmeyi büyük ölçüde etkilediği açıktır. Çalışma zamanı, istenen sayfanın işlenmiş içeriğini oluşturmak için `.aspx` dosyasında tanımlanan metin, HTML ve Web denetimi sözdizimi ile nasıl çalışır?

WAP 'ler ve Wsps 'ler arasında farklılık gösteren alt düzey uygulama ayrıntılarına çok fazla bilgi almak istemiyorum, ancak bir kısaca 'de çalışma zamanı, korumalı üye ve yöntemler olarak çeşitli Web denetimlerini içeren bir sınıf dosyası otomatik olarak oluşturur. Oluşturulan bu dosya, karşılık gelen arka plan kod sınıfına *kısmi bir sınıf* olarak uygulanır. ([Kısmi sınıflar](http://www.dotnet-guide.com/partialclasses.html) , tek bir sınıfın içeriğinin birden çok Dosya arasında yayılmasını sağlar.) Bu nedenle, arka plan kod sınıfı iki yerde tanımlanmıştır: oluşturduğunuz `.aspx.cs` dosyasında ve çalışma zamanı tarafından oluşturulan bu otomatik oluşturulan sınıfta. Bu otomatik oluşturulan sınıf `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` klasöründe depolanır.

Burada önemli olan nokta, bir ASP.NET sayfasının, hem bildirime dayalı hem de kaynak kodu bölümlerinin bir derlemeye derlenmesi gerekir. WAP 'ler ile, kaynak kodu dağıtımdan önceki bir derlemeye açıkça derlenir, ancak bildirim temelli biçimlendirme hala koda dönüştürülüp Web sunucusunda çalışma zamanı tarafından derlenmelidir. WSPs 'yi otomatik derleme kullanarak, hem kaynak kodu hem de bildirim temelli biçimlendirmenin Web sunucusu tarafından derlenmesi gerekir.

WSP modeliyle açık derlemeyi kullanmak mümkündür. WAP modeliyle benzer şekilde kaynak kodu bölümünü açıkça derleyebilirsiniz. Ayrıca, bildirim temelli biçimlendirmeyi de derleyebilirsiniz.

## <a name="precompilation-options"></a>Ön derleme seçenekleri

.NET Framework, WSP modeli kullanılarak oluşturulan bir ASP.NET uygulamasının kaynak kodunu (ve hatta içeriğini) derlemenize olanak tanıyan bir [ASP.NET derleme aracı (`aspnet_compiler.exe`)](https://msdn.microsoft.com/library/ms229863.aspx) ile birlikte gelir. Bu araç .NET Framework sürüm 2,0 ile yayımlanmıştır ve `%WINDIR%\Microsoft.NET\Framework\v2.0.50727` klasöründe bulunur; Bu, komut satırından kullanılabilir veya Visual Studio içinden, derleme menüsünün Web sitesi yayımla seçeneği aracılığıyla başlatılabilir.

Derleme aracı iki genel derleme biçimi sağlar: yerinde ön derleme ve dağıtım için ön derleme. Yerinde ön derleme ile komut satırından `aspnet_compiler.exe` aracını çalıştırın ve sanal dizinin yolunu veya bilgisayarınızda bulunan bir Web sitesinin fiziksel yolunu belirtin. Derleme aracı daha sonra projede her bir ASP.NET sayfasını derler ve sayfaların her biri bir tarayıcıdan ilk kez ziyaret edildiğinde olduğu gibi `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files` klasörde depolar. Yerinde ön derleme, çalışma zamanının bu adımı gerçekleştirmesine gerek duymasından konuma almayı azaltır olduğundan, sitenizdeki yeni dağıtılan ASP.NET sayfalarına yapılan ilk isteği hızlandırabilir. Ancak, Web sunucusunun komut satırından programları çalıştırabilmeniz gerektiğinden, yerinde ön derleme barındırılan Web sitelerinin çoğunluğu için yararlı değildir. Paylaşılan barındırma ortamlarında bu erişim düzeyine izin verilmez.

> [!NOTE]
> Yerinde ön derleme hakkında daha fazla bilgi için bkz. [nasıl yapılır: ASP.NET Web sitelerini ön](https://msdn.microsoft.com/library/ms227972.aspx) derleme ve [ASP.NET 2,0 ' de ön derleme](http://www.odetocode.com/Articles/417.aspx).

Web sitesindeki sayfaları `Temporary ASP.NET Files` klasörüne derlemek yerine, dağıtım için ön derleme, sayfaları seçtiğiniz bir dizine ve üretim ortamına dağıtılabilecek bir biçimde derler.

Bu öğreticide araştırdığımız dağıtım için önceden derlemenin iki özelliği vardır: güncelleştirilebilir bir kullanıcı arabirimiyle ön derleme ve güncelleştirilebilir olmayan kullanıcı arabirimiyle ön derleme. Güncelleştirilebilir bir kullanıcı arabirimiyle ön derleme, `.aspx`, `.ascx`ve `.master` dosyalarındaki bildirim temelli biçimlendirmeyi bırakır, böylece bir geliştiricinin görüntülemesini sağlar ve isterseniz üretim sunucusundaki bildirim temelli biçimlendirmeyi değiştirebilir. Güncellenebilir olmayan bir kullanıcı arabirimiyle ön derleme, herhangi bir içeriğin void ve `.ascx` ve `.master` dosyalarını kaldıran `.aspx` sayfaları oluşturur ve bu sayede bildirim temelli biçimlendirmeyi gizler ve bir geliştiricinin üretim ortamından değiştirmesini yasaklıyor.

### <a name="precompiling-for-deployment-with-an-updatable-user-interface"></a>Güncelleştirilebilir kullanıcı arabirimiyle dağıtım için ön derleme

Dağıtım için ön derlemeyi anlamanın en iyi yolu, bir örnek eylemde görmektir. Güncelleştirilebilir kullanıcı arabirimini kullanarak dağıtım için kitap Incelemelerini WSP için önceden derleyelim. ASP.NET derleme aracı, Visual Studio 'nun Build menüsünden veya komut satırından çağrılabilir. Bu bölüm, Visual Studio içinden aracı kullanmayı inceler; "komut satırından ön derleme" bölümünde, komut satırından derleyici aracını çalıştırma bölümüne bakar.

Visual Studio 'da kitap Incelemesi WSP ' nı açın, derleme menüsüne gidin ve Web sitesi yayımla menü seçeneğini belirleyin. Bu, Web sitesi Yayımla iletişim kutusunu (bkz. **Şekil 1**) başlatır; burada, ön derlenmiş sitenin Kullanıcı arabiriminin güncelleştirilebilir olup olmadığını ve diğer derleyici aracı seçeneklerini belirleyebilirsiniz. Hedef konum bir uzak Web sunucusu veya FTP sunucusu olabilir, ancak şimdilik bilgisayarınızın sabit sürücüsündeki bir klasörü seçin. Siteyi güncelleştirilebilir bir kullanıcı arabirimiyle önceden derlemek istiyoruz, "Bu ön derlenmiş sitenin güncelleştirilebilir olmasını sağla" onay kutusunu işaretli bırakın ve Tamam ' a tıklayın.

[![](precompiling-your-website-cs/_static/image2.png)](precompiling-your-website-cs/_static/image1.png)

**Şekil 1**: ASP.NET derleme aracı, Web sitenizin belirtilen hedef konuma ön derlemesini sağlar  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](precompiling-your-website-cs/_static/image3.png))

> [!NOTE]
> Build menüsündeki Web sitesi yayımla seçeneği Visual Web Developer 'da kullanılamaz. Visual Web Developer kullanıyorsanız, "komut satırından ön derleme" bölümünde ele alınan ASP.NET derleme aracının komut satırı sürümünü kullanmanız gerekir.

Web sitesi önceden derlendikten sonra Web sitesi Yayımla iletişim kutusuna girdiğiniz hedef konuma gidin. Bu klasörün içeriğini Web sitenizin içeriğiyle karşılaştırmak için bir dakikanızı ayırın. **Şekil 2** ' de, Book İncelemeleri Web sitesi klasörü gösterilmektedir. Hem `.aspx` hem de `.aspx.cs` dosyaları içerdiğini unutmayın. Ayrıca, `Bin` dizininin, [önceki öğreticide](logging-error-details-with-elmah-cs.md) eklediğimiz yalnızca bir dosya `Elmah.dll`içerdiğini unutmayın

[![](precompiling-your-website-cs/_static/image5.png)](precompiling-your-website-cs/_static/image4.png)

**Şekil 2**: proje dizini `.aspx` ve `.aspx.cs` dosyalarını içerir; `Bin` klasörü yalnızca `Elmah.dll` Içerir  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](precompiling-your-website-cs/_static/image6.png))

**Şekil 3** ' te, içeriği ASP.NET derleme aracı tarafından oluşturulan hedef konum klasörü gösterilmektedir. Bu klasör herhangi bir arka plan kod dosyası içermiyor. Ayrıca, bu klasörün `Bin` dizini `Elmah.dll` derlemeye ek olarak çeşitli derlemeler ve iki `.compiled` dosyası içerir.

[![](precompiling-your-website-cs/_static/image8.png)](precompiling-your-website-cs/_static/image7.png)

**Şekil 3**: hedef konum klasörü, dağıtım dosyalarını içerir  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](precompiling-your-website-cs/_static/image9.png))

WAP 'ler içindeki açık derlemeden farklı olarak, dağıtım işlemi için ön derleme tüm site için bir derleme oluşturmaz. Bunun yerine, her bir derlemede birden çok sayfa birlikte toplu işler. Ayrıca, `Global.asax` dosyasını (varsa) kendi derlemesine ve `App_Code` klasöründeki sınıflara derler. ASP.NET Web sayfaları, Kullanıcı denetimleri ve ana sayfalar (sırasıyla`.aspx`, `.ascx`ve `.master` dosyaları) için bildirim temelli biçimlendirmeyi tutan dosyalar hedef konum dizinine kopyalanır. Benzer şekilde, `Web.config` dosyası, görüntü, CSS sınıfları ve PDF dosyaları gibi herhangi bir statik dosya ile birlikte düz olarak kopyalanır. Derleme aracının çeşitli dosya türlerini nasıl işleyeceği hakkında daha resmi bir açıklama için, [ASP.net prebuild sırasında dosya işleme](https://msdn.microsoft.com/library/e22s60h9.aspx)bölümüne bakın.

> [!NOTE]
> Web sitesi Yayımla iletişim kutusundan "kullanılan sabit adlandırma ve tek sayfa derlemelerini" onay kutusunu işaretleyerek, derleme aracına ASP.NET sayfası, Kullanıcı denetimi veya ana sayfa başına bir derleme oluşturmasını isteyebilirsiniz. Her bir ASP.NET sayfasının kendi derlemesinde derlenmiş olması, dağıtım üzerinde daha ayrıntılı denetim sağlar. Örneğin, tek bir ASP.NET Web sayfasını güncelleştirdiyseniz ve bu değişikliği dağıtmak için gerekiyorsa, bu sayfanın `.aspx` dosyasını ve ilişkili derlemeyi üretim ortamına dağıtmanız gerekir. Daha fazla bilgi için [nasıl yapılır: ASP.NET derleme aracıyla Sabit adlar oluşturma](https://msdn.microsoft.com/library/ms228040.aspx) bölümüne bakın.

Hedef konum dizini Ayrıca, önceden derlenmiş Web projesinin parçası olmayan bir dosya içerir, yani `PrecompiledApp.config`. Bu dosya, ASP.NET çalışma zamanına uygulamanın önceden derlenmiş olduğunu ve güncelleştirilebilir veya öğleden sonra güncelleştirilebilir bir kullanıcı arabirimi ile önceden derlenmiş olup olmadığını bildirir.

Son olarak, Visual Studio 'Yu veya tercih ettiğiniz metin düzenleyicisini kullanarak hedef konumdaki `.aspx` dosyalarından birini açmak için bir dakikanızı ayırın. Güncelleştirilebilir bir kullanıcı arabirimiyle dağıtım için ön derleme yaparken, hedef konum dizinindeki ASP.NET sayfaları, Web sitesindeki ilgili dosyalarla tam olarak aynı biçimlendirmeyi içerir.

### <a name="precompiling-for-deployment-with-a-non-updatable-user-interface"></a>Güncelleştirilebilir olmayan bir kullanıcı arabirimiyle dağıtım için ön derleme

ASP.NET derleyici aracı Ayrıca, güncelleştirilebilir olmayan bir kullanıcı arabirimi ile dağıtım için bir siteyi önceden derlemek üzere kullanılabilir. Güncelleştirilemeyen bir kullanıcı ARABIRIMI ile siteyi önceden derlemek, güncelleştirilebilir bir kullanıcı arabirimi ile önceden derleme gibi çalışarak, hedef dizindeki ASP.NET sayfaları, Kullanıcı denetimleri ve ana sayfaların işaretlemesinin kaldırılmasının önemli farkıdır. Güncelleştirilemez bir kullanıcı arabirimi ile dağıtım için bir Web sitesini önceden derlemek için, derleme menüsünden Web sitesi Yayımla seçeneğini belirleyin, ancak "Bu ön derlenmiş sitenin güncelleştirilebilir olmasını sağla" seçeneğinin işaretini kaldırın (bkz. **Şekil 4**).

[![](precompiling-your-website-cs/_static/image11.png)](precompiling-your-website-cs/_static/image10.png)

**Şekil 4**: güncelleştirilebilir olmayan bir kullanıcı arabirimi Ile önceden derlemek için "Bu ön derlenmiş sitenin güncelleştirilebilir olmasını izin ver" seçeneğinin işaretini kaldırın  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](precompiling-your-website-cs/_static/image12.png))

**Şekil 5** ' te, güncelleştirilebilir olmayan bir kullanıcı arabirimiyle ön derleme yapıldıktan sonra hedef konum klasörü gösterilmektedir.

[![](precompiling-your-website-cs/_static/image14.png)](precompiling-your-website-cs/_static/image13.png)

**Şekil 5**: güncelleştirilebilir olmayan bir kullanıcı arabirimi ile dağıtım Için hedef konum klasörü  
 ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](precompiling-your-website-cs/_static/image15.png))

**Şekil 3** ' ü **Şekil 5**' e karşılaştırın. İki klasör özdeş görünebilir, ancak güncelleştirilebilir olmayan kullanıcı arabirimi klasörünün ana sayfanın `Site.master`olmadığına unutmayın. **Şekil 5** ' te çeşitli ASP.NET sayfaları da dahil olmak üzere, bu dosyaların içeriğini görüntülediğinizde, bunların bildirim temelli işaretlerinden kaldırılmış olduğunu ve yer tutucu metinle değiştirildiğini görürsünüz: "Bu, ön derleme aracı tarafından oluşturulan bir işaretleyici dosyasıdır ve silinmemelidir!"

[![](precompiling-your-website-cs/_static/image17.png)](precompiling-your-website-cs/_static/image16.png)

**Şekil 5**: bildirime dayalı biçimlendirme ASP.net sayfalarından kaldırılmıştır

**Şekil 3** ve **5** ' teki `Bin` klasörler daha önemli ölçüde farklılık gösterir. Derlemelere ek olarak, **Şekil 5** ' teki `Bin` klasörü her ASP.NET sayfası, Kullanıcı denetimi ve ana sayfa için bir `.compiled` dosyası içerir.

Güncelleştirilebilir olmayan bir kullanıcı arabirimi ile bir siteyi önceden derlemek, ASP.NET sayfalarının içeriğini üretim ortamında Web sitesini yükleyen veya yöneten kişi veya şirket tarafından değiştirilmesini istemediğiniz durumlarda faydalıdır. Kendi Web sunucularına yüklemek üzere müşterilere satış yaptığınız bir ASP.NET Web uygulaması oluşturursanız, bu kullanıcıların, sevk ettiğiniz `.aspx` sayfalarını doğrudan düzenleyerek sitenizin görünümünü değiştirmemesini sağlamak isteyebilirsiniz. Web sitenizi güncellenebilir olmayan bir kullanıcı arabirimi ile önceden derleyerek, yer tutucuyu yüklemenin bir parçası olarak `.aspx`, böylece müşterilerinizin içeriğini incelemeden veya değiştirmelerini engellemiş olursunuz.

### <a name="precompiling-from-the-command-line"></a>Komut satırından ön derleme

Arka planda, Visual Studio 'nun Web sitesini Yayımla iletişim kutusu, Web sitesini önceden derlemek için ASP.NET derleme aracı 'nı (`aspnet_compiler.exe`) çağırır. Alternatif olarak, komut satırından bu aracı çağırabilirsiniz. Aslında, Visual Web Developer kullanıyorsanız, Visual Web Developer 'ın Build menüsü Web sitesini yayımla seçeneği dahil olmadığı için, komut satırından derleyici aracını çalıştırmanız gerekir.

Derleyici aracını komut satırından kullanmak için, komut satırına bırakarak başlatın ve Framework dizinine gidin `%WINDIR%\Microsoft.NET\Framework\v2.0.50727`. Ardından, komut satırına aşağıdaki ifadeyi girin:

`aspnet_compiler -p "physical_path_to_app" -v / -f -u "target_location_folder"`

Yukarıdaki komut, ASP.NET derleyici aracını (`aspnet_compiler.exe`) başlatır ve `-p` anahtarı aracılığıyla, *fiziksel\_yol\_* kök web sitesini\_uygulamasına önceden derlemeye yönlendirir. Bu değer `C:\MySites\BookReviews`gibi bir şey olur ve tırnak işaretleriyle sınırlandırılmalıdır.

`-v` anahtarı, sitenin sanal dizinini belirtir. Siteniz IIS metatabanında varsayılan Web sitesi olarak kayıtlıysa `-p` anahtarını atlayabilir ve yalnızca uygulamanın sanal dizinini belirtebilirsiniz. `-p` anahtarını kullanırsanız, `-v` anahtarı devam eden değer Web sitesinin kökünü gösterir ve uygulama kök başvurularını çözümlemek için kullanılır. Örneğin, `-v /MySite` değerini belirtirseniz uygulamadaki başvurular `~/path/file` `~/MySite/path/file`olarak çözümlenir. Book Incelemeleri sitesi, Web barındırma şirketimin `-v /`bir kök dizinde bulunduğundan, anahtar.

Varsa `-f` anahtarı, derleme aracına zaten varsa *hedef\_konumu\_klasör* dizininin üzerine yazmasını söyler. `-f` anahtarını atlarsanız ve hedef konum klasörü zaten mevcutsa, derleme aracı şu hatayla çıkılacak: "hata ASPRUNTIME: hedef dizin boş değil. Lütfen el ile silin veya farklı bir hedef seçin. "

Varsa `-u` anahtarı, bir güncelleştirilebilir kullanıcı arabirimi oluşturmak için araca bildirir. Siteyi güncelleştirilebilir olmayan bir kullanıcı arabirimiyle önceden derlemek için bu anahtarı atlayın.

Son olarak, hedef *\_konum\_klasörü* hedef konum dizininin fiziksel yoludur; Bu değer `C:\MySites\Output\BookReviews`gibi bir şey olur ve tırnak işaretleriyle sınırlandırılmalıdır.

## <a name="deploying-the-precompiled-website"></a>Ön derlenmiş Web sitesini dağıtma

Bu noktada, hem güncelleştirilebilir hem de güncelleştirilebilir olmayan kullanıcı arabirimi seçeneklerini kullanarak bir Web sitesini önceden derlemek için ASP.NET derleme aracının nasıl kullanılacağını gördünüz. Ancak, bu nedenle, bu nedenle Web sitesini üretim ortamına değil yerel bir klasöre önceden derlenmiş. İyi haber, ön derlenmiş Web sitesini dağıtmanın bir kreeze ve Visual Studio aracılığıyla ya da tek başına bir FTP istemcisinden olduğu gibi başka bir dosya kopyalama mekanizmasıyla yapılabilir.

Web sitesi Yayımla iletişim kutusu (ilk olarak **Şekil 1**' de gösterilir), ön derlenmiş Web sitesi dosyalarının nereye kopyalandığını gösteren bir hedef konum seçeneğine sahiptir. Bu konum, uzak bir Web sunucusu veya FTP sunucusu olabilir. Bu metin kutusuna uzak bir sunucu girilmesi önceden derlenir ve Web sitesini tek bir adımda belirtilen sunucuya dağıtır. Alternatif olarak, Web sitesini yerel bir klasöre önceden derleyebilir ve ardından FTP veya başka bir yaklaşım ile bu klasörün içeriğini üretim ortamına el ile kopyalayabilirsiniz.

Önceden derlenmiş Web sitesini Visual Studio 'nun Web sitesi yayımlama iletişim kutusu aracılığıyla otomatik olarak dağıtmaktan, geliştirme ve üretim ortamları arasında hiçbir yapılandırma farkı olmadığı basit siteler için yararlıdır. Bununla birlikte, [ *geliştirme ve üretim öğreticisi arasındaki yaygın yapılandırma farklılıkları* ](common-configuration-differences-between-development-and-production-cs.md) bölümünde belirtildiği gibi, bu farklılıklara benzer bir şekilde rastlanmaz. Örneğin, kitap Incelemeleri Web uygulaması, üretim ortamındaki geliştirme ortamından farklı bir veritabanı kullanır. Visual Studio Web sitesini bir uzak sunucuya yayımladığında, geliştirme ortamındaki yapılandırma dosyası bilgilerini kopyalar.

Geliştirme ve üretim ortamları arasında yapılandırma farklarına sahip sitelerde, siteyi yerel bir dizine önceden derlemek, üretime özgü yapılandırma dosyalarını kopyalamak ve ardından önceden derlenmiş çıkışın içeriğini üzerine kopyalamak en iyi yöntem olabilir. üretiminden.

Geliştirme ortamından üretim ortamına dosya kopyalamaya yönelik Yenileyici için, bir [*FTP Istemcisi kullanarak Web sitenizi dağıtma*](deploying-your-site-using-an-ftp-client-cs.md) ve [*Visual Studio öğreticileri kullanarak Web sitenizi dağıtma*](determining-what-files-need-to-be-deployed-cs.md) bölümüne bakın.

## <a name="summary"></a>Özet

ASP.NET iki derleme modunu destekler: otomatik ve açık. Web uygulaması projeleri (WAP 'ler), önceki öğreticilerde anlatıldığı gibi açık derleme kullanır, ancak Web sitesi projeleri (WSPs) varsayılan olarak otomatik derleme kullanır. Ancak, ASP.NET derleme Aracı kullanılarak dağıtımdan önce bir WSP 'yi açıkça derlemek mümkündür.

Bu öğreticide, dağıtım desteği için derleme aracının ön derlemesi üzerine odaklanılmıştır. Dağıtım için ön derleme aracı, bir hedef konum klasörü oluşturur, belirtilen Web uygulamasının kaynak kodunu derler ve bu derlenmiş derlemeleri ve içerik dosyalarını hedef konum klasörüne kopyalar. Derleme aracı güncelleştirilebilir veya güncelleştirilemez bir kullanıcı arabirimi oluşturmak için yapılandırılabilir. Güncelleştirilebilir olmayan bir kullanıcı arabirimi seçeneğiyle ön derleme yaparken, içerik dosyalarındaki bildirim temelli biçimlendirme kaldırılır. Bir Nutshell 'de, ön derleme, Web sitesi proje tabanlı uygulamanızı herhangi bir kaynak kodu dosyası dahil etmeden ve isterseniz, bildirime dayalı biçimlendirme kaldırılarak dağıtmanıza izin verir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET Web sitesi ön derlemesi](https://msdn.microsoft.com/library/ms228015.aspx)
- [ASP.NET 2,0 ' de codebehind ve derleme](https://msdn.microsoft.com/magazine/cc163675.aspx)
- [ASP.NET içinde ön derleme](http://www.odetocode.com/Articles/417.aspx)
- [ASP.NET 'de önceden derlenmiş site seçenekleri](http://www.dotnetperls.com/precompiled)

> [!div class="step-by-step"]
> [Önceki](logging-error-details-with-elmah-cs.md)
> [İleri](users-and-roles-on-the-production-website-cs.md)
