---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: JavaScript ekleme saldırılarını önlemek (VB) | Microsoft Docs
author: StephenWalther
description: JavaScript ekleme saldırılarını ve siteler arası betik saldırılarının sizin için oluşmasını önleyin. Bu öğreticide, Stephen Walther nasıl kolayca de kullanabilirsiniz...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: dfe09085f26c62c566649bc6f570aa25367a0f07
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624098"
---
# <a name="preventing-javascript-injection-attacks-vb"></a>JavaScript Ekleme Saldırılarını Engelleme (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

[PDF 'YI indir](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> JavaScript ekleme saldırılarını ve siteler arası betik saldırılarının sizin için oluşmasını önleyin. Bu öğreticide, Stephen Walther bu tür saldırıları nasıl kolayca erteleyerek içeriğinizi Kodlayabileceğiniz açıklanır.

Bu öğreticinin amacı, ASP.NET MVC uygulamalarınızda JavaScript ekleme saldırılarını nasıl önleyebileceğini açıklamaktır. Bu öğreticide, bir JavaScript ekleme saldırısından Web sitenizin sonlandırılabileceği iki yaklaşım ele alınmaktadır. Görüntülenen verileri kodlayarak JavaScript ekleme saldırılarını nasıl önleyeceğinizi öğrenirsiniz. Ayrıca, kabul ettiğiniz verileri kodlayarak JavaScript ekleme saldırılarını nasıl önleyeceğinizi öğreneceksiniz.

## <a name="what-is-a-javascript-injection-attack"></a>JavaScript ekleme saldırısı nedir?

Kullanıcı girişini kabul ettiğinizde ve Kullanıcı girişini yeniden görüntülerseniz, Web sitenizi JavaScript ekleme saldırılarına açık olarak açarsınız. JavaScript ekleme saldırılarına açık olan somut bir uygulamayı inceleyelim.

Müşteri geri bildirim Web sitesi oluşturduğunuzu düşünün (bkz. Şekil 1). Müşteriler web sitesini ziyaret edebilir ve ürünlerinizi kullanarak deneyimlerine ilişkin geri bildirim girebilir. Bir müşteri geri bildirimi gönderdiğinde geri bildirim sayfasında geri bildirim yeniden görüntülenir.

[![müşteri geri bildirim Web sitesi](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)

**Şekil 01**: müşteri geri bildirim Web sitesi ([tam boyutlu görüntüyü görüntülemek için tıklayın](preventing-javascript-injection-attacks-vb/_static/image3.png))

Müşteri geri bildirim Web sitesi, liste 1 ' deki `controller` kullanır. Bu `controller`, `Index()` ve `Create()`adında iki eylem içerir.

**Listeleme 1 – `HomeController.vb`**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

`Index()` yöntemi `Index` görünümünü görüntüler. Bu yöntem, veritabanındaki geri bildirimleri (LINQ to SQL bir sorgu kullanarak) alarak önceki müşteri geri bildirimini `Index` görünümüne geçirir.

`Create()` yöntemi yeni bir geri bildirim öğesi oluşturur ve veritabanına ekler. Müşterinin forma girdiği ileti, ileti parametresindeki `Create()` yöntemine geçirilir. Bir geri bildirim öğesi oluşturulur ve ileti, geri bildirim öğesinin `Message` özelliğine atanır. Geri bildirim öğesi `DataContext.SubmitChanges()` yöntemi çağrısıyla veritabanına gönderilir. Son olarak, ziyaretçi tüm geri bildirimin görüntülendiği `Index` görünümüne yeniden yönlendirilir.

`Index` görünümü liste 2 ' de yer alır.

**Listeleme 2 – `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

`Index` görünümü iki bölümden oluşur. En üstteki bölüm, gerçek müşteri geri bildirim formunu içerir. Alt bölüm Için bir içerir... Tüm önceki müşteri geri bildirim öğelerinin üzerinden döngü yapan ve her bir geri bildirim öğesi için EntryDate ve Message özelliklerini görüntüleyen her döngü.

Müşteri geri bildirimi web sitesi, basit bir Web sitesidir. Ne yazık ki, Web sitesi JavaScript ekleme saldırılarına açıktır.

Müşteri geri bildirim formuna aşağıdaki metni girdiğinizi düşünelim:

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

Bu metin, bir uyarı ileti kutusu gösteren bir JavaScript betiğini temsil eder. Birisi bu betiği geri bildirim formuna gönderdikten sonra ileti <em>Boo,!</em> Müşteri geri bildirim Web sitesini herkes ziyaret ettiğinde görüntülenir (bkz. Şekil 2).

[JavaScript ekleme ![](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)

**Şekil 02**: JavaScript ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](preventing-javascript-injection-attacks-vb/_static/image6.png))

Şimdi, JavaScript ekleme saldırılarına ilk yanıtınız Apathy olabilir. JavaScript ekleme saldırılarının yalnızca bir *savunma* saldırısı türü olduğunu düşünebilirsiniz. JavaScript ekleme saldırısı gerçekleştirerek hiç kimse gerçekten bir şey yapamadığımızı düşünebilirsiniz.

Ne yazık ki, bir korsan ekleme JavaScript 'ı bir Web sitesine kadar gerçekten, gerçekten bir şekilde gerçekleştirebilir. Bir siteler arası komut dosyası (XSS) saldırısı gerçekleştirmek için JavaScript ekleme saldırısı kullanabilirsiniz. Bir siteler arası betik saldırısında, gizli Kullanıcı bilgilerini çalmaya ve bilgileri başka bir Web sitesine göndermektir.

Örneğin, bir korsan tarayıcı tanımlama bilgilerinin değerlerini diğer kullanıcılardan çalmak için JavaScript ekleme saldırısı kullanabilir. Parolalar, kredi kartı numaraları veya sosyal güvenlik numaraları gibi hassas bilgiler tarayıcı tanımlama bilgilerinde depolanıyorsa, bir korsan bu bilgileri çalmak için JavaScript ekleme saldırısı kullanabilir. Ya da bir Kullanıcı, JavaScript saldırılarına karşı riskli bir sayfada bulunan bir form alanına gizli bilgiler girerse, korsan, form verilerini almak ve başka bir Web sitesine göndermek için eklenen JavaScript 'i kullanabilir.

*Lütfen korkmuş olun*. JavaScript ekleme saldırılarını önemli ölçüde yapın ve kullanıcılarınızın gizli bilgilerini koruyun. Sonraki iki bölümde, JavaScript ekleme saldırılarına karşı ASP.NET MVC uygulamalarınızı savunmak için kullanabileceğiniz iki teknik tartışıyoruz.

## <a name="approach-1-html-encode-in-the-view"></a>Yaklaşım #1: görünümdeki HTML kodlaması

JavaScript ekleme saldırılarını önlemek için kullanabileceğiniz kolay bir yöntem, bir görünümdeki verileri yeniden görüntülediğinizde Web sitesi kullanıcıları tarafından girilen tüm verileri HTML olarak kodlayabilmektedir. Listeleme 3 ' teki güncelleştirilmiş `Index` görünümü bu yaklaşımı izler.

**Listeleme 3 – `Index.aspx` (HTML kodlamalı)**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

Değer aşağıdaki kodla görüntülenmeden önce, `feedback.Message` değerinin HTML kodlamalı olduğuna dikkat edin:

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

Bir dizeyi HTML olarak kodlamak ne anlama geliyor? HTML 'yi bir dizeyi kodlarken, `<` ve `>` gibi tehlikeli karakterler `&lt;` ve `&gt;`gibi HTML varlık başvurularına göre değiştirilmiştir. Bu nedenle dize `<script>alert("Boo!")</script>` HTML kodlandığında, `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`dönüştürülür. Kodlanmış dize, bir tarayıcı tarafından yorumlanan bir JavaScript betiği olarak çalışmaz. Bunun yerine, Şekil 3 ' te zararsız sayfa alırsınız.

[![, beklenen JavaScript saldırısı](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)

**Şekil 03**: beklenen JavaScript saldırısı ([tam boyutlu görüntüyü görüntülemek için tıklayın](preventing-javascript-injection-attacks-vb/_static/image9.png))

Kod 3 ' teki `Index` görünümünde yalnızca `feedback.Message` değerinin kodlandığını unutmayın. `feedback.EntryDate` değeri kodlanmadı. Yalnızca bir kullanıcı tarafından girilen verileri kodlamanız gerekir. EntryDate değeri denetleyicide oluşturulduğundan, bu değeri HTML olarak kodlamak zorunda kalmazsınız.

## <a name="approach-2-html-encode-in-the-controller"></a>Yaklaşım #2: denetleyicide HTML kodlaması

Verileri bir görünümde görüntülediğinizde HTML kodlama verileri yerine verileri veritabanına göndermeden önce HTML kodlaması yapabilirsiniz. Bu ikinci yaklaşım, liste 4 ' teki `controller` söz konusu olduğunda alınır.

**Listeleme 4 – `HomeController.cs` (HTML kodlamalı)**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

Değer, `Create()` eyleminde veritabanına gönderilmeden önce Ileti değerinin HTML olarak kodlandığını unutmayın. Ileti görünümde yeniden görüntülendiğinde, Ileti HTML kodlamalı olur ve Iletiye eklenen herhangi bir JavaScript yürütülmez.

Genellikle, bu öğreticide açıklanan ilk yaklaşımı bu ikinci yaklaşımda benimsemelisiniz. Bu ikinci yaklaşımla ilgili sorun, veritabanınızdaki HTML kodlu verilerle sona erdirmek için gereklidir. Diğer bir deyişle, veritabanı verileriniz, komik görünen karakterlerle dizinlenmiş.

Bu neden yanlış? Veritabanı verilerini bir Web sayfası dışında bir şekilde görüntülemeye ihtiyacınız varsa, sorunlar olur. Örneğin, verileri artık Windows Forms bir uygulamada kolayca görüntüleyemezsiniz.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, JavaScript ekleme saldırısının aday adına yönelik olarak korsalcıdır. Bu öğretici, JavaScript ekleme saldırılarına karşı ASP.NET MVC uygulamalarınızın ertelanması için iki yaklaşımdan bahseterek, görünümdeki Kullanıcı tarafından gönderilen verileri HTML olarak kodlayabilir veya denetleyicideki Kullanıcı tarafından gönderilen verileri kodlayabilirsiniz.

> [!div class="step-by-step"]
> [Öncekini](authenticating-users-with-windows-authentication-vb.md)
