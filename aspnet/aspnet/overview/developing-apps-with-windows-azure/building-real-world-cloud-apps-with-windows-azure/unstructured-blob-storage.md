---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: Yapılandırılmamış BLOB depolama (Azure ile gerçek dünyada bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: 2afd4b5cf640eb97080de7e5280409f5e5347731
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583633"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>Yapılandırılmamış BLOB depolama (Azure ile gerçek dünyada bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Önceki bölümde bölümleme düzenlerini inceledik ve BT BT uygulamasının, Azure Depolama Blobu hizmetinde görüntüleri nasıl sakladığı ve Azure SQL veritabanı 'ndaki diğer görev verileri açıklanmaktadır. Bu bölümde, blob hizmetini daha ayrıntılı bir şekilde inceleyeceğiz ve BT Proje kodunu nasıl düzelteceğinizi nasıl uygulandığını göstereceğiz.

## <a name="what-is-blob-storage"></a>BLOB depolama nedir?

Azure Depolama Blobu hizmeti, dosyaları bulutta depolamak için bir yol sağlar. Blob hizmeti, dosyaları yerel ağ dosya sisteminde depolamanın çeşitli avantajları içerir:

- Oldukça ölçeklenebilir. Tek bir depolama hesabı [yüzlerce terabayt](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)saklayabilir ve birden çok depolama hesabınız olabilir. En büyük Azure müşterilerinin yüzlerce Petabaytlarca depolama alanı. Microsoft SkyDrive blob Storage kullanır.
- Dayanıklı. Blob hizmetinde depoladığınız her dosya otomatik olarak yedeklenir.
- Yüksek kullanılabilirlik sağlar. [Depolama SLA 'sı](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) , seçtiğiniz coğrafi artıklık seçeneğine bağlı olarak% 99,9 veya% 99,99 çalışma süresini taahhüt eder.
- Azure 'un bir hizmet olarak platform (PaaS) özelliğidir. Bu, yalnızca dosya depoladığınız ve aldığınız, yalnızca kullandığınız depolama alanı için ödeme yaptığınız ve Azure 'un şu şekilde gerektirdiği tüm VM 'Leri ve disk sürücüleri ayarlama ve yönetme işlemini otomatik olarak gerçekleştirir. hizmetle.
- Blob hizmetine bir REST API kullanarak veya bir programlama dili API 'SI kullanarak erişebilirsiniz. SDK 'lar .NET, Java, Ruby ve diğerleri için kullanılabilir.
- Blob hizmetinde bir dosyayı depolayadığınızda, kolayca Internet üzerinden kullanılabilir hale getirebilirsiniz.
- Blob hizmetindeki dosyaları yalnızca yetkili kullanıcılar tarafından erişilebilmeleri için güvenli hale getirebilirsiniz veya yalnızca sınırlı bir süre için kullanılabilir hale getiren geçici erişim belirteçleri sağlayabilirsiniz.

Azure için bir uygulama oluşturduğunuzda ve şirket içi bir ortamda çok fazla veri depolamak istediğinizde, resimler, videolar, PDF 'Ler, elektronik tablolar vb. gibi dosyalar da vardır. blob hizmetini düşünün.

## <a name="creating-a-storage-account"></a>Depolama hesabı oluşturma

Blob hizmetini kullanmaya başlamak için Azure 'da bir depolama hesabı oluşturursunuz. Portalda, **yeni** -- **veri hizmetleri** -- **depolama** -- **hızlı oluştur**' a tıklayın ve ardından bir URL ve veri merkezi konumu girin. Veri merkezi konumu, Web uygulamanız ile aynı olmalıdır.

![Depolama hesabı oluşturma](unstructured-blob-storage/_static/image1.png)

İçeriği depolamak istediğiniz birincil bölgeyi seçersiniz ve [coğrafi çoğaltma](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) seçeneğini belirlerseniz Azure, diğer tüm verilerinizin, ülkenin başka bir bölgesindeki farklı bir veri merkezinde kopyalarını oluşturur. Örneğin, Batı ABD veri merkezini seçerseniz, Batı ABD veri merkezine giden bir dosyayı depoladığınız halde Azure, arka planda diğer ABD veri merkezlerinden birine de kopyalanır. Ülkenin bir bölgesinde bir olağanüstü durum oluşursa, verileriniz hala güvende olur.

Azure, coğrafi olmayan sınırlar arasında veri çoğaltmayacaktır: birincil konumunuz ABD içindeyse dosyalarınız yalnızca ABD içindeki başka bir bölgeye çoğaltılır; birincil konumunuz Avustralya ise dosyalarınız yalnızca Avustralya 'daki başka bir veri merkezine çoğaltılır.

Kuşkusuz, daha önce gördüğünüz gibi bir betikten komutları yürüterek bir depolama hesabı da oluşturabilirsiniz. Bir depolama hesabı oluşturmak için bir Windows PowerShell komutu aşağıda verilmiştir:

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

Depolama Hesabınız olduktan sonra blob hizmetinde dosyaları depolamaya hemen başlayabilirsiniz.

## <a name="using-blob-storage-in-the-fix-it-app"></a>BT BT uygulamasında blob depolamayı kullanma

BT BT uygulaması, Fotoğrafları karşıya yüklemenizi sağlar.

![Bir düzelme görevi oluşturun](unstructured-blob-storage/_static/image2.png)

**Armatürü oluştur**' a tıkladığınızda, uygulama belirtilen görüntü dosyasını karşıya yükler ve BLOB hizmetinde depolar.

### <a name="set-up-the-blob-container"></a>Blob kapsayıcısını ayarlama

Blob hizmetinde bir dosyayı depolamak için bir *kapsayıcıya* ihtiyacınız vardır. Blob hizmeti kapsayıcısı bir dosya sistemi klasörüne karşılık gelir. [Her şeyi otomatikleştirin](automate-everything.md) bölümünde gözden geçirdiğimiz ortam oluşturma betikleri depolama hesabını oluşturur, ancak bir kapsayıcı oluşturmaz. Bu nedenle, `PhotoService` sınıfının `CreateAndConfigure` yönteminin amacı, zaten mevcut değilse bir kapsayıcı oluşturmaktır. Bu yöntem, *Global. asax*dosyasındaki `Application_Start` yönteminden çağrılır.

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

Depolama hesabı adı ve erişim anahtarı, *Web. config* dosyasının `appSettings` koleksiyonunda depolanır ve `StorageUtils.StorageAccount` yöntemindeki kod bu değerleri bir bağlantı dizesi oluşturmak ve bir bağlantı oluşturmak için kullanır:

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

`CreateAndConfigureAsync` yöntemi daha sonra blob hizmetini temsil eden bir nesne ve BLOB hizmetinde "görüntüler" adlı bir kapsayıcıyı (klasör) temsil eden bir nesneyi oluşturur:

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

"Görüntüler" adlı bir kapsayıcı henüz yoksa ve uygulamayı yeni bir depolama hesabında ilk kez çalıştırdığınızda doğru olacaktır; kod kapsayıcıyı oluşturur ve ortak hale getirmek için izinleri ayarlar. (Varsayılan olarak, yeni blob kapsayıcıları özeldir ve yalnızca depolama hesabınıza erişim izni olan kullanıcılar için erişilebilir.)

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>Karşıya yüklenen fotoğrafı BLOB depolama alanına depolayın

Uygulama, görüntü dosyasını karşıya yüklemek ve kaydetmek için bir `IPhotoService` arabirimi ve `PhotoService` sınıfında arabirimin bir uygulamasını kullanır. *Photoservice.cs* dosyası, blob hizmetiyle Iletişim kuran BT BT uygulamasındaki tüm kodu içerir.

Aşağıdaki MVC denetleyici yöntemi, Kullanıcı **Armaöğeyi oluştur**' a tıkladığında çağrılır. Bu kodda, `photoService` `PhotoService` sınıfının bir örneğine başvurur ve `fixittask` yeni bir görev için veri depolayan `FixItTask` Entity sınıfının bir örneğine başvurur.

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

`PhotoService` sınıfındaki `UploadPhotoAsync` yöntemi, karşıya yüklenen dosyayı blob hizmetinde depolar ve yeni Blobun işaret eden bir URL döndürür.

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

`CreateAndConfigure` yönteminde olduğu gibi, kod depolama hesabına bağlanır ve "görüntüler" blob kapsayıcısını temsil eden bir nesne oluşturur; burada, kapsayıcının zaten var olduğunu varsaymaktadır.

Sonra, dosya uzantısıyla yeni bir GUID değeri birleştirerek karşıya yüklenmek üzere bir benzersiz tanımlayıcı oluşturur:

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

Daha sonra kod, blob nesnesi oluşturmak için blob kapsayıcı nesnesini ve yeni benzersiz tanımlayıcıyı kullanır, bu nesne üzerinde ne tür dosya olduğunu gösteren bir özniteliği ayarlar ve sonra blob nesnesini kullanarak dosyayı BLOB depolama alanında depolar.

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

Son olarak, blob 'a başvuran bir URL alır. Bu URL veritabanında depolanacak ve karşıya yüklenen görüntüyü göstermek için BT Web sayfalarında kullanılabilir.

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

Bu URL, FixItTask tablosunun sütunlarından biri olarak veritabanında depolanır.

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

Yalnızca veritabanındaki URL ve BLOB depolamada bulunan görüntüler ile, BT BT uygulaması veritabanını küçük, ölçeklenebilir ve pahalı halde tutar, ancak resimler depolamanın depolama birimi olduğu ve terabayt veya petabaytlarca işleme yeteneğine sahip olduğu yerde saklanır. Bir depolama hesabı yüzlerce terabaytlık BT fotoğraflarını saklayabilir ve yalnızca kullandığınız kadar ödersiniz. Bu nedenle, ilk gigabayt için küçük ödeme 9 ' u kapatabilir ve ek gigabayt başına yarımada için daha fazla görüntü ekleyebilirsiniz.

### <a name="display-the-uploaded-file"></a>Karşıya yüklenen dosyayı görüntüle

BT BT uygulaması, bir görevin ayrıntılarını görüntülediğinde karşıya yüklenen resim dosyasını görüntüler.

![Fotoğraf ile BT görevi ayrıntılarını onarma](unstructured-blob-storage/_static/image3.png)

Görüntüyü görüntülemek için, tüm MVC görünümü tarayıcıya gönderilen HTML 'de `PhotoUrl` değerini içermelidir. Web sunucusu ve veritabanı, görüntüyü göstermek için döngüleri kullanmıyor, görüntü URL 'sine yalnızca birkaç bayt sunuluyor. Aşağıdaki Razor kodunda, `Model` `FixItTask` varlık sınıfının bir örneğine başvurur.

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

Görüntülenen sayfanın HTML 'sine bakarsanız, BLOB depolama alanındaki görüntüye doğrudan işaret eden URL 'yi görürsünüz, şöyle bir şey vardır:

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>Özet

Bu uygulamayı onarma uygulamasının, blob hizmetinde görüntüleri ve yalnızca SQL veritabanındaki görüntü URL 'Lerini nasıl depoladığını gördünüz. Blob hizmetini kullanmak SQL veritabanının çok daha küçük olmasını önler, aksi takdirde, neredeyse sınırsız sayıda göreve kadar ölçeklendirme yapabilir ve çok fazla kod yazmadan yapılabilir.

Bir depolama hesabında yüzlerce terabayta sahip olabilirsiniz ve depolama maliyeti SQL veritabanı depolamadan çok daha ucuzdur. Bu işlem, ayda gigabayt başına yaklaşık 3 sent ve küçük bir işlem ücreti ile başlar. Ve yalnızca gerçekten depoladığınız miktar için, en yüksek kapasite için ödeme yapmadıysanız, ancak uygulamanızın ölçeklendirmeye hazır olması, ancak tüm bu ek kapasiteniz için ödeme yapamayacağınızı unutmayın.

Bir [sonraki bölümde](design-to-survive-failures.md) , bir bulut uygulamasının sorunları sorunsuz bir şekilde işlemesini sağlamak için önem derecesi hakkında konuşacağız.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Azure Blob depolamaya giriş](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/). Mike Wood tarafından blog.
- [.Net ' te Azure Blob depolama hizmetini kullanma](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs). MicrosoftAzure.com sitesinde resmi belgeler. Blob depolamaya kısa bir giriş ve ardından blob depolamaya bağlanmayı, kapsayıcılar oluşturmayı, Blobları yüklemeyi ve indirmeyi gösteren kod örnekleri, vb.
- [Failsafe: ölçeklenebilir, dayanıklı Cloud Services oluşturma](https://channel9.msdn.com/Series/FailSafe). Ulrich Homann, Marc Mercuri ve Mark Simms ile dokuz parçalı video serisi. , Microsoft Müşteri danışmanlık ekibi (CAT) deneyiminden gerçek müşterilerle çekilen hikayelerle, yüksek düzeyde kavramlar ve mimari ilkeleri çok erişilebilir ve ilginç bir şekilde sunar. Azure depolama hizmeti ve Blobları hakkında bir tartışma için 35:13 adresinden başlayan Bölüm 5 ' i inceleyin.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). Bkz. Valet anahtar stili.

> [!div class="step-by-step"]
> [Önceki](data-partitioning-strategies.md)
> [İleri](design-to-survive-failures.md)
