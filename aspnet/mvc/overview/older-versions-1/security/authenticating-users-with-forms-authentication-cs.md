---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: Forms kimlik doğrulaması ile kullanıcıların kimliğiniC#doğrulama () | Microsoft Docs
author: microsoft
description: MVC uygulamanızda belirli sayfaları korumak için [Yetkilendir] özniteliğini nasıl kullanacağınızı öğrenin. Web sitesi yönetimini de nasıl kullanacağınızı öğrenirsiniz...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bed2eafa47fec25ac04cb07e0037f596494bb7d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541512"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>Forms Kimlik Doğrulaması ile Kullanıcıların Kimliğini Doğrulama (C#)

[Microsoft](https://github.com/microsoft) tarafından

> MVC uygulamanızda belirli sayfaları korumak için [Yetkilendir] özniteliğini nasıl kullanacağınızı öğrenin. Kullanıcı ve rolleri oluşturmak ve yönetmek için Web sitesi yönetim aracı 'nın nasıl kullanılacağını öğrenirsiniz. Ayrıca Kullanıcı hesabı ve rol bilgilerinin nerede depolandığını nasıl yapılandıracağınızı öğreneceksiniz.

Bu öğreticinin amacı, ASP.NET MVC uygulamalarınızda görünümleri parolayla korumak için Forms kimlik doğrulamasını nasıl kullanabileceğinizi açıklamaktır. Kullanıcı ve rolleri oluşturmak için Web sitesi yönetim aracı 'nın nasıl kullanılacağını öğrenirsiniz. Ayrıca, yetkisiz kullanıcıların denetleyici eylemlerini yürütmesini nasıl önleyeceğinizi öğreneceksiniz. Son olarak, Kullanıcı adlarının ve parolaların nerede depolandığını nasıl yapılandıracağınızı öğrenirsiniz.

#### <a name="using-the-web-site-administration-tool"></a>Web sitesi yönetim aracı 'nı kullanma

Başka bir şey yapmadan önce bazı kullanıcılar ve roller oluşturarak başlamamız gerekir. Yeni Kullanıcı ve rol oluşturmanın en kolay yolu, Visual Studio 2008 Web sitesi yönetim aracından faydalanabilir. Bu aracı **, proje, ASP.NET yapılandırma**menü seçeneğini belirleyerek başlatabilirsiniz. Alternatif olarak, Çözüm Gezgini penceresinin en üstünde görünen dünyaya vurarak (biraz Scary) simgesine tıklayarak web sitesi yönetim aracını başlatabilirsiniz (bkz. Şekil 1).

**Şekil 1 – Web sitesi yönetim aracı başlatılıyor**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

Web sitesi yönetim aracı 'nda Güvenlik sekmesini seçerek yeni kullanıcılar ve roller oluşturursunuz. Stephen adlı yeni bir kullanıcı oluşturmak için **Kullanıcı oluştur** bağlantısına tıklayın (bkz. Şekil 2). Stephen kullanıcısına istediğiniz parolayı (örneğin, *gizli*) sağlayın.

**Şekil 2 – yeni bir Kullanıcı oluşturma**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

Önce rolleri etkinleştirerek ve bir veya daha fazla rol tanımlayarak yeni roller oluşturursunuz. Rolleri **Etkinleştir** bağlantısına tıklayarak rolleri etkinleştirin. Ardından, **Roller oluştur veya Yönet** bağlantısına tıklayarak *Yöneticiler* adlı bir rol oluşturun (bkz. Şekil 3).

**Şekil 3 – yeni bir rol oluşturma**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

Son olarak, Sally adlı yeni bir kullanıcı oluşturun ve kullanıcı oluştur bağlantısına tıklayıp yöneticiler ' i (bkz. Şekil 4) seçerek Yöneticiler rolüyle Sally ilişkilendirin.

**Şekil 4: bir role Kullanıcı ekleme**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

Tümü bir kez söylenir ve tamamlandığında, Stephen ve Sally adlı iki yeni kullanıcınız olmalıdır. Ayrıca, Yöneticiler adlı yeni bir rolünüzün olması gerekir. Sally, Yöneticiler rolünün bir üyesidir ve Stephen değildir.

#### <a name="requiring-authorization"></a>Yetkilendirme gerektirme

Kullanıcı, eyleme [Yetkilendir] özniteliği ekleyerek bir denetleyici eylemi çağırmadan önce bir kullanıcının kimliğinin doğrulanmasını zorunlu kılabilirsiniz. [Yetkilendir] özniteliğini tek bir denetleyici eylemine uygulayabilir veya bu özniteliği bir denetleyici sınıfına uygulayabilirsiniz.

Örneğin, liste 1 ' deki denetleyici Companygizlilikler () adlı bir eylem gösterir. Bu eylem [Yetkilendir] özniteliğiyle donatılmış olduğundan, bu eylem, bir kullanıcının kimliği doğrulanmadıkça çağrılamaz.

**Listeleme 1 – Controllers\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

Tarayıcınızın adres çubuğuna/Home/companygizlilikler URL 'sini girerek Companygizlilikler () eylemini çağırırsanız ve kimliği doğrulanmış bir kullanıcı değilseniz, otomatik olarak oturum açma görünümüne yönlendirilirsiniz (bkz. Şekil 5).

**Şekil 5 – oturum açma görünümü**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

Kullanıcı adınızı ve parolanızı girmek için oturum açma görünümünü kullanabilirsiniz. Kayıtlı bir kullanıcı değilseniz, **Kaydet bağlantısına tıklayarak kayıt görünümüne** gidebilirsiniz (bkz. Şekil 6). Yeni bir kullanıcı hesabı oluşturmak için kayıt görünümünü kullanabilirsiniz.

**Şekil 6 – kayıt görünümü**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

Başarıyla oturum açtıktan sonra Companygizlilikler görünümü ' ne bakabilirsiniz (bkz. Şekil 7). Varsayılan olarak, tarayıcı pencerenizi kapatıncaya kadar oturum açmaya devam edersiniz.

**Şekil 7 – Companygizlilikler görünümü**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>Kullanıcı adına veya kullanıcı rolüne göre yetkilendirme

Bir denetleyici eylemine erişimi belirli bir Kullanıcı kümesiyle veya belirli bir kullanıcı rolü kümesiyle kısıtlamak için [Yetkilendir] özniteliğini kullanabilirsiniz. Örneğin, liste 2 ' deki değiştirilmiş giriş denetleyicisi, StephenSecrets () ve Tınsırlar () adlı iki yeni eylem içerir.

**Listeleme 2 – Controllers\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

Yalnızca Stephen Kullanıcı adı olan bir Kullanıcı StephenSecrets () eylemini çağırabilir. Diğer tüm kullanıcılar oturum açma görünümüne yönlendirilir. Users özelliği, Kullanıcı hesabı adlarının virgülle ayrılmış bir listesini kabul eder.

Yalnızca Yöneticiler rolündeki kullanıcılar Tınsırlar () eylemini çağırabilir. Örneğin, Sally Administrators grubunun bir üyesi olduğundan, Tınsırlar () eylemini çağırabilir. Diğer tüm kullanıcılar oturum açma görünümüne yönlendirilir. Roles Özelliği, rol adlarının virgülle ayrılmış bir listesini kabul eder.

#### <a name="configuring-authentication"></a>Kimlik doğrulamasını yapılandırma

Bu noktada, Kullanıcı hesabının ve rol bilgilerinin nerede depolanmakta olduğunu merak ediyor olabilirsiniz. Varsayılan olarak, bilgiler MVC uygulamanızın App\_Data klasöründe bulunan ASPNETDB. mdf adlı bir (RANU) SQL Express veritabanında depolanır. Bu veritabanı, üyeliği kullanmaya başladığınızda ASP.NET Framework tarafından otomatik olarak oluşturulur.

Çözüm Gezgini penceresinde ASPNETDB. mdf veritabanını görmek için, önce menü seçeneği projesi ' ni seçmelisiniz, tüm dosyaları göster ' i seçmeniz gerekir.

Varsayılan SQL Express veritabanını kullanmak, bir uygulama geliştirirken iyi bir uygulamadır. Ancak büyük olasılıkla, bir üretim uygulaması için varsayılan ASPNETDB. mdf veritabanını kullanmak istemezsiniz. Bu durumda, aşağıdaki iki adımı tamamlayarak Kullanıcı hesabı bilgilerinin nerede depolandığını değiştirebilirsiniz:

1. Uygulama Hizmetleri veritabanı nesnelerini üretim veritabanınıza ekleyin-uygulama Bağlantı dizenizi üretim veritabanınıza işaret etmek üzere değiştirin

İlk adım, tüm gerekli veritabanı nesnelerini (tablolar ve saklı yordamlar) üretim veritabanınıza eklemektir. Bu nesneleri yeni bir veritabanına eklemenin en kolay yolu, ASP.NET SQL Server kurulum sihirbazından faydalanabilir (bkz. Şekil 8). Bu aracı Microsoft Visual Studio 2008 program grubundan Visual Studio 2008 komut Istemi ' ni açıp komut isteminden aşağıdaki komutu yürüterek başlatabilirsiniz:

ASPNET\_regsql

**Şekil 8 – ASP.NET SQL Server Kurulum Sihirbazı**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

ASP.NET SQL Server Kurulum Sihirbazı, ağınızdaki bir SQL Server veritabanını seçmenizi ve ASP.NET uygulama hizmetleri için gereken tüm veritabanı nesnelerini yüklemenizi sağlar. Veritabanı sunucusunun yerel makinenizde bulunması gerekli değildir.

> [!NOTE] 
> 
> ASP.NET SQL Server Kurulum Sihirbazı 'Nı kullanmak istemiyorsanız, aşağıdaki klasöre uygulama Hizmetleri veritabanı nesneleri eklemek için SQL betikleri bulabilirsiniz:
> 
> > C:\Windows\Microsoft.NET\Framework\v2.0.50727

Gerekli veritabanı nesnelerini oluşturduktan sonra, MVC uygulamanız tarafından kullanılan veritabanı bağlantısını değiştirmeniz gerekir. Web yapılandırma (Web. config) dosyanızdaki ApplicationServices bağlantı dizesini, üretim veritabanına işaret eden şekilde değiştirin. Örneğin, Listeleme 3 ' teki değiştirilen bağlantı Myüretim DB adlı bir veritabanına işaret eder (özgün ApplicationServices bağlantı dizesi açıklama eklenmiş).

**Listeleme 3 – Web. config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>Veritabanı Izinlerini yapılandırma

Veritabanınıza bağlanmak için tümleşik güvenlik kullanıyorsanız, veritabanınıza oturum açmak için doğru Windows Kullanıcı hesabını eklemeniz gerekir. Doğru hesap, ASP.NET geliştirme sunucusunu veya Internet Information Services Web sunucunuz olarak kullanıp kullanmayacağınızı bağlıdır. Doğru Kullanıcı hesabı da işletim sisteminize bağlıdır.

ASP.NET geliştirme sunucusunu kullanıyorsanız (Visual Studio tarafından kullanılan varsayılan Web sunucusu), uygulamanız Windows Kullanıcı hesabınızın bağlamı içinde yürütülür. Bu durumda, bir veritabanı sunucusu oturumu olarak Windows kullanıcı hesabınızı eklemeniz gerekir.

Alternatif olarak, Internet Information Services kullanıyorsanız, ASPNET hesabını ya da NT YETKILISI/ağ HIZMETI hesabını bir veritabanı sunucusu oturumu olarak eklemeniz gerekir. Windows XP kullanıyorsanız, ASPNET hesabını veritabanınıza oturum açma olarak ekleyin. Windows Vista veya Windows Server 2008 gibi daha yeni bir işletim sistemi kullanıyorsanız, veritabanı oturumu açmak için NT YETKILISI/ağ HIZMETI hesabını ekleyin.

Veritabanınıza Microsoft SQL Server Management Studio kullanarak yeni bir kullanıcı hesabı ekleyebilirsiniz (bkz. Şekil 9).

**Şekil 9 – yeni Microsoft SQL Server oturum açma oluşturma**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

Gerekli oturum açma bilgilerini oluşturduktan sonra, oturum açma bilgilerini doğru veritabanı rolleriyle bir veritabanı kullanıcısına eşlemeniz gerekir. Oturum aç ' a çift tıklayın ve Kullanıcı eşleme sekmesini seçin. bir veya daha fazla uygulama Hizmetleri veritabanı rolü seçin. Örneğin, kullanıcıların kimliğini doğrulamak için, ASPNET\_üyeliğini\_BasicAccess veritabanı rolü ' ne etkinleştirmeniz gerekir. Yeni kullanıcılar oluşturmak için ASPNET\_üyeliğini\_FullAccess veritabanı rolüne (bkz. Şekil 10) etkinleştirmeniz gerekir.

**Şekil 10: Uygulama Hizmetleri veritabanı rolleri ekleme**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>Özet

Bu öğreticide, ASP.NET MVC uygulaması oluştururken Forms kimlik doğrulamasını nasıl kullanacağınızı öğrendiniz. İlk olarak, Web sitesi yönetim aracı 'nın avantajlarından yararlanarak yeni kullanıcılar ve roller oluşturmayı öğrendiniz. Bundan sonra, yetkisiz kullanıcıların denetleyici eylemlerini yürütmesini engellemek için [Yetkilendir] özniteliğini nasıl kullanacağınızı öğrendiniz. Son olarak, MVC uygulamanızı, Kullanıcı ve rol bilgilerini bir üretim veritabanında depolamak üzere nasıl yapılandıracağınızı öğrendiniz.

> [!div class="step-by-step"]
> [Next](authenticating-users-with-windows-authentication-cs.md)
