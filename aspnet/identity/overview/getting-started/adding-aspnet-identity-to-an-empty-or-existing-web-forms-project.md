---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: Boş veya var olan bir Web Forms projeye ASP.NET Identity ekleme-ASP.NET 4. x
author: raquelsa
description: Bu öğreticide, bir ASP.NET uygulamasına ASP.NET Identity (ASP.NET için üyelik sistemi) nasıl ekleneceği gösterilmektedir. Yeni bir Web Forms veya MVC oluşturduğunuzda...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584128"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>Boş veya Mevcut Bir Web Forms Projesine ASP.NET Identity Ekleme

> Bu öğreticide, bir ASP.NET uygulamasına [ASP.NET Identity](introduction-to-aspnet-identity.md) (ASP.NET için yeni üyelik sistemi) nasıl ekleneceği gösterilmektedir.
> 
> Visual Studio 2017 RTM 'de tek tek hesaplarla yeni bir Web Forms veya MVC projesi oluşturduğunuzda, Visual Studio gerekli tüm paketleri yükler ve tüm gerekli sınıfları sizin için ekler. Bu öğreticide, mevcut Web Forms projenize veya yeni boş bir projeye ASP.NET Identity desteği ekleme adımları gösterilmektedir. Yüklemeniz gereken tüm NuGet paketlerini ve eklemeniz gereken sınıfları ana hatlarıyla barındıracak. Kullanıcı yönetimi ve kimlik doğrulaması için tüm ana giriş noktası API 'Lerini vurgularken yeni kullanıcıları kaydetmek ve oturum açmak için örnek Web Forms üzerine gidecağım. Bu örnek, Entity Framework oluşturulan SQL veri depolaması için ASP.NET Identity varsayılan uygulamasını kullanır. Bu öğreticide, SQL veritabanı için LocalDB kullanacağız.
> 

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity kullanmaya başlayın

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)' i yükleyip çalıştırarak başlayın.
2. Başlangıç sayfasından **Yeni proje** ' yi seçin veya menüsünü ve ardından **Dosya**' yı ve ardından **Yeni proje**' yi seçin.
3. Sol bölmede, **görsel C#** ' i genişletin, ardından **Web**ve **ASP.NET Web uygulaması (.NET Framework)** öğesini seçin. Projenizi "Webformsıdentity" olarak adlandırın ve **Tamam**' ı seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. **Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   **Kimlik doğrulamasını Değiştir** düğmesinin devre dışı bırakıldığını ve bu şablonda kimlik doğrulama desteğinin sağlandığına dikkat edin. Web Forms, MVC ve Web API 'SI şablonları, kimlik doğrulama yaklaşımını seçmenizi sağlar.

## <a name="add-identity-packages-to-your-app"></a>Uygulamanıza kimlik paketleri ekleyin

Çözüm Gezgini, projenize sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin. **Microsoft. Aspnet. Identity. EntityFramework** paketini arayın ve yükler. 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
Bu paketin bağımlılık paketlerini yükleyeceğini unutmayın: **EntityFramework** ve **Microsoft ASP.NET Identity Core**.

## <a name="add-a-web-form-to-register-users"></a>Kullanıcıları kaydetmek için bir Web formu ekleme

1. **Çözüm Gezgini**, projenize sağ tıklayın ve **Ekle**' yi ve ardından **Web formu**' nu seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. **Öğe Için ad belirtin** iletişim kutusunda, yeni Web formu **kaydını**adlandırın ve ardından **Tamam** ' ı seçin.
3. Oluşturulan *register. aspx* dosyasındaki biçimlendirmeyi aşağıdaki kodla değiştirin. Kod değişiklikleri vurgulanır. 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > Bu, yeni bir ASP.NET Web Forms projesi oluşturduğunuzda oluşturulan *register. aspx* dosyasının yalnızca Basitleştirilmiş bir sürümüdür. Yukarıdaki biçimlendirme form alanları ve yeni bir kullanıcıyı kaydetmek için bir düğme ekler.
4. *Register.aspx.cs* dosyasını açın ve dosyanın içeriğini aşağıdaki kodla değiştirin:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. Yukarıdaki kod, yeni bir ASP.NET Web Forms projesi oluşturduğunuzda oluşturulan *register.aspx.cs* dosyasının basitleştirilmiş bir sürümüdür.
    > 2. *Identityuser* sınıfı, *IUser* arabiriminin varsayılan EntityFramework uygulamasıdır. *IUser* arabirimi, bir kullanıcı Için ASP.NET Identity çekirdekli en düşük arabirimdir.
    > 3. *UserStore* sınıfı, bir Kullanıcı deposunun varsayılan EntityFramework uygulamasıdır. Bu sınıf ASP.NET Identity çekirdeğin en düşük arabirimlerini uygular: *ıuserstore*, *ıuserloginstore*, *ıuserclaimstore* ve *ıuserrolestore*.
    > 4. *UserManager* sınıfı, Kullanıcı Ilgili API 'leri kullanıma sunar. Bu, değişiklikleri otomatik olarak *userStore*'a kaydeder.
    > 5. *Identityresult* sınıfı bir kimlik işleminin sonucunu temsil eder.
