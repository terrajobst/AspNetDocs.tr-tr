---
uid: web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
title: Kullanıcı hesaplarının kilidini açma ve onaylama (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, kullanıcıların kilitli ve onaylanmış durumları yönetmesi için yöneticilerin bir Web sayfası oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. Ayrıca yeni kullanıcıları nasıl onayladığımızda de görülecektir...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: 041854a5-ea8c-4de0-82f1-121ba6cb2893
msc.legacyurl: /web-forms/overview/older-versions-security/admin/unlocking-and-approving-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 4a7474676b8f502c583e226678de2b275e0ea3c7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590592"
---
# <a name="unlocking-and-approving-user-accounts-vb"></a>Kullanıcı Hesaplarının Kilidini Açma ve Kullanıcı Hesaplarını Onaylama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.14.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial14_UnlockAndApprove_vb.pdf)

> Bu öğreticide, kullanıcıların kilitli ve onaylanmış durumları yönetmesi için yöneticilerin bir Web sayfası oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. Ayrıca, yeni kullanıcıların e-posta adreslerini doğruladıktan sonra nasıl onaylanacağını da görüyoruz.

## <a name="introduction"></a>Giriş

Kullanıcı adı, parola ve e-posta ile birlikte her kullanıcı hesabının, kullanıcının sitede oturum açıp kullanamayacağını belirten iki durum alanı vardır: kilitli ve onaylanmış. Bir Kullanıcı belirli bir dakika içinde belirtilen sayıda geçersiz kimlik bilgileri sağladıklarında otomatik olarak kilitlenir (varsayılan ayarlar, 10 dakika içinde 5 geçersiz oturum açma denemesinden sonra bir kullanıcıyı kilitler). Onaylanan durum, yeni bir kullanıcının sitede oturum açabilbilmesi için bazı eylemler transpire gereken senaryolarda faydalıdır. Örneğin, bir kullanıcının oturum açabilmek için önce e-posta adreslerini doğrulaması veya yönetici tarafından onaylanması gerekebilir.

Kilitli veya onaylanmamış bir Kullanıcı oturum açamadığından, yalnızca bu durumların nasıl sıfırlandığını merak edebilir. ASP.NET, kullanıcıların kilitli ve onaylanmış durumlarını yönetmek için herhangi bir yerleşik işlevsellik veya Web denetimi içermez, çünkü bu kararların bir siteden siteye göre işlenmesi gerekir. Bazı siteler tüm yeni kullanıcı hesaplarını otomatik olarak onaylayabilir (varsayılan davranış). Diğer kullanıcılar, kaydolduklarında belirtilen e-posta adresine gönderilen bir bağlantıyı ziyaret edene kadar yönetici yeni hesapları onaylar veya kullanıcıları onaylamaz. Benzer şekilde, bazı siteler bir yönetici durumlarını sıfırlana kadar kullanıcıları kilitleyebilir, ancak diğer siteler, kullanıcının hesabının kilidini açmak için ziyaret edebilecekleri bir URL 'ye sahip kilitli kullanıcıya bir e-posta gönderir.

Bu öğreticide, kullanıcıların kilitli ve onaylanmış durumları yönetmesi için yöneticilerin bir Web sayfası oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. Ayrıca, yeni kullanıcıların e-posta adreslerini doğruladıktan sonra nasıl onaylanacağını da görüyoruz.

## <a name="step-1-managing-users-locked-out-and-approved-statuses"></a>Adım 1: kullanıcıların kilitli ve onaylanan durumlarını yönetme

<a id="Tutorial12"> </a> [*Birçok öğreticiden bir kullanıcı hesabı seçmek için arabirim oluşturma*](building-an-interface-to-select-one-user-account-from-many-vb.md) bölümünde, disk belleğine alınmış ve filtrelenmiş GridView 'da her bir kullanıcı hesabının listelendiğine ilişkin bir sayfa oluşturduk. Kılavuza her kullanıcının adı ve e-postası, onaylanmış ve kilitli durumları, şu anda çevrimiçi olup olmadıkları ve Kullanıcı hakkında herhangi bir yorum listelenir. Kullanıcıların onaylı ve kilitli durumlarını yönetmek için bu kılavuzu düzenlenebilir hale yapabiliriz. Kullanıcının onaylanan durumunu değiştirmek için, yönetici önce Kullanıcı hesabını bulup ilgili GridView satırını düzenleyerek, onaylanan onay kutusunu işaretleyerek veya denetlemesinin kaldırılması gerekir. Alternatif olarak, onaylanan ve kilitlenen durumları ayrı bir ASP.NET sayfası aracılığıyla yönetebiliriz.

Bu öğretici için iki ASP.NET sayfası kullanalım: `ManageUsers.aspx` ve `UserInformation.aspx`. Buradaki fikir, `ManageUsers.aspx` sistemdeki kullanıcı hesaplarını listelemesidir, `UserInformation.aspx` yöneticinin belirli bir kullanıcı için onaylanan ve kilitlenen durumları yönetmesine olanak sağlar. İlk iş sıramız, `ManageUsers.aspx` bir bağlantı sütunu olarak işleyen bir Hyperlinkalanı içerecek şekilde GridView 'u genişletmek. Her bağlantının `UserInformation.aspx?user=UserName`işaret etmek istiyoruz *. burada Kullanıcı adı,* düzenlenecek kullanıcının adıdır.

> [!NOTE]
> <a id="Tutorial13"> </a> [*Kurtarma ve değiştirme parolaları*](recovering-and-changing-passwords-vb.md) için kodu indirdiyseniz `ManageUsers.aspx` sayfasında zaten bir "Yönet" bağlantıları olduğunu fark etmiş olabilirsiniz ve `UserInformation.aspx` sayfası seçili kullanıcının parolasını değiştirmek için bir arabirim sağlar. Bu öğreticiyle ilişkili kodda bu işlevselliği çoğaltmamaya karar verdim çünkü üyelik API 'sini atlatıp ve doğrudan bir kullanıcının parolasını değiştirmek için SQL Server veritabanıyla birlikte çalışan. Bu öğretici `UserInformation.aspx` sayfasıyla sıfırdan başlar.

### <a name="adding-manage-links-to-theuseraccountsgridview"></a>`UserAccounts`GridView 'a "Manage" bağlantıları ekleniyor

`ManageUsers.aspx` sayfasını açın ve `UserAccounts` GridView 'a bir Hyperlinkalanı ekleyin. HyperLinkField 'ın `Text` özelliğini, sırasıyla `UserName` ve "UserInformation. aspx? User ={0}" gibi `DataNavigateUrlFields` ve `DataNavigateUrlFormatString` özelliklerini "Yönet" olarak ayarlayın. Bu ayarlar, tüm köprülerin "Yönet" metnini görüntülemesi için Hyperlinkalanını yapılandırır, ancak her bağlantı uygun *Kullanıcı adı* değerini QueryString öğesine geçirir.

GridView 'a HyperLinkField eklendikten sonra, `ManageUsers.aspx` sayfasını bir tarayıcıdan görüntülemek için bir dakikanızı ayırın. Şekil 1 ' de gösterildiği gibi, her GridView satırı artık bir "Yönet" bağlantısı içerir. `UserInformation.aspx?user=Bruce`için "Yönet" bağlantısı, "Yönet" bağlantısının `UserInformation.aspx?user=Dave`ve işaret noktaları için "yönetme" bağlantısı.

[Hyperlinkalanı ![ekler](unlocking-and-approving-user-accounts-vb/_static/image2.png)](unlocking-and-approving-user-accounts-vb/_static/image1.png)

**Şekil 1**: Hyperlinkalanı her kullanıcı hesabı için bir "Yönet" bağlantısı ekler ([tam boyutlu görüntüyü görüntülemek için tıklayın](unlocking-and-approving-user-accounts-vb/_static/image3.png))

`UserInformation.aspx` sayfası için Kullanıcı arabirimi ve kodu bir süre içinde oluşturacağız, ancak ilk olarak bir kullanıcının kilitli ve onaylanmış durumlarını nasıl değiştirelim hakkında konuşacağız. [`MembershipUser` sınıfı](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx) ve [`IsApproved` özelliklere](https://msdn.microsoft.com/library/system.web.security.membershipuser.isapproved.aspx)sahiptir. `IsLockedOut` özelliği salt okunurdur. Bir kullanıcıyı programlı bir şekilde kilitlemeye yönelik bir mekanizma yoktur; bir kullanıcının kilidini açmak için `MembershipUser` sınıfının [`UnlockUser` metodunu](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx)kullanın. `IsApproved` özelliği okunabilir ve yazılabilir. Bu özellikte yapılan değişiklikleri kaydetmek için, değiştirilen `MembershipUser` nesnesini geçirerek `Membership` sınıfın [`UpdateUser` yöntemini](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)çağırmanız gerekir.

`IsApproved` özelliği okunabilir ve yazılabilir olduğundan, bir CheckBox denetimi büyük olasılıkla bu özelliği yapılandırmak için en iyi kullanıcı arabirimi öğesidir. Ancak, bir yönetici bir kullanıcıyı kilitleyemediği için `IsLockedOut` özelliği için bir onay kutusu çalışmaz, yalnızca bir kullanıcının kilidini açabilir. `IsLockedOut` özelliği için uygun bir kullanıcı arabirimi, tıklandığı sırada Kullanıcı hesabının kilidini açarken kullanılan bir düğmedir. Bu düğme yalnızca Kullanıcı kilitli olduğunda etkinleştirilmelidir.

### <a name="creating-theuserinformationaspxpage"></a>`UserInformation.aspx`sayfasını oluşturma

Artık Kullanıcı arabirimini `UserInformation.aspx`uygulamaya hazırlıyoruz. Bu sayfayı açın ve aşağıdaki Web denetimlerini ekleyin:

- Tıklandığında, yönetici `ManageUsers.aspx` sayfasına döndüren köprü denetimi.
- Seçilen kullanıcının adını görüntülemek için bir etiket Web denetimi. Bu etiketin `ID` `UserNameLabel` olarak ayarlayın ve Text özelliğini temizleyin.
- `IsApproved`adlı bir CheckBox denetimi. `AutoPostBack` özelliğini `True`olarak ayarlayın.
- Kullanıcının son kilitli tarihini görüntülemek için bir etiket denetimi. Bu etiketin adını `LastLockedOutDateLabel` ve `Text` özelliğini temizleyin.
- Kullanıcının kilidini açmak için bir düğme. Bu düğmeyi `UnlockUserButton` adlandırın ve `Text` özelliğini "Kullanıcı kilidini aç" olarak ayarlayın.
- "Kullanıcının onaylanan durumu güncelleştirildi" gibi durum iletilerini görüntülemek için bir etiket denetimi. Bu denetimi `StatusMessage`adlandırın, `Text` özelliğini temizleyin ve `CssClass` özelliğini `Important`olarak ayarlayın. (`Important` CSS sınıfı `Styles.css` stil sayfası dosyasında tanımlanır; ilgili metni büyük ve kırmızı bir yazı tipinde görüntüler.)

Bu denetimler eklendikten sonra, Visual Studio 'daki Tasarım görünümü Şekil 2 ' de ekran görüntüsüne benzer görünmelidir.

[UserInformation. aspx için Kullanıcı arabirimi oluşturma ![](unlocking-and-approving-user-accounts-vb/_static/image5.png)](unlocking-and-approving-user-accounts-vb/_static/image4.png)

**Şekil 2**: `UserInformation.aspx` Için Kullanıcı arabirimi oluşturma ([tam boyutlu görüntüyü görüntülemek için tıklayın](unlocking-and-approving-user-accounts-vb/_static/image6.png))

Kullanıcı arabirimi tamamlanmalı bir sonraki göreviniz, seçili kullanıcının bilgilerine göre `IsApproved` onay kutusunu ve diğer denetimleri ayarlamanıza olanak sağlar. Sayfanın `Load` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample1.vb)]

