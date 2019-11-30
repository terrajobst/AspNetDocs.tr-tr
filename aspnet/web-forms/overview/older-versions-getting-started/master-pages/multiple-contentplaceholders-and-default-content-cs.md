---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
title: Birden çok Contenttutucuları ve varsayılan IçerikC#() | Microsoft Docs
author: rick-anderson
description: Birden çok içerik alanı sahiplerini bir ana sayfaya nasıl ekleneceğini ve içerik yer tutucuları içinde varsayılan içeriğin nasıl belirtilme konusunda inceler.
ms.author: riande
ms.date: 05/21/2008
ms.assetid: b9b9798b-027d-46cc-9636-473378e437ac
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
msc.type: authoredcontent
ms.openlocfilehash: e902bcae05c0e7976a20293f2b01e5f2e2bee13a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639403"
---
# <a name="multiple-contentplaceholders-and-default-content-c"></a>Birden Çok ContentPlaceHolder ve Varsayılan İçerik (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_CS.pdf)

> Birden çok içerik alanı sahiplerini bir ana sayfaya nasıl ekleneceğini ve içerik yer tutucuları içinde varsayılan içeriğin nasıl belirtilme konusunda inceler.

## <a name="introduction"></a>Giriş

Önceki öğreticide, ana sayfaların ASP.NET geliştiricilerin tutarlı bir site genelinde düzen oluşturmasını nasıl sağladığımızda anlatılmıştır. Ana sayfalar, sayfa temelinde özelleştirilebilen tüm içerik sayfaları ve bölgeleri için ortak olan her iki biçimlendirmeyi tanımlar. Önceki öğreticide basit bir ana sayfa (`Site.master`) ve iki içerik sayfası (`Default.aspx` ve `About.aspx`) oluşturduk. Ana sayfamız, sırasıyla `<head>` öğesinde ve Web formunda bulunan `head` ve `MainContent`adlı iki Contentbir yer tutucudan oluşur. Her birinin içerik sayfalarında iki Içerik denetimi olsa da, yalnızca `MainContent`karşılık gelen biçimlendirme belirtiyoruz.

`Site.master`, bir ana sayfa birden fazla Içerik yer tutucusu içerebilir. Daha fazlası, ana sayfa ContentPlaceHolder denetimleri için varsayılan biçimlendirmeyi belirtebilir. Daha sonra bir içerik sayfası, isteğe bağlı olarak kendi işaretlemesini belirtebilir veya varsayılan biçimlendirmeyi kullanabilir. Bu öğreticide, ana sayfada birden çok içerik denetimi kullanmayı ve ContentPlaceHolder denetimlerinde nasıl varsayılan biçimlendirme tanımlanacağını görmeyi inceleyeceğiz.

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>1\. Adım: Ana sayfaya ek ContentPlaceHolder denetimleri ekleme

Birçok Web sitesi tasarımı, ekranda sayfa temelinde özelleştirilmiş birkaç alan içerir. `Site.master`, önceki öğreticide oluşturduğumuz ana sayfa, `MainContent`adlı Web formu içinde tek bir ContentPlaceHolder içerir. Özellikle, bu ContentPlaceHolder `mainContent` `<div>` öğesi içinde bulunur.

Şekil 1 ' de bir tarayıcıdan görüntülendiklerinde `Default.aspx` gösterilmektedir. Daire içinde kırmızı olan bölge, `MainContent`karşılık gelen sayfaya özgü işaretlemedir.

[Daire Içinde bulunan bölge ![sayfa temelinde şu anda özelleştirilebilen alanı gösterir](multiple-contentplaceholders-and-default-content-cs/_static/image2.png)](multiple-contentplaceholders-and-default-content-cs/_static/image1.png)

**Şekil 01**: Daire Içinde olan bölge, şu anda sayfa sayfa temelinde özelleştirilebilir alanı gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image3.png))

