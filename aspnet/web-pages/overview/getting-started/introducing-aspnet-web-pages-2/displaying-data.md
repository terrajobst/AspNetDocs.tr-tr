---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: ASP.NET Web sayfalarına giriş-verileri görüntüleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda WebMatrix 'te veritabanı oluşturma ve veritabanı verilerinin bir sayfada nasıl görüntüleneceği gösterilmektedir. Y... olarak kabul edilir.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525223"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a>ASP.NET Web sayfalarına giriş-verileri görüntüleme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda WebMatrix 'te veritabanı oluşturma ve veritabanı verilerinin bir sayfada nasıl görüntüleneceği gösterilmektedir. [ASP.NET Web sayfaları programlamasına giriş](../introducing-razor-syntax-c.md)aracılığıyla seriyi tamamlamış olduğunu varsayar.
> 
> Öğrenecekleriniz:
> 
> - Bir veritabanı ve veritabanı tabloları oluşturmak için WebMatrix araçlarını kullanma.
> - Bir veritabanına veri eklemek için WebMatrix araçlarını kullanma.
> - Sayfadaki verileri veritabanından görüntüleme.
> - ASP.NET Web sayfalarında SQL komutlarını çalıştırma.
> - `WebGrid` yardımcısını özelleştirerek veri görüntüsünü değiştirme ve sayfalama ve sıralama ekleme.
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - WebMatrix veritabanı araçları.
> - `WebGrid` Yardımcısı.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Önceki öğreticide, ASP.NET Web sayfalarına ( *. cshtml* dosyaları), Razor söz dizimi temel bilgileri ve yardımcıları temel almaktadır. Bu öğreticide, serinin geri kalanı için kullanacağınız gerçek Web uygulamasını oluşturmaya başlayacaksınız. Uygulama, filmlerle ilgili bilgileri görüntülemenize, eklemenize, değiştirmenize ve silmenize olanak tanıyan basit bir film uygulamasıdır.

Bu öğreticiyi tamamladığınızda, şu sayfada görünen bir film listesini görüntüleyebileceksiniz:

![CSS sınıf adlarına ayarlanan parametreleri içeren WebGrid görüntüsü](displaying-data/_static/image1.png)

Ancak başlamak için bir veritabanı oluşturmanız gerekir.

## <a name="a-very-brief-introduction-to-databases"></a>Veritabanlarına çok kısa bir giriş

Bu öğretici, veritabanlarına yalnızca Briest giriş bilgilerini sağlar. Veritabanı deneyiminiz varsa, bu kısa bölümü atlayabilirsiniz.

Bir veritabanı, örneğin, müşteriler, siparişler ve satıcılar için tablolar ya da öğrenciler, öğretmenler, sınıflar ve notlar için &mdash; bilgiler içeren bir veya daha fazla tablo içerir. Yapısal olarak, bir veritabanı tablosu elektronik tablo gibidir. Tipik bir adres kitabı düşünün. Adres defterindeki her giriş için (yani, her bir kişi için) adı, soyadı, adresi, e-posta adresi ve telefon numarası gibi çeşitli bilgi parçaları vardır.

![Basit kılavuz olarak örnek veritabanı tablosu](displaying-data/_static/image2.png)

(Satırlar bazen *kayıt*olarak adlandırılır ve sütunlar bazen *alan*olarak adlandırılır.)

Çoğu veritabanı tablolarında, tabloda, bir müşteri numarası, hesap numarası vb. gibi benzersiz bir değer içeren bir sütun olması gerekir. Bu değer tablonun *birincil anahtarı*olarak bilinir ve tablodaki her satırı tanımlamak için kullanırsınız. Örnekte, KIMLIK sütunu, önceki örnekte gösterilen adres defterinin birincil anahtarıdır.