Yukarıdaki kod, sonraki geri gönderimin değil, sayfanın ilk ziyaretinin olduğundan emin olarak başlar. Daha sonra, `user` QueryString alanından geçirilen kullanıcı adını okur ve `Membership.GetUser(username)` yöntemi aracılığıyla bu kullanıcı hesabı hakkındaki bilgileri alır. QueryString aracılığıyla hiçbir Kullanıcı adı sağlanmadığında veya belirtilen kullanıcı bulunamazsa, yönetici `ManageUsers.aspx` sayfasına geri gönderilir.

`MembershipUser` nesnenin `UserName` değeri `UserNameLabel` görüntülenir ve `IsApproved` onay kutusu `IsApproved` özellik değerine göre denetlenir.

`MembershipUser` nesnesinin [`LastLockoutDate` özelliği](https://msdn.microsoft.com/library/system.web.security.membershipuser.lastlockoutdate.aspx) , kullanıcının en son ne zaman kilitlendiğini gösteren bir `DateTime` değeri döndürür. Kullanıcı hiçbir daha kilitlenmediyse, döndürülen değer üyelik sağlayıcısına bağlıdır. Yeni bir hesap oluşturulduğunda `SqlMembershipProvider`, `aspnet_Membership` tablosunun `LastLockoutDate` alanını `1754-01-01 12:00:00 AM`olarak ayarlar. Yukarıdaki kod, `LastLockoutDate` özelliği 2000 tarihinden önce oluşursa `LastLockoutDateLabel` boş bir dize görüntüler. Aksi takdirde, `LastLockoutDate` özelliğinin tarih kısmı etikette görüntülenir. `UnlockUserButton``Enabled` özelliği kullanıcının kilitli durumuna ayarlanır, yani bu düğme yalnızca Kullanıcı kilitlenmişse etkinleştirilecek.

`UserInformation.aspx` sayfasını bir tarayıcı ile test etmek için bir dakikanızı ayırın. Elbette `ManageUsers.aspx` başlayıp yönetilecek bir kullanıcı hesabı seçmeniz gerekir. `UserInformation.aspx`adresinden sonra, `IsApproved` onay kutusunun yalnızca Kullanıcı onaylanırsa denetlendiğini unutmayın. Kullanıcı kilitliyse, son kilitleme tarihi görüntülenir. Kullanıcı kilidini aç düğmesi yalnızca Kullanıcı kilitli ise etkindir. `IsApproved` onay kutusunun işaretlenmesi veya kaldırılması veya Kullanıcı kilidini aç düğmesinin tıklatılması geri göndermeye neden olur, ancak henüz bu olaylar için olay işleyicileri oluşturduğumuz için Kullanıcı hesabında hiçbir değişiklik yapılmaz.

Visual Studio 'ya dönün ve `IsApproved` CheckBox 'ın `CheckedChanged` olayı ve `UnlockUser` düğmenin `Click` olayı için olay işleyicileri oluşturun. `CheckedChanged` olay işleyicisinde, kullanıcının `IsApproved` özelliğini onay kutusunun `Checked` özelliğine ayarlayın ve sonra değişiklikleri `Membership.UpdateUser`çağrısı aracılığıyla kaydedin. `Click` olay işleyicisinde, `MembershipUser` nesnesinin `UnlockUser` yöntemini çağırmanız yeterlidir. Her iki olay işleyicilerinde de `StatusMessage` etiketinde uygun bir ileti görüntüleyin.

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample2.vb)]

