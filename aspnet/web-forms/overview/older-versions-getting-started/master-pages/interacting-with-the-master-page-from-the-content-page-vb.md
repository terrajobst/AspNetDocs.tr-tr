---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
title: Içerik sayfasından ana sayfa ile etkileşim kurma (VB) | Microsoft Docs
author: rick-anderson
description: Içerik sayfasındaki koddan, ana sayfanın özellikler, vs. yöntemlerini çağırma, özelliklerini ayarlama hakkında inceler.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 081fe010-ba0f-4e7d-b4ba-774840b601c2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
msc.type: authoredcontent
ms.openlocfilehash: fe1f7b80b26ff25c1ce744e4f823e3fb35eea074
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548218"
---
# <a name="interacting-with-the-master-page-from-the-content-page-vb"></a>Ana Sayfadan İçerik Sayfası ile Etkileşim Kurma (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_VB.pdf)

> Içerik sayfasındaki koddan, ana sayfanın özellikler, vs. yöntemlerini çağırma, özelliklerini ayarlama hakkında inceler.

## <a name="introduction"></a>Giriş

Son beş öğreticilerde, ana sayfa oluşturma, içerik bölgelerini tanımlama, ASP.NET sayfalarını ana sayfaya bağlama ve sayfaya özgü içerik tanımlama konusunda baktık. Bir ziyaretçi belirli bir içerik sayfasını istediğinde, içerik ve ana sayfaların biçimlendirmesi çalışma zamanında kullanılır ve bu da birleştirilmiş bir denetim hiyerarşisinin oluşturulmasına neden olur. Bu nedenle, ana sayfanın ve içerik sayfalarından birinin etkileşime girebileceği bir yol zaten gördük: içerik sayfası, ana sayfanın ContentPlaceHolder denetimlerinde kullanılacak biçimlendirmeyi yanlış bir biçimde gördünüz.

Henüz incelendiğimiz, ana sayfa ve içerik sayfasının programlama yoluyla nasıl etkileşim kurabileceğiz. Ana sayfanın ContentPlaceHolder denetimlerine yönelik biçimlendirmeyi tanımlamanın yanı sıra, bir içerik sayfası da ana sayfanın ortak özelliklerine değer atayabilir ve ortak yöntemlerini çağırabilir. Benzer şekilde, bir ana sayfa, içerik sayfalarıyla etkileşime geçebilir. Ana ve içerik sayfası arasındaki programlama etkileşimi, bildirim temelli işaretlemelerde etkileşim dışında daha az yaygın olsa da, bu tür programlama etkileşiminin gerektiği birçok senaryo vardır.

Bu öğreticide, bir içerik sayfasının, ana sayfası ile programlı olarak nasıl etkileşime girebileceği anlatılmaktadır; sonraki öğreticide, ana sayfanın içerik sayfalarıyla nasıl benzer şekilde etkileşime gireceğini inceleyeceğiz.

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>Bir Içerik sayfası ve onun ana sayfası arasındaki programlama etkileşimi örnekleri

Sayfanın belirli bir bölgesinin sayfa temelinde yapılandırılması gerektiğinde, ContentPlaceHolder denetimini kullanırız. Ancak sayfaların çoğunluğunun belirli bir çıktıyı yaymasına gerek duyduğu durumlar hakkında ne olur, ancak başka bir şey göstermek için az sayıda sayfanın özelleştirilmesi gerekir mi? [*Birden çok contentter ve varsayılan içerik*](multiple-contentplaceholders-and-default-content-vb.md) öğreticisinde incedığımız gibi bir örnek, her sayfada bir oturum açma arabirimi görüntülenmesini içerir. Çoğu sayfanın bir oturum açma arabirimi içermesi gerekir, ancak örneğin, ana oturum açma sayfası (`Login.aspx`) gibi bir sayfa için bastırılmalıdır. Hesap Oluştur sayfası; ve yalnızca kimliği doğrulanmış kullanıcılar tarafından erişilebilen diğer sayfalara. [*Birden çok Contenttutucuları ve varsayılan içerik*](multiple-contentplaceholders-and-default-content-vb.md) öğreticisi, ana sayfada bir ContentPlaceHolder için varsayılan içeriğin nasıl tanımlanacağını ve ardından varsayılan içeriğin istenmediğinde bu sayfalarda nasıl geçersiz kılınacağını gösterdi.

