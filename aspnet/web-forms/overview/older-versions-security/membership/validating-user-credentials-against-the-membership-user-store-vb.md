---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
title: Kullanıcı kimlik bilgilerini üyelik kullanıcı deposunda doğrulama (VB) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, Kullanıcı kimlik bilgilerinin hem programlı hem de oturum açma denetimi kullanılarak üyelik kullanıcı deposunda nasıl doğrulanacağı anlatılmaktadır...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 17772912-b47b-4557-9ce9-80f22df642f7
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
msc.type: authoredcontent
ms.openlocfilehash: 37574e4cdc86f518d01d12da58cc2862bc77d463
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78527932"
---
# <a name="validating-user-credentials-against-the-membership-user-store-vb"></a>Üyelik Kullanıcı Deposu ile Karşılaştırarak Kullanıcı Kimlik Bilgilerini Doğrulama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_VB.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_vb.pdf)

> Bu öğreticide, Kullanıcı kimlik bilgilerinin hem programlı hem de oturum açma denetimi kullanılarak üyelik kullanıcı deposunda nasıl doğrulanacağı anlatılmaktadır. Ayrıca, oturum açma denetiminin görünümünü ve davranışını özelleştirmeye de bakacağız.

## <a name="introduction"></a>Giriş

<a id="Tutorial05"> </a> [Önceki öğreticide](creating-user-accounts-vb.md) , üyelik çerçevesinde yeni bir kullanıcı hesabı oluşturmayı inceledik. İlk olarak, `Membership` sınıfın `CreateUser` yöntemi aracılığıyla Kullanıcı hesaplarını oluşturmaya ve ardından CreateUserWizard Web denetimi kullanılarak incelenmiştik. Ancak, oturum açma sayfası şu anda belirtilen kimlik bilgilerini sabit kodlanmış Kullanıcı adı ve parola çiftleri listesine göre doğrular. Oturum açma sayfasının mantığını, üyelik çerçevesinin Kullanıcı deposunda kimlik bilgilerini doğrulayacak şekilde güncelleştirmemiz gerekiyor.

Kullanıcı hesapları oluşturma konusunda çok benzer şekilde, kimlik bilgileri programlı bir şekilde veya bildirimli olarak doğrulanabilir. Üyelik API 'SI, kullanıcının kimlik bilgilerini Kullanıcı deposuna göre doğrulamaya yönelik bir yöntem içerir. Ve ASP.NET, oturum açma Web denetimiyle birlikte gönderilir. Bu, Kullanıcı arabirimini Kullanıcı arabirimi, Kullanıcı adı ve parola için metin kutularına ve oturum açmak için bir düğmeye sahiptir.

Bu öğreticide, Kullanıcı kimlik bilgilerinin hem programlı hem de oturum açma denetimi kullanılarak üyelik kullanıcı deposunda nasıl doğrulanacağı anlatılmaktadır. Ayrıca, oturum açma denetiminin görünümünü ve davranışını özelleştirmeye de bakacağız. Haydi başlayın!

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>1\. Adım: üyelik kullanıcı deposunda kimlik bilgilerini doğrulama

Form kimlik doğrulaması kullanan Web siteleri için, bir Kullanıcı oturum açma sayfasını ziyaret ederek ve kimlik bilgilerini girerek Web sitesinde oturum açar. Bu kimlik bilgileri daha sonra kullanıcı deposu ile karşılaştırılır. Bunlar geçerliyse, kullanıcıya ziyaretçinin kimliğini ve gerçekliğini gösteren bir güvenlik belirteci olan bir form kimlik doğrulama bileti verilir.

Bir kullanıcıyı üyelik çerçevesine karşı doğrulamak için `Membership` sınıfının [`ValidateUser` metodunu](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)kullanın. `ValidateUser` yöntemi iki giriş parametresi alır-`username` ve `password` ve kimlik bilgilerinin geçerli olup olmadığını gösteren bir Boole değeri döndürür. Önceki öğreticide incelenen `CreateUser` yöntemi gibi `ValidateUser` yöntemi, yapılandırılan üyelik sağlayıcısına gerçek doğrulamayı devreder.

`SqlMembershipProvider`, belirtilen kullanıcının parolasını `aspnet_Membership_GetPasswordWithFormat` saklı yordamı aracılığıyla alarak sağlanan kimlik bilgilerini doğrular. `SqlMembershipProvider`, kullanıcıların parolalarını üç biçimden birini kullanarak depoladığını hatırlayın: şifresiz, şifrelenmiş veya karma hale getirilmiş. `aspnet_Membership_GetPasswordWithFormat` saklı yordam, parolayı ham biçiminde döndürür. Şifrelenmiş veya karma parolalar için `SqlMembershipProvider`, `ValidateUser` yöntemine geçirilen `password` değerini eşdeğer şifreli veya karma durumuna dönüştürür ve sonra onu veritabanından döndürülmüş şekilde karşılaştırır. Veritabanında depolanan parola, Kullanıcı tarafından girilen biçimli parolayla eşleşiyorsa, kimlik bilgileri geçerlidir.

