---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: ObjectDataSource 'un parametre değerlerini programlı olarak ayarlama (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, tek bir giriş parametresi kabul eden ve verileri döndüren DAL ve BLL 'e bir yöntem ekleme bölümüne bakacağız. Örnek bu parametreyi ayarlar...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: f1dd50f46528e8dd51f85e503604d3f0dbc21ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577058"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a>ObjectDataSource Parametre Değerlerini Programlı Olarak Ayarlama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe) veya [PDF 'yi indirin](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)

> Bu öğreticide, tek bir giriş parametresi kabul eden ve verileri döndüren DAL ve BLL 'e bir yöntem ekleme bölümüne bakacağız. Örnek bu parametreyi programlı olarak ayarlar.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](declarative-parameters-vb.md)gördüğünüz gibi, bir dizi seçenek bildirimli olarak parametre değerlerini ObjectDataSource 'un yöntemlerine geçirmek için kullanılabilir. Parametre değeri sabit kodluysa, sayfadaki bir Web denetiminden gelir veya bir veri kaynağı `Parameter` nesnesi tarafından okunabilen başka bir kaynakta yer alıyorsa, bu değer bir kod satırı yazmadan giriş parametresine bağlanabilir.

Ancak, parametre değeri, yerleşik veri kaynağı `Parameter` nesnelerinden biri tarafından zaten hesaba katılmış olmayan bir kaynaktan geldiği zaman olabilir. Sitemiz Kullanıcı hesapları, oturum açmış olan ziyaretçi Kullanıcı KIMLIĞINE göre parametresini ayarlamak isteyebilir. Ya da bir parametre değerini, ObjectDataSource 'un temel alınan nesnesinin yöntemine göndermeden önce özelleştirmeniz gerekebilir.

ObjectDataSource 'un `Select` yöntemi çağrıldığında, ObjectDataSource önce kendi [seçme olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)oluşturur. ObjectDataSource 'un temel alınan nesnesinin yöntemi çağrılır. Bu işlem tamamlandıktan sonra, ObjectDataSource 'un [Seçili olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) harekete geçirilir (Şekil 1 Bu olay dizisini gösterir). ObjectDataSource 'un temel alınan nesne yöntemine geçirilen parametre değerleri, `Selecting` olayı için bir olay işleyicisinde ayarlanabilir veya özelleştirilebilir.

[ObjectDataSource 'un seçili olduğunu ![ve temel alınan nesnenin yöntemi çağrıldıktan önce ve sonra harekete geçirilen olayları seçme](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)

**Şekil 1**: ObjectDataSource 'un `Selected` ve `Selecting` olayları, temel alınan nesnenin yöntemi çağrılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png))

Bu öğreticide, `Integer` türünde `Month`tek bir giriş parametresi kabul eden DAL ve BLL ' ye bir yöntem ekleme ve bu çalışanların, belirtilen `Month`kendi istihdam etmelerine sahip olan çalışanlarla doldurulmuş bir `EmployeesDataTable` nesnesi döndüreceğiz. Örneğimiz bu parametreyi, geçerli aya göre programlı bir şekilde ayarlayacaktır ve "çalışan yıldönümlerine bu ay" bir listesini gösterir.

Haydi başlayın!

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>1\. Adım:`EmployeesTableAdapter` bir yöntem ekleme

İlk örneğimiz için `HireDate` belirli bir ayda gerçekleşen çalışanları almak için bir yol eklememiz gerekiyor. Mimarimize uygun olarak bu işlevselliği sağlamak için öncelikle uygun SQL ifadesiyle eşleşen `EmployeesTableAdapter` bir yöntem oluşturmamız gerekir. Bunu gerçekleştirmek için, Northwind türü belirtilmiş veri kümesini açarak başlayın. `EmployeesTableAdapter` etiketine sağ tıklayın ve sorgu Ekle ' yi seçin.

[![yeni bir sorgu eklemek için EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)

**Şekil 2**: `EmployeesTableAdapter` yeni bir sorgu ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))

Satırları döndüren bir SQL ifadesini eklemeyi seçin. `SELECT` belirtme ekranına ulaştığınızda, `EmployeesTableAdapter` için varsayılan `SELECT` ifade zaten yüklenir. `WHERE` yan tümcesine eklemeniz yeterlidir: `WHERE DATEPART(m, HireDate) = @Month`. [Datepart](https://msdn.microsoft.com/library/ms174420.aspx) , `datetime` türünün belirli bir tarih kısmını döndüren bir T-SQL işlevidir; Bu durumda, `HireDate` sütunun ayını döndürmek için `DATEPART` kullandık.

[![yalnızca HireDate sütununun @HiredBeforeDate parametresine eşit veya daha küçük olduğu satırları döndürür](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)

**Şekil 3**: yalnızca `HireDate` sütununun `@HiredBeforeDate` parametresine eşit veya daha küçük olduğu satırları Döndür ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))

Son olarak, `FillBy` ve `GetDataBy` yöntem adlarını sırasıyla `FillByHiredDateMonth` ve `GetEmployeesByHiredDateMonth`olarak değiştirin.

[![, FillBy ve GetDataBy 'Tan daha uygun yöntem adları seçin](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)

**Şekil 4**: `FillBy` ve `GetDataBy` daha uygun yöntem adlarını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))

Sihirbazı tamamlayıp veri kümesinin Tasarım yüzeyine dönmek için son ' a tıklayın. `EmployeesTableAdapter`, belirli bir ayda işe alınan çalışanlara erişmek için yeni bir yöntemler kümesi içermelidir.