Başka bir seçenek de ana sayfada, oturum açma arabiriminin gösterilip gösterilmeyeceğini veya gizlenmeyeceğini belirten bir ortak özellik veya yöntem oluşturmaktır. Örneğin, ana sayfa, ana sayfada oturum açma denetiminin `Visible` özelliğini ayarlamak için değeri kullanılan `ShowLoginUI` adlı ortak bir özellik içerebilir. Oturum açma kullanıcı arabiriminin gizlenmesi gereken içerik sayfaları, programlı olarak `ShowLoginUI` özelliğini `False`olarak ayarlayabilir.

En yaygın içerik ve ana sayfa etkileşimi örneği, ana sayfada görünen verilerin içerik sayfasında transpired olduktan sonra yenilenmesi gerektiğinde oluşur. Belirli bir veritabanı tablosundan en son eklenen beş kaydı görüntüleyen ve içerik sayfalarından birinin aynı tabloya yeni kayıtlar eklemek için bir arabirim içerdiği bir GridView içeren bir ana sayfayı düşünün.

Bir Kullanıcı yeni bir kayıt eklemek için sayfayı ziyaret ettiğinde, ana sayfada en son eklenen beş kaydı görür. Yeni kaydın sütunlarının değerlerini doldurduktan sonra formu gönderir. Ana sayfadaki GridView 'un `EnableViewState` özelliği true (varsayılan) olarak ayarlandığı varsayılırsa, içeriği görünüm durumundan yeniden yüklenir ve sonuç olarak veritabanına daha yeni bir kayıt eklenmiş olsa da, beş aynı kayıt görüntülenir. Bu, kullanıcıyı şaşırtır.

> [!NOTE]
> GridView 'un görünüm durumunu her geri göndermede arka plandaki veri kaynağına yeniden bağlanacak şekilde devre dışı bıraksanız bile, veriler, yeni kaydın daTaB 'ye eklendiğine göre daha önce sayfa yaşam döngüsü içinde GridView 'a bağlandığından yalnızca yeni eklenen kaydı göstermez. ASE.

Bu sorunu gidermek için, yeni kayıt veritabanına eklendikten *sonra* GridView 'un geri göndermede ana sayfanın GridView 'da gösterilmesi için GridView 'a bir veri kaynağına yeniden bağlamasını söylemek gerekir. Yeni kayıt (ve olay işleyicileri) ekleme arabirimi içerik sayfasında yer aldığı ancak yenilenmesi gereken GridView ana sayfada olduğundan, bu, içerik ve ana sayfalar arasında etkileşim gerektirir.

İçerik sayfasındaki bir olay işleyicisinden ana sayfanın görüntüsünü yenilemek, içerik ve ana sayfa etkileşimi için en yaygın gereksinimlerden biri olduğundan, bu konuyu daha ayrıntılı bir şekilde keşfedelim. Bu öğreticiye yönelik indirme, Web sitesinin `App_Data` klasöründe `NORTHWIND.MDF` adlı bir Microsoft SQL Server 2005 Express Edition veritabanı içerir. Northwind veritabanı, kurgusal bir şirket için ürün, çalışan ve satış bilgilerini depolar, Northwind Traders.

1\. adım, ana sayfada bir GridView 'da en son eklenen beş ürünü görüntülemeyi adım adım açıklar. 2\. adım yeni ürünler eklemek için bir içerik sayfası oluşturur. 3\. adım, ana sayfada ortak özellikler ve Yöntemler oluşturma ve 4. adım, içerik sayfasından bu özellikler ve yöntemlerle programlı bir şekilde arabirim oluşturmayı gösterir.

