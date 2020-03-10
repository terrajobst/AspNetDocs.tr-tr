---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
title: Veritabanı dağıtma (C#) | Microsoft Docs
author: rick-anderson
description: Bir ASP.NET Web uygulaması dağıtmak, geliştirme ortamından üretim ortamına gerekli dosyaları ve kaynakları almayı gerektirir. Da...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: ff537a10-9f1f-43fe-9bcb-3dda161ba8f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 83657be794e1ea31f6ad2f2b4adc274724d60cf2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638210"
---
# <a name="deploying-a-database-c"></a>Veritabanı Dağıtma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_cs.pdf)

> Bir ASP.NET Web uygulaması dağıtmak, geliştirme ortamından üretim ortamına gerekli dosyaları ve kaynakları almayı gerektirir. Veri odaklı web uygulamaları için bu veritabanı şemasını ve verilerini içerir. Bu öğretici, veritabanını geliştirme ortamından üretime başarıyla dağıtmak için gereken adımları ele alan ilk bir seridir.

## <a name="introduction"></a>Giriş

Bir ASP.NET Web uygulaması dağıtmak, geliştirme ortamından üretim ortamına gerekli dosyaları ve kaynakları almayı gerektirir. Son altı öğreticilerin, basit bir Book Incelemeleri Web uygulaması dağıtmaya baktık. Bu tanıtım sitesi bir dizi sunucu tarafı kaynağı-ASP.NET sayfa, yapılandırma dosyası, bir `Web.sitemap` dosyası ve benzer bir şekilde, görüntüler ve CSS dosyaları gibi istemci tarafı kaynaklarla birlikte oluşur. Ancak veri odaklı web uygulamaları hakkında ne var? Veritabanı kullanan bir Web uygulamasını dağıtmak için hangi ek adımların alınması gerekir?

Bir sonraki birkaç öğreticilerde, veri odaklı bir Web uygulamasını dağıtmak için gereken adımları ele alınacaktır. Bu öğretici, sonraki öğreticide gereken yapılandırma değişikliklerine baktığı sırada, geliştirme ortamından üretim ortamına bir veritabanı şeması ve içeriği alma hakkında inceleyerek başlar. Aşağıda, Uygulama Hizmetleri (üyelik, roller, profil vb.) kullanan bir veritabanını dağıtmanın sorunlarını araştıracağız.

## <a name="examining-the-updated-book-reviews-web-application"></a>Güncelleştirilmiş kitap Incelemeleri Web uygulamasını İnceleme

Veri odaklı bir Web uygulamasının dağıtılmasını göstermek için, Book Incelemeleri Web uygulamasını basit ve statik bir Web sitesinden veri odaklı bir Web sitesine güncelleştirdim. Daha önce olduğu gibi, bu öğreticide uygulamanın iki sürümü indirilir: Web uygulaması proje modelini kullanan bir tane ve Web sitesi proje modelini kullanan bir.

Güncelleştirilmiş kitap Incelemeleri Web uygulaması, site s `App_Data` klasöründe (`~/App_Data/Reviews.mdf`) depolanan [SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx) veritabanını kullanır. Bilgisayarınızda SQL Server 2008 yüklüyse tanıtım, hatasız çalışmalıdır. SQL Server eski bir sürümüne sahipseniz ücretsiz SQL Server 2008 Express sürümünü yükleyebilir ya da bu öğreticide bulunan veritabanı betiklerini kullanarak veritabanını kendiniz oluşturabilirsiniz.

`Reviews.mdf` veritabanı dört tablo içerir:

- `Genres`-teknoloji, kurgu ve Iş gibi her bir tarz için bir kayıt içerir.
- `Books`, diğerleri arasında `Title`, `GenreId`, `ReviewDate`ve `Review`gibi sütunlarla her İnceleme için bir kayıt içerir.
- `Authors`-gözden geçirilmiş bir kitaba katkıda bulunan her yazar hakkında bilgi içerir.
- `BooksAuthors`, hangi yazarların hangi defterlere yazıldığını belirten çoktan çoğa bir JOIN tablosu.

Şekil 1 ' de bu dört tablonun bir ER diyagramı gösterilmektedir.

[Kitap Incelemelerinin Web uygulaması veritabanının dört tablodan oluşan ![.](deploying-a-database-cs/_static/image2.jpg)](deploying-a-database-cs/_static/image1.jpg) 

**Şekil 1**: kitap Inceleme Web uygulaması veritabanı dört tablodan oluşur ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image3.jpg))

