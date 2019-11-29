---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
title: Sitenizi Visual Studio kullanarak dağıtma (C#) | Microsoft Docs
author: rick-anderson
description: Visual Studio, bir Web sitesi dağıtmaya yönelik araçlar içerir. Bu öğreticide bu araçlar hakkında daha fazla bilgi edinin.
ms.author: riande
ms.date: 04/01/2009
ms.assetid: cde4ee53-a5d0-4937-a54b-67877e8266c3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
msc.type: authoredcontent
ms.openlocfilehash: 4259e51f5a3e6a97bae2aa27b76cbd56ca3449d6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636312"
---
# <a name="deploying-your-site-using-visual-studio-c"></a>Sitenizi Visual Studio Kullanarak Dağıtma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_cs.pdf)

> Visual Studio, bir Web sitesi dağıtmaya yönelik araçlar içerir. Bu öğreticide bu araçlar hakkında daha fazla bilgi edinin.

## <a name="introduction"></a>Giriş

Önceki öğretici bir Web ana bilgisayar sağlayıcısına basit bir ASP.NET Web uygulamasının nasıl dağıtılacağını incelemiştir. Bu öğreticide, gerekli dosyaları geliştirme ortamından üretim ortamına aktarmak için FileZilla gibi bir FTP istemcisinin nasıl kullanılacağı gösterildi. Visual Studio, bir Web ana bilgisayar sağlayıcısına dağıtımı kolaylaştırmak için yerleşik araçlar da sunar. Bu öğreticide, bu araçların ikisi de incelenir: FTP veya FrontPage Sunucu uzantılarını kullanarak uzak Web sunucusuna veya buradan dosya taşıyabileceğiniz Web sitesi kopyalama aracı. ve tüm Web sitesini belirtilen bir konuma kopyalayan Yayımla aracı.

> [!NOTE]
> Visual Studio tarafından sunulan diğer dağıtımla ilgili araçlar, [Web kurulum projelerini](https://msdn.microsoft.com/library/wx3b589t.aspx) ve [Web dağıtımı projeleri](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) eklentisini içerir. Web Kurulum projeleri bir Web sitesinin içeriğini ve yapılandırma bilgilerini tek bir MSI dosyasında paketleyin. Bu seçenek, bir intranet içinde dağıtılan Web siteleri için veya müşterilerin kendi Web sunucularına yükleyen önceden paketlenmiş bir Web uygulaması satan şirketler için yararlıdır. Web dağıtımı projeleri eklentisi, geliştirme ortamları ve üretim ortamları için derlemeler arasında yapılandırma farklılıkları belirtmeyi kolaylaştıran bir Visual Studio eklentisi. Web Kurulum projeleri bu öğretici serisinde açıklanmıyor; Web dağıtımı projeleri, [*geliştirme ve üretim öğreticisi arasındaki yaygın yapılandırma farklılıkları*](common-configuration-differences-between-development-and-production-cs.md) halinde özetlenir.

## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>Web sitesi kopyalama aracını kullanarak sitenizi dağıtma

Visual Studio 'nun Web sitesi kopyalama aracı, tek başına bir FTP istemcisinin işlevselliğiyle benzerdir. Web sitesi kopyalama aracı bir Nutshell 'de FTP veya FrontPage Sunucu uzantıları aracılığıyla uzak bir Web sitesine bağlanmanızı sağlar. FileZilla 'ın Kullanıcı arabirimine benzer şekilde, kopyalama Web sitesi kullanıcı arabirimi iki bölmeden oluşur: sol bölmede yerel dosyalar listelenir ve sağ bölmede Bu dosyalar hedef sunucuda listelenir.

> [!NOTE]
> Web sitesi kopyalama aracı yalnızca Web sitesi projeleri için kullanılabilir. Visual Studio, bir Web uygulaması projesiyle çalışırken bu aracı sunar.

Şimdi, kitap Incelemesi uygulamasını üretime yayımlamak için Web sitesi kopyalama aracı 'nı kullanmaya göz atalım. Copy Web Site Aracı yalnızca Web sitesi proje modelini kullanan projelerle birlikte çalıştığından, bu aracı yalnızca Bookinceleyswsp projesiyle birlikte kullanmayı da inceleyebilirsiniz. Bu projeyi açın.

Çözüm Gezgini Web sitesi Kopyala simgesine tıklayarak web sitesini Kopyala araç projesini başlatın (Bu simge Şekil 1 ' de bir daire içinde); Alternatif olarak, Web sitesi menüsünden Web sitesini Kopyala seçeneğini belirleyebilirsiniz. Her iki yaklaşım da Şekil 1 ' de gösterilen kopyalama Web sitesi kullanıcı arabirimini başlatır; henüz uzak bir sunucuya bağlanamadığımızda Şekil 1 ' deki sol bölme doldurulur.

[Web sitesi kopyalama aracının Kullanıcı arabirimi Iki bölmeye ayrılmıştır ![](deploying-your-site-using-visual-studio-cs/_static/image2.png)](deploying-your-site-using-visual-studio-cs/_static/image1.png)

**Şekil 1**: kopya web sitesi aracının Kullanıcı arabirimi Iki bölmeye ayrılmıştır ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image3.png))

Sitemizi dağıtmak için öncelikle web ana bilgisayar sağlayıcısına bağlanmamız gerekiyor. Web sitesini Kopyala Kullanıcı arabiriminin en üstündeki Bağlan düğmesine tıklayın. Bu, Şekil 2 ' de gösterilen Web sitesini Aç iletişim kutusunu görüntüler.

Sol taraftaki dört seçenekten birini seçerek hedef Web sitesine bağlanabilirsiniz:

- **Dosya sistemi** -sitenizi bilgisayarınızdan erişilebilen bir klasöre veya ağ paylaşımında dağıtmak için bunu seçin.
- **Yerel IIS** -bu seçeneği, siteyi bilgisayarınızda yüklü olan IIS Web sunucusuna dağıtmak için kullanın.
- **FTP sitesi** -FTP kullanarak uzak Web sitesine bağlanın.
- **Uzak site** -FrontPage Sunucu uzantılarını kullanarak uzak Web sitesine bağlanın.

Web ana bilgisayar sağlayıcılarının çoğu FTP 'yi destekler, ancak daha az sayıda FrontPage Sunucu Uzantısı desteği sunar. Bu nedenle, FTP sitesi seçeneğini seçtim ve ardından şekil 2 ' de gösterildiği gibi bağlantı bilgilerini girdim.

[Hedef Web sitesini ![belirtin](deploying-your-site-using-visual-studio-cs/_static/image5.png)](deploying-your-site-using-visual-studio-cs/_static/image4.png)

**Şekil 2**: hedef Web sitesini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image6.png))