Şekil 1 ' de gösterilen bölgeye ek olarak, derslerin ve haber bölümlerinin altındaki sol sütuna sayfaya özgü öğeler de eklememiz gerektiğini düşünelim. Bunu gerçekleştirmek için ana sayfaya başka bir ContentPlaceHolder denetimi ekleyeceğiz. Bunun yanı sıra, Visual Web Developer 'da `Site.master` ana sayfasını açın ve ardından bir ContentPlaceHolder denetimini, Haberler bölümünün ardından araç kutusundan Tasarımcı üzerine sürükleyin. ContentPlaceHolder 'ın `ID` `LeftColumnContent`olarak ayarlayın.

[Ana sayfanın sol sütununa bir ContentPlaceHolder denetimi eklemek ![](multiple-contentplaceholders-and-default-content-cs/_static/image5.png)](multiple-contentplaceholders-and-default-content-cs/_static/image4.png)

**Şekil 02**: ana sayfanın sol sütununa bir ContentPlaceHolder denetimi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image6.png))

Ana sayfaya ContentPlaceHolder `LeftColumnContent` eklendiğinde, `ContentPlaceHolderID` `LeftColumnContent`olarak ayarlanan sayfada bir Içerik denetimi ekleyerek sayfa temelinde bu bölge için içerik tanımlayabiliriz. Bu işlemi adım 2 ' de inceleyeceğiz.

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>2\. Adım: Içerik sayfalarında yeni ContentPlaceHolder için Içerik tanımlama

Web sitesine yeni bir içerik sayfası eklerken, Visual Web Developer seçili ana sayfadaki her bir ContentPlaceHolder için sayfada otomatik olarak bir Içerik denetimi oluşturur. Adım 1 ' de ana sayfamızda bir `LeftColumnContent` eklenmiş olan yeni ASP.NET sayfalarında artık üç Içerik denetimi olacaktır.

Bunu göstermek için, `Site.master` ana sayfasına bağlanan `MultipleContentPlaceHolders.aspx` adlı kök dizine yeni bir içerik sayfası ekleyin. Visual Web Developer bu sayfayı aşağıdaki bildirim temelli işaretlerle oluşturur:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample1.aspx)]

Içerik denetimine `MainContent` Contentyertutucuları (`Content2`) başvuran içerik girin. Sonra, `Content3` Içerik denetimine aşağıdaki biçimlendirmeyi ekleyin (`LeftColumnContent` ContentPlaceHolder öğesine başvurur):

[!code-html[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample2.html)]

Bu biçimlendirmeyi ekledikten sonra bir tarayıcı aracılığıyla sayfayı ziyaret edin. Şekil 3 ' te gösterildiği gibi, `Content3` Içerik denetimine yerleştirilmiş olan biçimlendirme, Haberler bölümünün altındaki sol sütunda görüntülenir (kırmızı renkte daire içinde). `Content2` yerleştirilmiş olan biçimlendirme sayfanın sağ bölümünde görüntülenir (mavi renkli daire içinde).

[Sol sütun ![artık Haberler bölümünün altındaki sayfaya özgü Içerikleri Içerir](multiple-contentplaceholders-and-default-content-cs/_static/image8.png)](multiple-contentplaceholders-and-default-content-cs/_static/image7.png)

**Şekil 03**: sol sütun artık Haberler bölümünün altındaki sayfaya özgü içerikleri içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image9.png))

### <a name="defining-content-in-existing-content-pages"></a>Var olan Içerik sayfalarında Içerik tanımlama

Yeni bir içerik sayfası oluşturmak, 1. adımda eklediğimiz ContentPlaceHolder denetimini otomatik olarak ekler. Ancak var olan iki içerik sayfamız-`About.aspx` ve `Default.aspx`-`LeftColumnContent` ContentPlaceHolder için bir Içerik denetimine sahip değildir. Bu iki sayfada bu ContentPlaceHolder 'ın içeriğini belirtmek için bir Içerik denetimi kendimize eklememiz gerekiyor.

