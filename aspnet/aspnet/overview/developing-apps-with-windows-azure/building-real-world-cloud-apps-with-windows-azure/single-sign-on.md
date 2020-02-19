---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Çoklu oturum açma (Azure ile gerçek dünyada bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 1ca93cce22487295a24aae95437b3e69dfc5b504
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457147"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>Çoklu oturum açma (Azure ile gerçek dünyada bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Bir bulut uygulaması geliştirirken göz önünde bulundurabilecek birçok güvenlik sorunu var, ancak bu seri için tek bir oturum açma için odaklanacağız. Bir soru insanlar şu sıklıkla soruyor: "Şirketimin çalışanları için ilk olarak uygulama derleniyor; Bu uygulamaları bulutta barındırırım ve kullanıcıların güvenlik duvarında barındırılan uygulamaları çalıştırırken şirket içi ortamda kullandıkları ve kullandıkları aynı güvenlik modelini kullanmasına hala olanak tanır. " Bu senaryoyu etkinleştirdiğimiz yöntemlerle birine Azure Active Directory (Azure AD) denir. Azure AD, kurumsal iş kolu (LOB) uygulamalarını Internet üzerinden kullanılabilir hale getirmenizi sağlar ve bu uygulamaları iş ortakları için de kullanılabilir kılmanızı sağlar.

## <a name="introduction-to-azure-ad"></a>Azure AD 'ye giriş

[Azure AD](https://docs.microsoft.com/azure/active-directory/) , bulutta [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) sağlar. Temel özellikler şunları içerir:

- Şirket içi Active Directory ile tümleşir.
- Uygulamalarınızdaki çoklu oturum açma imkanı sunar.
- [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-beslenir](http://en.wikipedia.org/wiki/WS-Federation)ve [OAuth 2,0](http://oauth.net/2/)gibi açık standartları destekler.
- Kurumsal [grafik REST API](https://msdn.microsoft.com/library/hh974476.aspx)destekler.

Çalışanların Intranet uygulamalarında oturum açmasını sağlamak için kullandığınız bir şirket içi Windows Server Active Directory ortamınız olduğunu varsayalım:

![](single-sign-on/_static/image1.png)

Azure AD 'nin şunları yapmanızı sağlar, bulutta bir dizin oluşturur. Bu, ücretsiz bir özelliktir ve kolayca ayarlanabilir.

Şirket içi Active Directory tamamen bağımsız olabilir; istediğiniz herkesi yerleştirebilir ve bunları Internet Apps 'te doğrulayabilirsiniz.

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

İsterseniz, şirket içi AD 'niz ile tümleştirebilirsiniz.

![AD ve WAAD tümleştirmesi](single-sign-on/_static/image3.png)

Artık şirket içinde kimlik doğrulayabilecek tüm çalışanlar, bir güvenlik duvarı açmanıza veya veri merkezinizde yeni sunucular dağıtmanıza gerek kalmadan Internet üzerinden kimlik doğrulaması yapabilir. Bildiğiniz tüm mevcut Active Directory ortamlarından yararlanmaya devam edebilir ve şirket içi uygulamalarınızı çoklu oturum açma özelliğine sahip olmak için bugün kullanabilirsiniz.

AD ve Azure AD arasında bu bağlantıyı yaptıktan sonra, Web uygulamalarınızı ve mobil cihazlarınızı bulutta çalışanlarınızın kimliğini doğrulayacak şekilde etkinleştirebilir ve Office 365, SalesForce.com veya Google Apps gibi üçüncü taraf uygulamalarını kabul edebilirsiniz. çalışanların kimlik bilgileri. Office 365 kullanıyorsanız, kimlik doğrulaması ve yetkilendirme için Office 365 Azure AD 'yi kullandığından, zaten Azure AD ile ayarlandığınızı görürsünüz.

![3\. taraf uygulamalar](single-sign-on/_static/image4.png)

Bu yaklaşımın güzelliği, kuruluşunuzun Kullanıcı eklemesi veya silmesinden veya bir kullanıcının bir parolayı değiştirdiği her seferinde, bugün kullandığınız aynı işlemi şirket içi ortamınızda kullanmanız gerekir. Şirket içi AD değişikliklerinizin hepsi otomatik olarak bulut ortamına dağıtılır.

Şirketiniz Office 365 kullanıyorsa veya bu bir taşınmakta ise, iyi haber, Office 365 kimlik doğrulaması için Azure AD 'yi kullandığı için Azure AD 'nin otomatik olarak kurulumunu yapacağından emin olmanız gerekir. Böylece, kendi uygulamalarınızda Office 365 tarafından kullanılan kimlik doğrulamasını kolayca kullanabilirsiniz.

## <a name="set-up-an-azure-ad-tenant"></a>Azure AD kiracısı ayarlama

Azure AD dizini bir Azure AD [kiracısı](https://technet.microsoft.com/library/jj573650.aspx)olarak adlandırılır ve bir kiracının kurulması oldukça kolaydır. Kavramları göstermek için Azure Yönetim Portalı nasıl yapıldığını göstereceğiz, ancak diğer portal işlevleri gibi Elbette bunu bir betik veya yönetim API 'SI kullanarak da yapabilirsiniz.

Yönetim portalında Active Directory sekmesine tıklayın.

![Portalda WAAD](single-sign-on/_static/image5.png)

Azure hesabınız için otomatik olarak bir Azure AD kiracınız var ve ek dizinler oluşturmak için sayfanın alt kısmındaki **Ekle** düğmesine tıklayabilirsiniz. Örneğin, bir test ortamı ve bir üretim için bir tane olmak üzere bir test ortamı isteyebilirsiniz. Yeni bir dizin adı verdiğiniz şeyleri dikkatle düşünün. Dizin için adınızı kullanır ve ardından, kullanıcılardan biri için bir ad kullanırsanız, bu kafa karıştırıcı olabilir.

![Dizin ekleme](single-sign-on/_static/image6.png)

Portalın bu ortamda Kullanıcı oluşturmak, silmek ve yönetmek için tam desteği vardır. Örneğin, bir kullanıcı eklemek için **Kullanıcılar** sekmesine gidin ve **Kullanıcı Ekle** düğmesine tıklayın.

![Kullanıcı Ekle düğmesi](single-sign-on/_static/image7.png)

![Kullanıcı Ekle iletişim kutusu](single-sign-on/_static/image8.png)

Yalnızca bu dizinde bulunan yeni bir kullanıcı oluşturabilir veya bir Microsoft hesabını bu dizine kullanıcı olarak kaydedebilir veya başka bir Azure AD dizininden bu dizine kullanıcı olarak kaydedebilirsiniz. (Gerçek bir dizinde varsayılan etki alanı ContosoTest.onmicrosoft.com olacaktır. Ayrıca, contoso.com gibi kendi seçme etki alanını da kullanabilirsiniz.)

![Kullanıcı türleri](single-sign-on/_static/image9.png)

![Kullanıcı Ekle iletişim kutusu](single-sign-on/_static/image10.png)

Kullanıcıyı bir role atayabilirsiniz.

![Kullanıcı profili](single-sign-on/_static/image11.png)

Ve hesap geçici bir parolayla oluşturulur.

![Geçici parola](single-sign-on/_static/image12.png)

Bu şekilde oluşturduğunuz kullanıcılar, bu bulut dizinini kullanarak Web uygulamalarınızda anında oturum açabilir.

Kurumsal Çoklu oturum açma için harika olan özellikler, **Dizin tümleştirme** sekmesindedir:

![Dizin tümleştirme sekmesi](single-sign-on/_static/image13.png)

Dizin tümleştirmeyi etkinleştirir ve [bir araç yüklerseniz](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), bu bulut dizinini, zaten kuruluşunuzda kullanmakta olduğunuz mevcut şirket içi Active Directory ile eşitleyebilirsiniz. Ardından, dizininizde depolanan tüm kullanıcılar bu bulut dizininde görünür. Bulut uygulamalarınız artık, mevcut Active Directory kimlik bilgilerini kullanarak tüm çalışanlarınızın kimliğini doğrulayabilir. Tüm bu ücretsiz bir deyişle hem eşitleme aracı hem de Azure AD 'nin kendisidir.

Araç, bu ekran görüntüleriyle görebileceğiniz gibi kullanımı kolay bir sihirbazdır. Bunlar, yalnızca temel süreci gösteren bir örnek olan tam yönergeler değildir. Daha ayrıntılı nasıl yapılır-Yapılacaklar bilgileri için, bölümün sonundaki [kaynaklar](#resources) bölümünde bulunan bağlantılara bakın.

![WAAD eşitleme aracı Yapılandırma Sihirbazı](single-sign-on/_static/image14.png)

**İleri**' ye tıklayın ve ardından Azure Active Directory kimlik bilgilerinizi girin.

![WAAD eşitleme aracı Yapılandırma Sihirbazı](single-sign-on/_static/image15.png)

**İleri**' ye tıklayın ve ardından ŞIRKET içi ad kimlik bilgilerinizi girin.

![WAAD eşitleme aracı Yapılandırma Sihirbazı](single-sign-on/_static/image16.png)

**İleri**' ye tıklayın ve ardından bulutta ad parolalarınızın karmasını depolamak istediğinizi belirtin.

![WAAD eşitleme aracı Yapılandırma Sihirbazı](single-sign-on/_static/image17.png)

Bulutta depolayabilmeniz için Parola karması tek yönlü bir karmadır; gerçek parolalar hiçbir şekilde Azure AD 'de depolanmaz. Karmaların bulutta depolanmaya karar verirseniz [Active Directory Federasyon Hizmetleri (AD FS)](https://technet.microsoft.com/library/hh831502.aspx) (ADFS) kullanmanız gerekir. Ayrıca, [ADFS kullanıp kullanmayacağınızı seçerken göz önünde bulundurmanız gereken diğer faktörler](https://technet.microsoft.com/library/jj573653.aspx)de vardır. ADFS seçeneği birkaç ek yapılandırma adımı gerektirir.

Karma değerleri bulutta depolamayı seçerseniz, işiniz bittiğinde, **İleri**' ye tıkladığınızda araç dizinleri eşitlemeye başlar.

![WAAD eşitleme aracı Yapılandırma Sihirbazı](single-sign-on/_static/image18.png)

Ve birkaç dakika sonra işiniz bitti.

![WAAD eşitleme aracı Yapılandırma Sihirbazı](single-sign-on/_static/image19.png)

Bunu yalnızca kuruluştaki bir etki alanı denetleyicisinde, Windows 2003 veya üzeri sürümlerde çalıştırmanız yeterlidir. Ve yeniden başlatma gerekmez. İşiniz bittiğinde tüm kullanıcılarınız bulutta bulunur ve SAML, OAuth veya WS-besi kullanarak herhangi bir Web veya mobil uygulamadan çoklu oturum açma yapabilirsiniz.

Bazen bunun ne kadar güvenli olduğunu, Microsoft 'un kendi hassas iş verileri için mi kullandığını öğrenmek istiyorduk. Yanıt Evet. Örneğin, [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)adresinden Iç Microsoft SharePoint sitesine giderseniz, oturum açmanız istenir.

![Office 365 oturum açma](single-sign-on/_static/image20.png)

Microsoft, ADFS 'yi etkinleştirdi, bu nedenle bir Microsoft KIMLIĞI girdiğinizde bir ADFS oturum açma sayfasına yönlendirilirsiniz.

![ADFS oturum açma](single-sign-on/_static/image21.png)

Bir iç Microsoft AD hesabında depolanan kimlik bilgilerini girdikten sonra bu iç uygulamaya erişebilirsiniz.

![MS SharePoint sitesi](single-sign-on/_static/image22.png)

Azure AD kullanılabilir hale gelmeden önce ADFS ayarlamış olduğumuz ancak oturum açma işlemi buluttaki bir Azure AD dizininden ilerleyeceğinden, genellikle bir AD oturum açma sunucusu kullanıyoruz. Önemli belgelerimizi, kaynak denetimi, performans yönetim dosyalarını, satış raporlarınızı ve daha fazlasını buluta yerleştirdik ve bu aynı çözümü bu şekilde güvenli hale getirmek için kullanın.

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>Çoklu oturum açma için Azure AD kullanan bir ASP.NET uygulaması oluşturma

Visual Studio, birkaç ekran görüntüsünü görebileceğiniz gibi, çoklu oturum açma için Azure AD kullanan bir uygulama oluşturmayı gerçekten kolaylaştırır.

MVC veya Web Forms yeni bir ASP.NET uygulaması oluşturduğunuzda, varsayılan kimlik doğrulama yöntemi ASP.NET Identity. Azure AD 'de bunu değiştirmek için, bir **kimlik doğrulaması Değiştir** düğmesine tıklayın.

![Kimlik Doğrulamayı Değiştirme](single-sign-on/_static/image23.png)

Kuruluş hesapları ' nı seçin, etki alanı adınızı girin ve çoklu oturum aç ' ı seçin.

![Kimlik doğrulamasını Yapılandır iletişim kutusu](single-sign-on/_static/image24.png)

Ayrıca, uygulamaya dizin verileri için okuma veya okuma/yazma izni verebilirsiniz. Bunu yaparsanız, kullanıcıların telefon numarasını aramak, ofiste olup olmadığını bulmak, son oturum açtıklarında, vb. gibi [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) kullanabilir.

Yapmanız gereken tek şey, Visual Studio 'nun Azure AD kiracınız için bir yöneticinin kimlik bilgilerini ister ve ardından hem projenizi hem de Azure AD kiracınızı yeni uygulama için yapılandıracaktır.

Projeyi çalıştırdığınızda, bir oturum açma sayfası görürsünüz ve Azure AD dizininizde bir kullanıcının kimlik bilgileriyle oturum açabilirsiniz.

![Org hesabı oturum açma](single-sign-on/_static/image25.png)

![Oturum açıldı](single-sign-on/_static/image26.png)

Uygulamayı Azure 'a dağıttığınızda, tek yapmanız gereken, bir **Kurumsal kimlik doğrulamasını etkinleştir** onay kutusunu seçin ve Visual Studio bir kez daha sonra sizin için tüm yapılandırmayı üstlenir.

![Web Yayımlama](single-sign-on/_static/image27.png)

Bu ekran görüntüleri, Azure AD kimlik doğrulaması kullanan bir uygulamanın nasıl oluşturulduğunu gösteren kapsamlı bir adım adım öğreticiden gelir: [Azure Active Directory ile ASP.NET uygulamaları geliştirme](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).

## <a name="summary"></a>Özet

Bu bölümde Azure Active Directory, Visual Studio ve ASP.NET 'in, kuruluşunuzun kullanıcıları için Internet uygulamalarında çoklu oturum açmayı ayarlamayı kolaylaştırdığını gördünüz. Kullanıcılarınız, iç ağınızdaki Active Directory kullanarak oturum açmak için kullandıkları kimlik bilgilerini kullanarak Internet uygulamalarında oturum açabilir.

Bir [sonraki bölümde](data-storage-options.md) , bir bulut uygulaması için kullanılabilen veri depolama seçenekleri sunulmaktadır.

<a id="resources"></a>
## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Azure Active Directory belgeleri](https://docs.microsoft.com/azure/active-directory/). Windowsazure.com sitesinde Azure AD belgeleri için Portal sayfası. Adım adım öğreticiler için, **geliştirme** bölümüne bakın.
- [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/). Azure 'da Multi-Factor Authentication hakkındaki belgeler için Portal sayfası.
- [Kuruluş hesabı kimlik doğrulama seçenekleri](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions). Visual Studio 2013 yeni-proje iletişim kutusundaki Azure AD kimlik doğrulaması seçeneklerinin açıklaması.
- [Microsoft desenleri ve uygulamaları-federal kimlik düzeni](https://msdn.microsoft.com/library/dn589790.aspx).
- [Nasıl yapılır: Azure Active Directory eşitleme aracını yükler](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).
- [Active Directory Federasyon Hizmetleri (AD FS) 2,0 Içerik Haritası](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx). ADFS 2,0 hakkındaki belgelerin bağlantıları.
- [Bir Windows Azure AD uygulamasında rol tabanlı ve ACL tabanlı yetkilendirme](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1). Örnek uygulama.
- [Azure Active Directory Graph API blogu](https://blogs.msdn.com/b/aadgraphteam/).
- [Bir karma kimlik altyapısında BYOD ve Dizin tümleştirmesinde Access Control](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=). Teknik Ed 2014 oturum videosu, Gayana Ed Dadyan.

> [!div class="step-by-step"]
> [Önceki](web-development-best-practices.md)
> [İleri](data-storage-options.md)
