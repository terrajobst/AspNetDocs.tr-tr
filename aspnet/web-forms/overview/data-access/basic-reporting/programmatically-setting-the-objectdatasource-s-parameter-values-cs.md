---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
title: ObjectDataSource 'un parametre değerlerini programlı olarak ayarlama (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, tek bir giriş parametresi kabul eden ve verileri döndüren DAL ve BLL 'e bir yöntem ekleme bölümüne bakacağız. Örnek bu parametreyi ayarlar...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1c4588bb-255d-4088-b319-5208da756f4d
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs
msc.type: authoredcontent
ms.openlocfilehash: 8aa57172abcfc779fa74b128ad76d42c41dc5b98
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74602142"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-c"></a>ObjectDataSource Parametre Değerlerini Programlı Olarak Ayarlama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_6_CS.exe) veya [PDF 'yi indirin](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/datatutorial06cs1.pdf)

> Bu öğreticide, tek bir giriş parametresi kabul eden ve verileri döndüren DAL ve BLL 'e bir yöntem ekleme bölümüne bakacağız. Örnek bu parametreyi programlı olarak ayarlar.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](declarative-parameters-cs.md)gördüğünüz gibi, bir dizi seçenek bildirimli olarak parametre değerlerini ObjectDataSource 'un yöntemlerine geçirmek için kullanılabilir. Parametre değeri sabit kodluysa, sayfadaki bir Web denetiminden gelir veya bir veri kaynağı `Parameter` nesnesi tarafından okunabilen başka bir kaynakta yer alıyorsa, bu değer bir kod satırı yazmadan giriş parametresine bağlanabilir.

Ancak, parametre değeri, yerleşik veri kaynağı `Parameter` nesnelerinden biri tarafından zaten hesaba katılmış olmayan bir kaynaktan geldiği zaman olabilir. Sitemiz Kullanıcı hesapları, oturum açmış olan ziyaretçi Kullanıcı KIMLIĞINE göre parametresini ayarlamak isteyebilir. Ya da bir parametre değerini, ObjectDataSource 'un temel alınan nesnesinin yöntemine göndermeden önce özelleştirmeniz gerekebilir.

ObjectDataSource 'un `Select` yöntemi çağrıldığında, ObjectDataSource önce kendi [seçme olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)oluşturur. ObjectDataSource 'un temel alınan nesnesinin yöntemi çağrılır. Bu işlem tamamlandıktan sonra, ObjectDataSource 'un [Seçili olayını](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) harekete geçirilir (Şekil 1 Bu olay dizisini gösterir). ObjectDataSource 'un temel alınan nesne yöntemine geçirilen parametre değerleri, `Selecting` olayı için bir olay işleyicisinde ayarlanabilir veya özelleştirilebilir.

[ObjectDataSource 'un seçili olduğunu ![ve temel alınan nesnenin yöntemi çağrıldıktan önce ve sonra harekete geçirilen olayları seçme](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image1.png)

**Şekil 1**: ObjectDataSource 'un `Selected` ve `Selecting` olayları, temel alınan nesnenin yöntemi çağrılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image3.png))

Bu öğreticide, `int` türünde `Month`tek bir giriş parametresi kabul eden DAL ve BLL ' ye bir yöntem ekleme ve bu çalışanların, belirtilen `Month`kendi istihdam etmelerine sahip olan çalışanlarla doldurulmuş bir `EmployeesDataTable` nesnesi döndüreceğiz. Örneğimiz bu parametreyi, geçerli aya göre programlı bir şekilde ayarlayacaktır ve "çalışan yıldönümlerine bu ay" bir listesini gösterir.

Haydi başlayın!

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>1\. Adım:`EmployeesTableAdapter` bir yöntem ekleme

İlk örneğimiz için `HireDate` belirli bir ayda gerçekleşen çalışanları almak için bir yol eklememiz gerekiyor. Mimarimize uygun olarak bu işlevselliği sağlamak için öncelikle uygun SQL ifadesiyle eşleşen `EmployeesTableAdapter` bir yöntem oluşturmamız gerekir. Bunu gerçekleştirmek için, Northwind türü belirtilmiş veri kümesini açarak başlayın. `EmployeesTableAdapter` etiketine sağ tıklayın ve sorgu Ekle ' yi seçin.

[![yeni bir sorgu eklemek için EmployeesTableAdapter](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image4.png)

**Şekil 2**: `EmployeesTableAdapter` yeni bir sorgu ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image6.png))

Satırları döndüren bir SQL ifadesini eklemeyi seçin. `SELECT` belirtme ekranına ulaştığınızda, `EmployeesTableAdapter` için varsayılan `SELECT` ifade zaten yüklenir. `WHERE` yan tümcesine eklemeniz yeterlidir: `WHERE DATEPART(m, HireDate) = @Month`. [Datepart](https://msdn.microsoft.com/library/ms174420.aspx) , `datetime` türünün belirli bir tarih kısmını döndüren bir T-SQL işlevidir; Bu durumda, `HireDate` sütunun ayını döndürmek için `DATEPART` kullandık.

[![yalnızca HireDate sütununun @HiredBeforeDate parametresine eşit veya daha küçük olduğu satırları döndürür](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image7.png)

**Şekil 3**: yalnızca `HireDate` sütununun `@HiredBeforeDate` parametresine eşit veya daha küçük olduğu satırları Döndür ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image9.png))

Son olarak, `FillBy` ve `GetDataBy` yöntem adlarını sırasıyla `FillByHiredDateMonth` ve `GetEmployeesByHiredDateMonth`olarak değiştirin.

[![, FillBy ve GetDataBy 'Tan daha uygun yöntem adları seçin](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image10.png)

**Şekil 4**: `FillBy` ve `GetDataBy` daha uygun yöntem adlarını seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image12.png))

Sihirbazı tamamlayıp veri kümesinin Tasarım yüzeyine dönmek için son ' a tıklayın. `EmployeesTableAdapter`, belirli bir ayda işe alınan çalışanlara erişmek için yeni bir yöntemler kümesi içermelidir.

[![, yeni yöntemler veri kümesinin Tasarım Yüzeyi görünür](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image13.png)

**Şekil 5**: yeni yöntemler veri kümesinin Tasarım yüzeyi görünür ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image15.png))

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>2\. Adım:`GetEmployeesByHiredDateMonth(month)`yöntemini Iş mantığı katmanına ekleme

