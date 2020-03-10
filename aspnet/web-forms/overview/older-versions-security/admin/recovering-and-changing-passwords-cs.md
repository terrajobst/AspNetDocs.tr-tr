---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
title: Parolaları kurtarma ve değiştirme (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET, parolaları kurtarma ve değiştirme konusunda yardım almak için iki Web denetimi içerir. PasswordRecovery denetimi, bir ziyaretçinin kayıp PA 'yi kurtarmasını sağlar...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 19c4d042-4e34-4b44-9f1d-6bf2253ba366
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
msc.type: authoredcontent
ms.openlocfilehash: 8c07b8a3c36e4863c6d2d356b8483544ac4cafeb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566880"
---
# <a name="recovering-and-changing-passwords-c"></a>Parolaları Kurtarma ve Değiştirme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.13.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_cs.pdf)

> ASP.NET, parolaları kurtarma ve değiştirme konusunda yardım almak için iki Web denetimi içerir. PasswordRecovery denetimi, bir ziyaretçinin kayıp parolasını kurtarmasını sağlar. ChangePassword denetimi kullanıcının parolasını güncelleştirmesine izin verir. Bu öğretici serisinin tamamında gördüğdiğimiz diğer oturumla ilgili Web denetimleri gibi, PasswordRecovery ve ChangePassword denetimleri, kullanıcıların parolalarını sıfırlamak veya değiştirmek için arka planda üyelik çerçevesiyle birlikte çalışır.

## <a name="introduction"></a>Giriş

Bankanmın Web siteleri, yardımcı program şirketi, telefon şirketi, e-posta hesapları ve kişiselleştirilmiş Web portallarının yanı sıra, çoğu kişi gibi birçok kişinin farklı parolalara sahip olduğu anlaşılıyor. Bu günlerde çok sayıda kimlik bilgisi sayesinde kişilerin parolalarını unutmaları çok seyrek değildir. Bu hesap için, Kullanıcı hesapları sunan web siteleri, kullanıcının parolasını kurtarmasına yönelik bir yol içermesi gerekir. Bu işlem genellikle yeni, rastgele bir parola oluşturmayı ve dosyanın dosyadaki e-posta adresine e-posta ile uygulamayı içerir. Yeni parolalarını aldıktan sonra, çoğu kullanıcı siteye geri döner ve parolalarını rastgele oluşturulan bir şekilde daha iyi bir şekilde olarak değiştirir.

ASP.NET, parolaları kurtarma ve değiştirme konusunda yardım almak için iki Web denetimi içerir. PasswordRecovery denetimi, bir ziyaretçinin kayıp parolasını kurtarmasını sağlar. ChangePassword denetimi kullanıcının parolasını güncelleştirmesine izin verir. Bu öğretici serisinin tamamında gördüğdiğimiz diğer oturumla ilgili Web denetimleri gibi, PasswordRecovery ve ChangePassword denetimleri, kullanıcıların parolalarını sıfırlamak veya değiştirmek için arka planda üyelik çerçevesiyle birlikte çalışır.

Bu öğreticide, bu iki denetimi kullanmayı inceleyeceğiz. Ayrıca, bir kullanıcının parolasını `MembershipUser` sınıfın `ChangePassword` ve `ResetPassword` yöntemleri aracılığıyla nasıl değiştirebileceğimiz ve sıfırlayacağız.

## <a name="step-1-helping-users-recover-lost-passwords"></a>Adım 1: kullanıcıların kayıp parolaları kurtarmasına yardımcı olma

Kullanıcı hesaplarını destekleyen tüm Web sitelerinin, kullanıcılara unutulan parolalarını kurtarmak için bazı mekanizmalar sağlaması gerekir. İyi haber, ASP.NET ' de bu işlevlerin uygulanması, PasswordRecovery Web denetimi için teşekkürler bir Breeze ' dir. PasswordRecovery denetimi, kullanıcıdan Kullanıcı adı ve gerekirse güvenlik sorusunun yanıtını isteyen bir arabirim işler. Ardından Kullanıcı parolasını e-posta ile gönderir.

> [!NOTE]
> E-posta iletileri düz metin olarak kablo üzerinden aktarıldığından, kullanıcının parolasını e-postayla göndermesi ile ilgili güvenlik riskleri vardır.

PasswordRecovery denetimi üç görünümden oluşur:

- **Kullanıcı adı** -ziyaretçi Kullanıcı adını ister. Bu ilk görünümüdür.
- **Soru**-kullanıcının Kullanıcı adı ve güvenlik sorusunu metin olarak, kullanıcının güvenlik sorusunun yanıtını girmesi için bir metin kutusuyla birlikte görüntüler.
- **Başarılı**-kullanıcıya parolasının e-posta ile gönderilmiş olduğunu bildiren bir ileti görüntüler.

Belirtilen görünümler ve PasswordRecovery denetimi tarafından gerçekleştirilen eylemler aşağıdaki Üyelik yapılandırma ayarlarına bağımlıdır:

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

Üyelik çerçevesinin `RequiresQuestionAndAnswer` ayarı, kullanıcıların bir hesap için kaydolurken bir güvenlik sorusu ve yanıtı belirtmesini gerekip gerekmediğini belirtir. <a id="_msoanchor_1"> </a> [*Kullanıcı hesapları oluşturma*](../membership/creating-user-accounts-cs.md) öğreticisinde anlatıldığı gibi, `RequiresQuestionAndAnswer` true ise (varsayılan), CreateUserWizard 'in arabirimi yeni kullanıcının güvenlik sorusu ve yanıtı için TextBox denetimleri içerir; `RequiresQuestionAndAnswer` false ise, böyle bir bilgi toplanmaz. Benzer şekilde, `RequiresQuestionAndAnswer` true ise, Kullanıcı Kullanıcı adını girdikten sonra PasswordRecovery denetimi soru görünümünü görüntüler; parola yalnızca Kullanıcı doğru güvenlik yanıtını girerse kurtarılır. Ancak, `RequiresQuestionAndAnswer` false ise, PasswordRecovery denetimi doğrudan Kullanıcı adı görünümünden başarı görünümüne taşır.

Kullanıcı Kullanıcı adını ya da Kullanıcı adı ve güvenlik yanıtını sağladıktan sonra, `RequiresQuestionAndAnswer` true ise, PasswordRecovery kullanıcının parolasını e-posta ile gönderir. `EnablePasswordRetrieval` seçeneği true olarak ayarlanırsa, Kullanıcı geçerli parolasına e-postayla gönderilir. Yanlış olarak ayarlanırsa ve `EnablePasswordReset` true olarak ayarlanırsa, PasswordRecovery denetimi kullanıcı için yeni, rastgele bir parola oluşturur ve bu yeni parolayı e-posta ile gönderir. Hem `EnablePasswordRetrieval` hem de `EnablePasswordReset` false ise, PasswordRecovery denetimi bir özel durum oluşturur.

> [!NOTE]
> `SqlMembershipProvider` kullanıcıların parolalarını üç biçimden birinde depoladığını hatırlayın: Temizleme, karma hale getirilmiş (varsayılan) veya şifreli. Kullanılan depolama mekanizması, Üyelik yapılandırma ayarlarına bağlıdır; tanıtım uygulaması karma parola biçimini kullanır. Karma parola biçimi kullanılırken, sistem kullanıcının veritabanında depolanan karma sürümden gerçek parolasını belirleyemediği için `EnablePasswordRetrieval` seçeneği false olarak ayarlanmalıdır.

Şekil 1 ' de, PasswordRecovery 'nin arabiriminin ve davranışının üyelik yapılandırması tarafından nasıl etkilenebileceği gösterilmektedir.

[RequiresQuestionAndAnswer, Enablepasswordalımı ve EnablePasswordReset ![, PasswordRecovery denetiminin görünümünü ve davranışını etkiler](recovering-and-changing-passwords-cs/_static/image2.png)](recovering-and-changing-passwords-cs/_static/image1.png)

**Şekil 1**: `RequiresQuestionAndAnswer`, `EnablePasswordRetrieval`ve `EnablePasswordReset`, PasswordRecovery denetiminin görünümünü ve davranışını etkiler ([tam boyutlu görüntüyü görüntülemek için tıklayın](recovering-and-changing-passwords-cs/_static/image3.png))

> [!NOTE]
> <a id="_msoanchor_2"> </a> [*SQL Server için üyelik şeması oluşturma*](../membership/creating-the-membership-schema-in-sql-server-cs.md) öğreticisinde, üyelik sağlayıcısını `RequiresQuestionAndAnswer` true olarak ayarlayarak, false olarak `EnablePasswordRetrieval` ve true olarak `EnablePasswordReset`.

### <a name="using-the-passwordrecovery-control"></a>PasswordRecovery denetimini kullanma

PasswordRecovery denetimini bir ASP.NET sayfasında kullanmaya bakalım. `RecoverPassword.aspx` açın ve bir PasswordRecovery denetimini araç kutusundan tasarımcıya sürükleyip bırakın; `ID` `RecoverPwd`olarak ayarlayın. Login ve CreateUserWizard Web denetimleri gibi, PasswordRecovery denetiminin görünümleri Etiketler, metin kutuları, düğmeler ve doğrulama denetimleri içeren bir zengin bileşik arabirim işler. Görünümlerin görünümünü denetimin stil özellikleri aracılığıyla veya görünümleri şablonlara dönüştürerek özelleştirebilirsiniz. Bunu ilgilendiğiniz okuyucu için bir alıştırma olarak bırakıyorum.

Bir Kullanıcı bu sayfayı ziyaret ettiğinde, Kullanıcı adını girer ve Gönder düğmesine tıklamıştır. Üyelik yapılandırma ayarlarımızda `RequiresQuestionAndAnswer` özelliğini doğru olarak ayarlıyoruz, PasswordRecovery denetimi daha sonra soru görünümünü görüntüler. Kullanıcı doğru güvenlik yanıtını girdikten ve Gönder 'e tıkladıktan sonra, PasswordRecovery denetimi kullanıcının parolasını rastgele oluşturulmuş bir parola ile güncelleştirir ve bu parolayı dosyadaki e-posta adresine e-posta ile gönderir. Tek bir kod satırı yazmak zorunda kalmızdan tüm bu mümkün oldu!

Bu sayfayı test etmeden önce, bir adet son yapılandırma parçası vardır: `Web.config`' de posta teslim ayarlarını belirtmemiz gerekiyor. PasswordRecovery denetimi, e-postayı göndermek için bu ayarları kullanır.

Posta teslim yapılandırması, [`<system.net>` öğenin](https://msdn.microsoft.com/library/6484zdc1.aspx) [`<mailSettings>` öğesi](https://msdn.microsoft.com/library/w355a94k.aspx)aracılığıyla belirtilir. Teslim yöntemini ve varsayılan kimden adresini belirtmek için [`<smtp>` öğesini](https://msdn.microsoft.com/library/ms164240.aspx) kullanın. Aşağıdaki biçimlendirme posta ayarlarını 25 numaralı bağlantı noktasında `smtp.example.com` adlı bir ağ SMTP sunucusunu kullanacak şekilde yapılandırır ve Kullanıcı adı/parola kimlik bilgileri ve parola.

> [!NOTE]
> `<system.net>`, kök `<configuration>` öğesinin bir alt öğesidir ve `<system.web>`eşdüzey öğesidir. Bu nedenle, `<system.net>` öğesini `<system.web>` öğesi içine yerleştirmeyin; Bunun yerine, onu aynı düzeye koyun.

[!code-xml[Main](recovering-and-changing-passwords-cs/samples/sample1.xml)]

Ağ üzerinde bir SMTP sunucusu kullanmanın yanı sıra, gönderilecek e-posta iletilerinin bırakılması gereken bir toplama dizini de belirtebilirsiniz.

SMTP ayarlarını yapılandırdıktan sonra tarayıcıda `RecoverPassword.aspx` sayfasını ziyaret edin. Önce kullanıcı deposunda mevcut olmayan bir Kullanıcı adı girmeyi deneyin. Şekil 2 ' de gösterildiği gibi, PasswordRecovery denetimi kullanıcı bilgilerine erişilmediğini belirten bir ileti görüntüler. İletinin metni denetimin [`UserNameFailureText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)aracılığıyla özelleştirilebilir.

[Geçersiz bir Kullanıcı adı girilirse bir hata Iletisi ![görüntülenir](recovering-and-changing-passwords-cs/_static/image5.png)](recovering-and-changing-passwords-cs/_static/image4.png)

**Şekil 2**: geçersiz bir Kullanıcı adı girilirse bir hata iletisi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](recovering-and-changing-passwords-cs/_static/image6.png))

