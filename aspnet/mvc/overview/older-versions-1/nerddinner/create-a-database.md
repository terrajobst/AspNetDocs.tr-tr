---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: Veritabanı oluşturma | Microsoft Docs
author: microsoft
description: 2\. adım, Nerdakşam yemeği uygulamamız için akşam yemeği ve RSVP verilerinin tümünü tutan veritabanını oluşturma adımlarını gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581006"
---
# <a name="create-a-database"></a>Veritabanı Oluşturma

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 2. adımından oluşur.
> 
> 2\. adım, Nerdakşam yemeği uygulamamız için akşam yemeği ve RSVP verilerinin tümünü tutan veritabanını oluşturma adımlarını gösterir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-2-creating-the-database"></a>Nerdakşam yemeği adım 2: veritabanını oluşturma

Nerdakşam yemeği uygulamamız için tüm akşam yemeği ve RSVP verilerini depolamak üzere bir veritabanı kullanacağız.

Aşağıdaki adımlarda, ücretsiz SQL Server Express sürümünü kullanarak veritabanı oluşturma ( [Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)v2 'yi kullanarak kolayca yükleyebileceğiniz) gösterilmektedir. Yazılacak tüm kodlar hem SQL Server Express hem de tam SQL Server ile birlikte çalışacak.

### <a name="creating-a-new-sql-server-express-database"></a>Yeni bir SQL Server Express veritabanı oluşturma

Web projemizi sağ tıklayıp ardından **&gt;yeni öğe Ekle** menü komutunu seçerek başlayacağız:

![](create-a-database/_static/image1.png)

Bu işlem, Visual Studio 'nun "yeni öğe Ekle" iletişim kutusunu getirir. "Veri" kategorisine göre filtreleyecek ve "veritabanı SQL Server" öğe şablonunu seçeceğiz:

![](create-a-database/_static/image2.png)

"Nerdakşam. mdf" oluşturmak istediğimiz SQL Server Express veritabanını adı vereceğiz ve Tamam ' a tıklayın. Daha sonra Visual Studio, bu dosyayı \app\_veri dizinimize eklemek isteyip istemediğini sorar (bir dizin zaten hem okuma hem de yazma güvenlik ACL 'Leri ile kuruldu):

![](create-a-database/_static/image3.png)

"Evet" i tıklayacağız ve yeni veritabanımız Çözüm Gezgini oluşturulacak ve şu eklenecektir:

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>Veritabanımız içinde tablo oluşturma

Artık yeni bir boş veritabanı var. Buraya tablo ekleyelim.

Bunu yapmak için, Visual Studio içindeki "Sunucu Gezgini" sekme penceresine giderek veritabanlarını ve sunucuları yönetebilmenizi sağlar. Uygulamamızın \app\_Data klasöründe depolanan SQL Server Express veritabanları, Sunucu Gezgini içinde otomatik olarak görünür. İsteğe bağlı olarak, listeye ek SQL Server veritabanları (yerel ve uzak) eklemek için "Sunucu Gezgini" penceresinin en üstündeki "veritabanına Bağlan" simgesine de tıklayabilirsiniz:

![](create-a-database/_static/image5.png)

Nerdakşam yemeği veritabanımız için bir tane olmak üzere bir tane olmak üzere, dinlerimizi depolamak için bir tane ve diğeri de RSVP kabulleri izlemek için diğerini. Veritabanımız içindeki "tablolar" klasörüne sağ tıklayıp "yeni tablo Ekle" menü komutunu seçerek yeni tablolar oluşturuyoruz:

![](create-a-database/_static/image6.png)

Bu, tablomızın şemasını yapılandırmamızı sağlayan bir Tablo Tasarımcısı açar. "Dinlenebilir" tablomız için 10 veri sütunu ekleyeceğiz:

![](create-a-database/_static/image7.png)

"DinnerID" sütununun tablo için benzersiz bir birincil anahtar olmasını istiyoruz. Bunu, "DinnerID" sütununa sağ tıklayıp "birincil anahtarı ayarla" menü öğesini seçerek yapılandırabiliriz:

![](create-a-database/_static/image8.png)

Bir birincil anahtar DinnerID yapmanın yanı sıra, tabloya yeni veri satırları eklendikçe değeri otomatik olarak artan bir "kimlik" sütunu olarak yapılandırmak istiyoruz (yani ilk eklenen akşam yemeği satırı, ikinci eklenen satır için bir DinnerID 1 olacaktır) DinnerID, vb. olur.