Çoğu ASP.NET Web denetiminin aksine, Visual Web Developer araç kutusu bir Içerik denetim öğesi içermez. Kaynak görünümüne Içerik denetiminin bildirim temelli işaretlemesini el ile yazalım, ancak daha kolay ve daha hızlı bir yaklaşım Tasarım görünümü kullanmaktır. `About.aspx` sayfasını açın ve Tasarım görünümü geçin. Şekil 4 ' te gösterildiği gibi, Tasarım görünümü `LeftColumnContent` ContentPlaceHolder görüntülenir; üzerine fare eklerseniz, başlık şöyle görünür: "LeftColumnContent (Master)." Başlığa "Master" eklenmesi, bu ContentPlaceHolder için sayfada tanımlanmış Içerik denetimi olmadığını gösterir. ContentPlaceHolder için bir Içerik denetimi varsa, `MainContent`için başlık şu şekilde görünür: "*ContentPlaceHolderID* (Custom)."

`About.aspx``LeftColumnContent` ContentPlaceHolder için bir Içerik denetimi eklemek için, ContentPlaceHolder 'ın akıllı etiketini genişletin ve özel Içerik oluştur bağlantısına tıklayın.

[![. aspx için Tasarım görünümünde, LeftColumnContent ContentPlaceHolder görüntülenir](multiple-contentplaceholders-and-default-content-cs/_static/image11.png)](multiple-contentplaceholders-and-default-content-cs/_static/image10.png)

**Şekil 04**: `About.aspx` Için tasarım görünümü `LeftColumnContent` ContentPlaceHolder 'ı gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image12.png))

Özel Içerik oluştur bağlantısına tıkladığınızda sayfada gerekli Içerik denetimi oluşturulur ve `ContentPlaceHolderID` özelliği ContentPlaceHolder 'ın `ID`olarak ayarlanır. Örneğin, `About.aspx` `LeftColumnContent` bölgesi için özel Içerik oluştur bağlantısına tıkladığınızda, aşağıdaki bildirim temelli biçimlendirmeyi sayfaya ekler:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>Içerik denetimlerini atlama

ASP.NET, tüm içerik sayfalarının ana sayfada tanımlanan her bir ve her ContentPlaceHolder için Içerik denetimlerini içermesini gerektirmez. Bir Içerik denetimi atlanırsa, ASP.NET altyapısı ana sayfada ContentPlaceHolder içinde tanımlanan biçimlendirmeyi kullanır. Bu biçimlendirme, ContentPlaceHolder 'ın *varsayılan içeriği* olarak adlandırılır ve bazı bölgelere ait içeriğin sayfaların çoğunluğu arasında ortak olduğu, ancak az sayıda sayfa için özelleştirilme gereken senaryolarda faydalıdır. 3\. adım ana sayfada varsayılan içeriği belirtmeyi araştırır.

Şu anda `Default.aspx` `head` ve `MainContent` Contentyertutucuları için iki Içerik denetimi içerir; `LeftColumnContent`için bir Içerik denetimi yoktur. Sonuç olarak, `Default.aspx` işlendiğinde `LeftColumnContent` ContentPlaceHolder 'ın varsayılan içeriği kullanılır. Henüz bu ContentPlaceHolder için herhangi bir varsayılan içerik tanımlanmadığımızda, net etkisi, bu bölge için hiçbir biçimlendirme yayınlanmamıştır. Bu davranışı doğrulamak için `Default.aspx` bir tarayıcı üzerinden ziyaret edin. Şekil 5 ' te gösterildiği gibi, Haberler bölümünün altındaki sol sütunda hiçbir işaretleme yayılmadı.

[![, LeftColumnContent ContentPlaceHolder için hiçbir Içerik Işlenmiyor](multiple-contentplaceholders-and-default-content-cs/_static/image14.png)](multiple-contentplaceholders-and-default-content-cs/_static/image13.png)

**Şekil 05**: `LeftColumnContent` ContentPlaceHolder Için hiçbir içerik işlenmiyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image15.png))

## <a name="step-3-specifying-default-content-in-the-master-page"></a>3\. Adım: Ana sayfada varsayılan Içeriği belirtme