Şimdi bir Kullanıcı adı girin. Sisteminizdeki bir hesabın kullanıcı adını, erişebileceğiniz ve güvenlik yanıtını bildiğiniz bir e-posta adresiyle kullanın. Kullanıcı adını girdikten ve Gönder ' i tıkladıktan sonra, PasswordRecovery denetimi kendi soru görünümünü görüntüler. Kullanıcı adı görünümünde olduğu gibi, yanlış bir yanıt girerseniz, PasswordRecovery denetiminde bir hata iletisi görüntülenir (bkz. Şekil 3). Bu hata iletisini özelleştirmek için [`QuestionFailureText` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx) kullanın.

[Kullanıcı geçersiz bir güvenlik yanıtı girerse bir hata Iletisi ![görüntülenir](recovering-and-changing-passwords-cs/_static/image8.png)](recovering-and-changing-passwords-cs/_static/image7.png)

**Şekil 3**: Kullanıcı geçersiz bir güvenlik yanıtı girerse bir hata iletisi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](recovering-and-changing-passwords-cs/_static/image9.png))

Son olarak, doğru güvenlik yanıtını girip gönder ' e tıklayın. Arka planda, PasswordRecovery denetimi rastgele bir parola oluşturur, bunu Kullanıcı hesabına atar, kullanıcıya yeni parolalarını bildiren bir e-posta gönderir (bkz. Şekil 4) ve sonra başarı görünümünü görüntüler.

