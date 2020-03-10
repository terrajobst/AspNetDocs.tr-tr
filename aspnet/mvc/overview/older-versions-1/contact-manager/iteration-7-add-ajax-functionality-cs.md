---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
title: 'Yineleme #7 – Ajax işlevselliği ekleme (C#) | Microsoft Docs'
author: microsoft
description: Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1b0809e-8909-444e-b6bb-a5cd1dea3f72
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
msc.type: authoredcontent
ms.openlocfilehash: 7c8eb3d3688674dd2c220b4bd1b5982f2610d0eb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544179"
---
# <a name="iteration-7--add-ajax-functionality-c"></a>Yineleme #7 – Ajax işlevselliği ekleme (C#)

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-7-add-ajax-functionality-cs/_static/contactmanager_7_cs1.zip)

> Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Kişi yönetimi ASP.NET MVC uygulaması (C#) oluşturma

Bu öğretici dizisinde, başlangıçtan sonuna kadar bir Iletişim yönetimi uygulaması oluşturacaksınız. Ilgili kişi Yöneticisi uygulaması, kişi listesi için kişi bilgilerini, telefon numaralarını ve e-posta adreslerini depolamanıza olanak sağlar.

Uygulamayı birden çok yineleme üzerinde oluşturacağız. Her yinelemede, uygulamayı kademeli olarak geliştirdik. Bu birden çok yineleme yaklaşımının hedefi, her bir değişikliğin nedenini anlamanıza olanak sağlamaktır.

- Yineleme #1-uygulamayı oluşturun. İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve silme (CRUD).

- Yineleme #2-uygulamanın iyi görünmesini sağlayın. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.

- Yineleme #3-form doğrulaması ekleme. Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğruladık.

- Yineleme #4-uygulamayı gevşek olarak bağlanmış hale getirin. Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. Örneğin, uygulamamız depo deseninin ve bağımlılık ekleme düzeninin kullanılması için yeniden düzenliyoruz.

- Yineleme #5-birim testleri oluşturun. Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. Denetleyicilerimizin ve doğrulama mantığımız için veri modeli Sınıflarımızı ve derleme birimi testlerini modelliyoruz.

- Yineleme #6-test odaklı geliştirme kullanın. Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede kişi grupları ekleyeceğiz.

- Yineleme #7-Ajax işlevselliği ekleme. Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.

## <a name="this-iteration"></a>Bu yineleme

Contact Manager uygulamasının bu yinelemesinde, Ajax 'un kullanımını sağlamak için uygulamamızı yeniden düzenlemelisiniz. Ajax 'tan yararlanarak uygulamamızı daha hızlı hale getirir. Sayfada yalnızca belirli bir bölgeyi güncelleştirmeniz gerektiğinde sayfanın tamamını oluşturmaktan kaçınabilirsiniz.

Dizin görünümümüzü yeniden görüntüleyeceğiz, böylece her biri yeni bir kişi grubu seçtiğinde sayfanın tamamını yeniden görüntülemeye gerek kalmaz. Bunun yerine, birisi bir kişi grubunu tıkladığında yalnızca kişi listesini güncelleştirip sayfanın geri kalanını tek başına bırakacağız.

Ayrıca, silme bağlantımız çalışma şeklini de değiştireceksiniz. Ayrı bir onay sayfası görüntülemek yerine bir JavaScript onay iletişim kutusu görüntüleriz. Bir kişiyi silmek istediğinizi onaylamanız durumunda, veritabanından kişi kaydını silmek için bir HTTP SILME işlemi gerçekleştirilir.

Ayrıca, Dizin görünümimize animasyon etkileri eklemek için jQuery 'tan faydalanacağız. Yeni kişiler listesi sunucudan getirilirken bir animasyon görüntüleriz.

Son olarak, tarayıcı geçmişini yönetmek için ASP.NET AJAX Framework desteği avantajlarından faydalanacağız. Kişi listesini güncelleştirmek için bir AJAX çağrısı gerçekleştirdiğimiz her seferinde geçmiş noktaları oluşturacağız. Bu şekilde, geri ve ileri tarayıcı düğmeleri çalışacaktır.

## <a name="why-use-ajax"></a>Ajax neden kullanılmalıdır?

Ajax kullanmanın birçok avantajı vardır. İlk olarak, bir uygulamaya Ajax işlevselliği eklendiğinde daha iyi bir kullanıcı deneyimi elde edilecek. Normal bir Web uygulamasında, sayfanın tamamı her seferinde sunucuya ve her bir eylem gerçekleştirdiğinde sunucuya geri gönderilebilir. Bir eylem gerçekleştirdiğinizde tarayıcı kilitlenir ve Kullanıcı tüm sayfa getirilme ve yeniden görüntülenene kadar beklemeniz gerekir.

Bu, masaüstü uygulaması durumunda kabul edilemez bir deneyim olacaktır. Ancak, bu durum geleneksel olarak, bir Web uygulaması durumunda bu kötü Kullanıcı deneyimiyle karşılaşacağız, ancak daha iyi yapabileceğimizi bilmiyor. Bir Web uygulamaları sınırlaması olduğunu düşündük, bu durumda, imaginations bir kısıtlamadır.

Bir AJAX uygulamasında, bir sayfayı güncellemek için Kullanıcı deneyimini bir durdurmak için gerekli kılmazsınız. Bunun yerine, sayfayı güncelleştirmek için arka planda zaman uyumsuz bir istek gerçekleştirebilirsiniz. Sayfanın bir bölümü güncelleştirilirken kullanıcıyı beklemeye zorlarsınız.

Ajax 'un avantajlarından yararlanarak uygulamanızın performansını de artırabilirsiniz. Contact Manager uygulamasının Ajax işlevselliği olmadan Şu anda nasıl çalıştığını göz önünde bulundurun. Bir kişi grubuna tıkladığınızda, tüm dizin görünümünün yeniden görüntülenmesi gerekir. Kişiler ve kişi gruplarının listesi, veritabanı sunucusundan alınmalıdır. Bu verilerin tümünün Web sunucusundan Web tarayıcısına geçirilmesi gerekir.

Uygulamamıza Ajax işlevselliği eklendikten sonra, Kullanıcı bir kişi grubuna tıkladığında sayfanın tamamını yeniden görüntülememize kaçınabilirsiniz. Artık veritabanından kişi gruplarını almak zorunda kalmıyoruz. Ayrıca tüm dizin görünümünü tel da göndermemiz gerekmez. Ajax 'tan yararlanarak, veritabanı sunucunuzun gerçekleştirmesi gereken iş miktarını azalttık ve uygulamamız için gereken ağ trafiği miktarını azalttık.

## <a name="don-t-be-afraid-of-ajax"></a>Ajax 'un Afraıd 'i olamaz

Bazı geliştiriciler, alt düzey tarayıcılarla uğraşdığı için AJAX kullanmaktan kaçınır. JavaScript desteklemeyen bir tarayıcı tarafından erişildiğinde Web uygulamalarının hala çalışır durumda olduğundan emin olmak ister. Ajax JavaScript 'e bağlı olduğundan, bazı geliştiriciler Ajax kullanmaktan kaçınır.

Ancak, Ajax 'u nasıl uygulayacağından emin değilseniz, hem üst düzey hem de alt düzey tarayıcılarla çalışan uygulamalar oluşturabilirsiniz. Contact Manager uygulamamız, JavaScript ve olmayan tarayıcıları destekleyen tarayıcılarla çalışacaktır.

JavaScript 'ı destekleyen bir tarayıcıyla Contact Manager uygulamasını kullanıyorsanız daha iyi bir kullanıcı deneyimi olacaktır. Örneğin, bir kişi grubuna tıkladığınızda, yalnızca ilgili kişileri görüntüleyen sayfanın bölgesi güncelleştirilir.

Diğer taraftan, Contact Manager uygulamasını JavaScript desteklemeyen bir tarayıcıyla (veya JavaScript devre dışı bırakılmış) kullanıyorsanız, daha az bir tercih ettiğiniz Kullanıcı deneyimi olur. Örneğin, bir kişi grubuna tıkladığınızda, ilgili kişi listesini görüntülemek için tüm dizin görünümünün tarayıcıya geri nakledilmesi gerekir.

## <a name="adding-the-required-javascript-files"></a>Gerekli JavaScript dosyaları ekleniyor

Uygulamamıza Ajax işlevselliği eklemek için üç JavaScript dosyası kullanmanız gerekir. Bu dosyaların üçü de yeni bir ASP.NET MVC uygulamasının Scripts klasörüne eklenir.

Ajax 'ı uygulamanızdaki birden çok sayfada kullanmayı planlıyorsanız, gereken JavaScript dosyalarını uygulama s görünüm ana sayfanıza dahil etmek mantıklı olur. Bu şekilde, JavaScript dosyaları uygulamanızdaki tüm sayfalara otomatik olarak dahil edilir.

Aşağıdaki JavaScript 'ı, görünüm ana sayfanızın &lt;Head&gt; etiketinin içine ekleyin:

[!code-html[Main](iteration-7-add-ajax-functionality-cs/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Dizin görünümünü Ajax kullanacak şekilde yeniden düzenleme

Bir kişi grubuna tıklamak yalnızca kişileri görüntüleyen görünümün bölgesini güncelleştirmeleri için Dizin görünümümüzü değiştirerek başlayalım. Şekil 1 ' deki kırmızı kutu, güncelleştirmek istediğimiz bölgeyi içerir.

[yalnızca kişileri güncelleştirmek ![](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)

**Şekil 01**: yalnızca kişiler güncelleştiriliyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-7-add-ajax-functionality-cs/_static/image2.png))

İlk adım, görünümün zaman uyumsuz olarak güncelleştirilmesini istediğimiz bölümünü ayrı bir kısmi (Kullanıcı denetimini görüntüle) olarak ayırmaktır. Kişiler tablosunu görüntüleyen Dizin görünümünün bölümü, liste 1 ' de kısmi tabloya taşındı.

**Listeleme 1-Views\contact\contactlist.exe**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample2.aspx)]