Book Incelemeleri Web sitesinin önceki sürümünde, her kitap için ayrı bir ASP.NET sayfası vardı. Örneğin, *24 saat Içinde kendinize ASP.NET 3,5 öğretmek*için gözden geçirmeyi içeren `~/Tech/TYASP35.aspx` adlı bir sayfa vardı. Web sitesinin bu yeni veri odaklı sürümünde, veritabanında depolanan incelemeler ve tek bir ASP.NET sayfasında, belirtilen kitap için gözden geçirmeyi gösteren Review. aspx? ID =*BookID*bulunur. Benzer şekilde, belirtilen tarzda gözden geçirilmiş kitapları listeleyen bir tarz. aspx? ID =*Genreıd* sayfası vardır.

Şekil 2 ve 3, `Genre.aspx` ve `Review.aspx` sayfalarını eylemde görüntüleyin. Her sayfanın adres çubuğundaki URL 'YI aklınızda edin. Şekil 2 ' de bu tarz. aspx? ID = 85d164ba-1123-4c47-82a0-c8ec75de7e0e. 85d164ba-1123-4c47-82a0-c8ec75de7e0e, teknoloji tarzı için `GenreId` değer olduğundan, sayfa başlığı "teknoloji Incelemelerini" okur ve madde işaretli liste bu tarz kapsamında olan sitede bu İncelemeleri numaralandırır.

[Teknoloji tarzı sayfasını ![](deploying-a-database-cs/_static/image5.jpg)](deploying-a-database-cs/_static/image4.jpg) 

**Şekil 2**: teknoloji tarzı sayfası ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image6.jpg))

[ASP.NET 3,5, 24 saat içinde kendi kendinize eğitim ![](deploying-a-database-cs/_static/image8.jpg)](deploying-a-database-cs/_static/image7.jpg) 

**Şekil 3**: *ASP.NET 3,5* ([tam boyutlu görüntüyü görüntülemek Için tıklayın](deploying-a-database-cs/_static/image9.jpg)) için gözden geçirin.

Book Incelemeleri Web uygulaması, yöneticilerin tarzlar, incelemeler ve yazar bilgilerini ekleyebilecekleri, düzenleyebildiği ve silebileceği bir yönetim bölümü de içerir. Şu anda herhangi bir ziyaretçi Yönetim bölümüne erişebilir. Gelecekteki bir öğreticide Kullanıcı hesapları için destek ekleyecek ve yalnızca yetkili kullanıcılara yönetim sayfalarına izin vereceğiz.

Book Incelemeleri uygulamasını indirdiğinizde, bunun amacını, veri tabanlı bir uygulama dağıtma hakkında dikkat edin. Uygulama tasarımı kadar en iyi yöntemleri göstermez. Örneğin, ayrı bir veri erişim katmanı (DAL) yoktur; ASP.NET sayfaları, kod arkasındaki sınıflarda bulunan SqlDataSource Control veya ADO.NET Code aracılığıyla doğrudan veritabanıyla iletişim kurar. Katmanlı bir mimari kullanarak veri odaklı uygulamalar oluşturmaya yönelik daha ayrıntılı bir bakış için [ *veri öğreticilerle çalışma* ](../../data-access/index.md)bölümüne bakın.

## <a name="databases-on-development-versus-production"></a>Geliştirme ve üretime yönelik veritabanları

Veri odaklı bir Web uygulamasında geliştirme başlattığınızda, veritabanına bağlanma hakkında uygulama ayrıntıları sağlayan bir veritabanı bağlantı dizesi belirtmeniz gerekir. Bu bağlantı dizesi, diğer şeyleri, veritabanı sunucusunu, veritabanı adını ve güvenlik bilgilerini belirtir. Çoğu zaman, geliştirme sırasında uygulama tarafından kullanılan veritabanı, üretimde olduğu zaman kullanılan veritabanından farklıdır. Geliştirme ve üretime karşı farklı veritabanlarını kullanmanın birçok avantajı vardır. Geliştirme sırasında farklı bir veritabanı olması, canlı verileri yanlışlıkla değiştirme veya silme konusunda endişelenmeniz gerekmediği anlamına gelir. Ayrıca, üretimde uygulamadaki etkilerle ilgili endişelenmenize gerek kalmadan kukla test verilerini veya veri modelinde önemli değişiklikler yapmanızı sağlar. Geliştirme ve üretim ortamlarında farklı bir veritabanına sahip olmanın dezavantajı, uygulamanın veritabanını dağıtmasının yanı sıra veritabanı şemasında veya verilerde yapılan ilgili değişikliklerin de dağıtılması gerekir.

