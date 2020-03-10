---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: ASP.NET Web Pages (Razor) sitelerinde HTML formlarıyla çalışma | Microsoft Docs
author: Rick-Anderson
description: Form, metin kutuları, onay kutuları, radyo düğmeleri ve aşağı açılan listeler gibi kullanıcı girişi denetimleri yerleştirdiğiniz bir HTML belgesi bölümüdür. Biçimleri kullanıyorsunuz...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639708"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) sitelerinde HTML formlarıyla çalışma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede bir ASP.NET Web Pages (Razor) Web sitesinde çalışırken bir HTML formunun (metin kutuları ve düğmeler ile) nasıl işlenmesi açıklanmaktadır.
> 
> **Şunları öğreneceksiniz:** 
> 
> - HTML formu oluşturma.
> - Formdan Kullanıcı girişini okuma.
> - Kullanıcı girişini doğrulama.
> - Sayfa gönderildikten sonra form değerlerini geri yükleme.
> 
> Makalesinde sunulan ASP.NET programlama kavramları şunlardır:
> 
> - `Request` nesnesi.
> - Giriş doğrulaması.
> - HTML kodlaması.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 3
>   
> 
> Bu öğretici, ASP.NET Web Pages 2 ile de kullanılabilir.

## <a name="creating-a-simple-html-form"></a>Basit HTML formu oluşturma

1. Yeni bir Web sitesi oluşturun.
2. Kök klasörde, *form. cshtml* adlı bir Web sayfası oluşturun ve aşağıdaki biçimlendirmeyi girin:

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. Sayfayı tarayıcınızda başlatın. (WebMatrix 'te **dosyalar** çalışma alanında, dosyaya sağ tıklayın ve ardından **tarayıcıda Başlat**' ı seçin.) Üç giriş alanı ve **Gönder** düğmesi içeren basit bir form görüntülenir.

    ![Üç metin kutusu içeren bir formun ekran görüntüsü.](4-working-with-forms/_static/image1.png)

    Bu noktada **Gönder** düğmesine tıklarsanız hiçbir şey olmaz. Formu faydalı hale getirmek için sunucuda çalışacak bir kod eklemeniz gerekir.

## <a name="reading-user-input-from-the-form"></a>Formdan Kullanıcı girişi okunuyor

Formu işlemek için, gönderilen alan değerlerini okuyan ve bunlarla bir şey yapan kodu eklersiniz. Bu yordam, alanların nasıl okunacağını ve Kullanıcı girişinin sayfada nasıl görüntüleneceğini gösterir. (Bir üretim uygulamasında genellikle Kullanıcı girişiyle ilgili daha ilgi çekici şeyler olursunuz. Bu, veritabanlarıyla çalışma hakkında makalesinde yapılır.)

1. *Form. cshtml* dosyasının en üstünde aşağıdaki kodu girin:

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    Kullanıcı sayfayı ilk kez istediğinde yalnızca boş form görüntülenir. Kullanıcı (sizin olur) formu doldurur ve ardından **Gönder**' i tıklamalıdır. Bu, Kullanıcı girişini sunucuya gönderir (gönderir). Varsayılan olarak, istek aynı sayfaya (yani, *form. cshtml*) gider.

    Sayfayı bu kez gönderdiğinizde, girdiğiniz değerler formun hemen üzerinde görüntülenir:

    ![Sayfada girdiğiniz değerleri gösteren ekran görüntüsü.](4-working-with-forms/_static/image2.png)

    Sayfanın koduna bakın. İlk olarak, bir kullanıcının **Gönder** düğmesine tıklamadığı bir, sayfanın mi nakledildiğini &#8212; öğrenmek için `IsPost` yöntemini kullanırsınız. Bu bir gönderise, `IsPost` true döndürür. Bu, ASP.NET Web sayfalarında bir ilk istek (bir GET isteği) veya geri gönderme (POST isteği) ile çalışıp çalışmadığını belirlemede standart bir yoldur. (GET ve POST hakkında daha fazla bilgi için, [Razor söz dizimini kullanarak ASP.NET Web sayfaları programlamasına giriş](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)bölümünde "http get ve post ve ıspost özelliği" başlıklı kenar çubuğuna bakın.)

    Ardından, kullanıcının `Request.Form` nesnesinden doldurduğu değerleri alır ve bunları daha sonra değişkenlere yerleştirebilirsiniz. `Request.Form` nesnesi, her biri bir anahtarla tanımlanan sayfayla gönderilen tüm değerleri içerir. Anahtar, okumak istediğiniz form alanının `name` özniteliğine eşdeğerdir. Örneğin, `companyname` alanını (metin kutusu) okumak için `Request.Form["companyname"]`kullanırsınız.

    Form değerleri, `Request.Form` nesnesinde dizeler olarak depolanır. Bu nedenle, bir sayı veya tarih ya da başka bir tür olarak bir değerle çalışmanız gerektiğinde, bir dizeden bu türe dönüştürmeniz gerekir. Örnekte, `Request.Form` `AsInt` yöntemi, çalışanlar alanının (bir çalışan sayısı içeren) değerini bir tamsayıya dönüştürmek için kullanılır.