Liste 1 ' deki kısmen dizin görünümünden farklı bir modele sahip olduğuna dikkat edin. &lt;% @ Page%&gt; yönergesinin *Inherits* özniteliği, kısmen viewusercontrol&lt;Group&gt; sınıfından devraldığını belirtir.

Güncelleştirilmiş dizin görünümü liste 2 ' de yer alır.

**Listeleme 2-Views\contact\ındex.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample3.aspx)]

Liste 2 ' de güncelleştirilmiş görünüm hakkında dikkat etmeniz gereken iki şey vardır. İlk olarak, kısmi olarak taşınan tüm içeriğin HTML. RenderPartial () çağrısıyla değiştirildiğini fark edersiniz. İlk kişi kümesini görüntülemek için dizin görünümü istendiğinde, HTML. RenderPartial () yöntemi çağrılır.

İkincisi, iletişim gruplarını göstermek için kullanılan html. ActionLink (), bir AJAX. ActionLink () ile değiştirildiğini unutmayın. AJAX. ActionLink () aşağıdaki parametrelerle çağrılır:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample4.aspx)]

İlk parametre bağlantı için görüntülenecek metni temsil eder, ikinci parametre yol değerlerini temsil eder ve üçüncü parametre Ajax seçeneklerini temsil eder. Bu durumda, Ajax isteği tamamlandıktan sonra güncelleştirmek istediğimiz HTML &lt;div&gt; etiketini işaret etmek için UpdateTargetId Ajax seçeneğini kullanıyoruz. &lt;div&gt; etiketini yeni kişiler listesiyle güncelleştirmek istiyoruz.