İlk dağıtımdan önce, veritabanının yalnızca bir örneği vardır ve bu örnek geliştirme ortamında bulunur. Uygulamayı üretime ilk kez dağıttığınızda, yalnızca gerekli sunucu tarafı ve istemci tarafı dosyalarını kopyalamamız, ayrıca veritabanını geliştirme ortamından üretim ortamına kopyalamanız gerekir. Bu, şu anda Book Incelemeleri Web uygulamasıyla birlikte sunduğumuz, veritabanının geliştirme ortamımızda `App_Data` klasöründe yer aldığı ancak henüz üretim ortamına gönderilmemiş olduğu yerdir.

Uygulama dağıtıldıktan sonra veritabanının iki kopyası vardır. Uygulama geliştikçe, yeni özellikler eklenebilir, veri modelinde bir değişiklik tasarımda (varolan tablolara yeni sütunlar ekleme, mevcut sütunlarda değişiklik yapma, yeni tablolar ekleme vb.). Web uygulaması bir sonraki dağıtıldığında, son dağıtımın üretim veritabanına uygulanması gerektiğinden bu değişiklikler geliştirme ortamında veritabanına uygulanır. Bu işlemi yönetmeye yönelik bazı stratejiler gelecekteki bir öğreticide ele alınmıştır. Bu öğretici, tüm veritabanını geliştirme ortamından üretime dağıtmaya odaklanır.

## <a name="deploying-the-database-to-the-production-environment"></a>Veritabanını üretim ortamına dağıtma

Bu öğreticinin geri kalanı, veritabanını geliştirme ortamından üretim ortamına nasıl dağıtacağınızı inceler. Aşağıdaki durumlarda, Web ana bilgisayar sağlayıcınızla hesabınızın Microsoft SQL Server veritabanı desteği içerdiğinden emin olmanız gerekir. Ayrıca, veritabanı sunucu adı, veritabanı adı ve veritabanına bağlanmak için kullanılan Kullanıcı adı ve parola gibi bazı bilgilere de sahip olmanız gerekir.

Bu öğreticide daha önce belirtildiği gibi kitap, Web sitesi s veritabanını, `App_Data` klasöründe depolanan bir SQL Server 2008 Express Edition veritabanıdır. Bu tür bir veritabanını dağıtmak, `App_Data` klasörünü geliştirme ortamından üretim ortamına kopyalamak kadar basit hale gelir. Ancak, Web ana bilgisayar sağlayıcılarının çoğu güvenlik nedeniyle veritabanlarının `App_Data` klasöründe barındırılmasını desteklemez. Bunun yerine, Web Konakları, ortamları içinde SQL Server veritabanı sunucusu üzerinde bir hesap sağlar. Veritabanını geliştirme ortamınızdan üretim ortamına dağıtmak için veritabanınızın Web ana bilgisayar s veritabanı sunucusunda kayıtlı olması gerekir.

Bu nedenle, veritabanınızı geliştirme ortamından üretim ortamına nasıl alabilirim? Web ana bilgisayarın sunduğu hizmetlere bağlı olarak bunu yapmanın birkaç yolu vardır. DiscountASP.NET gibi bazı konaklarla, bir veritabanının veya gerçek `.mdf` dosyanın bir yedeğini Web sitenize yükleyebilir ve sonra denetim masasından, yedekleme dosyasını geri yükleyebilir veya `.mdf` dosyasını SQL Server veritabanı sunucusuna ekleyebilirsiniz. Bu tür araçlarla veritabanını dağıtmak, `App_Data` klasörünü üretim ortamına kopyalamak ve sonra bunu Denetim Masası aracılığıyla eklemek kadar basittir. Bu muhtemelen veritabanınızı ilk kez yayımlamanın en kolay ve en hızlı yoludur.