Uygulama mimarimiz iş mantığı ve veri erişim mantığı için ayrı bir katman kullandığından, belirli bir tarihten önce işe alınan çalışanları almak için DAL 'e çağıran BLL 'larımıza bir yöntem eklememiz gerekir. `EmployeesBLL.cs` dosyasını açın ve aşağıdaki yöntemi ekleyin:

[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample1.cs)]

Bu sınıftaki diğer yöntemlerimizde olduğu gibi, `GetEmployeesByHiredDateMonth(month)` yalnızca DAL içine çağrı yaparak sonuçları döndürür.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>3\. Adım: Istihdam yıldönümü bu ay olan çalışanları görüntüleme

Bu örnek için son adımımız, bu ay için istihdam yıldönümü olan çalışanları görüntülemektir. `BasicReporting` klasöründeki `ProgrammaticParams.aspx` sayfasına bir GridView ekleyerek başlayın ve veri kaynağı olarak yeni bir ObjectDataSource ekleyin. `SelectMethod` `GetEmployeesByHiredDateMonth(month)`olarak ayarlanan `EmployeesBLL` sınıfını kullanacak şekilde ObjectDataSource 'ı yapılandırın.

[![EmployeesBLL sınıfını kullanın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image16.png)

**Şekil 6**: `EmployeesBLL` sınıfını kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image18.png))