[![kullanıcıya yeni parolası ile bir e-posta gönderilir](recovering-and-changing-passwords-cs/_static/image11.png)](recovering-and-changing-passwords-cs/_static/image10.png)

**Şekil 4**: kullanıcıya yeni parolası ([tam boyutlu görüntüyü görüntülemek için tıklayın](recovering-and-changing-passwords-cs/_static/image12.png)) Ile bir e-posta gönderilir

### <a name="customizing-the-email"></a>E-postayı özelleştirme

PasswordRecovery denetimi tarafından gönderilen varsayılan e-posta, donuk ' dür (bkz. Şekil 4). İleti, `<smtp>` öğenin `from` özniteliğinde belirtilen hesaptan konu parolasıyla ve düz metin gövdesiyle gönderilir:

Lütfen siteye dönüp aşağıdaki bilgileri kullanarak oturum açın.

Kullanıcı adı: *kullanıcıadı*

Parola: *parola*

Bu ileti, PasswordRecovery denetiminin [`SendingMail` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)için bir olay işleyicisi aracılığıyla veya bildirimli olarak [`MailDefinition` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)aracılığıyla özelleştirilebilir. Bu seçeneklerin her ikisini de keşfedelim.

`SendingMail` olay, e-posta iletisi gönderilmeden önce tetiklenir ve e-posta iletisini programlı bir şekilde ayarlamak için en son şansınız olur. Bu olay harekete geçirildiğinde, olay işleyicisi, `Message` özelliği gönderilmek üzere e-postaya bir başvuru içeren [`MailMessageEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)türünde bir nesne iletilir.

`SendingMail` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyerek CC listesine programlı olarak `webmaster@example.com` ekler.

[!code-csharp[Main](recovering-and-changing-passwords-cs/samples/sample2.cs)]

E-posta iletisi ayrıca bildirim temelli yollarla da yapılandırılabilir. PasswordRecovery 'nin `MailDefinition` özelliği, [`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)türünde bir nesnedir. `MailDefinition` sınıfı, `From`, `CC`, `Priority`, `Subject`, `IsBodyHtml`, `BodyFileName`ve diğerleri dahil olmak üzere, e-posta ile ilgili özelliklerin bir konağını sunar. Başlayıcılar için [`Subject` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx) , parola sıfırlandı gibi varsayılan (parola) tarafından kullanılandan daha açıklayıcı bir değere ayarlayın...