Başka bir yaklaşım de veritabanı Yayımlama Sihirbazı 'nı kullanmaktır. Veritabanı Yayımlama Sihirbazı, veritabanınızı, saklı yordamları, görünümleri, Kullanıcı tanımlı işlevleri, vb. ve isteğe bağlı olarak tablolardaki verileri oluşturmak için SQL komutlarını oluşturacak bir Windows masaüstü uygulamasıdır. Daha sonra SQL Server Management Studio aracılığıyla Web ana bilgisayar sağlayıcısı veritabanı sunucunuza bağlanabilir ve ardından veritabanını üretimde çoğaltmak için bu betiği yürütebilirsiniz. Daha da iyisi, Web ana bilgisayar sağlayıcınız Microsoft s [veritabanı yayımlama hizmetlerini](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home) destekliyorsa, veritabanı Yayımlama Sihirbazı tarafından oluşturulan betiğin sizin adınıza veritabanı sunucusunda otomatik olarak yürütülmesini sağlayabilirsiniz. Veritabanı Yayımlama Sihirbazı veritabanı şemasını ve verilerini oluşturan bir betik oluşturduğundan, Web ana bilgisayar sağlayıcınız karşıya yüklenen bir `.mdf` dosyası iliştirme gibi özellikler sunmadığına bakılmaksızın çalışacaktır.

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>Veritabanı oluşturma Sihirbazı 'Nı kullanarak veritabanı şemasını ve verilerini oluşturmak için SQL komutları oluşturma

Kitap Incelemelerinin veritabanını üretime dağıtmak için veritabanı Yayımlama Sihirbazı 'nı kullanmayı görelim. Visual Studio 2008 veya sonrasını kullanıyorsanız, veritabanı Yayımlama Sihirbazı zaten yüklüdür. Visual Studio 2005 kullanıyorsanız, öncelikle Sihirbazı [indirmeniz ve yüklemeniz](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en) gerekecektir.

Visual Studio 'Yu açın ve `Reviews.mdf` veritabanına gidin. Visual Web Developer kullanıyorsanız, Veritabanı Gezgini gidin. Visual Studio kullanıyorsanız, Sunucu Gezgini kullanın. Şekil 4 ' te, Visual Web Developer Veritabanı Gezgini `Reviews.mdf` veritabanı gösterilmektedir. Şekil 4 ' te gösterildiği gibi, `Reviews.mdf` veritabanı dört tablodan, üç saklı yordamdan ve Kullanıcı tanımlı bir işlevle oluşur.

[Veritabanını Veritabanı Gezgini veya Sunucu Gezgini ![bulun](deploying-a-database-cs/_static/image11.jpg)](deploying-a-database-cs/_static/image10.jpg) 

**Şekil 4**: Veritabanı Gezgini veya Sunucu Gezgini veritabanını bulun ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image12.jpg))

Veritabanı adına sağ tıklayın ve bağlam menüsünden "sağlayıcıya Yayımla" seçeneğini belirleyin. Bu, veritabanı Yayımlama Sihirbazı 'Nı başlatır (bkz. Şekil 5). Ileri ' ye tıklayarak giriş ekranını ilerletin.

[Veritabanı Yayımlama Sihirbazı Giriş ekranını ![](deploying-a-database-cs/_static/image14.jpg)](deploying-a-database-cs/_static/image13.jpg) 

**Şekil 5**: veritabanı Yayımlama Sihirbazı Giriş ekranı ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image15.jpg))

Sihirbazdaki ikinci ekran, veritabanı Yayımlama Sihirbazı 'Nın erişebileceği veritabanlarını listeler ve seçili veritabanındaki tüm nesneleri betiğe veya betiğe yönelik nesneleri seçmenizi sağlar. Uygun veritabanını seçin ve "seçili veritabanındaki tüm nesneleri komut dosyası" seçeneğini işaretlenmiş olarak bırakın.

> [!NOTE]
> Şekil 6 ' da gösterilen ekranda Ileri ' ye tıklandığınızda, "Bu sihirbaz tarafından komut dosyası \ dosya *adı* \ Betik veritabanı \ ' de bir nesne yok" hatasını alırsanız, veritabanı dosyanızın yolunun aşırı uzun olmadığından emin olun. Veritabanı dosyasının yolu çok uzun olduğunda bu hata ortaya çıkabilir.

[Veritabanı Yayımlama Sihirbazı Giriş ekranını ![](deploying-a-database-cs/_static/image17.jpg)](deploying-a-database-cs/_static/image16.jpg) 

