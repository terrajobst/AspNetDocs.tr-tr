---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET Web sayfalarına giriş-veritabanı verilerini silme | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, tek bir veritabanı girişinin nasıl silineceği gösterilir. ASP.NET Web PA 'de veritabanı verilerini güncelleştirerek seriyi tamamladığınız varsayılmaktadır...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629040"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a>ASP.NET Web sayfalarına giriş-veritabanı verilerini silme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, tek bir veritabanı girişinin nasıl silineceği gösterilir. [ASP.NET Web sayfalarındaki veritabanı verilerini güncelleştirerek](updating-data.md)seriyi tamamladığınız varsayılır.
> 
> Öğrenecekleriniz:
> 
> - Kayıt listesinden tek bir kayıt seçme.
> - Veritabanından tek bir kaydı silme.
> - Bir formda belirli bir düğmenin tıklandığını denetleme.
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - `WebGrid` Yardımcısı.
> - SQL `Delete` komutu.
> - Bir SQL `Delete` komutu çalıştırmak için `Database.Execute` yöntemi.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Önceki öğreticide, var olan bir veritabanı kaydını güncelleştirmeyi öğrendiniz. Bu öğretici benzerdir, çünkü kaydı güncelleştirmek yerine onu silersiniz. Süreçler çok daha basit olduğundan, bu öğretici bu öğreticiyi bir hale getirir.

*Filmler* sayfasında, daha önce eklediğiniz **düzenleme** bağlantısına eşlik etmek için `WebGrid` yardımcısını her filmin yanında bir **silme** bağlantısı görüntüleyecek şekilde güncelleştireceksiniz.

![Her film için silme bağlantısı gösteren filmler sayfası](deleting-data/_static/image1.png)

Düzenlemede olduğu gibi, **Sil** bağlantısına tıkladığınızda, sizi film bilgisinin zaten bir biçimde olduğu farklı bir sayfaya götürür:

![Bir film görüntülenirken film sayfasını Sil](deleting-data/_static/image2.png)

Ardından, kaydı kalıcı olarak silmek için düğmeye tıklayabilirsiniz.

## <a name="adding-a-delete-link-to-the-movie-listing"></a>Film listesine silme bağlantısı ekleme

`WebGrid` Yardımcısı 'na **silme** bağlantısı ekleyerek başlayacaksınız. Bu bağlantı, önceki bir öğreticide eklediğiniz **düzenleme** bağlantısına benzer.

*Filmler. cshtml* dosyasını açın.

Sütun ekleyerek sayfanın gövdesindeki `WebGrid` işaretlemesini değiştirin. Değiştirilen biçimlendirme şu şekildedir:

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

Yeni sütun budur:

[!code-html[Main](deleting-data/samples/sample2.html)]

Kılavuzun yapılandırıldığı şekilde, **düzenleme** sütunu kılavuzda en solda, **silme** sütunu ise en sağdaki bir yöntemdir. (Bunu fark etmediğiniz durumlarda `Year` sütundan sonra bir virgül vardır.) Bu bağlantı sütunlarının nereye gittiğine ilişkin hiçbir şey yoktur ve bunların yanına kolayca yerleştirebilirsiniz. Bu durumda, karışık bir şekilde yararlanmak daha zor hale getirmek için ayrıdır.

![Düzenleme ve ayrıntı bağlantıları içeren filmler sayfası, birbirini ileri bir yanından gösterme](deleting-data/_static/image3.png)

Yeni sütun, metni "Sil" ifadesini içeren bir bağlantıyı (`<a>` öğesi) gösterir. Bağlantının hedefi (`href` özniteliği), son olarak, her film için `id` değeri farklı olan bu URL gibi bir şekilde çözümlenen koddur:

[!code-css[Main](deleting-data/samples/sample3.css)]

Bu bağlantı, *deletefilm* adlı bir sayfayı çağırır ve SEÇTIĞINIZ filmin kimliğini iletmeyecektir.

Bu öğretici, önceki öğreticideki **düzenleme** bağlantısı ile neredeyse özdeş olduğundan ([ASP.NET Web sayfalarındaki veritabanı verilerini güncelleştirme](updating-data.md)) Bu bağlantının nasıl oluşturulduğu hakkında ayrıntı vermez.

