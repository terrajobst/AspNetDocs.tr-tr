---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: GridView denetiminde TemplateFields kullanma (C#) | Microsoft Docs
author: rick-anderson
description: Esneklik sağlamak için GridView, şablon kullanarak işleyen TemplateField alanını sunar. Bir şablon statik HTML, Web denetimleri ve... karışımı içerebilir.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ec17a16d7bb487d1c5cacf2d5971bbeffc1ba031
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627785"
---
# <a name="using-templatefields-in-the-gridview-control-c"></a>GridView Denetiminde TemplateField Kullanma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe) veya [PDF 'yi indirin](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> Esneklik sağlamak için GridView, şablon kullanarak işleyen TemplateField alanını sunar. Bir şablon statik HTML, Web denetimleri ve veri bağlama söz dizimi karışımını içerebilir. Bu öğreticide, GridView denetimiyle daha fazla özelleştirmeye ulaşmak için TemplateField 'ın nasıl kullanılacağını inceleyeceğiz.

## <a name="introduction"></a>Giriş

GridView, verilerin nasıl görüntüleneceği ile birlikte `DataSource` hangi özelliklerin işlenmiş çıkışa ekleneceğini belirten bir alan kümesinden oluşur. En basit alan türü, metin olarak bir veri değeri görüntüleyen BoundField değeridir. Diğer alan türleri, alternatif HTML öğelerini kullanarak verileri görüntüler. CheckBoxField, örneğin, denetlenen durumu belirtilen veri alanının değerine bağlı olan bir CheckBox olarak işler; ImageField, görüntü kaynağı belirtilen veri alanını temel alan bir görüntü oluşturur. Durumu temel alınan bir veri alanı değerine bağlı olan köprüler ve düğmeler, HyperLinkField ve ButtonField alan türleri kullanılarak oluşturulabilir.

CheckBoxField, ImageField, HyperLinkField ve ButtonField alan türleri verilerin alternatif bir görünümü için izin verirken, biçimlendirme açısından oldukça sınırlı kalır. Bir CheckBoxField yalnızca tek bir onay kutusu görüntüleyebilir, ancak bir ImageField yalnızca tek bir resim görüntüleyebilir. Belirli bir alanın, farklı veri alanı değerlerine göre bir metin, onay kutusu *ve* görüntü görüntülemesi gerektiğinde ne olacak? Veya onay kutusu, görüntü, köprü ya da düğme dışında bir Web denetimi kullanarak verileri göstermek isteseydi ne olursa? Ayrıca, BoundField görünümünü tek bir veri alanı olarak sınırlandırır. Tek bir GridView sütununda iki veya daha fazla veri alanı değeri göstermek istiyorsam ne olacak?

Bu esneklik düzeyine uyum sağlamak için GridView, *şablon*kullanarak Işleyen TemplateField alanını sunmaktadır. Bir şablon statik HTML, Web denetimleri ve veri bağlama söz dizimi karışımını içerebilir. Ayrıca, TemplateField, farklı durumlar için işlemeyi özelleştirmek üzere kullanılabilecek çeşitli şablonlar içerir. Örneğin, `ItemTemplate` her satır için hücreyi işlemek üzere varsayılan olarak kullanılır, ancak `EditItemTemplate` şablonu veri düzenlenirken arabirimi özelleştirmek için kullanılabilir.

Bu öğreticide, GridView denetimiyle daha fazla özelleştirmeye ulaşmak için TemplateField 'ın nasıl kullanılacağını inceleyeceğiz. [Önceki öğreticide](custom-formatting-based-upon-data-cs.md) , `DataBound` ve `RowDataBound` olay işleyicilerini kullanarak, temel alınan verilere göre biçimlendirmeyi özelleştirmeyi gördük. Temel verileri temel alan biçimlendirmeyi özelleştirmenin başka bir yolu da bir şablon içinden biçimlendirme yöntemlerini çağırıyor. Bu öğreticide da bu teknikte bakacağız.

Bu öğretici için, bir çalışanlar listesinin görünümünü özelleştirmek üzere TemplateFields kullanacağız. Özellikle, tüm çalışanları listeliyoruz, ancak çalışanın ilk ve son adlarını tek bir sütunda, bir takvim denetimindeki işe alma tarihine ve şirkette kaç gün çalıştırıldıklarından emin olan bir durum sütununa görüntülenecektir.

[Gösterimi özelleştirmek için üç TemplateField ![kullanılır](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**Şekil 1**: ekranı özelleştirmek Için üç Templatefields kullanılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image3.png))

## <a name="step-1-binding-the-data-to-the-gridview"></a>1\. Adım: verileri GridView 'a bağlama

Görünümü özelleştirmek için TemplateFields kullanmanız gereken raporlama senaryolarında, ilk olarak yalnızca BoundFields içeren bir GridView denetimi oluşturup yeni TemplateFields eklemek veya var olan BoundFields alanlarını öğesine dönüştürmek için en kolay şekilde Gerektiğinde TemplateFields. Bu nedenle, tasarımcı aracılığıyla sayfaya bir GridView ekleyerek ve çalışanların listesini döndüren bir ObjectDataSource 'a bağlayarak bu öğreticiyi başlaalım. Bu adımlar, çalışan alanlarının her biri için BoundFields içeren bir GridView oluşturacak.

`GridViewTemplateField.aspx` sayfasını açın ve araç kutusundan bir GridView 'ı tasarımcı üzerine sürükleyin. GridView 'un akıllı etiketinden `EmployeesBLL` sınıfının `GetEmployees()` yöntemini çağıran yeni bir ObjectDataSource denetimi eklemeyi seçin.

[GetEmployees () yöntemini çağıran yeni bir ObjectDataSource denetimi eklemek ![](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**Şekil 2**: `GetEmployees()` yöntemini çağıran yeni bir ObjectDataSource denetimi ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image6.png))

GridView 'un bu şekilde bağlanması, her bir çalışan özelliği için otomatik olarak bir BoundField ekler: `EmployeeID`, `LastName`, `FirstName`, `Title`, `HireDate`, `ReportsTo`ve `Country`. Bu rapor için `EmployeeID`, `ReportsTo`veya `Country` özelliklerini görüntüleme konusunda bir sorun oluşturmamalıdır. Bu BoundFields alanlarını kaldırmak için şunları yapabilirsiniz:

- Bu iletişim kutusunu açmak için GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayın alanları iletişim kutusunu kullanın. Ardından sol alt taraftaki listeden BoundFields alanlarını seçin ve sonra da BoundField öğesini kaldırmak için kırmızı X düğmesine tıklayın.
- GridView 'un bildirim temelli sözdizimini kaynak görünümünden el ile düzenleyin, kaldırmak istediğiniz BoundField için `<asp:BoundField>` öğesini silin.

`EmployeeID`, `ReportsTo`ve `Country` BoundFields alanlarını kaldırdıktan sonra, GridView 'un biçimlendirmesi şöyle görünmelidir:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

Sürmekte olan ilerlemeyi bir tarayıcıda görüntülemek için bir dakikanızı ayırın. Bu noktada, her çalışana ait bir kayıt ve dört sütun için bir kayıt içeren bir tablo görmeniz gerekir: biri çalışanın soyadı, biri kendi adı, biri unvanları ve diğeri ise işe alınma tarihi için.

[![her çalışan için LastName, FirstName, title ve HireDate alanları görüntülenir](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**Şekil 3**: `LastName`, `FirstName`, `Title`ve `HireDate` alanları her çalışan için görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image9.png))

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>2\. Adım: tek bir sütunda Ilk ve son Isimleri görüntüleme

Şu anda, her çalışanın adı ve soyadı ayrı bir sütunda görüntülenir. Bunun yerine tek bir sütunda birleştirmek iyi olabilir. Bunu gerçekleştirmek için, bir TemplateField kullanmanız gerekir. Yeni bir TemplateField ekleyebilir, buna gerekli biçimlendirme ve veri bağlama söz dizimini ekleyebilir, sonra `FirstName` ve `LastName` BoundFields alanlarını silebilir veya `FirstName` BoundField alanını bir TemplateField 'a dönüştürebiliriz, TemplateField 'ı `LastName` değeri içerecek şekilde düzenleyebilir ve ardından `LastName` BoundField öğesini kaldırabilirsiniz.

Her iki yaklaşım da aynı sonucu artırır, ancak dönüştürme otomatik olarak bir `ItemTemplate` ve `EditItemTemplate` bir Web denetimleri ve veri bağlama sözdizimiyle, BoundField 'ın görünüm ve işlevselliğini taklit etmek için bir ve ekler. Bunun avantajı, dönüştürme işlemi bizim için çalışmanın bir kısmını gerçekleştirmesinden önce TemplateField ile daha az iş yapmamız gerekir.

Var olan bir BoundField öğesini TemplateField 'a dönüştürmek için GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayın, alanlar iletişim kutusu açılır. Sol alt köşedeki listeden dönüştürülecek olan BoundField öğesini seçin ve sağ alt köşedeki "Bu alanı TemplateField 'a Dönüştür" bağlantısına tıklayın.

[Alanlar Iletişim kutusunda bir BoundField öğesini TemplateField 'A dönüştürmek ![](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**Şekil 4**: alanlar iletişim kutusundan bir BoundField öğesini TemplateField 'a Dönüştür ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image12.png))