Bağlandıktan sonra, Web sitesi kopyalama aracı, dosyaları sağ bölmedeki uzak siteye yükler ve her bir dosyanın durumunu gösterir: yeni, silinmiş, değiştirilmiş veya değiştirilmemiş. Yerel siteden uzak siteye veya tam tersi yönde bir dosya kopyalayabilirsiniz.

Ayrıca, Bookinceleyeceğiz Swsp projesine yeni bir sayfa ekleyelim ve sonra Web sitesini Kopyala aracını eylemde görebilmemiz için dağıtırsınız. `Privacy.aspx`adlı kök dizinde Visual Studio 'da yeni bir ASP.NET sayfası oluşturun. Sayfanın ana sayfa `Site.master` kullanmasını ve sitenizin gizlilik ilkesini bu sayfaya eklemesini sağlayabilirsiniz. Şekil 3 ' te Bu sayfa oluşturulduktan sonra Visual Studio gösterilmektedir.

[![Web sitesinin kök klasörüne &lt;Code&gt;privacy. aspx&lt;/Code&gt; adlı yeni bir sayfa ekleyin](deploying-your-site-using-visual-studio-cs/_static/image8.png)](deploying-your-site-using-visual-studio-cs/_static/image7.png)

**Şekil 3**: Web sitesinin kök klasörüne `Privacy.aspx` adlı yeni bir sayfa ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image9.png))