E-posta iletisinin gövdesini özelleştirmek için, gövdenin içeriğini içeren ayrı bir e-posta şablonu dosyası oluşturulması gerekir. `EmailTemplates`adlı Web sitesinde yeni bir klasör oluşturarak başlayın. Sonra, `PasswordRecovery.txt` adlı bu klasöre yeni bir metin dosyası ekleyin ve aşağıdaki içeriği ekleyin:

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample3.aspx)]

`<%UserName%>` ve `<%Password%>`yer tutucuların kullanımını göz önünde edin. PasswordRecovery denetimi, e-postayı göndermeden önce bu iki yer tutucuyu kullanıcının Kullanıcı adı ve kurtarılan parolasıyla otomatik olarak değiştirir.

Son olarak, `MailDefinition`[`BodyFileName` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) yeni oluşturduğumuz e-posta şablonuna (`~/EmailTemplates/PasswordRecovery.txt`) işaret edin.

Bu değişiklikleri yaptıktan sonra `RecoverPassword.aspx` sayfasını yeniden ziyaret edin ve Kullanıcı adınızı ve güvenlik yanıtınızı girin. Şekil 5 ' te aşağıdakine benzer bir e-posta alırsınız. `webmaster@example.com` BILGI olduğunu ve konunun ve gövdenin güncelleştirildiğini unutmayın.

[Konunun, gövdenin ve CC listesinin güncelleştirilmiş ![](recovering-and-changing-passwords-cs/_static/image14.png)](recovering-and-changing-passwords-cs/_static/image13.png)

**Şekil 5**: konu, gövde ve bilgi listesi güncelleştirildi ([tam boyutlu görüntüyü görüntülemek için tıklayın](recovering-and-changing-passwords-cs/_static/image15.png))

HTML biçimli e-posta kümesi [`IsBodyHtml`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) doğru bir şekilde göndermek için (varsayılan değer false) ve e-posta şablonunu HTML içerecek şekilde güncelleştirin.

`MailDefinition` özelliği PasswordRecovery sınıfına özgü değil. Adım 2 ' de göreceğiniz gibi, ChangePassword denetimi de `MailDefinition` bir özellik sunar. Üstelik, CreateUserWizard denetimi, yeni kullanıcılara otomatik olarak bir hoş geldiniz e-posta iletisi göndermek için yapılandırabileceğiniz bu tür bir özelliği içerir.

> [!NOTE]
> Şu anda `RecoverPassword.aspx` sayfasına ulaşmak için sol taraftaki gezinmede hiç bağlantı yok. Kullanıcı yalnızca sitede başarıyla oturum açması durumunda bu sayfayı ziyaret ederek ilgileniyor. Bu nedenle, `Login.aspx` sayfasını `RecoverPassword.aspx` sayfasına bir bağlantı içerecek şekilde güncelleştirin.

### <a name="programmatically-resetting-a-users-password"></a>Kullanıcı parolasını program aracılığıyla sıfırlama