Devam edin ve `FirstName` BoundField öğesini TemplateField öğesine dönüştürün. Bu değişiklikten sonra tasarımcıda Perceptive fark yoktur. Bunun nedeni, BoundField öğesinin bir TemplateField 'a dönüştürülmesi, BoundField 'un görünüm ve yapısını tutan bir TemplateField oluşturur. Bu noktada tasarımcıda hiçbir görsel fark bulunmadığından, bu dönüştürme işlemi aşağıdaki TemplateField söz dizimine sahip olan BoundField 'in bildirime dayalı sözdizimini `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />` değiştirdi:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

Görebileceğiniz gibi, TemplateField, `Text` özelliği `FirstName` veri alanının değerine ayarlanmış bir etikete sahip bir `ItemTemplate` ve `Text` özelliği `FirstName` veri alanına ayarlanmış bir TextBox denetimiyle bir `EditItemTemplate` olan iki şablondan oluşur. Veri bağlama söz dizimi-`<%# Bind("fieldName") %>`-veri alanı *`fieldName`* belirtilen Web denetimi özelliğine bağlandığını gösterir.

Bu TemplateField 'a `LastName` veri alanı değerini eklemek için, `ItemTemplate` başka bir etiket Web denetimi eklemesi ve `Text` özelliğini `LastName`olarak bağlamanız gerekir. Bu, el ile ya da tasarımcı aracılığıyla gerçekleştirilebilir. Bunu el ile yapmak için, `ItemTemplate`uygun bildirime dayalı sözdizimini eklemeniz yeterlidir:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

