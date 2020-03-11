---
uid: web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
title: ComboBox denetimini kullanmak Nasıl yaparım? mı? (VB) | Microsoft Docs
author: microsoft
description: ComboBox, bir TextBox 'ın esnekliğini kullanıcıların seçebileceği seçenekler listesiyle birleştiren bir ASP.NET AJAX denetimidir.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: e887e7b2-a6e7-4a28-a134-ba334494badb
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/combobox/how-do-i-use-the-combobox-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 468063a72253cce55a02bfaef1219bff03d06418
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554490"
---
# <a name="how-do-i-use-the-combobox-control-vb"></a>ComboBox denetimini kullanmak Nasıl yaparım? mı? VB

[Microsoft](https://github.com/microsoft) tarafından

> ComboBox, bir TextBox 'ın esnekliğini kullanıcıların seçebileceği seçenekler listesiyle birleştiren bir ASP.NET AJAX denetimidir.

Bu öğreticinin amacı, AJAX denetim araç seti ComboBox denetimini açıklamaktır. ComboBox, standart ASP.NET DropDownList denetimi ve TextBox denetimi arasında bir bileşim gibi çalışmaktadır. Önceden varolan bir öğe listesinden seçim yapabilir veya yeni bir öğe girebilirsiniz.

ComboBox, AutoComplete denetim genişleticine benzerdir, ancak denetimler farklı senaryolarda kullanılır. Otomatik tamamlama genişletici, eşleşen girdileri almak için bir Web hizmetini sorgular. Aksine ComboBox denetimi bir dizi öğe ile başlatılır. Otomatik tamamlama genişletici 'in kullanılması, büyük bir veri kümesiyle (milyonlarca araba bölümü) çalışırken, ComboBox denetimini kullanırken küçük bir veri kümesiyle (onlarca araç parçaları) çalışırken mantıklı hale geldiğinde anlamlı hale gelir.

## <a name="selecting-from-a-static-list-of-items"></a>Statik bir öğe listesinden seçme

ComboBox denetimini kullanarak bir basit örnekle başlayalım. Bir açılan listede öğelerin statik listesini göstermek istediğinizi düşünün. Ancak, listenin tamamlanmamış olma olasılığını açık bırakmak istersiniz. Bir kullanıcının listeye özel bir değer girmesine izin vermek istiyorsunuz.

Yeni bir ASP.NET Web Forms sayfası oluşturacağız ve sayfada ComboBox denetimini kullanacaksınız. Yeni ASP.NET sayfasını projenize ekleyin ve Tasarım görünümü değiştirin.

Sayfada ComboBox denetimini kullanmak istiyorsanız, sayfaya bir ScriptManager denetimi eklemeniz gerekir. ScriptManager denetimini, AJAX Uzantıları sekmesinin altında bulunan tasarımcı yüzeyine sürükleyin. Sayfanın üst kısmına ScriptManager denetimini eklemeniz gerekir; sunucu tarafında açma &lt;form&gt; etiketinin hemen altına ekleyebilirsiniz.

Sonra, ComboBox denetimini sayfaya sürükleyin. ComboBox denetimini, diğer AJAX denetim araç seti denetimleri ve denetim Genişleticileri ile birlikte araç kutusu 'nda bulabilirsiniz (bkz. Şekil 1).

[iş kartı oluşturmaya yönelik basit form ![](how-do-i-use-the-combobox-control-vb/_static/image1.jpg)](how-do-i-use-the-combobox-control-vb/_static/image1.png)

**Şekil 01**: araç kutusu 'ndan ComboBox denetimini seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image2.png))

Bir statik seçim listesi göstermek için ComboBox denetimini kullanacağız. Kullanıcı üç seçenekten oluşan bir listeden belirli bir sıyeme düzeyi seçebilir: hafif, orta ve sık erişimli (bkz. Şekil 2).

[![statik bir öğe listesinden seçme](how-do-i-use-the-combobox-control-vb/_static/image2.jpg)](how-do-i-use-the-combobox-control-vb/_static/image3.png)

**Şekil 02**: statik bir öğe listesinden seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image4.png))

Bu seçimleri ComboBox denetimine eklemenin iki yolu vardır. Önce, farenizi Tasarım görünümü içindeki denetimin üzerine geldiğinizde seçenekleri Düzenle görev seçeneğini belirleyin ve öğe düzenleyicisini açın (bkz. Şekil 3).

[ComboBox öğelerini ![düzenlemesi](how-do-i-use-the-combobox-control-vb/_static/image3.jpg)](how-do-i-use-the-combobox-control-vb/_static/image5.png)

**Şekil 03**: ComboBox öğelerini düzenlemeyle ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image6.png))

İkinci seçenek, kaynak görünümündeki açýlýþ ve Closing &lt;ASP: ComboBox&gt; etiketleri arasına öğe listesini eklemektir. Liste 1 ' deki sayfa, öğe listesine sahip güncelleştirilmiş ComboBox 'ı içerir.

