---
uid: web-forms/overview/getting-started/code-editing-in-web-forms-pages
title: Visual Studio 2013 Web Forms kod düzenlemesi ASP.NET | Microsoft Docs
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: 5344b74e-b888-479a-92bc-601a33bd61a2
msc.legacyurl: /web-forms/overview/getting-started/code-editing-in-web-forms-pages
msc.type: authoredcontent
ms.openlocfilehash: 3473ad476fbbebc58e12586334b4600f57cf17ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632750"
---
# <a name="code-editing-aspnet-web-forms-in-visual-studio-2013"></a>Visual Studio 2013’te ASP.NET Web Forms Kodunu Düzenleme

by [Erik Reitan](https://github.com/Erikre)

Birçok ASP.NET Web form sayfasında, kodu Visual Basic, C#veya başka bir dilde yazarsınız. Visual Studio 'daki kod Düzenleyicisi, hatalardan kaçınmanıza yardımcı olurken kodu hızlı bir şekilde yazmanıza yardımcı olabilir. Ayrıca, düzenleyici, yapmanız gereken iş miktarını azaltmaya yardımcı olmak için yeniden kullanılabilir kod oluşturmanız için yollar sağlar.

Bu izlenecek yol, Visual Studio kod Düzenleyicisi 'nin çeşitli özelliklerini gösterir.

Bu izlenecek yol sırasında şunları yapmayı öğreneceksiniz:

- Satır içi kodlama hatalarını düzeltin.
- Kodu yeniden düzenleme ve yeniden adlandırma.
- Değişkenleri ve nesneleri yeniden adlandırın.
- Kod parçacıkları ekleyin.

## <a name="prerequisites"></a>Önkoşullar

Bu izlenecek yolu tamamlamak için şunlar gerekir:

- Web için [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) veya [Microsoft Visual Studio Express 2013](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework otomatik olarak yüklenir. 

    > [!NOTE] 
    > 
    > Web için Microsoft Visual Studio 2013 ve Microsoft Visual Studio Express 2013, genellikle bu öğretici serisinin tamamında Visual Studio olarak adlandırılır.  
    >   
    > Visual Studio kullanıyorsanız, Bu izlenecek yol, Visual Studio 'Yu ilk kez başlattığınızda ayarların **Web geliştirme** koleksiyonunu seçtiğinizi varsayar. Daha fazla bilgi için bkz. [nasıl yapılır: Web geliştirme ortamı ayarlarını seçme](https://msdn.microsoft.com/library/ff521558.aspx).

## <a name="creating-a-web-application-project-and-a-page"></a>Web uygulaması projesi ve sayfa oluşturma

<a id="sectionToggle0"></a>

İzlenecek yolun bu bölümünde bir Web uygulaması projesi oluşturacak ve buna yeni bir sayfa ekleyeceksiniz.

### <a name="to-create-a-web-application-project"></a>Bir Web uygulaması projesi oluşturmak için

1. Microsoft Visual Studio açın.
2. **Dosya** menüsünde **Yeni proje**' yi seçin.  
    ![Dosya menüsü](code-editing-in-web-forms-pages/_static/image1.png)

    **Yeni Proje** iletişim kutusu görünür.
3. Soldaki -**Şablonlar** &gt; **Visual C#**  -&gt; **Web** şablonları grubunu seçin.
4. Orta sütundaki **ASP.NET Web uygulaması** şablonunu seçin.
5. Projeyi ***Basicwebapp*** olarak adlandırın ve **Tamam** düğmesine tıklayın.   
Yeni proje iletişim kutusunu ![](code-editing-in-web-forms-pages/_static/image2.png)
6. Sonra, **Web Forms** şablonunu seçin ve projeyi oluşturmak için **Tamam** düğmesine tıklayın.  
Yeni ASP.NET projesi iletişim kutusu ![](code-editing-in-web-forms-pages/_static/image3.png)  

    Visual Studio Web Forms şablonunu temel alan önceden oluşturulmuş işlevsellik içeren yeni bir proje oluşturur.

## <a name="creating-a-new-aspnet-web-forms-page"></a>Yeni bir ASP.NET Web Forms sayfası oluşturma

**ASP.NET Web uygulaması** proje şablonunu kullanarak yeni bir Web Forms uygulaması oluşturduğunuzda, Visual Studio *varsayılan. aspx*adlı bir ASP.NET sayfası (Web Forms sayfası) ve diğer birçok dosya ve klasör ekler. Web uygulamanızın giriş sayfası olarak *default. aspx* sayfasını kullanabilirsiniz. Bununla birlikte, Bu anlatım için yeni bir sayfa oluşturacak ve bunlarla çalışacaksınız.

### <a name="to-add-a-page-to-the-web-application"></a>Web uygulamasına bir sayfa eklemek için

1. **Çözüm Gezgini**, Web uygulaması adına (Bu öğreticide, uygulama adı **basicwebsite**) sağ tıklayın ve ardından **Yeni öğe**&gt; -**Ekle** ' ye tıklayın.   
**Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Sol taraftaki **Visual C#**  -&gt; **Web** şablonları grubunu seçin. Ardından, ortadaki listeden **Web formu** ' nu seçin ve *firstweb sayfası. aspx*olarak adlandırın.   
    ![yeni öğe Ekle iletişim kutusu](code-editing-in-web-forms-pages/_static/image4.png)
3. Projenize Web Forms sayfasını eklemek için **Ekle** ' ye tıklayın.  
 Visual Studio yeni sayfayı oluşturur ve açar.
4. Sonra, bu yeni sayfayı varsayılan başlangıç sayfası olarak ayarlayın. **Çözüm Gezgini**' de, *firstweb. aspx* adlı yeni sayfaya sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin. İlerleme durumunu test etmek için bu uygulamayı bir daha çalıştırdığınızda bu yeni sayfayı tarayıcıda otomatik olarak görürsünüz.

## <a name="correcting-inline-coding-errors"></a>Satır Içi kodlama hatalarını düzeltme

Visual Studio 'daki kod Düzenleyicisi, kod yazarken hatalardan kaçınmanıza yardımcı olur ve bir hata yaptıysanız, kod Düzenleyicisi hatayı düzeltmenize yardımcı olur. İzlenecek yolun bu bölümünde, düzenleyicide hata düzeltme özelliklerini gösteren bir kod satırı yazacaksınız.

### <a name="to-correct-simple-coding-errors-in-visual-studio"></a>Visual Studio 'da basit kodlama hatalarını düzeltmek için

1. **Tasarım** görünümünde, sayfanın **yükleme** olayı için bir işleyici oluşturmak üzere boş sayfaya çift tıklayın.   
   Olay işleyicisini yalnızca kod yazmak için bir yer olarak kullanıyorsunuz.
2. İşleyici içinde, bir hata içeren aşağıdaki satırı yazın ve **ENTER**tuşuna basın:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample1.cs)]

   **ENTER**tuşuna bastığınızda, kod Düzenleyicisi yeşil ve kırmızı alt çizgiler (genellikle &quot;, yaygın olarak çağrı&quot; satırları), sorunların bulunduğu kodun alanlarında yer verir. Yeşil alt çizgi bir uyarı gösterir. Kırmızı alt çizgi, düzeltilmesi gereken bir hata olduğunu gösterir. 

    Uyarı hakkında sizi bildiren bir araç ipucunu görmek için fare işaretçisini `myStr` üzerinde tutun. Ayrıca, hata iletisini görmek için fare işaretçinizi kırmızı alt çizginin üzerinde tutun.

    Aşağıdaki görüntüde, alt çizgileri olan kod gösterilmektedir.

    ![Tasarım görünümü 'de hoş geldiniz metni](code-editing-in-web-forms-pages/_static/image5.png "Tasarım görünümü 'de hoş geldiniz metni")  
   Satırın sonuna noktalı virgül `;` eklenerek hata düzeltilmelidir. Uyarı yalnızca `myStr` değişkenini henüz kullanmadığınız size bildirir.  

    > [!NOTE] 
    > 
    > Geçerli kod biçimlendirme ayarlarınızı, Visual Studio 'daki **araçlar** -&gt; **Seçenekler** &gt; -**yazı tipi ve renkler ' i**seçerek görüntüleyebilirsiniz.

## <a name="refactoring-and-renaming"></a>Yeniden düzenleme ve yeniden adlandırma

Yeniden düzenleme, işlevselliğini korurken ve bakımını kolaylaştırmak için kodunuzu yeniden yapılandırma ile ilgili bir yazılım metodolojisidir. Basit bir örnek, bir veritabanından veri almak için bir olay işleyicisine kod yazmanız olabilir. Sayfanızı geliştirirken, birkaç farklı işleyicilerden veriye erişmeniz gerektiğini fark edersiniz. Bu nedenle, sayfada bir veri erişim yöntemi oluşturarak ve işleyicilerde yöntemine çağrılar ekleyerek sayfanın kodunu yeniden düzenleyin.

Kod Düzenleyicisi, çeşitli yeniden düzenleme görevlerini gerçekleştirmenize yardımcı olan araçları içerir. Bu kılavuzda, iki yeniden düzenleme tekniği ile çalışacaksınız: değişkenleri yeniden adlandırma ve yöntemleri ayıklama. Diğer yeniden düzenleme seçenekleri, kapsülleme alanları, yerel değişkenleri Yöntem parametrelerine yükseltme ve yöntem parametrelerini yönetme içerir. Bu yeniden düzenleme seçeneklerinin kullanılabilirliği koddaki konuma bağlıdır.

### <a name="refactoring-code"></a>Kodu yeniden düzenleme

Ortak bir yeniden düzenleme senaryosu, bir yöntemi gibi başka bir üyenin içindeki koddan bir yöntemi oluşturmaktır (ayıklamaya). Bu, orijinal üyenin boyutunu azaltır ve ayıklanan kodu yeniden kullanılabilir hale getirir.

İzlenecek yolun bu bölümünde bazı basit kodlar yazacak ve bundan sonra bir yöntemi ayıklayacaksınız. İçin C#yeniden düzenleme desteklenir, bu nedenle programlama dili olarak kullanan C# bir sayfa oluşturacaksınız.

### <a name="to-extract-a-method-in-a-c-page"></a>C# Sayfadaki bir yöntemi ayıklamak için

1. **Tasarım** görünümüne geçin.
2. **Araç kutusunda**, **Standart** sekmesinden sayfaya bir [düğme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) denetimi sürükleyin.
3. [Tıklama](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) olayına bir işleyici oluşturmak için **düğme** denetimine çift tıklayın ve ardından aşağıdaki vurgulanmış kodu ekleyin:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample2.cs?highlight=3-16)]

   Kod bir **ArrayList** nesnesi oluşturur, değerleri ile yüklemek için bir döngü kullanır ve ardından **ArrayList** nesnesinin içeriğini göstermek için başka bir döngü kullanır.