Tasarımcı aracılığıyla eklemek için GridView 'un akıllı etiketindeki Şablonları Düzenle bağlantısına tıklayın. Bu, GridView 'un şablon düzenlemesi arabirimini görüntüler. Bu arabirimin akıllı etiketinde, GridView 'daki şablonların bir listesi bulunur. Bu noktada yalnızca bir TemplateField olduğundan, açılan listede yalnızca bir TemplateField bulunan şablonlar, `EmptyDataTemplate` ve `PagerTemplate`birlikte `FirstName` TemplateField için bu şablonlardır. Eğer belirtilmişse, GridView 'a bağlantılı verilerde sonuç yoksa GridView 'un çıkışını işlemek için `EmptyDataTemplate` şablonu kullanılır; belirtilmişse `PagerTemplate`, sayfalama destekleyen bir GridView için sayfalama arabirimini işlemek için kullanılır.

[GridView 'un şablonları tasarımcı aracılığıyla düzenlenebilirler ![](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**Şekil 5**: GridView 'un şablonları tasarımcı aracılığıyla düzenlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](using-templatefields-in-the-gridview-control-cs/_static/image15.png))

Ayrıca, `FirstName` TemplateField 'daki `LastName` göstermek için, başlık denetimini araç kutusundan, GridView 'un şablon düzenleyici arabirimindeki `FirstName` template`ItemTemplate` Field ' a sürükleyin.