> [!NOTE]
> Bu öğreticide, ASP.NET 'deki verilerle çalışma özelliklerinin açıklaması yoktur. Ana sayfayı verileri görüntüleyecek şekilde ayarlamaya yönelik adımlar ve veri ekleme için içerik sayfası tamamlanmıştır, ancak Breezy. Daha ayrıntılı bir bakış için veri görüntüleme ve ekleme ve SqlDataSource ve GridView denetimlerini kullanma hakkında daha fazla bilgi için, Bu öğreticinin sonundaki diğer okumalar bölümünde bulunan kaynaklara bakın.

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>1\. Adım: Ana sayfada en son eklenen beş ürünü görüntüleme

Site. Master ana sayfasını açın ve `leftContent` `<div>`bir etiket ve bir GridView denetimi ekleyin. Etiketin `Text` özelliğini temizleyin, `EnableViewState` özelliğini `False`ve `ID` özelliği `GridMessage`olarak ayarlayın. GridView 'un `ID` özelliğini `RecentProducts`olarak ayarlayın. Sonra, tasarımcıdan GridView 'un akıllı etiketini genişletin ve yeni bir veri kaynağına bağlamayı seçin. Bu, veri kaynağı Yapılandırma Sihirbazı 'nı başlatır. `App_Data` klasöründeki Northwind veritabanı Microsoft SQL Server bir veritabanı olduğundan, öğesini seçerek bir SqlDataSource oluşturmayı seçin (bkz. Şekil 1); SqlDataSource `RecentProductsDataSource`adlandırın.

[GridView 'u, RecentProductsDataSource adlı bir SqlDataSource denetimine bağlama ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image1.png)

**Şekil 01**: GridView öğesini `RecentProductsDataSource` adlı bir SqlDataSource denetimine bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image3.png))

Sonraki adım bize hangi veritabanının bağlanılacağını belirtmemizi ister. Açılan listeden `NORTHWIND.MDF` veritabanı dosyasını seçin ve Ileri ' ye tıklayın. Bu veritabanını ilk kez kullandığımızda, sihirbaz `Web.config`' de bağlantı dizesini depolamayı sunacak. `NorthwindConnectionString`adı kullanarak bağlantı dizesini depoladığından.

[![Northwind veritabanına bağlanın](interacting-with-the-master-page-from-the-content-page-vb/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image4.png)

**Şekil 02**: Northwind veritabanına bağlanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image6.png))

Veri kaynağını yapılandırma Sihirbazı, verileri almak için kullanılan sorguyu belirleyebilmemiz için iki yol sunar:

- Özel bir SQL ifadesini veya saklı yordamı belirterek veya
- Bir tablo veya görünüm seçerek ve sonra döndürülecek sütunları belirterek

Yalnızca beş adet en son eklenen ürünü döndürmek istiyoruz, özel bir SQL ekstresi belirtmemiz gerekir. Aşağıdaki `SELECT` sorgusunu kullanın:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample1.sql)]

`TOP 5` anahtar sözcüğü sorgudaki ilk beş kaydı döndürür. `Products` tablonun birincil anahtarı `ProductID`, tabloya eklenen her yeni ürünün önceki girdiden daha büyük bir değere sahip olduğunu sağlayan bir `IDENTITY` sütunudur. Bu nedenle, sonuçları azalan sırada `ProductID` sıralamada, en son oluşturulanlar ile başlayan ürünler döndürülür.

[![en son eklenen beş ürünü döndürür](interacting-with-the-master-page-from-the-content-page-vb/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image7.png)

**Şekil 03**: en son eklenen beş ürünü döndürün ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image9.png))

Sihirbazı tamamladıktan sonra, Visual Studio GridView için iki BoundFields üretir ve veritabanından döndürülen `ProductName` ve `UnitPrice` alanlarını görüntüler. Bu noktada, ana sayfanızın bildirim temelli biçimlendirmesi aşağıdakine benzer bir biçimlendirme içermelidir:

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample2.aspx)]

Gördüğünüz gibi, biçimlendirme şunları içerir: Label Web Control (`GridMessage`); GridView `RecentProducts`, iki BoundFields ile; ve en son eklenen beş ürünü geri getiren bir SqlDataSource denetimi.

