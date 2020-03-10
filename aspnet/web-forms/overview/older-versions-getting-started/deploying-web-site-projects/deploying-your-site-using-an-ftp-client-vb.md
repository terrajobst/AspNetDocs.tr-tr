---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
title: Sitenizi FTP Istemcisi kullanarak dağıtma (VB) | Microsoft Docs
author: rick-anderson
description: Bir ASP.NET uygulamasını dağıtmanın en basit yolu, gerekli dosyaları geliştirme ortamından üretim ortamına el ile kopyalamadır. Thi...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 09279194-bcf9-4b59-a09d-c68e5926a758
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
msc.type: authoredcontent
ms.openlocfilehash: 7875304c672625d8c0eaaf0fea8ef509bb801a3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545509"
---
# <a name="deploying-your-site-using-an-ftp-client-vb"></a>Sitenizi FTP İstemcisi Kullanarak Dağıtma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_vb.pdf)

> Bir ASP.NET uygulamasını dağıtmanın en basit yolu, gerekli dosyaları geliştirme ortamından üretim ortamına el ile kopyalamadır. Bu öğreticide, masaüstünüzdeki dosyaları Web ana bilgisayar sağlayıcısına almak için bir FTP istemcisinin nasıl kullanılacağı gösterilmektedir.

## <a name="introduction"></a>Giriş

Önceki öğreticide, bir ASP.NET sayfalarından, ana sayfadan, özel bir temel `Page` sınıftan, bir dizi görüntüden ve üç CSS stil sayfasından oluşan basit bir Book Review ASP.NET Web uygulaması tanıtılmıştır. Artık bu uygulamayı bir Web ana bilgisayar sağlayıcısına dağıtmaya hazırdır, bu noktada uygulamaya Internet bağlantısı olan herkes tarafından erişilebilecektir!