[![adı TemplateField 'ın ItemTemplate 'e bir etiket Web denetimi ekleyin](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**Şekil 6**: `FirstName` TemplateField 'ın ItemTemplate 'e bir etiket Web denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image18.png))

Bu noktada, TemplateField 'a eklenen etiket Web denetiminin `Text` özelliği "etiket" olarak ayarlanmıştır. Bunun yerine, bu özelliğin `LastName` veri alanının değerine bağlanması için bunu değiştirmemiz gerekiyor. Bunu gerçekleştirmek için etiket denetiminin akıllı etiketine tıklayın ve DataBindings 'i Düzenle seçeneğini belirleyin.

[![etiketin akıllı etiketindeki DataBindings 'ı Düzenle seçeneğini belirleyin](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**Şekil 7**: etiketin akıllı etiketindeki DataBindings 'ı Düzenle seçeneğini belirleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image21.png))

Bu, DataBindings iletişim kutusunu getirir. Buradan, sol taraftaki listeden veri bağlama 'ya katılacak özelliği seçebilir ve sağ taraftaki açılan listeden verileri bağlamak için alanı seçebilirsiniz. Soldan ve `LastName` alanından `Text` özelliğini seçip Tamam ' a tıklayın.

[Text özelliğini ![LastName Data alanına bağlayın](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**Şekil 8**: `Text` özelliğini `LastName` veri alanına bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image24.png))

> [!NOTE]
> DataBindings iletişim kutusu, iki yönlü veri bağlamayı gerçekleştirip gerçekleştirmeyeceğinizi belirtmenize olanak tanır. Bunu işaretsiz bırakırsanız, `<%# Bind("LastName")%>`yerine `<%# Eval("LastName")%>` veri bağlama söz dizimi kullanılacaktır. Her iki yaklaşım da bu öğretici için uygundur. Veri eklenirken ve düzenlenirken iki yönlü veri bağlama önemli hale gelir. Ancak, yalnızca verilerin görüntülenmesi için iki yaklaşım da aynı şekilde çalışır. Sonraki öğreticilerde ayrıntılı olarak iki yönlü veri bağlamayı tartışacağız.

Bu sayfayı bir tarayıcı aracılığıyla görüntülemek için bir dakikanızı ayırın. Gördüğünüz gibi, GridView hala dört sütun içerir; Ancak `FirstName` sütunu artık `FirstName` ve `LastName` veri alanı *değerlerini listeler.*

[![hem FirstName hem de LastName değerlerinin tek bir sütunda gösterilmesi](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**Şekil 9**: hem `FirstName` hem de `LastName` değerleri tek bir sütunda gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image27.png))

Bu ilk adımı tamamlayabilmeniz için `LastName` BoundField öğesini kaldırın ve `FirstName` TemplateField `HeaderText` özelliğini "ad" olarak yeniden adlandırın. Bu değişikliklerden sonra GridView 'un bildirim temelli işaretleme aşağıdaki gibi görünmelidir:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]

[Her çalışanın adı ve soyadı ![bir sütunda görüntülenir](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**Şekil 10**: her çalışanın adı ve soyadı tek bir sütunda görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image30.png))

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>3\. Adım:`HiredDate`alanını göstermek için Takvim denetimini kullanma

Veri alanı değerini GridView 'da metin olarak görüntülemek, bir BoundField kullanarak basittir. Ancak, bazı senaryolarda veriler en iyi şekilde yalnızca metin yerine belirli bir Web denetimi kullanılarak ifade edilir. Veri görüntülemenin bu tür özelleştirmesi TemplateFields ile mümkündür. Örneğin, çalışanın işe alınma tarihini metin olarak görüntülemek yerine, bir takvim ( [Takvim denetimini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)kullanarak), işe alma tarihleri vurgulanmış olarak gösterilebilir.