İzin verilen kimlik bilgilerini üyelik çerçevesi kullanıcı deposunda doğrulamak için oturum açma sayfamızı (~/`Login.aspx`) güncelleştirelim. Bu oturum açma sayfasını <a id="Tutorial02"> </a> [*form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-vb.md) bölümünde, Kullanıcı adı ve parola, beni anımsa onay kutusu ve oturum açma düğmesi için iki metin kutusuna sahip bir arabirim oluşturma (bkz. Şekil 1). Kod, girilen kimlik bilgilerini sabit kodlanmış Kullanıcı adı ve parola çiftleri (Scott/Password, Jisun/Password ve Sam/Password) listesiyle karşılaştırarak doğrular. <a id="Tutorial03"> </a> [*Forms kimlik doğrulaması yapılandırması ve gelişmiş konular*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) öğreticisinde, form kimlik doğrulama biletinin `UserData` özelliğindeki ek bilgileri depolamak için oturum açma sayfasının kodunu güncelleştirdik.

[![oturum açma sayfasının arabirimi Iki metin kutuları, bir CheckBoxList ve bir düğme Içerir](validating-user-credentials-against-the-membership-user-store-vb/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image1.png)

**Şekil 1**: oturum açma sayfasının arabirimi Iki metin kutuları, bir CheckBoxList ve bir düğme içerir ([tam boyutlu görüntüyü görüntülemek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image3.png))

Oturum açma sayfasının Kullanıcı arabirimi değişmeden kalabilir, ancak oturum açma düğmesinin `Click` olay işleyicisini, kullanıcıyı üyelik çerçevesi kullanıcı deposunda karşı doğrulayan kodla değiştirmemiz gerekiyor. Olay işleyicisini kodun aşağıdaki gibi görünmesi için güncelleştirin:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample1.vb)]

Bu kod daha basit bir işlemdir. `Membership.ValidateUser` yöntemini çağırarak, sağlanan Kullanıcı adı ve parolayı geçirerek başladık. Bu yöntem true değerini döndürürse, Kullanıcı `FormsAuthentication` sınıfının RedirectFromLoginPage yöntemi aracılığıyla sitede oturum açmış olur. ( <a id="Tutorial02"> </a> [*Form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-vb.md) konusunda anlatıldığı gibi `FormsAuthentication.RedirectFromLoginPage`, Forms kimlik doğrulama bileti oluşturur ve kullanıcıyı uygun sayfaya yönlendirir.) Kimlik bilgileri geçersiz ise, kullanıcıya Kullanıcı adının veya parolasının yanlış olduğunu bildiren `InvalidCredentialsMessage` etiketi görüntülenir.

İşte bu kadar kolay!

Oturum açma sayfasının beklendiği gibi çalışıp çalışmadığını sınamak için, önceki öğreticide oluşturduğunuz kullanıcı hesaplarından biriyle oturum açmayı deneyin. Ya da henüz bir hesap oluşturmadıysanız `~/Membership/CreatingUserAccounts.aspx` sayfasından bir tane oluşturun.

> [!NOTE]
> Kullanıcı kimlik bilgilerini girdiğinde ve oturum açma sayfası formunu gönderdiğinde, parola da dahil olmak üzere kimlik bilgileri Internet üzerinden *düz metin*olarak iletilir. Bu, tüm korsanlarının ağ trafiğinin Kullanıcı adını ve parolayı göremeyeceğini gösterir. Bunu engellemek için [Güvenli Yuva katmanları (SSL)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)kullanarak ağ trafiğini şifrelemek gereklidir. Bu, kimlik bilgilerinin (Ayrıca tüm sayfanın HTML işaretlemesi) Web sunucusu tarafından alınana kadar tarayıcıdan ayrıldıklarından emin olur.

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>Üyelik çerçevesi geçersiz oturum açma girişimlerini nasıl Işler?

Bir ziyaretçi oturum açma sayfasına ulaştığında ve kimlik bilgilerini gönderdiğinde, tarayıcıları oturum açma sayfasına bir HTTP isteği oluşturur. Kimlik bilgileri geçerliyse, HTTP yanıtı bir tanımlama bilgisinde kimlik doğrulama biletini içerir. Bu nedenle, sitenize kesintiye uğramaya çalışan bir korsan, oturum açma sayfasına geçerli bir Kullanıcı adı ve parola tahminiyle, her zaman çalışan bir program oluşturabilir. Parola tahmini doğruysa, oturum açma sayfası, kimlik doğrulama anahtarı tanımlama bilgisini döndürür. bu noktada, programın geçerli bir Kullanıcı adı/parola çiftinin üzerinde olduğunu bildiğinde haberdar olur. Bu tür bir program, deneme yanılma aracılığıyla bir kullanıcının parolasıyla, özellikle de parolanın zayıfına göre anlaşılabilir.

Bu tür deneme yanılma saldırılarını engellemek için, belirli bir süre içinde belirli sayıda başarısız oturum açma girişimi varsa üyelik çerçevesi bir kullanıcıyı kilitler. Tam parametreler aşağıdaki iki üyelik sağlayıcısı yapılandırma ayarları aracılığıyla yapılandırılabilir:

- `maxInvalidPasswordAttempts`-Kullanıcı için, hesap kilitlenmeden önce geçen süre içinde geçersiz parola denemesine izin verildiğini belirtir. Varsayılan değer 5 ' tir.
- `passwordAttemptWindow`-belirtilen geçersiz oturum açma girişimi sayısının, hesabın kilitlenmesine neden olacağı süreyi dakika cinsinden gösterir. Varsayılan değer 10 ' dur.

