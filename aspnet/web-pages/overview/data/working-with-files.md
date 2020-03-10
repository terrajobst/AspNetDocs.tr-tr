---
uid: web-pages/overview/data/working-with-files
title: Bir ASP.NET Web Pages (Razor) sitesindeki dosyalarla çalışma | Microsoft Docs
author: Rick-Anderson
description: Bu bölümde, dosyaları okuma, yazma, ekleme, silme ve karşıya yükleme işlemleri açıklanmaktadır.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: eee916e4-ba4c-439a-a24e-68df7d45a569
msc.legacyurl: /web-pages/overview/data/working-with-files
msc.type: authoredcontent
ms.openlocfilehash: 684c47a8a8480dc040e5144144577c94c35d39e5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642368"
---
# <a name="working-with-files-in-an-aspnet-web-pages-razor-site"></a>Bir ASP.NET Web Pages (Razor) sitesinde dosyalarla çalışma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu makalede, bir ASP.NET Web Pages (Razor) sitesinde dosyaları okuma, yazma, ekleme, silme ve karşıya yükleme işlemleri açıklanmaktadır.
> 
> > [!NOTE]
> > Görüntüleri karşıya yüklemek ve işlemek istiyorsanız (örneğin, bunları çevirin veya yeniden boyutlandırın), bkz. [ASP.NET Web Pages sitesindeki görüntülerle çalışma](/aspnet/web-pages/overview/ui-layouts-and-themes/9-working-with-images).
> 
> 
> **Şunları öğreneceksiniz:** 
> 
> - Metin dosyası oluşturma ve verileri yazma.
> - Mevcut bir dosyaya veri ekleme.
> - Dosya okuma ve dosyadan görüntüleme.
> - Bir Web sitesinden dosyaları silme.
> - Kullanıcıların bir dosya veya birden çok dosyayı karşıya yüklemesine izin verin.
> 
> Makalesinde sunulan ASP.NET programlama özellikleri şunlardır:
> 
> - Dosyaları yönetmek için bir yol sağlayan `File` nesnesi.
> - `FileUpload` Yardımcısı.
> - Yolu ve dosya adlarını değiştirmenize olanak sağlayan yöntemler sağlayan `Path` nesnesi.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - ASP.NET Web sayfaları (Razor) 2
> - WebMatrix 2
>   
> 
> Bu öğretici WebMatrix 3 ile de kullanılabilir.

<a id="Creating_a_Text_File"></a>
## <a name="creating-a-text-file-and-writing-data-to-it"></a>Metin dosyası oluşturma ve verileri yazma

Web sitenizde bir veritabanı kullanmanın yanı sıra dosyalarla çalışabilirsiniz. Örneğin, site verilerini depolamak için basit bir yol olarak metin dosyalarını kullanabilirsiniz. (Verileri depolamak için kullanılan bir metin dosyası bazen *düz dosya*olarak adlandırılır.) Metin dosyaları *. txt*, *. xml*veya *. csv* (virgülle ayrılmış değerler) gibi farklı biçimlerde olabilir.

Verileri bir metin dosyasında depolamak istiyorsanız, oluşturulacak dosyayı ve dosyaya yazılacak verileri belirtmek için `File.WriteAllText` yöntemini kullanabilirsiniz. Bu yordamda, üç `input` öğesi (ad, son ad ve e-posta adresi) ve **Gönder** düğmesi içeren basit bir form içeren bir sayfa oluşturacaksınız. Kullanıcı formu gönderdiğinde, kullanıcının girişini bir metin dosyasında depolayacaksınız.