Web uygulamalarında yaptığınız çalışmanın çoğu, veritabanından veri okuma ve bir sayfada görüntüleme uygulamalarından oluşur. Ayrıca genellikle kullanıcılardan bilgi toplayıp bir veritabanına ekleyebilirsiniz ya da veritabanında zaten bulunan kayıtları değiştirirsiniz. (Bu öğreticinin her türlü bu işlem, bu öğretici kümesi konusunda ele alınacaktır.)

Veritabanı çalışması, büyük bir karmaşık olabilir ve özel bilgi gerektirebilir. Bu öğretici için, ancak yalnızca temel kavramları anlamanız gerekir. Bu, her şey sizin gittiğiniz şekilde açıklanmaktadır.

## <a name="creating-a-database"></a>Veritabanı Oluşturma

WebMatrix, veritabanı oluşturmayı ve veritabanında tablo oluşturmayı kolaylaştıran araçlar içerir. (Bir veritabanının yapısı, veritabanının *şeması*olarak adlandırılır.) Bu öğretici kümesi için, &mdash; filmlerde yalnızca bir tablo içeren bir veritabanı oluşturacaksınız.

Daha önce yapmadıysanız WebMatrix 'i açın ve önceki öğreticide oluşturduğunuz Webpagesfilmlerini sitesini açın.

Sol bölmede **veritabanı** çalışma alanına tıklayın.

![WebMatrix veritabanı çalışma alanı sekmesi](displaying-data/_static/image3.png)

Şerit, veritabanıyla ilgili görevleri gösterecek şekilde değişir. Şeritte **Yeni veritabanı**' na tıklayın.

![WebMatrix şeridinde ' yeni veritabanı ' düğmesi](displaying-data/_static/image4.png)

WebMatrix, *Webpagesfilmlerini. sdf*&mdash; siteniz ile aynı ada sahip BIR SQL Server CE veritabanı ( *. sdf* dosyası) oluşturur. (Bu işlemi burada gerçekleştirmezsiniz, ancak *. sdf* uzantısına sahip olduğu sürece dosyayı istediğiniz herhangi bir şekilde yeniden adlandırabilirsiniz.)

## <a name="creating-a-table"></a>Tablo oluşturma

Şeritte **Yeni tablo**' ya tıklayın. WebMatrix, tablo tasarımcısını yeni bir sekmede açar. (yeni tablo seçeneği kullanılamıyorsa, sol taraftaki ağaç görünümünde yeni veritabanının seçildiğinden emin olun.)

![WebMatrix şeridinde ' yeni tablo ' düğmesi](displaying-data/_static/image5.png)

Üstteki metin kutusunda ("tablo adını girin" ifadesinin bulunduğu yer), "Filmler" yazın.

![WebMatrix veritabanı tasarımcısına tablo adı girme](displaying-data/_static/image6.png)

Tablo adının altındaki bölme, sütunları ayrı ayrı tanımladığınız yerdir. Bu öğreticide *film* tablosu için yalnızca birkaç sütun oluşturacaksınız: *kimlik*, *başlık*, *tarz*ve *yıl*.

**Ad** kutusuna "kimlik" yazın. Buraya bir değer girilmesi, yeni sütun için tüm denetimleri etkinleştirir.

Sekmesine tıklayın ve ardından **int**' i seçin. Bu değer, ID sütununun Integer (sayı) verisi içerdiğini belirtir.

> [!NOTE]
> Burada daha fazla çağırmayacağız (çok), ancak bu kılavuzda gezinmek için standart Windows klavye hareketlerini kullanabilirsiniz. Örneğin, alanlar arasında sekme oluşturabilirsiniz, yalnızca bir listedeki öğeyi seçmek için yazmaya başlayabilirsiniz, vb.

Sekme **varsayılan değer** kutusunu geçti (yani boş bırakın). Sekmesine tıklayın ve bu **anahtarı** seçin. Bu seçenek veritabanına *ID* sütununun tek tek satırları tanımlayan verileri içerdiğini söyler. (Diğer bir deyişle, her bir satır, bu satırı bulmak için kullanabileceğiniz ID sütununda benzersiz bir değere sahip olacaktır.)