[*Hangi dosyaların dağıtılması gerektiğini belirleme*](determining-what-files-need-to-be-deployed-vb.md) öğreticilerimizden, hangi dosyaların Web ana bilgisayar sağlayıcısına kopyalanması gerektiğini biliyoruz. (Hangi dosyaların kopyalandığına, uygulamanızın açıkça veya otomatik olarak derlendiğine göre geri çekin.) Ancak geliştirme ortamından (masaüstümüzü), üretim ortamına (Web ana bilgisayar sağlayıcısı tarafından yönetilen Web sunucusu) kadar dosya nasıl alınır? [ **F** ve **T** ransfer **P** rotocol (FTP)](http://en.wikipedia.org/wiki/File_Transfer_Protocol) , dosyaları ağ üzerinden bir makineden diğerine kopyalamak için yaygın olarak kullanılan bir protokoldür. Başka bir seçenek de FrontPage Server Extensions (FPSE). Bu öğreticide, gerekli dosyaları geliştirme ortamından üretim ortamına dağıtmak için tek başına FTP istemci yazılımı kullanımı ele alınmaktadır.

> [!NOTE]
> Visual Studio, FTP aracılığıyla Web siteleri yayımlamaya yönelik araçlar içerir; Bu araçların yanı sıra, FPSE kullanan araçlara göz atın ve sonraki öğreticide ele alınmıştır.

FTP kullanarak dosyaları kopyalamak için geliştirme ortamında bir *FTP istemcisi* gerekir. FTP istemcisi, yüklü olduğu bilgisayardan *FTP sunucusu*çalıştıran bir bilgisayara dosya kopyalamak için tasarlanan bir uygulamadır. (Web ana bilgisayar sağlayıcınız FTP aracılığıyla dosya aktarımlarını destekliyorsa, çoğu durumda, Web sunucularında çalışan bir FTP sunucusu vardır.) Kullanılabilir sayıda FTP istemci uygulaması vardır. Web tarayıcınız bir FTP istemcisi olarak da çift olabilir. Sık kullanılan FTP istemcim ve bu öğretici için kullanacağınız [FileZilla](http://filezilla-project.org/), Windows, Linux ve Mac için kullanılabilen ücretsiz, açık KAYNAKLı bir FTP istemcisidir. Tüm FTP istemcileri çalışacaktır, ancak en çok rahat olduğunu hissettiğiniz bir istemciyi kullanmayı ücretsiz hale getirmeniz gerekir.

Bu öğreticiyi takip ediyorsanız, bu öğreticiyi tamamlayabilmeniz için bir Web ana bilgisayar sağlayıcısına sahip bir hesap oluşturmanız gerekir. Önceki öğreticide belirtildiği gibi, geniş bir fiyat, özellik ve hizmet kalitesi yelpazesini içeren, Web ana bilgisayar sağlayıcısı şirketlerinden oluşan Gaggle vardır. Bu öğretici serisi için, Web barındırma sağlayıcım olarak [Discount ASP.net](http://discountasp.net) kullanıyorum, ancak sitenizin üzerinde geliştirildiği ASP.NET sürümünü destekledikleri sürece herhangi bir Web ana bilgisayar sağlayıcısıyla birlikte takip edebilirsiniz. (Bu öğreticiler ASP.NET 3,5 kullanılarak oluşturulmuştur.) Ayrıca, bu öğreticide FTP kullanarak dosyaları Web ana bilgisayar sağlayıcısına kopyalayacağız ve gelecekte de Web ana bilgisayar sağlayıcınız Web sunucularına FTP erişimini destekliyor olması zorunludur. Neredeyse tüm Web ana bilgisayar sağlayıcıları bu özelliği sunar, ancak kaydolmadan önce iki kez kontrol etmeniz gerekir.

## <a name="deploying-the-book-review-web-application-project"></a>Kitap Inceleme Web uygulaması projesini dağıtma

Book Review Web uygulamasının iki sürümünün bulunduğunu hatırlayın: Web uygulaması proje modeli (Bookincelemenizi swap) kullanılarak, diğeri ise Web sitesi proje modeli (BookReview Swsp) kullanılarak uygulanır. Proje türü, sitenin otomatik olarak mı yoksa açık mı olduğunu ve derleme modelinin hangi dosyaların dağıtılması gerektiğini belirler. Bu nedenle, bookinceleyswap ile başlayarak kitap yazısı takas ve Bookinceleyswsp projelerini ayrı ayrı dağıtma konusunda inceleyeceğiz. Daha önce yapmadıysanız, bu iki ASP.NET uygulamasını indirmek için bir dakikanızı ayırın.

`BookReviewsWAP` klasöre gidip `BookReviewsWAP.sln` dosyasına çift tıklayarak Bookgözden değiştirme projesini başlatın. Projeyi dağıtılmadan önce, kaynak koddaki tüm değişikliklerin derlenmiş derlemeye eklendiğinden emin olmak için oluşturmak önemlidir. Projeyi derlemek için, derleme menüsüne gidin ve Build Bookgözden geçirmeyi Değiştir menü seçeneğini belirleyin. Bu, projedeki kaynak kodu, `Bin` klasörüne yerleştirilmiş olan tek bir derlemede derler `BookReviewsWAP.dll`.

Artık gerekli dosyaları dağıtmaya hazırsınız! FTP istemcinizi başlatın ve Web barındırma sağlayıcınızdaki Web sunucusuna bağlanın. (Bir Web barındırma şirketi ile kaydolduğunuzda, FTP sunucusuna nasıl bağlanacağından ilgili bilgileri e-posta ile bir Kullanıcı adı ve parola ile birlikte bu adresi de içerir.)

Aşağıdaki dosyaları masaüstünüzden Web barındırma sağlayıcınızdaki kök Web sitesi klasörüne kopyalayın. Web ana bilgisayar sağlayıcısındaki Web sunucusunda FTP kullandığınızda büyük olasılıkla kök Web sitesi dizininde olabilirsiniz. Ancak bazı Web ana bilgisayar sağlayıcılarının, Web sitesi dosyalarınız için kök klasör olarak hizmet veren `www` veya `wwwroot` adlı bir alt klasörü vardır. Son olarak, dosyaları FTPing yaparken, üretim ortamında ilgili klasör yapısını (`Bin` klasörü, `Fiction` klasörü, `Images` klasörü vb.) oluşturmanız gerekebilir.

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` klasörünün tüm içeriği
- `Images` klasörünün (ve alt klasörünün, `BookCovers`) tüm içerikleri
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

Şekil 1 ' de gerekli dosyalar kopyalandıktan sonra FileZilla gösterilmektedir. FileZilla, sol taraftaki yerel bilgisayardaki dosyaları ve sağ taraftaki uzak bilgisayardaki dosyaları görüntüler. Şekil 1 ' de gösterildiği gibi, `About.aspx.vb`gibi ASP.NET kaynak kodu dosyaları yerel bilgisayardır (geliştirme ortamı), ancak kod dosyalarının açık derleme kullanılırken dağıtılması gerekmiyorsa, Web ana bilgisayar sağlayıcısına (üretim ortamı) kopyalanmaz.

> [!NOTE]
> Kaynak kodu dosyalarının, dikkate alındıkları için üretim sunucusunda bulunması hiçbir zarar yoktur. ASP.NET yasaklıyor HTTP isteklerini kaynak kodu dosyaları için varsayılan olarak, kaynak kodu dosyaları üretim sunucusunda mevcut olsa bile, Web sitenize ziyaretçi erişemez. (Yani, bir Kullanıcı `http://www.yoursite.com/Default.aspx.vb` ziyaret etmeye çalışırsa, bu dosya türlerinin `.vb` dosyaların yasak olduğunu açıklayan bir hata sayfası alırlar.)

[![, masaüstünüzdeki gerekli dosyaları Web ana bilgisayar sağlayıcısındaki Web sunucusuna kopyalamak için bir FTP Istemcisi kullanın.](deploying-your-site-using-an-ftp-client-vb/_static/image2.png)](deploying-your-site-using-an-ftp-client-vb/_static/image1.png)

**Şekil 1**: masaüstünüzdeki gerekli dosyaları Web ana bilgisayar sağlayıcısındaki Web sunucusuna kopyalamak IÇIN bir FTP istemcisi kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-an-ftp-client-vb/_static/image3.png))

Sitenizi dağıttıktan sonra siteyi test etmek biraz zaman ayırın. Bir etki alanı adı satın aldıysanız ve DNS ayarlarını doğru şekilde yapılandırdıysanız, etki alanı adınızı girerek sitenizi ziyaret edebilirsiniz. Alternatif olarak, Web ana bilgisayar sağlayıcınız size sitenizin bir URL 'sini sağlamalıdır, bu da *AccountName*gibi bir şey arayacaktır. *webhostprovider*. com veya *webhostprovider*. com/*AccountName*. Örneğin, Indirimli ASP.NET 'daki Hesabım URL 'SI: `http://httpruntime.web703.discountasp.net`.

Şekil 2 ' de dağıtılan kitap Incelemeleri sitesi gösterilmektedir. Bunu, Indirimli ASP üzerinde görüntülüyorum. AĞ sunucularının `http://httpruntime.web703.discountasp.net`. Bu noktada, Internet bağlantısı olan herkesin Web sitemi görüntüleyeme zamanı vardır! Beklentiğimiz gibi, site geliştirme ortamında test edilirken olduğu gibi görünür ve davranır.

> [!NOTE]
> Uygulamanızı görüntülerken bir hata alırsanız doğru dosya kümesini dağıttığınızdan emin olun. Ardından, sorun ile ilgili herhangi bir ipuçları ortaya çıkardığından emin olmak için hata iletisini kontrol edin. Bundan sonra, Web barındırma şirketinizin yardım masasına veya sorunuzu [ASP.net forumlarındaki](https://forums.asp.net/)uygun foruma gönderebilirsiniz.

[Kitap Incelemeleriyle ilgili ![, artık Internet bağlantısı olan herkes tarafından erişilebilir.](deploying-your-site-using-an-ftp-client-vb/_static/image5.png)](deploying-your-site-using-an-ftp-client-vb/_static/image4.png)

**Şekil 2**: kitap Inceleme sitesine artık Internet bağlantısı olan herkes erişebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](deploying-your-site-using-an-ftp-client-vb/_static/image6.png))