Bazı Web sitesi tasarımları, bir veya iki özel durum dışında, içeriği sitedeki tüm sayfalar için aynı olan bir bölge içerir. Kullanıcı hesaplarını destekleyen bir Web sitesi düşünün. Bu tür bir site, ziyaretçilerin sitede oturum açmak için kimlik bilgilerini girebilecekleri bir oturum açma sayfası gerektirir. Oturum açma işlemini hızlandırmak için, Web sitesi tasarımcıları her sayfanın sol üst köşesine Kullanıcı adı ve parola kutuları ekleyebilir ve kullanıcıların oturum açma sayfasını açıkça ziyaret etmesini sağlamak için oturum açmasını sağlar. Bu Kullanıcı adı ve parola kutuları pek çok sayfada yardımcı olmakla kalmaz, oturum açma sayfasında, kullanıcının kimlik bilgileri için zaten metin kutuları içeren, bunlar gereksizdir.

Bu tasarımı uygulamak için ana sayfanın sol üst köşesinde bir ContentPlaceHolder denetimi oluşturabilirsiniz. Kullanıcı adı ve parola metin kutularını görüntülemesi gereken her sayfa, bu ContentPlaceHolder için bir Içerik denetimi oluşturur ve gerekli arabirimi ekler. Diğer yandan oturum açma sayfası, bu ContentPlaceHolder için bir Içerik denetimi eklemeyi ya da hiçbir işaretleme tanımlanmadığında bir Içerik denetimi oluşturmayı yok sayacaktır. Bu yaklaşımın aşağı tarafında, siteye eklediğimiz her sayfaya (oturum açma sayfası hariç) Kullanıcı adı ve parola metin kutuları eklemeyi unutmamanız gerekir. Bu sorun sizi istiyor. Bu metin kutularını bir sayfaya ya da daha kötüleştireceğiz, arabirimi doğru bir şekilde uygulayamazyız (Belki de iki tane yerine yalnızca bir TextBox ekleyebilirsiniz).

Daha iyi bir çözüm, ContentPlaceHolder 'ın varsayılan içeriğiyle Kullanıcı adı ve parola metin kutuları tanımlamaktır. Bunu yaptığınızda, bu varsayılan içeriği yalnızca Kullanıcı adı ve parola metin kutuları (örneğin, oturum açma sayfası) görüntülemek. ContentPlaceHolder denetimine yönelik varsayılan içerik belirtmeyi göstermek için, yalnızca tartışılan senaryoyu uygulayalim.

> [!NOTE]
> Bu öğreticinin geri kalanı, Web sitemizi tüm sayfalar için sol sütuna, ancak oturum açma sayfasına yönelik bir oturum açma arabirimi içerecek şekilde güncelleştirir. Ancak, bu öğretici Web sitesinin kullanıcı hesaplarını destekleyecek şekilde nasıl yapılandırılacağını incelemez. Bu konu hakkında daha fazla bilgi için [formlarım kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rol](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) öğreticilerimize bakın.

### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>ContentPlaceHolder ekleme ve varsayılan Içeriğini belirtme

`Site.master` ana sayfasını açın ve `DateDisplay` etiketi ile dersler bölümü arasındaki sol sütuna aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample4.aspx)]

Bu biçimlendirmeyi ekledikten sonra ana sayfanızın Tasarım görünümü Şekil 6 ' ya benzer görünmelidir.

[Ana sayfa bir oturum açma denetimi Içerir ![](multiple-contentplaceholders-and-default-content-cs/_static/image17.png)](multiple-contentplaceholders-and-default-content-cs/_static/image16.png)

**Şekil 06**: Ana sayfa bir oturum açma denetimi içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image18.png))