2. Sayfayı tarayıcınızda başlatın, form alanlarını doldurup **Gönder**' e tıklayın. Sayfada girdiğiniz değerler görüntülenir.

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>Görünüm ve güvenlik için HTML kodlaması
> 
> HTML 'de `<`, `>`ve `&`gibi karakterlerin özel kullanımları vardır. Bu özel karakterler beklenmediği yerlerde görünürse, Web sayfanızın görünümü ve işlevselliği için bir görünüm verebilir. Örneğin, tarayıcı, `<b>` veya `<input ...>`gibi bir HTML öğesinin başlangıcına kadar `<` karakterini (bir boşluk değilse) yorumlar. Tarayıcı öğeyi tanımıyorsa, tekrar tanıdığı bir şeye ulaşana kadar `<` ile başlayan dizeyi atar. Kuşkusuz, bu, sayfada bazı tuhaf işlemeye neden olabilir.
> 
> HTML kodlaması, bu ayrılmış karakterlerin, tarayıcıların doğru sembol olarak yorumlayacağı bir kodla yerini alır. Örneğin, `<` karakteri `&lt;` ile, `>` karakteri ise `&gt;`ile değiştirilmiştir. Tarayıcı, bu değiştirme dizelerini görmek istediğiniz karakterler olarak işler.
> 
> Bir kullanıcıdan aldığınız dizeleri (giriş) görüntülediğinizde HTML kodlaması kullanmak iyi bir fikirdir. Bunu yapmazsanız, bir Kullanıcı, Web sayfanızı kötü amaçlı bir betik çalıştırmak veya site güvenliğini karşılayan başka bir şey yapmak ya da yalnızca sizin tasarladığınız şeyi yapmak için deneyebilir. (Kullanıcı girişi gerçekleştirmezseniz, bunu bir yerde depolarsanız ve daha &#8212; sonra Örneğin, bir blog yorumu, Kullanıcı incelemesi veya bunun gibi bir şey gibi), bu özellikle önemlidir.
> 
> Bu sorunları önlemeye yardımcı olmak için, ASP.NET Web sayfaları otomatik olarak HTML-kodlarınızdan çıktı aldığınız tüm metin içeriğini kodlar. Örneğin, `@MyVar`gibi kodu kullanarak bir değişkenin veya ifadenin içeriğini görüntülediğinizde, ASP.NET Web sayfaları çıktıyı otomatik olarak kodlar.

## <a name="validating-user-input"></a>Kullanıcı girişini doğrulama

Kullanıcılar hata yapar. Bu kullanıcılardan bir alanı doldurmasını ve bunları unutmasını veya çalışanların sayısını girmesini istediğinizi ve bunun yerine bir ad yazmalarını isteyebilirsiniz. Bir formun işlem yapılmadan önce doğru şekilde doldurulduğundan emin olmak için, kullanıcının girişini doğrularsınız.

Bu yordamda, kullanıcının onları boş bırakmaması için üç form alanının tümünün nasıl doğrulanacağı gösterilmektedir. Ayrıca, çalışan sayısı değerinin bir sayı olup olmadığını kontrol edersiniz. Hatalar varsa, kullanıcıya hangi değerlerin doğrulamadan geçemeyeceğini belirten bir hata iletisi görüntülenir.

1. *Form. cshtml* dosyasında, ilk kod bloğunu aşağıdaki kodla değiştirin: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    Kullanıcı girişini doğrulamak için `Validation` Yardımcısı ' nı kullanırsınız. Gerekli alanları `Validation.RequireField`çağırarak kaydedersiniz. `Validation.Add` çağırarak ve doğrulanacak alanı ve gerçekleştirilecek doğrulama türünü girerek diğer doğrulama türlerini kaydedersiniz.

    Sayfa çalıştırıldığında, ASP.NET tüm doğrulama yapar. `Validation.IsValid`çağırarak sonuçları kontrol edebilirsiniz, her şey başarılı olursa true, herhangi bir alan doğrulamada başarısız olursa false döndürür. Genellikle, Kullanıcı girişinde herhangi bir işlem gerçekleştirmeden önce `Validation.IsValid` çağırın.
2. Aşağıdaki gibi `Html.ValidationMessage` yöntemine üç çağrı ekleyerek `<body>` öğesini güncelleştirin:

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    Doğrulama hata iletilerini göstermek için HTML 'yi çağırabilirsiniz.`ValidationMessage` ve iletiyi istediğiniz alanın adı olarak geçirin.
3. Sayfayı çalıştırın. Alanları boş bırakın ve **Gönder**' e tıklayın. Hata iletilerini görürsünüz.

    ![Kullanıcı girişi doğrulamayı geçemediğinde görüntülenen hata iletilerini gösteren ekran görüntüsü.](4-working-with-forms/_static/image3.jpg)
4. **Çalışan sayısı** alanına bir dize (örneğin, "abc") ekleyin ve yeniden **Gönder** ' e tıklayın. Bu kez, dizenin doğru biçimde olmadığını belirten bir hata görürsünüz, yani bir tamsayı.

    ![Kullanıcılar çalışanlar alanı için bir dize girirse görüntülenen hata iletilerini gösteren ekran görüntüsü.](4-working-with-forms/_static/image4.jpg)

ASP.NET Web sayfaları, kullanıcıların tarayıcıda anında geri bildirim alması için istemci betiği kullanılarak otomatik olarak doğrulama gerçekleştirme özelliği de dahil olmak üzere Kullanıcı girişini doğrulamak için daha fazla seçenek sunar. Daha fazla bilgi için daha sonra [ek kaynaklar](#Additional_Resources) bölümüne bakın.

## <a name="restoring-form-values-after-postbacks"></a>Geri göndermeler sonrasında form değerlerini geri yükleme

Önceki bölümde yer alan sayfayı sınadıktan sonra, girdiğiniz her şey (yalnızca geçersiz veriler değil) geçmiş olduğunu fark etmiş olabilirsiniz ve tüm alanlar için değerleri yeniden girmeniz gerekiyordu. Bu önemli bir noktayı gösterir: bir sayfa gönderdiğinizde, işlem tamamlandıktan sonra sayfayı yeniden oluşturduktan sonra sayfa sıfırdan yeniden oluşturulur. Gördüğünüz gibi, bu, gönderildiği sırada sayfadaki tüm değerlerin kaybedildiği anlamına gelir.

Ancak bunu kolayca çözebilirsiniz. Gönderilen değerlere erişiminiz vardır (`Request.Form` nesnesinde, sayfa işlendiğinde bu değerleri form alanlarına geri doldurabilirsiniz.

1. *Form. cshtml* dosyasında, `value` özniteliğini kullanarak `<input>` öğelerinin `value` özniteliklerini değiştirin.: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    `<input>` öğelerinin `value` özniteliği `Request.Form` nesnesinden alan değerini dinamik olarak okumak üzere ayarlanmıştır. Sayfa istendiğinde ilk kez `Request.Form` nesnesindeki değerler boştur. Bu, formun boş olduğu şekilde bu şekilde iyidir.
2. Sayfayı tarayıcınızda başlatın, form alanlarını doldurup boş bırakın ve **Gönder**' e tıklayın. Gönderilen değerleri gösteren bir sayfa görüntülenir.

    ![Formlar-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

- [Web kullanıcılarından giriş almanın 1.001 yolu](https://msdn.microsoft.com/library/ms971057.aspx)
- [Formları kullanma ve Kullanıcı girişini Işleme](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [ASP.NET Web Sayfaları Sitelerinde Kullanıcı Girişini Doğrulama](https://go.microsoft.com/fwlink/?LinkId=253002)
- [HTML formlarında otomatik tamamlamayı kullanma](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