[![, yeni yöntemler veri kümesinin Tasarım Yüzeyi görünür](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)

**Şekil 5**: yeni yöntemler veri kümesinin Tasarım yüzeyi görünür ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png))

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>2\. Adım:`GetEmployeesByHiredDateMonth(month)`yöntemini Iş mantığı katmanına ekleme

Uygulama mimarimiz iş mantığı ve veri erişim mantığı için ayrı bir katman kullandığından, belirli bir tarihten önce işe alınan çalışanları almak için DAL 'e çağıran BLL 'larımıza bir yöntem eklememiz gerekir. `EmployeesBLL.vb` dosyasını açın ve aşağıdaki yöntemi ekleyin:

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

Bu sınıftaki diğer yöntemlerimizde olduğu gibi, `GetEmployeesByHiredDateMonth(month)` yalnızca DAL içine çağrı yaparak sonuçları döndürür.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>3\. Adım: Istihdam yıldönümü bu ay olan çalışanları görüntüleme

Bu örnek için son adımımız, bu ay için istihdam yıldönümü olan çalışanları görüntülemektir. `BasicReporting` klasöründeki `ProgrammaticParams.aspx` sayfasına bir GridView ekleyerek başlayın ve veri kaynağı olarak yeni bir ObjectDataSource ekleyin. `SelectMethod` `GetEmployeesByHiredDateMonth(month)`olarak ayarlanan `EmployeesBLL` sınıfını kullanacak şekilde ObjectDataSource 'ı yapılandırın.

[![EmployeesBLL sınıfını kullanın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)

**Şekil 6**: `EmployeesBLL` sınıfını kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))

[GetEmployeesByHiredDateMonth (month) yönteminden ![seçin](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)

**Şekil 7**: `GetEmployeesByHiredDateMonth(month)` yönteminden seçim yapın ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))

Son ekran, `month` parametre değerinin kaynağını sağlamamızı ister. Bu değeri program aracılığıyla ayarlayacağız, parametre kaynağını varsayılan None seçeneğine bırakın ve son ' a tıklayın.

[Parametre kaynağı None olarak ayarlanmış ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)

**Şekil 8**: parametre kaynağını yok olarak bırakın ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))

Bu, ObjectDataSource 'un `SelectParameters` koleksiyonunda belirtilen bir değere sahip olmayan bir `Parameter` nesnesi oluşturur.

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

Bu değeri programlı bir şekilde ayarlamak için, ObjectDataSource 'un `Selecting` olayı için bir olay işleyicisi oluşturmanız gerekir. Bunu gerçekleştirmek için Tasarım görünümü gidin ve ObjectDataSource 'a çift tıklayın. Alternatif olarak, ObjectDataSource ' ı seçin, Özellikler penceresi gidin ve şimşek simgesine tıklayın. Sonra, `Selecting` olayının yanındaki TextBox ' a çift tıklayın ya da kullanmak istediğiniz olay işleyicisinin adını yazın. Üçüncü bir seçenek olarak, sayfanın arka plan kod sınıfının en üstündeki iki açılan listeden ObjectDataSource ve onun `Selecting` olayını seçerek olay işleyicisini oluşturabilirsiniz.

![Web denetiminin olaylarını listelemek için Özellikler penceresinde şimşek simgesine tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

**Şekil 9**: Web denetiminin olaylarını listelemek Için Özellikler penceresinde şimşek simgesine tıklayın

Üç yaklaşımdan bazıları, sayfanın arka plan kod sınıfına olan ObjectDataSource 'un `Selecting` olayı için yeni bir olay işleyicisi ekler. Bu olay işleyicisinde, `e.InputParameters(parameterName)`kullanarak parametre değerlerini okuyup yazalım, burada *`parameterName`* `<asp:Parameter>` etiketindeki `Name` özniteliğinin değeridir (`InputParameters` koleksiyonu, `e.InputParameters(index)`olarak da oluşturulabilir). `month` parametresini geçerli aya ayarlamak için aşağıdakini `Selecting` olay işleyicisine ekleyin:

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

Bu sayfayı bir tarayıcı aracılığıyla ziyaret ederken, bu ay (Mart), Şirket 1994 ' den beri olan bu ayda yalnızca bir çalışan olduğunu görebiliriz.

[Bu aya ait yıldönümlerini gösterilen çalışanları ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)

**Şekil 10**: Bu ayın yıldönümlerini gösterilen çalışanlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))

## <a name="summary"></a>Özet

ObjectDataSource 'un parametrelerinin değerleri genellikle bildirimli olarak ayarlanabilir, ancak kod satırı gerekmeden parametre değerlerini programlı bir şekilde ayarlamak kolaydır. Tüm yapmanız gereken, temel alınan nesnenin yöntemi çağrılmadan önce başlatılan ve bir veya daha fazla parametre için değerleri el ile `InputParameters` koleksiyonu aracılığıyla harekete geçirilen `Selecting` olayı için bir olay işleyicisi oluşturmaktır.

Bu öğreticide temel raporlama bölümü sonlanır. [Sonraki öğreticide](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) , ziyaretçilerin verileri filtrelemesine ve bir ana rapordan ayrıntı raporuna gidebilmesine izin verme tekniklerine bakacağımız filtreleme ve ana Ayrıntılar senaryolarının bölümü açılır.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Öncekini](declarative-parameters-vb.md)