Bir Kullanıcı kilitlendiyse, yönetici hesabının kilidini açana kadar oturum açamaz. Bir Kullanıcı kilitlendiğinde, geçerli kimlik bilgileri sağlanmış olsa bile `ValidateUser` yöntemi *her zaman* `False`döndürür. Bu davranış, bir korsanın, deneme yanılma yöntemleri aracılığıyla sitenize bölünmesinin olasılığını azaltır, ancak parolasını unutduktan veya yanlışlıkla Caps Lock 'ta veya hatalı yazma gününe sahip olan geçerli bir kullanıcının kilitlenmesini sonlandırabilir.

Ne yazık ki, bir kullanıcı hesabının kilidini açmak için yerleşik bir araç yoktur. Bir hesabın kilidini açmak için veritabanını doğrudan değiştirebilir ve uygun Kullanıcı hesabı için `aspnet_Membership` tablosundaki `IsLockedOut` alanını değiştirebilir veya kilit açma seçeneklerinin kilidini açmak için seçenekleri olan kilitli hesapları listeleyen Web tabanlı bir arabirim oluşturabilirsiniz. Gelecekteki bir öğreticide, ortak kullanıcı hesabı ve rolle ilgili görevleri yerine getirmeye yönelik yönetim arabirimleri oluşturmayı inceleyeceğiz.

> [!NOTE]
> `ValidateUser` yönteminin bir alt tarafı, sağlanan kimlik bilgileri geçersiz olduğunda, neden bir açıklama sağlamaz. Kullanıcı deposunda eşleşen bir Kullanıcı adı/parola çifti olmadığından veya Kullanıcı henüz onaylanmadığından veya Kullanıcı kilitlenmiş olduğundan kimlik bilgileri geçersiz olabilir. Adım 4 ' te, oturum açma girişimi başarısız olduğunda kullanıcıya daha ayrıntılı bir ileti göstermeyi öğreneceğiz.

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>2\. Adım: oturum açma Web denetimi aracılığıyla kimlik bilgileri toplama

[Oturum açma Web denetimi](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) , <a id="Tutorial02"> </a> [*form kimlik doğrulaması öğreticisine genel bakış*](../introduction/an-overview-of-forms-authentication-vb.md) konusunda daha sonra oluşturduğumuz bir varsayılan kullanıcı arabirimini çok benzer şekilde işler. Oturum açma denetiminin kullanılması, ziyaretçi kimlik bilgilerini toplamak için arabirim oluşturmak üzere sahip olma zorunluluğunu kaydeder. Üstelik, oturum açma denetimi kullanıcı oturumunu otomatik olarak imzalar (gönderilen kimlik bilgilerinin geçerli olduğu varsayıldığında) ve bu sayede herhangi bir kod yazmak zorunda kalmaktan tasarruf edin.

El ile oluşturulan arabirimi ve kodu bir oturum açma denetimiyle değiştirerek `Login.aspx`güncelleştirelim. `Login.aspx`içindeki mevcut biçimlendirmeyi ve kodu kaldırarak başlayın. Doğru bir şekilde silebilirsiniz ya da yalnızca bir açıklama olarak görebilirsiniz. Bildirim temelli işaretlemeyi açıklama eklemek için `<%--` ve `--%>` sınırlayıcılarıyla çevreleyin. Bu sınırlayıcıları el ile girebilir veya şekil 2 ' de gösterildiği gibi, açıklama eklemek için metni seçip araç çubuğunda Seçili çizgiler simgesine tıklayabilirsiniz. Benzer şekilde, arka plan kod sınıfında seçili kodu açıklama olarak eklemek için seçili çizgiler simgesini açıklama olarak kullanabilirsiniz.

[Login. aspx dosyasındaki mevcut bildirime dayalı biçimlendirmeyi ve kaynak kodunu açıklama ![](validating-user-credentials-against-the-membership-user-store-vb/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image4.png)

**Şekil 2**: login. aspx dosyasındaki mevcut bildirime dayalı biçimlendirmeyi ve kaynak kodunu açıklama olarak ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image6.png))

> [!NOTE]
> Visual Studio 2005 ' de bildirim temelli biçimlendirme görüntülenirken Seçili satırlar simgesinin açıklaması kullanılamaz. Visual Studio 2008 kullanmıyorsanız `<%--` ve `--%>` sınırlayıcılarını el ile eklemeniz gerekir.

Sonra, bir oturum açma denetimini sayfada bulunan araç kutusundan sürükleyin ve `ID` özelliğini `myLogin`olarak ayarlayın. Bu noktada, ekranınızda şekil 3 ' e benzer görünmelidir. Oturum açma denetiminin varsayılan arabiriminin Kullanıcı adı ve parola, bir sonraki zaman beni anımsa onay kutusu ve oturum açma düğmesi için TextBox denetimleri içerdiğini unutmayın. Ayrıca iki metin kutuları için `RequiredFieldValidator` denetimleri vardır.

[![sayfaya bir oturum açma denetimi ekleyin](validating-user-credentials-against-the-membership-user-store-vb/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image7.png)

**Şekil 3**: sayfaya bir oturum açma denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image9.png))

Tebrikler! Oturum açma denetiminin oturum açma düğmesine tıklandığında, bir geri gönderme gerçekleşir ve oturum açma denetimi, girilen Kullanıcı adı ve parolayı geçirerek `Membership.ValidateUser` yöntemini çağırır. Kimlik bilgileri geçersizse, oturum açma denetimi şöyle bir ileti görüntüler. Ancak, kimlik bilgileri geçerliyse, oturum açma denetimi Forms kimlik doğrulama bileti oluşturur ve kullanıcıyı uygun sayfaya yönlendirir.