Bunu gerçekleştirmek için, `HiredDate` BoundField öğesini TemplateField öğesine dönüştürerek başlayın. GridView 'un akıllı etiketine gitmeniz ve alanları Düzenle bağlantısına tıklayarak alanlar iletişim kutusu ' na tıklamanız yeterlidir. `HiredDate` BoundField öğesini seçin ve "Bu alanı TemplateField 'a Dönüştür" seçeneğine tıklayın.

[HiredDate BoundField öğesini TemplateField 'A dönüştürmek ![](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**Şekil 11**: `HiredDate` BoundField öğesini TemplateField 'a Dönüştür ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image33.png))

2\. adımda gördüğünüz gibi, bu, BoundField öğesini bir `ItemTemplate` içeren bir TemplateField ve `EditItemTemplate` `Text` özellikleri, veri bağlama söz dizimi `<%# Bind("HiredDate")%>`kullanılarak `HiredDate` değere bağlanan bir etiket ve metin kutusuyla değiştirecek.

Metnin bir takvim denetimiyle değiştirilmesini sağlamak için, etiketi kaldırarak ve Takvim denetimi ekleyerek şablonu düzenleyin. Tasarımcıdan GridView 'un akıllı etiketindeki Şablonları Düzenle ' yi seçin ve açılan listeden `HireDate` TemplateField ' `ItemTemplate` seçin. Sonra, etiket denetimini silin ve araç kutusundan bir Takvim denetimini şablon düzenlemesi arabirimine sürükleyin.

