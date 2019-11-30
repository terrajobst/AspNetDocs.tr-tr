---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs
title: Geliştirme ve üretim arasındaki yaygın yapılandırma farklılıkları (C#) | Microsoft Docs
author: rick-anderson
description: Önceki öğreticilerde, tüm ilgili dosyaları geliştirme ortamından üretim ortamına kopyalayarak Web sitemizi dağıttık. Ancak, ı...
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 721a5c37-7e21-48e0-832e-535c6351dcae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs
msc.type: authoredcontent
ms.openlocfilehash: 60379c87a8cf58b89066a6070ac659e65930b4fa
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620428"
---
# <a name="common-configuration-differences-between-development-and-production-c"></a>Geliştirme ile Üretim Arasındaki Yaygın Yapılandırma Farklılıkları (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_cs.pdf)

> Önceki öğreticilerde, tüm ilgili dosyaları geliştirme ortamından üretim ortamına kopyalayarak Web sitemizi dağıttık. Ancak, ortamlar arasında yapılandırma farklılıkları olması mümkün değildir, bu da her bir ortamın benzersiz bir Web. config dosyasına sahip olmasını gerektirir. Bu öğretici tipik yapılandırma farklarını inceler ve ayrı yapılandırma bilgilerinin korunmasıyla ilgili stratejileri arar.

## <a name="introduction"></a>Giriş

Basit bir Web uygulaması dağıtmaya yönelik son iki öğretici. [*SITENIZI FTP Istemcisi kullanarak dağıtma*](deploying-your-site-using-an-ftp-client-cs.md) öğreticisini kullanarak, gerekli dosyaları geliştirme ortamından üretime kopyalamak için tek BAŞıNA bir FTP istemcisinin nasıl kullanılacağı gösterildi. Önceki öğreticide, [*sitenizi Visual Studio kullanarak dağıtma*](deploying-your-site-using-visual-studio-cs.md), Visual Studio 'Nun Web sitesi kopyalama aracını ve Yayımla seçeneğini kullanarak dağıtıma bakıyor. Her iki öğreticde, üretim ortamındaki her dosya geliştirme ortamında bir dosyanın kopyasıdır. Ancak, üretim ortamındaki yapılandırma dosyaları geliştirme ortamdakilerle farklı olacak şekilde yaygın olmayan bir durumdur. Bir Web uygulamasının yapılandırması `Web.config` dosyasında depolanır ve genellikle veritabanı, Web ve e-posta sunucuları gibi dış kaynaklarla ilgili bilgiler içerir. Ayrıca, işlenmeyen bir özel durum oluştuğunda gerçekleştirilecek eylem kursu gibi belirli durumlarda uygulamanın davranışını da geçersiz kılar.

Bir Web uygulaması dağıtıldığında, doğru yapılandırma bilgilerinin üretim ortamında bitmesi önemlidir. Çoğu durumda, geliştirme ortamındaki `Web.config` dosyası olduğu gibi üretim ortamına kopyalanamaz. Bunun yerine, `Web.config` özelleştirilmiş bir sürümünün üretime yüklenmesi gerekir. Bu öğretici, daha yaygın yapılandırma farklarından bazılarını kısaca inceler; Ayrıca, ortamlar arasında farklı yapılandırma bilgilerinin sürdürülmesi için bazı teknikleri özetler.

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>Geliştirme ve üretim ortamları arasındaki tipik yapılandırma farklılıkları

`Web.config` dosyası, bir ASP.NET uygulaması için bir dizi yapılandırma bilgisi içerir. Bu yapılandırma bilgilerinin bazıları ortamınızdan bağımsız olarak aynıdır. Örneğin, kimlik doğrulama ayarları ve URL Yetkilendirme kuralları `Web.config` dosyanın `<authentication>` ve `<authorization>` öğeleri genellikle ortamdan bağımsız olarak aynıdır. Ancak dış kaynaklarla ilgili bilgiler gibi diğer yapılandırma bilgileri, genellikle ortama göre farklılık gösterir.

Veritabanı bağlantı dizeleri, ortama göre farklılık gösteren başlıca yapılandırma bilgilerine bir örnektir. Bir Web uygulaması bir veritabanı sunucusuyla iletişim kurduğunda, önce bir bağlantı oluşturmanız ve bir [bağlantı dizesi](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)aracılığıyla elde edilmesi gerekir. Veritabanı bağlantı dizesini doğrudan Web sayfalarında veya veritabanına bağlanan kodda sabit olarak kodlarken, bağlantı dizesi bilgilerinin tek ve merkezi bir konumda olması için `Web.config`[`<connectionStrings>` öğesini](https://msdn.microsoft.com/library/bf7sd233.aspx) yerleştirmek en iyisidir. Geliştirme sırasında üretim sırasında kullanılandan farklı bir veritabanı kullanılır; Sonuç olarak, bağlantı dizesi bilgileri her ortam için benzersiz olmalıdır.

> [!NOTE]
> Gelecekteki öğreticiler veri odaklı uygulamaları dağıtmaya, bu noktada veritabanı bağlantı dizelerinin yapılandırma dosyasında nasıl depolanabileceğini adım adım inceleyeceğiz.

Geliştirme ve üretim ortamlarının amaçlanan davranışı önemli ölçüde farklılık gösterir. Geliştirme ortamındaki bir Web uygulaması, küçük bir geliştiriciler grubu tarafından oluşturuluyor, test ediliyor ve hata ayıklaması yapılıyor. Üretim ortamında, aynı uygulamanın birçok farklı eşzamanlı kullanıcı tarafından ziyaret edilmekte. ASP.NET, geliştiricilerin bir uygulamada test edilmesine ve hata ayıklamasına yardımcı olan bazı özellikler içerir, ancak üretim ortamında performans ve güvenlik nedenleriyle bu özellikler devre dışı bırakılmalıdır. Bu yapılandırma ayarlarına göz atalım.

### <a name="configuration-settings-that-impact-performance"></a>Performansı etkileyen yapılandırma ayarları

Bir ASP.NET sayfası ilk kez ziyaret edildiğinde (veya değiştirildikten sonra ilk kez), bildirime dayalı biçimlendirmenin bir sınıfa dönüştürülmesi ve bu sınıfın derlenmesi gerekir. Web uygulaması otomatik derleme kullanıyorsa, sayfanın arka plan kod sınıfının de derlenmesi gerekir. `Web.config` dosyanın [`<compilation>` öğesi](https://msdn.microsoft.com/library/s10awwz0.aspx)aracılığıyla bir dizi derleme seçeneği yapılandırabilirsiniz.

Hata ayıklama özniteliği, `<compilation>` öğesindeki en önemli özniteliklerin biridir. `debug` özniteliği "true" olarak ayarlanırsa, derlenmiş derlemeler Visual Studio 'da bir uygulamanın hatalarını ayıklarken gereken hata ayıklama sembollerini içerir. Ancak hata ayıklama sembolleri derleme boyutunu artırır ve kodu çalıştırırken ek bellek gereksinimleri vermez. Ayrıca, `debug` özniteliği "true" olarak ayarlandığında, `WebResource.axd` tarafından döndürülen herhangi bir içerik önbelleğe alınmaz, yani Kullanıcı bir sayfayı ziyaret ettiğinde `WebResource.axd`tarafından döndürülen statik içeriği yeniden indirmesi gerekir.

> [!NOTE]
> `WebResource.axd`, ASP.NET 2,0 ' de sunulan ve sunucu denetimlerinin betik dosyaları, görüntüler, CSS dosyaları ve diğer içerikler gibi katıştırılmış kaynakları almak için kullandığı yerleşik bir HTTP Işleyicisidir. `WebResource.axd` nasıl çalıştığı ve özel sunucu denetimlerinizin katıştırılmış kaynaklarına erişmek için nasıl kullanabileceğiniz hakkında daha fazla bilgi için, bkz. [`WebResource.axd`kullanarak URL aracılığıyla gömülü kaynaklara erişme ](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx).

`<compilation>` öğenin `debug` özniteliği, genellikle geliştirme ortamında "true" olarak ayarlanır. Aslında, bir Web uygulamasında hata ayıklamak için bu özniteliğin "true" olarak ayarlanması gerekir. Visual Studio 'da bir ASP.NET uygulamasında hata ayıklamaya çalışırsanız ve `debug` özniteliği "false" olarak ayarlanırsa, Visual Studio, `debug` özniteliği "true" olarak ayarlanana ve bu değişikliği sizin için sunmayı önerene kadar uygulamanın ayıklanamayacağını belirten bir ileti görüntüler.

Performans üzerindeki etkisi nedeniyle, bir üretim ortamında **hiçbir** durumda `debug` özniteliği "true" olarak ayarlanmalıdır. Bu konuyla ilgili daha ayrıntılı bir tartışma için [Scott Guthrie](https://weblogs.asp.net/scottgu/)'nin blog gönderisine bakın, [`debug="true"` etkin olan üretim ASP.NET uygulamalarını çalıştırmayın](https://weblogs.asp.net/scottgu/442448).

### <a name="custom-errors-and-tracing"></a>Özel hatalar ve Izleme

Bir ASP.NET uygulamasında işlenmeyen bir özel durum oluştuğunda, üç durumdan biri olduğunda çalışma zamanına göre balon çıkar:

- Genel çalışma zamanı hata iletisi görüntülenir. Bu sayfa, kullanıcıya bir çalışma zamanı hatası olduğunu bildirir, ancak hatayla ilgili herhangi bir ayrıntı sağlamaz.
- Yeni oluşturulan özel durum hakkında bilgi içeren bir özel durum ayrıntıları iletisi görüntülenir.
- Oluşturduğunuz bir iletiyi görüntüleyen bir ASP.NET sayfası olan özel bir hata sayfası görüntülenir.

İşlenmemiş bir özel durumun yüzde ne olacağı, `Web.config` dosyanın [`<customErrors>` bölümüne](https://msdn.microsoft.com/library/h0hfz6fc.aspx)bağlıdır.

Bir uygulamayı geliştirirken ve test ederken, tarayıcıda herhangi bir özel durumun ayrıntılarını görmeyi sağlar. Ancak, üretimde bir uygulamadaki özel durum ayrıntılarını göstermek potansiyel bir güvenlik riskidir. Üstelik, bu, Web sitenizin uzmanından yararlanmasına neden olur. İdeal olarak, işlenmemiş bir özel durum durumunda geliştirme ortamında bir Web uygulaması özel bir hata sayfası gösterirken özel durumun ayrıntıları gösterir.

> [!NOTE]
> Varsayılan `<customErrors>` bölümü ayarı, yalnızca sayfa localhost aracılığıyla ziyaret edildiğinde özel durum ayrıntıları iletisini gösterir ve aksi takdirde genel çalışma zamanı hata sayfasını gösterir. Bu ideal değildir, ancak varsayılan davranışın yerel olmayan ziyaretçilere özel durum ayrıntılarını açığa çıkarmıyor olduğunu bilmelidir. Sonraki öğreticide, `<customErrors>` bölümünde daha ayrıntılı bilgi incelenecektir ve üretimde bir hata oluştuğunda nasıl özel bir hata sayfası görüntüleneceğini gösterir.

Geliştirme sırasında yararlı olan başka bir ASP.NET özelliği izliyor. İzleme, etkinleştirilirse, her gelen istek hakkındaki bilgileri kaydeder ve son istek ayrıntılarını görüntülemek için `Trace.axd`özel bir Web sayfası sağlar. İzlemeyi açabilir ve `Web.config`[`<trace>` öğesi](https://msdn.microsoft.com/library/6915t83k.aspx) aracılığıyla yapılandırabilirsiniz.

İzlemeyi etkinleştirirseniz, üretimde devre dışı bırakıldığından emin olun. İzleme bilgileri tanımlama bilgilerini, oturum verilerini ve diğer potansiyel duyarlı bilgileri içerdiğinden, üretimde izlemenin devre dışı bırakılması önemlidir. Doğru Haberler, varsayılan olarak izleme devre dışıdır ve `Trace.axd` dosyasına yalnızca localhost aracılığıyla erişilebilir. Bu varsayılan ayarları geliştirmede değiştirirseniz, bu ayarların üretimde devre dışı bırakıldıklarından emin olun.

## <a name="techniques-for-maintaining-separate-configuration-information"></a>Ayrı yapılandırma bilgilerini koruma teknikleri

Geliştirme ve üretim ortamlarında farklı yapılandırma ayarlarına sahip olmak, dağıtım sürecini karmaşıklaştırır. Önceki iki öğreticinin dağıtım süreci, tüm gerekli dosyaları geliştirmeden üretime kopyalamaya dahil değildir, ancak bu yaklaşım yalnızca yapılandırma bilgileri her iki ortamda da aynıysa işe yarar. Farklı yapılandırma bilgileriyle uygulama dağıtmaya yönelik çeşitli teknikler vardır. Daha sonra barındırılan Web uygulamaları için bu seçeneklerin bazılarını kataloglayalım.

### <a name="manually-deploying-the-production-environment-configuration-file"></a>Üretim ortamı yapılandırma dosyasını el ile dağıtma

En basit yaklaşım, tek bir geliştirme ortamı ve bir üretim ortamı için olmak üzere `Web.config` dosyanın iki sürümünü sürdürmektedir. Bir siteyi üretime dağıtmak, `Web.config` dosyası *hariç* olmak üzere tüm dosyaları geliştirme ortamında üretim sunucusuna kopyalamayı gerektirir. Bunun yerine, üretim ortamına özgü `Web.config` dosyası üretime kopyalanabilir.

Bu yaklaşım çok karmaşık değildir, ancak yapılandırma bilgileri seyrek değiştiği için kolayca uygulanması kolaydır. Tek bir Web sunucusunda barındırılan ve yapılandırma bilgileri seyrek olarak değiştirilen küçük bir geliştirme ekibine sahip uygulamalarda en iyi şekilde çalışıyor. Tek başına bir FTP istemcisi kullanarak uygulama dosyalarını el ile dağıttığınızda bu en çok kullanım dışı olur. Visual Studio 'nun Web sitesini Kopyala aracını veya Yayımla seçeneğini kullanırken, önce dağıtıma özgü `Web.config` dosyasını dağıtmadan önce üretime özgü bir dosya ile değiştirmeniz gerekir, sonra dağıtım tamamlandıktan sonra bunları yeniden değiştireceksiniz.

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>Yapı veya dağıtım Işlemi sırasında yapılandırmayı değiştirme

Şimdiye kadar tartışmalar, bir geçici derleme ve dağıtım işlemi olduğunu varsayan varsayılır. Birçok büyük yazılım projesi, açık kaynak, ev-büyütme veya üçüncü taraf araçları kullanan daha fazla şekillendirilmiş işleme sahiptir. Bu tür projeler için, üretim ortamına gönderilmeden önce yapılandırma bilgilerini uygun şekilde değiştirmek üzere derleme veya dağıtım sürecini özelleştirebilirsiniz. Web uygulamanızı [MSBuild](http://en.wikipedia.org/wiki/MSBuild), [Nant](http://nant.sourceforge.net/)veya başka bir derleme aracı kullanarak derleyebilirsiniz, büyük olasılıkla `Web.config` dosyasını, üretime özgü ayarları içerecek şekilde değiştirmek için bir yapı adımı ekleyebilirsiniz. Ya da dağıtım iş akışınız, kaynak denetimi sunucusuna programlı bir şekilde bağlanabilir ve uygun `Web.config` dosyasını alabilir.

Uygun yapılandırma bilgilerini üretime almaya yönelik gerçek yaklaşım, araçlara ve iş akışınıza göre farklılık gösterir. Bu nedenle, bu konuya daha fazla Not vermeyecektir. MSBuild veya NAnt gibi popüler bir yapı aracı kullanıyorsanız, bu araçlara özel dağıtım makalelerini ve öğreticilerini bir Web araması aracılığıyla bulabilirsiniz.

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>Web dağıtımı proje eklentisi aracılığıyla yapılandırma farklarını yönetme

2006 ' de Microsoft, Visual Studio 2005 için Web geliştirme projesi eklentisini yayımladı. Visual Studio 2008 için bir eklenti 2008 ' de yayımlanmıştır. Bu eklenti, ASP.NET geliştiricilerinin Web uygulaması projesiyle birlikte, Web uygulamasını açıkça derleyen ve yerel bir çıkış dizinine dağıtılacak dosyaları kopyalayan ayrı bir Web Dağıtım projesi oluşturmalarına olanak tanır. Web uygulaması projesi, arka planda MSBuild 'i kullanır.

Varsayılan olarak, geliştirme ortamının `Web.config` dosyası çıkış dizinine kopyalanır, ancak bunu özelleştirmek için Web dağıtım projesini ayarlayabilirsiniz.

Aşağıdaki yollarla bu dizine kopyalanmış yapılandırma bilgileri:

- Değiştirilecek bölümü ve yerine konacak metni içeren bir XML dosyasını belirttiğiniz `Web.config` dosya bölümü değişikliği aracılığıyla.
- Bir dış yapılandırma kaynak dosyasının yolunu sağlayarak. Bu seçenek belirlendiğinde, Web dağıtımı projesi belirli bir `Web.config` dosyasını çıkış dizinine kopyalar (geliştirme ortamında kullanılan `Web.config` dosyası yerine).
- Web dağıtımı projesi tarafından kullanılan MSBuild dosyasına özel kurallar ekleyerek.

Web uygulamasını dağıtmak için Web dağıtım projesini oluşturun ve ardından dosyaları projenin çıkış klasöründen üretim ortamına kopyalayın.

Web dağıtım projesini kullanma hakkında daha fazla bilgi edinmek için [MSDN Magazine](https://msdn.microsoft.com/magazine/default.aspx)'in Nisan 2007 sorunundan [Bu Web Dağıtım projelerini](https://msdn.microsoft.com/magazine/cc163448.aspx) inceleyin veya Bu öğreticinin sonunda daha fazla okuma bölümündeki bağlantılara başvurun.

> [!NOTE]
> Web dağıtımı projesi Visual Studio eklentisi olarak uygulandığından ve Visual Studio Express sürümleri (Visual Web Developer dahil) eklentileri desteklemediğinden, Web dağıtım projesini Visual Web Developer ile kullanamazsınız.

## <a name="summary"></a>Özet

Geliştirme aşamasında bir Web uygulamasının dış kaynakları ve davranışı genellikle aynı uygulamanın üretimde olduğu tarihten farklıdır. Örneğin, veritabanı bağlantı dizeleri, derleme seçenekleri ve işlenmeyen bir özel durum oluştuğunda genellikle ortamlar arasında farklılık gösterir. Dağıtım işlemi bu farklılıklara uymalıdır. Bu öğreticide anlatıldığı gibi en basit yaklaşım, alternatif bir yapılandırma dosyasını üretim ortamına el ile kopyalamadır. Web dağıtımı proje eklentisi veya bu tür özelleştirmeleri barındırabilecek daha fazla şekillendirilmiş bir derleme veya dağıtım işlemi kullanılırken daha zarif çözümler mümkündür.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Açıklanan bağlantı dizeleri](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [Veritabanı bağlantı dizeleri @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [`debug="true"` etkin olan üretim ASP.NET uygulamalarını çalıştırma](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [Işlenmeyen özel durumlara düzgün şekilde yanıt verme-Kullanıcı dostu hata sayfalarını görüntüleme](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [Nasıl yapılır: Visual Studio 2008 Web Dağıtım projesi kullanma?](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [Bir veritabanı dağıtımında anahtar yapılandırma ayarları](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual studio 2008 Web Dağıtım projeleri indir](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 Web dağıtımı projeleri indirme](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- [Vs 2008 Web dağıtımı projeleri](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) | [vs 2008 Web dağıtımı proje desteği yayımlandı](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Web Dağıtımı Projeleri](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [Önceki](deploying-your-site-using-visual-studio-cs.md)
> [İleri](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