Bu GridView oluşturuldu ve SqlDataSource denetimi yapılandırılmışsa Web sitesini bir tarayıcı aracılığıyla ziyaret edin. Şekil 4 ' te gösterildiği gibi, sol alt köşede en son eklenen beş ürünü listeleyen bir kılavuz görürsünüz.

[GridView ![en son eklenen beş ürünü görüntüler](interacting-with-the-master-page-from-the-content-page-vb/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image10.png)

**Şekil 04**: GridView en son eklenen beş ürünü görüntüler ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image12.png))

> [!NOTE]
> GridView 'un görünümünü temizlemeyi ücretsiz olarak hissetmekten çekinmeyin. Bazı öneriler, görüntülenecek `UnitPrice` değerini para birimi olarak biçimlendirmeyi ve kılavuz görünümünü geliştirmek için arka plan renkleri ve yazı tiplerini kullanmayı içerir.

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>2\. Adım: yeni ürünler eklemek için Içerik sayfası oluşturma

Bir sonraki göreviniz, bir kullanıcının `Products` tablosuna yeni bir ürün ekleyebileceği bir içerik sayfası oluşturmaktır. `AddProduct.aspx`adlı `Admin` klasöre yeni bir içerik sayfası ekleyerek `Site.master` ana sayfasına bağlamayı unutmayın. Şekil 5 ' te, Bu sayfa Web sitesine eklendikten sonra Çözüm Gezgini gösterilmektedir.

[Yönetici klasörüne yeni bir ASP.NET sayfası eklemek ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image13.png)

**Şekil 05**: `Admin` klasöre yeni bir ASP.NET sayfası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image15.png))

[*Ana sayfada başlık, meta etiketler ve DIĞER HTML üst bilgilerini belirtme*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) öğreticisinde, açıkça ayarlanmamışsa sayfanın başlığını oluşturan `BasePage` adlı özel bir temel sayfa sınıfı oluşturduğumuz hatırlayın. `AddProduct.aspx` sayfanın arka plan kod sınıfına gidin ve `BasePage` türetebilirsiniz (`System.Web.UI.Page`yerine).

Son olarak, `Web.sitemap` dosyasını bu ders için bir giriş içerecek şekilde güncelleştirin. Denetim KIMLIĞI adlandırma sorunları dersi için `<siteMapNode>` altına aşağıdaki biçimlendirmeyi ekleyin:

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample3.xml)]

Şekil 6 ' da gösterildiği gibi, bu `<siteMapNode>` öğesinin eklenmesi dersler listesinde yansıtılır.

`AddProduct.aspx`dön. `MainContent` ContentPlaceHolder Içerik denetiminde, bir DetailsView denetimi ekleyin ve `NewProduct`adlandırın. DetailsView öğesini `NewProductDataSource`adlı yeni bir SqlDataSource denetimine bağlayın. Adım 1 ' deki SqlDataSource ile benzer şekilde, Sihirbazı Northwind veritabanını kullanacak şekilde yapılandırın ve özel bir SQL ifadesini belirtmeyi seçin. DetailsView veritabanına öğe eklemek için kullanılacağından, hem `SELECT` hem de bir `INSERT` ifadesini belirtmemiz gerekir. Aşağıdaki `SELECT` sorgusunu kullanın:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample4.sql)]

Ardından, Ekle sekmesinden aşağıdaki `INSERT` ifadesini ekleyin:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample5.sql)]

Sihirbazı tamamladıktan sonra DetailsView 'un akıllı etiketine gidin ve "eklemeyi etkinleştir" onay kutusunu işaretleyin. Bu, DetailsView öğesine `ShowInsertButton` özelliği true olarak ayarlanmış bir CommandField ekler. Bu DetailsView yalnızca veri eklemek için kullanılacağından, DetailsView 'un `DefaultMode` özelliğini `Insert`olarak ayarlayın.

İşte bu kadar kolay! Bu sayfayı test edelim. `AddProduct.aspx` bir tarayıcı aracılığıyla ziyaret edin, bir ad ve fiyat girin (bkz. Şekil 6).