Sonra, Web sitesi kopyalama Kullanıcı arabirimine dönün. Şekil 4 ' ün gösterdiği gibi, sol bölmede artık yeni dosyalar bulunur-`Policy.aspx` ve `Policy.aspx.cs`. Ayrıca, bu dosyalar bir ok simgesiyle ve yeni durumu olarak işaretlenir ve bu, uzak sitede değil, yerel sitede var olduğunu gösterir.

[Web sitesi kopyalama aracı ![, sol bölmedeki yeni &lt;Code&gt;privacy. aspx&lt;/Code&gt; sayfasını Içerir](deploying-your-site-using-visual-studio-cs/_static/image11.png)](deploying-your-site-using-visual-studio-cs/_static/image10.png)

**Şekil 4**: Web sitesini Kopyala Aracı, sol bölmedeki yeni `Privacy.aspx` sayfasını içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image12.png))

Yeni dosyaları dağıtmak için bunları seçin ve ardından uzak siteye aktarmak üzere ok simgesine tıklayın. Aktarım işlemi tamamlandıktan sonra `Policy.aspx` ve hem yerel hem de uzak sitelerde durum değiştirilmeden `Policy.aspx.cs` dosyalar bulunur.

Yeni dosyalar listelenerek, Web sitesi kopyalama aracı yerel ve uzak siteler arasında farklı olan dosyaları vurgular. Bunu eylemde görmek için `Privacy.aspx` sayfasına dönün ve gizlilik ilkesine birkaç sözcük daha ekleyin. Sayfayı kaydedin ve Web sitesi Kopyala aracına geri dönün. Şekil 5 ' te gösterildiği gibi, sol bölmedeki `Privacy.aspx` sayfasının, uzak siteyle eşitlenmemiş olduğunu belirten bir durumu değiştirildi.

[Web sitesi kopyalama aracı ![, &lt;Code&gt;privacy. aspx&lt;/Code&gt; sayfasının değiştirildiğini gösterir](deploying-your-site-using-visual-studio-cs/_static/image14.png)](deploying-your-site-using-visual-studio-cs/_static/image13.png)

**Şekil 5**: Web sitesini kopyala aracı `Privacy.aspx` sayfanın değiştirildiğini belirtir ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image15.png))

Web sitesi kopyalama aracı Ayrıca, son kopyalama işleminden bu yana bir dosyanın silinip silinmediğini de gösterir. `Privacy.aspx` yerel projeden silin ve Web sitesi kopyalama aracını yenileyin. `Privacy.aspx` ve `Privacy.aspx.cs` dosyalar sol bölmede listelenir, ancak en son kopyalama işleminden bu yana kaldırıldıklarından sonra silinmiş bir durum durumunda kalır.

## <a name="publishing-a-web-application"></a>Web uygulaması yayımlama

Web uygulamanızı Visual Studio içinden dağıtmanın başka bir yolu da, derleme menüsü aracılığıyla erişilebilen Yayımla seçeneğini kullanmaktır. Yayımla seçeneği, uygulamayı açıkça derler ve gerekli tüm dosyaları belirtilen uzak siteye kopyalar. Kısa süre içinde de göreceğiniz gibi yayımla seçeneği Web sitesini Kopyala aracından daha fazla yeniden bağlama olur. Web sitesi kopyalama aracı yerel ve uzak sitelerdeki dosyaları incelemenizi sağlar ve gerektiğinde tek tek dosyaları karşıya yüklemenize veya indirmenize izin verir, Yayımla seçeneği tüm Web uygulamasını dağıtır.

