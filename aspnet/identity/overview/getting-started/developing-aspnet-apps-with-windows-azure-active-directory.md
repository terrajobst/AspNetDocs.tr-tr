---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: Azure Active Directory-ASP.NET 4. x ile ASP.NET uygulamaları geliştirme
author: Rick-Anderson
description: Azure Active Directory için Microsoft ASP.NET araçları, Azure 'da barındırılan Web uygulamaları için kimlik doğrulamasını etkinleştirmeyi kolaylaştırır. Azure ön 'ı kullanabilirsiniz...
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456731"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>Azure Active Directory ile ASP.NET Uygulamaları geliştirme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

Azure Active Directory araçları, [Azure](https://www.windowsazure.com/home/features/web-sites/)'da barındırılan Web uygulamaları için kimlik doğrulamasını etkinleştirmeyi basitleştirir. Microsoft ASP.net Kuruluşunuzdaki Office 365 kullanıcılarının kimliğini doğrulamak için Azure kimlik doğrulamasını kullanabilirsiniz, şirket içi Active Directory veya kendi özel Azure Active Directory etki alanında oluşturulan kullanıcılarınız tarafından eşitlenmiş kurumsal hesaplardır. Windows Azure kimlik doğrulamasının etkinleştirilmesi, uygulamanızı tek bir [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) kiracı kullanarak kullanıcıların kimliğini doğrulayacak şekilde yapılandırır.

Bu öğreticide, [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) (Azure AD) ile oturum açma için yapılandırılmış bir ASP.NET uygulaması oluşturma işlemi gösterilir. Ayrıca, şu anda oturum açmış olan Kullanıcı ve uygulamayı Azure 'a dağıtma hakkında bilgi almak için Graph API nasıl çağrılacağını öğreneceksiniz.

## <a name="prerequisites"></a>Önkoşullar

1. Web veya [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) [için Visual Studio Express 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) .
2. [Visual Studio 2013 güncelleştirme 4](https://www.microsoft.com/download/details.aspx?id=44921) -güncelleştirme 3 veya üzeri gereklidir.
3. Bir Azure hesabı. Henüz bir hesabınız yoksa, ücretsiz deneme için [buraya tıklayın](https://azure.microsoft.com/pricing/free-trial/) .

## <a name="add-a-global-administrator-to-your-active-directory"></a>Active Directory genel yönetici ekleme

1. [Azure yönetim portalı](https://manage.windowsazure.com/)oturum açın.
2. Tüm Azure hesapları varsayılan bir **Dizin** içerir--üzerine tıklayın, ardından sayfanın en üstündeki **Kullanıcılar** sekmesine tıklayın (aşağıdaki resme bakın).
3. Kullanıcı Ekle ' ye tıklayın.
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. **Genel yönetici** rolüne sahip yeni bir kullanıcı oluşturun. Üstteki menüden **Kullanıcılar** ' a tıklayın ve ardından komut çubuğunda **Kullanıcı Ekle** düğmesine tıklayın.
5. **Kullanıcı Ekle** iletişim kutusunda, Yeni Kullanıcı için bir ad girin ve ardından sağ oka tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. Kullanıcı adını girin ve rolü **genel yönetici**olarak ayarlayın. Genel yöneticiler parola kurtarma amacıyla alternatif bir e-posta adresi gerektirir. İşiniz bittiğinde, sağ oka tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. İletişim kutusunun sonraki sayfasında **Oluştur**' a tıklayın. Yeni Kullanıcı için geçici bir parola oluşturulacak ve iletişim kutusunda görüntülenmeyecektir.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   Parolayı kaydedin, ilk oturum açma işleminden sonra parolayı değiştirmeniz gerekecektir. Aşağıdaki görüntüde yeni yönetici hesabı gösterilmektedir. Bu sayfada da gösterilen Microsoft hesabı değil, uygulamanızda oturum açmak için Azure Active Directory kullanmanız gerekir.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>ASP.NET uygulaması oluşturma

Aşağıdaki adımlarda [Web için Visual Studio Express 2013](https://www.microsoft.com/download/details.aspx?id=40747)kullanılır ve [Visual Studio 2013 güncelleştirme 3](https://www.microsoft.com/download/details.aspx?id=43721)gerekir.

1. Visual Studio 'da **Dosya** ' ya ve ardından **Yeni proje**' ye tıklayın. **Yeni proje** iletişim kutusunda, sol menüden görsel C# Web projesi ' ni seçin ve **Tamam**' ı tıklatın. Uygulamanız için işlevselliği istemiyorsanız, **projenin Application Insights Ekle** seçeneğinin işaretini kaldırmanız da isteyebilirsiniz.
2. **Yeni ASP.NET projesi** Iletişim kutusunda **MVC**' yi seçin ve ardından **kimlik doğrulamasını Değiştir**' e tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. **Kimlik doğrulamayı Değiştir** Iletişim kutusunda **kuruluş hesapları**' nı seçin. Bu seçenekler, uygulamanızı Azure AD 'ye otomatik olarak kaydetmek ve uygulamanızı Azure AD ile tümleştirilecek şekilde otomatik olarak yapılandırmak için kullanılabilir. Uygulamanızı kaydetmek ve yapılandırmak için **kimlik doğrulaması Değiştir** iletişim kutusunu kullanmanız gerekmez, ancak daha kolay hale gelir. Örneğin, Visual Studio 2012 kullanıyorsanız, uygulamayı Azure Yönetim Portalı el ile kaydedebilir ve yapılandırmasını Azure AD ile tümleştirilecek şekilde güncelleştirebilirsiniz.
   Açılan menülerde, **bulut-tek kuruluş** ve **Çoklu oturum açma, dizin verilerini okuma '** yı seçin. Azure AD dizininize ait etki alanını (örneğin, aşağıdaki görüntüler) *aricka0yahoo.onmicrosoft.com*girin ve ardından **Tamam**' a tıklayın. Etki alanı adını Azure portalında varsayılan dizinin etki alanları sekmesinden alabilirsiniz (sonraki resme bakın).

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   Aşağıdaki görüntüde Azure portal etki alanı adı gösterilmektedir.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > İsteğe bağlı olarak, Azure AD 'ye kaydedilecek uygulama KIMLIĞI URI 'sini **daha fazla seçeneğe**tıklayarak yapılandırabilirsiniz. Uygulama KIMLIĞI URI 'SI, Azure AD 'de kayıtlı olan ve uygulama tarafından Azure AD ile iletişim kurarken kendisini tanımlamak için kullanılan benzersiz tanıtıcıdır. Uygulama KIMLIĞI URI 'SI ve kayıtlı uygulamaların diğer özellikleri hakkında daha fazla bilgi için [Bu konuya](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering)bakın. Uygulama KIMLIĞI URI 'SI alanının altındaki onay kutusuna tıklayarak aynı uygulama KIMLIĞI URI 'sini kullanan Azure AD 'de var olan bir kaydın üzerine yazılmasını da tercih edebilirsiniz.
4. **Tamam**' a tıkladıktan sonra bir oturum açma iletişim kutusu görüntülenir ve bir genel yönetici hesabı (aboneliğinizle ilişkili Microsoft hesabı değil) kullanarak oturum açmanız gerekir. Daha önce yeni bir yönetici hesabı oluşturduysanız, parolayı değiştirmeniz ve ardından yeni parolayı kullanarak yeniden oturum açmanız gerekir.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. Kimliği başarıyla doğrulandıktan sonra, **yeni ASP.NET projesi** iletişim kutusu, kimlik doğrulama seçiminizi (**kuruluş** ) ve yeni uygulamanın kaydedileceği dizini (aşağıdaki görüntüde*aricka0yahoo.onmicrosoft.com* ) gösterir. Bu bilgilerin altında, **bulutta ana bilgisayar**etiketli onay kutusunu seçin. Bu onay kutusu işaretliyse, proje bir Azure Web uygulaması olarak sağlanacak ve daha sonra kolay yayımlama için etkinleştirilecek. **Tamam**'a tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. **Azure Web sitesi yapılandırma** iletişim kutusu, otomatik olarak oluşturulan bir site adı ve bölgesi kullanılarak görüntülenir. Ayrıca, iletişim kutusunda oturum açmış olduğunuz hesabı da aklınızda bulabilirsiniz. Bu hesabın, Azure aboneliğinizin bağlı olduğundan ve genellikle bir Microsoft hesabı olduğundan emin olmak istiyorsunuz.

    > [!NOTE]
    > Bu proje için bir veritabanı gerekiyor. Var olan veritabanlarınızdan birini seçmeniz veya yeni bir tane oluşturmanız gerekir. Proje, az miktarda kimlik doğrulama yapılandırma verilerini depolamak için zaten yerel bir veritabanı dosyası kullandığından bir veritabanı gereklidir. Uygulamayı bir Azure Web sitesine dağıttığınızda, bu veritabanı dağıtımıyla birlikte paketlenmez, bu nedenle bulutta erişilebilen bir tane seçmeniz gerekir. **Tamam**'a tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. Proje oluşturulur ve kimlik doğrulama seçenekleriniz ve Web uygulaması seçenekleriniz proje ile otomatik olarak yapılandırılır. Bu işlem tamamlandıktan sonra **^ F5**tuşuna basarak projeyi yerel olarak çalıştırın. Kuruluş hesabınızı kullanarak oturum açmanız gerekecektir. Daha önce oluşturduğunuz hesabın kullanıcı adını ve parolasını girip **oturum aç**' a tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. Başarıyla oturum açtıktan sonra, ASP.NET sitesi, sayfanın sağ üst köşesindeki Kullanıcı adını görüntüleyerek kimliği doğruladığınızı gösterir.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   Hata alırsanız: değer null veya boş olamaz. Parametre adı: linkText ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   öğreticinin sonundaki [hata ayıklama](#dbg) bölümüne bakın.

## <a name="basics-of-the-graph-api"></a>Graph API temel kavramları

[Graph API,](https://msdn.microsoft.com/library/azure/hh974476.aspx) Azure AD dizininizde bulunan nesnelerde CRUD ve diğer işlemleri gerçekleştirmek için kullanılan programlama arabirimidir. Visual Studio 2013 yeni bir proje oluştururken kimlik doğrulaması için bir kuruluş hesabı seçeneği belirlerseniz, uygulamanız zaten Graph API çağırmak üzere yapılandırılmıştır. Bu bölümde Graph API nasıl çalıştığı kısaca gösterilmektedir.

1. Çalışan uygulamanızda, sayfanın sağ üst kısmındaki oturum açan kullanıcının adına tıklayın. Bu işlem sizi, giriş denetleyicisindeki bir eylem olan kullanıcı profili sayfasına götürür. Tablonun daha önce oluşturduğunuz yönetici hesabıyla ilgili Kullanıcı bilgilerini içerdiğini fark edeceksiniz. Bu bilgiler dizininizde depolanır ve sayfa yüklendiğinde bu bilgileri almak için Graph API çağırılır.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. Visual Studio 'ya geri dönün ve **denetleyiciler** klasörünü genişletin ve ardından **HomeController.cs** dosyasını açın. Bir belirteci almak ve sonra Graph API çağırmak için kod içeren bir **USERPROFILE ()** eylemi görürsünüz. Bu kod aşağıda yineleniyor:

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    Graph API çağırmak için önce bir belirteç almanız gerekir. Belirteç alındığında, Graph API sonraki tüm isteklerin yetkilendirme üst bilgisinde dize değeri eklenmelidir. Yukarıdaki kodun çoğu, bir belirteci almak için Azure AD 'de kimlik doğrulamanın ayrıntılarını işler, Graph API çağrısı yapmak için belirteci kullanarak ve ardından yanıtı görünümde sunulacak şekilde dönüştürülüyor.

    Tartışma için en ilgili bölüm, aşağıdaki vurgulanmış satırdır: `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`. Bu satır, JSON yanıtından Serisi kaldırılan ve görünümde gösterilen kullanıcının adını temsil eder.

    HttpClient kullanarak Graph API çağırabilir ve ham verileri kendiniz işleyebilirsiniz, ancak [NuGet aracılığıyla kullanılabilen Graf Istemci kitaplığını](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)kullanmak daha kolay bir yoldur. Istemci kitaplığı, ham HTTP isteklerini ve döndürülen verilerin dönüşümünü işler ve bir .NET ortamında Graph API çalışmasını çok daha kolay hale getirir. GitHub 'da ilgili Graph API kod örneklerine bakın [.](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>Uygulamayı Azure 'a dağıtma

Aşağıdaki adımlar, uygulamayı Azure 'a nasıl dağıtacağınızı gösterir. Önceki adımlarda, yeni projenizi Azure 'da bir Web uygulamasıyla bağladınız, bu nedenle yalnızca birkaç adımda yayımlanmaya hazırlanın.

1. Visual Studio 'da projeye sağ tıklayın ve **Yayımla**' yı seçin. **Web 'ı Yayımla** iletişim kutusu, önceden yapılandırılmış her bir ayar ile görüntülenir. **Ayarlar** sayfasına gitmek için **İleri** düğmesine tıklayın. Kimlik doğrulamanız istenebilir; daha önce oluşturduğunuz kurumsal hesabı değil, Azure abonelik hesabınızı (genellikle bir Microsoft hesabı) kullanarak kimlik doğrulaması yaptığınızdan emin olun.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. **Kuruluş kimlik doğrulamasını etkinleştir** seçeneğini işaretleyin. **Etki alanı** alanına, dizininizin etki alanını girin. **Erişim düzeyi** açılan listesinden **Çoklu oturum açma ' yı seçin, dizin verilerini okuyun**. Kullandığınız önceki veritabanının **veritabanları** bölümünde zaten doldurulmuş olduğunu fark edeceksiniz. **Yayımla**’ta tıklayın.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio, Web sitenizi dağıtmaya başlayacak ve sonra yeni bir tarayıcı penceresi görünecektir. Dizininizde bir kez daha kimlik doğrulaması yapmanız istenebilir. Kimliğiniz doğrulandıktan sonra Azure 'da yeni yayınlanan web sitenize yönlendirilirsiniz.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>Uygulamada hata ayıklama

Şu hatayı alırsanız: değer null veya boş olamaz. Parametre adı: linkText

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

*Views\shared\\_LoginPartial. cshtml* dosyasındaki kodu aşağıdakiler ile değiştirin:

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

Uygulamayı çalıştırdıktan sonra, oturum açmış kullanıcı "null Kullanıcı" gösteriyorsa, oturumu kapatın ve daha önce oluşturduğunuz Active Directory hesabıyla yeniden oturum açın.

Takip etmek için harika bir öğretici, [Azure AD Ile Azure Web siteleri ve kurumsal kimlik doğrulaması](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)Rick pon 'ın derinlemesine bakış halidir.

## <a name="more-information"></a>Daha Fazla Bilgi

- [Derin bakış: Azure AD ile Azure Web siteleri ve kurumsal kimlik doğrulama](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Azure AD Graph API genel bakış](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Azure AD 'de kimlik doğrulama senaryoları](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [GitHub 'da Azure AD kod örnekleri](https://github.com/AzureADSamples)