[Veritabanına yeni bir ürün eklemek ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image16.png)

**Şekil 06**: veritabanına yeni bir ürün ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image18.png))

Yeni ürününüzün adını ve fiyatını yazdıktan sonra Ekle düğmesine tıklayın. Bu, formun geri göndermeye neden olur. Geri göndermede, SqlDataSource denetiminin `INSERT` deyimleri yürütülür; iki parametresi, DetailsView 'un iki metin kutusu denetimlerinde Kullanıcı tarafından girilen değerlerle doldurulur. Ne yazık ki, bir ekleme gerçekleştiyse görsel geri bildirim yok. Yeni bir kaydın eklendiğini onaylayan bir ileti görüntülenmesi iyi bir hale gelir. Bunu okuyucu için bir alıştırma olarak bırakıyorum. Ayrıca, DetailsView 'tan yeni bir kayıt eklendikten sonra ana sayfada GridView, önceki ile aynı beş kaydı gösterir; yalnızca eklenen kaydı içermez. Yaklaşan adımlarda bunu nasıl ortadan sileceğiz.

> [!NOTE]
> Ekleme işlemi başarılı olan bazı görsel geri bildirimleri eklemenin yanı sıra, Ayrıca, DetailsView 'un doğrulama arabirimini de içerecek şekilde güncelleştirmeniz önerilir. Şu anda doğrulama yok. Bir Kullanıcı `UnitPrice` alanı için geçersiz bir değer girerse (örneğin, "çok pahalı"), sistem bu dizeyi bir Decimal 'e dönüştürmeye çalıştığında geri gönderme sırasında bir özel durum atılır. Ekleme arabirimini özelleştirme hakkında daha fazla bilgi için veri [ *değişim arabirimi* öğreticisini](https://asp.net/learn/data-access/tutorial-20-vb.aspx) [veri öğreticisi ile çalışma öğreticiden](../../data-access/index.md)özelleştirme bölümüne bakın.

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>3\. Adım: Ana sayfada ortak özellikler ve Yöntemler oluşturma

1\. adımda, ana sayfada GridView 'un üzerinde `GridMessage` adlı bir etiket Web denetimi ekledik. Bu etiketin isteğe bağlı olarak bir ileti görüntülemesi amaçlanmıştır. Örneğin, `Products` tabloya yeni bir kayıt eklendikten sonra, "*ProductName* veritabanına eklenmiş" iletisini şöyle göstermek isteyebilirsiniz. Ana sayfada bu etiketin metnini sabit koda eklemek yerine, iletinin içerik sayfası tarafından özelleştirilebilir olmasını isteyebilir.

Etiket denetimi ana sayfa içinde korumalı üye değişkeni olarak uygulandığından, doğrudan içerik sayfalarından erişilemez. İçerik sayfasından ana sayfa içindeki etiketle çalışmak için (veya bu şekilde, ana sayfadaki herhangi bir Web denetimi), Web denetimini kullanıma sunan ana sayfada bir ortak özellik oluşturmanız veya özelliklerinden birinin bir ara sunucu olarak işlev görmemiz gerekir  erişim. Etiketin `Text` özelliğini göstermek için ana sayfanın arka plan kod sınıfına aşağıdaki sözdizimini ekleyin:

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample6.vb)]

Bir içerik sayfasından `Products` tablosuna yeni bir kayıt eklendiğinde, ana sayfadaki `RecentProducts` GridView 'un temel alınan veri kaynağına yeniden bağlanması gerekir. GridView 'un yeniden bağlamak için `DataBind` yöntemini çağırın. Ana sayfadaki GridView, içerik sayfaları için programlı olarak erişilebilir olmadığından, ana sayfada, çağrıldığında verileri GridView 'a yeniden bağlayan bir genel yöntem oluşturuyoruz. Aşağıdaki yöntemi ana sayfanın arka plan kod sınıfına ekleyin:

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample7.vb)]

