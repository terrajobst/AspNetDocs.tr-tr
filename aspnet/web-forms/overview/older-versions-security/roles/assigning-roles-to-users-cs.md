---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
title: Kullanıcılara rol atama (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, kullanıcıların hangi rollere ait olduğunu yönetmeye yardımcı olmak için iki ASP.NET sayfası oluşturacağız. İlk sayfa, nelerin hangileri olduğunu görmek için tesislere dahil edilir.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: d522639a-5aca-421e-9a76-d73f95607f57
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-cs
msc.type: authoredcontent
ms.openlocfilehash: 3346e47cf604ed1d4003ca83203116666e37cb1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78571773"
---
# <a name="assigning-roles-to-users-c"></a>Kullanıcılara Rol Atama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.10.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_cs.pdf)

> Bu öğreticide, kullanıcıların hangi rollere ait olduğunu yönetmeye yardımcı olmak için iki ASP.NET sayfası oluşturacağız. İlk sayfa, hangi kullanıcıların belirli bir role ait olduğunu, belirli bir kullanıcının hangi rollere ait olduğunu ve belirli bir rolün belirli bir rolü atama veya kaldırma olanağını görmek için tesis içerir. İkinci sayfada, yeni oluşturulan kullanıcının hangi rollere ait olduğunu belirleyen bir adım içerecek şekilde CreateUserWizard denetimini geliştireceğiz. Bu, yöneticinin yeni kullanıcı hesapları oluşturabilebileceği senaryolarda faydalıdır.

## <a name="introduction"></a>Giriş

<a id="_msoanchor_1"> </a> [Önceki öğreticide](creating-and-managing-roles-cs.md) , rol çatısı ve `SqlRoleProvider`incelendi. rolleri oluşturmak, almak ve silmek için `Roles` sınıfını nasıl kullanacağınızı gördük. Rolleri oluşturmanın ve silmenin yanı sıra, bir role Kullanıcı atayabilmeniz veya kaldırabilmemiz gerekir. Ne yazık ki ASP.NET, kullanıcıların hangi rollere ait olduğunu yönetmek için herhangi bir Web denetimleriyle birlikte gelmez. Bunun yerine, bu ilişkilendirmeleri yönetmek için kendi ASP.NET sayfalarınızın oluşturulması gerekir. İyi haber, kullanıcıları rollere eklemek ve kaldırmak oldukça kolaydır. `Roles` sınıfı bir veya daha fazla role bir veya daha fazla kullanıcı eklemek için bir dizi yöntem içerir.

Bu öğreticide, kullanıcıların hangi rollere ait olduğunu yönetmeye yardımcı olmak için iki ASP.NET sayfası oluşturacağız. İlk sayfa, hangi kullanıcıların belirli bir role ait olduğunu, belirli bir kullanıcının hangi rollere ait olduğunu ve belirli bir rolün belirli bir rolü atama veya kaldırma olanağını görmek için tesis içerir. İkinci sayfada, yeni oluşturulan kullanıcının hangi rollere ait olduğunu belirleyen bir adım içerecek şekilde CreateUserWizard denetimini geliştireceğiz. Bu, yöneticinin yeni kullanıcı hesapları oluşturabilebileceği senaryolarda faydalıdır.

Haydi başlayın!

## <a name="listing-what-users-belong-to-what-roles"></a>Hangi kullanıcıların hangi rollere ait olduğunu listeleme

Bu öğreticide ilk iş sırası, kullanıcıların rollere atanabileceği bir Web sayfası oluşturmaktır. Kullanıcılara rolleri nasıl atayacağınızı kendimize konusunda endişelenmemiz için öncelikle hangi kullanıcıların hangi rollere ait olduğunu belirleme konusunda odaklanalım. Bu bilgileri görüntülemenin iki yolu vardır: "role göre" veya "Kullanıcı tarafından". Ziyaretçinin bir rol seçmesini ve sonra bu rolü role ait tüm kullanıcıları ("role göre" görüntülemesi) göstermesini ve ardından ziyaretçinin bir Kullanıcı seçmesini ve ardından bu kullanıcıya atanan rolleri ("Kullanıcı tarafından" görüntülemesi) göstermesini istemiz.

"Role göre" görünümü, ziyaretçinin belirli bir role ait olan kullanıcılar kümesini bilmek istediği koşullarda yararlıdır; "Kullanıcı tarafından" görünümü, ziyaretçi belirli bir kullanıcının rolünü bilmeleri gerektiğinde idealdir. Sayfamıza hem "role göre" hem de "Kullanıcı tarafından" arabirimleri dahil edelim.

"Kullanıcı tarafından" arabirimi oluşturmaya başlayacağız. Bu arabirim, açılan bir listeden ve onay listesi listesinden oluşur. Açılan liste, sistemdeki kullanıcı kümesiyle doldurulur; onay kutuları, rolleri numaralandıracaktır. Açılır listeden bir kullanıcı seçildiğinde, kullanıcının ait olduğu roller kontrol edilir. Sayfayı ziyaret eden kişi, seçilen kullanıcıyı ilgili rollerden eklemek veya kaldırmak için onay kutularını denetleyebilir veya işaretini kaldırabilir.

> [!NOTE]
> Kullanıcı hesaplarını listelemek için açılan bir liste kullanmak, yüzlerce Kullanıcı hesabının olabileceği Web siteleri için ideal bir seçenek değildir. Bir açılan liste, kullanıcının görece bir seçenek listesinden bir öğe seçmesine olanak tanımak için tasarlanmıştır. Liste öğelerinin sayısı arttıkça hızlı bir şekilde hale gelir. Potansiyel olarak çok sayıda kullanıcı hesabı olacak bir Web sitesi oluşturuyorsanız, disk belleğine alınabilir GridView veya filtrelenebilir bir arabirim gibi farklı bir kullanıcı arabirimi kullanmayı düşünmek isteyebilirsiniz. Bu, ziyaretçilerin bir harf seçmesini ve sonra yalnızca Kullanıcı adı seçili harfle başlayan kullanıcıları gösterir.

## <a name="step-1-building-the-by-user-user-interface"></a>1\. Adım: "Kullanıcı tarafından" Kullanıcı arabirimini oluşturma

`UsersAndRoles.aspx` sayfasını açın. Sayfanın üst kısmında, `ActionStatus` adlı bir etiket Web denetimi ekleyin ve `Text` özelliğini temizleyin. Bu etiketi, gerçekleştirilen eylemler hakkında geri bildirim sağlamak, "Yöneticiler rolüne kullanıcı Tito eklendi" veya "Kullanıcı Jisun, ana bilgisayar rolünden kaldırılmadı" gibi iletileri görüntülemek için kullanacağız. Bu iletilerin öne çıkmasını sağlamak için etiketin `CssClass` özelliğini "önemli" olarak ayarlayın.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample1.aspx)]