4. Sayfayı çalıştırmak için **CTRL + F5** tuşlarına basın ve ardından aşağıdaki çıktıyı **gördüğdiğinizden** emin olmak için düğmeye tıklayın:   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample3.html)]
5. Kod düzenleyicisine dönün ve olay işleyicisindeki aşağıdaki satırları seçin.   

    [!code-html[Main](code-editing-in-web-forms-pages/samples/sample4.html)]
6. Seçimi sağ tıklatın, yeniden **Düzenle**' yi tıklatın ve sonra **yöntemi Ayıkla**' yı seçin. 

    **Ayıklama yöntemi** iletişim kutusu görüntülenir.
7. **Yeni yöntem adı** kutusuna **displayarray**yazın ve ardından **Tamam**' a tıklayın. 

    Kod Düzenleyicisi `DisplayArray`adlı yeni bir yöntem oluşturur ve döngünün ilk kullanıldığı **tıklama** işleyicisine yeni yönteme bir çağrı koyar.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample5.cs?highlight=12)]
8. **CTRL + F5** tuşlarına basarak sayfayı yeniden çalıştırın ve **düğmeye**tıklayın.

    Sayfa, daha önce olduğu gibi çalışır. `DisplayArray` yöntemi artık sayfa sınıfında herhangi bir yerden çağrı yapılabilir.