**Listeleme 1-static. aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample1.aspx)]

Sayfayı liste 1 ' de açtığınızda, açılan kutudan önceden varolan seçeneklerden birini seçebilirsiniz. Diğer bir deyişle, ComboBox yalnızca bir DropDownList denetimi gibi çalışmaktadır.

Bununla birlikte, mevcut listede olmayan yeni bir seçim (örneğin, süper Spicy) girme seçeneğiniz de vardır. Bu nedenle, ComboBox bir TextBox denetimi gibi da çalışmaktadır.

Önceden var olan bir öğeyi seçip veya özel bir öğe girip girmeyeceğinizi ne olursa olsun, formu gönderdiğinizde, seçiminiz etiket denetiminde görünür. Formu gönderdiğinizde, Btngönder\_tıklama işleyicisi çalıştırılır ve etiketi güncelleştirir (bkz. Şekil 4).

[Seçili öğeyi görüntüleme ![](how-do-i-use-the-combobox-control-vb/_static/image4.jpg)](how-do-i-use-the-combobox-control-vb/_static/image7.png)

**Şekil 04**: Seçili öğeyi görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image8.png))

ComboBox, form gönderildikten sonra seçili öğeyi almak için DropDownList denetimiyle aynı özellikleri destekler:

- Selectedidıtem. Text-seçili öğenin Text özelliğinin değerini görüntüler.
- Selectedidıtem. Value-seçili öğenin Value özelliğinin değerini görüntüler veya ComboBox içine yazılan metni görüntüler.
- SelectedValue-Selectedidıtem. Value ile aynı, bu özellik varsayılan (başlangıçtaki) seçili öğeyi belirtmenizi sağlar.

ComboBox öğesine özel bir seçenek yazarsanız, özel seçim hem Selectedidıtem. Text hem de Selectedidıtem. Value özelliklerine atanır.

## <a name="selecting-the-list-of-items-from-the-database"></a>Veritabanından öğe listesini seçme

ComboBox 'ın bir veritabanından görüntülediği öğelerin listesini alabilirsiniz. Örneğin, ComboBox 'ı bir SqlDataSource denetimine, bir ObjectDataSource denetimine, bir LinqDataSource 'ya veya bir EntityDataSource öğesine bağlayabilirsiniz.

Bir ComboBox içindeki bir film listesini göstermek istediğinizi düşünün. Filmler veritabanı tablosundan film listesini almak istiyorsunuz. Aşağıdaki adımları uygulayın:

1. Filmler. aspx adlı bir sayfa oluşturun
2. ScriptManager 'ı araç kutusundaki AJAX Uzantıları sekmesinden sayfanın üzerine sürükleyerek sayfaya bir ScriptManager denetimi ekleyin.
3. ComboBox 'ı sayfanın üzerine sürükleyerek sayfaya ComboBox denetimi ekleyin.
4. Tasarım görünümü, farenizi ComboBox denetiminin üzerine getirin ve **veri kaynağı seç** görev seçeneğini belirleyin (bkz. Şekil 5). Veri kaynağı Yapılandırma Sihirbazı başlatılır.
5. **Veri kaynağı seçin** adımında &lt;yeni veri kaynağı&gt; seçeneğini belirleyin.
6. **Veri kaynağı türü seçin** adımında veritabanı ' nı seçin.
7. **Veri bağlantınızı seçin** adımında, veritabanınızı (örneğin, MoviesDB. mdf) seçin.
8. **Bağlantı dizesini uygulama yapılandırma dosyasına kaydet** adımında, Bağlantı dizenizi kaydetme seçeneğini belirleyin.
9. **Select Ifadesini Yapılandır** adımında, filmler veritabanı tablosunu seçin ve tüm sütunları seçin.
10. **Sorgu testi** adımında, son düğmesine tıklayın.
11. **Veri kaynağı seç** adımını geri dönüp görüntülenecek alanın başlık sütununu ve veri alanı için kimlik sütununu seçin (bkz. Şekil).
12. Sihirbazı kapatmak için Tamam düğmesine tıklayın.

[veri kaynağı seçme ![](how-do-i-use-the-combobox-control-vb/_static/image5.jpg)](how-do-i-use-the-combobox-control-vb/_static/image9.png)

**Şekil 05**: veri kaynağı seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image10.png))

[veri metni ve değer alanlarını seçme ![](how-do-i-use-the-combobox-control-vb/_static/image6.jpg)](how-do-i-use-the-combobox-control-vb/_static/image11.png)

**Şekil 06**: veri metin ve değer alanlarını seçme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image12.png))

Yukarıdaki adımları tamamladıktan sonra, ComboBox, filmler veritabanı tablosundan filmleri temsil eden bir SqlDataSource denetimine bağlanır. Sayfanın kaynağı, liste 2 gibi görünür (biçimlendirmeyi küçük bir bit olarak temizdum).

**Listeleme 2-filmler. aspx**