Sonra, aşağıdaki CSS sınıfı tanımını `Styles.css` stil sayfasına ekleyin:

[!code-css[Main](assigning-roles-to-users-cs/samples/sample2.css)]

Bu CSS tanımı, tarayıcıya büyük ve kırmızı bir yazı tipi kullanarak etiketi görüntülemesini söyler. Şekil 1 ' de bu efekt Visual Studio Tasarımcısı aracılığıyla gösterilmiştir.

[Etiketin CssClass özelliği büyük ve kırmızı bir yazı tipiyle sonuçlanıyor ![](assigning-roles-to-users-cs/_static/image2.png)](assigning-roles-to-users-cs/_static/image1.png)

**Şekil 1**: etiketin `CssClass` özelliği büyük ve kırmızı bir yazı tipiyle sonuçlanıyor ([tam boyutlu görüntüyü görüntülemek için tıklatın](assigning-roles-to-users-cs/_static/image3.png))

Sonra, sayfaya bir DropDownList ekleyin, `ID` özelliğini `UserList`olarak ayarlayın ve `AutoPostBack` özelliğini true olarak ayarlayın. Bu DropDownList 'i sistemdeki tüm kullanıcıları listelemek için kullanacağız. Bu DropDownList, bir MembershipUser nesneleri koleksiyonuna bağlanacak. DropDownList 'in, MembershipUser nesnesinin UserName özelliğini göstermesini istiyoruz (ve bunu liste öğelerinin değeri olarak kullanın), DropDownList 'in `DataTextField` ve `DataValueField` özelliklerini "UserName" olarak ayarlayın.

DropDownList 'in altında, `UsersRoleList`adlı bir yineleyici ekleyin. Bu Yineleyici, sistemdeki tüm rolleri bir dizi onay kutusu olarak listeler. Yineleyicisi 'nin `ItemTemplate` aşağıdaki bildirim temelli biçimlendirmeyi kullanarak tanımlayın:

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample3.aspx)]

`ItemTemplate` biçimlendirmesi, `RoleCheckBox`adlı tek bir CheckBox Web denetimini içerir. CheckBox 'ın `AutoPostBack` özelliği true olarak ayarlanır ve `Text` özelliği `Container.DataItem`'e bağlanır. Veri bağlama sözdiziminin `Container.DataItem` nedeni, rol çerçevesinin rol adları listesini bir dize dizisi olarak döndürmesi ve bu dize dizisi, yineleyici öğesine bağlamamız olacaktır. Bu sözdiziminin, bir veri Web denetimine yönelik bir dizinin içeriğini göstermek için nasıl kullanıldığına ilişkin kapsamlı bir açıklama, Bu öğreticinin kapsamının dışındadır. Bu konuyla ilgili daha fazla bilgi için, bir [skalar diziyi veri Web denetimine bağlama](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx)konusuna bakın.

Bu noktada, "kullanıcıya göre" arabiriminin bildirime dayalı biçimlendirmesi aşağıdakine benzer görünmelidir:

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample4.aspx)]

Artık Kullanıcı hesaplarının kümesini DropDownList 'e ve roller kümesini Repeater 'a bağlamak için kodu yazmaya hazırsınız. Sayfanın arka plan kod sınıfında, aşağıdaki kodu kullanarak `BindUsersToUserList` adlı bir yöntemi ve başka bir adlandırılmış `BindRolesList`ekleyin:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample5.cs)]

`BindUsersToUserList` yöntemi, [`Membership.GetAllUsers` yöntemi](https://msdn.microsoft.com/library/dy8swhya.aspx)aracılığıyla sistemdeki tüm Kullanıcı hesaplarını alır. Bu, bir [`MembershipUser` örnekleri](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx)koleksiyonu olan [`MembershipUserCollection` nesnesini](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx)döndürür. Bu koleksiyon daha sonra `UserList` DropDownList 'e bağlanır. Koleksiyonu oluşturan `MembershipUser` örnekleri, `UserName`, `Email`, `CreationDate`ve `IsOnline`gibi çeşitli özellikler içerir. DropDownList 'in `UserName` özelliğinin değerini göstermesini söylemek için `UserList` DropDownList 'in `DataTextField` ve `DataValueField` özelliklerinin "UserName" olarak ayarlandığından emin olun.

> [!NOTE]
> `Membership.GetAllUsers` yönteminin iki aşırı yüklemesi vardır: giriş parametresi yok kabul eden ve tüm kullanıcıları ve sayfa dizini ve sayfa boyutu için tamsayı değerlerini alan ve yalnızca belirtilen kullanıcıların alt kümesini döndüren bir tane. Çok sayıda kullanıcı hesabı, disk belleğine alınabilen bir kullanıcı arabirimi öğesinde görüntülenirken, ikinci aşırı yükleme, Kullanıcı hesaplarının yalnızca tam alt kümesini döndürdüğünden, bunların tümünün yerine daha verimli bir şekilde görüntülenmesini sağlamak için kullanılabilir.

`BindRolesToList` yöntemi, sistem içindeki rolleri içeren bir dize dizisi döndüren `Roles` sınıfının [`GetAllRoles` yöntemini](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)çağırarak başlar. Bu dize dizisi daha sonra yineleyicisi 'ne bağlanır.

Son olarak, sayfa ilk yüklendiğinde bu iki yöntemi çağırmalıdır. `Page_Load` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample6.cs)]