## <a name="creating-the-delete-page"></a>Silme sayfası oluşturma

Artık kılavuzdaki **Delete** bağlantısının hedefi olacak sayfayı oluşturabilirsiniz.

> [!NOTE] 
> 
> **Önemli** İlk olarak silmek için bir kayıt seçme ve sonra ayrı bir sayfa ve düğme kullanarak işlemin güvenlik açısından çok önemli olduğunu belirleme tekniği. Önceki öğreticilerde okuduğunuzdan, Web sitenizde *herhangi* bir değişiklik yapmak *her zaman* bir HTTP POST işlemi kullanılarak &mdash; bir form kullanılarak yapılmalıdır. Yalnızca bir bağlantıya tıklayarak (yani, bir GET işlemi kullanarak) siteyi değiştirmeyi mümkün kıldıysanız, kişiler sitenize basit istekler yapabilir ve verilerinizi silebilir. Sitenizi dizine alan bir arama motoru Gezgini bile, verileri yanlışlıkla izleyen bağlantıları yanlışlıkla silebilir.
> 
> Uygulamanız kişilerin bir kaydı değiştirmesine izin veriyorsun, kaydı kullanıcıya yine de düzenlemeniz gerekir. Ancak bir kaydı silmek için bu adımı atlamayı düşünebilirsiniz. Bu adımı atlayın, ancak. (Kullanıcıların kaydı görmesini ve hedeflediğiniz kaydı sildiklerini onaylamasını de yararlı olur.)
> 
> Sonraki bir öğretici kümesinde, kullanıcının bir kaydı silmeden önce oturum açması için oturum açma işlevselliği ekleme hakkında bilgi edineceksiniz.

*Deletemovie. cshtml* adlı bir sayfa oluşturun ve dosyadaki nelerin aşağıdaki biçimlendirmeyle değiştirin:

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

Bu biçimlendirme *Editmovie* sayfaları gibi olduğundan, metin kutuları (`<input type="text">`) kullanmak yerine, biçimlendirme `<span>` öğelerini içerir. Burada düzenlemek için bir şey yoktur. Tüm yapmanız gereken, kullanıcıların doğru filmi sildiklerinden emin olmak için film ayrıntılarını görüntüleriz.

Biçimlendirme zaten kullanıcının film listesi sayfasına dönüşmesine izin veren bir bağlantı içeriyor.

*Editmovie* sayfasında, SEÇILI filmin kimliği gizli bir alanda saklanır. (Bu, ilk yerde bir sorgu dizesi değeri olarak sayfaya geçirilir.) Doğrulama hatalarını görüntüleyen bir `Html.ValidationSummary` çağrısı vardır. Bu durumda hata, sayfaya hiçbir film KIMLIĞI geçirilmemişse veya film KIMLIĞI geçersiz olabilir. Bu durum, birisi önce *filmler* sayfasında bir filmi seçmeden bu sayfayı çalıştırmışsa meydana gelebilir.

Düğme başlığı **filmi siler**ve ad özniteliği `buttonDelete`olarak ayarlanır. `name` özniteliği, formu gönderen düğmeyi tanımlamak için kodda kullanılacaktır.

1 ' e kod yazmanız gerekir) sayfa ilk görüntülendiğinde film ayrıntılarını okumak ve 2) aslında Kullanıcı düğmeye tıkladığında filmi silmeniz gerekir.

## <a name="adding-code-to-read-a-single-movie"></a>Tek bir filmi okumak için kod ekleme

*Deletemovie. cshtml* sayfasının en üstünde aşağıdaki kod bloğunu ekleyin:

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

Bu biçimlendirme, *Editmovie* sayfasındaki karşılık gelen kodla aynıdır. Film KIMLIĞINI sorgu dizesinden alır ve veritabanından bir kaydı okumak için KIMLIĞI kullanır. Kod, sayfaya geçirilen film KIMLIĞININ geçerli olduğundan emin olmak için doğrulama testini (`IsInt()` ve `row != null`) içerir.

Bu kodun yalnızca sayfa ilk kez çalıştığında çalışacağını unutmayın. Kullanıcı **filmi Sil** düğmesine tıkladığında film kaydını veritabanından yeniden okumak istemezsiniz. Bu nedenle, filmi okuma kodu, *istek bir POST işlemi değilse (form gönderimi)* `if(!IsPost)` &mdash; belirten bir test içindedir.

