---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 'Yineleme #3 – form doğrulaması ekleme (VB) | Microsoft Docs'
author: microsoft
description: Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Emaı de doğrulıyoruz...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544452"
---
# <a name="iteration-3--add-form-validation-vb"></a>Yineleme #3 – form doğrulaması ekleme (VB)

[Microsoft](https://github.com/microsoft) tarafından

[Kodu indir](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğruladık.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Kişi yönetimi ASP.NET MVC uygulaması oluşturma (VB)

Bu öğretici dizisinde, başlangıçtan sonuna kadar bir Iletişim yönetimi uygulaması oluşturacaksınız. Ilgili kişi Yöneticisi uygulaması, kişi listesi için kişi bilgilerini, telefon numaralarını ve e-posta adreslerini depolamanıza olanak sağlar.

Uygulamayı birden çok yineleme üzerinde oluşturacağız. Her yinelemede, uygulamayı kademeli olarak geliştirdik. Bu birden çok yineleme yaklaşımının hedefi, her bir değişikliğin nedenini anlamanıza olanak sağlamaktır.

- Yineleme #1-uygulamayı oluşturun. İlk yinelemede, mümkün olan en kolay şekilde Contact Manager oluşturacağız. Temel veritabanı işlemleri için destek ekledik: oluşturma, okuma, güncelleştirme ve silme (CRUD).

- Yineleme #2-uygulamanın iyi görünmesini sağlayın. Bu yinelemede, varsayılan ASP.NET MVC görünüm ana sayfası ve geçişli stil sayfasını değiştirerek uygulamanın görünüşünü geliştiririz.

- Yineleme #3-form doğrulaması ekleme. Üçüncü yinelemede, temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarını tamamlamadan form göndermesini önliyoruz. Ayrıca e-posta adreslerini ve telefon numaralarını da doğruladık.

- Yineleme #4-uygulamayı gevşek olarak bağlanmış hale getirin. Bu dördüncü yinelemede, Contact Manager uygulamasının bakımını ve değiştirmesini kolaylaştırmak için çeşitli yazılım tasarımı desenlerinden faydalanır. Örneğin, uygulamamız depo deseninin ve bağımlılık ekleme düzeninin kullanılması için yeniden düzenliyoruz.

- Yineleme #5-birim testleri oluşturun. Beşinci yinelemede, uygulamanızın birim testlerini ekleyerek bakımını ve değiştirmeyi daha kolay hale sunuyoruz. Denetleyicilerimizin ve doğrulama mantığımız için veri modeli Sınıflarımızı ve derleme birimi testlerini modelliyoruz.

- Yineleme #6-test odaklı geliştirme kullanın. Bu altıncı yinelemede, önce birim testlerini yazarak ve birim testlerine göre kod yazarak uygulamamıza yeni işlevsellik ekleyeceğiz. Bu yinelemede kişi grupları ekleyeceğiz.

- Yineleme #7-Ajax işlevselliği ekleme. Yedinci yinelemede, Ajax desteği ekleyerek uygulamamızın yanıt hızını ve performansını geliştirdik.

## <a name="this-iteration"></a>Bu yineleme

Contact Manager uygulamasının bu ikinci yinelemesinde temel form doğrulaması ekleyeceğiz. Kullanıcıların gerekli form alanlarına değer girmeden kişi göndermesini önliyoruz. Ayrıca telefon numaralarını ve e-posta adreslerini de doğruladık (bkz. Şekil 1).

[Yeni proje iletişim kutusunu ![](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**Şekil 01**: doğrulama içeren bir form ([tam boyutlu görüntüyü görüntülemek için tıklayın](iteration-3-add-form-validation-vb/_static/image2.png))

Bu yinelemede, doğrulama mantığını doğrudan denetleyici eylemlerine ekleyeceğiz. Genel olarak, bu, bir ASP.NET MVC uygulamasına doğrulama eklemenin önerilen yolu değildir. Daha iyi bir yaklaşım, bir uygulama doğrulama mantığını ayrı bir [hizmet katmanına](http://martinfowler.com/eaaCatalog/serviceLayer.html)yerleştirmaktır. Bir sonraki yinelemede, uygulamayı daha sürdürülebilir hale getirmek için Contact Manager uygulamasını yeniden tasarlıyoruz.

Bu yinelemede, şeyleri basit tutmak için tüm doğrulama kodunu el ile yazdık. Doğrulama kodu kendimize yazmak yerine, doğrulama çerçevesinden yararlanabiliyoruz. Örneğin, ASP.NET MVC uygulamanız için doğrulama mantığını uygulamak üzere Microsoft Kurumsal Kitaplık doğrulama uygulaması bloğunu (VAB) kullanabilirsiniz. Doğrulama uygulama bloğu hakkında daha fazla bilgi edinmek için bkz.:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Oluşturma görünümüne doğrulama ekleme

Oluşturma görünümüne doğrulama mantığı ekleyerek başlayalım. Neyse ki, Visual Studio ile oluşturma görünümü oluşturduğumuz için, oluşturma görünümü doğrulama iletilerini görüntülemek için gereken tüm Kullanıcı arabirimi mantığını zaten içeriyor. Oluşturma görünümü, liste 1 ' de yer alır.

**Listeleme 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

Alan-doğrulama-hata sınıfı, HTML. ValidationMessage () Yardımcısı tarafından işlenen çıktının stilini almak için kullanılır. Input-Validation-Error sınıfı, HTML. TextBox () Yardımcısı tarafından oluşturulan TextBox (giriş) stilini yapmak için kullanılır. Doğrulama-Summary-Errors sınıfı, HTML. ValidationSummary () Yardımcısı tarafından işlenen sıralanmamış listeyi stiletmek için kullanılır.

> [!NOTE] 
> 
> Bu bölümde açıklanan stil sayfası sınıflarını, doğrulama hata iletilerinin görünümünü özelleştirmek için değiştirebilirsiniz.

## <a name="adding-validation-logic-to-the-create-action"></a>Oluşturma eylemine doğrulama mantığı ekleme

Artık, herhangi bir ileti oluşturma mantığını yazmadığımızda, oluşturma görünümü hiçbir şekilde doğrulama hata iletilerini görüntülemez. Doğrulama hata iletilerini göstermek için, hata iletilerini ModelState 'e eklemeniz gerekir.

> [!NOTE] 
> 
> UpdateModel () yöntemi, bir form alanının değeri bir özelliğe atanırken bir hata olduğunda ModelState 'e otomatik olarak hata iletileri ekler. Örneğin, "Apple" dizesini, DateTime değerlerini kabul eden bir Doğum tarihi özelliğine atamaya çalışırsanız, UpdateModel () yöntemi ModelState 'e bir hata ekler.

Liste 2 ' de değiştirilmiş oluşturma () yöntemi, yeni kişi veritabanına eklenmeden önce kişi sınıfının özelliklerini doğrulayan yeni bir bölüm içerir.

**Listeleme 2-Controllers\contactcontroller.exe (doğrulamayla oluştur)**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

Validate bölümü dört ayrı doğrulama kuralı uygular:

- FirstName özelliğinin uzunluğu sıfırdan büyük olmalıdır (ve yalnızca boşluklardan oluşamaz)
- LastName özelliğinin uzunluğu sıfırdan büyük olmalıdır (ve yalnızca boşluklardan oluşamaz)
- Phone özelliğinde bir değer varsa (0 ' dan büyük bir uzunluğa sahipse), Phone özelliğinin bir normal ifadeyle eşleşmesi gerekir.
- E-posta özelliğinde bir değer varsa (0 ' dan büyük bir uzunluğa sahipse), e-posta özelliği normal ifadeyle eşleşmelidir.

Bir doğrulama kuralı ihlali olduğunda, AddModelError () yönteminin yardımıyla ModelState 'e bir hata iletisi eklenir. ModelState 'e bir ileti eklediğinizde bir özelliğin adını ve doğrulama hata iletisinin metnini sağlarsınız. Bu hata iletisi, HTML. ValidationSummary () ve HTML. ValidationMessage () yardımcı yöntemlerine göre görünümde görüntülenir.

Doğrulama kuralları yürütüldükten sonra, ModelState 'in IsValid özelliği denetlenir. Ivvalid özelliği, ModelState 'e herhangi bir doğrulama hata iletisi eklendiğinde false döndürür. Doğrulama başarısız olursa, oluşturma formu hata iletileriyle yeniden görüntülenir.

> [!NOTE] 
> 
> http://regexlib.comkonumundaki normal ifade deposundan telefon numarasını ve e-posta adresini doğrulamak için normal ifadeler aldım [](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>Düzenleme eylemine doğrulama mantığı ekleme

Düzenle () eylemi bir kişiyi güncelleştirir. Düzenle () eyleminin Create () eylemiyle tamamen aynı doğrulamayı gerçekleştirmesi gerekir. Aynı doğrulama kodunu çoğaltmak yerine, hem Create () hem de Edit () eylemlerinin aynı doğrulama yöntemini çağırması için Ilgili kişi denetleyicisini yeniden düzenlemelisiniz.

Değiştirilen kişi denetleyicisi sınıfı, Listeleme 3 ' te bulunur. Bu sınıfta, Create () ve Edit () eylemleri içinde çağrılan yeni bir ValidateContact () yöntemi vardır.

**Listeleme 3-Controllers\contactcontroller.exe**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>Özet

Bu yinelemede, Contact Manager uygulamamıza temel form doğrulaması ekledik. Doğrulama mantığımız, kullanıcıların FirstName ve LastName özelliklerine değer vermeden yeni bir kişi göndermesini veya mevcut bir kişiyi düzenlemesini engeller. Ayrıca, kullanıcıların geçerli telefon numaralarını ve e-posta adreslerini sağlaması gerekir.

Bu yinelemede, doğrulama mantığını en kolay şekilde Contact Manager uygulamamıza ekledik. Ancak, doğrulama mantığımızı denetleyici mantığımızda karıştırmak, bizim için uzun vadede sorunlar oluşturacaktır. Uygulamamız zaman içinde bakım ve değiştirme konusunda daha zor olacaktır.

Bir sonraki yinelemede, doğrulama mantığı ve veritabanı erişim mantığımızı denetleyicilerimizden dışarı yeniden oluşturacağız. Daha esnek bir şekilde bağlanmış ve daha sürdürülebilir, uygulamalar oluşturmamızı sağlamak için çeşitli yazılım tasarımı ilkelerinin avantajlarından faydalanacağız.

> [!div class="step-by-step"]
> [Önceki](iteration-2-make-the-application-look-nice-vb.md)
> [İleri](iteration-4-make-the-application-loosely-coupled-vb.md)