Bu kodla birlikte, bir tarayıcı aracılığıyla sayfayı ziyaret etmek için bir dakikanızı ayırın; ekranınızın Şekil 2 ' ye benzer olması gerekir. Tüm Kullanıcı hesapları açılan listede doldurulur ve altında her bir rol onay kutusu olarak görünür. DropDownList ve CheckBox 'ın `AutoPostBack` özelliklerini true olarak belirlediğimiz için, seçilen kullanıcıyı değiştirmek veya bir rolü denetlemek ya da kaldırmak geri göndermeye neden olur. Ancak, bu eylemleri işlemek için henüz kod yazdığımız için hiçbir eylem yapılmaz. Sonraki iki bölümde bu görevleri ele alacağız.

[![, Kullanıcı ve rolleri görüntüleyen sayfa](assigning-roles-to-users-cs/_static/image5.png)](assigning-roles-to-users-cs/_static/image4.png)

**Şekil 2**: sayfada kullanıcılar ve roller görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image6.png))

### <a name="checking-the-roles-the-selected-user-belongs-to"></a>Seçilen kullanıcının ait olduğu roller denetleniyor

Sayfa ilk yüklendiğinde veya ziyaretçi aşağı açılan listeden yeni bir Kullanıcı seçtiğinde, belirli bir rol onay kutusunun yalnızca seçili Kullanıcı söz konusu role aitse denetlenmesi için `UsersRoleList`onay kutularını güncelleştirmemiz gerekir. Bunu gerçekleştirmek için aşağıdaki kodla `CheckRolesForSelectedUser` adlı bir yöntem oluşturun:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample7.cs)]

Yukarıdaki kod, seçilen kullanıcının kim olduğunu belirleyerek başlar. Daha sonra, belirtilen kullanıcının roller kümesini dize dizisi olarak döndürmek için rol sınıfının [`GetRolesForUser(userName)` yöntemini](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx) kullanır. Sonra, yineleyicisi 'nin öğeleri numaralandırılır ve her bir öğenin `RoleCheckBox` onay kutusu programlama yoluyla başvurulur. Onay kutusu yalnızca karşılık gelen rolün `selectedUsersRoles` dize dizisi içinde yer alıyorsa denetlenir.

> [!NOTE]
> `selectedUserRoles.Contains<string>(...)` sözdizimi, ASP.NET sürüm 2,0 kullanıyorsanız derlenmeyecektir. `Contains<string>` yöntemi, ASP.NET 3,5 ' de yeni olan [LINQ kitaplığı](http://en.wikipedia.org/wiki/Language_Integrated_Query)'nın bir parçasıdır. Hala ASP.NET sürüm 2,0 kullanıyorsanız, bunun yerine [`Array.IndexOf<string>` yöntemini](https://msdn.microsoft.com/library/eha9t187.aspx) kullanın.

`CheckRolesForSelectedUser` yönteminin iki durumda çağrılması gerekir: sayfa ilk yüklendiğinde ve `UserList` DropDownList 'in seçili dizini değiştirildiğinde her seferinde. Bu nedenle, `Page_Load` olay işleyiciden bu yöntemi çağırın (`BindUsersToUserList` ve `BindRolesToList`çağrılarından sonra). Ayrıca, DropDownList 'in `SelectedIndexChanged` olayı için bir olay işleyicisi oluşturun ve bu yöntemi buradan çağırın.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample8.cs)]

Bu kodla birlikte, sayfayı tarayıcı üzerinden test edebilirsiniz. Ancak, `UsersAndRoles.aspx` sayfası şu anda rollere kullanıcı atama yeteneği olmadığından, hiçbir kullanıcı role sahip değildir. Kullanıcılara bir süre içinde Kullanıcı atamaya yönelik bir arabirim oluşturacağız. bu nedenle, bu kodun çalıştığı Sözcüklerimi alabilir ve daha sonra bu işlevi test etmek için `aspnet_UsersInRoles` tabloya kayıtları ekleyerek el ile roller ekleyebilirsiniz.

### <a name="assigning-and-removing-users-from-roles"></a>Rollerden Kullanıcı atama ve kaldırma

Ziyaretçi `UsersRoleList` Yineleyici içindeki bir onay kutusunu denetlediğinde veya denetlediğinde, Seçili kullanıcıyı ilgili role eklemesi veya kaldırması gerekir. CheckBox 'ın `AutoPostBack` özelliği şu anda true olarak ayarlanmıştır. Bu, bir geri göndermeye her zaman yineleyici onay kutusu işaretli veya işaretlenmemiş olarak neden olur. Kısaca, CheckBox 'ın `CheckChanged` olayı için bir olay işleyicisi oluşturuyoruz. Onay kutusu bir yineleyici denetiminde olduğundan, olay işleyicisi sıhhi tesisat 'yi el ile eklememiz gerekiyor. Olay işleyicisini, bir `protected` yöntemi olarak, bu şekilde arka plan kod sınıfına ekleyerek başlayın:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample9.cs)]