Iletişim denetleyicisinin güncelleştirilmiş Index () yöntemi, Listeleme 3 ' te bulunur.

**Listeleme 3-Controllers\ContactController.cs (Dizin yöntemi)**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample5.cs)]

Güncelleştirilmiş Index () eylemi, iki işlemlerden birini koşullu olarak döndürür. Dizin () eylemi bir AJAX isteği tarafından çağrılırsa, denetleyici kısmi döndürür. Aksi takdirde, Index () eylemi bir görünümün tamamını döndürür.

Dizin () eyleminin bir AJAX isteği tarafından çağrıldığında çok fazla veri döndürmesi gerekmediğini unutmayın. Normal bir istek bağlamında, Dizin eylemi tüm kişi gruplarının ve seçilen kişi grubunun bir listesini döndürür. Ajax isteği bağlamında, Index () eylemi yalnızca seçili grubu döndürür. Ajax, veritabanı sunucunuzda daha az iş anlamına gelir.

Değiştirilen Dizin görünümümüzde, hem upLevel hem de alt düzey tarayıcıların durumunda çalışmaktadır. Bir kişi grubuna tıklarsanız ve tarayıcınız JavaScript 'i destekliyorsa, yalnızca kişi listesini içeren görünümün bölgesi güncellenir. Öte yandan, tarayıcınız JavaScript 'ı desteklemiyorsa, tüm görünüm güncellenir.