`GridMessageText` özelliği ve `RefreshRecentProductsGrid` yöntemi yerine, herhangi bir içerik sayfası programlı olarak `GridMessage` etiketin `Text` özelliğinin değerini ayarlayabilir veya okuyabilir veya verileri `RecentProducts` GridView 'a yeniden bağlayabilirsiniz. 4\. adım, ana sayfanın ortak özelliklerine ve yöntemlerine bir içerik sayfasından nasıl erişekullanacağınızı inceler.

> [!NOTE]
> Ana sayfanın özelliklerini ve yöntemlerini `Public`olarak işaretlemeyi unutmayın. Bu özellikleri ve yöntemleri `Public`olarak açıkça belirtmezseniz, içerik sayfasından erişilemeyecektir.

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>4\. Adım: ana sayfanın ortak üyelerini bir Içerik sayfasından çağırma

Artık ana sayfada gerekli ortak özellikler ve Yöntemler olduğuna göre, bu özellikleri ve yöntemleri `AddProduct.aspx` içerik sayfasından çağırmaya hazırız. Özellikle, ana sayfanın `GridMessageText` özelliğini ayarlaması ve yeni ürün veritabanına eklendikten sonra `RefreshRecentProductsGrid` yöntemini çağırması gerekir. Tüm ASP.NET Data Web verileri, çeşitli görevleri tamamladıktan hemen önce ve sonra olayları harekete geçirdikten sonra, bu da sayfa geliştiricilerinin görevden önce veya sonra bazı programlı eylemler yapmasını kolaylaştırır. Örneğin, Son Kullanıcı DetailsView 'un INSERT düğmesine tıkladığında, geri gönderme sırasında DetailsView, ekleme iş akışı başlamadan önce `ItemInserting` olayını oluşturur. Daha sonra kaydı veritabanına ekler. Bunun ardından, DetailsView `ItemInserted` olayını oluşturur. Bu nedenle, yeni ürün eklendikten sonra ana sayfayla çalışmak için, DetailsView 'un `ItemInserted` olayı için bir olay işleyicisi oluşturun.

Bir içerik sayfasının, ana sayfası ile programlı bir şekilde arabirim oluşturma için iki yol vardır:

- Ana sayfaya gevşek olarak yazılmış bir başvuru döndüren `Page.Master` özelliğini kullanma veya
- Bir `@MasterType` yönergesi aracılığıyla sayfanın ana sayfa türünü veya dosya yolunu belirtin; Bu, `Master`adlı sayfaya otomatik olarak türü kesin belirlenmiş bir özellik ekler.

Her iki yaklaşımı de inceleyelim.

### <a name="using-the-loosely-typedpagemasterproperty"></a>Gevşek yazılı`Page.Master`özelliğini kullanma

Tüm ASP.NET Web sayfaları, `System.Web.UI` ad alanında bulunan `Page` sınıfından türetilmelidir. `Page` sınıfı, sayfanın ana sayfasına bir başvuru döndüren bir [`Master` özelliği](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx) içerir. Sayfada bir ana sayfa yoksa `Master` `Nothing`döndürür.

`Master` özelliği, tüm ana sayfaların türevi olan temel tür olan [`MasterPage`](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) türünde (Ayrıca `System.Web.UI` ad alanında bulunan) bir nesne döndürür. Bu nedenle, Web sitenizin ana sayfasında tanımlanan ortak özellikleri veya yöntemleri kullanmak için `Master` özelliğinden döndürülen `MasterPage` nesnesini uygun türe atamalısınız. Ana sayfa dosyası `Site.master`adlandırdığımız için, arka plan kod sınıfı `Site`olarak adlandırılmıştır. Bu nedenle, aşağıdaki kod `Page.Master` özelliğini `Site` sınıfının bir örneğine yayınlar.

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample8.vb)]

Gevşek olarak yazılmış `Page.Master` özelliğini site türüne güncelleştirdiğimiz için, siteye özgü özelliklere ve yöntemlere başvuracağız. Şekil 7 ' de gösterildiği gibi, ortak özellik `GridMessageText` IntelliSense açılır penceresinde görünür.