Oturum açma denetimi, kullanıcıyı başarılı bir oturum açma üzerine yönlendiren uygun sayfayı belirlemekte kullanılacak dört faktörü kullanır:

- Oturum açma denetiminin, form kimlik doğrulaması yapılandırmasındaki `loginUrl` ayarı tarafından tanımlanan oturum açma sayfasında olup olmadığı. Bu ayarın varsayılan değeri `Login.aspx`
- `ReturnUrl` QueryString parametresinin varlığı
- Oturum açma denetiminin [`DestinationUrl` özelliğinin](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx) değeri
- Forms kimlik doğrulaması yapılandırma ayarlarında belirtilen `defaultUrl` değeri; Bu ayarın varsayılan değeri default. aspx ' dir

Şekil 4 ' te, oturum açma denetiminin ilgili sayfa kararına ulaşmak için bu dört parametreyi nasıl kullandığı gösterilmektedir.

[![sayfaya bir oturum açma denetimi ekleyin](validating-user-credentials-against-the-membership-user-store-vb/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image10.png)

**Şekil 4**: sayfaya bir oturum açma denetimi ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image12.png))

Bir tarayıcı aracılığıyla siteyi ziyaret ederek ve üyelik çerçevesinde var olan bir kullanıcı olarak oturum açarak, oturum açma denetimini test etmek için bir dakikanızı ayırın.

Oturum açma denetiminin işlenmiş arabirimi yüksek oranda yapılandırılabilir. Görünümünü etkileyen bazı özellikler vardır; Artık, oturum açma denetimi, Kullanıcı arabirimi öğelerinin düzeni üzerinde kesin denetim için bir şablona dönüştürülebilir. Bu adımın geri kalanında görünümün ve düzenin nasıl özelleştirileceği incelenir.

### <a name="customizing-the-login-controls-appearance"></a>Oturum açma denetiminin görünümünü özelleştirme

Oturum açma denetiminin varsayılan özellik ayarları, Kullanıcı arabirimini bir başlık (oturum açma), TextBox ve etiket denetimleri Kullanıcı adı ve parola girişleri, bir sonraki zaman anımsa onay kutusu ve oturum açma düğmesi ile birlikte işler. Bu öğelerin görünümleri, oturum açma denetiminin çok sayıda özelliği aracılığıyla yapılandırılabilir. Ayrıca, Yeni Kullanıcı hesabı oluşturmak için bir sayfanın bağlantısı gibi ek kullanıcı arabirimi öğeleri, bir özellik veya ikisi ayarlanarak eklenebilir.

Oturum açma denetimizin görünümünü en az bir dakika sonra harcayalım. `Login.aspx` sayfanın en üstünde, oturum açma bilgisi olan bir metin zaten olduğundan, oturum açma denetiminin başlığı gereksiz. Bu nedenle, oturum açma denetiminin başlığını kaldırmak için [`TitleText` Özellik](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) değerini temizleyin.

Kullanıcı adı: ve parola: iki metin kutusu denetiminin solundaki Etiketler sırasıyla [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) ve [`PasswordLabelText` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx)aracılığıyla özelleştirilebilir. Kullanıcı adını değiştirelim: etiketle Kullanıcı adı:. Etiket ve metin kutusu stilleri sırasıyla [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) ve [`TextBoxStyle` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx)aracılığıyla yapılandırılabilir.

