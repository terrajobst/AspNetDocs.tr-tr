---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
title: WebMatrix kullanarak Site yayımlama - ASP.NET Web sayfaları ile tanışın | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, ASP.NET Web sayfaları ve Microsoft WebMatrix tanıtan öğretici kümesi son bölümünde bölümüdür. Bu, sitenizi t yayımlamak nasıl ele alınmaktadır...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 7e85c70e-1a88-4408-8b3d-29611c7713ed
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/publishing
msc.type: authoredcontent
ms.openlocfilehash: 49a841dbda183bf1d59153b83f694c9f517e0b94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633618"
---
# <a name="introducing-aspnet-web-pages---publishing-a-site-by-using-webmatrix"></a>WebMatrix kullanarak Site yayımlama - ASP.NET Web sayfalarına giriş

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğretici, ASP.NET Web sayfaları ve Microsoft WebMatrix tanıtan öğretici kümesi son bölümünde bölümüdür. Bu, diğerleri ile çalışabilmeniz için Internet'e sitenizi yayımlama açıklanır. [ASP.NET Web sayfaları siteleri Için tutarlı bir görünüm oluşturarak](https://go.microsoft.com/fwlink/?LinkId=251585)seriyi tamamladığınız varsayılır.
> 
> Kullanarak site yayımlama öğreneceksiniz:
> 
> - Microsoft Azure
> - Web barındırma şirketi

## <a name="about-publishing-your-site"></a>Sitenizi yayımlama hakkında

Şimdiye kadar test sayfalarınıza dahil olmak üzere yerel bir bilgisayardaki tüm iş yaptık. <em>. Cshtml</em> sayfalarınızı çalıştırmak Için, WebMatrix içinde yerleşik olan Web sunucusunu kullandınız, yani IIS Express. Ancak Elbette hiç dışında oluşturduğunuz site görebilirsiniz. Başkalarının siteniz ile çalışmak için Internet'te yayımlamak zorunda.

Zaten bir genel Web sunucusuna erişiminiz yoksa, yayımlama, *bulut platformu* veya *barındırma sağlayıcısı*içeren bir hesabınız olması gerektiği anlamına gelir. Microsoft Azure gibi bir bulut platformu, uygulamalarınız için isteğe bağlı altyapı sağlar. Bir barındırma sağlayıcısı, kiraya ve genel olarak erişilebilir web sunucuları sahip olan bir şirket alanı siteniz için ' dir. Barındırma planları aylık birkaç lira karşılığında dosyasından çalıştırın (veya hatta ücretsiz) ABD Doları aylık yüksek hacimli ticari Web siteleri için yüzlerce küçük sitelere için.

> [!NOTE]
> Bir genel web sunucusuna internet hizmet evde almak için kullandığınız internet hizmet sağlayıcısı (ISS) aracılığıyla erişimi olabilir. Ancak, barındırma sağlayıcınızda ASP.NET Web Pages desteklemesi gerekir. Birçok ISS yoktur, ancak bu her zaman denetimi değerindedir.

Bu öğreticide, biz, nasıl yayımlamak genel bir bakış sunacağız. Her şey için tam Ayrıntılar sağlayan pratik değildir, çünkü işlemi, her bir barındırma sağlayıcısı için biraz farklılık gösterir. Ancak, işlemin nasıl çalıştığına ilişkin bir fikir elde edersiniz.

Bu öğreticide, dört bölüm içerir:

