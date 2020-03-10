---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 geliştirmeleri | Microsoft Docs
author: microsoft
description: Visual Studio 2005, Web projelerine yönelik uzun bir iyileştirmeler ve geliştirmeler listesi sunan Web uygulaması geliştiricileri sağlar.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575581"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005’teki Geliştirmeler

[Microsoft](https://github.com/microsoft) tarafından

> Visual Studio 2005, Web projelerine yönelik uzun bir iyileştirmeler ve geliştirmeler listesi sunan Web uygulaması geliştiricileri sağlar.

Visual Studio 2005, Web projelerine yönelik uzun bir iyileştirmeler ve geliştirmeler listesi sunan Web uygulaması geliştiricileri sağlar. Visual Studio .NET 2002 ve 2003 gibi güçlü bir deyişle, web projelerinin işlendiği şekilde birçok şikayet vardır. Visual Studio 2005, bu şikayeti ele almak için önemli sayıda yeni özellik ekler. Visual Studio .NET 2003 'in Web uygulamalarının derlemesini nasıl ele aldığı konusunda tercih eden kullanıcılar için bkz. [Web uygulaması projeleri](https://go.microsoft.com/fwlink/?LinkId=57870).

Bu modülde, Web projesi oluşturma, yönetim ve geliştirme konusundaki geliştirmeleri de kapsar. Daha sonraki bir modülde, Web projeleri oluşturma ve bunları dağıtma geliştirmeleri hakkında daha fazla geliştirmeler de kapsar.

## <a name="frontpage-server-extensions"></a>FrontPage Sunucu uzantıları

Web projeleri oluşturmak veya oluşturmak için, kutuda Visual Studio .NET 2002 ve 2003 gerekli FrontPage Server uzantıları. Geliştiricilerin iki farklı erişim modu (FrontPage Sunucu uzantıları veya dosya erişim modu) arasında bir seçeneği vardır, her ikisi de IIS 'de uygulama kökünü ayarlama gibi görevleri gerçekleştirmek için kullanılan FrontPage Sunucu uzantıları, vb.

Visual Studio 2005, yerel projeler için FrontPage sunucu uzantılarında güvenini kaldırır. Visual Studio 2005 artık FrontPage Sunucu uzantılarını kullanmak yerine IIS metatabanına doğrudan erişir. Visual Studio 2005, FrontPage Sunucu uzantıları gerekmeden uzak proje erişimine izin veren FTP desteğini de ekler.

Projelerinde FrontPage Server Extensions kullanmak isteyen geliştiriciler için, bu seçenek hala kullanılabilir. Ancak, ASP.NET geliştirici topluluğunun güçlü geri bildirimlerine bağlı olarak, bir gereksinim değildir.

> [!NOTE]
> Uzak proje oluşturma, açma, vb. için FrontPage Sunucu uzantıları yine de gereklidir.

## <a name="aspnet-development-server"></a>ASP.NET Geliştirme Sunucusu

Visual Studio 2005, ASP.NET Development Server adlı yeni bir Web sunucusuyla birlikte gelir. (Bu Web sunucusu daha önce Cassini olarak biliniyordu.)

ASP.NET geliştirme sunucusunun çeşitli avantajları vardır.

- Yönetici olmayanlar Web sunucusunda geliştirme ve hata ayıklama işlemlerini artık mümkündür.
- ASP.NET Development Server, sanal dizinleri, esnek proje konumlarına izin veren dosya sistemindeki herhangi bir konuma dinamik olarak eşler.
- Daha önce IIS kullanan Windows XP Professional kullanıcıları, IIS 'de varsayılan Web sitelerinin dosya veya klasör yapısını etkilemeyen yeni Web uygulamaları oluşturabiliyor.

ASP.NET Development Server avantajlarından yararlanmak için özel yapılandırma gerekmez. Dosya sisteminde barındırılan bir Web projesi hata ayıklaması veya tarandığında, Visual Studio 2005, isteğe hizmet vermek için rastgele bir bağlantı noktasında ASP.NET Development Server örneğini otomatik olarak başlatır.

Daha sonra bu modülün ASP.NET geliştirme sunucusunda daha fazla bilgi alınacaktır.

## <a name="improved-file-management"></a>Geliştirilmiş dosya yönetimi

Visual Studio 2002 ve 2003 ' de, bir proje dosyası (örneğin C#, vb.net ve. csproj için. vbproj) Web uygulamasındaki tüm dosyalarda depolanan bilgileri saklı. Çözüm Gezgini görüntüsü, proje dosyasındaki dosya bilgilerine bağlıdır. Bu nedenle Çözüm Gezgini, genellikle dış düzenleyicilerin kullanıldığı durumlarda yanlış bilgiler görüntüler. Visual Studio 2002 ve 2003 çoğu zaman dosya değişikliklerinin üzerine yazar veya dosyaların en son sürümünü görüntülemez.

Visual Studio 2005, proje dosyası ile uzakta. Bunun yerine, dosya ve klasör bilgilerini doğrudan diskten okur ve bu, projenizdeki dosyaların doğru bir görüntüsüne neden olur. Visual Studio 2002 ve 2003 ' deki başvurular klasörü Web uygulamanızdaki gerçek bir klasörü temsil etmediği için, Visual Studio 2005 aynı zamanda başvurular klasörünü Çözüm Gezgini de kaldırır. Visual Studio 2005 ' de projenizin başvurularına erişmek için, projenin özellik sayfalarını kullanmanız gerekir.

## <a name="creating-web-projects"></a>Web projeleri oluşturma

Web geliştiricilerinin, Visual Studio 2005 ' de proje oluşturmaya yönelik birçok yeni seçenek bulunur. Web siteleri artık dosya sisteminde herhangi bir yerde oluşturulabilir ve sonra, yeni ASP.NET geliştirme sunucusu kullanılarak ayıklanamaz veya gözatılabilir. Geliştiriciler, FTP kullanarak yeni Web siteleri de oluşturabilir.

Visual Studio 2005 ' de Web projeleri oluşturmaya yönelik bir video kılavuzunu görüntülemek için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image1.png)

[Tam ekran videosunu açın](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>Dosya sistemi projeleri

Video kılavuzunuzda gördüğünüz gibi, dosya sisteminde yerel makinede ya da bir dosya paylaşımından uzak bir konumda Web siteleri oluşturmayı tercih edebilirsiniz. Dosya sisteminde oluşturulan Web sitelerine Gözatılıyor ve ASP.NET Development Server kullanılarak hata ayıklıyor.

> [!NOTE]
> ASP.NET geliştirme sunucusu müşterilerin bazı karışıklığına neden olabilir. IISS dizin yapısındaki (ör. c:/ınetpub/Wwwroot) dosya sisteminde bir Web projesi oluşturulduysa, Visual Studio 2005 içinden başlatıldığında Web sitesine hala ASP.NET geliştirme sunucusu üzerinden gözatılabilir. Bu nedenle, herhangi bir IIS yapılandırması (Yani kimlik doğrulama yöntemleri) uygulanamaz.

Varsayılan Web projesi Ayrıca, yalnızca bir default. aspx sayfası, default.cs dosyası ve bir App/_Data klasörü içeren ek yükün çoğunu da kaldırır. Web. config ve özel klasörler (örn. uygulama/_code) gerektiği gibi eklenir. Web projeniz yalnızca ihtiyacınız olan dosya ve klasörleri içerir.

### <a name="http-projects"></a>HTTP projeleri

HTTP projeleri, yerel bir IIS Web sitesinde veya uzak Web sitesinde oluşturulmuş projeler olabilir. Varsayılan proje konumu `http://localhost`. Tarayıcı düğmesine tıklarsanız, iki HTTP seçeneği vardır: yerel IIS ve uzak site. Bu iki seçenek içindeki temel fark, Web sitesi bilgilerinin konum Seç iletişim kutusunda ve dosyaların Web sunucusuna nasıl kopyalandığı yöntemi olan yöntemdir.

Yerel IIS seçeneği, yerel makinedeki metatabanından site bilgilerini okur ve dosyalar dosya sistemi kullanılarak kopyalanır. Uzak site seçeneği, FrontPage Sunucu uzantılarını ve site bilgilerini ve dosyaları, HTTP ve FrontPage Sunucu uzantıları RPC çağrıları kullanılarak kopyalanır.

> [!NOTE]
> Vs # # #/_tmp. htm dosyası ve Get/_aspx/_ver. aspx artık sürüm bilgilerini belirlemede kullanılmıyor.

Varsayılan HTTP seçeneği yerel IIS 'dir. Bu seçenek, hangi sitelerin kullanılabilir olduğunu ve içeriğin oluşturulacağı konumu öğrenmek için IIS metatabanını okur. Ağaç görünümünde seçerek, farklı bir klasör veya sanal dizin seçebilirsiniz. Ayrıca, yeni bir sanal dizin oluşturabilir, klasörleri uygulamalar olarak işaretleyebilir ve var olan sanal dizinleri bu iletişim kutusundan silebilirsiniz.

![Konum Seç Iletişim kutusu](improvements-in-visual-studio-2005/_static/image1.gif)

**Şekil 1**: konum Seç iletişim kutusu

Visual Studio 'nun önceki sürümlerinden farklı olarak, **Use güvenli yuva katmanı** onay kutusunu IŞARETLERSENIZ ve SSL sertifikası GÖZATTıĞıNıZ URL ile eşleşmiyorsa, devam etmek isteyip istemediğinizi soran bir güvenlik uyarısı iletişim kutusu görüntülenir. Visual Studio .NET 2003 kullanarak, sertifika eşleşen bir sertifika değilse, projenin oluşturulması başarısız olur.

![SSL sertifikasıyla Ilgili güvenlik uyarısı](improvements-in-visual-studio-2005/_static/image2.gif)

**Şekil 2**: SSL sertifikasıyla Ilgili güvenlik uyarısı

### <a name="note-on-host-headers"></a>Konak başlıklarında göz önünde

Belirli bir IP 'ye bağlı bir sitede Web uygulaması oluşturuyorsanız, bir ana bilgisayar üstbilgisinin yapılandırıldığından emin olmanız gerekir. Aksi halde, Visual Studio `http://localhost`sitesini oluşturur, ancak site gözatılırken veya IDE içinden hata ayıklaması yapıldığında IP adresi doğru şekilde çözümlenmeyecektir.

Uzak site seçeneğini belirlerseniz, iletişim kutusu, yeni Web sitesinin hedef URL 'sini girmenize izin verecek şekilde değişir. Bu URL, FrontPage sunucu uzantılarının etkin olduğu bir sunucuda olmalıdır. FrontPage Sunucu uzantılarını kullanarak yerel Web sunucunuz ile çalışmak istiyorsanız, uzak site seçeneğini kullanabilir ve yerel bir URL belirtebilirsiniz.

![Uzak sunucuda bir Web sitesi oluşturma](improvements-in-visual-studio-2005/_static/image1.jpg)

**Şekil 3**: uzak sunucuda bir Web sitesi oluşturma

SSL aracılığıyla uzak bir sitede bir uygulama oluştururken, SSL sertifikası eşleşmezse, onay iletişim kutusu yerel IIS seçeneği kullanılırken görüntülenenden biraz farklıdır.

![Uzak site güvenlik uyarısı](improvements-in-visual-studio-2005/_static/image3.gif)

**Şekil 4**: uzak site güvenlik uyarısı

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005, FTP aracılığıyla Web siteleri oluşturma seçeneğini sunar. Bu seçeneği kullandığınızda, IDE dosyaları kullanıcılar geçici klasöründe yerel olarak oluşturur ve sonra FTP 'yi kullanarak dosyaları FTP konumuna taşır.

> [!NOTE]
> Geçici klasör konumu c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;uygulama adı&gt;

FTP seçeneğini kullanırken konum Seç iletişim kutusu görüntülenir. Gerekli FTP bağlantı bilgilerini aşağıda gösterildiği gibi bu iletişim kutusuna girersiniz.

![FTP için konum seç Iletişim kutusu](improvements-in-visual-studio-2005/_static/image2.jpg)

**Şekil 5**: FTP Için konum Seç iletişim kutusu

## <a name="lab-setup-ftp-site-and-create-a-project"></a>Laboratuvar: FTP sitesini ayarlama ve proje oluşturma

Aşağıdaki adımlar FTP sitesini bir kullanıcının FTP aracılığıyla yalnızca yükleyebilecekleri bir konuma sahip olacak şekilde yapılandırır.

### <a name="install-the-ftp-service"></a>FTP hizmetini yükler

1. Program Ekle Kaldır ' ı açın, Windows Bileşenlerini Ekle/Kaldır ' ı seçin
2. Internet Information Services (Windows 2003 üzerinde uygulama sunucusu) öğesini seçin ve **Ayrıntılar**' a tıklayın.
3. **Dosya Aktarım Protokolü (FTP) hizmetini** denetleyin ve **Tamam 'a**tıklayın.
4. FTP hizmetini yüklemek için **İleri** 'ye tıklayın.

### <a name="create-a-new-folder-for-content"></a>Içerik için yeni bir klasör oluştur

1. Windows Gezgini 'nde, c:/ınetpub/Wwwroot içinde **kullanıcı1** adlı yeni bir klasör oluşturun.

#### <a name="configure-folders-and-permissions-on-folders"></a>Klasörler üzerinde klasörleri ve izinleri yapılandırın.

1. Yönetim araçlarından Internet Information Services ek bileşenini açın. Artık bilgisayar adı düğümünün altında bir FTP siteleri klasörünüze sahip olursunuz.
2. **FTP siteleri**' ni genişletin.
3. **Varsayılan FTP sitesini**sağ tıklatın, **Yeni**' yi ve ardından **sanal dizin**' i seçin ve ardından **İleri**' ye tıklayın.
4. Sanal dizin adı için **kullanıcı1** girin ve **İleri**' ye tıklayın.
5. Yol için **c:/ınetpub/Wwwroot/Kullanıcı1** yazın ve **İleri**' ye tıklayın.
6. **İleri** ' ye tıklayın ve Sihirbazı tamamladıktan sonra **son** ' a tıklayın.
7. Varsayılan FTP sitesi altında **kullanıcı1** sanal dizinine sağ tıklayın ve **Özellikler**' i seçin.
8. **Yazma** onay kutusunu Işaretleyin ve **Tamam** ' a tıklayarak iletişim kutusunu kapatın.
9. **Varsayılan FTP sitesi** ' ne sağ tıklayın ve **Özellikler**' i seçin.
10. **Güvenlik hesapları** sekmesinde, **anonim bağlantılara izin ver**onay işaretini kaldırın.
11. Devam etmek isteyip istemediğinizi soran iletişim kutusunda **Evet** ' e tıklayın.
12. İletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.
13. **Web siteleri** düğümünün altında **varsayılan Web sitesi** ' ni genişletin.
14. **Kullanıcı1** dizinine sağ tıklayıp **Özellikler** ' i seçin
15. **Uygulama ayarları** bölümünde, klasörü bir uygulama olarak Işaretlemek için **Oluştur** ' a tıklayın.
16. İletişim kutusunu kapatmak için **Tamam** ' ı tıklatın.
17. Internet Information Services ek bileşenini kapatın.

### <a name="create-web-project"></a>Web projesi oluştur

1. Visual Studio 2005 ' i açın.
2. **Dosya** menüsünde **Yeni Web sitesi**' ni seçin.
3. **Konum** açılır listesinde **FTP**' yi seçin.
4. **Gözat**'ı tıklatın.
5. **Sunucu** metin kutusuna **localhost** girin.
6. Dizin metin kutusuna **kullanıcı1** yazın.
7. **Aç**'a tıklayın. FTP konumu yeni Web sitesi iletişim kutusuna girilir.
8. **Tamam**’a tıklayın.
9. FTP oturum açma iletişim kutusunda **anonim oturum** açma seçeneğinin işaretini kaldırın, kimlik bilgilerinizi girin ve **Tamam**' a tıklayın.
10. Projenin URL 'SI nedir? (Projenin URL 'SI Çözüm Gezgini içinde görüntülenir.)
11. **Derleme** menüsünden **Web sitesi oluştur** veya **çözüm oluştur**' u seçin.
12. Çözüm Gezgini ' de default. aspx ' e sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin.
13. Web sitesi URL 'SI gerekli iletişim kutusunda URL için `http://localhost/user1` girin ve **Tamam**' a tıklayın.

> [!NOTE]
> Türü/_Default yükleyemediğini belirten bir hata alırsanız, ASP.NET 2,0 ' i daha önceki bir sürümü değil web sitenizde çalıştırdığınızdan emin olun. Bunu, Internet Information Services ASP.NET sekmesinden yapabilirsiniz.

## <a name="opening-web-projects"></a>Web projelerini açma

Web projelerini açmak, proje oluşturmaya benzer. Aşağıdaki bölümlerde, IDE içinde çalışırken bir göz atın. Ayrıca, HTTP ve FTP kullanarak Web projeleriyle çalışmayı da ele alır.

Bir Web projesi açmak için Dosya menüsünden Web sitesi aç ' ı seçin. Daha önce ele alınan aynı konum Seç iletişim kutusuyla istenir ve kullanabileceğiniz dört seçenek vardır: dosya sistemi, yerel IIS, FTP ve uzak site.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>Dosya sistemi

Bu modülde daha önce belirtildiği gibi, Visual Studio artık bir proje dosyası kullanmaz. Bu nedenle, dosya sisteminden bir Web sitesi açmayı seçerseniz, seçtiğiniz klasör Visual Studio 'da başlangıçta bir Web projesi olarak oluşturulmasa bile, istediğiniz herhangi bir klasörü seçme seçeneğiniz vardır. Örneğin, Belgelerim klasörünü bir Web sitesi olarak açmayı seçebilirsiniz ve Visual Studio bu dosyayı açıp açmak ve dosyalarınızı aşağıda gösterildiği gibi görüntülemektir.

![Web sitesi olarak açılan Belgelerim](improvements-in-visual-studio-2005/_static/image3.jpg)

**Şekil 6**: *Belgelerim* bir Web sitesi olarak açıldı

Visual Studio, gerekli olduğunda yalnızca ek dosya ve klasörler oluşturduğundan, açtığınız konuma ek dosya veya klasör eklenmez. Bu mimarinin yan etkisi, Web sitelerini dosya sistemine iç içe geçirmeyi engellemektedir. Örneğin, aşağıdaki dizin yapısını göz önünde bulundurun.

C:/MyWebSite konumundaki Web projesi

C:/MyWebSite/Iç Içe geçmiş bir Web projesi

Web sitesini c:/MyWebSite adresinde açtığınızda, Iç Içe geçmiş klasör o uygulamanın alt klasörü olarak görünür.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

HTTP üzerinden Web siteleri açılırken, ayarlar IIS metatabanından (yerel IIS) veya FrontPage Sunucu Uzantıları (uzak site) kullanılarak okunabilir. İç içe geçmiş Web uygulamaları varsa bunlar, bunları uygulama olarak tanımlayan bir simgeyle birlikte görüntülenir. FrontPage 'de Web uygulamalarıyla çalışmaya alışdıysanız, Visual Studio 2005 davranışı benzerdir.

Visual Studio, IDE içinde o anda açılan uygulamanın altında iç içe yerleştirilmiş uygulamalar için bir simge görüntülemesine rağmen, içeriğini görmek için bunları genişletmenizi sağlar. Ancak, bunları açmak için çift tıklayabilirsiniz. Bunu yaptığınızda, Web uygulamasını açmak isteyip istemediğinizi soran bir iletişim kutusu görüntülenir (ve şu anda açık olan çözümü değiştirmeniz) veya Web uygulamasını geçerli çözümünüze eklemeniz istenir.

![İç içe yerleştirilmiş bir uygulama simgesine çift tıklamak size bu iletişim kutusunu sunar](improvements-in-visual-studio-2005/_static/image4.jpg)

**Şekil 7**: iç içe geçmiş bir uygulama simgesine çift tıklamak size bu iletişim kutusunu sunar

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP Sitesi

FTP aracılığıyla bir site açtığınızda dosyaların tümü geçici klasörünüze yerel olarak kopyalanır. Yerel depolama konumunun tam yolu, projenin Özellikler bölmesinde görüntülenir ve aşağıdaki biçim kullanılarak oluşturulur.

C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;uygulama adı&gt;

FTP kullanırken, Visual Studio 'nun, aşağıda gösterildiği gibi gözatabilmeniz için projenizin temel URL 'sini belirtmesi gerekir. Temel URL belirtmezseniz, Visual Studio sizden Web sitesindeki bir sayfaya ilk kez gözatmaya çalıştığınızda sizi sorar.

![FTP siteleri için temel URL belirtme](improvements-in-visual-studio-2005/_static/image5.jpg)

**Şekil 8**: FTP siteleri IÇIN temel URL belirtme

## <a name="improvements-in-compilation"></a>Derlemedeki geliştirmeler

Visual Studio 2005 ' de Web uygulamalarıyla çalışma, önceki sürümlere göre önemli ölçüde hızlıdır. Bunun nedeni, derleme mimarisinde değişikliklere küçük bir bölüm değildir.

Visual Studio 2002 ve 2003 ' de Web uygulamaları,/bin klasöründe bulunan bir birincil derlemede derlendi. Visual Studio 2005 ' de bir uygulama/_Code klasörü eklenmiştir. Sınıflar ve diğer kullanıcı arabirimi olmayan kodlar App/_Code klasörüne eklenir. Visual Studio projeyi oluşturduğunda, uygulama/_Code klasöründeki tüm dosyalar tek bir App/_Code. dll dosyasında derlenir. Bu değişikliğin sonucu, sonraki derlemelerin önceki sürümlerden çok daha hızlı olmasını sağlar.

> [!NOTE]
> MSBuild komut satırı yardımcı programı, ASP.NET Web uygulamaları oluşturmak için de kullanılabilir. Bu araç modül 9 ' da ele alınacaktır.

Başka bir derleme geliştirmesi, derleme menüsündeki yeni derleme sayfası seçeneğidir. Bu özellik, bir geliştiricinin değişiklikler daha hızlı derlenebilecek şekilde yalnızca geçerli sayfayı (Elbette ve bağımlılıklarla birlikte) yeniden derlemesine olanak tanır. C# , IntelliSense 'i güncelleştirme amaçları için arka plan derlemesi sunmadığından, IntelliSense 'in tek bir sayfayı yeniden oluşturarak IntelliSense 'in hızla güncelleştirilmesini sağlayacak olduğundan bu özellikten özellikle bu özellikten faydalanacaktır.

Bir projenin yapı özellikleri, başlangıç sayfası yürütülmeden önce oluşan yapı türünü yapılandırmanıza olanak tanır. Geliştiriciler, kod değişikliklerinden sonra Visual Studio 'Nun uygulamalarda hata ayıklamayı daha hızlı başlatabilmesi için yalnızca geçerli sayfayı derlemeyi seçebilir.

![Derleme sayfası başlatma eylemi](improvements-in-visual-studio-2005/_static/image6.jpg)

**Şekil 9**: derleme sayfası başlatma eylemi

Visual Studio ve ASP.NET mimarisine yönelik harika bir geliştirme, Düzenle ve devam et alanıdır. Visual Studio 2005 ' de geliştiriciler bir projede hata ayıklamaya başlayabilir ve hata ayıklayıcıyı kullanımdan çıkarmadan proje üzerinde kod değişiklikleri yapabilir. Aslında, bir projede hata ayıklamaya başlayabilir, yeni bir sınıf ekleyebilir, bu sınıfa kod ekleyebilir, bu sınıfın yeni bir örneğini oluşturan ve sınıfın bir yöntemini yürütebilmeniz ve hata ayıklayıcıyı kullanımdan çıkarmadan, sayfanıza kod ekleyebilirsiniz. Yeni kodun yürütülmesi, tarayıcıyı yenilemek kadar kolaydır!

Visual Studio 2005 ' de Düzenle ve devam et özelliğine yönelik bir video kılavuzu görmek için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image2.png)

[Tam ekran videosunu açın](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2,0 ve Visual Studio 2005 ' deki güçlü düzenleme ve devam etme işlevleri, ASP.NET uygulamalarının mimari değişikliği nedeniyle yapılır. ASP.NET 1. x içinde, Visual Studio 2002/2003 ' de oluşturulan uygulamalar,/bin klasöründe depolanan bir birincil derlemede derlendi. Uygulamanın tüm sınıfları, sayfaları, vb., bu DLL 'ye derlendi. Sonra, ASP.NET çalışma zamanında tüm denetimleri, biçimlendirmeyi ve ASP.NET kodunu sayfalar içinde derleyip bu DLL 'Leri ASP.NET geçici klasörüne kopyalar.

Visual Studio 2005 ' de ASP.NET 2,0 kullanarak, yukarıdaki iki derleme modeli ana hattı (Visual Studio için bir diğeri de çalışma zamanında ASP.NET için), tek bir ortak derleme modelinde birleştirilmiştir. Diğer bir deyişle, çalışma zamanı yerine geliştirme aşamasında tüm derleme sorunlarının artık yakalandığını gösterir. Ayrıca, Kullanıcı denetimleri ve ana sayfalar gibi özellikler için tasarımcı ve IntelliSense desteğine de olanak tanır.

Kullanıcı denetimleri için tasarımcı desteğinin videosunu görmek için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image3.png)

[Tam ekran videosunu açın](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> Bir kullanıcı denetimi bir sayfadan kaldırıldığında, @Register yönergesi biçimlendirmede kalır ve Kullanıcı denetimi Web sitesinden silinirse ayrıştırıcı hatalarından kaçınmak için el ile kaldırılmalıdır.

Visual Studio derleme modelinde başka bir geliştirme de Web sitesi yayımla özelliğidir. Yayımla özelliği Web sitesini önceden derlediğinden, geliştiriciler isteğe bağlı bir şeyi derlemek zorunda kalmadan eklenen performansın tadını çıkarabilirsiniz. Ayrıca, uygulama/_Code klasöründeki tüm kaynak kodlarını bir DLL 'ye önceden derler, böylece kaynak kodu dağıtılmalıdır.

![Web sitesi yayımla Iletişim kutusu](improvements-in-visual-studio-2005/_static/image7.jpg)

**Şekil 10**: Web sitesi Yayımla iletişim kutusu

> [!NOTE]
> ASPNET/_compile. exe yardımcı programı, bir ASP.NET Web uygulamasını önceden derlemek için de kullanılabilir. Bu araç modül 9 ' da ele alınacaktır.

Bir Web sitesi yayımladığınızda, önceden derlenmiş dosyalar aşağıda gösterildiği gibi Temporary ASP.NET Files klasöründe depolanır. *. Derlenmiş* bir dosya uzantısına sahip dosyalar, belirli dll 'lerin BAĞıMLıLıKLARıNı tanımlayan xml dosyalarıdır. Tüm WebForm veya Kullanıcı denetimleri, *App/_Web/_* Ile başlayan rastgele dll 'ler halinde derlenir.

*Bu önceden derlenmiş sitenin güncelleştirilebilir olmasına Izin ver* onay kutusunu işaretli bırakırsanız, WebForms ve Kullanıcı denetimlerinizin içindeki işaretleme, dağıtımdan sonra değişiklik yapmanıza izin veren bir dll 'ye önceden derlenmeyecektir. Dağıtılan içerikte değişikliklere izin verilmediğinden biçimlendirmeyi kilitlemeyi tercih ediyorsanız, bu kutunun işaretini kaldırın.

*Sabit adlandırma ve tek sayfa bütünleştirilmiş kodlarını kullan* onay kutusu, her sayfanın sabit adlı bir derlemeye derlenmesi için Batch derlemesini devre dışı bırakmanıza olanak tanır. Bu kutuyu işaretsiz bırakmak, Batch derleme özelliğinden yararlanmanızı sağlar.

*Önceden derlenmiş derlemelerde tanımlayıcı adlandırmayı etkinleştir* onay kutusu, önceden derlenmiş derlemelerinizi güçlü bir şekilde adlandıralmanıza olanak sağlar.

> [!NOTE]
> ASP.NET 1. x içinde, tanımlayıcı adlı derlemelerin genel derleme önbelleği 'ne (GAC) yüklenmesi gerekiyordu. ASP.NET 2,0 ' de, kesin adlı derlemeleri GAC içine yüklemenize gerek yoktur.

![Önceden derlenmiş ASP.NET uygulamaları](improvements-in-visual-studio-2005/_static/image8.jpg)

**Şekil 11**: ASP.NET uygulamaları önceden derlenmiş dosyalar

> [!NOTE]
> Yukarıdaki uygulamada, Web. config dosyası yoktu. Varsa, Web sitesi yayımla işleminden sonra *PreCompiledApp. config* olarak adlandırılırlar.

## <a name="improvements-in-deployment"></a>Dağıtımdaki geliştirmeler

Visual Studio 2002 ve 2003 ' de olduğu gibi, Visual Studio 2005 de bir proje kopyalama özelliği sunar. Ancak özellik Visual Studio 2005 ' de geliştirilmiştir ve artık Web sitesi kopyalama olarak adlandırılmaktadır.

Web sitesini Kopyala iletişim kutusu, bir sol çerçeveye ve doğru çerçeveye bölünür. Sol çerçeveye kaynak web sitesi denir ve doğru çerçeveye uzak Web sitesi denir. Bazı geliştiricilere karıştırabilecek bir şey, doğru çerçevede görüntülenen Sitenin uzak bir site olması gerekmez. Yerel dosya sisteminde veya IIS 'nin yerel örneğindeki bir site olabilir. Ayrıca, iletişim kutusu uzak *Web sitesinden kaynak Web sitesine yayımlamanıza* izin verdiğinden, sol çerçevede görüntülenecek site kaynak web sitesi değildir.

Bir projeyi uzak bir Web sitesine kopyalıyorsanız, bu sitede FrontPage sunucu uzantılarının yüklü olması gerekir. Aksi takdirde, FTP kullanarak bağlanmanız gerekir. Öte yandan, bir projeyi yerel IIS örneğine kopyalıyorsanız, FrontPage Sunucu uzantıları gerekli değildir.

> [!NOTE]
> Yerel IIS örneğinde yeni bir Web sitesi oluşturmayı denerseniz ve FrontPage 2002 Sunucu uzantıları yüklüyse, Web siteleri oluşturmanın bir SharePoint sunucusunda desteklenmediğini belirten bir hata iletisi alırsınız. Bu durumda FrontPage 2000 sunucu uzantılarını yükleme veya FrontPage Sunucu uzantılarını kaldırma seçeneğiniz vardır.

Web sitesini Kopyala özelliği hakkında bir video kılavuzu için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image4.png)

[Tam ekran videosunu açın](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>Hata ayıklama geliştirmeleri

Visual Studio 2005 ' de hata ayıklamada dört temel geliştirmeler vardır.

- Yönetici olmayan olarak yerel olarak hata ayıklama, kutudan çıkar.
- Derleme öğesinin hata ayıklama özniteliği varsayılan olarak false 'tur.
- Uzaktan hata ayıklama kurulumu ve yapılandırması, daha kolay.
- Artık FTP konumu aracılığıyla açılan bir Web sitesinde hata ayıklaması yapabilirsiniz.

## <a name="debugging-as-a-non-administrator"></a>Yönetici olmayan olarak hata ayıklama

ASP.NET Development Server 'ın eklenmesi, yönetici olmayanların ASP.NET uygulamalarında kolayca hata ayıklamasına olanak tanır. Yerel dosya sisteminde çalışan bir ASP.NET uygulamasının hatası ayıklandığında, Visual Studio, oturum açan kullanıcının bağlamı altında ASP.NET geliştirme sunucusunu başlatır. Bu Kullanıcı daha sonra herhangi bir ek yapılandırma olmadan bu uygulamada hata ayıklayabilirler.

## <a name="debug-is-false-by-default"></a>Hata ayıklama varsayılan olarak false şeklindedir

ASP.NET 1. x içinde, Web. config dosyasının *derleme* öğesindeki *Debug* özniteliği varsayılan olarak *true* olarak ayarlanmıştır. Her zaman, geliştiricilerin bir uygulamayı üretime dağıtmadan önce bu özniteliği *false* olarak ayarlamış olması önerilir, ancak çoğu geliştirici hata ayıklama özniteliği true olarak ayarlanan sonuçları tam olarak anlamadığından, yalnızca olduğu gibi ayrılmaları gerekir.

Hata ayıklama özniteliği true olarak ayarlanmış en ciddi sorun, ASP. netme Batch derleme modelini devre dışı bırakmasıdır. Bu nedenle, her sayfa ayrı bir DLL 'de derlenir. Bir Web uygulaması binlerce sayfadan oluşuyorsa (herhangi bir anlama göre değil), bu uygulama tarafından birkaç bin küçük dll oluşturulacak demektir. Bu dll 'Lerin boyutu küçük olsa da, bellekte belirli bir konuma yüklenmez. Bu nedenle, sistem belleğinde parçalanma oluşmasına neden olur ve OutOfMemoryException oluşumlarına katkıda bulunabilir.

ASP.NET 2,0 ' de, hata ayıklama özniteliği varsayılan olarak false olarak ayarlanır. Zaten gördüğünüze göre, bir geliştirici Visual Studio 2005 ' de bir ASP.NET uygulamasını hata ayıkladığında, hata ayıklama etkinken bir Web. config dosyası eklemesi istenir. Bunun yapılması, ASP.NET 1. x içinde bulunan dezavantajları doğurur, ancak artık geliştirici, uygulamanın üretime taşınmadan önce özniteliğin yanlış olarak sıfırlanması gerektiğini açıkça unutmayın.

## <a name="remote-debugging-setup-and-configuration"></a>Uzaktan hata ayıklama kurulumu ve yapılandırması

Visual Studio 2002/2003 ' de, uzaktan hata ayıklama makine hata ayıklama Yöneticisi 'ne (MDM. exe) ve Vs7jit. exe işlemine güvendi. Bu nedenle, uzaktan hata ayıklama sorunlarının giderilmesi genellikle müşteriler için siyah bir kutu olduğunu ve genellikle PSS için çok daha iyi bir seçenektir.

Visual Studio 2005, MDM. exe ve Vs7jit. exe işlemlerine güvenliğini ortadan kaldırır. Bunun yerine, artık uzaktan hata ayıklama Izleyicisi hizmetini (Msvsmon. exe) kullanır.

Visual Studio 2005 ' de uzaktan hata ayıklama gereksinimi oldukça basittir. Hata ayıklamadan önce uzak sunucuda Msvsmon. exe ' yi çalıştırmanız gerekir. Uzaktan hata ayıklama Izleyicisi 'Ni Visual Studio CD 'sinden yükleyebilir veya yalnızca Web sunucusunda herhangi bir şey yüklemeden bir paylaşımdan Msvsmon. exe dosyasını çalıştırabilirsiniz.

Msvsmon. exe dosyasını çalıştırdığınızda, uzaktan hata ayıklama için engellenmekte olan bağlantı noktaları hakkında şikayetde olabilir. Neyse ki, aşağıda gösterildiği gibi, uyarı iletişim kutusunda sağ taraftaki bağlantı noktalarını kolayca kaldırabilirsiniz.

![Windows Güvenlik Duvarı 'nın uzaktan hata ayıklamayı engellediğini bildirme](improvements-in-visual-studio-2005/_static/image9.jpg)

**Şekil 12**: Windows Güvenlik Duvarı 'Nın uzaktan hata ayıklamayı engellediğini bildirme

Hata ayıklama için gereken bağlantı noktalarının engeli kaldırıldıktan sonra, aşağıda gösterildiği gibi Uzaktan Hata Ayıklama İzleyicisi görürsünüz. Bu arabirimden bağlantıları izleyebilir ve hata ayıklama izinlerini kolayca değiştirebilirsiniz.

![Uzaktan Hata Ayıklama İzleyicisi](improvements-in-visual-studio-2005/_static/image10.jpg)

**Şekil 13**: uzaktan hata ayıklama İzleyicisi

FTP aracılığıyla açılan bir Web uygulamasında uzaktan hata ayıklama de mümkündür. Adımlar, daha önce kapsanmış olanlarla aynıdır. Ancak, bu modülde daha önce özetlenen şekilde, FTP projesine göz atmak için bir temel URL belirtmeniz gerekir.

## <a name="lab-2"></a>Laboratuvar 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Visual Studio 2005 ile uzaktan hata ayıklama

Bu laboratuvar, Visual Studio 2005 ile uzaktan hata ayıklama boyunca size yol gösterecektir.

Bu laboratuvarın video kılavuzu için buraya tıklayın.

![](improvements-in-visual-studio-2005/_static/image5.png)

[Tam ekran videosunu açın](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

Bu laboratuvar, biri Visual Studio 2005 çalıştıran ve IIS 5 ya da üstünü çalıştıran iki makineniz olmasını gerektirir.

1. Visual Studio 2005 ' i açın ve uzak sunucuda yeni bir Web sitesi oluşturun.

> [!NOTE]
> Web sitesini uzak bir IIS örneğinde veya FTP aracılığıyla oluşturabilirsiniz.

1. Uzak Web sunucusundan, bir UNC yolu kullanarak geliştirme makinesindeki Msvsmon. exe ' yi bulun ve yürütün.  
 Msvsmon. exe için varsayılan konum/sunucu \ sunucu/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.
2. Uzaktan hata ayıklama için bağlantı noktalarının engellemesini kaldırmanız istenirse, bunu yapın.
3. Geliştirme makinesinden, default. aspx için arka plan kodunu açın ve sayfa/_Load yönteminde bir kesme noktası ayarlayın.
4. Geliştirme makinesinden hata ayıklamayı başlatın.

Kesme noktasına beklenen şekilde vurmalısınız.

## <a name="aspnet-development-server"></a>ASP.NET Geliştirme Sunucusu

Zaten tartışıyoruz. Visual Studio 2005, ASP.NET Development Server adlı bir Web sunucusuyla birlikte gelir. (ASP.NET geliştirme sunucusu bazen Cassini olarak adlandırılır.) Bu Web sunucusu, dosya sisteminde çalışan Web uygulamalarına gözatacağınız ve hata ayıklamanın uygun bir yoludur.

ASP.NET Development Server, kısıtlı bir Web sunucusudur. Uzak bağlantılara izin vermez, Web sunucusunu başlatan kullanıcı dışında herhangi bir kullanıcıdan gelen isteklere izin vermez. Ayrıca, ASP sayfaları sunma özelliğine sahip değildir. Yalnızca ASP.NET kaynakları ve HTML kaynakları (görüntüler, CSS dosyaları vb. dahil) sunulur.

ASP.NET geliştirme sunucusu, c:/Windows/Microsoft. NET/Framework/v 2.0./ */* / */* /* konumunda bulunan webdev. webserver. exe dosyası çalıştırılarak komut satırı aracılığıyla başlatılabilir. Aşağıdaki iletişim kutusu kullanılabilir parametreleri görüntüler.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**Şekil 14**

> [!NOTE]
> ASP.NET geliştirme sunucusu, komut satırı aracılığıyla açıkça başlatıldığında desteklenmez.