Bu ContentPlaceHolder `QuickLoginUI`, varsayılan içeriği olarak bir oturum açma Web denetimine sahiptir. Oturum açma denetimi, kullanıcıdan bir oturum açma düğmesi ile birlikte Kullanıcı adı ve parola girmesini isteyen bir kullanıcı arabirimi görüntüler. Oturum Aç düğmesine tıklandıktan sonra oturum açma denetimi, kullanıcının kimlik bilgilerini üyelik API 'sine göre dahili olarak doğrular. Bu oturum açma denetimini uygulamada kullanmak için, sitenizi üyelik kullanacak şekilde yapılandırmanız gerekir. Bu konu, Bu öğreticinin kapsamı dışındadır. Kullanıcı hesaplarını destekleyen bir Web uygulaması oluşturma hakkında daha fazla bilgi için [form kimlik doğrulaması, yetkilendirme, Kullanıcı hesapları ve rol](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) öğreticilerime bakın.

Oturum açma denetiminin davranışını veya görünümünü özelleştirmek için ücretsizdir. Özelliklerinden ikisini de ayarladı: `TitleText` ve `FailureAction`. Varsayılan olarak "oturum aç" olan `TitleText` Özellik değeri, denetimin kullanıcı arabiriminin en üstünde görüntülenir. Bu özelliği, bir `<h3>` öğesi olarak "oturum aç" metnini görüntüleyecek şekilde ayarladı. `FailureAction` özelliği, kullanıcının kimlik bilgileri geçersizse ne yapılacağını belirtir. Bu, kullanıcıyı aynı sayfada bırakan ve oturum açma denetimi içinde bir hata iletisi görüntüleyen `Refresh`bir değeri varsayılan olarak alır. Kullanıcıyı geçersiz kimlik bilgileri olayında oturum açma sayfasına gönderen `RedirectToLoginPage`olarak değiştirdim. Kullanıcı başka bir sayfadan oturum açmaya çalıştığında Kullanıcı oturum açma sayfasına göndermek istiyorum, ancak oturum açma sayfası, sol sütuna kolayca sığmayan ek yönergeler ve seçenekler içerebildiğinden, başarısız olur. Örneğin, oturum açma sayfası unutulmuş bir parolayı alma veya yeni bir hesap oluşturma seçeneklerini içerebilir.

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>Oturum açma sayfası oluşturma ve varsayılan Içeriği geçersiz kılma

Ana sayfa tamamlandıktan sonra bir sonraki adımımız oturum açma sayfası oluşturmaktır. Sitenizin `Login.aspx`adlı kök dizinine `Site.master` ana sayfasına bağlayarak bir ASP.NET sayfası ekleyin. Bunun yapılması, `Site.master`' de tanımlanan her bir Contenttutucuları için bir tane olmak üzere dört Içerik denetimi içeren bir sayfa oluşturur.

`MainContent` Içerik denetimine bir oturum açma denetimi ekleyin. Benzer şekilde, `LeftColumnContent` bölgeye herhangi bir içerik eklemek ücretsizdir. Ancak, `QuickLoginUI` ContentPlaceHolder boş olan Içerik denetimini ayrıldığınızdan emin olun. Bu, oturum açma denetiminin, oturum açma sayfasının sol sütununda görünmemesini güvence altına alacak.

`MainContent` ve `LeftColumnContent` bölgeleri için içerik tanımladıktan sonra, oturum açma sayfanızın bildirim temelli işaretleme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample5.aspx)]

Şekil 7 ' de bir tarayıcıdan görüntülendiklerinde Bu sayfa gösterilmektedir. Bu sayfa, `QuickLoginUI` ContentPlaceHolder için bir Içerik denetimi belirttiğinden, ana sayfada belirtilen varsayılan içeriği geçersiz kılar. Net etkisi, ana sayfa Tasarım görünümü (Şekil 6 ' da) görüntülenen oturum açma denetiminin bu sayfada işlenmeyecektir.