## <a name="adding-code-to-delete-the-selected-movie"></a>Seçili filmi silmek için kod ekleme

Kullanıcı düğmeye tıkladığında filmi silmek için, `@` bloğunun kapanış ayracın içine aşağıdaki kodu ekleyin:

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

Bu kod, var olan bir kaydın güncelleştirilmesine yönelik koda benzerdir, ancak daha basittir. Kod temelde bir SQL `Delete` ifadesini çalıştırır.

 *Editmovie* sayfasında olduğu gibi, kod `if(IsPost)` bloğudur. Bu kez `if()` koşulu biraz daha karmaşıktır: 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

Burada iki koşul vardır. Birincisi, &mdash; `if(IsPost)`önce gördüğünüz gibi sayfanın gönderilme sayfasıdır.

İkinci koşul `!Request["buttonDelete"].IsEmpty()`, isteğin `buttonDelete`adlı bir nesneye sahip olduğu anlamına gelir. Admitetki, formu hangi düğmenin gönderdiğine yönelik dolaylı bir yoldur. Form birden çok Gönder düğmesi içeriyorsa, istekte yalnızca tıklanan düğmenin adı görüntülenir. Bu nedenle, mantıksal olarak, belirli bir düğmenin adı istek &mdash; veya kodda belirtilen şekilde görünüyorsa, bu düğme boş değilse formu gönderen düğmedir &mdash;.

`&&` işleci "and" (Logical ve) anlamına gelir. Bu nedenle `if` koşulu tamamen...

*Bu istek bir gönderi (ilk kez istek değil)*  
  
 AND  
  
*`buttonDelete`* *düğmesi formu gönderen düğmedir.*

Bu form (Aslında, Bu sayfa) yalnızca bir düğme içerir, bu nedenle `buttonDelete` ek testi Teknik olarak gerekli değildir. Hala, verileri kalıcı olarak kaldıracak bir işlem gerçekleştirmeye çalışıyoruz. Bu nedenle, işlemi yalnızca kullanıcı açıkça talep edildiğinde gerçekleştirdiğinizden emin olmak isteyebilirsiniz. Örneğin, bu sayfayı daha sonra genişletdiğinizi ve diğer düğmeleri daha sonra eklediğinizi varsayalım. Daha sonra bile, filmi silen kod yalnızca `buttonDelete` düğmesi tıklandıysa çalışacaktır.

*Editmovie* sayfasında, gızlı alandan kimliği alır ve sonra SQL komutunu çalıştırırsınız. `Delete` deyimin sözdizimi şöyledir:

`DELETE FROM table WHERE ID = value`

`WHERE` yan tümcesini ve KIMLIĞINI eklemek çok önemlidir. WHERE yan tümcesini bıraktığınızda, *tablodaki tüm kayıtlar silinir*. Gördüğünüz gibi, bir yer tutucu kullanarak KIMLIK değerini SQL komutuna geçirirsiniz.

## <a name="testing-the-movie-delete-process"></a>Film silme Işlemini test etme

Artık test edebilirsiniz. *Filmler* sayfasını çalıştırın ve filmin yanındaki **Sil** ' e tıklayın. *Deletemovie* sayfası göründüğünde **filmi Sil**' e tıklayın.

![Filmi Sil düğmesinin vurgulandığı film sayfasını Sil](deleting-data/_static/image4.png)

Düğmeye tıkladığınızda, kod filmleri siler ve film listesine geri döner. Silinen filmi arayabilir ve silindiğini doğrulayabilirsiniz.

## <a name="coming-up-next"></a>Sonraki adımda

Sonraki öğreticide, sitenizdeki tüm sayfalara ortak bir görünüm ve düzen verme konusu gösterilmektedir.

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>Film sayfası için komple liste (silme bağlantılarıyla güncelleştirildi)

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie sayfası için komple liste

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](../introducing-razor-syntax-c.md)
- W3Schools sitesindeki [SQL DELETE deyimleri](http://www.w3schools.com/sql/sql_delete.asp)

> [!div class="step-by-step"]
> [Önceki](updating-data.md)
> [İleri](layouts.md)