5. **Çözüm Gezgini**, projenize sağ tıklayın ve **Ekle**, **ASP.NET klasörü Ekle** ve sonra **uygulama\_verileri**' ni seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. *Web. config* dosyasını açın ve Kullanıcı bilgilerini depolamak için kullanacağız veritabanına bir bağlantı dizesi girişi ekleyin. Veritabanı, kimlik varlıkları için EntityFramework tarafından çalışma zamanında oluşturulur. Yeni bir Web Forms projesi oluşturduğunuzda, bağlantı dizesi sizin için oluşturulmuş birine benzerdir. Vurgulanan kod, eklemeniz gereken biçimlendirmeyi gösterir:

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > Visual Studio 2015 veya üzeri için `(localdb)\v11.0`, bağlantı dizinizdeki `(localdb)\MSSQLLocalDB` ile değiştirin.
    
7. Projenizde dosya *Kaydet. aspx* ' e sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin. Web uygulamasını derlemek ve çalıştırmak için CTRL + F5 tuşlarına basın. Yeni bir Kullanıcı adı ve parola girin ve ardından **Kaydet**' i seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity doğrulama desteğine sahiptir ve bu örnekte, kimlik çekirdeği paketinden gelen Kullanıcı ve parola doğrulayıcılarındaki varsayılan davranışı doğrulayabilirsiniz. Kullanıcı (`UserValidator`) için varsayılan doğrulayıcının, varsayılan değeri `true`olarak ayarlanmış bir özellik `AllowOnlyAlphanumericUserNames` vardır. Parola (`MinimumLengthValidator`) için varsayılan Doğrulayıcı, Parolada en az 6 karakter olmasını sağlar. Bu doğrulayıcılar, özel doğrulamaya sahip olmak istiyorsanız geçersiz kılınabilen `UserManager` özelliklerdir.

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>Entity Framework tarafından oluşturulan LocalDb kimlik veritabanını ve tablolarını doğrulayın

1. **Görünüm** menüsünde **Sunucu Gezgini**' yi seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. **DefaultConnection (Webformsıdentity)** öğesini genişletin, **Tablolar**' ı genişletin, **aspnetusers** öğesine sağ tıklayın ve ardından **tablo verilerini göster**' i seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>Uygulamayı OWıN kimlik doğrulaması için yapılandırma