**Şekil 6**: veritabanı Yayımlama Sihirbazı Giriş ekranı ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image18.jpg))

Bir sonraki ekranda bir betik dosyası oluşturabilir veya Web ana bilgisayarınız destekliyorsa, veritabanını doğrudan Web ana bilgisayar sağlayıcınız s veritabanı sunucusuna yayımlayabilirsiniz. Şekil 7 ' de gösterildiği gibi, betiğe dosya `C:\REVIEWS.MDF.sql`yazıldığını yaşıyorum.

[Veritabanını bir dosyaya betik olarak ![veya doğrudan Web ana bilgisayar sağlayıcınızda yayımlayın](deploying-a-database-cs/_static/image20.jpg)](deploying-a-database-cs/_static/image19.jpg) 

**Şekil 7**: veritabanını bir dosyaya komut dosyasına koyun veya doğrudan Web ana sağlayıcınıza yayımlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image21.jpg))

Sonraki ekranda çeşitli komut dosyası seçenekleri istenir. Bu mevcut nesneleri kaldırmak için betiğin DROP deyimlerini içerip içermediğini belirtebilirsiniz. Bu varsayılan olarak true değerini alır, bu, bir veritabanını ilk kez dağıtmada ince bir değerdir. Hedef veritabanının SQL Server 2000, SQL Server 2005 veya SQL Server 2008 olduğunu da belirtebilirsiniz. Son olarak, şemayı ve verileri, yalnızca verileri veya yalnızca şemayı betiğin yapılıp yapılmayacağını belirtebilirsiniz. Şema, veritabanı nesneleri, tablolar, saklı yordamlar, görünümler vb. koleksiyonudur. Veriler, tablolarda bulunan bilgiler.

Şekil 8 ' de gösterildiği gibi, Sihirbazı var olan veritabanı nesnelerini bırakacak, SQL Server 2008 veritabanı için betik oluşturacak ve hem şemayı hem de verileri yayınlayacak şekilde yapılandırdım.

[![yayımlama seçeneklerini belirtin](deploying-a-database-cs/_static/image23.jpg)](deploying-a-database-cs/_static/image22.jpg) 

**Şekil 8**: yayımlama seçeneklerini belirtin ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image24.jpg))

Son iki ekran, alınması gereken eylemleri özetler ve sonra betik durumunu görüntüler. Sihirbazı çalıştırmanın net sonucu, üretimde veritabanını oluşturmak için gereken SQL komutlarını içeren bir betik dosyası ve geliştirmeyle aynı verilerle doldurulmaktır.

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>Üretim ortamı veritabanında SQL komutları yürütülüyor

Artık veritabanını oluşturmak için SQL komutlarını içeren betiğimize ve bu durumda kalan tüm veriler, betiği üretim veritabanında çalıştırmaktır. Bazı Web ana bilgisayar sağlayıcıları, veritabanınızdaki yürütmek üzere SQL komutları girebileceğiniz Denetim Masası 'nda bir metin kutusu sunar. Çok büyük bir betik dosyanız varsa, bu seçenek çalışmayabilir (örnek için `REVIEWS.MDF.sql` betik dosyası 425 KB 'tan fazla olabilir).

Daha iyi bir yaklaşım, SQL Server Management Studio (SSMS) kullanarak doğrudan üretim veritabanı sunucusuna bağlanmasıdır. Bilgisayarınızda yüklü SQL Server Express olmayan bir sürümüne sahipseniz, büyük olasılıkla SSMS zaten yüklüdür. Aksi takdirde, SQL Server Management Studio Express Edition 'ın ücretsiz bir kopyasını [indirebilir ve yükleyebilirsiniz](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) .

SSMS 'yi başlatın ve Web ana bilgisayar sağlayıcınız tarafından sunulan bilgileri kullanarak Web ana bilgisayar s veritabanı sunucunuza bağlanın.

[![Web ana bilgisayar sağlayıcınız s veritabanı sunucusuna bağlanma](deploying-a-database-cs/_static/image26.jpg)](deploying-a-database-cs/_static/image25.jpg) 

**Şekil 9**: Web ana bilgisayar sağlayıcınızda veritabanı sunucusuna bağlanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image27.jpg))