## <a name="renaming-variables"></a>Değişkenleri yeniden adlandırma

Değişkenlerle ve nesneler ile çalışırken, kodunuzda zaten başvurulduktan sonra bunları yeniden adlandırmak isteyebilirsiniz. Ancak, değişkenlerin ve nesnelerin yeniden adlandırılması, başvurulardan birini yeniden adlandırmayı kaçırırsanız kodun bozulmasına neden olabilir. Bu nedenle, yeniden adlandırmayı gerçekleştirmek için yeniden düzenlemeyi kullanabilirsiniz.

### <a name="to-use-refactoring-to-rename-a-variable"></a>Bir değişkeni yeniden adlandırmak için yeniden düzenlemeyi kullanmak için

1. **Click** olay işleyicisinde aşağıdaki satırı bulun:

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample6.cs)]
2. `alist`değişken adına sağ tıklayın, yeniden **Düzenle**' yi ve ardından **Yeniden Adlandır**' ı seçin.

    **Yeniden Adlandır** iletişim kutusu görüntülenir.
3. **Yeni ad** kutusuna **ArrayList1** yazın ve **başvuru değişikliklerinin önizlemesini görüntüle** onay kutusunun seçili olduğundan emin olun. Daha sonra, **Tamam**'a tıklayın.

    **Değişiklikleri Önizle** iletişim kutusu görünür ve yeniden adlandırmakta olduğunuz değişkene yapılan tüm başvuruları içeren bir ağaç görüntüler.