**Kimlik kimliği** seçeneğini belirleyin. Bu seçenek, veritabanına her yeni satır için otomatik olarak bir sonraki ardışık numarayı oluşturmasını söyler. ( **Identity** seçeneği yalnızca **birincil anahtar** seçeneğini de seçtiyseniz kullanılabilir.)

Sonraki kılavuz satırına tıklayın veya geçerli satırı son vermek için Tab tuşuna iki kez basın. Her iki hareket de geçerli satırı kaydeder ve sonraki birini başlatır. **Varsayılan değer** sütununun artık **null**olduğunu bildiren bir uyarı görürsünüz. (Null, varsayılan değer için varsayılan değerdir, yani konuşmak için.)

Yeni **kimlik** sütununu tanımlamayı bitirdiğinizde tasarımcı aşağıdaki şekilde görünür:

![Filmler tablosu için ID sütununu tanımladıktan sonra WebMatrix Veritabanı Tasarımcısı](displaying-data/_static/image7.png)

Sonraki sütunu oluşturmak için **ad** sütunundaki kutuya tıklayın. Sütun için "title" yazın ve ardından **veri türü** değeri için **nvarchar** 'yi seçin. **Nvarchar** 'nin "var" bölümü, veritabanına bu sütundaki verilerin boyutu, kaydın kaydına göre değişebilen bir dize olacağını söyler. ("N" öneki, alanın herhangi bir alfabe veya yazma sistemi için karakter verilerini tutabileceğini gösteren "Ulusal" ı temsil eder; diğer bir deyişle, alan Unicode verilerini barındırır.)

**Nvarchar**seçtiğinizde, alan için maksimum uzunluğu girebileceğiniz başka bir kutu belirir. Bu öğreticide birlikte çalışacağımız hiçbir film başlığının 50 karakterden uzun olacağını varsayarak 50 yazın.

**Varsayılan değeri** atlayın ve **null değerlere izin ver** seçeneğini temizleyin. Veritabanının, bir başlığa sahip olmayan veritabanına herhangi bir filmin girilmesini izin vermemenizi istemezsiniz.

İşiniz bittiğinde ve sonraki satıra geçtiğinizde, tasarımcı aşağıdaki şekilde görünür:

![Filmler tablosu için başlık sütununu tanımladıktan sonra WebMatrix Veritabanı Tasarımcısı](displaying-data/_static/image8.png)

"Tarz" adlı bir sütun oluşturmak için bu adımları tekrarlayın, uzunluk dışında, bunu yalnızca 30 olarak ayarlayın.

"Year" adlı başka bir sütun oluşturun. Veri türü için, **nchar** ( **nvarchar**değil) öğesini seçin ve uzunluğu 4 olarak ayarlayın. Yıl için, "1995" veya "2010" gibi 4 basamaklı bir sayı kullanacaksınız, bu nedenle değişken boyutlu bir sütun gerekmez.

Tamamlanmış tasarımın şöyle olduğu aşağıda verilmiştir:

![Tüm alanlar filmler tablosu için tanımlandıktan sonra WebMatrix Veritabanı Tasarımcısı](displaying-data/_static/image9.png)

CTRL + S tuşlarına basın veya hızlı erişim araç çubuğunda **Kaydet** düğmesine tıklayın. Sekmeyi kapatarak veritabanı tasarımcısını kapatın.

## <a name="adding-some-example-data"></a>Örnek veri ekleme

Bu öğretici serisinde daha sonra, yeni filmleri bir forma girebileceğiniz bir sayfa oluşturacaksınız. Ancak şimdilik, daha sonra bir sayfada görüntülenebilecek örnek veriler ekleyebilirsiniz.