Bir kullanıcının parolasını sıfırlarken PasswordRecovery denetimi `MembershipUser` nesnenin [`ResetPassword` yöntemini](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)çağırır. Bu yöntemin iki aşırı yüklemesi vardır:

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -kullanıcının parolasını sıfırlar. `RequiresQuestionAndAnswer` yanlışsa bu aşırı yüklemeyi kullanın.
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -bir kullanıcının parolasını yalnızca sağlanan *Securityanswer* doğruysa sıfırlar. `RequiresQuestionAndAnswer` true ise bu aşırı yüklemeyi kullanın.

Her iki aşırı yükleme de yeni, rastgele oluşturulan parolayı döndürür.

Üyelik çerçevesindeki diğer yöntemlerle olduğu gibi `ResetPassword` yöntemi yapılandırılan sağlayıcıya de temsilci seçer. `SqlMembershipProvider`, kullanıcının Kullanıcı adını, yeni parolayı ve sağlanan parola yanıtını diğer alanlar arasında geçirerek `aspnet_Membership_ResetPassword` saklı yordamını çağırır. Saklı yordam, parola yanıtının eşleştiğinden emin olur ve Kullanıcı parolasını günceller.

Birkaç alt düzey uygulama notu:

- Kilitlenmiş bir Kullanıcı parolasını sıfırlayamaz. Ancak onaylanmamış bir kullanıcı olabilir. Kilitleme ve onaylanan durumları, <a id="_msoanchor_3"> </a> [*Kullanıcı hesaplarını açma ve onaylama*](unlocking-and-approving-user-accounts-cs.md) öğreticisinde daha ayrıntılı olarak ele alınacaktır.
- Parola yanıtı yanlışsa, kullanıcının başarısız parola yanıt denemesi sayısı artırılır. Belirtilen bir zaman penceresi içinde belirtilen sayıda geçersiz güvenlik yanıtı oluşursa, Kullanıcı kilitlenir.

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>Rastgele parolaların nasıl oluşturulduğu hakkında bir kelime

Şekil 4 ve 5 ' teki e-posta iletilerinde gösterilen rastgele oluşturulan parolalar, üyelik sınıfının [`GeneratePassword` yöntemi](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)tarafından oluşturulur. Bu *Yöntem, iki* tamsayı giriş parametreleri ve *uzunluğu* ve olmayan alfasayısal karakterleri kabul eder ve en az *boş* *karakter uzunluğunda* bir dize döndürür. Bu yöntem, üyelik sınıfları veya oturum ile ilgili Web denetimleri içinden çağrıldığında, bu iki parametrenin değerleri, üyelik yapılandırmasının `MinRequiredPasswordLength` ve `MinRequiredNonalphanumericCharacters` özellikleri tarafından belirlenir ve sırasıyla 7 ve 1 olarak ayarlanır.

`GeneratePassword` yöntemi, rastgele karakterlerin seçildiği bir sapma olmamasını sağlamak için şifreleme güçlü rastgele sayı Oluşturucu kullanır. Ayrıca, `GeneratePassword` `public`, rastgele dizeler veya parolalar oluşturmanız gerekiyorsa bunu doğrudan ASP.NET uygulamanızdan kullanabileceğiniz anlamına gelir.

> [!NOTE]
> `SqlMembershipProvider` sınıfı her zaman en az 14 karakter uzunluğunda rastgele bir parola üretir, bu nedenle `MinRequiredPasswordLength` 14 ' ten küçükse, değeri yok sayılır.

## <a name="step-2-changing-passwords"></a>2\. Adım: parolaları değiştirme

Rastgele oluşturulan parolaların anımsanması zordur. Şekil 4: `WWGUZv(f2yM:Bd`gösterildiği parolayı göz önünde bulundurun. Bu belleği belleğe yürütmeyi deneyin! Daha az ki, bir Kullanıcı bu sıralamanın rastgele oluşturulmuş bir parolasıyla gönderildikten sonra, parolayı daha kolay bir şekilde değiştirmek ister.

Parolasını değiştirmek üzere bir kullanıcı arabirimi oluşturmak için ChangePassword denetimini kullanın. PasswordRecovery denetimine benzer şekilde, ChangePassword denetimi iki görünümden oluşur: parolayı değiştirme ve başarı. Parolayı Değiştir görünümü kullanıcıdan eski ve yeni parolalarını ister. Doğru eski parolayı ve en küçük uzunluğu ve alfasayısal olmayan karakter gereksinimlerini karşılayan yeni bir parolayı sağlarken, ChangePassword denetimi kullanıcının parolasını güncelleştirir ve başarı görünümünü görüntüler.

> [!NOTE]
> ChangePassword denetimi, `MembershipUser` nesnenin [`ChangePassword` yöntemini](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)çağırarak kullanıcının parolasını değiştirir. ChangePassword yöntemi iki `string` giriş parametresini kabul eder- *oldPassword* ve *YeniParola*-, sağlanan *oldPassword* doğru olduğu varsayılarak Kullanıcı hesabını *YeniParola*ile güncelleştirir.