[![IntelliSense ana sayfanın ortak özelliklerini ve yöntemlerini gösterir](interacting-with-the-master-page-from-the-content-page-vb/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image19.png)

**Şekil 07**: IntelliSense ana sayfanın ortak özelliklerini ve yöntemlerini gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image21.png))

> [!NOTE]
> Ana sayfa dosyanızı `MasterPage.master`, ana sayfanın arka plan kod sınıfı adı `MasterPage`. Bu, `System.Web.UI.MasterPage` türünden `MasterPage` sınıfınıza atama yaparken belirsiz koda yol açabilir. Kısacası,, Web sitesi proje modeli kullanılırken biraz daha karmaşık olabilecek bir şekilde, atama yaptığınız türü tam olarak nitelemeniz gerekir. Önerim, ana sayfanızı `MasterPage.master` dışında bir adla adlandırdığınızı veya daha da iyi bir şekilde, ana sayfaya kesin olarak yazılmış bir başvuru oluşturmanız durumunda olduğundan emin olmak olacaktır.

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>`@MasterType`yönergesi ile kesin türü belirtilmiş bir başvuru oluşturma

Bir ASP.NET sayfasının arka plan kod sınıfının kısmi bir sınıf olduğunu görebilirsiniz (sınıf tanımındaki `Partial` anahtar sözcüğünü unutmayın). Kısmi sınıflar, ve Visual Basic C# with.NET Framework 2,0 ' de tanıtılmıştı ve bir Nutshell içinde, bir sınıfın üyelerinin birden çok dosya genelinde tanımlanmasını sağlar. Arka plan kod dosyası `AddProduct.aspx.vb`(örneğin,), yaptığımız kodu, sayfa geliştiricisi, oluşturma ' yı içerir. ASP.NET motoru, kodumuza ek olarak, bildirim temelli biçimlendirmeyi sayfanın sınıf hiyerarşisine çeviren, içindeki Özellikler ve olay işleyicileri ile ayrı bir sınıf dosyası oluşturur.

Bir ASP.NET sayfası her ziyaret edildiğinde oluşan otomatik kod oluşturma, bazı ilginç ve yararlı olanaklar için bir yol sunar. Ana sayfalar söz konusu olduğunda, ASP.NET Engine 'e içerik sayfamız tarafından hangi ana sayfanın kullanıldığını söylüyoruz, bizim için kesin olarak belirlenmiş `Master` bir özellik oluşturur.

İçerik sayfasının ana sayfa türünün ASP.NET altyapısını bilgilendirmek için [`@MasterType` yönergesini](https://msdn.microsoft.com/library/ms228274.aspx) kullanın. `@MasterType` yönergesi, ana sayfanın ya da dosya yolunun tür adını kabul edebilir. `AddProduct.aspx` sayfanın ana sayfa olarak `Site.master` kullandığını belirtmek için, `AddProduct.aspx`en üstüne aşağıdaki yönergeyi ekleyin:

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample9.aspx)]

Bu yönerge, ASP.NET altyapısına `Master`adlı bir özellik aracılığıyla ana sayfaya kesin olarak yazılmış bir başvuru eklemesini söyler. `@MasterType` yönergesi yerine, `Site.master` ana sayfanın ortak özelliklerini ve yöntemlerini, herhangi bir yayını olmadan doğrudan `Master` özelliği aracılığıyla çağırabiliriz.