## <a name="deploying-the-book-review-web-site-project"></a>Kitap Inceleme Web sitesi projesini dağıtma

Book, Swsp Web sitesi projesi gibi otomatik derleme kullanan bir ASP.NET uygulaması dağıtıldığında, `Bin` klasöründe derlenmiş bir derleme yoktur. Sonuç olarak, Web uygulamasının kaynak kodu dosyalarının üretim ortamına dağıtılması gerekir. Bu işlemi adım adım inceleyelim.

Web uygulaması projesinde olduğu gibi, uygulamayı dağıtılmadan önce ilk oluşturmak sizin için bir uygulamadır. Bir Web sitesi projesi derlenirken derleme oluşturmaz, sayfada herhangi bir derleme zamanı hatası olup olmadığını denetler. Sitenize yönelik bir ziyaretçinin sizin için bulmasını sağlamak yerine bu hataları hemen bulmanın daha iyi olması gerekir!

Projeyi başarıyla oluşturduktan sonra, aşağıdaki dosyaları Web barındırma sağlayıcınızdaki kök Web sitesi klasörüne kopyalamak için FTP istemcinizi kullanın. Üretim ortamında ilgili klasör yapısını oluşturmanız gerekebilir.

> [!NOTE]
> Bookgözden değiştirme projesini zaten dağıttıysanız ancak bookbelgeadı \ SP projesini dağıtmayı denemek istiyorsanız, önce Web sunucusunda, bookbelgedosyası değiştirme dağıtılırken karşıya yüklenen tüm dosyaları silin ve ardından kitap listesi \ SP için dosyaları dağıtın.

