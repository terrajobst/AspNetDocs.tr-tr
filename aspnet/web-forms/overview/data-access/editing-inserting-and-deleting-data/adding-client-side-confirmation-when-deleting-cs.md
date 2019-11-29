---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: Silinirken Istemci tarafı onayı ekleniyor (C#) | Microsoft Docs
author: rick-anderson
description: Şimdiye kadar oluşturduğumuz arabirimlerde, bir Kullanıcı düzenleme düğmesine tıklamaları gerektiğinde Sil düğmesine tıklayarak verileri yanlışlıkla silebilir. Bu t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: e7d53bc65fdbbfa9ce9bfa5fbdbfa0dea598eebe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623540"
---
# <a name="adding-client-side-confirmation-when-deleting-c"></a>Silerken İstemci Tarafı Doğrulama Ekleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe) veya [PDF 'yi indirin](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)

> Şimdiye kadar oluşturduğumuz arabirimlerde, bir Kullanıcı düzenleme düğmesine tıklamaları gerektiğinde Sil düğmesine tıklayarak verileri yanlışlıkla silebilir. Bu öğreticide, Sil düğmesine tıklandığında görüntülenen bir istemci tarafı onay iletişim kutusu ekleyeceğiz.

## <a name="introduction"></a>Giriş

Son birkaç öğreticide uygulama mimarimizi, ObjectDataSource 'u ve veri Web denetimlerini ekleme, oluşturma ve silme özellikleri sağlamak için nasıl kullanacağınızı gördünüz. Bu ana kadar incelediğimiz silme arabirimleri, tıklandığı sırada bir geri göndermeye neden olan ve ObjectDataSource s `Delete()` yöntemini çağıran bir Sil düğmesinden oluşur. `Delete()` yöntemi daha sonra Iş mantığı katmanından yapılandırılan yöntemi çağırır ve bu da çağrıyı, gerçek `DELETE` bildirisini veritabanına veren veri erişim katmanına yayar.

Bu Kullanıcı arabirimi, ziyaretçilerin GridView, DetailsView veya FormView denetimleri aracılığıyla kayıtları silmesini sağladığından, Kullanıcı Sil düğmesine tıkladığında hiçbir onay sıralaması yoktur. Kullanıcı Düzenle ' ye tıklamaları gerektiğinde Sil düğmesine yanlışlıkla tıkladığında, güncelleştirilmesi amaçlanan kayıt silinir. Bunu önlemeye yardımcı olmak için, bu öğreticide Sil düğmesine tıklandığında görüntülenen bir istemci tarafı onay iletişim kutusu ekleyeceğiz.

JavaScript `confirm(string)` işlevi, dize giriş parametresini iki düğme ile donatılmış bir kalıcı iletişim kutusu içindeki metin olarak görüntüler-Tamam ve Iptal (bkz. Şekil 1). `confirm(string)` işlevi, tıklatılan düğmeye (`true`, Kullanıcı Tamam ' a tıkladıktan `false` ve Iptal ' e tıkladıklarında) göre bir Boole değeri döndürür.

![JavaScript onayla (dize) yöntemi, bir kalıcı, Istemci tarafı MessageBox görüntüler](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

**Şekil 1**: JavaScript `confirm(string)` yöntemi, bir kalıcı, Istemci tarafı MessageBox görüntüler

Bir form gönderimi sırasında, istemci tarafı olay işleyicisinden bir `false` değeri döndürülürse, form gönderme işlemi iptal edilir. Bu özelliği kullanarak, silme düğmesi ' nin istemci tarafı `onclick` olay işleyicisi `confirm("Are you sure you want to delete this product?")`bir çağrının değerini döndürmesini sağlayabilirsiniz. Kullanıcı Iptal ' i tıklarsa `confirm(string)` false döndürür, bu nedenle form teslimesinin iptal olmasına neden olur. Geri gönderme olmadan, silme düğmesine tıklamış olan ürün silinmez. Ancak, Kullanıcı onay iletişim kutusunda Tamam ' a tıkladığında, geri gönderme geri alınamaz ve ürün silinir. Bu teknik hakkında daha fazla bilgi için [bkz. form gönderimini denetlemek Için JavaScript s `confirm()` yöntemi kullanma](http://www.webreference.com/programming/javascript/confirm/) .

Gerekli istemci tarafı komut dosyasını eklemek, bir CommandField kullanırken şablonlar kullanılıyorsa biraz farklılık gösterir. Bu nedenle, bu öğreticide hem FormView hem de GridView örneğine bakacağız.

> [!NOTE]
> Bu öğreticide ele alınanlara benzer şekilde, istemci tarafı onaylama tekniklerini kullanmak, kullanıcılarınızın JavaScript 'ı destekleyen ve JavaScript 'in etkinleştirildiği tarayıcılarla ziyaret ettiğini varsayar. Bu varsayımlardan herhangi biri belirli bir kullanıcı için doğru değilse, Sil düğmesine tıklamak anında geri göndermeye neden olur (bir onaylama MessageBox gösterilmiyor).

## <a name="step-1-creating-a-formview-that-supports-deletion"></a>1\. Adım: silmeyi destekleyen bir FormView oluşturma

`EditInsertDelete` klasöründeki `ConfirmationOnDelete.aspx` sayfasına bir FormView ekleyerek başlayın ve `ProductsBLL` sınıf s `GetProducts()` yöntemi aracılığıyla ürün bilgilerini geri çeken yeni bir ObjectDataSource 'a bağlayarak bunu başlatın. Ayrıca, `ProductsBLL` sınıf s `DeleteProduct(productID)` yönteminin ObjectDataSource s `Delete()` yöntemiyle eşlendiği şekilde ObjectDataSource 'ı da yapılandırın; Ekle ve GÜNCELLEŞTIR sekmelerinin açılan listelerinin (hiçbiri) olarak ayarlandığından emin olun. Son olarak, FormView s akıllı etiketinde sayfalama etkinleştir onay kutusunu işaretleyin.

Bu adımlardan sonra, yeni ObjectDataSource tarafından bildirim temelli biçimlendirme aşağıdaki gibi görünür:

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

İyimser eşzamanlılık kullanmayan geçmiş örneklerimizde olduğu gibi, ObjectDataSource s `OldValuesParameterFormatString` özelliğini temizlemek için bir dakikanızı ayırın.

Yalnızca silmeyi destekleyen bir ObjectDataSource denetimine bağlandığından, FormView s `ItemTemplate`, yeni ve güncelleştirme düğmelerinden yalnızca silme düğmesini sunmaktadır. Ancak, FormView için bildirim temelli biçimlendirme, kaldırılabilir bir `EditItemTemplate` ve `InsertItemTemplate`içerir. Yalnızca ürün verileri alanlarının yalnızca bir alt kümesini gösteren `ItemTemplate` özelleştirmek için biraz zaman ayırın. Daha sonra, ürün adını tedarikçinin ve kategori adlarının üzerindeki bir `<h3>` başlığında göstermek için benimben yapılandırdım ve (Sil düğmesiyle birlikte).

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

Bu değişikliklerle, bir kullanıcının ürünleri birer birer açıp değiştirmesine izin veren tam işlevli bir Web sayfası vardır ve yalnızca Sil düğmesine tıklayarak bir ürünü silebilirsiniz. Şekil 2 ' de, bir tarayıcıdan görüntülendiklerinde ilerimizin ekran görüntüsü gösterilir.

[FormView ![tek bir ürünle Ilgili bilgileri gösterir](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)

**Şekil 2**: FormView, tek bir ürünle Ilgili bilgileri gösterir ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-client-side-confirmation-when-deleting-cs/_static/image4.png))

## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>2\. Adım: silme düğmelerini Istemci tarafı OnClick olayından onayla (dize) Işlevini çağırma

FormView oluşturulduğunda, son adım Delete düğmesini ziyaretçi tarafından tıklandığı gibi, JavaScript `confirm(string)` işlevinin çağrıldığı şekilde yapılandırmaktır. Bir düğmeye, LinkButton 'a veya ImageButton s istemci tarafı `onclick` olayına istemci tarafı komut dosyası eklemek, ASP.NET 2,0 ' de yeni olan `OnClientClick property`kullanılarak gerçekleştirilebilir. `confirm(string)` işlevin değerini almak istediğimiz için, bu özelliği şu şekilde ayarlamanız yeterlidir: `return confirm('Are you certain that you want to delete this product?');`

Bu değişiklikten sonra, DELETE LinkButton ' ın bildirime dayalı sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

İşte bu kadar! Şekil 3 ' te bu onayın bir ekran görüntüsü gösterilir. Sil düğmesine tıkladığınızda Onayla iletişim kutusu açılır. Kullanıcı Iptal ' i tıklarsa, geri gönderme iptal edilir ve ürün silinmez. Ancak, Kullanıcı Tamam ' ı tıklarsa, geri gönderme devam eder ve ObjectDataSource `Delete()` yöntemi çağrılır, bu da silinmekte olan veritabanı kaydında olur.

> [!NOTE]
> `confirm(string)` JavaScript işlevine geçirilen dize, kesme işareti (tırnak işaretleriyle değil) ile sınırlandırılmıştır. JavaScript 'te, dizeler herhangi bir karakter kullanılarak sınırlandırılabilir. Buraya, `confirm(string)` geçirilecek dize için sınırlayıcılar `OnClientClick` Özellik değeri için kullanılan sınırlayıcılarla belirsizliğe yol seçmemesi için burada kesme işareti kullanıyoruz.

[![, silme düğmesine tıklanınca artık görüntülenir](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)

**Şekil 3**: silme düğmesine Tıklandığınızda bir onay görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](adding-client-side-confirmation-when-deleting-cs/_static/image7.png))

## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>Adım 3: CommandField içindeki Delete düğmesine yönelik OnClientClick özelliğini yapılandırma

Bir düğme, LinkButton veya ImageButton ile doğrudan bir şablonda çalışırken, `OnClientClick` özelliğini JavaScript `confirm(string)` işlevinin sonuçlarını döndürecek şekilde yapılandırarak bir onay iletişim kutusu onunla ilişkilendirilebilir. Ancak, bir GridView veya DetailsView 'a Delete düğmeleri alanı ekleyen CommandField-bildirimli olarak ayarlanabilir bir `OnClientClick` özelliğine sahip değildir. Bunun yerine, GridView veya DetailsView `DataBound` olay işleyicisindeki Delete düğmesine program aracılığıyla başvurduk ve sonra `OnClientClick` özelliğini orada ayarlayacağız.

> [!NOTE]
> Uygun `DataBound` olay işleyicisindeki Delete düğmesi s `OnClientClick` özelliği ayarlanırken, verilere erişimi geçerli kayda bağladık. Bu, "Örneğin," Chai ürününü silmek istediğinizden emin misiniz? "gibi belirli bir kayıtla ilgili ayrıntıları dahil etmek için onay iletisini genişletebiliriz. Bu tür özelleştirmeler, veri bağlama söz dizimi kullanılarak şablonlarda de mümkündür.