[!code-aspx[Main](how-do-i-use-the-combobox-control-vb/samples/sample2.aspx)]

ComboBox denetiminin SqlDataSource denetimine işaret eden bir DataSourceID özelliği olduğuna dikkat edin. Sayfayı bir tarayıcıda açtığınızda, veritabanındaki film listesi görüntülenir (bkz. Şekil 7). Listeden bir filmi seçebilir veya filmi ComboBox öğesine yazarak yeni bir filmi girebilirsiniz.

[film listesini görüntüleme ![](how-do-i-use-the-combobox-control-vb/_static/image7.jpg)](how-do-i-use-the-combobox-control-vb/_static/image13.png)

**Şekil 07**: bir film listesi görüntüleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image14.png))

## <a name="setting-the-dropdownstyle"></a>DropDownStyle ayarlanıyor

ComboBox 'ın davranışını değiştirmek için ComboBox DropDownStyle özelliğini kullanabilirsiniz. Bu özellik olası değerleri kabul eder:

- Açılan menü-(varsayılan değer) oka tıkladığınızda bir açılan liste görüntüler ve özel bir değer girebilirsiniz.
- Basit-ComboBox, otomatik olarak bir açılan liste görüntüler ve özel bir değer girebilirsiniz.
- DropDownList-ComboBox yalnızca bir DropDownList denetimi gibi çalışmaktadır.

Öğe listesi görüntülendiğinde açılır ve basit arasındaki farklılık farklıdır. Basit durumda, odağı ComboBox 'a taşıdığınızda liste hemen görüntülenir. Açılan listede, öğelerin listesini görmek için oka tıklamalısınız.

DropDownList değeri, ComboBox denetiminin tıpkı standart bir DropDownList denetimi gibi çalışmasına neden olur. Ancak burada önemli bir farklılık vardır. Internet Explorer 'ın eski sürümlerinde, denetimin önüne yerleştirilmiş herhangi bir denetimin önünde görünmesi için, sınırsız bir z diziniyle bir DropDownList denetimi görüntülenir. ComboBox, HTML &lt;yerine bir HTML &lt;div&gt; etiketi oluşturduğundan&gt; Tag ' i seçin ComboBox, z sıralamasına doğru şekilde uyar.

## <a name="setting-the-autocompletemode"></a>AutoCompleteMode ayarlama

ComboBox öğesine metin yazdığında ne olacağını belirtmek için ComboBox AutoCompleteMode özelliğini kullanabilirsiniz. Bu özellik aşağıdaki olası değerleri kabul eder:

- None-(varsayılan değer) ComboBox, hiçbir otomatik tamamlanmış davranış sağlamaz.
- Öner-ComboBox listeyi görüntüler ve listede eşleşen öğeyi vurgular (bkz. Şekil 8).
- Append-ComboBox, listeyi görüntülemez ve eşleşen öğeyi, listede yazdığınız öğeye ekler (bkz. Şekil 9).
- Müleytappend-ComboBox her ikisi de listeyi görüntüler ve eşleşen öğeyi listeden, üzerine yazdığınıza ekler (bkz. Şekil 10).

[ComboBox 'ın bir önerisi yaptığı ![](how-do-i-use-the-combobox-control-vb/_static/image8.jpg)](how-do-i-use-the-combobox-control-vb/_static/image15.png)

**Şekil 08**: ComboBox bir öneri yapar ([tam boyutlu görüntüyü görüntülemek için tıklatın](how-do-i-use-the-combobox-control-vb/_static/image16.png))

[![ComboBox, eşleşen metni ekler](how-do-i-use-the-combobox-control-vb/_static/image9.jpg)](how-do-i-use-the-combobox-control-vb/_static/image17.png)

**Şekil 09**: ComboBox eşleşen metni ekler ([tam boyutlu görüntüyü görüntülemek için tıklatın](how-do-i-use-the-combobox-control-vb/_static/image18.png))

[ComboBox 'ın önerdiği ve ekleyeceği ![](how-do-i-use-the-combobox-control-vb/_static/image10.jpg)](how-do-i-use-the-combobox-control-vb/_static/image19.png)

**Şekil 10**: ComboBox 'ın önerdiği ve ekleyeceği ([tam boyutlu görüntüyü görüntülemek için tıklayın](how-do-i-use-the-combobox-control-vb/_static/image20.png))

## <a name="summary"></a>Özet

Bu öğreticide, bir sabit öğe kümesini göstermek için ComboBox denetimini nasıl kullanacağınızı öğrendiniz. ComboBox denetimini hem statik bir öğe kümesine hem de bir veritabanı tablosuna bağladık. Son olarak, ComboBox 'ın davranışını DropDownStyle ve AutoCompleteMode özelliklerini ayarlayarak nasıl değiştireceğiniz hakkında daha fazla öğrendiniz.

> [!div class="step-by-step"]
> [Öncekini](how-do-i-use-the-combobox-control-cs.md)
