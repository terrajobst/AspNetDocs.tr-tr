---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4 ile OAuth sağlayıcılarını kullanma | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, kullanıcıların, bir dış sağlayıcıdan gelen kimlik bilgileriyle oturum açmasına olanak tanıyan bir ASP.NET MVC 4 Web uygulamasının nasıl oluşturulacağı gösterilmektedir...
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539083"
---
# <a name="using-oauth-providers-with-mvc-4"></a>MVC 4 ile OAuth Sağlayıcıları Kullanma

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, kullanıcıların Facebook, Twitter, Microsoft veya Google gibi bir dış sağlayıcıdan kimlik bilgileriyle oturum açmasını sağlayan bir ASP.NET MVC 4 Web uygulaması oluşturma ve ardından bu sağlayıcılardan bazı işlevleri tümleştirme Web uygulaması. Kolaylık olması için, bu öğretici Facebook kimlik bilgileriyle çalışmaya odaklanır.
> 
> Dış kimlik bilgilerini bir ASP.NET MVC 5 Web uygulamasında kullanmak için bkz. [Facebook ve Google OAuth2 Ile OpenID oturum açma ile ASP.NET MVC 5 uygulaması oluşturma](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
> 
> Bu kimlik bilgilerini Web sitelerinizde etkinleştirmek, milyonlarca kullanıcının zaten bu dış sağlayıcıları olan hesapları olduğundan önemli bir avantaj sağlar. Bu kullanıcılar yeni bir kimlik bilgileri kümesi oluşturup hatırlamaları zorunda olmadıkları takdirde sitenize kaydolmak için daha fazla işlem yapılabilir. Ayrıca, bir Kullanıcı bu sağlayıcılardan biri aracılığıyla oturum açtıktan sonra, sağlayıcıdan sosyal işlemler ekleyebilirsiniz.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Bu öğreticide iki ana hedef vardır:

1. Bir kullanıcının OAuth sağlayıcısından kimlik bilgileriyle oturum açmasını sağlar.
2. Sağlayıcıdan hesap bilgilerini alın ve bu bilgileri sitenizin hesap kaydıyla tümleştirin.

Bu öğreticideki örneklerde, kimlik doğrulama sağlayıcısı olarak Facebook kullanmaya odaklanmakla birlikte, sağlayıcıyı kullanmak için kodu değiştirebilirsiniz. Herhangi bir sağlayıcıyı uygulama adımları, bu öğreticide göreceğiniz adımlara çok benzer. Sağlayıcının API kümesine doğrudan çağrı yaparken yalnızca önemli farklılıklar olduğunu fark edeceksiniz.

## <a name="prerequisites"></a>Önkoşullar

- Web için [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) veya [Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

Veya

- Microsoft Visual Studio 2010 SP1 veya [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

Ayrıca, bu konuda ASP.NET MVC ve Visual Studio hakkında temel bilgiye sahip olduğunuz varsayılmaktadır. ASP.NET MVC 4 ' e giriş yapmanız gerekiyorsa, bkz. [ASP.NET MVC 4 ' e giriş](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).

## <a name="create-the-project"></a>Projeyi oluşturma

Visual Studio 'da yeni bir ASP.NET MVC 4 Web uygulaması oluşturun ve &quot;OAuthMVC&quot;olarak adlandırın. .NET Framework 4,5 veya 4 ' ü hedefleyebilirsiniz.

![proje oluştur](using-oauth-providers-with-mvc/_static/image1.png)

Yeni ASP.NET MVC 4 proje penceresinde **Internet uygulaması** ' nı seçin ve **Razor** 'yi Görünüm altyapısı olarak bırakın.

![Internet uygulaması Seç](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>Sağlayıcıyı etkinleştir

Internet uygulama şablonuyla MVC 4 Web uygulaması oluşturduğunuzda, proje, uygulama\_başlangıç klasöründe AuthConfig.cs adlı bir dosya ile oluşturulur.

![AuthConfig dosyası](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig dosyası, dış kimlik doğrulama sağlayıcılarının istemcilerini kaydetmek için kod içerir. Bu kod, varsayılan olarak açıklama olarak belirlenir, bu nedenle dış sağlayıcıların hiçbiri etkinleştirilmez.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

Dış kimlik doğrulama istemcisini kullanmak için bu kodun açıklamasını kaldırmalısınız. Yalnızca sitenize dahil etmek istediğiniz sağlayıcıların açıklamalarını kaldırın. Bu öğretici için yalnızca Facebook kimlik bilgilerini etkinleştirecektir.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

Yukarıdaki örnekte, yönteminin kayıt parametreleri için boş dizeler içerdiğine dikkat edin. Uygulamayı şimdi çalıştırmayı denerseniz, parametreler için boş dizelere izin verilmediğinden uygulama bir bağımsız değişken özel durumu oluşturur. Geçerli değerler sağlamak için, sonraki bölümde gösterildiği gibi, Web sitenizi dış sağlayıcılarla kaydetmeniz gerekir.

## <a name="registering-with-an-external-provider"></a>Dış sağlayıcıya kaydolma

Bir dış sağlayıcıdan kimlik bilgileriyle kullanıcıların kimliğini doğrulamak için, Web sitenizi sağlayıcıya kaydetmeniz gerekir. Sitenizi kaydettiğinizde, istemciyi kaydederken dahil edilecek parametreleri (anahtar veya kimlik ve gizli dizi) alacaksınız. Kullanmak istediğiniz sağlayıcıları içeren bir hesabınız olmalıdır.

Bu öğretici, bu sağlayıcılarla kaydolmak için gerçekleştirmeniz gereken adımların tümünü göstermez. Adımlar genellikle zor değildir. Sitenizi başarıyla kaydetmek için, bu sitelerde belirtilen yönergeleri izleyin. Sitenizi kaydetmeye başlamak için geliştirici sitesine bakın:

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [MICROSOFT](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

Sitenizi Facebook 'a kaydederken, aşağıdaki görüntüde gösterildiği gibi site etki alanı için &quot;localhost&quot; ve URL için `&quot; http://localhost/&quot;` sağlayabilirsiniz. Localhost kullanılması çoğu sağlayıcı ile çalışır, ancak şu anda Microsoft sağlayıcısıyla birlikte çalışmaz. Microsoft sağlayıcısı için geçerli bir Web sitesi URL 'SI dahil etmeniz gerekir.

![Siteyi Kaydet](using-oauth-providers-with-mvc/_static/image4.png)

Önceki görüntüde, uygulama kimliği, uygulama gizli anahtarı ve iletişim e-postası için değerler kaldırılmıştır. Sitenizi gerçekten kaydettiğinizde, bu değerler mevcut olacaktır. Uygulama kimliği ve uygulama gizli anahtarı değerlerini uygulamanıza ekleyecek şekilde aklınızda olmak isteyeceksiniz.

## <a name="creating-test-users"></a>Test kullanıcıları oluşturma

Sitenizi test etmek için mevcut bir Facebook hesabını kullanmıyorsanız, bu bölümü atlayabilirsiniz.

Facebook uygulama yönetimi sayfasından uygulamanız için test kullanıcılarını kolayca oluşturabilirsiniz. Bu test hesaplarını, sitenizde oturum açmak için kullanabilirsiniz. Sol gezinti bölmesindeki **Roller** bağlantısına tıklayıp **Oluştur** bağlantısına tıklayarak test kullanıcıları oluşturun.

![Test kullanıcıları oluşturma](using-oauth-providers-with-mvc/_static/image5.png)

Facebook sitesi, isteğiniz test hesaplarının sayısını otomatik olarak oluşturur.

## <a name="adding-application-id-and-secret-from-the-provider"></a>Sağlayıcıdan uygulama kimliği ve gizli dizi ekleme

Artık Facebook 'tan kimliği ve gizli dizi aldığınızı öğrenolduğunuza göre, AuthConfig dosyasına geri dönün ve parametre değerleri olarak ekleyin. Aşağıda gösterilen değerler gerçek değer değildir.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>Dış kimlik bilgileriyle oturum açma

Sitenizde dış kimlik bilgilerini etkinleştirmek için yapmanız gereken tek şey vardır. Uygulamanızı çalıştırın ve sağ üst köşedeki oturum aç bağlantısına tıklayın. Şablon, Facebook 'a sağlayıcı olarak kaydolduysanız ve sağlayıcı için bir düğme içerdiğine göre otomatik olarak tanır. Birden çok sağlayıcıyı kaydettiğinizde, her biri için bir düğme otomatik olarak eklenir.

![Dış oturum açma](using-oauth-providers-with-mvc/_static/image6.png)

Bu öğreticide, dış sağlayıcılar için oturum açma düğmelerinin nasıl özelleştirileceği ele alınmaktadır. Bu bilgi için bkz. [OAuth/OpenID kullanırken oturum açma kullanıcı arabirimini özelleştirme](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).

Facebook kimlik bilgileriyle oturum açmak için Facebook düğmesine tıklayın. Dış sağlayıcılardan birini seçtiğinizde, bu siteye yönlendirilirsiniz ve bu hizmetin oturum açması istenir.

Aşağıdaki görüntüde Facebook oturum açma ekranı gösterilmektedir. Oauthmvcexample adlı bir sitede oturum açmak için Facebook hesabınızı kullandığınızı not edin.

![Facebook kimlik doğrulaması](using-oauth-providers-with-mvc/_static/image7.png)

Facebook kimlik bilgileriyle oturum açtıktan sonra, bir sayfa kullanıcıya sitenin temel bilgilere erişimi olduğunu bildirir.

![izin iste](using-oauth-providers-with-mvc/_static/image8.png)

**Uygulamaya git**' i seçtikten sonra, kullanıcının siteye kaydolması gerekir. Aşağıdaki görüntüde, Kullanıcı Facebook kimlik bilgileriyle oturum açtıktan sonra kayıt sayfası gösterilmektedir. Kullanıcı adı, genellikle sağlayıcıdan bir ad ile önceden doldurulur.

![register](using-oauth-providers-with-mvc/_static/image9.png)

Kayıt işleminin tamamlanabilmesi için **Kaydol** ' a tıklayın. Tarayıcıyı kapatın.

Yeni hesabın veritabanınıza eklendiğini görebilirsiniz. Sunucu Gezgini, **DefaultConnection** veritabanını açın ve **Tables** klasörünü açın.

![veritabanı tabloları](using-oauth-providers-with-mvc/_static/image10.png)

**USERPROFILE** tablosuna sağ tıklayın ve **tablo verilerini göster**' i seçin.

![verileri göster](using-oauth-providers-with-mvc/_static/image11.png)

Eklediğiniz yeni hesap görüntülenir. **Web sayfası\_OAuthMembership** tablosundaki verilere bakın. Yeni eklediğiniz hesap için dış sağlayıcıyla ilgili daha fazla veri görürsünüz.

Yalnızca dış kimlik doğrulamasını etkinleştirmek istiyorsanız işiniz yapılır. Ancak, aşağıdaki bölümlerde gösterildiği gibi sağlayıcıdan bilgileri yeni kullanıcı kayıt işlemine daha fazla tümleştirebilirsiniz.

## <a name="create-models-for-additional-user-information"></a>Ek Kullanıcı bilgileri için modeller oluşturma

Önceki bölümlerde fark ettiğiniz gibi, yerleşik hesap kaydının çalışması için ek bilgi almanız gerekmez. Ancak, çoğu dış sağlayıcı kullanıcı hakkında ek bilgileri geri iletir. Aşağıdaki bölümlerde bu bilgilerin nasıl saklanacağı ve bir veritabanına nasıl kaydedileceği gösterilmektedir. Özellikle, kullanıcının tam adı, kullanıcının kişisel Web sayfasının URI 'SI ve Facebook 'un hesabı doğruladığını belirten bir değer olacak şekilde değerleri koruyabilirsiniz.

Ek Kullanıcı bilgilerini depolamak için bir tablo eklemek üzere [Code First Migrations](https://msdn.microsoft.com/data/jj591621) kullanacaksınız. Tabloyu var olan bir veritabanına ekliyoruz, bu nedenle ilk olarak geçerli veritabanının bir anlık görüntüsünü oluşturmanız gerekir. Geçerli veritabanının bir anlık görüntüsünü oluşturarak, daha sonra yalnızca yeni tabloyu içeren bir geçiş oluşturabilirsiniz. Geçerli veritabanının anlık görüntüsünü oluşturmak için:

1. **Paket Yöneticisi konsolunu** açın
2. **Enable-geçişler** komutunu çalıştırın
3. Komut **geçişi ilk-ıgnorechanges** komutunu çalıştırın
4. **Update-Database** komutunu çalıştırın

Şimdi yeni özellikleri ekleyeceksiniz. Modeller klasöründe, AccountModels.cs dosyasını açın ve RegisterExternalLoginModel sınıfını bulun. RegisterExternalLoginModel sınıfı, kimlik doğrulama sağlayıcısından geri gelen değerleri barındırır. Aşağıda vurgulanan şekilde, FullName ve LINK adlı özellikleri ekleyin.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

Ayrıca, AccountModels.cs içinde, Extrauserınformation adlı yeni bir sınıf ekleyin. Bu sınıf, veritabanında oluşturulacak yeni tabloyu temsil eder.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

UsersContext sınıfında, yeni sınıf için bir DbSet özelliği oluşturmak üzere aşağıdaki vurgulanmış kodu ekleyin.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

Artık yeni tabloyu oluşturmaya hazırsınız. Paket Yöneticisi konsolunu yeniden açın ve şu Zamanı:

1. **Add-Migration Addextrauserınformation** komutunu çalıştırın
2. **Update-Database** komutunu çalıştırın

Yeni tablo artık veritabanında bulunuyor.

## <a name="retrieve-the-additional-data"></a>Ek verileri alma

Ek kullanıcı verilerini almanın iki yolu vardır. İlk yöntem, kimlik doğrulama isteği sırasında varsayılan olarak geri geçirilen kullanıcı verilerinin saklanması olur. İkinci yöntem, özellikle sağlayıcı API 'sini çağırmak ve daha fazla bilgi isteğidir. FullName ve LINK değerleri Facebook tarafından otomatik olarak geri geçirilir. Facebook 'un, Facebook API çağrısı aracılığıyla hesabın alındığını doğruladığını belirten bir değer. İlk olarak, FullName ve LINK değerlerini dolduracaksınız ve sonra doğrulanmış değeri alırsınız.

Ek kullanıcı verilerini almak için, **accountcontroller.cs** dosyasını **denetleyiciler** klasöründe açın.

Bu dosya, hesapları günlüğe kaydetme, kaydetme ve yönetme mantığını içerir. Özellikle, **Externallogincallback** ve **externalloginconfirmation**adlı yöntemlere dikkat edin. Bu yöntemler içinde, uygulamanız için dış oturum açma işlemlerini özelleştirmek üzere kod ekleyebilirsiniz. **Externallogincallback** yönteminin ilk satırı şunları içerir:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

Daha fazla kullanıcı verisi, **doğrulama Yauthentication** yönteminden döndürülen **Authenticationresult** nesnesinin **ExtraData** özelliğine geri geçirilir. Facebook istemcisi, **ExtraData** özelliğinde aşağıdaki değerleri içerir:

- kimlik
- name
- bağlantı
- cinsiyet
- accesstoken

Diğer sağlayıcılar, ExtraData özelliğinde benzer ancak biraz farklı verilere sahip olacaktır.

Kullanıcı siteniz için yeni ise, bazı ek verileri alır ve bu verileri onay görünümüne geçitirsiniz. Yöntemdeki kodun son bloğu yalnızca Kullanıcı siteniz için yeni ise çalıştırılır. Aşağıdaki satırı değiştirin:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

Bu satırla:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

Bu değişiklik yalnızca FullName ve bağlantı özelliklerine ilişkin değerleri içerir.

**Externalloginconfirmation** yönteminde, ek kullanıcı bilgilerini kaydetmek için kodu aşağıda vurgulanan şekilde değiştirin.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>Görünümü ayarlama

Sağlayıcıdan aldığınız ek kullanıcı verileri kayıt sayfasında görüntülenir.

**Görünümler**/**Hesap** klasöründe **externalloginconfirmation. cshtml**dosyasını açın. Kullanıcı adı için mevcut alanın altında, FullName, LINK ve PictureLink için alanlar ekleyin.

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

Artık uygulamayı çalıştırmaya neredeyse hazırsınız ve ek bilgiler kaydedilecek şekilde yeni bir Kullanıcı Kaydet. Zaten siteye kayıtlı olmayan bir hesabınız olmalıdır. Farklı bir test hesabı kullanabilir veya **Kullanıcı profili** ve web sayfaları\_, yeniden kullanmak istediğiniz hesap Için **oauthmembership** tablolarındaki satırları silebilirsiniz. Bu satırları silerek, hesabın yeniden kaydettirildiğinden emin olursunuz.

Uygulamayı çalıştırın ve yeni kullanıcıyı kaydedin. Bu zaman onay sayfasının daha fazla değer içerdiğine dikkat edin.

![register](using-oauth-providers-with-mvc/_static/image12.png)

Kaydı tamamladıktan sonra tarayıcıyı kapatın. **Extrauserınformation** tablosundaki yeni değerleri fark etmek için veritabanına bakın.

## <a name="install-nuget-package-for-facebook-api"></a>Facebook API için NuGet paketini yükler

Facebook, işlemleri gerçekleştirmek için çağırabilmeniz gereken bir [API](https://developers.facebook.com/docs/reference/apis/) sağlar. HTTP istekleri göndererek veya bu istekleri göndermeyi kolaylaştıran bir NuGet paketi yükleme yoluyla Facebook API 'sini çağırabilirsiniz. Bu öğreticide bir NuGet paketi kullanılması, ancak NuGet paketinin yüklenmesi gerekli değildir. Bu öğreticide, Facebook C# SDK paketinin nasıl kullanılacağı gösterilmektedir. Facebook API 'SI çağırmaya yardımcı olan başka NuGet paketleri de vardır.

**NuGet Paketlerini Yönet** penceresinden Facebook C# SDK paketi ' ni seçin.

![paketi yükler](using-oauth-providers-with-mvc/_static/image13.png)

Kullanıcı için erişim belirteci gerektiren C# bir işlemi çağırmak için Facebook SDK 'sını kullanacaksınız. Sonraki bölümde, erişim belirtecinin nasıl alınacağı gösterilmektedir.

## <a name="retrieve-access-token"></a>Erişim belirtecini al

Çoğu dış sağlayıcı, kullanıcının kimlik bilgileri doğrulandıktan sonra bir erişim belirtecini geri iletir. Yalnızca kimliği doğrulanmış kullanıcılar için kullanılabilir olan işlemleri çağırmanızı sağladığından bu erişim belirteci çok önemlidir. Bu nedenle, daha fazla işlevsellik sağlamak istediğinizde erişim belirtecinin alınması ve depolanması önemlidir.

Dış sağlayıcıya bağlı olarak, erişim belirteci yalnızca sınırlı bir süre için geçerli olabilir. Geçerli bir erişim belirteciniz olduğundan emin olmak için, Kullanıcı oturum açtığında bu dosyayı alacak ve bir veritabanına kaydetmek yerine bir oturum değeri olarak depolayacaksınız.

**Externallogincallback** yönteminde, erişim belirteci de **Authenticationresult** nesnesinin **ExtraData** özelliğine geçirilir. Erişim belirtecini **oturum** nesnesine kaydetmek Için **Externallogincallback** öğesine vurgulanmış kodu ekleyin. Bu kod, Kullanıcı her bir Facebook hesabıyla oturum açtığında çalıştırılır.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

Bu örnek, Facebook 'tan bir erişim belirteci almasına karşın, erişim belirtecini &quot;accesstoken&quot;adlı aynı anahtar aracılığıyla herhangi bir dış sağlayıcıdan alabilirsiniz.

## <a name="logging-off"></a>Oturumu kapatma

Varsayılan **oturum kapatma** yöntemi, kullanıcının uygulamanız dışında oturum açmasını, ancak kullanıcının dış sağlayıcıdan dışarıya kaydetmez. Kullanıcıyı Facebook 'Ta günlüğe kaydetmek ve Kullanıcı oturumu kapattıktan sonra belirtecin kalıcı olmasını engellemek için, AccountController 'daki **logoff** yöntemine aşağıdaki vurgulanmış kodu ekleyebilirsiniz.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

`next` parametresinde sağladığınız değer, kullanıcının Facebook oturumu kapatıldıktan sonra kullanılacak URL 'dir. Yerel bilgisayarınızda test edilirken, yerel siteniz için doğru bağlantı noktası numarasını sağlarsınız. Üretimde, contoso.com gibi bir varsayılan sayfa sağlarsınız.

## <a name="retrieve-user-information-that-requires-the-access-token"></a>Erişim belirteci gerektiren Kullanıcı bilgilerini alma

Erişim belirtecini depoladığınıza ve Facebook C# SDK paketini yükleolduğunuza göre, Facebook 'tan ek kullanıcı bilgileri istemek için bunları birlikte kullanabilirsiniz. **Externalloginconfirmation** yönteminde, erişim belirtecinin değerini geçirerek çok **yönlü istemci** sınıfının bir örneğini oluşturun. Geçerli, kimliği doğrulanmış kullanıcı için **doğrulanmış** özelliğin değerini isteyin. **Doğrulanan** özellik, Facebook 'un hesabı bir cep telefonuna ileti gönderme gibi başka yollarla doğruladığını gösterir. Bu değeri veritabanına kaydedin.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

Kullanıcı için veritabanındaki kayıtları silmeniz ya da farklı bir Facebook hesabı kullanmanız gerekir.

Uygulamayı çalıştırın ve yeni kullanıcıyı kaydedin. Doğrulanan özelliğin değerini görmek için **Extrauserınformation** tablosuna bakın.

## <a name="conclusion"></a>Sonuç

Bu öğreticide, Kullanıcı kimlik doğrulaması ve kayıt verileri için Facebook ile tümleştirilmiş bir site oluşturdunuz. MVC 4 Web uygulaması için ayarlanan varsayılan davranış ve bu varsayılan davranışı özelleştirme hakkında bilgi edindiniz.

## <a name="related-topics"></a>İlgili konular

- [Auth ve SQL DB ile ASP.NET MVC uygulaması oluşturma ve Azure App Service dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
