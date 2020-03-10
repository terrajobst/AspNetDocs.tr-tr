---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery kullanıcı arabirimini kullanarak DropDownList 'e yeni bir kategori ekleme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: 3207079ee468232e5f75b081421241c232936baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538838"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>jQuery kullanıcı arabirimini kullanarak DropDownList’e Yeni Kategori ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

HTML `Select` etiketi, sabit kategori verilerinin bir listesini sunmak için idealdir, ancak genellikle yeni bir kategori eklemeniz gereken zamanlar. "Opera" tarzımızı veritabanımız kategorilere eklemek istediğimizi varsayalım. Bu bölümde, yeni bir kategori eklemek için kullanılabilecek bir iletişim kutusu eklemek için jQuery kullanıcı arabirimini kullanacağız. Aşağıdaki görüntüde, Kullanıcı arabiriminin tarayıcıda nasıl bulunduğu gösterilmektedir.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

Bir Kullanıcı **yeni tarz Ekle** bağlantısını seçtiğinde, bir açılan iletişim kutusu kullanıcıdan yeni bir tarz adı (ve isteğe bağlı olarak bir açıklama) ister. Aşağıdaki görüntüde **tarzı Ekle** açılır iletişim kutusu gösterilir.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

Yeni bir tarz adı girildiğinde ve **Kaydet** düğmesi gönderildiğinde, şunlar olur:

1. AJAX çağrısı, verileri yeni tarzı veritabanına kaydeden ve yeni tarz bilgilerini (tarz adı ve KIMLIĞI) JSON olarak döndüren tarzı denetleyicinin oluşturma yöntemine gönderir.
2. JavaScript yeni tarz verilerini seçim listesine ekler.
3. JavaScript yeni tarzı seçili öğe yapar.

   Aşağıdaki görüntüde, **Opera** veritabanına eklendi ve **tarz** açılan listesinde seçildi. 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

*Views\storemanager\create5cshtml* dosyasını açın ve tarz işaretlemesini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` kısmi görünümü, yeni tarz Ekle özelliğini uygulamak için kullanılan JavaScript ve jQuery 'i bağlamak için tüm mantığı içerir. Kodu tamamladıktan sonra, sanatçı Kullanıcı arabirimi ile aynı yapmak basit olacaktır.

Çözüm Gezgini, *Views\storemanager* klasörüne sağ tıklayın ve **Ekle**' yi ve ardından **görüntüle**' yi seçin. **Görünüm adı** girişinde `_ChooseGenre` girin ve ardından **Ekle**' yi seçin. *Views\storemanager\\_ChooseGenre. cshtml* dosyasındaki biçimlendirmeyi aşağıdakiler ile değiştirin:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

İlk satır, modelimiz olarak bir `Album` geçirdiğimiz ve oluşturma görünümünde tam olarak aynı model bildiriminin bulunduğunu bildirir. Sonraki birkaç satır **etiket** Yardımcısı işaretlemedir. Sonraki satır, özgün oluşturma görünümündeki ile tam olarak aynı olan **DropDownList** yardımcı çağrıdır. Sonraki satır, `Add New Genre`adıyla bir bağlantı ekler ve bir düğme gibi stillerdir. `ValidationMessageFor` içeren çizgi doğrudan oluştur görünümünden kopyalanır. Aşağıdaki satırlar:

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

`genreDialog`KIMLIKLI gizli bir div oluşturur. Bu div içindeki ID `genreDialog` **tarz Ekle** iletişim kutusumuzu bağlamak için jQuery kullanacağız. Son iki betik etiketi, yeni tarz Ekle özelliğini uygulamak için kullanacağız JavaScript dosyalarının bağlantılarını içerir. */Scripts/chooseGenre.js* dosyası projede sizin için verilmiştir. bu işlemi öğreticide daha sonra inceleyeceğiz.

Uygulamayı çalıştırın ve **yeni tarz Ekle** düğmesine tıklayın. **Tarz Ekle** Iletişim kutusunda **ad** giriş kutusuna **Opera** girin.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

**Kaydet** düğmesine tıklayın. AJAX çağrısı Opera kategorisini oluşturur ve ardından açılan listeyi Opera ile doldurur ve Opera 'yı seçili tarz olarak ayarlar.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

Bir sanatçı, başlık ve fiyat girin, ardından **Oluştur** düğmesini seçin. $8,99 'den düşük bir fiyat girerseniz, yeni albüm Dizin görünümünün en üstünde görünür. Yeni albüm girişinin veritabanına kaydedildiğini doğrulayın.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

Yalnızca bir harfle yeni bir tarz oluşturmayı deneyin. *Models\genre.cs* dosyasında bulunan aşağıdaki kod, tarz adının minimum ve maksimum uzunluğunu ayarlar.

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

İstemci tarafı doğrulama raporları 2 ila 20 karakter arasında bir dize girmeniz gerekir.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>Veritabanına ve seçim listesine yeni bir tarz eklendiğini İnceleme.

*Scripts\chooseGenre.js* dosyasını açın ve kodu inceleyin.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

İkinci satır, *Views\storemanager\\_ChooseGenre. cshtml* dosyasındaki div etiketinde bir iletişim kutusu oluşturmak için kimlik `genreDialog` kullanır. Adlandırılmış parametrelerin çoğu kendi kendine açıklayıcıdır. `autoOpen` parametresi false olarak ayarlanır, **tarz oluştur** düğmesi seçildiğinde iletişim kutusu açıkça açılır (Bu, ikinci üzerinde açıklanmıştır). İletişim kutusunda iki düğme bulunur, **Kaydet** ve **iptal et**. **İptal** düğmesi iletişim kutusunu kapatır. Aşağıdaki kodda **Kaydet** düğmesi işlevi gösterilmektedir.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm` `createGenreForm` KIMLIĞINDEN seçilir. `createGenreForm` KIMLIĞI, *Views\tarz\\_CreateGenre. cshtml* dosyasında bulunan aşağıdaki kodda ayarlandı.

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