1. [Varsayılan sayfayı ayarlama](#defaultpage)
2. Yayımlama (aşağıdakilerden birini seçin)  
 a. [Sitenizi Microsoft Azure yayımlama](#azure)  
 b. [Sitenizi bir Web barındırma şirketine yayımlama](#host)
3. [Canlı siteyi güncelleştirme: yeniden yayımlama](#update)

<a id="defaultpage"></a>
## <a name="setting-up-the-default-page"></a>Varsayılan sayfayı ayarlama

Bir kullanıcının web siteniz için temel adresi gittiğinde, siteniz için varsayılan sayfa kullanıcıya görüntülenir. Örneğin, *default. htm* , `www.contoso.com`site için varsayılan sayfa olarak ayarlandığında, `www.contoso.com` 'ye gidildiğinde `www.contoso.com/Default.htm`gezinme ile aynı olur.

Şu anda siteniz varsayılan sayfa olarak **default. cshtml** kullanır. Bu sayfada varsayılan sayfanız için uygundur, ancak boş bir sayfa görüntülemek için Bu öğreticide, herhangi bir içerik söz konusu sayfaya eklemediniz. Default.cshtml açın ve içeriğini aşağıdaki kodla değiştirin.

[!code-cshtml[Main](publishing/samples/sample1.cshtml)]

Artık sitenizin yayın için hazırdır. İlk olarak, sitesinin Azure'a nasıl dağıtılacağı ve bir web barındırma şirketi dağıtma görürsünüz. Her iki seçeneği çalışır ve web siteniz için yalnızca dağıtım seçeneklerinden birini izlemeniz gerekir.

<a id="azure"></a>
## <a name="publishing-your-site-to-microsoft-azure"></a>Sitenizi Microsoft Azure'a yayımlama

Bu öğreticide ilk sitenizi Microsoft Azure'a dağıtmak nasıl gösterilecek. Bir Microsoft hesabıyla oturum açarak, Azure'da en fazla 10 ücretsiz siteleri oluşturabilirsiniz. Bu ücretsiz siteleri sitelerinizi test etmek için kullanışlı bir yol sağlar. Bu örnek site daha sonra tüm ücretsiz sitelerinizden kullanarak önlemek için her zaman silebilirsiniz. Yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

WebMatrix şeridinde **Yayımla** düğmesine tıklayın.

![WebMatrix şeridinde 'Publish' düğmesi](publishing/_static/image1.png)

**Sitenizi Yayımla** iletişim kutusu görüntülenir. Microsoft hesabı oturumunuzu açmadıysanız, iletişim kutusunda **Azure ile çalışmaya başlama** bağlantısı bulunur. Bu bağlantıya tıklayın.

![Sitenizi yayımlayın](publishing/_static/image2.png)

Bir Microsoft hesabı ile oturum açmanızdan değil ise, yeniden oturum açmak için bir fırsat sunulur. Bir Microsoft hesabına sitenizi azure'da yayımlamak için oturum açmanız gerekir.

![Oturum Açma](publishing/_static/image3.png)

Microsoft hesabınızda oturum açtıktan sonra iletişim kutusu, Azure'da yeni bir site oluşturmak veya mevcut sitelerinizi azure'da birine bağlanmak için bağlantılar içerir.

![Yeni Site oluşturma](publishing/_static/image4.png)

**Yeni site oluştur**' u seçin.

Projenizi **Webpagesfilmlerini**olarak adlandırdıysanız sitenizin varsayılan adı **webpagesmovies.azurewebsites.net**olacaktır. Büyük olasılıkla bu varsayılan adı kullanılamıyor, kırmızı bir ünlem işareti tarafından belirtildiği şekilde.

![Varsayılan Web sitesi adı](publishing/_static/image5.png)

Kullanılabilir olan bir site adı değiştirin ve konumunuz yakın bir konum seçin.

![Değiştirilen site adı](publishing/_static/image6.png)

**Tamam**’a tıklayın.

WebMatrix performss sunucu siteniz ile uyumlu olup olmadığını belirlemek için bir test.

![Uyumluluk testi](publishing/_static/image7.png)

**Devam**'ı seçin.

Uyumluluk testinin sonuçları görüntülenir.

![Uyumluluk sonucu](publishing/_static/image8.png)

**Devam**'ı seçin.

WebMatrix sitede yayınlanan veritabanları ve dosyaları görüntüler. Bu sitenin yayımladığınız ilk kez olduğundan, tüm dosyalar listelenmektedir. Yayımlanmaya hazır olmayan bir dosya işaretini kaldırabilirsiniz. Sonraki yayınlarda yalnızca değişen dosyaları görüntülenir. Bkz. [canlı siteyi güncelleştirme: yeniden yayımlama](#update).

![Yayımlama önizlemesi](publishing/_static/image9.png)

**Devam**'ı seçin.

Site Azure'a dağıtıldıktan sonra dağıtımın tamamlandığını bir ileti görüntülenir.

![Yayımlama tamamlandı](publishing/_static/image10.png)

Sitenizi ve veritabanınızı Azure'a yayımlandı ve genel kullanıma sunulmuştur. Yayımlama tamamlandı ve artık dağıtılan sitenizi görürsünüz belirten iletiyi bağlantıya tıklayın. Siz veya Internet erişimi olan herkes, ekleyin veya veritabanında kayıt değiştirin.

![](publishing/_static/image11.png)

<a id="host"></a>
## <a name="publishing-your-site-to-a-web-hosting-company"></a>Barındırma şirketi bir Web sitenizi yayımlama

Azure'a yayımlama değil karar verirseniz, bunun yerine bir web barındırma şirketi, sitenizi yayımlayabilirsiniz.

**Web barındırma 'Yı bul** bağlantısına tıklayın.

![Yayımlama Ayarları iletişim kutusunda 'web barındırma Bul' düğmesi](publishing/_static/image12.png)

ASP.NET'i destekleyen barındırma sağlayıcılarının listeleyen Microsoft sitesi bir sayfasına gidin.

![Barındırma sağlayıcıları listeler Microsoft sitesinde sayfası](publishing/_static/image13.png)

Kuşkusuz, artık tam olarak uzun vadeli gerektirebilir barındırma özellikleri anlamak zor olabilir. Birkaç göz önünde bulundurulması gerekenler şunlardır:

- WebPagesMovies site amacı doğrultusunda, genellikle ek maliyetler SQL Server için ayrı bir eklenti olması gerekmez. Sitenizdeki, kendi içinde olduğu SQL Server Compact Edition kullanıyorsanız. Ancak, bazı gelecek Web sitesi iş yaptığınız için SQL Server erişimi gerekebilir. Yapabileceğiniz düşünüyorsanız, SQL Server özelliği daha sonra ekleyebilirsiniz emin olun.
- Barındırma sağlayıcısı, Web dağıtımı yayımlama Protokolü destekleyip desteklemediğini kontrol edin. FTP protokolünü kullanarak yayımlayabilirsiniz ancak Web dağıtımı kullanabilmeniz daha uygundur.

Bazı siteler ücretsiz deneme süresi sunar. Ücretsiz deneme yayımlama denemek için iyi bir yoludur ve basılı barındırma hala denemeler WebMatrix ve ASP.NET Web sayfaları ile.

İstediğiniz birini seçin. Bu öğretici için şu öğreticiyi kalıyorduk, ancak bu şirket birkaç ay boyunca ücretsiz olan bir site konak kişilere bir promosyon olduğundan DiscountASP.NET, seçtik.

> [!NOTE]
> Bu öğretici için bir barındırma sağlayıcısının kendi, şirketin bir onay diğer yorumlanacağını olmamalıdır. Ancak bir çizim için çekme vardı ve yayımlama için ASP.NET Web sayfaları ve Web dağıtımı protokolünü destekleyen birçok şirket, DiscountASP.NET biridir.

Genellikle, bir barındırma sağlayıcısında açtıktan sonra şirket, bir kullanıcı adı ve parola, web sunucusu ve benzeri URL'sini içeren bir e-posta gönderir. Barındırma şirketinin Web dağıtımı protokolünü destekliyorsa, içeren bir dosya yayımlama ayarları veya bir indirme izin gönderebilir. Yayımlama ayarları dosyası işlemi sizin için basitleştirir.

Kaydolup yayımlamaya hazırsanız, WebMatrix şeridinde **Yayımla** düğmesine tıklayın. **Ayarları Yayımla** iletişim kutusu görüntülenir.

Barındırma sağlayıcısı size bir yayımlama ayarları dosyası gönderdiyse, **Yayımlama ayarlarını Içeri aktar** bağlantısına tıklayın ve dosyayı içeri aktarın. Yayımlama ayarları dosyası yoksa, barındırma şirket e-posta ile gönderilen değerler kullanılarak alanları doldurun. İşte **yayınlama ayarları** iletişim kutusu işiniz bittiğinde şöyle görünebilir:

![Yayımlama ayarlarını 'Yayımlama Ayarları' iletişim kutusunda doldurulur](publishing/_static/image14.png)

**Bağlantıyı doğrula**' ya tıklayın. Her şey tamam ise, iletişim kutusu **başarıyla bağlanır**, bu da barındırma sağlayıcısının sunucusuyla iletişim kurabildiği anlamına gelir.

![Başarılı iletisi, yayımlama ayarları doğru](publishing/_static/image15.png)

Bir sorun varsa, WebMatrix sorunun ne olduğunu söylemek için en iyi şekilde yapar:

![Yayımlama ayarları ile ilgili bir sorun varsa hata iletisi](publishing/_static/image16.png)

Ayarlarınızı kaydetmek için **Kaydet** ' e tıklayın. WebMatrix, onu doğru barındırma siteyle iletişim kurabildiğinden emin olmak için bir test gerçekleştirmek sunar:

![İleti yayımlama işleminin bir test gerçekleştirmek teklifi](publishing/_static/image17.png)

**Evet**'i tıklayın. WebMatrix, barındırma sağlayıcısının bazı örnek dosyalarını yükler. WebMatrix, uyumluluk testi tamamlandığında, sonuçları raporları:

![Yayımlama test sonuçları](publishing/_static/image18.png)

Çalışmaya hazırsanız, **devam** ' a tıklayarak yayımlama işlemini gerçek için başlatın. WebMatrix, hangi dosyalar sitenizdeki ve ana bilgisayar sunucusunda (şu anda hiçbiri) durumda ve yayımlama işlemi, bir önizleme sunar kullanıma rakamları:

![Yayımlama işlemi yükleyeceği hangi dosyaların önizlemesini](publishing/_static/image19.png)

Yayımlanacak dosyaların listesi, *filmler. cshtml*gibi oluşturduğunuz Web sayfalarını içerir. Bu liste, dosyaları, yüklemiş olduğunuz için Yardımcıları veritabanınız için SQL Server Compact Edition'ı çalıştırın ve benzeri için dosyaları da içerir. Sonuç olarak, ilk yayımlama işlemi olabilmektedir.

**Devam**'a tıklayın. WebMatrix, dosyalar, barındırma sağlayıcısının sunucusuna kopyalar. İşlem tamamlandığında, sonuçları durum çubuğunda bildirilir:

![Yayımlama işlemi başarıyla tamamlandığında durum çubuğu iletisi](publishing/_static/image20.png)

Sitenizin Canlı görmek için durum çubuğundaki bağlantıya tıklayın. URL 'ye *film* ekleyin ve oluşturduğunuz *filmler. cshtml* dosyasını görürsünüz:

![Filmler sayfasını gösteren Canlı site](publishing/_static/image21.png)

<a id="update"></a>
## <a name="updating-the-live-site-republishing"></a>Canlı siteyi güncelleştirmeden: yeniden yayımlama

Sitenizi yayımladıktan sonra (Azure 'a veya bir Web barındırma şirketine), bilgisayarınızın sürümü ve Hizmet sağlayıcısındaki sürüm &mdash; iki kopyası vardır. Site geliştirmeye devam isteyebilirsiniz (başka bir şey varsa sonraki öğretici kümesinin bir parçası olarak). Bunu yaptığınızda, değişiklikler hizmet sağlayıcısına bilgisayarınızdan kopyalanması için sitenizi yeniden yayımlamanız gerekir. WebMatrix yayımlama işleminde, sitenizde hangi dosyaların değiştiğini belirlemek ve yalnızca bu dosyaları yayımlayın.

Yeniden yayımmadan nasıl çalıştığını görmek için, *filmler. cshtml* sitesini açın, küçük bir değişiklik yapın ve dosyayı kaydedin. Örneğin, başlığı `Movies - Updated`olarak değiştirin.

Şeritteki **Yayımla** düğmesine tıklayın. WebMatrix, neyin değiştirilir ve bu yayımlayacak dosyaların önizlemesini belirler.

![Yeniden yayımlanması için hazır dosyalar değiştirilmiş gösteren 'Yayımla' iletişim kutusu](publishing/_static/image22.png)

> [!IMPORTANT] 
> 
> Varsayılan olarak, WebMatrix veritabanını ( *. sdf* dosyası) yalnızca siteyi ilk kez yayımladığınızda yayımlar. Sitenizi yayımlanır ve kişiler ile Web sitesi etkileşim sonra canlı site veritabanında sitenin gerçek veriler genellikle vardır. Bilgisayarınızda genellikle test verilerini içeren *. sdf* dosyası ile canlı veritabanının üzerine yazılmamaya dikkat etmeniz gerekir. Uyarı **yayımlamanın her türlü uzak veritabanının üzerine yazılmasına**neden olduğunu ve *webpagesfilmlerini. sdf* onay kutusunun neden varsayılan olarak temizlendiğinizi görürsünüz.

**Devam**'a tıklayın. WebMatrix, değiştirilmiş dosyalar yayımlar ve yayımladığınız ilk kez yaptığınız gibi bir başarı iletisi gösterilir.

Canlı site (tıklayabilirsiniz başarılı iletisi bağlantıdaki hala gösteriliyorsa) gidin ve değişikliğinizi yayımlandığından emin olun.

> [!TIP] 
> 
> **Dosyaları uzaktan Düzenle**
> 
> Sitenizi değiştirme ve ardından yeniden yayımlanması için alternatif olarak, WebMatrix uzak dosyaları doğrudan düzenleyebilirsiniz. Bu senaryoda, hizmet sağlayıcısına bir dosya açın ve bir kopyasını düzenlemek, Webmatrix'i yükler. Her dosyayı kaydettiğinizde, WebMatrix değişiklikleri siteye gönderir.
> 
> Uzaktan düzenleme, Canlı sitenize değişiklik yapmak için kolay bir yoludur. Ancak, böylece yaptığınız değişiklikler sitenizde yerel dosyalarla eşitlenmedi. Yerel dosyaları uzak siteyle eşitlemek için Uzak dosyaları indirebilirsiniz. Bu işlem, yayımlama gibi dışında tersten çalışır.
> 
> Uzaktan düzenleme ve Uzaktan Yükleme özelliklerine WebMatrix hakkında burada fazla açıklanmaktadır olmaz. Bunlar birden çok kişinin aynı sitede farklı bilgisayarlarda çalışması varsa oldukça kullanışlıdır. Daha fazla bilgi için bkz. [WebMatrix 2 Beta Ile uzak site yayımlama ve düzenleme](https://go.microsoft.com/fwlink/?LinkId=251591).

## <a name="additional-resources"></a>Ek Kaynaklar

- [ASP.net WebMatrix ASP.NET Web sayfaları Forumu](https://forums.asp.net/1224.aspx/1?WebMatrix+and+ASP+NET+Web+Pages), sorularınızı göndermek ve yanıt almak için harika bir yerdir.

> [!div class="step-by-step"]
> [Öncekini](layouts.md)