### <a name="testing-theuserinformationaspxpage"></a>`UserInformation.aspx`sayfasını test etme

Bu olay işleyicileri yerinde, sayfayı yeniden ziyaret edin ve kullanıcıyı onaylanmamış yapın. Şekil 3 ' te gösterildiği gibi, sayfada kullanıcının `IsApproved` özelliğinin başarıyla değiştirildiğini belirten kısa bir ileti görmeniz gerekir.

[Chris ![onaylanmamış](unlocking-and-approving-user-accounts-vb/_static/image8.png)](unlocking-and-approving-user-accounts-vb/_static/image7.png)

**Şekil 3**: Chris onaylanmamış ([tam boyutlu görüntüyü görüntülemek için tıklayın](unlocking-and-approving-user-accounts-vb/_static/image9.png))

Sonra, oturumu kapatın ve hesabı yalnızca onaylanmamış Kullanıcı olarak oturum açmayı deneyin. Kullanıcı onaylanmadığı için oturum açamazlar. Varsayılan olarak, Kullanıcı oturum açlamazsa, nedeni ne olursa olsun, oturum açma denetimi aynı iletiyi görüntüler. <a id="Tutorial6"> </a>Ancak [*Kullanıcı kimlik bilgilerini üyelik kullanıcı deposu öğreticisine karşı doğrulayarak*](../membership/validating-user-credentials-against-the-membership-user-store-vb.md) , daha uygun bir ileti göstermek için oturum açma denetimini geliştirmeye baktık. Şekil 4 ' te gösterildiği gibi kemal, hesabı henüz onaylanmadığı için oturum açamadığı belirten bir ileti gösterilir.