`ChangePassword.aspx` sayfasını açın ve sayfaya `ChangePwd`adlandırarak bir ChangePassword denetimi ekleyin. Bu noktada, Tasarım görünümü parolayı Değiştir görünümünü göstermelidir (bkz. Şekil 6). PasswordRecovery denetimiyle olduğu gibi, denetimin akıllı etiketi aracılığıyla görünümler arasında geçiş yapabilirsiniz. Ayrıca, bu görünümlerin görünümleri, assıralanan stil özellikleri aracılığıyla veya bir şablona dönüştürerek özelleştirilebilir.

[Sayfaya ChangePassword denetimi eklemek ![](recovering-and-changing-passwords-cs/_static/image17.png)](recovering-and-changing-passwords-cs/_static/image16.png)

**Şekil 6**: sayfaya ChangePassword denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](recovering-and-changing-passwords-cs/_static/image18.png))

ChangePassword denetimi şu anda oturum açmış olan kullanıcının parolasını *veya* başka bir belirtilen kullanıcının parolasını güncelleştirebilir. Şekil 6 ' da gösterildiği gibi, varsayılan parola değiştirme görünümü yalnızca üç metin kutusu denetimi oluşturur: biri eski parola için, diğeri ise yeni parola. Bu varsayılan arabirim, oturum açmış olan kullanıcının parolasını güncelleştirmek için kullanılır.

Başka bir kullanıcının parolasını güncelleştirmek üzere ChangePassword denetimini kullanmak için denetimin [`DisplayUserName` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx) true olarak ayarlayın. Bunun yapılması, sayfaya bir dördüncü TextBox ekler ve parolayı değiştirecek kullanıcının Kullanıcı adını sorar.

Oturumu açmış bir kullanıcının oturum açmak zorunda kalmadan parolasını değiştirmesine izin vermek istiyorsanız, `DisplayUserName` true olarak ayarlanması yararlı olur. Kişisel olarak, kullanıcının parolasını değiştirmesine izin vermeden önce oturum açmasını gerektiren bir sorun olmadığını düşündüm. Bu nedenle, `DisplayUserName` değerini false (varsayılan) olarak ayarlayın. Bununla birlikte, bu kararı verirken, anonim kullanıcıların bu sayfaya ulaşmasını sağladık. Anonim kullanıcıların `ChangePassword.aspx`ziyaret etmesini engellemek için sitenin URL yetkilendirme kurallarını güncelleştirin. URL yetkilendirme kuralı sözdiziminde belleğinizin yenilenmesi gerekiyorsa, <a id="_msoanchor_4"> </a> [*Kullanıcı tabanlı yetkilendirme*](../membership/user-based-authorization-cs.md) öğreticisine geri bakın.

> [!NOTE]
> `DisplayUserName` özelliği, yöneticilerin diğer kullanıcıların parolalarını değiştirmesine izin vermek için kullanışlı olabilir. Ancak, `DisplayUserName` true olarak ayarlandığında bile, doğru eski parolanın bilinmeli ve girilmesi gerekir. 3\. adımda yöneticilerin Kullanıcı parolalarını değiştirmesine izin verme teknikleri hakkında konuşacağız.

`ChangePassword.aspx` sayfasını bir tarayıcıda ziyaret edin ve parolanızı değiştirin. Üyelik yapılandırmasında belirtilen parola uzunluğu ve alfasayısal olmayan karakter gereksinimlerini karşılayamayan yeni bir parola girdiğinizde bir hata iletisi görüntülendiğini unutmayın (bkz. Şekil 7).

[Sayfaya ChangePassword denetimi eklemek ![](recovering-and-changing-passwords-cs/_static/image20.png)](recovering-and-changing-passwords-cs/_static/image19.png)

**Şekil 7**: sayfaya ChangePassword denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](recovering-and-changing-passwords-cs/_static/image21.png))

Doğru eski parolayı ve geçerli bir yeni parolayı girdikten sonra, oturum açan kullanıcının parolası değiştirilir ve başarı görünümü görüntülenir.

### <a name="sending-a-confirmation-email"></a>Onay e-postası gönderiliyor

Varsayılan olarak, ChangePassword denetimi, parolası az önce güncelleştirilmiş kullanıcıya bir e-posta iletisi göndermez. E-posta göndermek isterseniz, denetimin `MailDefinition` özelliğini yapılandırmanız yeterlidir. Kullanıcının yeni parolalarını içeren HTML biçimli bir e-posta gönderilmesini sağlamak için ChangePassword denetimini yapılandıralim.

`ChangePassword.htm`adlı `EmailTemplates` klasörde yeni bir dosya oluşturarak başlayın. Aşağıdaki biçimlendirmeyi ekleyin:

[!code-html[Main](recovering-and-changing-passwords-cs/samples/sample4.html)]

Sonra, ChangePassword denetiminin `MailDefinition` özelliğinin `BodyFileName`, `IsBodyHtml`ve `Subject` özelliklerini ~/EmailTemplates/ChangePassword.htm, true olarak ayarlayın ve parolanız sırasıyla!, değişmiştir.