Bu olay işleyicisine yönelik kodu bir süre içinde yazmak için geri dönebiliyoruz. Ancak ilk olarak olay işleme sıhhi tesisat 'yi tamamlayalim. Yineleyicisi 'nin `ItemTemplate`içindeki onay kutusundan `OnCheckedChanged="RoleCheckBox_CheckChanged"`ekleyin. Bu söz dizimi `RoleCheckBox_CheckChanged` olay işleyicisini `RoleCheckBox``CheckedChanged` olayına kablolar.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample10.aspx)]

Son göreviniz `RoleCheckBox_CheckChanged` olay işleyicisini tamammız. Bu onay kutusu örneği, `Text` ve `Checked` özellikleri aracılığıyla hangi rolün işaretli veya işaretlenmemiş olduğunu bize söylerken, olayı oluşturan CheckBox denetimine başvurarak başlatmamız gerekiyor. Seçilen kullanıcının Kullanıcı adı ile birlikte bu bilgileri kullanarak, `Roles` sınıfın [`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx) veya [`RemoveUserFromRole` yöntemi](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)aracılığıyla Kullanıcı ekleme veya rol çıkardık.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample11.cs)]

Yukarıdaki kod, `sender` giriş parametresi aracılığıyla kullanılabilir olan olayı oluşturan onay kutusuna programlı bir şekilde gönderilir. Onay kutusu işaretliyse, seçilen kullanıcı belirtilen role eklenir, aksi takdirde rolden kaldırılır. Her iki durumda da `ActionStatus` etiketi, az önce gerçekleştirilen eylemi özetleyen bir ileti görüntüler.

Bu sayfayı bir tarayıcı ile test etmek için bir dakikanızı ayırın. Kullanıcı Tito ' ı seçin ve ardından hem Yöneticiler hem de süper yönetici rollerine Tito ' ı ekleyin.

[![Tito, Yöneticiler ve süper yönetici rollerine eklenmiştir](assigning-roles-to-users-cs/_static/image8.png)](assigning-roles-to-users-cs/_static/image7.png)

**Şekil 3**: yönetim ve süper yönetici rollerine Tito eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image9.png))

Sonra, açılan listeden Kullanıcı deneme tarafı ' nı seçin. Bir geri gönderme işlemi ve yineleyicisi 'nin onay kutuları `CheckRolesForSelectedUser`aracılığıyla güncelleştirilir. Deneme CE hiçbir role ait olmadığından, iki onay kutusu işaretlenmemiştir. Ardından, süper vizörler rolüne bir deneme yanılması ekleyin.

[![deneme süresi, süper vizörler rolüne eklendi](assigning-roles-to-users-cs/_static/image11.png)](assigning-roles-to-users-cs/_static/image10.png)

**Şekil 4**: deneme süresi, süper vizörler rolüne eklendi ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image12.png))

`CheckRolesForSelectedUser` yönteminin işlevlerini daha fazla doğrulamak için, Tito veya Bruce dışında bir kullanıcı seçin. Onay kutularının, hiçbir role ait olmadığını belirten otomatik olarak işaretlenmediğini not edin. Tito 'ya geri dönün. Hem Yöneticiler hem de süper vizörler onay kutuları denetlenmelidir.

## <a name="step-2-building-the-by-roles-user-interface"></a>2\. Adım: "roller tarafından" Kullanıcı arabirimini oluşturma

Bu noktada, "kullanıcılar tarafından" arabirimini tamamladık ve "rollere göre" arabirimine göz atın. "Rol ölçütü" arabirimi, kullanıcıdan bir açılan listeden bir rol seçmesini ve ardından GridView içinde bu role ait olan kullanıcı kümesini görüntüler.

`UsersAndRoles.aspx` sayfasına başka bir DropDownList denetimi ekleyin. Bunu Yineleyici denetiminin altına yerleştirin, `RoleList`adlandırın ve `AutoPostBack` özelliğini true olarak ayarlayın. Bunun altında, bir GridView ekleyip `RolesUserList`adlandırın. Bu GridView, seçili role ait olan kullanıcıları listeler. GridView 'ın `AutoGenerateColumns` özelliğini false olarak ayarlayın, Grid 'in `Columns` koleksiyonuna bir TemplateField ekleyin ve `HeaderText` özelliğini "Users" olarak ayarlayın. TemplateField 'ın `ItemTemplate`, `UserNameLabel`adlı bir etiketin `Text` özelliğinde `Container.DataItem` veri bağlama ifadesinin değerini görüntüleyecek şekilde tanımlayın.

GridView eklendikten ve yapılandırıldıktan sonra, "role göre" arabiriminin bildirim temelli biçimlendirmesi aşağıdakine benzer olmalıdır:

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample12.aspx)]

`RoleList` DropDownList öğesini sistemdeki roller kümesiyle doldurmamız gerekir. Bunu gerçekleştirmek için `BindRolesToList` yöntemini, `Roles.GetAllRoles` yöntemi tarafından döndürülen dize dizisini `RolesList` DropDownList 'e (Ayrıca `UsersRoleList` Yineleyici) bağlayan şekilde güncelleştirin.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample13.cs)]

`BindRolesToList` yöntemi içindeki son iki satır, rol kümesini `RoleList` DropDownList denetimine bağlamak için eklenmiştir. Şekil 5 ' te, bir tarayıcıdan görüntülendiklerinde son sonuç gösterilir. bir açılan liste, sistem rolleriyle doldurulur.

[![roller RoleList DropDownList içinde görüntülenir](assigning-roles-to-users-cs/_static/image14.png)](assigning-roles-to-users-cs/_static/image13.png)

**Şekil 5**: roller `RoleList` DropDownList 'de görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image15.png))

### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>Seçili role ait olan kullanıcıları görüntüleme

Sayfa ilk yüklendiğinde veya `RoleList` DropDownList 'den yeni bir rol seçildiğinde, GridView 'da bu role ait olan kullanıcıların listesini görüntüliyoruz. Aşağıdaki kodu kullanarak `DisplayUsersBelongingToRole` adlı bir yöntem oluşturun:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample14.cs)]

Bu yöntem, seçili rolü `RoleList` DropDownList 'den alarak başlatılır. Daha sonra bu role ait olan kullanıcıların kullanıcı adlarının dize dizisini almak için [`Roles.GetUsersInRole(roleName)` yöntemini](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx) kullanır. Daha sonra bu dizi `RolesUserList` GridView 'a bağlanır.

Bu yöntemin iki durumda çağrılması gerekir: sayfa başlangıçta yüklendiğinde ve `RoleList` DropDownList içindeki seçili rol değiştiğinde. Bu nedenle, bu yöntemin `CheckRolesForSelectedUser`çağrısından sonra çağrılması için `Page_Load` olay işleyicisini güncelleştirin. Sonra, `RoleList``SelectedIndexChanged` olayı için bir olay işleyicisi oluşturun ve bu yöntemi buradan da çağırın.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample15.cs)]

Bu kodla birlikte `RolesUserList` GridView, seçili role ait olan kullanıcıları görüntülemelidir. Şekil 6 ' da gösterildiği gibi, süper vizörler rolü iki üyeden oluşur: deneme sürümü ve Tito.

[GridView ![seçili role ait olan kullanıcıları listeler](assigning-roles-to-users-cs/_static/image17.png)](assigning-roles-to-users-cs/_static/image16.png)

**Şekil 6**: GridView, seçili role ait olan kullanıcıları listeler ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image18.png))

### <a name="removing-users-from-the-selected-role"></a>Kullanıcılar seçili rolden kaldırılıyor

`RolesUserList` GridView 'ı, "Kaldır" düğmelerinin bir sütununu içerecek şekilde kullanalım. Belirli bir kullanıcı için "Kaldır" düğmesine tıklamak bu rolden kaldıracaktır.

GridView 'a bir Delete düğmesi alanı ekleyerek başlayın. Bu alanın en son dosyalanmış olarak görünmesini sağlayın ve `DeleteText` özelliğini "Sil" (varsayılan) olarak "Kaldır" olarak değiştirin.

[![ekleyin](assigning-roles-to-users-cs/_static/image20.png)](assigning-roles-to-users-cs/_static/image19.png)

**Şekil 7**: GridView 'A "Kaldır" düğmesini ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image21.png))

"Kaldır" düğmesine tıklandığında bir geri gönderme işlemi başarılı olur ve GridView 'un `RowDeleting` olayı tetiklenir. Bu olay için bir olay işleyicisi oluşturmalı ve Kullanıcı seçili rolden kaldıran kod yazmaktır. Olay işleyicisini oluşturun ve ardından aşağıdaki kodu ekleyin:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample16.cs)]

Kod, seçilen rol adı belirlenerek başlar. Daha sonra, kaldırılacak kullanıcının Kullanıcı adını öğrenmek için, "Kaldır" düğmesine tıklanan satırdan `UserNameLabel` denetimine programlı bir şekilde başvurur. Daha sonra Kullanıcı `Roles.RemoveUserFromRole` metoduna yapılan bir çağrı aracılığıyla rolden kaldırılır. `RolesUserList` GridView daha sonra yenilenir ve bir ileti `ActionStatus` etiketi denetimi aracılığıyla görüntülenir.

> [!NOTE]
> "Kaldır" düğmesi kullanıcıdan Kullanıcı kaldırılmadan önce herhangi bir onay sıralaması gerektirmez. Size bazı Kullanıcı onay düzeyi eklemenizi davet ediyorum. Bir eylemi onaylamaya yönelik en kolay yollarından biri, istemci tarafı onaylama iletişim kutusunu kullanmaktır. Bu teknik hakkında daha fazla bilgi için bkz. [silerken Istemci tarafı onaylama ekleme](https://asp.net/learn/data-access/tutorial-42-cs.aspx).

Şekil 8 ' de, kullanıcı denetimli gruptan kaldırıldıktan sonra sayfa görüntülenir.

[![alas, artık gözetmen yok](assigning-roles-to-users-cs/_static/image23.png)](assigning-roles-to-users-cs/_static/image22.png)

**Şekil 8**: alas, Tito artık bir gözetmen değil ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image24.png))

### <a name="adding-new-users-to-the-selected-role"></a>Yeni kullanıcılar seçili role ekleniyor

Kullanıcıları seçili rolden kaldırmanın yanı sıra, bu sayfaya ziyaretçi de seçili role bir Kullanıcı ekleyebilmelidir. Seçili role bir kullanıcı eklemek için en iyi arabirim, sahip olmasını istediğiniz kullanıcı hesabı sayısına bağlıdır. Web siteniz yalnızca birkaç düzine Kullanıcı hesabını veya daha az bir kullanıcı hesabı barındırabilir, burada bir DropDownList kullanabilirsiniz. Binlerce kullanıcı hesabı söz konusu olduğunda, ziyaretçilerin hesaplar arasında gezinmesine, belirli bir hesabı aramasına veya Kullanıcı hesaplarını başka bir şekilde filtrelemesine izin veren bir kullanıcı arabirimi eklemek istersiniz.

Bu sayfada, sistemdeki kullanıcı hesaplarının sayısından bağımsız olarak çalışacak çok basit bir arabirim kullanalım. Yani, ziyaretçiye, seçili role eklemek istediği kullanıcının Kullanıcı adını girmesini isteyen bir metin kutusu kullanacağız. Bu adı taşıyan bir kullanıcı yoksa veya Kullanıcı zaten rolün üyesiyse, `ActionStatus` etiketinde bir ileti görüntüleriz. Ancak kullanıcı varsa ve rolün bir üyesi değilse, bunları role ekleyecek ve Kılavuzu yeniletireceğiz.

GridView 'un altına bir TextBox ve düğme ekleyin. TextBox 'ın `ID` `UserNameToAddToRole` olarak ayarlayın ve düğmenin `ID` ve `Text` özelliklerini sırasıyla `AddUserToRoleButton` ve "Role Kullanıcı Ekle" olarak ayarlayın.

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample17.aspx)]

Sonra, `AddUserToRoleButton` için `Click` bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample18.cs)]

`Click` olay işleyicisindeki kodun çoğunluğu çeşitli doğrulama denetimleri gerçekleştirir. Ziyaretçi `UserNameToAddToRole` metin kutusuna bir Kullanıcı adı verilmesini, kullanıcının sistemde mevcut olduğunu ve bu kullanıcıların zaten seçili role ait olmamasını sağlar. Bu denetimlerden herhangi biri başarısız olursa, `ActionStatus` uygun bir ileti görüntülenir ve olay işleyicisine çıkış yapılır. Tüm denetimler başarılı olursa, Kullanıcı `Roles.AddUserToRole` yöntemi aracılığıyla role eklenir. Bunun ardından, TextBox 'ın `Text` özelliği temizlenir, GridView yenilenir ve `ActionStatus` etiketi belirtilen kullanıcının seçili role başarıyla eklendiğini belirten bir ileti görüntüler.

> [!NOTE]
> Belirtilen kullanıcının seçili role ait olmadığından emin olmak için, *Kullanıcı adının* *roleName*üyesi olup olmadığını gösteren bir Boole değeri döndüren [`Roles.IsUserInRole(userName, roleName)` yöntemini](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)kullanırız. Rol tabanlı yetkilendirmeye baktığımızda <a id="_msoanchor_2"> </a>, bu yöntemi [sonraki öğreticide](role-based-authorization-cs.md) yeniden kullanacağız.

Sayfayı bir tarayıcıdan ziyaret edin ve `RoleList` DropDownList ' den süper vizörler rolünü seçin. Geçersiz Kullanıcı adı girmeyi deneyin – kullanıcının sistemde mevcut olmadığını belirten bir ileti görmeniz gerekir.

[![var olmayan bir kullanıcıyı role ekleyemezsiniz](assigning-roles-to-users-cs/_static/image26.png)](assigning-roles-to-users-cs/_static/image25.png)

**Şekil 9**: var olmayan bir kullanıcıyı bir role ekleyemezsiniz ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image27.png))

Şimdi geçerli bir Kullanıcı eklemeyi deneyin. Devam edin ve Supervisors rolüne yeniden ekleyin.

[![Tito bir kez yeniden gözetmen!](assigning-roles-to-users-cs/_static/image29.png)](assigning-roles-to-users-cs/_static/image28.png)

**Şekil 10**: Tito bir gözetmen bir kez daha.  ([Tam boyutlu görüntüyü görüntülemek Için tıklayın](assigning-roles-to-users-cs/_static/image30.png))

## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>3\. Adım: "Kullanıcı tarafından" ve "role göre" arabirimleri için çapraz güncelleştirme

`UsersAndRoles.aspx` sayfası, kullanıcıları ve rolleri yönetmeye yönelik iki ayrı arabirim sunar. Şu anda, bu iki arabirim birbirinden bağımsız olarak davranır, böylece bir arabirimde yapılan bir değişiklik diğerinden hemen yansıtılmayacaktır. Örneğin, sayfa ziyaretçisinin, bu `RoleList` DropDownList 'den, kendi üyeleri olarak ve Tito ' ı listeleyen üst yöneticiler rolünü seçdiğine düşünün. Sonra ziyaretçi, `UsersRoleList` Yineleyici içindeki Yöneticiler ve ana bilgisayar onay kutularını denetleyen `UserList` DropDownList 'ten Tito seçer. Ziyaretçi daha sonra, bir Kullanıcı Yöneticisi rolünü yineleyicisi 'nden denetlediğinde, Tito, süper vizörler rolünden kaldırılır, ancak bu değişiklik "role göre" arabirimine yansıtılmaz. GridView, Gözeviziler rolünün bir üyesi olarak Tito 'ı göstermeye devam eder.

Bu hatayı onarmak için, bir rol her eklendiğinde veya `UsersRoleList` Yineleyici tarafından işaretlenmediğinde GridView 'ı yenilememiz gerekir. Benzer şekilde, bir kullanıcı kaldırıldığında veya "role göre" arabiriminden bir role eklendiğinde yineleyicisi yenilememiz gerekir.

"Kullanıcıya göre" arabirimindeki Yineleyici, `CheckRolesForSelectedUser` metodu çağırarak yenilenir. "Role göre" arabirimi `RolesUserList` GridView 'un `RowDeleting` olay işleyicisinde ve `AddUserToRoleButton` düğmesinin `Click` olay işleyicisinde değiştirilebilir. Bu nedenle, bu yöntemlerin her birinden `CheckRolesForSelectedUser` yöntemini çağırmanız gerekir.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample19.cs)]

Benzer şekilde, "role göre" arabirimindeki GridView `DisplayUsersBelongingToRole` yöntemi çağırarak yenilenir ve "Kullanıcı tarafından" arabirimi `RoleCheckBox_CheckChanged` olay işleyicisi aracılığıyla değiştirilir. Bu nedenle, bu olay işleyicisinden `DisplayUsersBelongingToRole` yöntemini çağırmanız gerekiyor.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample20.cs)]

Bu küçük kod değişiklikleriyle, "kullanıcıya göre" ve "role göre" arabirimleri artık yeniden güncelleştirme için doğru şekilde yapılır. Bunu doğrulamak için, sayfayı bir tarayıcıda ziyaret edin ve sırasıyla `UserList` ve `RoleList` DropDownLists ' i seçin. "Kullanıcı" arabirimindeki yineleyicisi 'nin "Kullanıcı" arabirimindeki yineleyicisi rolünü kaldırdıkça, Tito 'nın "role göre" arabirimindeki GridView 'dan otomatik olarak kaldırılacağını unutmayın. "Role göre" arabiriminden Supervisors rolüne TITO geri eklemek, "Kullanıcı tarafından" arabirimindeki Gözelebilirlik onay kutusunu otomatik olarak yeniden denetler.

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>4\. Adım: CreateUserWizard "rol belirt" adımını Içerecek şekilde özelleştirme

<a id="_msoanchor_3"> </a> [*Kullanıcı hesapları oluşturma*](../membership/creating-user-accounts-cs.md) öğreticisinde, CreateUserWizard Web denetiminin yeni bir kullanıcı hesabı oluşturmak için arabirim sağlamak üzere nasıl kullanılacağını gördük. CreateUserWizard denetimi iki şekilde kullanılabilir:

- Diğer bir deyişle, ziyaretçilerin sitede kendi Kullanıcı hesabını oluşturması ve
- Yöneticiler yeni hesaplar oluşturmak için bir yol olarak

İlk kullanım durumunda ziyaretçi siteye gönderilir ve CreateUserWizard, bu bilgileri siteye kaydolmak için bilgilerini girerek doldurur. İkinci durumda, yönetici başka bir kişi için yeni bir hesap oluşturur.

Bir hesap bir yönetici tarafından başka bir kişi için oluşturulduğunda, yöneticinin yeni kullanıcı hesabının ait olduğu rolleri belirtmesini sağlamak yararlı olabilir. <a id="_msoanchor_4"> </a> [ *Ek kullanıcı bilgilerini* depolama](../membership/storing-additional-user-information-cs.md) öğreticisinde, ek `WizardSteps`ekleyerek CreateUserWizard özelleştirmeyi nasıl özelleştireceğinizi gördük. Yeni kullanıcının rollerini belirtmek için CreateUserWizard 'e ek bir adım ekleme bölümüne bakalım.

`CreateUserWizardWithRoles.aspx` sayfasını açın ve `RegisterUserWithRoles`adlı bir CreateUserWizard denetimi ekleyin. Denetimin `ContinueDestinationPageUrl` özelliğini "~/default.aspx" olarak ayarlayın. Buradaki fikir bir yöneticinin yeni kullanıcı hesapları oluşturmak için bu CreateUserWizard denetimini kullanacağı için, denetimin `LoginCreatedUser` özelliğini false olarak ayarlayın. Bu `LoginCreatedUser` özelliği, ziyaretçinin otomatik olarak yeni oluşturulan kullanıcı olarak oturum açıp açmamadığını belirtir ve varsayılan olarak true değerini alır. Bir yönetici, hımself olarak oturum açdığımız yeni bir hesap oluşturduğunda, bu değeri false olarak ayarlayacağız.

Sonra, "Ekle/Kaldır `WizardSteps`..." öğesini seçin. CreateUserWizard 'in akıllı etiketinden ve yeni bir `WizardStep`ekleyerek `ID` `SpecifyRolesStep`olarak ayarlayarak. `SpecifyRolesStep WizardStep`, "yeni hesabınız için kaydolun" adımından sonra gelen, ancak "Tamam" adımından önce gelecek şekilde taşıyın. `WizardStep``Title` özelliğini "rolleri belirtin", `StepType` özelliğini `Step`ve `AllowReturn` özelliğini false olarak ayarlayın.

[![ekleyin](assigning-roles-to-users-cs/_static/image32.png)](assigning-roles-to-users-cs/_static/image31.png)

**Şekil 11**: "rolleri belirt" `WizardStep` CreateUserWizard ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image33.png))

Bu değişiklikten sonra, CreateUserWizard 'in bildirim temelli biçimlendirmesinin aşağıdaki gibi görünmesi gerekir:

[!code-aspx[Main](assigning-roles-to-users-cs/samples/sample21.aspx)]

"Rolleri belirtin" `WizardStep`, `RoleList`adlı bir CheckBoxList ekleyin. Bu CheckBoxList, kullanılabilir rolleri listeler ve yeni oluşturulan kullanıcının hangi rollere ait olduğunu denetlemek için sayfayı ziyaret eden kişiyi kontrol eder.

İki kodlama görevini doldurduk: ilk olarak `RoleList` CheckBoxList öğesini sistemdeki rollerle doldurmamız gerekir; İkinci olarak, Kullanıcı "rolleri belirt" adımından "Tamam" adımına geçerse oluşturulan kullanıcıyı seçili rollere eklememiz gerekiyor. `Page_Load` olay işleyicisindeki ilk görevi gerçekleştirebiliriz. Aşağıdaki kod programlı olarak sayfaya ilk ziyaretteki `RoleList` onay kutusuna başvurur ve sistemdeki rolleri buna bağlar.

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample22.cs)]

Yukarıdaki kod tanıdık gelmelidir. <a id="_msoanchor_5"> </a> [ *Ek kullanıcı bilgilerini* depolayan](../membership/storing-additional-user-information-cs.md) öğreticide, özel bir `WizardStep`içinden bir Web denetimine başvurmak için iki `FindControl` deyimi kullandık. Ve bu öğreticide, rolleri CheckBoxList 'e bağlayan kod alınmıştır.

İkinci programlama görevini gerçekleştirmek için "rol belirt" adımının tamamlandığını bilmemiz gerekiyor. CreateUserWizard bir `ActiveStepChanged` olayına sahip olduğunu anımsayın, bu, ziyaretçi bir adımdan diğerine her gittiğinde ateşlenir. Burada, kullanıcının "tamamlandı" adımına ulaşılmadığını tespit ettik. Bu durumda, kullanıcıyı seçili rollere eklememiz gerekiyor.

`ActiveStepChanged` olayı için bir olay işleyicisi oluşturun ve aşağıdaki kodu ekleyin:

[!code-csharp[Main](assigning-roles-to-users-cs/samples/sample23.cs)]

Kullanıcı "tamamlandı" adımına ulaştıysa, olay işleyicisi `RoleList` CheckBoxList öğelerini numaralandırır ve yalnızca oluşturulan Kullanıcı seçili rollere atanır.

Bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. CreateUserWizard ilk adımı, yeni kullanıcının Kullanıcı adı, parola, e-posta ve diğer anahtar bilgilerini isteyen standart "yeni hesabınızda kaydolma" adımsıdır. Wda adlı yeni bir kullanıcı oluşturmak için bilgileri girin.

[Wda adlı yeni bir kullanıcı oluşturmak ![](assigning-roles-to-users-cs/_static/image35.png)](assigning-roles-to-users-cs/_static/image34.png)

**Şekil 12**: wda adlı yeni bir kullanıcı oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image36.png))

"Kullanıcı Oluştur" düğmesine tıklayın. CreateUserWizard dahili olarak `Membership.CreateUser` yöntemini çağırır, Yeni Kullanıcı hesabını oluşturur ve sonraki adıma geçerek "rolleri belirt" i ilerler. Burada sistem rolleri listelenir. Supervizler onay kutusunu işaretleyin ve Ileri ' ye tıklayın.

[![, süper vizörlerin rolünün bir üyesini yapın](assigning-roles-to-users-cs/_static/image38.png)](assigning-roles-to-users-cs/_static/image37.png)

**Şekil 13**: wda ' ı süper vizörler rolünün bir üyesi yapın ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image39.png))

Ileri ' ye tıklamak geri göndermeye neden olur ve `ActiveStep` "Tamam" adımını güncelleştirir. `ActiveStepChanged` olay işleyicisinde, son oluşturulan kullanıcı hesabı, süper vizörler rolüne atanır. Bunu doğrulamak için `UsersAndRoles.aspx` sayfasına dönün ve `RoleList` DropDownList 'ten süper vizörleri seçin. Şekil 14 ' te gösterildiği gibi, üst yöneticiler artık üç kullanıcıdan oluşur: deneme sürümü, Tito ve wda.

[![Bruce, Tito ve wda tüm süper bilgisayarlar](assigning-roles-to-users-cs/_static/image41.png)](assigning-roles-to-users-cs/_static/image40.png)

**Şekil 14**: deneme tarafı, Tito ve wda tüm süper vizörler ([tam boyutlu görüntüyü görüntülemek için tıklayın](assigning-roles-to-users-cs/_static/image42.png))

## <a name="summary"></a>Özet

Rol çerçevesi, belirli bir role hangi kullanıcıların ait olduğunu belirlemek için belirli bir kullanıcının rolleri ve yöntemleri hakkındaki bilgileri almak için yöntemler sunar. Ayrıca, bir veya daha fazla kullanıcı için bir veya daha fazla rol eklemek ve kaldırmak için çeşitli yöntemler vardır. Bu öğreticide şu yöntemlerin yalnızca iki birine odaklanıyoruz: `AddUserToRole` ve `RemoveUserFromRole`. Tek bir role birden çok kullanıcı eklemek ve tek bir kullanıcıya birden çok rol atamak için tasarlanan ek çeşitler vardır.

Bu öğretici Ayrıca, yeni oluşturulan kullanıcının rollerini belirtmek için bir `WizardStep` dahil etmek üzere CreateUserWizard denetimini genişletmeye bir görünüm de eklenmiştir. Böyle bir adım, bir yöneticinin yeni kullanıcılar için Kullanıcı hesapları oluşturma sürecini kolaylaştırmaya yardımcı olabilir.

Bu noktada, rolleri oluşturma ve silme ve rollerden Kullanıcı ekleme ve kaldırma işlemlerinin nasıl yapıldığını gördünüz. Ancak rol tabanlı yetkilendirme uygulamak için henüz bakacağız. <a id="_msoanchor_6"> </a> [Aşağıdaki öğreticide](role-based-authorization-cs.md) , rol rol temelinde URL Yetkilendirme kuralları tanımlamayı ve şu anda oturum açmış olan kullanıcının rollerine göre sayfa düzeyi işlevselliğinin nasıl sınırlandıralınacağını inceleyeceğiz.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET Web sitesi yönetim aracına genel bakış](https://msdn.microsoft.com/library/ms228053.aspx)
- [ASP 'yi İnceleme. NET 'in üyelik, roller ve profil](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Kendi web sitesi yönetim aracınızı toplama](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler...

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni bir Murphy idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) bir satır bırakın

> [!div class="step-by-step"]
> [Önceki](creating-and-managing-roles-cs.md)
> [İleri](role-based-authorization-cs.md)