[Hesabı onaylanmamış olduğundan ![Chris oturum açılamıyor](unlocking-and-approving-user-accounts-vb/_static/image11.png)](unlocking-and-approving-user-accounts-vb/_static/image10.png)

**Şekil 4**: hesap onaylanmamış olduğu Için Chris oturum açılamıyor ([tam boyutlu görüntüyü görüntülemek için tıklayın](unlocking-and-approving-user-accounts-vb/_static/image12.png))

Kilitli işlevselliği test etmek için, onaylanan bir kullanıcı olarak oturum açmayı deneyin, ancak yanlış bir parola kullanın. Bu işlemi, Kullanıcı hesabı kilitlenene kadar gereken sayıda tekrarlayın. Bir kilitli hesaptan oturum açmaya çalıştığınızda, oturum açma denetimi de özel bir ileti gösterecek şekilde güncelleştirildi. Oturum açma sayfasında şu iletiyi görmeye başladıktan sonra bir hesabın kilitli olduğunu bilirsiniz: "hesabınız çok fazla sayıda geçersiz oturum açma girişimi nedeniyle kilitlendi. Hesabınızın kilidi açık olması için lütfen yöneticiye başvurun. "

`ManageUsers.aspx` sayfasına dönün ve kilitli kullanıcının Yönet bağlantısına tıklayın. Şekil 5 ' te gösterildiği gibi, Kullanıcı kilidini aç düğmesinin etkinleştirilmesi `LastLockedOutDateLabel` bir değer görmeniz gerekir. Kullanıcı hesabının kilidini açmak için Kullanıcı kilidini aç düğmesine tıklayın. Kullanıcının kilidini açtıktan sonra yeniden oturum açabilirler.