Güncelleştirilmiş Dizin görünümümüzde bir sorun vardır. Bir kişi grubuna tıkladığınızda, seçilen grup vurgulanmaz. Grup listesi, bir AJAX isteği sırasında güncelleştirilmiş bölge dışında görüntülendiğinden, doğru grup vurgulanmaz. Sonraki bölümde bu sorunu çözeceğiz.

## <a name="adding-jquery-animation-effects"></a>JQuery animasyon etkileri ekleme

Normalde, bir Web sayfasındaki bir bağlantıya tıkladığınızda, tarayıcının güncelleştirilmiş içeriği etkin bir şekilde mi getirmediğini saptamak için tarayıcı ilerleme çubuğunu kullanabilirsiniz. Diğer taraftan, bir AJAX isteği gerçekleştirirken, tarayıcı ilerleme çubuğu herhangi bir ilerleme göstermez. Bu, kullanıcıları nervous yapabilir. Tarayıcının dondurulmuş olup olmadığını nasıl anlarsınız?

Bir AJAX isteği gerçekleştirirken çalışmanın gerçekleştirildiği bir kullanıcıya gösterdiğiniz birçok yol vardır. Bir yaklaşım basit bir animasyon görüntülemektir. Örneğin, bir AJAX isteği başladığında bir bölgeyi soluklaştırarak istek tamamlandığında bölgede geçiş yapabilirsiniz.

Animasyon efektlerini oluşturmak için Microsoft ASP.NET MVC çerçevesine dahil olan jQuery kitaplığını kullanacağız. Güncelleştirilmiş dizin görünümü liste 4 ' te bulunur.

**Listeleme 4-Views\contact\ındex.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample6.aspx)]

Güncelleştirilmiş Dizin görünümünün üç yeni JavaScript işlevi içerdiğine dikkat edin. İlk iki işlev, yeni bir kişi grubuna tıkladığınızda kişiler listesinde soluklaştırmak ve soluklaştırmak için jQuery kullanır. Üçüncü işlev bir AJAX isteği bir hatayla (örneğin, ağ zaman aşımı) sonuçlanırsa bir hata mesajı görüntüler.

İlk işlev Ayrıca seçili grubu vurgulamaya de karşı sürer. Bir Class = Selected özniteliği, tıklanan öğenin üst öğesine (LI element) eklenir. Yine, jQuery doğru öğeyi seçmenizi ve CSS sınıfını eklemenizi kolaylaştırır.

Bu betikler, Ajax. ActionLink () AjaxOptions parametresinin yardımıyla grup bağlantılarına bağlanır. Güncelleştirilmiş Ajax. ActionLink () yöntem çağrısı şöyle görünür:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Tarayıcı geçmişi desteği ekleme