Bu değişiklikleri yaptıktan sonra sayfayı yeniden ziyaret edin ve parolanızı tekrar değiştirin. Bu kez, ChangePassword denetimi kullanıcının dosyadaki e-posta adresine özelleştirilmiş, HTML biçimli bir e-posta gönderir (bkz. Şekil 8).

[e-posta Iletisi ![, kullanıcıya parolasının değiştiğini bildirir](recovering-and-changing-passwords-cs/_static/image23.png)](recovering-and-changing-passwords-cs/_static/image22.png)

**Şekil 8**: kullanıcıya parolasının değiştiğini bildiren bir e-posta iletisi ([tam boyutlu görüntüyü görüntülemek için tıklatın](recovering-and-changing-passwords-cs/_static/image24.png))

## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>3\. Adım: yöneticilerin kullanıcıların parolalarını değiştirmesine Izin verme

Kullanıcı hesaplarını destekleyen uygulamalarda ortak bir özellik, yönetici kullanıcının diğer kullanıcıların parolalarını değiştirme yeteneğidir. Bu işlevsellik, sistem kullanıcıların kendi parolalarını değiştirmesine olanak sağladığından, bazı durumlarda gereklidir. Böyle bir durumda, kullanıcının unutulan parolasını kurtarmaları için tek yol, yöneticinin yeni bir parola atamasını sağlar. Ancak, PasswordRecovery ve ChangePassword denetimleriyle birlikte, yönetici kullanıcıların bu kullanıcıların parolalarını değiştirmesini sağladıkça kullanıcıların parolalarını değiştirmemelerine gerek kalmaz.

Ancak istemciniz, yönetici kullanıcıların diğer kullanıcıların parolalarını değiştirebilmeleri insists ne olur? Ne yazık ki bu işlevselliği eklemek bir iş biraz olabilir. Bir kullanıcının parolasını değiştirmek için, hem eski hem de yeni parolanın `MembershipUser` nesnenin `ChangePassword` yöntemine sağlanması gerekir, ancak bir yöneticinin onu değiştirmek için kullanıcının parolasını bilmesi gerekmez.

Tek bir geçici çözüm, önce kullanıcının parolasını sıfırlamasıdır ve ardından aşağıdaki gibi kodu kullanarak yeni parolayla değiştirin:

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample5.aspx)]

Bu kod, parolasını yöneticinin değiştirmesini istediği Kullanıcı olan Kullanıcı *adı*hakkındaki bilgileri alarak başlar. Ardından `ResetPassword` yöntemi çağrılır, bu, kullanıcıya yeni ve rastgele bir parola atar. Rastgele oluşturulan bu parola, yöntemi tarafından döndürülür ve `resetPwd`değişkeninde depolanır. Artık kullanıcının parolasını öğrendiğimiz için `ChangePassword`çağrısıyla değiştirebiliriz.

Bu sorun, bu kodun yalnızca, üyelik sistemi yapılandırması `RequiresQuestionAndAnswer` false olarak ayarlandıysa geçerlidir. `RequiresQuestionAndAnswer` true ise, uygulamamızda olduğu gibi, `ResetPassword` yönteminin güvenlik yanıtını geçirilmesi gerekir, aksi takdirde bir özel durum oluşturur.

Üyelik çerçevesi bir güvenlik sorusu ve yanıtı gerektirecek şekilde yapılandırıldıysa ve istemciniz, yöneticilerin kullanıcıların parolalarını değiştirebilmesini insists, üç seçeneğiniz vardır:

- Ellerinizi uçak ortamında oluşturun ve istemciye bu işlemi yapamayan tek bir şey olduğunu söyleyin.
- `RequiresQuestionAndAnswer` false olarak ayarlayın. Bu, daha az güvenli bir uygulamayla sonuçlanır. Nefarli bir kullanıcının başka bir kullanıcının e-posta gelen kutusuna erişim kazandığını düşünün. Tehlikede olan Kullanıcı, öğle yemeği 'ne gitmek ve iş istasyonunu kilitleyememesi ya da e-postalarını ortak terminalden erişmemesi ve oturumu kapatma konusunda kalmadığı belki. Her iki durumda da, nefarli Kullanıcı `RecoverPassword.aspx` sayfasını ziyaret edebilir ve kullanıcının Kullanıcı adını girebilir. Daha sonra sistem, güvenlik yanıtını istemeden kurtarılan parolayı e-posta olarak gönder.
- Üyelik çerçevesi tarafından oluşturulan Özet katmanını atlayın ve SQL Server veritabanıyla doğrudan çalışın. Üyelik şeması, bir kullanıcının parolasını ayarlayan ve kendi görevini gerçekleştirmek için güvenlik yanıtı veya eski parola gerektirmeyen `aspnet_Membership_SetPassword` adlı saklı yordamı içerir.

Bu seçeneklerden hiçbiri özellikle çarpıcı değildir, ancak bir geliştiricinin ömrü bazen ne kadar zaman girer.