[![Davve sistemden kilitlenmiş](unlocking-and-approving-user-accounts-vb/_static/image14.png)](unlocking-and-approving-user-accounts-vb/_static/image13.png)

**Şekil 5**: anve sistemden kilitlenmiş ([tam boyutlu görüntüyü görüntülemek için tıklayın](unlocking-and-approving-user-accounts-vb/_static/image15.png))

## <a name="step-2-specifying-new-users-approved-status"></a>2\. Adım: yeni kullanıcıların onaylanan durumunu belirtme

Onaylanan durum, yeni bir Kullanıcı oturum açıp sitenin kullanıcıya özgü özelliklerine erişebilmesinden önce bazı eylemin gerçekleştirilmesini istediğiniz senaryolarda yararlıdır. Örneğin, oturum açma ve kaydolma sayfaları dışındaki tüm sayfaların yalnızca kimliği doğrulanmış kullanıcılara erişilebilen özel bir Web sitesi çalıştırıyor olabilirsiniz. Ancak bir yabancıya Web sitenize ulaşırsa ne olur, kaydolma sayfasını bulur ve bir hesap oluşturur mi? Bunun oluşmasını engellemek için kaydolma sayfasını bir `Administration` klasöre taşıyabilir ve bir yöneticinin her hesabı el ile oluşturmasını isteyebilirsiniz. Alternatif olarak, bir yöneticinin kullanıcı hesabını onaylaana kadar site erişimini yasaklayabilmeniz için bir kişiye izin verebilirsiniz.