1. Zaten mevcut değilse, *uygulama\_veri*adlı yeni bir klasör oluşturun.
2. Web sitenizin kökünde, *UserData. cshtml*adlı yeni bir dosya oluşturun.
3. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](working-with-files/samples/sample1.cshtml)]

    HTML biçimlendirmesi, formu üç metin kutusu ile oluşturur. Kodda, işleme başlamadan önce sayfanın gönderilip gönderilmediğini anlamak için `IsPost` özelliğini kullanırsınız.

    İlk görev, Kullanıcı girişini almak ve bunları değişkenlere atayacaktır. Kod daha sonra ayrı değişkenlerin değerlerini virgülle ayrılmış tek bir dizede birleştirir, bu daha sonra farklı bir değişkende depolanır. Oluşturmakta olduğunuz büyük dizeye tam olarak bir virgül Katıştırırken, virgül ayırıcısının tırnak işaretleri (",") içinde bulunan bir dize olduğunu unutmayın. Birlikte birleştirdiğiniz verilerin sonunda `Environment.NewLine`eklersiniz. Bu bir satır sonu ekler (yeni satır karakteri). Bu birleştirme ile oluşturduğunuz şey şöyle görünen bir dizedir:

    [!code-css[Main](working-with-files/samples/sample2.css)]

    (Sonunda görünmez bir satır sonuyla birlikte.)

    Ardından, verilerin depolandığı dosyanın konumunu ve adını içeren bir değişken (`dataFile`) oluşturursunuz. Konumun ayarlanması için bazı özel işlem yapılması gerekir. Web sitelerinde, Web sunucusundaki dosyalar için *C:\folder\dosya.txt* gibi mutlak yollara kodda başvurmak kötü bir uygulamadır. Bir Web sitesi taşınırsa, mutlak bir yol yanlış olur. Üstelik, barındırılan bir site için (kendi bilgisayarınızda aksine), kodu yazarken doğru yolun ne olduğunu de bilemezsiniz.

    Ancak bazen (Şimdi de bir dosya yazmak için), tüm yola ihtiyacınız vardır. Çözüm, `Server` nesnesinin `MapPath` yöntemini kullanmaktır. Bu, Web sitenizin tüm yolunu döndürür. Web sitesi kökünün yolunu almak için, `~` işlecine (sitenin sanal kökünü yeniden eklemek için) `MapPath`. (Bu alt klasörün yolunu almak için *~/App\_Data/* gibi bir alt klasör adı da geçirebilirsiniz.) Daha sonra, bir bütün yol oluşturmak için yöntemin döndürdüğü her şeyi üzerine ek bilgileri birleştirebilirsiniz. Bu örnekte, bir dosya adı eklersiniz. ( [Razor söz dizimini kullanarak ASP.NET Web sayfaları programlamasına giriş](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths)bölümünde dosya ve klasör yollarıyla çalışma hakkında daha fazla bilgi edinebilirsiniz.)

    Dosya, *App\_veri* klasörüne kaydedilir. Bu klasör, [ASP.NET Web sayfaları sitelerinde bir veritabanıyla çalışmaya giriş](https://go.microsoft.com/fwlink/?LinkId=195209)bölümünde açıklandığı gibi, ASP.NET içinde veri dosyalarını depolamak için kullanılan özel bir klasördür.

    `File` nesnesinin `WriteAllText` yöntemi, verileri dosyaya yazar. Bu yöntem iki parametre alır: yazılacak dosyanın adı (yol ile) ve yazılacak gerçek veriler. İlk parametrenin adının ön ek olarak bir `@` karakteri olduğuna dikkat edin. Bu, tam bir dize sabit değeri ASP.NET ve "/" gibi karakterlerin özel yollarla yorumlanmaması gerektiğini söyler. (Daha fazla bilgi için bkz. [Razor sözdizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkId=195205#ID_WorkingWithFileAndFolderPaths).)

    > [!NOTE]
    > Kodunuzun *App\_Data* klasöründeki dosyaları kaydetmesi için, uygulamanın bu klasör için okuma-yazma izinlerine sahip olması gerekir. Geliştirme bilgisayarınızda bu genellikle bir sorun değildir. Ancak, sitenizi bir barındırma sağlayıcısının Web sunucusunda yayımladığınızda, bu izinleri açıkça ayarlamanız gerekebilir. Bu kodu bir barındırma sağlayıcısının sunucusunda çalıştırırsanız ve hata alırsanız, bu izinleri nasıl ayarlayacağınızı öğrenmek için barındırma sağlayıcısına başvurun.

- Sayfayı bir tarayıcıda çalıştırın. 

    ![](working-with-files/_static/image1.jpg)
- Alanlara değerler girin ve ardından **Gönder**' e tıklayın.
- Tarayıcıyı kapatın.
- Projeye dönün ve görünümü yenileyin.
- *Data. txt* dosyasını açın. Formda gönderdiğiniz veriler dosyasında bulunur. 

    ![görüntüyle](working-with-files/_static/image2.jpg)
- *Data. txt* dosyasını kapatın.

<a id="Appending_Data"></a>
## <a name="appending-data-to-an-existing-file"></a>Mevcut bir dosyaya veri ekleme

Önceki örnekte, içinde yalnızca bir veri parçası olan bir metin dosyası oluşturmak için `WriteAllText` kullandınız. Yöntemi yeniden çağırır ve aynı dosya adına geçirirseniz, var olan dosyanın tamamen üzerine yazılır. Bununla birlikte, bir dosyayı oluşturduktan sonra genellikle dosyanın sonuna yeni veri eklemek istersiniz. Bunu, `File` nesnesinin `AppendAllText` yöntemini kullanarak yapabilirsiniz.

1. Web sitesinde, *UserData. cshtml* dosyasının bir kopyasını oluşturun ve Copy *userdatamultiple. cshtml*olarak adlandırın.
2. Kod bloğunu, açma `<!DOCTYPE html>` etiketinden önce aşağıdaki kod bloğu ile değiştirin: 

    [!code-cshtml[Main](working-with-files/samples/sample3.cshtml)]

    Bu kodun önceki örnekteki bir değişikliği vardır. `WriteAllText`kullanmak yerine `the AppendAllText` yöntemini kullanır. Yöntemler benzerdir, çünkü `AppendAllText` verileri dosyanın sonuna ekler. `WriteAllText`gibi, zaten yoksa, `AppendAllText` dosyayı oluşturur.
3. Sayfayı bir tarayıcıda çalıştırın.
4. Alanlar için değerler girin ve ardından **Gönder**' e tıklayın.
5. Daha fazla veri ekleyin ve formu yeniden gönderebilirsiniz.
6. Projenize dönün, proje klasörüne sağ tıklayın ve ardından **Yenile**' ye tıklayın.
7. *Data. txt* dosyasını açın. Şimdi girdiğiniz yeni verileri içerir. 

    ![görüntüyle](working-with-files/_static/image3.jpg)

<a id="Reading_and_Displaying_Data"></a>
## <a name="reading-and-displaying-data-from-a-file"></a>Dosyadaki verileri okuma ve görüntüleme

Bir metin dosyasına veri yazmanıza gerek olmasa bile, bazen verileri bir dosyadan okumanız gerekebilir. Bunu yapmak için `File` nesnesini yeniden kullanabilirsiniz. Her satırı ayrı ayrı okumak için `File` nesnesini kullanabilirsiniz (satır sonlarına göre) veya birbirinden ayrıldıklarında bağımsız bir öğeyi okuyabilirsiniz.

Bu yordam, önceki örnekte oluşturduğunuz verilerin nasıl okunacağını ve görüntüleneceğini gösterir.

1. Web sitenizin kökünde *displayData. cshtml*adlı yeni bir dosya oluşturun.
2. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](working-with-files/samples/sample4.cshtml)]

    Kod, önceki örnekte oluşturduğunuz dosyayı, bu yöntem çağrısını kullanarak `userData`adlı bir değişkene okuyarak başlar:

    [!code-css[Main](working-with-files/samples/sample5.css)]

    Bunu yapmak için kod `if` deyimin içindedir. Bir dosyayı okumak istediğinizde, dosyanın kullanılabilir olup olmadığını anlamak için `File.Exists` metodunu kullanmak iyi bir fikirdir. Kod ayrıca dosyanın boş olup olmadığını denetler.

    Sayfanın gövdesi, diğeri içinde iç içe olan iki `foreach` döngüsü içerir. Dış `foreach` döngüsü, veri dosyasından bir seferde bir satır alır. Bu durumda, satırlar dosyadaki &#8212; satır sonları tarafından tanımlanır, her veri öğesi kendi satırlardır. Dış döngü sıralı bir liste içinde (`<ol>` öğesi) yeni bir öğe (`<li>` öğesi) oluşturur.

    İç döngü, her bir veri satırını bir sınırlayıcı olarak virgül kullanarak öğelere (alanlar) böler. (Önceki örneğe bağlı olarak, her bir satırın adı, son adı ve e &#8212; -posta adresi, her biri bir virgülle ayrılmış olarak üç alan içerdiği anlamına gelir.) İç döngü Ayrıca bir `<ul>` listesi oluşturur ve veri satırındaki her alan için bir liste öğesi görüntüler.

    Kod, iki veri türü, bir dizi ve `char` veri türü kullanmayı gösterir. `File.ReadAllLines` yöntemi verileri dizi olarak döndürdüğünden dizi gereklidir. `char` veri türü gereklidir çünkü `Split` yöntemi her bir öğenin `char`türünde olduğu bir `array` döndürür. (Diziler hakkında bilgi için bkz. [Razor sözdizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkId=202890#ID_CollectionsAndObjects).)
3. Sayfayı bir tarayıcıda çalıştırın. Önceki örnekler için girdiğiniz veriler görüntülenir. 

    ![görüntüyle](working-with-files/_static/image4.jpg)

> [!TIP] 
> 
> **Microsoft Excel virgülle ayrılmış bir dosyadan veri görüntüleme**
> 
> Bir elektronik tabloda bulunan verileri virgülle ayrılmış dosya ( *. csv* dosyası) olarak kaydetmek Için Microsoft Excel 'i kullanabilirsiniz. Bunu yaptığınızda, dosya Excel biçiminde değil, düz metin olarak kaydedilir. Elektronik tablodaki her satır metin dosyasında bir satır sonuyla ayrılır ve her bir veri öğesi virgülle ayrılır. Kodunuzda veri dosyasının adını değiştirerek, Excel virgülle ayrılmış bir dosyayı okumak için önceki örnekte gösterilen kodu kullanabilirsiniz.

<a id="Deleting_Files"></a>
## <a name="deleting-files"></a>Dosyalar siliniyor

Web sitenizdeki dosyaları silmek için `File.Delete` yöntemini kullanabilirsiniz. Bu yordamda, kullanıcıların dosyanın adını öğrendikleri bir *görüntü klasöründen bir görüntüyü (* *. jpg* dosyası) silmesine nasıl izin verilmektedir.

> [!NOTE] 
> 
> **Önemli** Bir üretim web sitesinde, genellikle verilerde değişiklik yapmasına izin verilen kişileri kısıtlayabilirsiniz. Üyeliği ayarlama ve kullanıcılara sitede görevler gerçekleştirme izni verme yolları hakkında bilgi için bkz. [ASP.NET Web Pages sitesine güvenlik ve üyelik ekleme](https://go.microsoft.com/fwlink/?LinkId=202904).

1. Web sitesinde *görüntüler*adlı bir alt klasör oluşturun.
2. Bir veya daha fazla *. jpg* dosyasını *görüntüler* klasörüne kopyalayın.
3. Web sitesinin kökünde, *Filedelete. cshtml*adlı yeni bir dosya oluşturun.
4. Var olan içeriği aşağıdaki ile değiştirin: 

    [!code-cshtml[Main](working-with-files/samples/sample6.cshtml)]

    Bu sayfa, kullanıcıların bir resim dosyası adını girebilecekleri bir form içerir. *. Jpg* dosya adı uzantısını girmez; dosya adını bu şekilde kısıtlayarak, kullanıcıların sitenizdeki rastgele dosyaları silmesini engeller.

    Kod, kullanıcının girdiği dosya adını okur ve sonra bir bütün yolu oluşturur. Bu yolu oluşturmak için, kod geçerli Web sitesi yolunu (`Server.MapPath` yöntemi tarafından döndürülen), *görüntüler* klasörünün adını, kullanıcının sağladıysa ve ". jpg" değerini sabit bir dize olarak kullanır.

    Dosyayı silmek için kod `File.Delete` yöntemini çağırarak, yeni oluşturduğunuz tam yolu geçirerek kodu çağırır. Biçimlendirmenin sonunda, kod dosyanın silindiğini belirten bir onay iletisi görüntüler.
5. Sayfayı bir tarayıcıda çalıştırın. 

    ![görüntüyle](working-with-files/_static/image5.jpg)
6. Silinecek dosyanın adını girin ve ardından **Gönder**' e tıklayın. Dosya silinmişse, dosyanın adı sayfanın altında görüntülenir.

<a id="Letting_Users_Upload_a_File"></a>
## <a name="letting-users-upload-a-file"></a>Kullanıcıların bir dosyayı karşıya yüklemesine izin verme

`FileUpload` yardımcı, kullanıcıların Web sitenize dosya yüklemesine olanak tanır. Aşağıdaki yordamda, kullanıcıların tek bir dosyayı karşıya yüklemesine izin vermek gösterilmektedir.

1. Daha önce eklemediğiniz [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığını Web sitenize ekleyin.
2. *App\_Data* klasöründe yeni bir klasör oluşturun ve bu dosyayı *UploadedFiles*olarak adlandırın.
3. Kökte, *FileUpload. cshtml*adlı yeni bir dosya oluşturun.
4. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin: 

    [!code-cshtml[Main](working-with-files/samples/sample7.cshtml)]

    Sayfanın gövde kısmı, büyük olasılıkla bildiğiniz karşıya yükleme kutusu ve düğmelerini oluşturmak için `FileUpload` yardımcısını kullanır:

    ![görüntüyle](working-with-files/_static/image6.jpg)

    `FileUpload` Yardımcısı için ayarladığınız özellikler, dosyanın karşıya yüklenmesini ve Gönder düğmesinin **karşıya yüklemeyi**okumasını istediğinizi belirtir. (Makalede daha sonra daha fazla kutu ekleyeceksiniz.)

    Kullanıcı **karşıya yükle**' ye tıkladığında, sayfanın üst kısmındaki kod dosyayı alır ve kaydeder. Normalde form alanlarından değerleri almak için kullandığınız `Request` nesnesi ayrıca karşıya yüklenmiş dosyayı (veya dosyaları) içeren bir `Files` dizisine sahiptir. Örneğin, ilk karşıya yüklenen dosyayı almak için, dosyadaki belirli konumlardan &#8212; ayrı ayrı dosyalar alabilirsiniz, `Request.Files[0]`alırsınız, ikinci dosyayı almak için, `Request.Files[1]`ve daha fazlasını yapın. (Programlamada, Sayın genellikle sıfırdan başlayacağını unutmayın.)

    Karşıya yüklenen bir dosyayı getirirken, bunu işleyebilmeniz için bir değişkene (burada `uploadedFile`) yerleştirebilirsiniz. Karşıya yüklenen dosyanın adını öğrenmek için, `FileName` özelliğini almanız yeterlidir. Ancak, Kullanıcı bir dosyayı karşıya yüklediğinde, `FileName` tüm yolu içeren kullanıcının özgün adını içerir. Şöyle görünebilir:

    *C:\users\ortakörnek.txt*

    Tüm bu yol bilgilerini istemezsiniz, ancak bu, sunucu için değil kullanıcı bilgisayarındaki yoldur. Yalnızca gerçek dosya adını (*Sample. txt*) istiyorsunuz. `Path.GetFileName` yöntemini kullanarak yalnızca bir yoldan dosya açabilirsiniz, örneğin:

    [!code-csharp[Main](working-with-files/samples/sample8.cs)]

    `Path` nesnesi, yolları eklemek, yolları birleştirmek, vb. gibi çeşitli yöntemlere sahip bir yardımcı programdır.

    Karşıya yüklenen dosyanın adını aldıktan sonra, karşıya yüklenen dosyayı Web sitenizde depolamak istediğiniz yere yeni bir yol oluşturabilirsiniz. Bu durumda, yeni bir yol oluşturmak için `Server.MapPath`, klasör adlarını (*App\_Data/UploadedFiles*) ve yeni bir dosya adı birleştirmelisiniz. Sonra dosyayı kaydetmek için karşıya yüklenen dosyanın `SaveAs` yöntemini çağırabilirsiniz.
5. Sayfayı bir tarayıcıda çalıştırın. 

    ![görüntüyle](working-with-files/_static/image7.jpg)
6. **Araştır** ' a tıklayın ve ardından karşıya yüklenecek dosyayı seçin. 

    ![görüntüyle](working-with-files/_static/image8.jpg)

    **Tarayıcı** düğmesinin yanındaki metin kutusu yolu ve dosya konumunu içerir.

    ![görüntüyle](working-with-files/_static/image9.jpg)
7. **Karşıya Yükle**'ye tıklayın.
8. Web sitesinde proje klasörüne sağ tıklayın ve ardından **Yenile**' ye tıklayın.
9. *UploadedFiles* klasörünü açın. Karşıya yüklediğiniz dosya klasöründe. 

    ![görüntüyle](working-with-files/_static/image10.jpg)

<a id="Letting_Users_Upload_Multiple_Files"></a>
## <a name="letting-users-upload-multiple-files"></a>Kullanıcıların birden çok dosyayı karşıya yüklemesine izin verme

Önceki örnekte, kullanıcıların bir dosyayı karşıya yüklemesine izin vereceksiniz. Ancak, aynı anda birden fazla dosyayı karşıya yüklemek için `FileUpload` yardımcısını kullanabilirsiniz. Bu, bir kerede bir dosyayı karşıya yüklemek sıkıcı olan fotoğrafları karşıya yükleme gibi senaryolar için kullanışlıdır. ( [ASP.NET Web Pages sitesindeki görüntülerle çalışma](https://go.microsoft.com/fwlink/?LinkId=202897)bölümünde fotoğraf yükleme hakkında bilgi edinebilirsiniz.) Bu örnekte, kullanıcıların aynı anda iki kez karşıya yüklemesine izin vermek gösterilmektedir, ancak aynı tekniği kullanarak daha fazla karşıya yükleme yapabilirsiniz.

1. Henüz yapmadıysanız, [bir ASP.NET Web sayfaları sitesine yardımcılar yükleme](https://go.microsoft.com/fwlink/?LinkId=252372)bölümünde açıklandığı gibi, ASP.NET Web yardımcıları kitaplığı 'nı Web sitenize ekleyin.
2. *Fileuploadmultiple. cshtml*adlı yeni bir sayfa oluşturun.
3. Sayfadaki mevcut içeriği aşağıdaki gibi değiştirin:  

    [!code-cshtml[Main](working-with-files/samples/sample9.cshtml)]

    Bu örnekte, sayfanın gövdesindeki `FileUpload` Yardımcısı, kullanıcıların varsayılan olarak iki dosyayı karşıya yüklemesine izin verecek şekilde yapılandırılmıştır. `allowMoreFilesToBeAdded` `true`olarak ayarlandığı için, yardımcı kullanıcının daha fazla karşıya yükleme kutusu eklemesini sağlayan bir bağlantı oluşturur:

    ![görüntüyle](working-with-files/_static/image11.jpg)

    Kullanıcının karşıya yükleyen dosyaları işlemek için, kod önceki örnekte &#8212; kullandığınız temel tekniği kullanır `Request.Files` bir dosyayı alır ve sonra kaydeder. (Doğru dosya adını ve yolunu almak için yapmanız gereken çeşitli şeyler dahil.) Bu sefer, kullanıcının birden çok dosyayı karşıya yükleme olabileceği ve pek çok bilginiz olmadığı konusunda yeniliği. Bunu öğrenmek için `Request.Files.Count`alabilirsiniz.

    Bu sayıyla birlikte `Request.Files`aracılığıyla döngü yapabilir, her dosyayı sırayla getirebilir ve kaydedebilirsiniz. Bir koleksiyonda bilinen sayıda zaman döngüsü yapmak istediğinizde, şöyle bir `for` döngüsünü kullanabilirsiniz:

    [!code-csharp[Main](working-with-files/samples/sample10.cs)]

    `i` değişkeni, yalnızca sizin ayarladığınız üst sınıra kadar, sıfırdan gidecek geçici bir sayaçtır. Bu durumda, üst sınır dosya sayısıdır. Ancak sayaç sıfırda başladığı için, ASP.NET 'deki sayma senaryolarında genellikle üst sınır dosya sayısından bir küçüktür. (Üç dosya karşıya yüklenirse, sayı sıfırdan 2 ' dir.)

    `uploadedCount` değişkeni başarıyla karşıya yüklenen ve kaydedilen tüm dosyaları toplar. Beklenen bir dosyanın yüklenememe olasılığı nedeniyle bu kod hesapları.
4. Sayfayı bir tarayıcıda çalıştırın. Tarayıcı, sayfayı ve iki yükleme kutusunu görüntüler.
5. Karşıya yüklemek için iki dosya seçin.
6. **Başka bir dosya Ekle**' ye tıklayın. Sayfada yeni bir karşıya yükleme kutusu görüntülenir. 

    ![görüntüyle](working-with-files/_static/image12.jpg)
7. **Karşıya Yükle**'ye tıklayın.
8. Web sitesinde proje klasörüne sağ tıklayın ve ardından **Yenile**' ye tıklayın.
9. Karşıya yüklenen dosyaları başarıyla karşıya görmek için *UploadedFiles* klasörünü açın.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET Web Pages sitesindeki görüntülerle çalışma](https://go.microsoft.com/fwlink/?LinkId=202897)

[CSV dosyasına dışarı aktarma](https://msdn.microsoft.com/library/ms155919.aspx)