Bu noktada yalnızca kullanıcı oluşturmaya yönelik destek ekledik. Şimdi, bir kullanıcının oturum açması için nasıl kimlik doğrulaması ekleyebileceğinizi göstereceğiz. ASP.NET Identity, form kimlik doğrulaması için Microsoft OWıN kimlik doğrulama ara yazılımını kullanır. OWıN tanımlama bilgisi kimlik doğrulaması, [owın](https://msdn.microsoft.com/magazine/dn451439.aspx) veya IIS üzerinde barındırılan herhangi bir çerçeve tarafından kullanılabilen bir tanımlama bilgisi ve talep tabanlı kimlik doğrulama mekanizmasıdır. Bu modelde, ASP.NET MVC ve Web Forms dahil olmak üzere birden çok çerçeve genelinde aynı kimlik doğrulama paketleri kullanılabilir. Proje Katana hakkında daha fazla bilgi ve bir konakta bir ana bilgisayar çalıştırmak için bkz. [Katana proje Ile çalışmaya](https://msdn.microsoft.com/magazine/dn451439.aspx)başlama.

## <a name="install-authentication-packages-to-your-application"></a>Uygulamanıza kimlik doğrulama paketleri yükler

1. Çözüm Gezgini, projenize sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin. ***Microsoft. Aspnet. Identity. Owin*** paketini arayın ve yükler. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. ***Microsoft. Owin. Host. SystemWeb*** paketini arayın ve yükler.

    > [!NOTE]
    > **Microsoft. Aspnet. Identity. Owin** paketi, ASP.NET Identity Core paketleri tarafından tüketilen owın kimlik doğrulama ara yazılımını yönetmek ve yapılandırmak IÇIN BIR Owin uzantı sınıfları kümesi içerir.
    > **Microsoft. Owin. Host. SystemWeb** PAKETI, owın tabanlı uygulamaların ASP.NET istek işlem HATTıNı kullanarak IIS üzerinde çalışmasını sağlayan bir owın sunucusu içerir. Daha fazla bilgi için bkz. [IIS Tümleşik ardışık düzeninde Owın ara yazılımı](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md).

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>OWıN başlangıç ve kimlik doğrulama yapılandırma sınıfları ekleme

1. **Çözüm Gezgini**, projenize sağ tıklayın, **Ekle**' yi ve ardından **Yeni öğe Ekle**' yi seçin. Arama metin kutusu iletişim kutusunda "*owın*" yazın. "*Startup*" sınıfını adlandırın ve **Ekle**' yi seçin. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. Startup.cs dosyasında, OWıN tanımlama bilgisi kimlik doğrulamasını yapılandırmak için aşağıda gösterilen vurgulanmış kodu ekleyin.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > Bu sınıf, OWıN başlangıç sınıfının belirtilmesine yönelik `OwinStartup` özniteliğini içerir. Her OWıN uygulamasının, uygulama ardışık düzeni için bileşenleri belirttiğiniz bir başlangıç sınıfı vardır. Bu model hakkında daha fazla bilgi için bkz. [Owın başlangıç sınıfı algılama](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) .

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>Kullanıcılara kaydolmak ve oturum açmak için Web formları ekleme

1. *Register.aspx.cs* dosyasını açın ve kayıt başarılı olduğunda kullanıcıya oturum açan aşağıdaki kodu ekleyin.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - ASP.NET Identity ve OWıN tanımlama bilgisi kimlik doğrulaması talep tabanlı sistem olduğundan, çerçeve, uygulama geliştiricisinin Kullanıcı için bir [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) oluşturmasını gerektirir. ClaimsIdentity kullanıcının ait olduğu roller gibi kullanıcı için tüm taleplerle ilgili bilgiler içerir. Ayrıca bu aşamada Kullanıcı için daha fazla talep ekleyebilirsiniz.
    > - Kullanıcı oturumunu OWıN ' dan AuthenticationManager ' a ve `SignIn` çağırarak ve yukarıda gösterildiği gibi ClaimsIdentity ' a geçirerek kullanarak oturum açabilirsiniz. Bu kod, kullanıcıya oturum açacaktır ve bir tanımlama bilgisi de oluşturur. Bu çağrı, [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) modülü tarafından kullanılan [Formauthentication. SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) öğesine benzerdir.
2. **Çözüm Gezgini**, projenize sağ tıklayın, **Ekle**' yi ve ardından **Web formu**' nu seçin. Web formunun **oturum**açmasını adlandırın.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. *Login. aspx* dosyasının içeriğini aşağıdaki kodla değiştirin:

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. *Login.aspx.cs* dosyasının içeriğini aşağıdaki kodla değiştirin:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` şimdi geçerli kullanıcının durumunu denetler ve `Context.User.Identity.IsAuthenticated` durumuna göre işlem gerçekleştirir.
    >   **Oturum açan kullanıcı adını görüntüle** : Microsoft ASP.NET Identity Framework, oturum açan kullanıcının `UserName` ve `UserId` almanızı sağlayan [System. Security. Principal. iıdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) üzerine uzantı yöntemleri ekledi. Bu uzantı yöntemleri `Microsoft.AspNet.Identity.Core` derlemesinde tanımlanmıştır. Bu genişletme yöntemleri [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) için yerini alır.
    > - SignIn yöntemi: `This` yöntemi bu örnekteki önceki `CreateUser_Click` yönteminin yerini alır ve şimdi kullanıcıyı başarıyla oluşturduktan sonra Kullanıcı oturumunu kapatır.   
    >   Microsoft OWIN Framework, bir `IOwinContext`başvurusu almanızı sağlayan `System.Web.HttpContext` uzantı yöntemleri ekledi. Bu uzantı yöntemleri `Microsoft.Owin.Host.SystemWeb` derlemede tanımlanmıştır. `OwinContext` sınıfı, geçerli istekte bulunan kimlik doğrulama ara yazılım işlevlerini temsil eden bir `IAuthenticationManager` özelliğini kullanıma sunar. OWIN `AuthenticationManager` kullanarak ve `SignIn` çağırarak ve yukarıda gösterildiği gibi `ClaimsIdentity` geçirerek Kullanıcı oturumunu açabilirsiniz. ASP.NET Identity ve OWıN tanımlama bilgisi kimlik doğrulaması talep tabanlı sistem olduğundan, çerçeve, uygulamanın kullanıcı için bir `ClaimsIdentity` oluşturmasını gerektirir. `ClaimsIdentity`, kullanıcının ait olduğu roller gibi kullanıcı için tüm taleplerle ilgili bilgiler içerir. Ayrıca bu aşamada Kullanıcı için daha fazla talep ekleyebilirsiniz. Bu kod, kullanıcıya oturum açacaktır ve bir tanımlama bilgisi de oluşturur. Bu çağrı, [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) modülü tarafından kullanılan [Formauthentication. SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) öğesine benzerdir.
    > - `SignOut` yöntemi: OWIN `AuthenticationManager` bir başvuru alır ve `SignOut`çağırır. Bu, [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) modülü tarafından kullanılan [FormsAuthentication. SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) yöntemine benzerdir.
5. Web uygulamasını derlemek ve çalıştırmak için **CTRL + F5** tuşlarına basın. Yeni bir Kullanıcı adı ve parola girin ve ardından **Kaydet**' i seçin.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   Note: Bu noktada yeni Kullanıcı oluşturulur ve oturum açar.
6. **Günlüğe kaydet** düğmesini seçin. Oturum açma formuna yönlendirilirsiniz.
7. Geçersiz bir Kullanıcı adı veya parola girin ve **oturum aç** düğmesini seçin. 
   `UserManager.Find` yöntemi null ve hata iletisi döndürür: " *Geçersiz Kullanıcı adı veya parola* " görüntülenir.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