Gerekli tüm dosyaları belirtilen uzak siteye kopyalamaya ek olarak, Yayımla seçeneği de uygulamayı açıkça derler. Web uygulaması projelerinin açık olarak derlenmesi gerekdiğine göre, yayımlama seçeneğinin Web uygulaması projeleri için kullanılabilir olduğu aniden Hayır olarak gelmelidir. Ne kadar çok anlamı olan, yayımlama seçeneğinin de Web sitesi projeleri için kullanılabilir olması olabilir. [*Hangi dosyaların dağıtılması gerektiğini belirleme*](determining-what-files-need-to-be-deployed-cs.md) öğreticisinde belirtildiği gibi, Web sitesi projeleri, *ön derleme*olarak adlandırılan bir işlem aracılığıyla açıkça derlenebilir. Bu öğretici, Web uygulaması projeleriyle Yayımla seçeneğinin kullanımına odaklanmaktadır; daha sonraki bir öğretici, Web sitesi projeleriyle Yayımla seçeneğini kullanmaya bakacağımız noktada ön derlemeyi keşfedebilir.

> [!NOTE]
> Web sitesi projeleri ve Web uygulaması projeleri için Visual Studio 'da yayımla seçeneği kullanılabilir olsa da, Visual Web Developer yalnızca Web uygulaması projeleri için Yayımla seçeneğini sunar.

Yayımla seçeneğini kullanarak kitap Incelemeleri uygulamasını dağıtmaya bakalım. Visual Studio 'da Bookgözden değiştirme (Web uygulaması projesi) öğesini açarak başlayın. Yayımla menüsünde Build Bookbelgeet takas projesini seçin. Bu, diğer yapılandırma seçenekleri arasında (bkz. Şekil 6) hedef konum isteyen bir iletişim kutusu açar. Web sitesi kopyalama aracı ile aynı şekilde yerel bir klasöre, IIS 'de yerel bir Web sitesine, FrontPage Sunucu uzantılarını destekleyen uzak bir Web sitesine veya bir FTP sunucu adresine işaret eden bir konum girebilirsiniz. Uzak Web sunucusundaki dosyaları dağıtılan dosyalarla değiştirmeyi veya yayımlamadan önce uzak sitedeki tüm içeriği silmeyi seçebilirsiniz. Ayrıca, kopyalamayı isteyip istemediğinizi de belirtebilirsiniz:

- Yalnızca projedeki dosyalar, gereksiz kaynak kodu ve projeyle ilgili dosyaları atlayacak şekilde uygulamayı çalıştırmak için gereklidir.
- Çözüm dosyası gibi kaynak kod dosyalarını ve Visual Studio proje dosyalarını içeren tüm proje dosyaları.
- Kaynak proje klasöründeki tüm dosyalar, projeye dahil edilip edilmediğine bakılmaksızın kaynak proje klasöründeki tüm dosyaları kopyalar.

Ayrıca, `App_Data` klasörünün içeriğini karşıya yükleme seçeneği de vardır.

[Hedef Web sitesini ![belirtin](deploying-your-site-using-visual-studio-cs/_static/image17.png)](deploying-your-site-using-visual-studio-cs/_static/image16.png)

**Şekil 6**: hedef Web sitesini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image18.png))

Kitap Incelemesi uygulaması için uzak site, Web sitesi Kopyala aracı aracılığıyla kitap İnceleme Swsp projesi kopyalanırken dağıtılan dosyaları içerir. Bu nedenle, var olan tüm içeriği silerek Yayımla seçeneğinin başlatılmasını sağlayabilirsiniz. Ayrıca, gerekli dosyaları, gereksiz kaynak kodu ve proje dosyaları ile üretim ortamına göre değil yalnızca kopyalayalim. Bu seçenekleri belirttikten sonra Yayımla düğmesine tıklayın. Sonraki birkaç saniye içinde, Visual Studio gerekli dosyaları hedef siteye dağıtır ve ilerleme durumunu çıkış penceresinde görüntüler.