4. **Değişiklikleri Önizle** iletişim kutusunu kapatmak için **Uygula** ' ya tıklayın.

    Özellikle seçtiğiniz örneğe başvuran değişkenler yeniden adlandırılır. Ancak, aşağıdaki satırdaki `alist` değişkeninin yeniden adlandırılmadığını unutmayın.

    [!code-csharp[Main](code-editing-in-web-forms-pages/samples/sample7.cs)]

    Bu satırdaki `alist` değişkeni, yeniden adlandırdığınız değişken `alist` aynı değeri temsil etmediği için yeniden adlandırılmadı. `DisplayArray` bildiriminde `alist` değişkeni, bu yöntem için yerel bir değişkendir. Bu, değişkenleri yeniden adlandırmak için yeniden düzenleme kullanmanın, düzenleyicide yalnızca bul ve Değiştir eylemi gerçekleştirmekten farklı olduğunu gösterir; yeniden düzenleme, değişkenlerini, üzerinde çalıştığı değişkenin semantiğinin bilgileriyle yeniden adlandırır.

## <a name="inserting-snippets"></a>Kod parçacıkları ekleme

Web Forms geliştiricilerin genellikle gerçekleştirmesi gereken çok sayıda kodlama görevi olduğundan, kod Düzenleyicisi bir parçacık kitaplığı veya önceden yazılmış kod blokları sağlar. Bu kod parçacıklarını sayfanıza ekleyebilirsiniz.

Visual Studio 'da kullandığınız her dilin, kod parçacıkları ekleme gibi küçük farklılıkları vardır. Kod parçacıkları ekleme hakkında daha fazla bilgi için bkz. [Visual Basic IntelliSense kod parçacıkları](https://msdn.microsoft.com/library/18yz4be4.aspx). Görsel C#koda kod ekleme hakkında daha fazla bilgi için bkz. [ C# görsel kod parçacıkları](https://msdn.microsoft.com/library/z41h7fat.aspx).

## <a name="next-steps"></a>Sonraki Adımlar

Bu kılavuzda, kodunuzdaki hataları düzeltmek, kodu yeniden adlandırmak, değişkenleri yeniden adlandırmak ve kod parçacıklarını kodunuza eklemek için Visual Studio 2010 kod düzenleyicisinin temel özellikleri gösterilmektedir. Düzenleyicideki ek özellikler uygulama geliştirmeyi hızlı ve kolay hale getirir. Örneğin, şunları yapmak isteyebilirsiniz:

- IntelliSense seçeneklerini değiştirme, kod parçacıklarını yönetme ve kod parçacıklarını çevrimiçi olarak arama gibi IntelliSense özellikleri hakkında daha fazla bilgi edinin. Daha fazla bilgi için bkz. [IntelliSense kullanma](https://msdn.microsoft.com/library/hcw1s69b.aspx).
- Kendi kod parçacıklarını oluşturmayı öğrenin. Daha fazla bilgi için bkz. [IntelliSense kod parçacıkları oluşturma ve kullanma](https://msdn.microsoft.com/library/ms165392.aspx)
- IntelliSense kod parçacıklarının ve sorun gidermeyi özelleştirme gibi Visual Basic özgü özellikleri hakkında daha fazla bilgi edinin. Daha fazla bilgi için bkz. [Visual Basic IntelliSense kod parçacıkları](https://msdn.microsoft.com/library/18yz4be4.aspx)
- IntelliSense 'in yeniden düzenleme C#ve kod parçacıkları gibi belirli özellikleri hakkında daha fazla bilgi edinin. Daha fazla bilgi için bkz [. C# Visual IntelliSense](https://msdn.microsoft.com/library/43f44291.aspx).