WebMatrix 'teki **veritabanı** çalışma alanında, daha önce oluşturduğunuz *. sdf* dosyasını gösteren bir ağaç olduğuna dikkat edin. Yeni *. sdf* dosyanız için düğümünü açın ve ardından **Tablolar** düğümünü açın.

![Filmler tablosuna açık ağaç içeren WebMatrix veritabanı çalışma alanı](displaying-data/_static/image10.png)

**Filmler** düğümüne sağ tıklayın ve ardından **veri**' yi seçin. WebMatrix, *filmler* tablosu için veri girebileceğiniz bir kılavuz açar:

![WebMatrix 'te veritabanı giriş Kılavuzu (boş)](displaying-data/_static/image11.png)

**Başlık** sütununa tıklayın ve "Harry karşılandığında Sally" yazın. **Tarzı** sütununa (Tab tuşunu kullanarak) geçin ve "romantik komedi" yazabilirsiniz. **Year** sütununa gidin ve "1989" yazın:

![Tek bir kayıt ile WebMatrix 'te veritabanı giriş Kılavuzu](displaying-data/_static/image12.png)

ENTER tuşuna basın ve WebMatrix yeni filmi kaydeder. **Kimlik** sütununun doldurulduğuna dikkat edin.

![Tek bir kayıt ve otomatik olarak oluşturulan KIMLIK ile WebMatrix 'te veritabanı girişi Kılavuzu](displaying-data/_static/image13.png)

Başka bir film girin (örneğin, "Rüzgar ile gitti", "drama", "1939"). KIMLIK sütunu yeniden doldurulmuştur:

![İki kayıt ve otomatik üretilen kimlik ile WebMatrix 'te veritabanı girişi Kılavuzu](displaying-data/_static/image14.png)

Üçüncü bir filmi girin (örneğin, "Ghostbusters", "komedi"). Bir deneme olarak, **yıl** sütununu boş bırakın ve ENTER tuşuna basın. **Null değerlere Izin ver** seçeneğinin seçili olmadığından, veritabanında bir hata gösterilir:

![Gerekli bir sütun değeri boş bırakılırsa ' geçersiz veri ' hatası görüntülenir](displaying-data/_static/image15.png)

Geri dönüp girişi ("Ghostbusters ve" yılı 1984) onarmak için **Tamam** ' ı tıklatın ve ardından ENTER tuşuna basın.

8 veya daha fazla olana kadar birçok film girin. (8 ' i girmek daha sonra sayfalama ile çalışmayı kolaylaştırır. Ancak bu çok fazla ise şimdilik yalnızca birkaç tane girin.) Gerçek veriler bu şekilde değildir.

![Her iki kayıtla birlikte WebMatrix 'teki veritabanı giriş Kılavuzu](displaying-data/_static/image16.png)

Tüm filmleri hata olmadan girdiyseniz, KIMLIK değerleri sıralıdır. Tamamlanmamış bir film kaydını kaydetmeye çalıştıysanız, KIMLIK numaraları sıralı olmayabilir. Öyleyse, bu sorunsuz bir şekilde yapılır. Sayıların hiçbir anlamı yoktur ve önemli olan tek şey, *filmler* tablosunda benzersiz olmalarıdır.

Veritabanı tasarımcısını içeren sekmeyi kapatın.

Artık bu verileri bir Web sayfasında görüntülemeyi etkinleştirebilirsiniz.

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a>WebGrid Yardımcısı 'nı kullanarak sayfadaki verileri görüntüleme

Verileri bir sayfada göstermek için `WebGrid` Yardımcısı 'nı kullanacaksınız. Bu yardımcı, bir kılavuz veya tabloda (satırlar ve sütunlar) bir görüntü oluşturur. Gördüğünüz gibi, biçimlendirme ve diğer özelliklerle ızgarayı iyileştirebilirsiniz.

Kılavuzu çalıştırmak için birkaç satır kod yazmanız gerekir. Bu çok sayıda satır, bu öğreticide yaptığınız tüm veri erişiminin neredeyse hepsi için bir tür model olarak görev yapar.

> [!NOTE]
> Aslında sayfada verileri görüntülemek için çok sayıda seçeneğiniz vardır; `WebGrid` Yardımcısı yalnızca bir. Bu öğreticide, verileri görüntülemenin en kolay yolu ve makul bir şekilde esnek olduğu için seçtik. Sonraki öğreticide, sayfadaki verilerle çalışmak için daha "el ile" bir yol kullanmayı öğreneceksiniz. Bu, verileri görüntüleme konusunda daha doğrudan denetim sağlar.

WebMatrix 'teki sol bölmede **dosyalar** çalışma alanına tıklayın.

Oluşturduğunuz yeni veritabanı, *App\_veri* klasöründedir. Klasör zaten yoksa, WebMatrix bunu yeni veritabanınız için oluşturmuştur. (Daha önce yardımcıları yüklediyseniz klasör var olabilir.)

Ağaç görünümünde Web sitesinin kökünü seçin. Web sitesinin kökünü seçmelisiniz; Aksi takdirde, yeni dosya App\_Data klasörüne eklenebilir.

Şeritte **Yeni**' ye tıklayın. **Dosya türü seçin** kutusunda, **cshtml**'yi seçin.

**Ad** kutusuna "filmler. cshtml" adlı yeni sayfayı adlandırın:

![' "Filmler" sayfasını gösteren ' bir dosya türü seçin ' iletişim kutusu](displaying-data/_static/image17.png)

**Tamam** düğmesine tıklayın. WebMatrix, içindeki bazı iskelet öğeleriyle yeni bir dosya açar. İlk olarak, veritabanından verileri almak için bazı kodlar yazacaksınız. Böylece, verileri gerçekten göstermek için sayfaya biçimlendirme ekleyeceksiniz.

### <a name="writing-the-data-query-code"></a>Veri sorgu kodunu yazma

Sayfanın üst kısmında, `@{` ve `}` karakterleri arasında aşağıdaki kodu girin. (Bu kodu açılış ve kapanış ayraçları arasında girdiğinizden emin olun.)

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

İlk satır, daha önce oluşturduğunuz veritabanını açar, bu, veritabanında bir şey yapmadan önce her zaman ilk adımdır. Açılacak veritabanının `Database.Open` yöntemi adına söylemiş olursunuz. Adında *. sdf* dahil olmadığınızdan emin olun. `Open` yöntemi, bir *. sdf* dosyası (yani *webpagesfilmlerini. sdf*) olduğunu ve *. sdf* dosyasının *App\_Data* klasöründe olduğunu varsayar. (Önceki adıyla, *uygulama\_veri* klasörü ayrıldık; bu senaryo, ASP.NET bu adla ilgili varsayımlar yaptığı yerlerden biridir.)

Veritabanı açıldığında, bir başvurusu `db`adlı değişkene konur. (Bir şey olarak adlandırılabilir.) `db` değişkeni, veritabanıyla etkileşime nasıl başlayacaksınız.

İkinci satır aslında `Query` yöntemini kullanarak veritabanı verilerini getirir. Bu kodun nasıl çalıştığına dikkat edin: `db` değişkeni, açılan veritabanına yönelik bir başvuruya sahiptir ve `db` değişkenini (`db.Query`) kullanarak `Query` yöntemini çağırabilirsiniz.

Sorgunun kendisi bir SQL `Select` deyimidir. (SQL hakkında biraz arka plan için daha sonra açıklamaya bakın.) İfadesinde, sorgulanacak tabloyu `Movies` tanımlar. `*` karakteri sorgunun tablodaki tüm sütunları döndürmesi gerektiğini belirtir. (Sütunları virgülle ayırarak ayrı ayrı de listeleyebilirsiniz.)

Sorgu sonuçları, varsa, `selectedData` değişkeninde döndürülür ve kullanılabilir hale getirilir. Yine, değişken bir şey olarak adlandırılabilir.

Son olarak, üçüncü satır ASP.NET `WebGrid` Yardımcısı örneğini kullanmak istediğinizi söyler. `new` anahtar sözcüğünü kullanarak yardımcı nesnesini oluşturur (*örnekleyebilirsiniz*) ve sorgu sonuçlarını `selectedData` değişkeni aracılığıyla geçirin. Yeni `WebGrid` nesnesi, veritabanı sorgusunun sonuçlarıyla birlikte `grid` değişkeninde kullanılabilir hale getirilir. Verilerin sayfada gerçekten görüntülenmesini sağlamak için bu işlemin bir süre içinde olması gerekir.

Bu aşamada, veritabanı açıldı, istediğiniz verileri aldınız ve `WebGrid` Yardımcısı 'nı bu verilerle hazırladınız. Sonra, sayfada işaretlemeyi oluşturmak.

> [!TIP] 
> 
> **Yapılandırılmış Sorgu Dili (SQL)**
> 
> SQL, bir veritabanındaki verileri yönetmek için en ilişkisel veritabanlarında kullanılan bir dildir. Verileri almanızı ve güncelleştirmenizi sağlayan ve veritabanı tablolarında veri oluşturmanıza, değiştirmenize ve yönetmenize olanak tanıyan komutları içerir. SQL bir programlama dilinden (gibi C#) farklıdır. SQL ile veritabanına istediğiniz şeyi söylersiniz ve verilerin nasıl alınacağını veya görevi nasıl gerçekleştirebileceğinizi anlamak için veritabanının işi. Aşağıda bazı SQL komutlarının örnekleri ve ne yapacaklarıdır:
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> İlk `Select` ifade, *filmler* tablosundan tüm sütunları alır (`*`tarafından belirtilir).
> 
> İkinci `Select` ifade, *ürün* tablosundaki, Fiyat sütunu değeri 10 ' dan fazla olan kayıtlardan kimliği, adı ve fiyat sütunlarını getirir. Komut, sonuçları Ad sütununun değerlerine göre alfabetik sırada döndürür. Fiyat ölçütleriyle eşleşen bir kayıt yoksa, komut boş bir küme döndürür.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> Bu komut, *ürün* tablosuna yeni bir kayıt ekler, ad sütununu "Croissant", açıklama sütununu "flaşa doğru" olarak, açıklama sütununu ise 1,99 olarak ayarlar.
> 
> Sayısal olmayan bir değer belirttiğinizde, değerin tek tırnak işaretleri içine alındığına (içinde C#olduğu gibi çift tırnak işaretleri değil) dikkat edin. Bu tırnak işaretlerini metin veya tarih değerlerinin etrafında kullanın, ancak sayıların etrafında kullanmayın.
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> Bu komut, son kullanma tarihi sütunu 1 Ocak 2008 ' den daha eski olan *ürün* tablosundaki kayıtları siler. (Komut, *ürün* tablosunda bu tür bir sütun olduğunu varsayar.) Tarih, AA/GG/YYYY biçiminde girilir, ancak yerel ayarınız için kullanılan biçimde girilmelidir.
> 
> `Insert` ve `Delete` komutları sonuç kümeleri döndürmez. Bunun yerine, komuttan kaç kaydın etkilendiğini belirten bir sayı döndürür.
> 
> Bu işlemlerden bazıları (kayıtları ekleme ve silme gibi) için, işlemi isteyen işlemin veritabanında uygun izinlere sahip olması gerekir. Bu nedenle, veritabanına bağlanırken genellikle bir Kullanıcı adı ve parola sağlamanız gerekir.
> 
> Onlarca SQL komutu vardır, ancak bunlar burada gördüğünüz komutlarla benzer bir şekilde gerçekleştirilir. SQL komutlarını kullanarak veritabanı tabloları oluşturabilir, tablodaki kayıt sayısını sayabilir, fiyatları hesaplayabilir ve birçok daha fazla işlem gerçekleştirebilirsiniz.

### <a name="adding-markup-to-display-the-data"></a>Verileri göstermek için biçimlendirme ekleme

`<head>` öğesinin içinde, `<title>` öğesinin içeriğini "Filmler" olarak ayarlayın:

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

Sayfanın `<body>` öğesi içinde aşağıdakileri ekleyin:

[!code-html[Main](displaying-data/samples/sample3.html)]

İşte bu kadar. `grid` değişkeni, önceki kodda `WebGrid` nesnesini oluştururken oluşturduğunuz değerdir.

WebMatrix ağacı görünümünde, sayfaya sağ tıklayın ve **tarayıcıda Başlat**' ı seçin. Şu sayfaya benzer bir şey göreceksiniz:

![Filmler tablosundan varsayılan WebGrid Yardımcısı çıkışı](displaying-data/_static/image18.png)

Sütuna göre sıralamak için bir sütun başlığı bağlantısına tıklayın. Bir başlığa tıklayarak sıralama yapabilmesi, **WebGrid** Yardımcısı içinde yerleşik bir özelliktir.

`GetHtml` yöntemi, adından da anlaşılacağı gibi, verileri görüntüleyen bir biçimlendirme oluşturur. Varsayılan olarak `GetHtml` yöntemi bir HTML `<table>` öğesi oluşturur. (İsterseniz, tarayıcıdaki sayfanın kaynağına bakarak işlemeyi doğrulayabilirsiniz.)

## <a name="modifying-the-look-of-the-grid"></a>Kılavuzun görünümünü değiştirme

`WebGrid` Yardımcısı kullanımı oldukça kolaydır, ancak elde edilen ekran düz bir işlemdir. `WebGrid` Yardımcısı, verilerin nasıl görüntülendiğini denetlemenize izin veren tüm seçeneklere sahiptir. Bu öğreticide araştırılacak kadar çok fazla var, ancak bu bölüm bu seçeneklerin bir fikrini size sunacaktır. Bu serideki sonraki öğreticilerde bazı ek seçenekler ele alınacaktır.

### <a name="specifying-individual-columns-to-display"></a>Görüntülenecek sütunları tek tek belirtme

Başlamak için yalnızca belirli sütunları görüntülenmesini istediğinizi belirtebilirsiniz. Varsayılan olarak, gördüğünüz gibi, bu kılavuzda, *filmler* tablosundan tüm dört sütun gösterilmektedir.

*Filmler. cshtml* dosyasında, yeni eklediğiniz `@grid.GetHtml()` işaretlemesini aşağıdaki şekilde değiştirin:

[!code-css[Main](displaying-data/samples/sample4.css)]

Görüntülenecek sütunları göstermek için, `GetHtml` yöntemi için bir `columns` parametresi ekleyin ve bir sütun koleksiyonunu geçirin. Koleksiyonda, içerilecek her bir sütunu belirtirsiniz. Bir `grid.Column` nesnesini ekleyerek ve istediğiniz veri sütununun adını geçirerek görüntülenecek tek bir sütun belirlersiniz. (Bu sütunlar SQL sorgu sonuçlarına dahil olmalıdır — `WebGrid` Yardımcısı sorgu tarafından döndürülmedi sütunları görüntüleyemez.)

Tarayıcıda *film. cshtml* sayfasını yeniden başlatın ve bu sefer aşağıdakine benzer bir ekran alırsınız (hiçbir kimlik sütununun gösterilmediğine dikkat edin):

![Yalnızca seçili sütunları gösteren WebGrid görüntüsü](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a>Kılavuzun görünümünü değiştirme

Sütunları görüntülemek için biraz daha fazla seçenek mevcuttur, bazıları bu küme içindeki sonraki öğreticilerde araştırılacak. Şimdilik, bu bölüm kılavuza bir bütün olarak stil eklemek için size yol gösterebilir.

Sayfanın `<head>` bölümü içinde, kapanış `</head>` etiketinden hemen önce, aşağıdaki `<style>` öğesini ekleyin:

[!code-css[Main](displaying-data/samples/sample5.css)]

Bu CSS işaretlemesi `grid`, `head`vb. adlı sınıfları tanımlar. Ayrıca, bu stil tanımlarını ayrı bir *. css* dosyasına yerleştirebilir ve sayfaya bağlayabilirsiniz. (Aslında Bu öğreticinin daha sonra bu öğreticide ayarlanabileceksiniz.) Ancak, bu öğreticide işlemleri kolaylaştırmak için verileri görüntüleyen aynı sayfada yer alırlar.

Artık bu stil sınıflarını kullanmak için `WebGrid` yardımcısını edinebilirsiniz. Yardımcı, yalnızca bu amaçla birçok özelliğe sahiptir (örneğin, `tableStyle`), bunlara bir CSS stil sınıfı adı atarsınız ve bu sınıf adı yardımcı tarafından işlenen biçimlendirmenin bir parçası olarak işlenir.

`grid.GetHtml` işaretlemesini şu kod gibi görünecek şekilde değiştirin:

[!code-css[Main](displaying-data/samples/sample6.css)]

Buradaki yenilikler, `GetHtml` yöntemine `tableStyle`, `headerStyle`ve `alternatingRowStyle` parametreleri ekledik. Bu parametreler, bir süre önce eklediğiniz CSS stillerinin adlarına ayarlanmıştır.

Sayfayı çalıştırın ve bu sefer şundan çok daha az düz bir ızgara görürsünüz:

![CSS sınıf adlarına ayarlanan parametreleri içeren WebGrid görüntüsü](displaying-data/_static/image20.png)

`GetHtml` yönteminin ne oluşturulduğunu görmek için tarayıcıda sayfanın kaynağına bakabilirsiniz. Burada ayrıntıya başvurmayacağız, ancak önemli nokta `tableStyle`gibi parametreleri belirterek, kılavuzun aşağıdaki gibi HTML etiketleri oluşturmasına neden oldu:

`<table class="grid">`

`<table>` etiketinde, daha önce eklediğiniz CSS kurallarından birine başvuran bir `class` özniteliği eklenmiş. Bu kod, `GetHtml` yöntemi için farklı parametreler &mdash; temel bir örüntüyi gösterir. CSS sınıflarıyla ne yapabilirsiniz?

## <a name="adding-paging"></a>Sayfalama ekleme

Bu öğreticide son görev olarak kılavuza sayfalama ekleyeceksiniz. Şimdi tüm filmlerinizi tek seferde görüntüleme sorunu değildir. Ancak yüzlerce film eklediyseniz sayfa görüntüleme uzun zaman alır.

Sayfa kodunda, `WebGrid` nesnesini oluşturan çizgiyi aşağıdaki koda değiştirin:

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

Öncesinde tek fark, 3 ' e ayarlanmış bir `rowsPerPage` parametresi ekledik.

Sayfayı çalıştırın. Kılavuz, bir seferde 3 satır, ek olarak, veritabanınızdaki filmlerde sayfa oluşturmanıza olanak sağlayan gezinti bağlantıları da görüntüler:

![Sayfalama ile WebGrid görüntüsü](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a>Sonraki adımda

Bir sonraki öğreticide, bir formda Kullanıcı girişi almak için Razor ve C# kod kullanmayı öğreneceksiniz. Filmleri başlığa veya tarzya göre bulabilmeniz için filmler sayfasına bir arama kutusu ekleyeceksiniz.

## <a name="complete-listing-for-movies-page"></a>Filmler sayfasının tamamını listeleme

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> [Önceki](intro-to-web-pages-programming.md)
> [İleri](form-basics.md)