Bir CommandField içindeki Delete düğmeleri için `OnClientClick` özelliğini ayarlamak için, s sayfasına GridView ekleme. Bu GridView öğesini FormView 'un kullandığı ObjectDataSource denetimini kullanacak şekilde yapılandırın. Ayrıca, GridView s BoundFields 'i yalnızca ürün adı, kategori ve tedarikçiyi içerecek şekilde sınırlandırın. Son olarak, GridView s akıllı etiketinden silmeyi etkinleştir onay kutusunu işaretleyin. Bu, GridView s `Columns` koleksiyonuna bir CommandField ekleyerek `ShowDeleteButton` özelliği `true`olarak ayarlanmıştır.

Bu değişiklikleri yaptıktan sonra, GridView s bildirim temelli işaretlerinizin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

CommandField, GridView s `RowDataBound` olay işleyiciden programlı bir şekilde erişilebilen tek bir Delete LinkButton örneği içerir. Başvurulduktan sonra, `OnClientClick` özelliğini uygun şekilde ayarlayabiliriz. Aşağıdaki kodu kullanarak `RowDataBound` olayı için bir olay işleyicisi oluşturun:

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

Bu olay işleyicisi, veri satırlarıyla (silme düğmesine sahip olacak) çalışır ve Sil düğmesine programlı olarak başvurarak başlar. Genel bölümünde aşağıdaki kalıbı kullanın:

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

*ButtonType* , CommandField-Button, LinkButton veya ImageButton tarafından kullanılan düğme türüdür. Varsayılan olarak, Komutalanı LinkButtons kullanır, ancak bu, CommandField s `ButtonType property`aracılığıyla özelleştirilebilir. *Commandfieldındex* , GridView s `Columns` koleksiyonundaki CommandField öğesinin Ordinal dizinidir, ancak *Controlindex* , CommandField s `Controls` koleksiyonu içindeki Delete düğmesinin dizinidir. *Controlindex* değeri, CommandField 'daki diğer düğmelere göre düğme s konumuna bağlıdır. Örneğin, CommandField ' da görünen tek düğme Sil düğmesidir, 0 dizinini kullanın. Ancak, Sil düğmesinden önce gelen bir düzenleme düğmesi varsa, 2 dizinini kullanın. 2 dizininin kullanılma nedeni, silme düğmesinden önce CommandField tarafından iki denetim eklenmesidir: Düzenle düğmesi ve Düzenle ve Sil düğmeleri arasına bir boşluk eklemek için kullanılan bir Edecontrol.

Özel örneğimizde, CommandField, LinkButtons kullanır ve en soldaki alan olan 0 ' ın *Commandfieldındex* ' i vardır. CommandField 'da başka düğme bulunmadığından ancak Delete düğmesi olmadığından, 0 olan bir *Controlindex* kullanıyoruz.