Varsayılan olarak, CreateUserWizard denetimi yeni hesapları onaylar. Bu davranışı denetimin [`DisableCreatedUser` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx)kullanarak yapılandırabilirsiniz. Yeni Kullanıcı hesaplarını onaylamamak için bu özelliği `True` olarak ayarlayın.

> [!NOTE]
> Varsayılan olarak, CreateUserWizard denetimi yeni kullanıcı hesabında otomatik olarak oturum açar. Bu davranış, denetimin [`LoginCreatedUser` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx)tarafından belirlenir. Onaylanmamış kullanıcılar sitede oturum açamadığından `DisableCreatedUser` `True` Yeni Kullanıcı hesabı, `LoginCreatedUser` özelliğinin değerinden bağımsız olarak sitede oturum açmamış olur.

`Membership.CreateUser` yöntemi aracılığıyla program aracılığıyla yeni kullanıcı hesapları oluşturuyorsanız, onaylanmamış bir kullanıcı hesabı oluşturmak için yeni kullanıcının `IsApproved` özellik değerini bir giriş parametresi olarak kabul eden aşırı yüklemelerden birini kullanın.

## <a name="step-3-approving-users-by-verifying-their-email-address"></a>3\. Adım: e-posta adreslerini doğrulayarak kullanıcıları onaylama

Kullanıcı hesaplarını destekleyen birçok Web sitesi, kayıt sırasında sağlandıkları e-posta adresini doğrulayarak yeni kullanıcıları onaylamaz. Bu doğrulama işlemi genellikle benzersiz, doğrulanmış bir e-posta adresi gerektirdiğinden ve kaydolma işlemine ek bir adım eklediğinden, botlar, posta gönderenler ve diğer nEk-Do-It-to-a 'lar için kullanılır. Bu modelde, yeni bir Kullanıcı kaydolduğunda doğrulama sayfasına bağlantı içeren bir e-posta iletisi gönderilir. Kullanıcının e-postayı aldığını kanıtlamış olduğunu ve bu nedenle, girilen e-posta adresinin geçerli olduğunu kanıtlamış olan bağlantıyı ziyaret edin. Doğrulama sayfası, kullanıcının onaylanmasından sorumludur. Bu, otomatik olarak gerçekleşebilir, bu sayede bu sayfaya ulaşan tüm kullanıcıları veya yalnızca Kullanıcı [CAPTCHA](http://en.wikipedia.org/wiki/Captcha)gibi bazı ek bilgiler sağlar.

Bu iş akışına uyum sağlamak için, ilk olarak yeni kullanıcıların onaylanmamış olması için hesap oluşturma sayfasını güncelleştirmemiz gerekir. `Membership` klasöründeki `EnhancedCreateUserWizard.aspx` sayfasını açın ve CreateUserWizard denetiminin `DisableCreatedUser` özelliğini `True`olarak ayarlayın.

Daha sonra, CreateUserWizard denetimini, yeni kullanıcıya hesaplarının nasıl doğrulancağına ilişkin yönergeler içeren bir e-posta gönderecek şekilde yapılandırmamız gerekir. Özellikle, bir e-postaya `Verification.aspx` sayfasına (henüz oluşturduğumuz) bir bağlantı ekleyecek ve yeni kullanıcının `UserId` QueryString aracılığıyla geçireceğiz. `Verification.aspx` sayfası belirtilen kullanıcıyı arar ve onaylanmış olarak işaretler.

### <a name="sending-a-verification-email-to-new-users"></a>Yeni kullanıcılara bir doğrulama e-postası gönderme