`Membership` ve `MembershipUser` sınıfları atlayan ve doğrudan `SecurityTutorials` veritabanına karşı çalışan bir kod yazarak, ileri ve üçüncü yaklaşımı uyguladım.

> [!NOTE]
> Doğrudan veritabanıyla çalışarak, üyelik çerçevesi tarafından sunulan kapsülleme, mil olur. Bu karar bize `SqlMembershipProvider`, kodumuzu daha az taşınabilir hale getirir. Ayrıca, üyelik şeması değişirse ASP.NET 'in gelecek sürümlerinde bu kod beklendiği gibi çalışmayabilir. Bu yaklaşım bir geçici çözümdür ve çoğu geçici çözüm gibi en iyi yöntemlere örnek değildir.

Kodun bazı etkileyici bitleri vardır ve oldukça uzun. Bu nedenle, bu öğreticiyi bir şekilde incelemek istemiyorum. Daha fazla bilgi edinmek istiyorsanız, Bu öğreticinin kodunu indirin ve `~/Administration/ManageUsers.aspx` sayfasını ziyaret edin. <a id="_msoanchor_5"> </a> [Önceki öğreticide](building-an-interface-to-select-one-user-account-from-many-cs.md)oluşturduğumuz Bu sayfa, her kullanıcıyı listeler. GridView 'u `UserInformation.aspx` sayfanın bir bağlantısını içerecek şekilde güncelleştirdim ve seçilen kullanıcının Kullanıcı adını QueryString aracılığıyla geçirdim. `UserInformation.aspx` sayfası, parolasını değiştirmek için seçilen kullanıcı ve metin kutuları hakkındaki bilgileri görüntüler (bkz. Şekil 9).

Yeni parolayı girdikten, ikinci metin kutusuna onayladıktan ve Kullanıcı Güncelleştir düğmesine tıkladıktan sonra Kullanıcı parolasını güncelleştiren bir geri gönderme ve `aspnet_Membership_SetPassword` saklı yordamı çağırılır. Bu işlevle ilgilenen okuyucuları koda daha tanıdık hale getirdim ve Kullanıcı parolasını değiştiren kullanıcıya bir e-posta göndermeye yönelik işlevselliği genişletmeyi deneyin.

[Yönetici ![kullanıcının parolasını değiştirebilir](recovering-and-changing-passwords-cs/_static/image26.png)](recovering-and-changing-passwords-cs/_static/image25.png)

**Şekil 9**: yönetici bir kullanıcının parolasını değiştirebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](recovering-and-changing-passwords-cs/_static/image27.png))

> [!NOTE]
> `UserInformation.aspx` sayfası şu anda yalnızca üyelik çerçevesi parolaları açık veya karma biçiminde depolayacak şekilde yapılandırıldıysa geçerlidir. Bu işlevi eklemek için davet edilseniz de, yeni parolayı şifrelemek için kod eksiktir. Gerekli kodu eklemek için önerdiğim Yöntem, .NET Framework içindeki yöntemlerin kaynak kodunu incelemek için [yansıtıcı](http://www.aisto.com/roeder/dotnet/) gibi bir dederleyicinin kullanılması. `SqlMembershipProvider` sınıfının `ChangePassword` metodunu inceleyerek başlayın. Bu, Parola karması oluşturmak için kodu yazmak üzere kullandığım tekniktir.

## <a name="summary"></a>Özet

ASP.NET kullanıcıların parolalarını yönetmesine yardımcı olmak için iki denetim sunar. PasswordRecovery denetimi, parolalarını unutanlar için yararlıdır. Üyelik çerçevesinin yapılandırmasına bağlı olarak, Kullanıcı var olan parolasını veya yeni, rastgele oluşturulmuş bir parolayı e-postayla alır. ChangePassword denetimi, kullanıcının parolasını güncelleştirmesine olanak sağlar.

Login ve CreateUserWizard denetimleri gibi, PasswordRecovery ve ChangePassword denetimleri, bir dizi bildirime dayalı biçimlendirme veya kod satırı yazmak zorunda kalmadan bir zengin Kullanıcı arabirimini işler. Varsayılan Kullanıcı arabirimi gereksinimlerinizi karşılamıyorsa, çeşitli stil özellikleri aracılığıyla özelleştirebilirsiniz. Alternatif olarak, denetimlerin arabirimleri daha da ayrıntılı bir ölçüde denetim için şablonlara dönüştürülebilir. Arka planda bu denetimlerin ardından, `MembershipUser` nesnenin `ResetPassword` ve `ChangePassword` yöntemlerini çağırarak üyelik API 'SI kullanılır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ChangePassword denetimi hızlı başlangıçlarını](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery denetimi hızlı başlangıçlarını](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [ASP.NET 'de e-posta gönderme](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` SSS](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, Michael Emmings ve suchi Banerjee ' i içerir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](building-an-interface-to-select-one-user-account-from-many-cs.md)
> [İleri](unlocking-and-approving-user-accounts-cs.md)