Normal olarak, bir sayfayı güncelleştirmek için bir bağlantıya tıkladığınızda, tarayıcı geçmişiniz güncellenir. Bu şekilde, sayfanın önceki durumuna geri dönmek için tarayıcıyı geri düğmesine tıklayabilirsiniz. Örneğin, arkadaşlar iletişim grubuna ve sonra Iş iletişim grubuna tıklarsanız, arkadaşlar iletişim grubu seçildiğinde sayfanın durumuna geri dönmek için tarayıcı geri düğmesine tıklayabilirsiniz.

Ne yazık ki, bir AJAX isteği gerçekleştirildiğinde tarayıcı geçmişi otomatik olarak güncelleştirmez. Bir kişi grubuna tıklarsanız ve eşleşen kişilerin listesi bir AJAX isteğiyle alınırsa, tarayıcı geçmişi güncellenmez. Yeni bir kişi grubu seçtikten sonra, bir kişi grubuna geri gitmek için tarayıcı geri düğmesini kullanamazsınız.

Kullanıcıların, Ajax isteklerini gerçekleştirdikten sonra tarayıcı geri düğmesini kullanabilmelerini istiyorsanız, biraz daha iş yapmanız gerekir. ASP.NET AJAX çerçevesinde yerleşik olarak bulunan tarayıcı geçmişi yönetim işlevlerinden faydalanabilirsiniz.

ASP.NET AJAX tarayıcı geçmişi, üç şey yapmanız gerekir:

1. EnableBrowserHistory özelliğini true olarak ayarlayarak tarayıcı geçmişini etkinleştirin.
2. Addgeçmişpoint () yöntemini çağırarak bir görünümün durumu değiştiğinde geçmiş noktalarını kaydedin.
3. Gezinme olayı başlatıldığında görünümün durumunu yeniden yapılandırma.

Güncelleştirilmiş dizin görünümü, Listeleme 5 ' te bulunur.

**Listeleme 5-Views\contact\ındex.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample8.aspx)]

Listeleme 5 ' te, pageInit () işlevinde tarayıcı geçmişi etkinleştirilir. PageInit () işlevi, gezinme olayı için olay işleyicisini ayarlamak üzere de kullanılır. Gezinme olayı, tarayıcı Ileri veya geri düğmesi sayfanın durumunun değişmesine neden olduğunda tetiklenir.

Bir kişi grubuna tıkladığınızda beginContactList () yöntemi çağrılır. Bu yöntem, Addgeçmişpoint () yöntemini çağırarak yeni bir geçmiş noktası oluşturur. Tıklanan kişi grubunun kimliği geçmişe eklenir.

Grup kimliği, kişi grubu bağlantısındaki bir bir bir özniteliği veritabanından alınır. Bağlantı, Ajax. ActionLink () için aşağıdaki çağrı ile işlenir.

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample9.aspx)]

AJAX. ActionLink () öğesine geçirilen son parametre, bağlantıya GroupID adlı bir bir öznitelik ekler (XHTML uyumluluğu için küçük harf).

Kullanıcı tarayıcıyı geri veya Ileri düğmesine geldiğinde, gezinme olayı tetiklenir ve gezin () yöntemi çağrılır. Bu yöntem, sayfada görüntülenen kişileri, gezinme yöntemine geçirilen tarayıcı geçmişi noktasına karşılık gelen sayfanın durumuyla eşleşecek şekilde güncelleştirir.

## <a name="performing-ajax-deletes"></a>Ajax silmeleri gerçekleştirme

Şu anda, bir kişiyi silmek için Sil bağlantısına tıkladıktan sonra silme onayı sayfasında görüntülenen Sil düğmesine Tıklamamız gerekir (bkz. Şekil 2). Bu, bir veritabanı kaydını silme gibi çok sayıda sayfa isteği gibi görünüyor.