- `~/Default.aspx`
- `~/Default.aspx.vb`
- `~/About.aspx`
- `~/About.aspx.vb`
- `~/Site.master`
- `~/Site.master.vb`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` klasörünün tüm içeriği
- `Images` klasörünün (ve alt klasörünün, `BookCovers`) tüm içerikleri
- `~/App_Code/BasePage.vb`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.vb`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.vb`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.vb`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.vb`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.vb`

Şekil 3 ' te, gerekli dosyaları kopyaladıktan sonra FileZilla gösterilmektedir. Görebileceğiniz gibi, otomatik derleme kullanılırken kod dosyalarının dağıtılması gerektiğinden `About.aspx.vb`gibi ASP.NET kaynak kodu dosyaları hem yerel bilgisayarda (geliştirme ortamında) hem de Web ana bilgisayar sağlayıcısında (üretim ortamında) bulunur.

[![, masaüstünüzdeki gerekli dosyaları Web ana bilgisayar sağlayıcısındaki Web sunucusuna kopyalamak için bir FTP Istemcisi kullanın](deploying-your-site-using-an-ftp-client-vb/_static/image8.png)](deploying-your-site-using-an-ftp-client-vb/_static/image7.png)

**Şekil 3**: gerekli dosyaları masaüstünüzden Web barındırma sağlayıcısındaki Web sunucusuna kopyalamak IÇIN bir FTP istemcisi kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-an-ftp-client-vb/_static/image9.png))

Kullanıcı deneyimi, uygulamanın derleme modelinden etkilenmez. Aynı ASP.NET sayfalarına erişilebilir ve Web sitesinin Web uygulaması proje modeli veya Web sitesi proje modeli kullanılarak oluşturulup oluşturulmayacağı aynı şekilde görünür ve aynı şekilde davranır.

## <a name="updating-a-web-application-on-production"></a>Üretimde bir Web uygulamasını güncelleştirme

