---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: Başlarken | Microsoft Docs
author: Rick-Anderson
description: WebMatrix artık ASP.NET Web sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. Visual Studio veya Visual Studio Code kullanın. Bu kılavuz bir...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: bb863f8605e6f8faca3b285607b63a3e88e83012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547105"
---
# <a name="getting-started"></a>Başlarken

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix artık ASP.NET Web sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) veya [Visual Studio Code](https://code.visualstudio.com/)kullanın.
> 
> 
> Bu kılavuz ve uygulama, ASP.NET Web sayfalarına (sürüm 2 veya üzeri) genel bir bakış ve Razor söz dizimi, dinamik Web siteleri oluşturmaya yönelik basit bir çerçeve sağlar. Ayrıca, sayfa ve site oluşturmaya yönelik bir araç olan WebMatrix 'i de tanıtır.
> 
> **Düzey**: ASP.NET Web Pages 'e yeni.  
> **Kabul edilen yetenekler**: HTML, temel geçişli stil sayfaları (CSS).
> 
> Bu, küme ilk öğreticisinde öğrenirsiniz:
> 
> - Web sayfaları teknolojisinin ne olduğu ve ne için ASP.NET.
> - WebMatrix nedir?
> - Her şeyi nasıl yükleyeceksiniz.
> - WebMatrix kullanarak Web sitesi oluşturma.
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - Microsoft Web Platformu Yükleyicisi.
> - WebMatrix.
> - *. cshtml* sayfaları
>   
> 
> Mike Pope başlangıçta bu öğreticiyi yazdı. Tom FitzMacken, Microsoft WebMatrix 3 için güncelleştirildi.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 3

## <a name="what-should-you-know"></a>Ne bilmeniz gerekir?

Hakkında bilgi sahibi olduğunuzu varsayıyoruz:

- **HTML**. Ayrıntılı uzmanlık gerekli değildir. HTML açıklanmayacağız, ancak karmaşık bir şeyi de kullanmıyoruz. Yararlı olduğunu düşündüğdiğimiz HTML öğreticilerine bağlantılar sağlıyoruz.
- **Geçişli stil sayfaları (CSS)** . HTML ile aynı.
- **Temel veritabanı fikirleri**. Veriler için bir elektronik tablo kullandıysanız ve verileri sıraladıysanız ve filtrelediyseniz bu, genellikle bu öğretici kümesini kabul ettiğimiz uzmanlık düzeyidir.

Ayrıca temel programlama hakkında bilgi edinmek istediğinizi varsayıyoruz. ASP.NET Web sayfaları adlı C#bir programlama dili kullanır. Yalnızca bir ilgilendiğiniz bir arka plana sahip olmanız gerekmez. Bir Web sayfasında daha önce hiç JavaScript yazdıysanız, çok sayıda arka plana sahip olursunuz.

Programlama hakkında bilginiz varsa, yeni programcılar hızla hızlanırken Bu öğreticinin başlangıçta yavaş taşındığını fark edebilirsiniz. Ancak ilk birkaç öğreticiden yararlandığımız için, açıklanmanız gereken daha az temel programlama olacaktır ve diğer bir deyişle daha hızlı bir klibe göre hareket eder.

## <a name="what-do-you-need"></a>Ne gerekir?

İşte gerekenler:

- Windows 8, Windows 7, Windows Server 2008 veya Windows Server 2012 çalıştıran bir bilgisayar.
- Canlı bir internet bağlantısı.
- Yönetici ayrıcalıkları (yükleme işlemi için gereklidir).

## <a name="what-is-aspnet-web-pages"></a>ASP.NET Web sayfaları nedir?

ASP.NET Web sayfaları, dinamik Web sayfaları oluşturmak için kullanabileceğiniz bir çerçevedir. Basit bir HTML Web sayfası statiktir; içeriği, sayfada bulunan sabit HTML biçimlendirmesine göre belirlenir. ASP.NET Web sayfaları ile oluşturduğunuz gibi dinamik sayfalar, kod kullanarak sayfa içeriğini anında oluşturmanıza olanak sağlar.

Dinamik sayfalar her türlü şeyi yapmanızı sağlar. Bir form kullanarak kullanıcıdan giriş yapmasını isteyebilir ve sonra sayfanın ne şekilde görüneceğini veya görünüşünü değiştirebilirsiniz. Bir kullanıcıdan bilgi alabilir, veritabanını bir veritabanına kaydedebilir ve daha sonra listeleyebilirsiniz. Sitenizden e-posta gönderebilirsiniz. Web üzerinde diğer hizmetlerle (örneğin, bir eşleme hizmeti) etkileşim kurabilir ve bu kaynaklardaki bilgileri tümleştiren sayfalar oluşturabilirsiniz.

## <a name="what-is-webmatrix"></a>WebMatrix nedir?

WebMatrix, bir Web sayfası düzenleyicisini, bir veritabanı yardımcı programını, sayfaları test etmek için bir Web sunucusunu ve Web sitenizi Internet 'Te yayımlamaya yönelik özellikleri tümleştiren bir araçtır. WebMatrix ücretsizdir ve kolayca yüklenebilir ve kolayca kullanılır. (Aynı zamanda yalnızca düz HTML sayfaları için de ve PHP gibi diğer teknolojiler için de kullanılır.)

ASP.NET Web sayfalarıyla çalışmak *için gerçekten WebMatrix kullanmanız gerekmez.* Bir metin düzenleyicisini kullanarak (örneğin, erişiminiz olan bir Web sunucusu kullanarak) sayfalar oluşturabilirsiniz. Ancak WebMatrix, bu öğreticiyi çok kolay hale getiriyor. böylece, bu öğreticiler genelinde WebMatrix kullanacaktır.

## <a name="about-these-tutorials"></a>Bu öğreticiler hakkında

Bu öğretici kümesi, ASP.NET Web sayfalarının nasıl kullanılacağına ilişkin bir giriş niteliğindedir. Bu tanıtım öğreticisi kümesinde 9 öğretici toplamı vardır. Bu, ASP.NET Web sayfalarından acemi olarak gerçek, profesyonel görünümlü Web siteleri oluşturmaya yönelik bir dizi öğretici kümesinin parçasıdır.

Bu ilk öğretici, ASP.NET Web sayfalarıyla çalışma hakkında temel bilgileri göstermeye yönelik olarak yoğunlaşır. İşiniz bittiğinde, bu en son nerede bittiğini ve Web sayfalarını daha ayrıntılı bir şekilde keşfetmenizi sağlayan ek öğretici kümeleriyle çalışabilirsiniz.

Derinlemesine açıklamaları bilerek daha kolay bir şekilde geçtik. Her şeyi gösterdiğimiz zaman, bu öğretici için en kolay anlaşılması gereken yöntemi her zaman seçtik. Sonraki öğretici kümeleri daha ayrıntılı bir şekilde geçer ve daha verimli veya daha esnek yaklaşımlara (Ayrıca daha eğlenceli) sahiptir. Ancak bu öğreticiler öncelikle temel kavramları anlamanıza gerek duyar.

Yeni başlattığınız öğretici kümesi, ASP.NET Web sayfalarının şu özelliklerini içerir:

- Giriş ve yükleme her şeyi alma. (Bu, okuduğunuz öğreticide.)
- ASP.NET Web sayfaları programlamasına ilişkin temel bilgiler.
- Veritabanı oluşturma.
- Kullanıcı giriş formu oluşturma ve işleme.
- Veritabanına veri ekleme, güncelleştirme ve silme.

## <a name="what-will-you-create"></a>Ne oluşturmanız gerekir?

Bu öğretici, ve sonraki bir Web sitesi etrafında, istediğiniz filmleri listeleyebilir. Film girebilir, düzenleyebilir ve listeleyebilir. Bu öğretici kümesinde oluşturacağınız sayfaların birkaç tanesini aşağıda bulabilirsiniz. İlki oluşturacağınız film listesi sayfasını gösterir:

![Bir film listesini gösteren ince bir film uygulaması](getting-started/_static/image1.png)

Sitenize yeni film bilgileri eklemenizi sağlayan sayfa:

![Film Ekle sayfasını gösteren tamamlanmış film uygulaması](getting-started/_static/image2.png)

Sonraki öğretici, bu küme üzerinde derleme yapar ve resim yükleme, kullanıcıların oturum açmasına, e-posta göndererek ve sosyal medya tümleştirmesiyle tümleştirme gibi daha fazla işlevsellik ekler.

## <a name="see-this-app-running-on-azure"></a>Bkz. Azure 'da çalışan bu uygulama

Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz? Aşağıdaki düğmeye tıklayarak uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir. Henüz bir hesabınız yoksa, aşağıdaki seçeneklere sahip olursunuz:

- [Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.
- [MSDN abonesi avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.

## <a name="installing-everything"></a>Her şeyi yükleme

Her şeyi Microsoft 'un Web Platformu Yükleyicisi ' ni kullanarak yükleyebilirsiniz. Aslında, yükleyiciyi yüklersiniz ve ardından başka her şeyi yüklemek için kullanacaksınız.

Web sayfalarını kullanmak için, SP3 yüklü en az Windows XP veya Windows Server 2008 veya sonraki bir sürümü olmalıdır.

ASP.NET Web sitesinin [Web sayfaları sayfasında](../../../index.md) , **yükler**' e tıklayın.

![ASP.NET &quot;&quot; düğmesini gösteren Web sitesi](getting-started/_static/image3.png)

WebMatrix 'i yüklemeden önce lisans koşullarını ve gizlilik bildirimini kabul etmeniz istenir.

![yüklemeyi başlatmak için terimi kabul et](getting-started/_static/image4.png)

Yüklemeyi başlatmak için **Çalıştır** ' a tıklayın. (Yükleyiciyi kaydetmek istiyorsanız **Kaydet** ' e tıklayın ve ardından dosyayı kaydettiğiniz klasörden çalıştırın.)

![](getting-started/_static/image5.png)

Web Platformu Yükleyicisi, WebMatrix yüklenmeye hazırlanmaya yönelik olarak görünür. **Yükle**'ye tıklatın.

![](getting-started/_static/image6.png)

Yükleme işlemi, bilgisayarınıza yüklemek için neler olduğunu ve işlemi başlatır. Tam olarak yüklenmesi gereken seçeneklere bağlı olarak, işlem birkaç dakika ile birkaç dakikaya kadar sürebilir. Lisans koşullarını kabul etmek için **kabul ediyorum** ' u seçin.

## <a name="hello-webmatrix"></a>Merhaba, WebMatrix

İşlem tamamlandığında, yükleme işlemi WebMatrix 'i otomatik olarak başlatabilir. Değilse, Windows 'ta, **Başlat** menüsünde **Microsoft WebMatrix**' i başlatın.

WebMatrix 'i ilk kez başlattığınızda, Microsoft hesabı Microsoft Azure için oturum açma şansı vermiş olursunuz. Oturum açarak, Azure üzerinden 10 Ücretsiz Web uygulaması alacaksınız. Bu ücretsiz web uygulamaları, uygulamalarınızı test etmek için kullanışlı bir yol sağlar. Henüz bir Azure hesabınız yoksa ancak bir MSDN aboneliğiniz varsa, [MSDN abonelik avantajlarınızı etkinleştirebilirsiniz](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604). Aksi takdirde, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

Bu öğreticiye devam etmek için hemen oturum açmanız gerekmez. Şimdi oturum açmanız durumunda daha sonra oturum açma seçeneğiniz de vardır. Bu öğretici serisindeki son [Konu](publishing.md) , Web sitenizin Azure 'a nasıl dağıtılacağını anlatmaktadır; Bu nedenle, bu konuyu tamamlayabilmeniz için oturum açmanız gerekir.

Bu noktada, Microsoft hesabı oturum açın ya da sağ alt köşede **Şimdi değil** ' i seçin.

![Oturum Açma](getting-started/_static/image7.png)

Başlamak için boş bir Web sitesi oluşturacak ve bir sayfa ekleyeceğiz. Bu küme içindeki sonraki bir öğreticide, yerleşik web sitesi şablonlarından biriyle oynayacaksınız.

Başlat penceresinde **Yeni**' ye tıklayın.

![WebMatrix başlangıç ekranı](getting-started/_static/image8.png)

Şablonlar, farklı Web sitesi türleri için önceden oluşturulmuş dosya ve sayfalardır. Varsayılan olarak kullanılabilen tüm şablonları görmek için Şablon Galerisi seçeneğini belirleyin.

![Şablon galerisini seçin](getting-started/_static/image9.png)

**Hızlı başlangıç** penceresinde, **ASP.net** grubundan **boş site** ' yi seçin ve "webpagesfilmlerini" adlı yeni siteyi adlandırın.

![Boş site şablonu seçiliyken WebMatrix hızlı başlangıç penceresi](getting-started/_static/image10.png)

**İleri**'ye tıklayın.

Microsoft hesabı oturum açtıysanız, Azure 'da site oluşturma fırsatı vermiş olursunuz. Sitenizin adına bağlı olarak, **WebPagesMovies.azurewebsites.net** varsayılan adı önerilir; Ancak, ünlem işareti bu adın Microsoft Azure 'da mevcut olmadığını gösterir. Basitlik için, şimdi Web sitesini Azure 'da oluşturmayı atlamak için **Atla** ' yı seçin. Bu serinin ilerleyen kısımlarında, siteyi Azure 'da yayımlayacağız.

![Azure sitesi oluştur](getting-started/_static/image11.png)

WebMatrix, siteyi oluşturur ve açar:

![WebMatrix 'te yeni Webpagesfilmlerini sitesi açık](getting-started/_static/image12.png)

En üstte, hızlı erişim araç çubuğu ve bir şerit vardır. Sol altta, görevler arasında geçiş yaptığınız çalışma alanı seçiciyi görürsünüz (**site**, **dosyalar**, **veritabanları**, **raporlar**). Sağ tarafta, düzenleyicinin ve raporların İçerik bölmesi bulunur. Ayrıca, iletiler için zaman zaman bir bildirim çubuğu görürsünüz.

Bu öğreticilerle ilgili olarak WebMatrix ve özellikleri hakkında daha fazla bilgi edineceksiniz.

## <a name="creating-a-web-page"></a>Web sayfası oluşturma

WebMatrix ve ASP.NET Web sayfalarıyla ilgili bilgi almak için basit bir sayfa oluşturacaksınız.

Çalışma alanı seçicide **dosyalar** çalışma alanını seçin. Bu çalışma alanı dosya ve klasörlerle çalışmanıza olanak sağlar. Sol bölmede sitenizin dosya yapısı gösterilir. Şerit, dosyayla ilgili görevleri gösterecek şekilde değişir.

![WebMatrix 'te dosya çalışma alanı](getting-started/_static/image13.png)

Şeritte, **Yeni** ' nin altındaki oka ve ardından **yeni dosya**' ya tıklayın.

![Yeni bir dosya oluşturmak için Şeritteki &quot;yeni&quot; komutunu kullanma](getting-started/_static/image14.png)

WebMatrix, dosya türlerinin bir listesini görüntüler. **Cshtml**'yi seçin ve **ad** kutusuna "HelloWorld" yazın. CSHTML sayfası bir ASP.NET Web sayfaları sayfasıdır.

![HelloWorld. cshtml adlı yeni bir CSHTML sayfası oluşturuluyor](getting-started/_static/image15.png)

**Tamam**’a tıklayın.

WebMatrix sayfayı oluşturur ve düzenleyicide açar.

![WebMatrix düzenleyicideki yeni HelloWorld sayfası](getting-started/_static/image16.png)

Gördüğünüz gibi, en üstte yer alan bir blok haricinde, sayfada çoğunlukla sıradan HTML biçimlendirmesi bulunur:

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

Bu, kısa süre içinde göreceğiniz gibi kod ekleme içindir.

Sayfanın farklı bölümlerinin öğe adlarının, özniteliklerin ve metinlerin yanı sıra üstteki bloğun de &mdash; farklı renklerde olduğunu unutmayın. Buna *sözdizimi vurgulama*denir ve her şeyin açık kalmasını kolaylaştırır. WebMatrix 'te Web sayfalarıyla çalışmayı kolaylaştıran özelliklerden biridir.

Aşağıdaki örnekte olduğu gibi `<head>` ve `<body>` öğeleri için içerik ekleyin. (İsterseniz, yalnızca aşağıdaki bloğu kopyalayabilir ve var olan sayfanın tamamını bu kodla değiştirebilirsiniz.)

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

Hızlı erişim araç çubuğunda veya **Dosya** menüsünde **Kaydet**' e tıklayın.

![WebMatrix hızlı erişim araç çubuğunda Kaydet düğmesi](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>Sayfayı test etme

**Dosyalar** çalışma alanında *HelloWorld. cshtml* sayfasına sağ tıklayın ve ardından **tarayıcıda Başlat**' a tıklayın.

![WebMatrix şeridinde Çalıştır düğmesini kullanarak bir sayfa çalıştırma](getting-started/_static/image18.png)

WebMatrix, bilgisayarınızdaki sayfaları test etmek için kullanabileceğiniz yerleşik bir Web sunucusu (IIS Express) başlatır. (WebMatrix 'te IIS Express olmadan, test etmeden önce sayfanızı bir Web sunucusuna yayımlamanız gerekir.) Sayfa varsayılan tarayıcınızda görüntülenir.

![tarayıcıda çalışan &quot;Merhaba Dünya&quot; sayfası](getting-started/_static/image19.png)

WebMatrix 'te bir sayfayı test ettiğinizde, tarayıcıdaki URL, *localhost* adının yerel bir sunucuya başvurduğu `http://localhost:33651/HelloWorld.cshtml.` gibi bir şeydir, yani sayfanın kendi bilgisayarınızdaki bir Web sunucusu tarafından hizmet verdiği anlamına gelir. Belirtildiği gibi, WebMatrix bir sayfa başlattığınızda çalışan IIS Express adlı bir Web sunucusu programı içerir.

*Localhost* 'tan sonraki sayı (örneğin, *localhost: 33651*) bilgisayarınızdaki bir *bağlantı noktası numarasını* belirtir. Bu, bu Web sitesi için IIS Express kullandığı "kanal" sayısıdır. Bağlantı noktası numarası, sitenizi oluştururken 1024 ile 65536 arasındaki aralıktan rastgele seçilir ve oluşturduğunuz her site için farklıdır. (Kendi sitenizi test ettiğinizde, bağlantı noktası numarası neredeyse tamamen 33561 ' den farklı bir sayı olacaktır.) Her Web sitesi için farklı bir bağlantı noktası kullanarak IIS Express, Sitelerim 'in konuştuğu bir şekilde devam edebilir.

Daha sonra, sitenizi ortak bir Web sunucusuna yayımladığınızda artık URL 'de *localhost* görmezsiniz. Bu noktada, `http://myhostingsite/mywebsite/HelloWorld.cshtml` gibi daha tipik bir URL veya sayfanın ne olduğunu görürsünüz. Bu öğretici serisinde daha sonra bir site yayımlama hakkında daha fazla bilgi edineceksiniz.

## <a name="adding-some-server-side-code"></a>Sunucu tarafı kod ekleme

Tarayıcıyı kapatın ve WebMatrix 'teki sayfaya geri dönün.

Kod bloğuna aşağıdaki kod gibi görünmesi için bir satır ekleyin:

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

Bu, çok sayıda Razor kodudur. Bu, geçerli tarih ve saati aldığından ve bu değeri `currentDateTime`adlı bir *değişkene* yerleştirdiğinden büyük olasılıkla temizleyebilir. Sonraki öğreticide Razor söz dizimi hakkında daha fazla bilgi edineceksiniz.

Sayfanın gövdesinde, `<p>Hello World!</p>` öğesinden sonra aşağıdakileri ekleyin:

[!code-html[Main](getting-started/samples/sample4.html)]

Bu kod, üstteki `currentDateTime` değişkenine yerleştirdiğiniz değeri alır ve sayfanın biçimlendirmesine ekler. `@` karakteri sayfadaki ASP.NET Web sayfaları kodunu işaretler.

Sayfayı yeniden çalıştırın (WebMatrix, sayfayı çalıştırmadan önce değişiklikleri sizin için kaydeder). Bu kez, sayfada tarih ve saati görürsünüz.

![dinamik olarak üretilen zaman görüntüsü ile tarayıcıda çalışan &quot;Merhaba Dünya&quot; sayfası](getting-started/_static/image20.png)

Birkaç dakika bekleyin ve ardından tarayıcıda sayfayı yenileyin. Tarih ve saat görünümü güncellenir.

Tarayıcıda, sayfa kaynağına bakın. Aşağıdaki biçimlendirme gibi görünür:

[!code-html[Main](getting-started/samples/sample5.html)]

Üstteki `@{ }` bloğunun orada olmadığını unutmayın. Ayrıca, tarih ve saat görüntülemenin, *. cshtml* sayfasında sahip olduğunuz gibi `@currentDateTime` değil, gerçek bir karakter dizesi (`1/18/2012 2:49:50 PM` veya herhangi bir) gösterdiğine dikkat edin. Burada ne olur, sayfayı çalıştırdığınızda, ASP.NET `@`işaretlenen tüm kodları (Bu durumda çok küçük) işledi. Kod çıktı üretir ve bu çıktı sayfaya eklenmiştir.

## <a name="this-is-what-aspnet-web-pages-are-about"></a>Bu, ASP.NET Web sayfaları hakkında

ASP.NET Web sayfalarının dinamik Web içeriği ürettiğini okuduğunuzda, bu fikir burada gördüğünüz şeydir. Yeni oluşturduğunuz sayfa, daha önce gördüğünüz HTML işaretlemesini içerir. Ayrıca, her türlü görevi gerçekleştirebilen kodu da içerebilir. Bu örnekte, geçerli tarih ve saati alma, önemsiz bir görevdir. Gördüğünüz gibi, sayfada çıktı üretmek için kodu bir HTML ile birlikte bırakabilirsiniz. Birisi tarayıcıda bir *. cshtml* sayfası istediğinde, ASP.NET sayfayı Web sunucusunda hala devam ederken işler. ASP.NET kodun çıkışını (varsa) HTML olarak sayfaya ekler. Kod işleme tamamlandığında, ASP.NET ortaya çıkan sayfayı tarayıcıya gönderir. Şimdiye kadar her bir tarayıcı HTML 'dir. Diyagram aşağıda verilmiştir:

![ASP.NET 'in HTML 'i dinamik olarak nasıl üretmesinin kavramsal akışı](getting-started/_static/image21.png)

Fikir basittir, ancak kodun gerçekleştirebileceği çok sayıda ilginç görev vardır ve sayfaya dinamik olarak HTML içeriği ekleyebileceğiniz birçok ilginç yol vardır. Ve ASP.NET *. cshtml* sayfaları, HERHANGI bir HTML sayfası gibi, tarayıcıda çalışan kodu da Içerebilir (JavaScript ve jQuery kodu). Bu öğreticide ve sonraki olanlarda bu öğelerin tümünü keşfedeceksiniz.

## <a name="coming-up-next"></a>Sonraki adımda

Bu serinin bir sonraki öğreticide, ASP.NET Web sayfaları programlamayı biraz daha bulabilirsiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

[Sıfırdan bir ASP.NET Web sitesi oluşturun](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch). Bu, özellikle WebMatrix (ASP.NET Web sayfaları değil) kullanımı hakkında bir öğreticidir. Bu öğretici kümesinin kapsamayacağız bazı WebMatrix özellikleri hakkında biraz daha ayrıntıya gider.

> [!div class="step-by-step"]
> [Next](intro-to-web-pages-programming.md)