[represses oturum açma sayfası, Quickloginuı ContentPlaceHolder 'ın varsayılan Içeriğini ![](multiple-contentplaceholders-and-default-content-cs/_static/image20.png)](multiple-contentplaceholders-and-default-content-cs/_static/image19.png)

**Şekil 07**: oturum açma sayfası, `QuickLoginUI` ContentPlaceHolder 'ın varsayılan içeriğini represses ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image21.png))

### <a name="using-the-default-content-in-new-pages"></a>Yeni sayfalarda varsayılan Içeriği kullanma

Oturum açma sayfası dışındaki tüm sayfalar için oturum açma denetimini sol sütunda göstermek istiyoruz. Bunu başarmak için, oturum açma sayfası hariç tüm içerik sayfaları, ContentPlaceHolder `QuickLoginUI` bir Içerik denetimini atmalıdır. Bir Içerik denetimini atlayarak, bunun yerine ContentPlaceHolder 'ın varsayılan içeriği kullanılacaktır.

Var olan içerik sayfalarımız-`Default.aspx`, `About.aspx`ve `MultipleContentPlaceHolders.aspx`, bu ContentPlaceHolder denetimini ana sayfaya eklemeden önce oluşturulduğundan `QuickLoginUI` için bir Içerik denetimi eklemeyin. Bu nedenle, bu mevcut sayfaların güncelleştirilmesine gerek yoktur. Ancak, Web sitesine eklenen yeni sayfalar, varsayılan olarak `QuickLoginUI` ContentPlaceHolder için bir Içerik denetimi içerir. Bu nedenle, her yeni içerik sayfası eklediğimiz her seferinde bu Içerik denetimlerini kaldırmayı unutmamanız gerekir (oturum açma sayfası durumunda olduğu gibi, ContentPlaceHolder 'ın varsayılan içeriğini geçersiz kılmak istediğimiz sürece).

Içerik denetimini kaldırmak için, bildirim temelli işaretlemesini kaynak görünümden el ile silebilir veya Tasarım görünümü, varsayılan olarak, akıllı etiketindeki ana Içerik bağlantısı ' nı seçin. Her iki yaklaşım da Içerik denetimini sayfadan kaldırır ve aynı net etkiyi üretir.

Şekil 8 ' de bir tarayıcıdan görüntülendiklerinde `Default.aspx` gösterilmektedir. `Default.aspx`, bildirim temelli işaretlerde bir tane `head` ve biri `MainContent`için belirtilen iki Içerik denetimine sahip olduğunu hatırlayın. Sonuç olarak, `LeftColumnContent` ve `QuickLoginUI` Contentyertutucuları için varsayılan içerik görüntülenir.

[![LeftColumnContent ve Quickloginuı Contentyertutucuları için varsayılan Içerik görüntülenir](multiple-contentplaceholders-and-default-content-cs/_static/image23.png)](multiple-contentplaceholders-and-default-content-cs/_static/image22.png)

**Şekil 08**: `LeftColumnContent` ve `QuickLoginUI` Contentyertutucuları Için varsayılan içerik görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](multiple-contentplaceholders-and-default-content-cs/_static/image24.png))

## <a name="summary"></a>Özet

ASP.NET ana sayfa modeli, ana sayfada rastgele sayıda Contentyer tutucu sağlar. Daha fazlası, içerik yer tutucuları, içerik sayfasında karşılık gelen Içerik denetimi olmaması durumunda oluşturulan varsayılan içeriğe sahiptir. Bu öğreticide, ana sayfaya ek ContentPlaceHolder denetimlerinin nasıl ekleneceğini ve hem yeni hem de var olan ASP.NET sayfalarındaki bu yeni Contentyertutucuları için Içerik denetimlerinin nasıl tanımlanacağını gördük. Ayrıca, bir ContentPlaceHolder 'da varsayılan içerik belirtmekten de bakıyoruz. Bu, yalnızca en az sayıda sayfanın belirli bir bölgedeki standart olmayan içeriği özelleştirmesini gerektiren senaryolarda faydalıdır.

Sonraki öğreticide, bir sayfa temelinde başlık, meta etiketler ve diğer HTML üst bilgilerini bildirimli ve programlı bir şekilde tanımlama hakkında daha ayrıntılı bilgi için `head` ContentPlaceHolder ' ı inceleyeceğiz.

Programlamanın kutlu olsun!

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Suçi Banerjee idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](creating-a-site-wide-layout-using-master-pages-cs.md)
> [İleri](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