CreateUserWizard denetiminden bir e-posta göndermek için `MailDefinition` özelliğini uygun şekilde yapılandırın. <a id="Tutorial13"> </a> [Önceki öğreticide](recovering-and-changing-passwords-vb.md)anlatıldığı gibi, ChangePassword ve PasswordRecovery denetimleri, CreateUserWizard denetimi ile aynı şekilde çalışacak [`MailDefinition` bir özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) içerir.

> [!NOTE]
> `MailDefinition` özelliğini kullanmak için `Web.config`e-posta teslim seçeneklerini belirtmeniz gerekir. Daha fazla bilgi için ASP.NET adresine [e-posta gönderme](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)bölümüne bakın.

`EmailTemplates` klasöründe `CreateUserWizard.txt` adlı yeni bir e-posta şablonu oluşturarak başlayın. Şablon için aşağıdaki metni kullanın:

[!code-aspx[Main](unlocking-and-approving-user-accounts-vb/samples/sample3.aspx)]

`MailDefinition``BodyFileName` özelliğini "~/EmailTemplates/CreateUserWizard.txt" olarak ayarlayın ve `Subject` özelliği "Web siteme hoş geldiniz!" olarak ayarlanır! Lütfen hesabınızı etkinleştirin. "

`CreateUserWizard.txt` e-posta şablonunun bir `<%VerificationUrl%>` yer tutucusu içerdiğine unutmayın. `Verification.aspx` sayfanın URL 'SI yerleştirilir. CreateUserWizard, `<%UserName%>` ve `<%Password%>` yer tutucuları otomatik olarak yeni hesabın Kullanıcı adı ve parolasıyla değiştirir, ancak yerleşik `<%VerificationUrl%>` yer tutucusu yoktur. Uygun doğrulama URL 'siyle el ile değiştirmeniz gerekir.

Bunu gerçekleştirmek için, CreateUserWizard 'in [`SendingMail` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.sendingmail.aspx) için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample4.vb)]

`SendingMail` olay `CreatedUser` olayından sonra ateşlenir, yani Yukarıdaki olay işleyicisi Yeni Kullanıcı hesabını yürüten zamana göre daha önce oluşturulmuştur. Yeni kullanıcının `UserId` değerine, CreateUserWizard denetimine girilen `UserName` geçirerek `Membership.GetUser` yöntemini çağırarak erişebiliriz. Ardından, doğrulama URL 'SI oluşturulur. Deyimin `Request.Url.GetLeftPart(UriPartial.Authority)`, URL 'nin `http://yourserver.com` kısmını döndürür; `Request.ApplicationPath`, uygulamanın kökü olan yolu döndürür. Doğrulama URL 'SI daha sonra `Verification.aspx?ID=userId`olarak tanımlanır. Bu iki dize daha sonra tüm URL 'YI oluşturacak şekilde birleştirilir. Son olarak, e-posta iletisi gövdesi (`e.Message.Body`) tam URL ile değiştirilmiş tüm `<%VerificationUrl%>` örnekleri içerir.

Net etkisi, yeni kullanıcıların onaylanmamış olduğu anlamına gelir ve bu da sitede oturum açabilirler. Ayrıca, doğrulama URL 'sine bağlantı içeren bir e-posta otomatik olarak gönderilir (bkz. Şekil 6).