[silme onayı sayfasını ![](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)

**Şekil 02**: silme onayı sayfası ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-7-add-ajax-functionality-cs/_static/image4.png))

Silme onayı sayfasını atlamak ve bir kişiyi doğrudan dizin görünümünden silmek önemlidir. Bu yaklaşımın önüne alınması uygulamanızı güvenlik delikleri üzerinde açtığından bu geçicinizi kullanmaktan kaçının. Genel olarak, Web uygulamanızın durumunu değiştiren bir eylem çağırırken HTTP GET işlemi gerçekleştirmek istemezsiniz. Silme işlemi gerçekleştirirken bir HTTP POST işlemini veya daha iyi bir HTTP SILME işlemini gerçekleştirmek istersiniz.

Sil bağlantısı, ContactList bölümünde yer alır. ContactList bölümünün güncelleştirilmiş bir sürümü listeleme 6 ' da bulunur.

**Liste 6-Views\contact\contactlist.exe**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample10.aspx)]

Delete bağlantısı, Ajax. ımageactionlink () yöntemine aşağıdaki çağrı ile işlenir:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample11.aspx)]

> [!NOTE] 
> 
> AJAX. ımageactionlink (), ASP.NET MVC çerçevesinin standart bir parçası değildir. AJAX. ımageactionlink (), Contact Manager projesine dahil olan özel bir yardımcı yöntemleridir.

AjaxOptions parametresinin iki özelliği vardır. İlk olarak, Onayla özelliği bir açılan JavaScript onay iletişim kutusunu göstermek için kullanılır. İkinci olarak, HttpMethod özelliği bir HTTP SILME işlemi gerçekleştirmek için kullanılır.

7\. liste, kişi denetleyicisine eklenmiş yeni bir AjaxDelete () eylemi içerir.

**7-Controllers\ContactController.cs (AjaxDelete) listeleniyor**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample12.cs)]

AjaxDelete () eylemi bir AcceptVerbs özniteliğiyle donatılmalıdır. Bu öznitelik, HTTP SILME işlemi dışında herhangi bir HTTP işlemi dışında eylemin çağrılmasını engeller. Özellikle, bu eylemi bir HTTP GET ile çağıramazsınız.

Veritabanı kaydını sildikten sonra, silinen kaydı içermeyen kişilerin güncelleştirilmiş listesini görüntüetmeniz gerekir. AjaxDelete () yöntemi, ContactList kısmını ve güncelleştirilmiş kişi listesini döndürür.

## <a name="summary"></a>Özet

Bu yinelemede, Contact Manager uygulamanıza Ajax işlevselliği ekledik. Uygulamamızın yanıt hızını ve performansını geliştirmek için AJAX kullandık.

İlk olarak, bir kişi grubuna tıklanması görünümün tamamını güncelleştirmemesi için dizin görünümüne yeniden düzenlenmiş. Bunun yerine, bir kişi grubuna tıkladığınızda yalnızca kişiler listesi güncelleştirilir.

Daha sonra, kişiler listesinde belirme ve belirme için jQuery animasyon efektlerini kullandık. Bir AJAX uygulamasına animasyon eklemek, uygulamanın kullanıcılarına bir tarayıcı ilerleme çubuğunun eşdeğerini sağlamak için kullanılabilir.

Ayrıca, Ajax uygulamamıza tarayıcı geçmişi desteği ekledik. Kullanıcıların, Dizin görünümünün durumunu değiştirmek için tarayıcıyı geri ve Ileri düğmelerine tıklamesini etkinleştirdik.

Son olarak, HTTP SILME işlemlerini destekleyen bir silme bağlantısı oluşturduk. Ajax silmeleri gerçekleştirerek, kullanıcıların ek silme onayı sayfası istememesini gerektirmeden veritabanı kayıtlarını silmesini olanaklı kıldık.

> [!div class="step-by-step"]
> [Önceki](iteration-6-use-test-driven-development-cs.md)
> [İleri](iteration-1-create-the-application-vb.md)