[![, bir Takvim denetimini HireDate TemplateField 'ın ItemTemplate 'e ekleme](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**Şekil 12**: `HireDate` TemplateField 'ın `ItemTemplate` Takvim denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image36.png))

Bu noktada, GridView 'daki her satır `HiredDate` TemplateField öğesinde bir Takvim denetimi içerecektir. Ancak, çalışanın gerçek `HiredDate` değeri takvim denetiminde herhangi bir yere ayarlanmadığından, her takvim denetiminin varsayılan olarak geçerli ay ve tarihi göstermesini sağlar. Bu sorunu gidermek için, her bir çalışanın `HiredDate` takvim denetiminin [SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx) ve [VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx) özelliklerine atanması gerekir.

Takvim denetiminin akıllı etiketinde DataBindings 'i Düzenle ' yi seçin. Sonra, hem `SelectedDate` hem de `VisibleDate` özelliklerini `HiredDate` veri alanına bağlayın.

[![SelectedDate ve VisibleDate özelliklerini HiredDate veri alanına bağlayın](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**Şekil 13**: `SelectedDate` ve `VisibleDate` özelliklerini `HiredDate` veri alanına bağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image39.png))

> [!NOTE]
> Takvim denetiminin seçili tarihinin görünür olması gerekmez. Örneğin, bir takvimde seçili tarih olarak 1<sup>St</sup>, 1999 Ağustos, ancak geçerli ay ve yılın gösterilmesi olabilir. Seçilen tarih ve görünür Tarih, takvim denetiminin `SelectedDate` ve `VisibleDate` özellikleri tarafından belirtilir. Hem çalışanın `HiredDate` seçip hem de gösterildiğinden emin olmak istiyoruz. bu özelliklerden her ikisini de `HireDate` veri alanına bağlamanız gerekir.

Sayfa bir tarayıcıda görüntülenirken, takvimde artık çalışanın işe alınan tarihinin ayı gösterilir ve söz konusu tarihi seçer.

[Çalışanın HiredDate 'i ![takvim denetiminde gösteriliyor](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**Şekil 14**: çalışanın `HiredDate` takvim denetiminde gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image42.png))

> [!NOTE]
> Bu nedenle şu ana kadar gördüğdiğimiz örneklerin aksine, bu öğretici için `EnableViewState` özelliği bu GridView için `false` *olarak ayarlanmıyordu* . Bu kararın nedeni, takvim denetiminin tarihleri tıklanması bir geri göndermeye neden olur ve takvimin seçili tarihini yeni tıklatılan tarihe ayarlar. GridView 'un görünüm durumu devre dışıysa, her bir geri göndermede GridView 'un verileri, temel alınan veri kaynağına yeniden bağlanır. Bu, takvimin seçili tarihinin, Kullanıcı tarafından seçilen tarihin üzerine yazılması için çalışanın `HireDate`*yeniden* başlatılmasına neden olur.

Bu öğreticide, Kullanıcı çalışanın `HireDate`güncelleştiremediğinden bu bir moot tartışmadır. Takvim denetiminin tarihleri seçilebilir olması için en iyi şekilde yapılandırılması olasıdır. Bu öğretici ne olursa olsun, belirli işlevleri sağlamak için bazı koşullarda görünüm durumunun etkinleştirilmesi gerektiğini gösterir.

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>4\. Adım: çalışanın şirket için çalıştığı gün sayısını gösterme

Şu ana kadar TemplateFields 'in iki uygulaması görüldü:

- İki veya daha fazla veri alanı değerini tek bir sütunda birleştirmek ve
- Bir veri alanı değerini metin yerine bir Web denetimi kullanarak ifade etme

TemplateFields 'in üçüncü kullanımı, GridView 'un temel alınan verileri hakkında meta verileri görüntülüyor. Örneğin, çalışanların işe alma tarihlerini göstermenin yanı sıra, işte kaç toplam gün kaldığını gösteren bir sütun da isteyebilirsiniz.

Hala, temeldeki verilerin Web sayfası raporunda, veritabanında depolanan biçimden farklı şekilde görüntülenmesi gerektiğinde senaryolar halinde TemplateFields 'in başka bir kullanımı ortaya çıkar. `Employees` tabloda, çalışanın sesemi olduğunu göstermek için karakter `M` veya `F` depolanan bir `Gender` alanı olduğunu düşünün. Bu bilgileri bir Web sayfasında görüntülerken, cinsiyetini "erkek" veya "kadın" olarak göstermek isteyebilir, yalnızca "e" veya "F" yerine.

Bu senaryoların her ikisi de, ASP.NET sayfasının arka plan kod sınıfında (veya bir `static` yöntemi olarak uygulanan ayrı bir sınıf kitaplığında), şablondan çağrılan bir *biçimlendirme yöntemi* oluşturularak işlenebilir. Bu tür bir biçimlendirme yöntemi, daha önce görülen aynı veri bağlama söz dizimi kullanılarak şablondan çağrılır. Biçimlendirme yöntemi herhangi bir sayıda parametre alabilir, ancak bir dize döndürmelidir. Bu döndürülen dize, şablona eklenen HTML 'dir.

Bu kavramı göstermek için Öğreticimizi, bir çalışanın işte kaç gün kaldığını listeleyen bir sütun gösterecek şekilde inceleyelim. Bu biçimlendirme yöntemi bir `Northwind.EmployeesRow` nesnesinde sürer ve çalışanın bir dize olarak kaç gün boyunca işe alınır. Bu yöntem, ASP.NET sayfasının arka plan kod sınıfına eklenebilir, ancak şablondan erişilebilir olması için `protected` veya `public` olarak *işaretlenmelidir* .

[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

`HiredDate` alan `NULL` veritabanı değerleri içerebildiği için öncelikle hesaplamaya geçmeden önce değerin `NULL` olmamasını sağlamalıdır. `HiredDate` değeri `NULL`, yalnızca "Unknown" dizesini döndürtik. `NULL`değilse, geçerli saat ve `HiredDate` değeri arasındaki farkı hesaplar ve gün sayısını döndürür.

Bu yöntemi kullanmak için, veri bağlama söz dizimini kullanarak GridView 'da bir TemplateField öğesinden çağırıdık. GridView 'un akıllı etiketindeki sütunları düzenle bağlantısına tıklayarak ve yeni bir TemplateField ekleyerek başlayın.

[GridView 'a yeni bir TemplateField ![ekleyin](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**Şekil 15**: GridView 'a yeni bir TemplateField ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image45.png))

Bu yeni TemplateField 'ın `HeaderText` özelliğini "Iş üzerindeki günler" ve `ItemStyle``HorizontalAlign` özelliği `Center`olarak ayarlayın. Şablondan `DisplayDaysOnJob` yöntemini çağırmak için bir `ItemTemplate` ekleyin ve aşağıdaki veri bağlama söz dizimini kullanın:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem`, `GridViewRow`bağlantılı `DataSource` kaydına karşılık gelen bir `DataRowView` nesnesi döndürür. `Row` özelliği, `DisplayDaysOnJob` yöntemine geçirilen kesin türü belirtilmiş `Northwind.EmployeesRow`döndürür. Bu veri bağlama söz dizimi doğrudan `ItemTemplate` bulunabilir (aşağıdaki bildirime dayalı sözdiziminde gösterildiği gibi) veya bir etiket Web denetiminin `Text` özelliğine atanabilir.

> [!NOTE]
> Alternatif olarak, bir `EmployeesRow` örneği geçirmek yerine `<%# DisplayDaysOnJob(Eval("HireDate")) %>`kullanarak `HireDate` değerini geçebiliriz. Ancak `Eval` yöntemi bir `object`döndürür, bu nedenle `DisplayDaysOnJob` Yöntem imzamızı `object`türünde bir giriş parametresi kabul edecek şekilde değiştirmeniz gerekir. `Employees` tablosundaki `HireDate` sütunu `NULL` değer içerebildiğinden, `Eval("HireDate")` çağrısını bir `DateTime` olarak dönüştüremezsiniz. Bu nedenle, `DisplayDaysOnJob` yöntemi için giriş parametresi olarak bir `object` kabul etmemiz gerekir, bir veritabanı `NULL` değeri olup olmadığını (`Convert.IsDBNull(objectToCheck)`kullanılarak gerçekleştirilebilir) görmek için kontrol edin ve ardından buna uygun olarak devam edin.

Bu alt tleler nedeniyle, tüm `EmployeesRow` örneğini geçirmeye karar aldım. Bir sonraki öğreticide, bir giriş parametresini biçimlendirme yöntemine geçirmek için `Eval("columnName")` sözdiziminin kullanılmasına yönelik daha fazla sığdırma örneği görüyoruz.

Aşağıda, TemplateField eklendikten sonra GridView bizim için bildirime dayalı sözdizimi ve `ItemTemplate`çağrılan `DisplayDaysOnJob` yöntemi gösterilmektedir:

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

Şekil 16, bir tarayıcı ile görüntülendiğinde tamamlanan öğreticiyi gösterir.

[![çalışanın Iş üzerinde olduğu gün sayısı](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**Şekil 16**: çalışanın iş üzerinde olduğu gün sayısı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](using-templatefields-in-the-gridview-control-cs/_static/image48.png))

## <a name="summary"></a>Özet

GridView denetimindeki TemplateField, verileri görüntülemede daha fazla esneklik sağlar ve diğer alan denetimlerinde kullanılabilir. TemplateFields, şu durumlarda idealdir:

- Birden çok veri alanının bir GridView sütununda gösterilmesi gerekir
- Veriler, düz metin yerine bir Web denetimi kullanılarak en iyi şekilde ifade edilir
- Çıktı, meta verileri görüntüleme veya verileri yeniden biçimlendirme gibi temel verilere bağlıdır

Veri görüntülemeyi özelleştirmenin yanı sıra TemplateFields, daha sonraki öğreticilerde göreceğiniz gibi verileri düzenlemede ve eklerken kullanılan kullanıcı arabirimlerini özelleştirmek için de kullanılır.

Sonraki iki öğretici, bir DetailsView 'da TemplateFields kullanmaya bir görünüm ile başlayarak şablonları keşfetmeye devam eder. Bundan sonra, verilerin düzeninde ve yapısında daha fazla esneklik sağlamak için alanları yerine şablonları kullanan FormView 'ı kullanacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider, gözden geçirenle. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](custom-formatting-based-upon-data-cs.md)
> [İleri](using-templatefields-in-the-detailsview-control-cs.md)