[Yeni Kullanıcı ![doğrulama URL 'sine bir bağlantı içeren bir e-posta alır](unlocking-and-approving-user-accounts-vb/_static/image17.png)](unlocking-and-approving-user-accounts-vb/_static/image16.png)

**Şekil 6**: Yeni Kullanıcı doğrulama URL 'Sine bir bağlantı Içeren bir e-posta alır ([tam boyutlu görüntüyü görüntülemek için tıklatın](unlocking-and-approving-user-accounts-vb/_static/image18.png))

> [!NOTE]
> CreateUserWizard denetiminin varsayılan CreateUserWizard adımı, kullanıcının hesabının oluşturulduğunu bildiren bir ileti görüntüler ve devam et düğmesini görüntüler. Bunu tıkladığınızda, Kullanıcı denetimin `ContinueDestinationPageUrl` özelliği tarafından belirtilen URL 'ye götürür. `EnhancedCreateUserWizard.aspx` içindeki CreateUserWizard `~/Membership/AdditionalUserInfo.aspx`yeni kullanıcıları gönderecek şekilde yapılandırılmıştır. Bu, kullanıcıya memleketiniz, giriş sayfası URL 'SI ve imza için istemde bulunur. Bu bilgiler yalnızca oturum açmış kullanıcılar tarafından eklenebildiğinden, kullanıcıları sitenin giriş sayfasına geri göndermek için bu özelliği güncellemek mantıklı olur (`~/Default.aspx`). Üstelik, kullanıcıya bir doğrulama e-postası gönderildiğini bildirmek ve bu e-postadaki yönergeleri izlediklerinde hesabı etkinleştirilmemesi için `EnhancedCreateUserWizard.aspx` sayfası veya CreateUserWizard adımının artırılması gerekir. Bu değişiklikleri okuyucu için bir alıştırma olarak bırakıyorum.

### <a name="creating-the-verification-page"></a>Doğrulama sayfası oluşturma

Son göreviniz `Verification.aspx` sayfasını oluşturmaktır. Bu sayfayı `Site.master` ana sayfayla ilişkilendirerek kök klasöre ekleyin. Siteye eklenen önceki içerik sayfalarının çoğunu yaptığımız gibi, içerik sayfasında ana sayfanın varsayılan içeriğini kullanması için `LoginContent` ContentPlaceHolder öğesine başvuran Içerik denetimini kaldırın.

`Verification.aspx` sayfasına bir etiket Web denetimi ekleyin, `ID` `StatusMessage` olarak ayarlayın ve Text özelliğini temizleyin. Sonra, `Page_Load` olay işleyicisini oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](unlocking-and-approving-user-accounts-vb/samples/sample5.vb)]

Yukarıdaki kodun toplu değeri, QueryString aracılığıyla sağlanan kullanıcı kimliğini doğrular, geçerli bir `Guid` değeri olduğunu ve var olan bir kullanıcı hesabına başvurmadığını doğrular. Bu denetimlerin hepsi başarılı olursa Kullanıcı hesabı onaylanır; Aksi takdirde, uygun bir durum iletisi görüntülenir.

Şekil 7 ' de bir tarayıcı aracılığıyla ziyaret edildiğinde `Verification.aspx` sayfası gösterilmektedir.

[![yeni kullanıcının hesabı artık onaylandı](unlocking-and-approving-user-accounts-vb/_static/image20.png)](unlocking-and-approving-user-accounts-vb/_static/image19.png)

**Şekil 7**: Yeni Kullanıcı hesabı artık onaylanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](unlocking-and-approving-user-accounts-vb/_static/image21.png))

## <a name="summary"></a>Özet

Tüm üyelik kullanıcı hesaplarının, kullanıcının sitede oturum açıp kullanamayacağını tespit eden iki durumu vardır: `IsLockedOut` ve `IsApproved`. Bu özelliklerin her ikisi de kullanıcının oturum açması için `True` olmalıdır.

Kullanıcının kilitli olma durumu, bir bilgisayar korsanının deneme yanılma yöntemleriyle bir siteye bölünmesi olasılığını azaltmak için bir güvenlik önlemi olarak kullanılır. Özellikle, belirli bir zaman penceresi içinde belirli sayıda geçersiz oturum açma denemesi varsa, Kullanıcı kilitlenir. Bu sınırlar `Web.config`üyelik sağlayıcısı ayarları aracılığıyla yapılandırılabilir.

Onaylanan durum genellikle yeni kullanıcıların oturum açmasını önlemek için bazı eylemler transpired sahip olana kadar bir yol olarak kullanılır. Site, yeni hesapların ilk olarak yönetici tarafından onaylanmasını veya 3. adımda, e-posta adreslerini doğrulayarak gördüğünüz için gereklidir.

Programlamanın kutlu olsun!

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Öncekini](recovering-and-changing-passwords-vb.md)