Veritabanları sekmesini genişletin ve veritabanınızı bulun. Araç çubuğunun sol üst köşesindeki Yeni sorgu düğmesine tıklayın, veritabanı Yayımlama Sihirbazı tarafından oluşturulan betik dosyasından SQL komutlarını yapıştırın ve Yürüt düğmesine tıklayarak bu komutları üretim veritabanı sunucusunda çalıştırın. Betik dosyanız özellikle büyükse, komutların yürütülmesi birkaç dakika sürebilir.

[![Web ana bilgisayar sağlayıcınız s veritabanı sunucusuna bağlanma](deploying-a-database-cs/_static/image29.jpg)](deploying-a-database-cs/_static/image28.jpg) 

**Şekil 10**: Web ana bilgisayar sağlayıcınızda veritabanı sunucusuna bağlanma ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image30.jpg))

İşte bu kadar! Bu noktada, geliştirme veritabanı üretime çoğaltılır. SSMS 'de veritabanını yenilerseniz yeni veritabanı nesnelerini görmeniz gerekir. Şekil 11 ' de, geliştirme veritabanını yansıtan üretim veritabanı tabloları, saklı yordamlar ve Kullanıcı tanımlı işlevler gösterilir. Veritabanı Yayımlama Sihirbazı 'nın verileri yayımlamasını sağladığımızda, üretim veritabanı tabloları, sihirbazın yürütüldüğü sırada geliştirme veritabanı s tablolarıyla aynı verilere sahiptir. Şekil 12 ' de, üretim veritabanındaki `Books` tablosundaki veriler gösterilir.

[![veritabanı nesneleri üretim veritabanında yinelenmiş](deploying-a-database-cs/_static/image32.jpg)](deploying-a-database-cs/_static/image31.jpg) 

**Şekil 11**: veritabanı nesneleri üretim veritabanında yinelendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image33.jpg))

[Üretim veritabanı ![geliştirme veritabanıyla aynı verileri Içerir](deploying-a-database-cs/_static/image35.jpg)](deploying-a-database-cs/_static/image34.jpg) 

**Şekil 12**: üretim veritabanı geliştirme veritabanıyla aynı verileri içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](deploying-a-database-cs/_static/image36.jpg))

Bu noktada, yalnızca geliştirme veritabanını üretime dağıttık. Web uygulamasını dağıtmaya henüz bakmadınız veya üretimde uygulamanın üretim veritabanını kullanması için hangi yapılandırma değişikliklerinin gerekli olduğunu inceliyoruz. Bu sorunları sonraki öğreticide ele alacağız!

## <a name="summary"></a>Özet

Veri odaklı bir Web uygulamasının dağıtımı, geliştirme sırasında kullanılan veritabanının üretim ortamına kopyalanmasını gerektirir. Birçok Web ana bilgisayar sağlayıcısı, bir veritabanını dağıtma işlemini basitleştirmek için araçlar sunar. Örneğin, DiscountASP.NET ile veritabanınızın `.mdf` dosyanızı (veya bir yedeklemeyi) ve ardından veritabanını denetim masasından veritabanı sunucusuna ekleyebilirsiniz. Web ana bilgisayar sağlayıcınız tarafından sunulan özelliklerden bağımsız olarak çalışarak, geliştirme veritabanı şemasını ve verilerini oluşturmak için bir SQL komutları betiği üreten Microsoft s veritabanı Yayımlama Sihirbazı aracı olan bir diğer seçenektir. Bu komut dosyası oluşturulduktan sonra üretim veritabanında yürütebilirsiniz.

Artık kitap, Web uygulaması veritabanını gözden geçirdiklerinde uygulamayı dağıtabileceğiniz bir üretim. Ancak, Web uygulaması yapılandırma bilgileri veritabanına yönelik bağlantı dizesini belirtir ve bu bağlantı dizesi geliştirme veritabanına başvurur. Siteyi üretime dağıttığınızda Bu bağlantı dizesi bilgilerini güncelleştirmemiz gerekir. Sonraki öğretici bu yapılandırma farklarına bakar ve veri odaklı kitap Incelemeleri sitesini üretime yayımlamak için gereken adımları adım adım açıklar.

Programlamanın kutlu olsun!

#### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Microsoft SQL Server veritabanı Yayımlama Sihirbazı 'Nı indirin 1,1](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [Microsoft SQL Server Management Studio Express Edition 'ı indirin](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [Önceki](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
> [İleri](configuring-the-production-web-application-to-use-the-production-database-cs.md)