CommandField içindeki Delete düğmesine başvurulduktan sonra, geçerli GridView satırına göre ürün ile ilgili bilgiler sağlıyoruz. Son olarak, Delete düğmesi s `OnClientClick` özelliğini, ürün adı da dahil olmak üzere uygun JavaScript 'e ayarlayacağız. `confirm(string)` işlevine geçirilen JavaScript dizesi, kesme işareti kullanılarak sınırlandırıldığından, ürün adı içinde görüntülenen herhangi bir kesme noktasına attık. Özellikle, ürün s adındaki tüm kesme noktalarının "`\'`" ile çıkış yapılır.

Bu değişiklikler tamamlandıktan sonra GridView 'da Sil düğmesine tıkladığınızda özelleştirilmiş bir onay iletişim kutusu görüntülenir (bkz. Şekil 4). FormView 'un onay MessageBox değeriyle olduğu gibi, Kullanıcı Iptal ' i tıklarsa geri gönderme Iptal edilir ve böylece silmenin oluşmasını önler.

> [!NOTE]
> Bu teknik, bir DetailsView içindeki CommandField içindeki Delete düğmesine programlı olarak erişmek için de kullanılabilir. Ancak, DetailsView için bir `RowDataBound` olayına sahip olmadığından `DataBound` olayı için bir olay işleyicisi oluşturun.

[GridView s Sil düğmesine tıklamak ![özelleştirilmiş bir onay Iletişim kutusu görüntüler](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)

**Şekil 4**: GridView s Sil düğmesine tıkladığınızda özelleştirilmiş bir onay Iletişim kutusu görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](adding-client-side-confirmation-when-deleting-cs/_static/image10.png))

## <a name="using-templatefields"></a>TemplateFields kullanma

CommandField 'ın dezavantajlarından biri, düğmelerine dizin oluşturma aracılığıyla erişilmesi ve sonuçta elde edilen nesnenin uygun düğme türüne (düğme, LinkButton veya ImageButton) dönüştürülmesi gerekir. "Sihirli sayılar" ve sabit kodlanmış türler kullanılması, çalışma zamanına kadar bulunamamakta olan sorunları davet eder. Örneğin, ya da başka bir geliştirici, daha sonra (bir düzenleme düğmesi gibi) CommandField 'a yeni düğmeler ekler veya `ButtonType` özelliğini değiştirirse, mevcut kod hata olmadan derlenmeye devam eder, ancak sayfanın ziyaret edildiği, kodunuzun nasıl yazıldığı ve yapılan değişikliklerin ne olduğuna bağlı olarak bir özel duruma veya beklenmedik davranışa neden olabilir.

Alternatif bir yaklaşım GridView ve DetailsView s CommandFields öğesini TemplateFields olarak dönüştürmelidir. Bu, CommandField 'daki her düğme için LinkButton (veya Button veya ImageButton) içeren `ItemTemplate` bir TemplateField oluşturur. Bu düğmeler `OnClientClick` özellikler, FormView ile gördüğünüz gibi bildirimli olarak atanabilir veya aşağıdaki model kullanılarak uygun `DataBound` olay işleyicisinde program aracılığıyla erişilebilir:

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

Burada *ControlID* , düğme s `ID` özelliğinin değeridir. Bu düzen, dönüştürme için hala sabit kodlanmış bir tür gerektirdiğinde, dizin oluşturma gereksinimini ortadan kaldırır ve bu, bir çalışma zamanı hatasına neden olmadan düzenin değiştirilmesine izin verir.

## <a name="summary"></a>Özet

JavaScript `confirm(string)` işlevi, form gönderme iş akışını denetlemek için yaygın olarak kullanılan bir tekniktir. Çalıştırıldığında, işlev iki düğme içeren bir kalıcı, istemci tarafı iletişim kutusu görüntüler, tamam ve Iptal et. Kullanıcı Tamam ' ı tıklarsa `confirm(string)` işlevi `true`döndürür; Iptal ' i tıklamak `false`döndürür. Bu işlevsellik, gönderme işlemi sırasında bir olay işleyicisi `false`döndürürse bir kayıt, bir kaydı silerken bir onay MessageBox 'ı göstermek için kullanılabilir.

`confirm(string)` işlevi, Control s `OnClientClick` özelliği aracılığıyla bir düğme web denetimi istemci tarafı `onclick` olay işleyicisiyle ilişkilendirilebilir. Bir şablonda silme düğmesi ile çalışırken, FormView s şablonlarından birinde ya da DetailsView veya GridView 'da TemplateField 'da olduğunda bu özellik, bu öğreticide gördüğünüz gibi bildirimli veya program aracılığıyla ayarlanabilir.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](implementing-optimistic-concurrency-cs.md)
> [İleri](limiting-data-modification-functionality-based-on-the-user-cs.md)