> [!NOTE]
> `@MasterType` yönergesini atlarsanız, sözdizimi `Page.Master` ve `Master` aynı şeyi döndürür: sayfanın ana sayfasına gevşek olarak yazılmış bir nesne. `@MasterType` yönergesini eklerseniz `Master` belirtilen ana sayfaya kesin olarak yazılmış bir başvuru döndürür. Ancak `Page.Master`, yine de gevşek olarak yazılmış bir başvuru döndürür. Bu durumun neden olduğu ve `@MasterType` yönergesi dahil `Master` özelliğinin nasıl oluşturulduğu hakkında daha fazla bilgi için, bkz. [ASP.NET 2,0 ' de](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx) [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx)'un blog girdisi`@MasterType`.

### <a name="updating-the-master-page-after-adding-a-new-product"></a>Yeni ürün eklendikten sonra ana sayfayı güncelleştirme

Artık, bir ana sayfanın ortak özelliklerini ve yöntemlerini bir içerik sayfasından nasıl çağırabileceğinizi öğrendiğimiz için, yeni bir ürün eklendikten sonra ana sayfanın yenilenmesi için `AddProduct.aspx` sayfasını güncelleştirmeye hazır hale getiriyoruz. Adım 4 ' ün başlangıcında, yeni ürün veritabanına eklendikten hemen sonra çalıştırılan DetailsView denetiminin `ItemInserting` olayı için bir olay işleyicisi oluşturdunuz. Aşağıdaki kodu bu olay işleyicisine ekleyin:

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample10.vb)]

Yukarıdaki kod hem gevşek türü belirlenmiş `Page.Master` özelliğini hem de kesin türü belirtilmiş `Master` özelliğini kullanır. `GridMessageText` özelliğinin "*ProductName* to Grid 'e eklenmiş" olarak ayarlandığını unutmayın. Yeni eklenen ürünün değerlerine `e.Values` koleksiyonu aracılığıyla erişilebilir. Gördüğünüz gibi, tam eklenen `ProductName` değerine `e.Values("ProductName")`aracılığıyla erişilir.

Şekil 8 ' de, veritabanına yeni bir ürün-Scott 'ın soda ' i eklendikten hemen sonra `AddProduct.aspx` sayfası gösterilir. Yeni eklenen ürün adının ana sayfanın etiketinde Not edileceğini ve GridView 'un ürünü ve fiyatını içerecek şekilde yenilendiğini unutmayın.

[Ana sayfanın etiketi ve GridView ![, tam eklenen ürünü gösterir](interacting-with-the-master-page-from-the-content-page-vb/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image22.png)

**Şekil 08**: ana sayfanın etiketi ve GridView, tek eklenen ürünü gösterir ([tam boyutlu görüntüyü görüntülemek için tıklayın](interacting-with-the-master-page-from-the-content-page-vb/_static/image24.png))

## <a name="summary"></a>Özet

İdeal olarak, bir ana sayfa ve içerik sayfaları diğerinden tamamen ayrıdır ve etkileşim düzeyi gerektirmez. Ana sayfalar ve içerik sayfaları bu hedefle birlikte tasarlanmalıdır, ancak bir içerik sayfasının ana sayfasıyla arabirim olması gereken birçok yaygın senaryo vardır. En yaygın nedenlerden biri, ana sayfanın belirli bir bölümünü güncelleştirme etrafında, içerik sayfasında transpired olan bazı eylemlere göre görüntüler.

İyi haber, bir içerik sayfasının programlı olarak ana sayfasıyla etkileşimde bulunması görece bir işlemdir. Ana sayfada bir içerik sayfası tarafından çağrılması gereken işlevselliği kapsülleyen ortak özellikler veya yöntemler oluşturarak başlayın. Ardından içerik sayfasında, gevşek olarak yazılmış `Page.Master` özelliği aracılığıyla ana sayfanın özelliklerine ve yöntemlerine erişin veya ana sayfaya kesin olarak yazılmış bir başvuru oluşturmak için `@MasterType` yönergesini kullanın.

Sonraki öğreticide, ana sayfanın programlama yoluyla içerik sayfalarından biriyle nasıl etkileşime gireceğini inceleyeceğiz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET 'deki verilere erişme ve verileri güncelleştirme](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET ana sayfaları: Ipuçları, püf noktaları ve tuzaklar](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 2,0 ' de `@MasterType`](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [Içerik ve ana sayfalar arasında bilgi geçirme](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET öğreticilerde verilerle çalışma](../../data-access/index.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 3,5 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)ister. Scott 'a [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni, Zack Jones idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](control-id-naming-in-content-pages-vb.md)
> [İleri](interacting-with-the-content-page-from-the-master-page-vb.md)