Şekil 7, yayımlama işlemi tamamlandıktan sonra FTP sitesindeki dosyaları gösterir. Yalnızca biçimlendirme sayfaları ve gerekli sunucu ve istemci tarafı destek dosyalarının karşıya yüklendiğini unutmayın.

[Yalnızca gerekli dosyalar üretim ortamında yayımlandı ![](deploying-your-site-using-visual-studio-cs/_static/image20.png)](deploying-your-site-using-visual-studio-cs/_static/image19.png)

**Şekil 7**: yalnızca gerekli dosyalar üretim ortamında yayımlandı ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-your-site-using-visual-studio-cs/_static/image21.png))

Yayımla seçeneği, Web sitesi kopyalama aracından daha az bir şekilde gelişmiş bir araçtır. Web sitesi kopyalama aracı, yerel ve uzak sitelerdeki dosyaları incelemenize ve bunların nasıl farklı olduğunu görmenize izin verir; yayımla seçeneği böyle bir arabirim sağlamaz. Ayrıca, Web sitesi kopyalama aracı tek tek değişiklikler yapmanızı, dosyaları karşıya yüklemeyi veya silmenizi sağlar. Yayımla seçeneği, ayrıntılı denetime izin vermez; Bunun yerine, *Tüm* uygulamayı yayınlar. Bu davranışın profesyonelleri ve dezavantajları vardır. Artı tarafında, Yayımla seçeneğini kullanırken önemli bir dosyayı karşıya yükleme işleminin ne zaman onaylanmayacağınızı bilirsiniz. Ancak çok büyük bir Web sitesinde küçük bir değişiklik yaptıysanız ne olacağını düşünün; Yayımla seçeneğiyle, bu sayfayı veya değiştirilmiş iki ayarı güncelleştiremezsiniz, ancak Visual Studio tüm siteyi dağıttığında beklemeniz gerekir.

İçeriği üretim ve geliştirme ortamları arasında farklı olan belirli dosyalar olması çok seyrek değildir. Anahtar örneği, uygulamanın yapılandırma dosyası `Web.config`. Yayımla seçeneği Web uygulama dosyalarını, Web uygulaması dosyalarını, geliştirme ortamındaki sürümle birlikte üretim ortamının özelleştirilmiş yapılandırma dosyalarını geçersiz kılar. Sonraki öğretici bu konuyu daha ayrıntılı bir şekilde ele almaktadır ve bu farklılıkları varsa bir Web uygulamasını dağıtmaya yönelik ipuçları sunar.

## <a name="summary"></a>Özet

Web sitesi dağıtmak, gerekli dosyaları geliştirme ortamından üretim ortamına kopyalamayı içerir. Önceki öğreticide, FileZilla gibi bir FTP istemcisi kullanılarak dosyaların nasıl aktarılacağı gösterildi. Bu öğretici, Visual Studio 'da iki dağıtım aracını inceledi: Web sitesi kopyalama aracı ve Yayımla seçeneği. Web sitesi kopyalama aracı, yerel bilgisayardaki dosyaları ve iki bilgisayar arasında dosya yüklemeyi veya indirmeyi kolaylaştıran, belirtilen bir uzak bilgisayarı içeren bir FTP istemcisine benzer. Yayımla seçeneği, projeyi açık bir şekilde derleyen ve sonra tüm uygulamayı belirtilen hedefe dağıtan daha fazla blönbağlama aracıdır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Web sitesi kopyalama Web sitesi aracıyla kopyalanıyor](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [Nasıl yapılır: Web sitesi kopyalama aracını kullanarak Web sitesi dağıtma](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md) (video)
- [Nasıl yapılır: Web uygulaması projelerini yayımlama](https://msdn.microsoft.com/library/aa983453.aspx)
- [Nasıl yapılır: Web sitelerini yayımlama](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [Visual Studio 'da kurulum ve dağıtım projeleri](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [Önceki](deploying-your-site-using-an-ftp-client-cs.md)
> [İleri](common-configuration-differences-between-development-and-production-cs.md)