*Views\tarz\\_CreateGenre. cshtml* dosyasında kullanılan [HTML. BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) yardımcı aşırı yüklemesi, formu göndermek için URL 'yi IÇEREN bir Action özniteliğiyle HTML oluşturur. Bu bunu, bir tarayıcıda albüm oluştur sayfasını görüntüleyerek ve kaynağı tarayıcıda göster ' i seçerek görebilirsiniz. Aşağıdaki biçimlendirme form etiketini içeren oluşturulan HTML 'yi gösterir.

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery `$.post` satırı eylem özniteliğine (`/StoreManager/Create`) bir AJAX çağrısı yapar ve **tarz oluştur** iletişim kutusundan verileri geçirir. Veriler, yeni tarz için ad ve isteğe bağlı bir açıklama içerir. AJAX çağrısı başarılı olursa, yeni tarz adı ve değeri seçim biçimlendirmesine eklenir ve yeni tarz seçili değere ayarlanır. Bu, dinamik olarak oluşturulan biçimlendirme olduğundan, kaynağı tarayıcıda görüntüleyerek yeni seçim seçeneğini göremezsiniz. IE 9 F12 geliştirici araçlarıyla yeni HTML 'yi görebilirsiniz. Yeni seçim seçeneğini görüntülemek için, Internet Explorer 9 ' da F12 Geliştirici Araçları ' nı başlatmak için F12 tuşuna basın. Oluştur sayfasına gidin ve yeni bir tarz ekleyin, bu nedenle tarz seçim listesinde yeni tarz seçilir. F12 geliştirici araçlarında:

1. HTML sekmesini seçin.
2. Yenile simgesine basın.  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. Arama kutusuna Genreıd girin.
4. İleri simgesini kullanarak,   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   Şu seçme etiketine gidin:

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. Son seçenek değerini genişletin.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

*Scripts\chooseGenre.js* dosyasında aşağıdaki kod, **yeni tarz Ekle** düğmesinin tıklama olayına nasıl bağlandığını ve **yeni tarz Ekle** iletişim kutusunun nasıl oluşturulduğunu gösterir.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

İlk satır, **yeni tarz Ekle** düğmesine iliştirilmiş bir tıklama işlevi oluşturur. Views\StoreManager\\_ChooseGenre. cshtml dosyasından aşağıdaki biçimlendirme, **yeni tarz Ekle** düğmesinin nasıl oluşturulduğunu gösterir:

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load yöntemi, tarz Ekle iletişim kutusunu oluşturup açar ve jQuery `parse` yöntemini çağırarak, iletişim kutusunda girilen verilerde istemci doğrulaması gerçekleşir.

Bu bölümde, bir seçim listesine yeni kategori verileri eklemek için kullanılabilecek bir iletişim kutusu oluşturmayı öğrendiniz. Sanatçı seçim listesine yeni bir sanatçı eklemek için Kullanıcı arabirimi oluşturmak üzere aynı yordamı izleyebilirsiniz. Bu öğreticide, ASP.NET MVC HTML Yardımcısı **DropDownList**ile çalışmaya genel bakış verilmiştir. **DropDownList**ile çalışma hakkında daha fazla bilgi için, aşağıdaki başvuruları ekleme bölümüne bakın. Lütfen Bu öğreticinin yararlı olup olmadığını bize bildirin.

Rick. Anderson [at] Microsoft. com

### <a name="additional-references"></a>Ek başvurular

- [ASP.NET MVC – geçişli aşağı açılan liste öğreticisini](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [oydu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- [Seçili](https://harvesthq.github.com/chosen/) Çoklu Seçme ve filtrelemeyi destekleyen bir JavaScript eklentisi.

### <a name="contributors"></a>Katkıda Bulunanlar

- [ÇDU Enuca](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean-Sébastien Goupıl
- [Atacan Solson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>Gözden Geçirenler

- Jean-Sébastien Goupıl
- [Atacan Solson](http://bradwilson.typepad.com/)
- Mike Pope
- Tom Dykstra

> [!div class="step-by-step"]
> [Öncekini](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