Web uygulaması geliştirme ve dağıtımı tek seferlik bir işlem değildir. Örneğin, kitap Incelemesi Web sitesini oluştururken çeşitli sayfaları yapılandırdım ve ilgili kodu kişisel bilgisayarıma (geliştirme ortamı) yazdı. Belirli bir kararlı duruma ulaştıktan sonra uygulamamı, diğerlerinin siteyi ziyaret edip incelemelerimi okuyabilmesini sağlayacak şekilde dağıttım. Ancak dağıtım bu sitede geliştirmemin sonunu işaretlemez. Daha fazla kitap incelemesi ekleyebilir veya ziyaretçilerin kitapları derecelendirmek veya kendi yorumlarını bırakmak gibi yeni özellikler uygulayabilirim. Bu tür geliştirmeler geliştirme ortamında geliştirilir ve tamamlandığında, dağıtılması gerekir. Geliştirme ve dağıtım, bu nedenle, döngüsel. Bir uygulama geliştirin ve ardından dağıtın. Site canlı ve üretimde, yeni özellikler eklenir ve hatalar zamana göre düzeltilir, bu da uygulamayı yeniden dağıtmaktadır. Vb.

Tahmin edebileceğiniz gibi, bir Web uygulamasını yeniden dağıttığınızda yalnızca yeni ve değiştirilmiş dosyaları kopyalamanız gerekir. Değişmeyen sayfaları veya sunucu ya da istemci tarafı destek dosyalarını yeniden dağıtmanız gerekmez (bunun için bir sorun olmasa da).

> [!NOTE]
> Açık derlemeyi kullanırken göz önünde bulundurmanız gereken tek şey, projeye yeni bir ASP.NET sayfası eklemediğinizde veya kodla ilgili herhangi bir değişiklik yapmanız gerektiğinde, `Bin` klasöründeki derlemeyi güncelleştiren projenizi yeniden oluşturmanız gerekir. Sonuç olarak, üretimde bir Web uygulamasını güncelleştirirken (diğer yeni ve güncelleştirilmiş içerikle birlikte) Bu güncelleştirilmiş derlemeyi üretime kopyalamanız gerekir.

Ayrıca, `Web.config` veya `Bin` dizinindeki dosyalardaki değişikliklerin, Web sitesinin uygulama havuzunu durdurup yeniden başlatduğunu da anlayın. Oturum durumunuzla `InProc` modu (varsayılan) kullanılarak depolanıyorsa, bu anahtar dosyaları her değiştirildiğinde sitenizin ziyaretçileri oturum durumlarını kaybeder. Bu hususları önlemek için `StateServer` veya `SQLServer` modlarını kullanarak oturumu depolamayı düşünün. Bu konu hakkında daha fazla bilgi için [oturum durumu modlarını](https://msdn.microsoft.com/library/ms178586.aspx)okuyun.

Son olarak, bir uygulamanın yeniden dağıtılmasının, üretim ortamına kopyalanması gereken dosyaların sayısına ve boyutuna bağlı olarak birkaç saniyeden birkaç dakikaya kadar bir süre sürebileceğini aklınızda bulundurun. Bu süre boyunca, sitenizi ziyaret eden kullanıcılar hata veya tek davranış gösterebilir. Uygulamanızın kök dizinine `App_Offline.htm` adlı bir sayfa ekleyerek uygulamanızın, sitenin bakım için devre dışı olduğunu (veya herhangi bir şekilde) ve kısa süre sonra geri alınacağını "olarak kullanabilirsiniz. `App_Offline.htm` dosyası mevcut olduğunda, ASP.NET Runtime tüm gelen istekleri bu sayfaya yönlendirir.

## <a name="summary"></a>Özet

Bir Web uygulamasının dağıtımı, gerekli dosyaları geliştirme ortamından üretim ortamına kopyalamayı gerektirir. Dosyaların bir ağ üzerinden aktarıldığı en yaygın yolu Dosya Aktarım Protokolü (FTP) ve Web ana bilgisayar sağlayıcılarının çoğu Web sunucularına FTP erişimini destekler. Bu öğreticide, gerekli dosyaları Web sunucusuna dağıtmak için bir FTP istemcisinin nasıl kullanılacağını gördük. Dağıtıldıktan sonra, Web sitesi Internet bağlantısı olan herkes tarafından ziyaret edilebilir!

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [App\_çevrimdışı. htm ve "IE kolay hatalar" özelliği etrafında çalışıyor](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [Oturum durumu modları](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [Önceki](determining-what-files-need-to-be-deployed-vb.md)
> [İleri](deploying-your-site-using-visual-studio-vb.md)