Bunu, "DinnerID" sütununu seçerek yapabiliriz ve ardından "sütun özellikleri" düzenleyicisini kullanarak sütunda "(kimlik)" özelliğini "Evet" olarak ayarlayabilirsiniz. Standart kimlik varsayılanlarını (1 ' den başlar ve her yeni akşam yemeği satırında 1 artışı) kullanacağız:

![](create-a-database/_static/image9.png)

Daha sonra CTRL-S yazarak veya **dosya&gt;kaydet** menü komutunu kullanarak tabloımızı kaydedeceğiz. Bu, tabloyu adı etmemizi ister. "Dinetleri" olarak adlandırın:

![](create-a-database/_static/image10.png)

Yeni dinlenebilir tablomız, Sunucu Gezgini 'nde veritabanı içinde görünür.

Daha sonra yukarıdaki adımları yineleyecektir ve bir "RSVP" tablosu oluşturacağız. Bu tabloda 3 sütun vardır. RsvpID Column öğesini birincil anahtar olarak ayarlayacağız ve ayrıca bunu bir kimlik sütunu oluşturacak:

![](create-a-database/_static/image11.png)

Bunu kaydedeceğiz ve "RSVP" adına sunacağız.

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>Tablolar arasında yabancı anahtar Ilişkisi ayarlama

Artık veritabanımızda iki tablo var. Son şema tasarım adımımız, her bir akşam yemeği satırını buna uygulanan sıfır veya daha fazla RSVP satırıyla ilişkilendirebilmemiz için, bu iki tablo arasında "bire çok" bir ilişki kurmak olacaktır. Bunu, RSVP tablosunun "DinnerID" sütununu "dinlenebilir" tablosundaki "DinnerID" sütunuyla bir yabancı anahtar ilişkisine sahip olacak şekilde yapılandırarak yapacağız.

Bunu yapmak için, Sunucu Gezgini 'nde çift tıklayarak, Tablo Tasarımcısı içindeki RSVP tablosunu açacağız. Bundan sonra, içinde "DinnerID" sütununu seçeceğiz, sağ tıklayıp "Ilişkiler..." seçeneğini belirleyin. bağlam menüsü komutu:

![](create-a-database/_static/image12.png)

Bu, tablolar arasındaki ilişkileri ayarlamak için kullandığımız bir iletişim kutusu getirir:

![](create-a-database/_static/image13.png)

İletişim kutusuna yeni bir ilişki eklemek için "Ekle" düğmesine tıklayacağız. İlişki eklendikten sonra, iletişim kutusunun sağındaki özellik kılavuzunda bulunan "tablolar ve sütun belirtimi" ağaç görünümü düğümünü genişleteceğiz ve ardından "..." sağ taraftaki düğme:

![](create-a-database/_static/image14.png)

"..." Seçeneğine tıklan düğme, ilişkiye hangi tabloların ve sütunların dahil olduğunu belirtmemizi sağlayan başka bir iletişim kutusu getirir ve ilişkiyi de vermemizi sağlar.

Birincil anahtar tablosunu "dinlenebilir" olacak şekilde değiştirecek ve birincil anahtar olarak dinlenebilir tablosu içindeki "DinnerID" sütununu seçeceğiz. RSVP tablomız yabancı anahtar tablosu ve RSVP olacaktır. DinnerID sütunu yabancı anahtar olarak ilişkilendirilir:

![](create-a-database/_static/image15.png)

Artık RSVP tablosundaki her bir satır, akşam yemeği tablosundaki bir satırla ilişkilendirilecektir. SQL Server, ABD için bilgi tutarlılığını koruyacak ve geçerli bir akşam yemeği satırına işaret etmezse yeni bir RSVP satırı eklememizi önlemektir. Ayrıca, kendisine başvuruda bulunan RSVP satırları varsa, bir akşam yemeği satırını silmemizi önler.

### <a name="adding-data-to-our-tables"></a>Tablolarımıza veri ekleme

Dinlenebilir tablolarımızla bazı örnek veriler ekleyerek bitelim. Tabloya sağ tıklayıp Sunucu Gezgini, "tablo verilerini göster" komutunu seçerek tabloya veri ekleyebiliriz:

![](create-a-database/_static/image16.png)

Uygulamayı uygulamaya başladığımızda daha sonra kullanacağımız birkaç akşam yemeği verisi satırı ekleyeceğiz:

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>Sonraki adım

Veritabanı oluşturma işlemi tamamlandı. Şimdi, sorgulamak ve güncelleştirmek için kullanabileceğiz model sınıfları oluşturalım.

> [!div class="step-by-step"]
> [Önceki](create-a-new-aspnet-mvc-project.md)
> [İleri](build-a-model-with-business-rule-validations.md)