[GetEmployeesByHiredDateMonth (month) yönteminden ![seçin](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image19.png)

**Şekil 7**: `GetEmployeesByHiredDateMonth(month)` yönteminden seçim yapın ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image21.png))

Son ekran, `month` parametre değerinin kaynağını sağlamamızı ister. Bu değeri program aracılığıyla ayarlayacağız, parametre kaynağını varsayılan None seçeneğine bırakın ve son ' a tıklayın.

[Parametre kaynağı None olarak ayarlanmış ![](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image22.png)

**Şekil 8**: parametre kaynağını yok olarak bırakın ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image24.png))

Bu, ObjectDataSource 'un `SelectParameters` koleksiyonunda belirtilen bir değere sahip olmayan bir `Parameter` nesnesi oluşturur.

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample2.aspx)]

Bu değeri programlı bir şekilde ayarlamak için, ObjectDataSource 'un `Selecting` olayı için bir olay işleyicisi oluşturmanız gerekir. Bunu gerçekleştirmek için Tasarım görünümü gidin ve ObjectDataSource 'a çift tıklayın. Alternatif olarak, ObjectDataSource ' ı seçin, Özellikler penceresi gidin ve şimşek simgesine tıklayın. Sonra, `Selecting` olayının yanındaki TextBox ' a çift tıklayın ya da kullanmak istediğiniz olay işleyicisinin adını yazın.

![Web denetiminin olaylarını listelemek için Özellikler penceresinde şimşek simgesine tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image25.png)

**Şekil 9**: Web denetiminin olaylarını listelemek Için Özellikler penceresinde şimşek simgesine tıklayın

Her iki yaklaşım da, sayfanın arka plan kod sınıfına olan ObjectDataSource 'un `Selecting` olayı için yeni bir olay işleyicisi ekler. Bu olay işleyicisinde, `e.InputParameters[parameterName]`kullanarak parametre değerlerini okuyup yazalım, burada *`parameterName`* `<asp:Parameter>` etiketindeki `Name` özniteliğinin değeridir (`InputParameters` koleksiyonu, `e.InputParameters[index]`olarak da oluşturulabilir). `month` parametresini geçerli aya ayarlamak için aşağıdakini `Selecting` olay işleyicisine ekleyin:

[!code-csharp[Main](programmatically-setting-the-objectdatasource-s-parameter-values-cs/samples/sample3.cs)]

Bu sayfayı bir tarayıcı aracılığıyla ziyaret ederken, bu ay (Mart), Şirket 1994 ' den beri olan bu ayda yalnızca bir çalışan olduğunu görebiliriz.

[Bu aya ait yıldönümlerini gösterilen çalışanları ![](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image26.png)

**Şekil 10**: Bu ayın yıldönümlerini gösterilen çalışanlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](programmatically-setting-the-objectdatasource-s-parameter-values-cs/_static/image28.png))

## <a name="summary"></a>Özet

ObjectDataSource 'un parametrelerinin değerleri genellikle bildirimli olarak ayarlanabilir, ancak kod satırı gerekmeden parametre değerlerini programlı bir şekilde ayarlamak kolaydır. Tüm yapmanız gereken, temel alınan nesnenin yöntemi çağrılmadan önce başlatılan ve bir veya daha fazla parametre için değerleri el ile `InputParameters` koleksiyonu aracılığıyla harekete geçirilen `Selecting` olayı için bir olay işleyicisi oluşturmaktır.

Bu öğreticide temel raporlama bölümü sonlanır. [Sonraki öğreticide](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) , ziyaretçilerin verileri filtrelemesine ve bir ana rapordan ayrıntı raporuna gidebilmesine izin verme tekniklerine bakacağımız filtreleme ve ana Ayrıntılar senaryolarının bölümü açılır.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](declarative-parameters-cs.md)
> [İleri](displaying-data-with-the-objectdatasource-vb.md)