Beni anımsa bir sonraki zaman onay kutusunun Text özelliği, oturum açma denetiminin [`RememberMeText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx)aracılığıyla ayarlanabilir ve varsayılan olarak denetlenen durumu [`RememberMeSet` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) (varsayılan olarak false ' dur) ile yapılandırılabilir. Devam edin ve şimdi beni anımsa onay kutusunun varsayılan olarak denetleneceğini sağlamak için `RememberMeSet` özelliğini true olarak ayarlayın.

Oturum açma denetimi, Kullanıcı arabirimi denetimlerinin yerleşimini ayarlamak için iki özellik sunar. [`TextLayout` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) , Kullanıcı adı: ve Password: etiketlerin Ilgili metin kutularının solunda (varsayılan) mi yoksa üzerinde mi göründüğünü gösterir. [`Orientation` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) , Kullanıcı adı ve parola girişlerinin dikey mi (diğeri üzerinde) yoksa yatay mi olduğunu gösterir. Bu iki özelliği varsayılan ayarlarına ayarlıyorum, ancak sonuçta ortaya çıkan etkiyi görmek için bu iki özelliği varsayılan olmayan değerlerine ayarlamayı deneyin.

> [!NOTE]
> Sonraki bölümde, oturum açma denetiminin yerleşimini yapılandırırken, düzen denetiminin Kullanıcı arabirimi öğelerinin kesin yerleşimini tanımlamak için şablonları kullanma bölümüne bakacağız.

[`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) ve [`CreateUserUrl` özelliklerini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) henüz kaydedilmemiş olarak ayarlayıp, oturum açma denetiminin özellik ayarlarını kaydırın. Hesap oluşturun! ve sırasıyla `~/Membership/CreatingUserAccounts.aspx`. Bu, <a id="Tutorial05"> </a> [önceki öğreticide](creating-user-accounts-vb.md)oluşturduğumuz sayfaya işaret eden, oturum açma denetiminin arabirimine bir köprü ekler. Oturum açma denetiminin [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) ve [`HelpPageUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) ve [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) ve [`PasswordRecoveryUrl` özellikleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) aynı şekilde çalışır, bir yardım sayfasına bağlantıları işleme ve parola kurtarma sayfası.

Bu özellik değiştirildikten sonra, oturum açma denetiminizin bildirim temelli biçimlendirme ve görünüşü Şekil 5 ' te gösterilenle benzer şekilde görünmelidir.

[Oturum açma denetiminin özelliklerinin değerlerini ![görünümü dikte](validating-user-credentials-against-the-membership-user-store-vb/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image13.png)

**Şekil 5**: oturum açma denetiminin özelliklerinin değerleri görünümü dikte ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image15.png))

### <a name="configuring-the-login-controls-layout"></a>Oturum açma denetiminin yerleşimini yapılandırma

Oturum açma Web denetiminin varsayılan kullanıcı arabirimi, bir HTML `<table>`arabirimini yerleştirir. Ancak işlenmiş çıktı üzerinde daha ayrıntılı denetime ihtiyacım varsa ne olacak? Belki de `<table>` bir dizi `<div>` etiketi ile değiştirmek istiyoruz. Veya uygulamamız kimlik doğrulaması için ek kimlik bilgileri gerektiriyorsa ne olacak? Örneğin, çok sayıda Finans Web sitesi, kullanıcıların yalnızca bir Kullanıcı adı ve parola sağlamalarına, ayrıca bir kişisel kimlik numarası (PIN) veya diğer tanımlama bilgilerine sahip olmasını gerektirir. Nedenler ne olursa olsun, oturum açma denetimini bir şablona dönüştürmek mümkündür ve bu, arabirimin bildirim temelli işaretlemesini açıkça tanımlayabiliriz.

Oturum açma denetimini ek kimlik bilgileri toplayacak şekilde güncelleştirmek için iki şey yapmanız gerekir:

1. Ek kimlik bilgilerini toplamak için, oturum açma denetiminin arabirimini Web denetimleri içerecek şekilde güncelleştirin.
2. Kullanıcının Kullanıcı adı ve parolası geçerliyse ve bunların ek kimlik bilgileri geçerli olduğunda kimlik doğrulaması yapmak için oturum açma denetiminin iç kimlik doğrulama mantığını geçersiz kılın.

İlk görevi gerçekleştirmek için, oturum açma denetimini bir şablona dönüştürmemiz ve gerekli Web denetimlerini eklemesi gerekir. İkinci görevde olduğu gibi, denetimin [`Authenticate` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)için bir olay işleyicisi oluşturularak, oturum açma denetiminin kimlik doğrulama mantığının yerini alabilirsiniz.

Oturum açma denetimini, Kullanıcı adı, parola ve e-posta adresi için sorar ve yalnızca belirtilen e-posta adresi dosyadaki e-posta adresiyle eşleşiyorsa kullanıcının kimliğini doğrular. Önce, oturum açma denetiminin arabirimini bir şablona dönüştürmeniz gerekir. Oturum açma denetiminin akıllı etiketinden şablona Dönüştür seçeneğini belirleyin.

[![oturum açma denetimini şablona dönüştürmek](validating-user-credentials-against-the-membership-user-store-vb/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image16.png)

**Şekil 6**: oturum açma denetimini bir şablona Dönüştür ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image18.png))

> [!NOTE]
> Oturum açma denetimini şablon öncesi sürümüne geri döndürmek için denetimin akıllı etiketindeki Sıfırla bağlantısına tıklayın.

Oturum açma denetimini bir şablona dönüştürmek, denetimin bildirim temelli işaretlemesini HTML öğeleriyle ve Kullanıcı arabirimini tanımlayan Web denetimleriyle bir `LayoutTemplate` ekler. Şekil 7 ' de gösterildiği gibi, denetimi bir şablona dönüştürmek, bir şablon kullanılırken bu özellik değerleri dikkate alındıklarından, Özellikler penceresi `TitleText`, `CreateUserUrl`vb. gibi birçok özelliği kaldırır.

[![, oturum açma denetimi bir şablona dönüştürüldüğünde daha az özellik kullanılabilir](validating-user-credentials-against-the-membership-user-store-vb/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image19.png)

**Şekil 7**: oturum açma denetimi bir şablona dönüştürüldüğünde daha az özellik kullanılabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](validating-user-credentials-against-the-membership-user-store-vb/_static/image21.png))

`LayoutTemplate` HTML biçimlendirmesi gerektiği şekilde değiştirilebilir. Benzer şekilde, şablona yeni Web denetimleri eklemeyi de ücretsiz olarak hissetmekten çekinmeyin. Ancak, oturum açma denetiminin çekirdek Web denetimlerinin şablonda kalması ve atanan `ID` değerlerinin tutulması önemlidir. Özellikle `UserName` veya `Password` metin kutularını, `RememberMe` onay kutusunu, `LoginButton` düğmesini, `FailureText` etiketini veya `RequiredFieldValidator` denetimlerini kaldırmayın veya yeniden adlandırmayın.

Ziyaretçi e-posta adresini toplamak için, şablona bir metin kutusu eklememiz gerekiyor. `Password` metin kutusunu içeren tablo satırı (`<tr>`) ve bir sonraki beni anımsa onay kutusunu tutan tablo satırı arasına aşağıdaki bildirim temelli biçimlendirmeyi ekleyin:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample2.aspx)]

`Email` metin kutusunu ekledikten sonra, sayfayı bir tarayıcıdan ziyaret edin. Şekil 8 ' de gösterildiği gibi, oturum açma denetiminin Kullanıcı arabirimi artık üçüncü bir TextBox içerir.

[![oturum açma denetimi artık kullanıcının e-posta adresi için bir metin kutusu Içeriyor](validating-user-credentials-against-the-membership-user-store-vb/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image22.png)

**Şekil 8**: oturum açma denetimi artık kullanıcının e-posta adresi Için bir metin kutusu içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image24.png))

Bu noktada, oturum açma denetimi, sağlanan kimlik bilgilerini doğrulamak için `Membership.ValidateUser` yöntemini kullanmaya devam eder. Karşılık gelen `Email` metin kutusuna girilen değerin, kullanıcının oturum açabilip oturum açıp etmeyeceğini hiçbir şekilde yok. 3\. adımda, kimlik bilgilerinin yalnızca Kullanıcı adı ve parola geçerli olduğunda ve sağlanan e-posta adresi dosyadaki e-posta adresiyle eşleşiyorsa, kimlik bilgilerinin geçerli kabul edilmesi için oturum açma denetiminin kimlik doğrulama mantığını geçersiz kılma bölümüne bakacağız.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>3\. Adım: oturum açma denetiminin kimlik doğrulama mantığını değiştirme

Bir ziyaretçi kimlik bilgilerini ne zaman sağlar ve oturum aç düğmesine tıkladığında, bir geri gönderme ve oturum açma denetimi kimlik doğrulama iş akışı üzerinden ilerler. İş akışı, [`LoggingIn` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx)yükselterek başlar. Bu olayla ilişkili herhangi bir olay işleyicisi, `e.Cancel` özelliğini `True`ayarlayarak, oturum açma işlemini iptal edebilir.

Oturum açma işlemi iptal edilmediğinden, iş akışı [`Authenticate` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)yükselterek ilerler. `Authenticate` olayı için bir olay işleyicisi varsa, sağlanan kimlik bilgilerinin geçerli olup olmadığını belirlemekten sorumludur. Hiçbir olay işleyicisi belirtilmemişse, oturum açma denetimi, kimlik bilgilerinin geçerliliğini belirlemede `Membership.ValidateUser` yöntemini kullanır.

Sağlanan kimlik bilgileri geçerliyse, Forms kimlik doğrulama bileti oluşturulur, [`LoggedIn` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) tetiklenir ve Kullanıcı uygun sayfaya yönlendirilir. Ancak, kimlik bilgileri geçersiz kabul edildiği takdirde, [`LoginError` olayı](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) tetiklenir ve kullanıcıya kimlik bilgilerinin geçersiz olduğunu bildiren bir ileti görüntülenir. Varsayılan olarak, hata durumunda oturum açma denetimi, `FailureText` etiket denetiminin Text özelliğini bir hata iletisine ayarlar (oturum açma denemeniz başarılı olmadı. Lütfen yeniden deneyin). Ancak, oturum açma denetiminin [`FailureAction` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) `RedirectToLoginPage`olarak ayarlanırsa, oturum açma denetimi, oturum açma sayfasına `loginfailure=1` QueryString parametresini (oturum açma denetiminin hata iletisini görüntülemesine neden olur) ekleyerek bir `Response.Redirect` yayınlar.

Şekil 9, kimlik doğrulama iş akışının Akış grafiğini sunar.

[Oturum açma denetiminin kimlik doğrulama Iş akışını ![](validating-user-credentials-against-the-membership-user-store-vb/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image25.png)

**Şekil 9**: oturum açma denetiminin kimlik doğrulama iş akışı ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image27.png))

> [!NOTE]
> `FailureAction``RedirectToLogin` sayfası seçeneğini ne zaman kullanacağınızı merak ediyorsanız, aşağıdaki senaryoyu göz önünde bulundurun. Şu anda `Site.master` ana sayfamızda, anonim bir kullanıcı tarafından ziyaret edildiğinde sol sütunda görüntülenen metin, Merhaba, yabanger metni var, ancak bu metni bir oturum açma denetimiyle değiştirmek istediğimizi düşünün. Bu, anonim bir kullanıcının oturum açma sayfasını doğrudan ziyaret etmesini gerektirmek yerine sitedeki herhangi bir sayfadan oturum açmasına olanak tanır. Ancak, bir Kullanıcı Ana sayfa tarafından işlenen oturum açma denetimi aracılığıyla oturum açmıyorsa, bu sayfada büyük olasılıkla ek yönergeler, bağlantılar ve yeni bir hesap oluşturmak veya kayıp bir parola almak için ana sayfaya eklenmemiş bağlantılar gibi diğer yardım bilgileri de dahil olmak üzere, bunları oturum açma sayfasına (`Login.aspx`) yönlendirmek mantıklı olabilir.

### <a name="creating-theauthenticateevent-handler"></a>`Authenticate`olay Işleyicisi oluşturma

Özel kimlik doğrulama mantığımızı eklemek için, oturum açma denetiminin `Authenticate` olayı için bir olay işleyicisi oluşturmamız gerekir. `Authenticate` olayı için bir olay işleyicisi oluşturmak aşağıdaki olay işleyicisi tanımını oluşturur:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample3.vb)]

Görebileceğiniz gibi, `Authenticate` olay işleyicisi ikinci giriş parametresi olarak [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) türünde bir nesne geçirdi. `AuthenticateEventArgs` sınıfı, sağlanan kimlik bilgilerinin geçerli olup olmadığını belirtmek için kullanılan `Authenticated` adlı bir Boole özelliği içerir. Bundan sonra, sağlanan kimlik bilgilerinin geçerli olup olmadığını ve `e.Authenticate` özelliğini uygun şekilde ayarlamayı belirleyen kodu buraya yazalım.

### <a name="determining-and-validating-the-supplied-credentials"></a>Sağlanan kimlik bilgilerini belirleme ve doğrulama

Kullanıcı tarafından girilen Kullanıcı adı ve parola kimlik bilgilerini öğrenmek için oturum açma denetiminin [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) ve [`Password` özelliklerini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) kullanın. Ek Web denetimlerine girilen değerleri (örneğin, önceki adımda eklediğimiz `Email` metin kutusu) belirleyebilmek için, `ID` özelliği *`controlID`* değerine eşit olan şablonda Web denetimine programlı bir başvuru almak için `LoginControlID.FindControl`(" *`controlID`* ") kullanın. Örneğin, `Email` metin kutusuna bir başvuru almak için aşağıdaki kodu kullanın:

`Dim EmailTextBox As TextBox = CType(myLogin.FindControl("Email"), TextBox)`

Kullanıcının kimlik bilgilerini doğrulamak için iki şey olması gerekir:

1. Belirtilen kullanıcı adının ve parolanın geçerli olduğundan emin olun
2. Girilen e-posta adresinin, oturum açmaya çalışan kullanıcının dosyadaki e-posta adresiyle eşleştiğinden emin olun

İlk denetimi gerçekleştirmek için, 1. adımda gördüğdiğimiz gibi `Membership.ValidateUser` yöntemi kullanabiliriz. İkinci denetim için kullanıcının e-posta adresini belirlememiz gerekir, böylece metin kutusu denetimine girdiğiniz e-posta adresiyle karşılaştırılmaktadır. Belirli bir kullanıcı hakkında bilgi almak için `Membership` sınıfının [`GetUser` metodunu](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)kullanın.

`GetUser` yönteminde çok sayıda aşırı yükleme vardır. Herhangi bir parametreye geçirilmeden kullanılırsa, o anda oturum açmış olan kullanıcı hakkında bilgi döndürür. Belirli bir kullanıcı hakkında bilgi almak için, ' ın Kullanıcı adında geçen `GetUser` çağırın. Her iki durumda da, `GetUser` `UserName`, `Email`, `IsApproved`, `IsOnline`gibi özelliklere sahip [`MembershipUser` nesnesini](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)döndürür.

Aşağıdaki kod bu iki denetimi uygular. Her iki geçiş ise `e.Authenticate` `True`olarak ayarlanır, aksi takdirde `False`atanır.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample4.vb)]

Bu kod yerine, doğru Kullanıcı adını, parolayı ve e-posta adresini girerek geçerli bir kullanıcı olarak oturum açmaya çalışın. Yeniden deneyin, ancak bu zaman, bu kez doğru bir e-posta adresi kullanır (bkz. Şekil 10). Son olarak, var olmayan bir Kullanıcı adı kullanarak bunu üçüncü kez deneyin. İlk durumda, sitede başarıyla oturum açmanız gerekir, ancak son iki durumda oturum açma denetiminin geçersiz kimlik bilgileri iletisini görmeniz gerekir.

[![Tito, yanlış bir e-posta adresi sağlarken oturum açılamıyor](validating-user-credentials-against-the-membership-user-store-vb/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image28.png)

**Şekil 10**: Hatalı bir e-posta adresi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image30.png)) sağlanırken oturum açılamıyor

> [!NOTE]
> Üyelik çerçevesinin adım 1 ' de geçersiz oturum açma girişimlerini nasıl Işleyeceği konusunda anlatıldığı gibi `Membership.ValidateUser` yöntemi çağrıldığında ve geçersiz kimlik bilgileri geçirildiğinde, geçersiz oturum açma girişimini izler ve belirtilen zaman penceresinde belirli bir eşik eşiğini aşarsa kullanıcıyı kilitler. Özel kimlik doğrulama mantığımız `ValidateUser` yöntemini çağırdığı için geçerli bir Kullanıcı adı için hatalı bir parola, geçersiz oturum açma denemesi sayacını artırır, ancak Kullanıcı adı ve parolanın geçerli olduğu, ancak e-posta adresinin yanlış olması durumunda bu sayaç artmaz. Bu davranış, bir korsanın Kullanıcı adı ve parolayı bilmesi, ancak kullanıcının e-posta adresini belirlemesi için deneme yanılma tekniklerini kullanması gereken bir olasılıktır.

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>4\. Adım: oturum açma denetiminin geçersiz kimlik bilgileri Iletisini geliştirme

Kullanıcı geçersiz kimlik bilgileriyle oturum açmaya çalıştığında, oturum açma denetimi, oturum açma girişiminin başarısız olduğunu belirten bir ileti görüntüler. Özellikle, denetim, oturum açma girişiminizin varsayılan bir değeri olan [`FailureText` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx)tarafından belirtilen iletiyi görüntüler. Lütfen yeniden deneyin.

Kullanıcının kimlik bilgilerinin geçersiz olmasının birçok nedeni olduğunu unutmayın:

- Kullanıcı adı mevcut olmayabilir
- Kullanıcı adı var, ancak parola geçersiz
- Kullanıcı adı ve parola geçerli, ancak kullanıcı henüz onaylanmamış
- Kullanıcı adı ve parola geçerli, ancak kullanıcı kilitli (büyük olasılıkla belirtilen zaman çerçevesinde geçersiz oturum açma girişimi sayısını aştıkları için)

Ve özel kimlik doğrulama mantığı kullanılırken başka nedenler de olabilir. Örneğin, adım 3 ' te yazdığımız kodla, Kullanıcı adı ve parola geçerli olabilir, ancak e-posta adresi hatalı olabilir.

Kimlik bilgilerinin neden geçersiz olmasından bağımsız olarak, oturum açma denetimi aynı hata iletisini görüntüler. Bu geri bildirim olmaması, hesabı henüz onaylanmamış veya kilitlenen bir kullanıcı için kafa karıştırıcı olabilir. Çok az iş sayesinde, oturum açma denetiminin daha uygun bir ileti görüntülemesini de sağlayabilirsiniz.

Kullanıcı geçersiz kimlik bilgileriyle oturum açma girişiminde bulunduğunda, oturum açma denetimi `LoginError` olayını başlatır. Devam edin ve bu olay için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample5.vb)]

Yukarıdaki kod, oturum açma denetiminin `FailureText` özelliği varsayılan değere ayarlanarak başlatılır (oturum açma denemeniz başarılı olmadı. Lütfen yeniden deneyin). Daha sonra sağlanan kullanıcı adının mevcut bir kullanıcı hesabına eşlendiğini kontrol eder. Bu durumda, `MembershipUser` nesnenin `IsLockedOut` ve `IsApproved` özelliklerine bakar ve hesabın kilitlenip kilitlenmediğini veya henüz onaylanmadığını belirleyebilir. Her iki durumda da `FailureText` özelliği karşılık gelen bir değere güncelleştirilir.

Bu kodu test etmek için,, mevcut bir kullanıcı olarak oturum açmaya çalışır, ancak yanlış bir parola kullanın. 10 dakikalık bir zaman çerçevesinde bu beş kez bir satırda bunu yapın ve hesap kilitlenir. Şekil 11 ' de gösterildiği gibi, sonraki oturum açma girişimleri her zaman başarısız olur (doğru parolayla bile), ancak artık çok fazla geçersiz oturum açma denemesi nedeniyle hesabınız daha açıklayıcı bir şekilde görüntülenir. Hesabınızın kilidi açık olması için lütfen yöneticiye başvurun.

[![Tito geçersiz oturum açma girişimi gerçekleştirdi ve kilitlenmiş](validating-user-credentials-against-the-membership-user-store-vb/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image31.png)

**Şekil 11**: Tito geçersiz oturum açma girişimi gerçekleştirdi ve kilitlendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](validating-user-credentials-against-the-membership-user-store-vb/_static/image33.png))

## <a name="summary"></a>Özet

Bu öğreticide, oturum açma sayfamız belirtilen kimlik bilgilerini sabit kodlanmış Kullanıcı adı/parola çiftleri listesine göre doğruladı. Bu öğreticide, üyelik çerçevesinde kimlik bilgilerini doğrulamak için sayfayı güncelleştirdik. 1\. adımda `Membership.ValidateUser` yöntemini programlı olarak kullanma hakkında baktık. 2\. adımda, el ile oluşturulan kullanıcı arabirimimizi ve kodumuzu oturum açma denetimiyle değiştirdik.

Oturum açma denetimi standart bir oturum açma kullanıcı arabirimini işler ve Kullanıcı kimlik bilgilerini üyelik çerçevesine göre otomatik olarak doğrular. Ayrıca, geçerli kimlik bilgileri durumunda oturum açma denetimi, Kullanıcı tarafından form kimlik doğrulaması aracılığıyla oturum açar. Kısacası, tam işlevli bir oturum açma kullanıcı deneyimi yalnızca oturum açma denetimini bir sayfaya sürükleyerek, ek bildirime dayalı biçimlendirme veya kod gerekli olmadan kullanılabilir. Artık, oturum açma denetimi, hem işlenmiş Kullanıcı arabirimi hem de kimlik doğrulama mantığı üzerinde ince bir denetim sağlayan yüksek düzeyde özelleştirilebilir.

Bu noktada, Web sitemizden ziyaretçi yeni bir kullanıcı hesabı oluşturabilir ve sitede oturum açabilir, ancak kimliği doğrulanmış kullanıcıya göre sayfaların erişimini kısıtlama konusunda bakmamız gerekir. Şu anda, tüm kullanıcılar, kimliği doğrulanmış veya anonim, sitemizdeki herhangi bir sayfayı görüntüleyebilir. Sitemizdeki sayfalara erişimi denetim altına alarak, işlevselliği kullanıcıya bağlı olan belirli sayfaları da olabilir. Sonraki öğreticide, oturum açmış kullanıcıya göre erişimin ve sayfa içi işlevlerin nasıl sınırlandırılır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Kilitli ve onaylanmamış kullanıcılara özel Iletiler görüntüleme](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [ASP.NET 2.0 'ın üyeliğini, rollerini ve profilini İnceleme](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Nasıl yapılır: ASP.NET oturum açma sayfası oluşturma](https://msdn.microsoft.com/library/ms178331.aspx)
- [Oturum açma denetimi teknik belgeleri](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Oturum açma denetimlerini kullanma](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler, bir Murphy ve Michael Kayvero. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](creating-user-accounts-vb.md)
> [İleri](user-based-authorization-vb.md)
