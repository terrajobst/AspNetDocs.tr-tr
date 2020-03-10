---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Ana sayfalar | Microsoft Docs
author: microsoft
description: Önemli bileşenlerden biri, başarılı bir Web sitesi için tutarlı bir görünüm ve kullanım açısından. ASP.NET 1. x içinde, geliştiriciler ortak sayfa eled 'yi çoğaltmak için Kullanıcı denetimleri kullandı...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567335"
---
# <a name="master-pages"></a>Ana Sayfalar

[Microsoft](https://github.com/microsoft) tarafından

> Önemli bileşenlerden biri, başarılı bir Web sitesi için tutarlı bir görünüm ve kullanım açısından. ASP.NET 1. x içinde, geliştiriciler bir Web uygulaması genelinde ortak sayfa öğelerini çoğaltmak için Kullanıcı denetimleri kullandı. Bu, çok daha fazla bir çözüm olsa da, Kullanıcı denetimlerinin kullanılması bazı dezavantajları vardır. Örneğin, bir kullanıcı denetiminin konumundaki bir değişiklik, bir sitede birden çok sayfada değişiklik yapılmasını gerektirir. Kullanıcı denetimleri, bir sayfaya eklendikten sonra Tasarım görünümü de işlenmez.

Önemli bileşenlerden biri, başarılı bir Web sitesi için tutarlı bir görünüm ve kullanım açısından. ASP.NET 1. x içinde, geliştiriciler bir Web uygulaması genelinde ortak sayfa öğelerini çoğaltmak için Kullanıcı denetimleri kullandı. Bu, çok daha fazla bir çözüm olsa da, Kullanıcı denetimlerinin kullanılması bazı dezavantajları vardır. Örneğin, bir kullanıcı denetiminin konumundaki bir değişiklik, bir sitede birden çok sayfada değişiklik yapılmasını gerektirir. Kullanıcı denetimleri, bir sayfaya eklendikten sonra Tasarım görünümü de işlenmez.

ASP.NET 2,0, tutarlı bir görünüm tutmanın bir yolu olarak ana sayfaları tanıtır ve yakında göreceğiniz gibi, ana sayfalar Kullanıcı denetimi yöntemi üzerinde önemli bir gelişimi temsil eder.

## <a name="why-master-pages"></a>Ana sayfalar neden?

ASP.NET 2,0 ' de ana sayfaların neden gerekli olduğunu merak ediyor olabilirsiniz. Tüm Web sitesi geliştiricileri, sayfalar arasında içerik alanı paylaşmak için ASP.NET 1. x içindeki kullanıcı denetimlerini zaten kullanıyor. Kullanıcı denetimlerinin ortak bir düzen oluşturmak için en iyi bir çözüm olmasının bazı nedenleri vardır.

Kullanıcı denetimleri sayfa düzeni gerçekten tanımlamaz. Bunun yerine, sayfanın bir bölümünün düzen ve işlevini tanımlar. Bir kullanıcı denetimi çözümünün yönetilebilirlik düzeyini çok daha zor hale getiren bu ikisi arasındaki ayrım önemlidir. Örneğin, sayfanızdaki bir kullanıcı denetiminin konumunu değiştirmek istediğinizde, Kullanıcı denetiminin göründüğü gerçek sayfayı düzenlemeniz gerekir. Yalnızca birkaç sayfanız varsa, ancak büyük sitelerde hızlı bir şekilde site yönetimi haline gelir.

Ortak bir düzen tanımlamak için kullanıcı denetimlerini kullanmanın başka bir dezavantajı, ASP.NET 'in mimarisindeki bir mimaridir. Bir kullanıcı denetiminin ortak bir üyesi değiştirilirse, Kullanıcı denetimini kullanan tüm sayfaları yeniden derlemeniz gerekir. Bu durumda, ASP.NET ilk kez erişildiğinde sayfalarınıza yeniden JıT. Bu, bir kez daha büyük siteler için ölçeklenemeyen bir mimari ve bir site yönetimi sorunu üretir.

Bu sorunların her ikisi de (ve çok daha fazlası) ASP.NET 2,0 ' deki ana sayfalarla sorunsuz bir şekilde karşılanır.

## <a name="how-master-pages-work"></a>Ana sayfaların çalışması

Ana sayfa, diğer sayfaların şablonuna benzer. Diğer sayfalar arasında paylaşılması gereken sayfa öğeleri (örn. menüler, kenarlıklar vb.) ana sayfaya eklenir. Siteye yeni sayfa eklendiğinde, bunları bir ana sayfayla ilişkilendirebilirsiniz. Ana sayfayla ilişkili bir sayfaya **içerik sayfası**denir. Varsayılan olarak, bir içerik sayfası ana sayfadan görünümü alır. Ancak, bir ana sayfa oluşturduğunuzda, sayfanın içerik sayfasının kendi içeriğiyle yerine geçecek kısımlarını tanımlayabilirsiniz. Bu bölümler ASP.NET 2,0 ' de tanıtılan yeni bir denetim kullanılarak tanımlanır; **ContentPlaceHolder** denetimi.

Ana sayfa, herhangi bir sayıda ContentPlaceHolder denetimini içerebilir (veya hiç hiçbirini içermez.) İçerik sayfasında, ContentPlaceHolder denetimlerinin içeriği **içerik** denetimlerinin içinde, ASP.NET 2,0 ' deki başka bir yeni denetim de görüntülenir. Varsayılan olarak, kendi içeriğinizi sağlayabilmeniz için içerik sayfaları Içerik denetimleri boştur. İçerik denetimlerinin içindeki ana sayfadaki içeriği kullanmak istiyorsanız, bu modülde daha sonra göreceğiniz şekilde bunu yapabilirsiniz. Içerik denetimi, Içerik denetiminin ContentPlaceHolderID özniteliği aracılığıyla ContentPlaceHolder denetimiyle eşleştirilir. Aşağıdaki kod bir Içerik denetimini ana sayfada mainBody adlı bir ContentPlaceHolder denetimiyle eşler.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> Genellikle, diğer sayfalar için ana sayfaları temel sınıf olarak tanıtın. Aslında doğru değil. Ana sayfalar ve içerik sayfaları arasındaki ilişki Devralınanlar değildir.

**Şekil 1** ' de, Visual Studio 2005 ' de göründükleri gibi bir ana sayfa ve ilişkili içerik sayfası gösterilmektedir. ContentPlaceHolder denetimini ana sayfada ve ilgili Içerik denetiminde içerik sayfasında görebilirsiniz. ContentPlaceHolder 'ın dışındaki ana sayfa içeriğinin görünür olduğunu ancak içerik sayfasında gri renkte olduğunu unutmayın. İçerik sayfası tarafından yalnızca ContentPlaceHolder 'ın içindeki içerik etkinleştirilebilir. Ana sayfadan gelen diğer tüm içerikler sabittir.

![Ana sayfa ve ilişkili içerik sayfası](master-pages/_static/image1.jpg)

**Şekil 1**: Ana sayfa ve ilişkili içerik sayfası

## <a name="creating-a-master-page"></a>Ana sayfa oluşturma

Yeni bir ana sayfa oluşturmak için:

1. Visual Studio 2005 ' i açın ve yeni bir Web sitesi oluşturun.
2. Dosya, yeni, dosya ' ya tıklayın.
3. **Şekil 2**' de gösterildiği gibi yeni öğe Ekle Iletişim kutusundan asıl dosya ' yı seçin.
4. Ekle’ye tıklayın.

![Yeni Ana sayfa oluşturma](master-pages/_static/image2.jpg)

**Şekil 2**: yeni bir ana sayfa oluşturma

Ana sayfa için dosya uzantısının *. Master*olduğunu unutmayın. Bu, ana sayfanın sıradan bir sayfadan farklı olan yöntemlerinden biridir. Diğer birincil fark, bir @Page yönergesinin yerine, ana sayfa bir @Master yönergesi içerir. Yeni oluşturduğunuz ana sayfa için kaynak görünümüne geçin ve kodu gözden geçirin.

Yeni bir ana sayfa varsayılan olarak bir ContentPlaceHolder denetimine sahip olur. Çoğu durumda, önce ortak sayfa öğelerini oluşturmak ve ardından özel içeriğin istendiği ContentPlaceHolder denetimlerini eklemek daha anlamlı hale gelir. Bu durumlarda, geliştiriciler varsayılan ContentPlaceHolder denetimini silmek ve sayfa geliştirildikleri sürece yenilerini eklemek isteyeceksiniz. ContentPlaceHolder denetimleri, boyutlandırma tutamaçlarını görüntüleyen bir olgusuna rağmen yeniden boyutlandırılabilir. ContentPlaceHolder denetim boyutları, içerdiği içeriğe göre otomatik olarak bir özel durumla belirlenir; Tablo hücresi gibi bir blok öğesinin içine ContentPlaceHolder denetimini yerleştirirseniz, öğe boyutuna göre boyut olur.

## <a name="lab-1-working-with-master-pages"></a>Laboratuvar 1 ana sayfalarla çalışma

Bu laboratuvarda yeni bir ana sayfa oluşturacak ve üç ContentPlaceHolder denetimi tanımlayacaksınız. Daha sonra yeni bir Içerik sayfası oluşturacak ve içeriği en az bir ContentPlaceHolder denetimleriyle değiştirecek.

1. Ana sayfa oluşturun ve ContentPlaceHolder denetimleri ekleyin. 

    1. Yukarıda açıklandığı gibi yeni bir ana sayfa oluşturun.
    2. Varsayılan ContentPlaceHolder denetimini silin.
    3. Denetimin gölgeli üst kenarlığına tıklayarak ContentPlaceHolder denetimini seçin ve ardından klavyenizdeki DEL tuşuna basarak silin.
    4. Şekil 3 ' te gösterildiği gibi *üstbilgiyi ve yan* şablonu kullanarak yeni bir tablo ekleyin. Tüm tablonun tasarımcıda görünmesi için Genişlik ve yükseklik değerlerini %90 olarak değiştirin.

![](master-pages/_static/image3.jpg)

**Şekil 3**

1. İmleci tablonun her bir hücresine yerleştirin ve *valıgn* özelliğini *top*olarak ayarlayın.
2. Araç kutusundan tablonun üst hücresine (başlık hücresi) bir ContentPlaceHolder denetimi ekleyin.
3. Bu ContentPlaceHolder denetimini eklediğinizde, Şekil 4 ' te gösterildiği gibi satır yüksekliğinin neredeyse sayfanın tamamını gösterdiğine dikkat edin. Bu noktada bundan endişe etmeyin.

![Boş alan, ContentPlaceHolder ile aynı hücrede](master-pages/_static/image1.gif)

**Şekil 4**: boş alan ContentPlaceHolder ile aynı hücrede

1. Bir ContentPlaceHolder denetimini diğer iki hücreye yerleştirin. Diğer ContentPlaceHolder denetimleri eklendikten sonra, tablo hücrelerinin boyutu beklenen şekilde olmalıdır. Sayfa artık **Şekil 5**' te gösterilen sayfa gibi görünmelidir.

![Tüm ContentPlaceHolder denetimleriyle ana öğe. Başlık hücresi için hücre yüksekliğinin artık ne olması gerektiğine dikkat edin](master-pages/_static/image2.gif)

**Şekil 5**: tüm ContentPlaceHolder denetimleriyle ana öğe. Başlık hücresi için hücre yüksekliğinin artık ne olması gerektiğine dikkat edin

1. Üç ContentPlaceHolder denetiminin her birine istediğiniz metin girin.
2. Ana sayfayı exercise1. Master olarak kaydedin.
3. Yeni bir Web formu oluşturun ve exercise1. Master ana sayfası ile ilişkilendirin.
4. Visual Studio 2005 'de dosya, yeni, dosya ' yı seçin.
5. Yeni öğe Ekle iletişim kutusunda **Web formu** ' nu seçin.
6. Şekil 6 ' da gösterildiği gibi ana sayfa seç onay kutusunun işaretli olduğundan emin olun.

![Yeni Içerik sayfası ekleme](master-pages/_static/image3.gif)

**Şekil 6**: yeni içerik sayfası ekleme

1. Ekle’ye tıklayın.
2. Şekil 7 ' de gösterildiği gibi ana sayfa Seç iletişim kutusunda exercise1. Master öğesini seçin.
3. Yeni içerik sayfasını eklemek için Tamam ' ı tıklatın.

Yeni içerik sayfası, Visual Studio 'da, ana sayfada bulunan her bir ContentPlaceHolder denetimi için bir Içerik denetimiyle görüntülenir. Varsayılan olarak, kendi içeriğinizi ekleyebilmeniz için Içerik denetimleri boştur. Ana sayfada bulunan ContentPlaceHolder denetimindeki içeriği kullanmak istiyorsanız, akıllı etiket simgesine (denetimin sağ üst köşesindeki küçük siyah ok) tıklayın ve **Şekil 8**' de gösterildiği gibi akıllı etiketin *Içeriğini Yöneticiler için varsayılan* öğesini seçin. Bunu yaptığınızda, menü öğesi *özel Içerik oluşturmak*için değişir. Bu noktada tıklanması, içeriği ana sayfadan kaldırarak söz konusu Içerik denetimi için özel içerik tanımlamanıza olanak sağlar.

![Içerik denetimini varsayılan olarak ana sayfa Içeriğine ayarlama](master-pages/_static/image4.gif)

**Şekil 7**: Içerik denetimini varsayılan olarak ana sayfa içeriğine ayarlama

## <a name="connecting-master-page-and-content-pages"></a>Ana sayfa ve Içerik sayfalarını bağlama

Ana sayfa ile içerik sayfası arasındaki ilişki dört farklı şekilde yapılandırılabilir:

- @Page yönergesinin <strong>MasterPageFile</strong> özniteliği
- Kodda **Page. MasterPageFile** özelliği ayarlanıyor.
- **&lt;sayfaları** , uygulamalar yapılandırma dosyasında (uygulamanın kök klasöründeki Web. config)&gt;öğesi
- **&lt;sayfaları** alt klasörler yapılandırma dosyasında (bir alt klasördeki Web. config)&gt;öğesi

## <a name="masterpagefile-attribute"></a>MasterPageFile özniteliği

MasterPageFile özniteliği, bir ana sayfanın belirli bir ASP.NET sayfasına uygulanmasını kolaylaştırır. Ayrıca, alıştırma 1 ' de yaptığınız gibi **Ana sayfa seç** onay kutusunu işaretlediğinizde ana sayfayı uygulamak için de kullanılan yöntemdir.

## <a name="setting-pagemasterpagefile-in-code"></a>Kodda Page. MasterPageFile ayarlanıyor

Kodda MasterPageFile özelliğini ayarlayarak, çalışma zamanında içeriğinize belirli bir ana sayfa uygulayabilirsiniz. Bu, bir kullanıcı rolüne veya diğer ölçütlere göre belirli bir ana sayfanın uygulanması gerekebilecek durumlarda faydalıdır. MasterPageFile özelliğinin PreInit yönteminde ayarlanması gerekir. PreInit yönteminden sonra ayarlandıysa, bir InvalidOperationException atılır. Bu özelliğin ayarlandığı sayfanın, sayfanın en üst düzey denetimi olarak bir Içerik denetimine sahip olması gerekir. Aksi takdirde, MasterPageFile özelliği ayarlandığında bir HttpException oluşturulur.

## <a name="using-the-ltpagesgt-element"></a>&lt;Pages&gt; öğesi kullanma

Web. config dosyasının &lt;Pages&gt; öğesinde masterPageFile özniteliğini ayarlayarak sayfalarınız için bir ana sayfa yapılandırabilirsiniz. Bu yöntemi kullanırken, uygulama yapısında daha düşük olan Web. config dosyalarının bu ayarı geçersiz kılabileceğini aklınızda bulundurun. @Page yönergesinde ayarlanan herhangi bir MasterPageFile özniteliği de bu ayarı geçersiz kılar. &lt;Pages&gt; öğesi kullanmak, belirli klasörlerde veya dosyalarda gerektiğinde geçersiz kılınabilen bir *ana* ana sayfa oluşturmayı kolaylaştırır.

## <a name="properties-in-master-pages"></a>Ana sayfalardaki Özellikler

Ana sayfa, bu özellikleri ana sayfa içinde ortak hale getirerek özellikleri açığa çıkarır. Örneğin, aşağıdaki kod SomeProperty adlı bir özelliği tanımlar:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

Içerik sayfasından SomeProperty özelliğine erişmek için şu şekilde ana özelliği kullanmanız gerekir:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>Ana sayfaları iç içe geçirme

Ana sayfalar, büyük bir Web uygulaması genelinde ortak bir görünüm sağlamaya yönelik mükemmel bir çözümdür. Bununla birlikte, büyük bir sitenin belirli bölümlerinin ortak bir arabirim paylaştığından, diğer parçalar farklı bir arabirim paylaştığından yaygın olmayan bir durumdur. Bu ihtiyacı karşılamak için, çok sayıda ana sayfa kusursuz çözümdür. Bununla birlikte, büyük bir uygulamanın belirli bileşenleri (örneğin, bir menü gibi), tüm sayfalar ve yalnızca sitenin belirli bölümleri arasında paylaşılan diğer bileşenler arasında paylaşılan bazı bileşenlere sahip olabileceğini de ele almamıştır. Bu tür bir durum için, iç içe geçmiş ana sayfalar, gereksinimi tamamen doldurur. Gördüğünüz gibi, normal ana sayfa bir ana sayfadan ve bir içerik sayfasından oluşur. İç içe yerleştirilmiş ana sayfa durumunda iki ana sayfa vardır; üst ana öğe ve alt ana öğe. Alt ana sayfa aynı zamanda bir içerik sayfasıdır ve ana ana sayfa üst sayfasıdır.

Tipik bir ana sayfanın kodu aşağıda verilmiştir:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

İç içe geçmiş bir ana senaryoda bu, üst ana öğe olur. Bu sayfayı, ana sayfası olarak başka bir ana sayfa kullanır ve bu kod şöyle görünür:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Bu senaryoda, alt ana ana ana öğe için de bir içerik sayfası olduğunu unutmayın. Alt ana öğenin tüm içeriği, üst öğenin ContentPlaceHolder denetiminden içeriğini alan bir Içerik denetiminin içinde görüntülenir.

> [!NOTE]
> Tasarımcı desteği iç içe yerleştirilmiş ana sayfalar için kullanılamaz. İç içe yerleştirilmiş ana şablonları kullanarak geliştirme yaparken, kaynak görünümü kullanmanız gerekir.

Bu videoda, iç içe yerleştirilmiş ana sayfaların kullanımına ilişkin bir anlatım gösterilmektedir.

![](master-pages/_static/image1.png)

[Tam ekran videosunu açın](master-pages/_static/nested1.wmv)

![Ana sayfa seçme](master-pages/_static/image4.jpg)

**Şekil 8**: Ana sayfa seçme
