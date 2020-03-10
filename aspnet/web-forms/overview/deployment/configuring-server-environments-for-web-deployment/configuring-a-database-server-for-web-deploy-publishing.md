---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
title: Web Dağıtımı yayımlama için bir veritabanı sunucusunu yapılandırma | Microsoft Docs
author: jrjlee
description: Bu konuda, Web dağıtımı ve yayımlamayı desteklemek üzere SQL Server 2008 R2 veritabanı sunucusunun nasıl yapılandırılacağı açıklanmaktadır. Bu konuda açıklanan görevler Co...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: e7c447f9-eddf-4bbe-9f18-3326d965d093
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing
msc.type: authoredcontent
ms.openlocfilehash: ade3c1ba1c470092f512436f39b8831458408c2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634619"
---
# <a name="configuring-a-database-server-for-web-deploy-publishing"></a>Bir Veritabanı Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, Web dağıtımı ve yayımlamayı desteklemek üzere SQL Server 2008 R2 veritabanı sunucusunun nasıl yapılandırılacağı açıklanmaktadır.
> 
> Bu konuda açıklanan görevler her dağıtım senaryosunda&#x2014;ortaktır, Web sunucularınızın IIS Web Dağıtım aracı (Web dağıtımı) uzak Aracı hizmeti, Web dağıtımı işleyicisi veya çevrimdışı dağıtım ya da uygulamanızın tek bir Web sunucusunda veya bir sunucu grubunda çalışıyor olması için yapılandırılmış olup olmadığı önemi yoktur. Veritabanını dağıtmanın yolu, güvenlik gereksinimlerine ve diğer noktalara göre değişebilir. Örneğin, veritabanını örnek verilerle veya olmayan bir şekilde dağıtabilir ve Kullanıcı rolü eşlemelerini dağıtabilir veya dağıtımdan sonra el ile yapılandırabilirsiniz. Ancak, veritabanı sunucusunu yapılandırdığınız Yöntem aynı kalır.

Web dağıtımını desteklemek üzere bir veritabanı sunucusunu yapılandırmak için ek ürün veya araç yüklemenize gerek yoktur. Veritabanı sunucunuzun ve Web sunucunuzun farklı makinelerde çalıştığı kabul edildiğinde, şunları yapmanız yeterlidir:

- SQL Server TCP/IP kullanarak iletişim kurmasına izin verme.
- Tüm güvenlik duvarları üzerinden SQL Server trafiğe izin verin.
- Web sunucusu makine hesabına SQL Server bir oturum açma hakkı verin.
- Makine hesabı oturum açma bilgilerini gerekli veritabanı rolleriyle eşleyin.
- SQL Server bir oturum açma ve veritabanı Oluşturucu izinleri için dağıtımı çalıştıracak hesaba izin verin.
- Yineleme dağıtımlarını desteklemek için, dağıtım hesabı oturum açma bilgilerini **db\_Owner** veritabanı rolüyle eşleyin.

Bu konu, bu yordamların her birini nasıl gerçekleştirekullanacağınızı gösterir. Bu konudaki görevler ve izlenecek yollar, Windows Server 2008 R2 üzerinde çalışan bir SQL Server 2008 R2 varsayılan örneğiyle başladığınızı varsayar. Devam etmeden önce aşağıdakileri doğrulayın:

- Windows Server 2008 R2 Service Pack 1 ve tüm kullanılabilir güncelleştirmeler yüklendi.
- Sunucu etki alanına katılmış.
- Sunucunun statik bir IP adresi vardır.
- SQL Server 2008 R2 Service Pack 1 ve tüm kullanılabilir güncelleştirmeler yüklendi.

SQL Server örneği yalnızca, herhangi bir SQL Server yüklemesinde otomatik olarak dahil edilen **Database Engine Services** rolünü içermelidir. Ancak, yapılandırma ve bakım kolaylığı için **Yönetim Araçları – temel** ve **Yönetim Araçları – tüm** sunucu rolleri dahil etmenizi öneririz.

> [!NOTE]
> Bilgisayarları etki alanına katma hakkında daha fazla bilgi için bkz. [bilgisayarları etki alanına katma ve oturum açma](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Statik IP adreslerini yapılandırma hakkında daha fazla bilgi için bkz. [STATIK IP adresi yapılandırma](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx). SQL Server yükleme hakkında daha fazla bilgi için bkz. [SQL Server 2008 R2 'Yi yükleme](https://technet.microsoft.com/library/bb500395.aspx).

## <a name="enable-remote-access-to-sql-server"></a>SQL Server uzaktan erişimi etkinleştir

SQL Server uzak bilgisayarlarla iletişim kurmak için TCP/IP kullanır. Veritabanı sunucunuz ve Web sunucunuz farklı makinelerinizde şunları yapmanız gerekir:

- TCP/IP üzerinden iletişime izin vermek için SQL Server ağ ayarlarını yapılandırın.
- SQL Server örneğinin kullandığı bağlantı noktalarında TCP trafiğine (ve bazı durumlarda Kullanıcı Datagram Protokolü (UDP) trafiğine) izin vermek için herhangi bir donanım veya yazılım güvenlik duvarı yapılandırın.

SQL Server TCP/IP üzerinden iletişim kurmak üzere etkinleştirmek için SQL Server Yapılandırma Yöneticisi kullanarak SQL Server örneğinizin ağ yapılandırmasını değiştirin.

**SQL Server TCP/IP kullanarak iletişim kurmak üzere etkinleştirmek için**

1. **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft SQL Server 2008 R2**' ye tıklayın, **yapılandırma araçları**' a ve ardından **SQL Server Yapılandırma Yöneticisi**' ye tıklayın.
2. Ağaç görünümü bölmesinde **SQL Server ağ yapılandırması**' nı genişletin ve ardından **MSSQLSERVER protokolleri**' ne tıklayın.

   > [!NOTE]
   > Birden çok SQL Server örneği yüklediyseniz, her örnek için<em>[örnek adı]</em> öğesi <strong>için bir protokoller</strong>görürsünüz. Örnek temelinde ağ ayarlarını yapılandırmanız gerekir.
3. Ayrıntılar bölmesinde **TCP/IP** satırına sağ tıklayın ve ardından **Etkinleştir**' e tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image1.png)
4. **Uyarı** Iletişim kutusunda **Tamam**' a tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image2.png)
5. Yeni ağ yapılandırmanızın etkili olabilmesi için MSSQLSERVER hizmetini yeniden başlatmanız gerekir. Bunu, bir komut isteminde, hizmetler konsolundan veya SQL Server Management Studio ' den yapabilirsiniz. Bu yordamda SQL Server Management Studio kullanacaksınız.
6. SQL Server Yapılandırma Yöneticisi’ni kapatın.
7. **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft SQL Server 2008 R2**' ye ve ardından **SQL Server Management Studio**' e tıklayın.
8. **Sunucuya Bağlan** iletişim kutusunda, **sunucu adı** kutusuna veritabanı sunucusunun adını yazın ve ardından **Bağlan**' a tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image3.png)
9. **Nesne Gezgini** bölmesinde, üst sunucu düğümüne (örneğin, **TESTDB1**) sağ tıklayın ve ardından **Yeniden Başlat**' a tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image4.png)
10. **Microsoft SQL Server Management Studio** Iletişim kutusunda **Evet**' e tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image5.png)
11. Hizmet yeniden başlatıldığında SQL Server Management Studio kapatın.

Bir güvenlik duvarı üzerinden SQL Server trafiğe izin vermek için, önce SQL Server örneğinizin kullandığı bağlantı noktalarını bilmeniz gerekir. Bu, SQL Server örneğinin nasıl oluşturulduğuna ve yapılandırıldığına bağlıdır:

- SQL Server *varsayılan örneği* , TCP bağlantı noktası 1433 ' deki istekleri dinler (ve yanıt verir).
- Adlandırılmış bir SQL Server *örneği* , dinamik olarak atanan TCP bağlantı noktasındaki istekleri dinler (ve yanıt verir).
- SQL Server Browser hizmeti etkinleştirilmişse istemciler, belirli bir SQL Server örneği için hangi TCP bağlantı noktasının kullanılacağını öğrenmek üzere UDP bağlantı noktası 1434 ' de hizmeti sorgulayabilir. Ancak, bu hizmet genellikle güvenlik nedenleriyle devre dışıdır.

SQL Server varsayılan bir örneğini kullandığınızı varsayarsak, güvenlik duvarınızı trafiğe izin verecek şekilde yapılandırmanız gerekir.

| Yön | Bağlantı noktasından | Bağlantı noktası | Bağlantı noktası türü |
| --- | --- | --- | --- |
| Gelen | Herhangi biri | 1433 | TCP |
| Giden | 1433 | Herhangi biri | TCP |

> [!NOTE]
> Teknik olarak, bir istemci bilgisayar SQL Server ile iletişim kurmak için 1024 ile 5000 arasında rastgele atanan bir TCP bağlantı noktası kullanır ve güvenlik duvarı kurallarınızı uygun şekilde kısıtlayabilirsiniz. SQL Server bağlantı noktaları ve güvenlik duvarları hakkında daha fazla bilgi için bkz. [bir güvenlik duvarı ÜZERINDEN SQL ile iletişim kurmak için gereken TCP/IP bağlantı noktası numaraları](https://go.microsoft.com/?linkid=9805125) ve [nasıl yapılır: belirli bir TCP bağlantı noktasını dinlemek üzere sunucu yapılandırma (SQL Server Yapılandırma Yöneticisi)](https://msdn.microsoft.com/library/ms177440.aspx).

Çoğu Windows Server ortamında, büyük olasılıkla veritabanı sunucusunda Windows Güvenlik Duvarı 'nı yapılandırmanız gerekecektir. Varsayılan olarak, bir kural özel olarak yasaklamadığı takdirde Windows Güvenlik Duvarı tüm giden trafiğe izin verir. Web sunucunuzun veritabanınıza ulaşmasını sağlamak için, SQL Server örneğinin kullandığı bağlantı noktası numarasında TCP trafiğine izin veren bir gelen kuralı yapılandırmanız gerekir. SQL Server varsayılan bir örneğini kullanıyorsanız, bu kuralı yapılandırmak için sonraki yordamı kullanabilirsiniz.

**Windows güvenlik duvarını varsayılan bir SQL Server örneğiyle iletişime izin verecek şekilde yapılandırmak için**

1. Veritabanı sunucusunda, **Başlat** menüsünde, **Yönetim Araçları**' nın üzerine gelin ve ardından **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı**' na tıklayın.
2. Ağaç görünümü bölmesinde **gelen kuralları**' na tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image6.png)
3. **Eylemler** bölmesinde, **gelen kuralları**altında **Yeni kural**' a tıklayın.
4. Yeni gelen kuralı sihirbazında, **kural türü** sayfasında, **bağlantı noktası**' nı seçin ve ardından **İleri**' ye tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image7.png)
5. **Protokol ve bağlantı noktaları** sayfasında, **TCP** ' nin seçili olduğundan emin olun ve **belirli yerel bağlantı noktaları** kutusunda **1433**yazın ve ardından **İleri**' ye tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image8.png)
6. **Eylem** sayfasında, **bağlantıya izin ver** ' i seçili bırakın ve **İleri**' ye tıklayın.
7. **Profil** sayfasında, **etki alanını** seçili bırakın, **özel** ve **genel** onay kutularını temizleyin ve ardından **İleri**' ye tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image9.png)
8. **Ad** sayfasında, kurala uygun şekilde açıklayıcı bir ad verin (örneğin, **varsayılan örnek SQL Server: ağ erişimi**) ve ardından **son**' a tıklayın.

SQL Server için Windows Güvenlik Duvarı 'nı yapılandırma hakkında daha fazla bilgi için, özellikle standart olmayan veya dinamik bağlantı noktaları üzerinden SQL Server ile iletişim oluşturmanız gerekiyorsa, bkz. [nasıl yapılır: veritabanı altyapısı Için Windows güvenlik duvarını yapılandırma](https://technet.microsoft.com/library/ms175043.aspx).

## <a name="configure-logins-and-database-permissions"></a>Oturum açmaları ve veritabanı Izinlerini yapılandırma

Bir Web uygulamasını Internet Information Services (IIS) uygulamasına dağıttığınızda, uygulama uygulama havuzunun kimliğini kullanarak çalışır. Bir etki alanı ortamında, uygulama havuzu kimlikleri ağ kaynaklarına erişmek için çalıştıkları sunucunun makine hesabını kullanır. Makine hesapları <em>[etki alanı adı]</em><strong>\</strong ><em>[makine adı]</em> <strong>$</strong> &#x2014;Örneğin, <strong>FABRIKAM\TESTWEB1 $</strong>. Web uygulamanızın bir veritabanına ağ üzerinden erişmesine izin vermek için şunları yapmanız gerekir:

- SQL Server örneğine Web sunucusu makine hesabı için bir oturum açma ekleyin.
- Makine hesabı oturum açma bilgilerini gerekli veritabanı rolleriyle eşleyin (genellikle **db\_DataReader** ve **DB\_DataWriter**).

Web uygulamanız tek bir sunucu yerine bir sunucu grubu üzerinde çalışıyorsa, sunucu grubundaki her Web sunucusu için bu yordamları tekrarlamanız gerekir.

> [!NOTE]
> Uygulama havuzu kimlikleri ve ağ kaynaklarına erişme hakkında daha fazla bilgi için bkz. [uygulama havuzu kimlikleri](https://go.microsoft.com/?linkid=9805123).

Bu görevlere çeşitli şekillerde yaklaşıtırabilirsiniz. Oturum açma bilgilerini oluşturmak için şunlardan birini yapabilirsiniz:

- Transact-SQL veya SQL Server Management Studio kullanarak veritabanı sunucusunda oturum açmayı el ile oluşturun.
- Oturum açma oluşturmak ve dağıtmak için Visual Studio 'da bir SQL Server 2008 sunucu projesi kullanın.

SQL Server oturum açma, veritabanı düzeyindeki bir nesne yerine sunucu düzeyindeki bir nesnedir, bu nedenle dağıtmak istediğiniz veritabanına bağlı değildir. Bu nedenle, oturum açmayı dilediğiniz zaman oluşturabilirsiniz ve en kolay yaklaşım, veritabanlarını dağıtmaya başlamadan önce oturum açma bilgilerini veritabanı sunucusunda el ile oluşturmak için kullanılır. SQL Server Management Studio bir oturum açma oluşturmak için sonraki yordamı kullanabilirsiniz.

**Web sunucusu makine hesabı için SQL Server oturum açma oluşturmak için**

1. Veritabanı sunucusunda, **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft SQL Server 2008 R2**' ye ve ardından **SQL Server Management Studio**' e tıklayın.
2. **Sunucuya Bağlan** iletişim kutusunda, **sunucu adı** kutusuna veritabanı sunucusunun adını yazın ve ardından **Bağlan**' a tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image10.png)
3. **Nesne Gezgini** bölmesinde, **güvenlik**' e sağ tıklayın, **Yeni**' nin üzerine gelin ve ardından **oturum aç**' a tıklayın.
4. **Oturum açma – yeni** iletişim kutusunda, **oturum açma adı** kutusuna Web sunucusu makine hesabınızın adını yazın (örneğin, **FABRIKAM\TESTWEB1 $** ).

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image11.png)
5. **Tamam**’a tıklayın.

Bu noktada, veritabanı sunucunuz Web Dağıtımı yayımlama için hazırlayın. Ancak, dağıttığınız tüm çözümler, makine hesabı oturum açma bilgilerini gerekli veritabanı rolleriyle eşleştirene kadar çalışmayacaktır. Veritabanını dağıtana kadar rolleri eşleyene kadar, oturum açmayı veritabanı rolleriyle eşlemek çok daha fazla düşünmelidir. Makine hesabı oturum açma bilgilerini gerekli veritabanı rolleriyle eşlemek için şunlardan birini yapabilirsiniz:

- Veritabanını ilk kez dağıttıktan sonra, veritabanı rollerini el ile oturum açmaya atayın.
- Veritabanı rollerini oturum açmaya atamak için dağıtım sonrası bir betik kullanın.

Oturum açma ve veritabanı rol eşlemelerinin oluşturulmasını otomatikleştirme hakkında daha fazla bilgi için bkz. [test ortamlarına veritabanı rolü üyelikleri dağıtma](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md). Alternatif olarak, makine hesabı oturum açma bilgilerini gerekli veritabanı rolleriyle el ile eşlemek için bir sonraki yordamı kullanabilirsiniz. Veritabanını *dağıtana kadar* bu yordamı gerçekleştireemiyorum unutmayın.

**Veritabanı rollerini Web sunucusu makine hesabı oturum açmayla eşlemek için**

1. SQL Server Management Studio önceki olarak açın.
2. **Nesne Gezgini** bölmesinde, **güvenlik** düğümünü genişletin, **oturum açmalar** düğümünü genişletin ve ardından makine hesabı oturum açma bilgilerini (örneğin, **FABRIKAM\TESTWEB1 $** ) çift tıklatın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image12.png)
3. **Oturum açma özellikleri** Iletişim kutusunda **Kullanıcı eşleme**' ye tıklayın.
4. **Bu oturum açmaya eşlenen kullanıcılar** tablosuna veritabanınızın adını (örneğin, **ContactManager**) seçin.
5. **Veritabanı rolü üyeliği:** *[veritabanı adı]* listesinde, gerekli izinleri seçin. Contact Manager örnek çözümü söz konusu olduğunda, **db\_DataReader** ve **DB\_DataWriter** rollerini seçmeniz gerekir.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image13.png)
6. **Tamam**’a tıklayın.

Veritabanı rollerini el ile eşleme, genellikle test ortamları için yeterli olduğundan, hazırlama veya üretim ortamlarında otomatik veya tek tıklamayla dağıtımlar için daha az tercih edilir. Bu tür bir görevi otomatikleştirme hakkında daha fazla bilgiyi, [veritabanı rolü üyeliklerini test ortamlarına dağıtma](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)bölümünde dağıtım sonrası betikleri kullanarak bulabilirsiniz.

> [!NOTE]
> Sunucu projeleri ve veritabanı projeleri hakkında daha fazla bilgi için bkz. [Visual Studio 2010 SQL Server veritabanı projeleri](https://msdn.microsoft.com/library/ff678491.aspx).

## <a name="configure-permissions-for-the-deployment-account"></a>Dağıtım hesabı için Izinleri yapılandırma

Dağıtımı çalıştırmak için kullanacağınız hesap SQL Server yönetici değilse, bu hesap için de bir oturum açma oluşturmanız gerekir. Veritabanını oluşturmak için, hesabın **dbcreator** sunucu rolünün bir üyesi olması veya eşdeğer izinlere sahip olması gerekir.

> [!NOTE]
> Bir veritabanını dağıtmak için Web Dağıtımı veya VSDBCMD kullandığınızda, Windows kimlik bilgilerini veya SQL Server kimlik bilgilerini (SQL Server Örneğiniz karma mod kimlik doğrulamasını destekleyecek şekilde yapılandırıldıysa) kullanabilirsiniz. Sonraki yordamda, Windows kimlik bilgilerini kullanmak istediğiniz varsayılır, ancak dağıtımı yapılandırırken bağlantı dizeniz SQL Server Kullanıcı adı ve parola belirtmekten dolayı hiçbir şey yapılmadı.

**Dağıtım hesabı için izinleri ayarlamak için**

1. SQL Server Management Studio önceki olarak açın.
2. **Nesne Gezgini** bölmesinde, **güvenlik**' e sağ tıklayın, **Yeni**' nin üzerine gelin ve ardından **oturum aç**' a tıklayın.
3. **Oturum açma – yeni** iletişim kutusunda, **oturum açma adı** kutusuna dağıtım hesabınızın adını yazın (örneğin, **FABRIKAM\matt**).
4. **Sayfa seç** bölmesinde, **sunucu rolleri**' ne tıklayın.
5. **Dbcreator**öğesini seçin ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image14.png)

Sonraki dağıtımları desteklemek için, ilk dağıtımdan sonra veritabanı **\_sahibi** rolüne dağıtım hesabını da eklemeniz gerekir. Bunun nedeni, sonraki dağıtımlarda yeni bir veritabanı oluşturmak yerine var olan bir veritabanının şemasını değiştirmekte olursunuz. Önceki bölümde açıklandığı gibi, bir veritabanı rolüne, daha belirgin nedenlerle veritabanını oluşturana kadar bir kullanıcı ekleyemezsiniz.

**Dağıtım hesabı oturum açma bilgilerini DB\_Owner veritabanı rolüyle eşlemek için**

1. SQL Server Management Studio önceki olarak açın.
2. **Nesne Gezgini** penceresinde **güvenlik** düğümünü genişletin, **oturum açmalar** düğümünü genişletin ve ardından makine hesabı oturum açma bilgilerini (örneğin, **FABRIKAM\matt**) çift tıklatın.
3. **Oturum açma özellikleri** Iletişim kutusunda **Kullanıcı eşleme**' ye tıklayın.
4. **Bu oturum açmaya eşlenen kullanıcılar** tablosuna veritabanınızın adını (örneğin, **ContactManager**) seçin.
5. **Veritabanı rolü üyeliği:** *[veritabanı adı]* listesinde, **DB\_Owner** rolünü seçin.

    ![](configuring-a-database-server-for-web-deploy-publishing/_static/image15.png)
6. **Tamam**’a tıklayın.

## <a name="conclusion"></a>Sonuç

Veritabanı sunucunuz artık uzak veritabanı dağıtımlarını kabul etmeye ve uzak IIS Web sunucularının veritabanlarınıza erişmesine izin verecek şekilde hazır olmalıdır. Veritabanlarını dağıtmayı ve kullanmayı denemeden önce şu anahtar noktalarını denetlemek isteyebilirsiniz:

- Uzak TCP/IP bağlantılarını kabul etmek için SQL Server yapılandırdınız mı?
- SQL Server trafiğe izin vermek için herhangi bir güvenlik duvarı yapılandırdınız mı?
- SQL Server erişecek her Web sunucusu için bir makine hesabı oturum açma oluşturmuş musunuz?
- Veritabanı dağıtımınız, Kullanıcı rolü eşlemeleri oluşturmak için bir komut dosyası içerir veya veritabanını ilk kez dağıttıktan sonra bunları el ile oluşturmanız gerekir mi?
- Dağıtım hesabı için bir oturum açma oluşturdunuz ve **dbcreator** sunucu rolüne eklediniz mi?

## <a name="further-reading"></a>Daha Fazla Bilgi

Veritabanı projelerini dağıtma hakkında yönergeler için bkz. [veritabanı projelerini dağıtma](../web-deployment-in-the-enterprise/deploying-database-projects.md). Dağıtım sonrası betiği çalıştırarak veritabanı rolü üyelikleri oluşturma konusunda rehberlik için bkz. [test ortamlarına veritabanı rolü üyelikleri dağıtma](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md). Veritabanlarının üyesi olduğu benzersiz dağıtım zorluklarının nasıl ele alınacağını gösteren yönergeler için bkz. [Üyelik veritabanlarını kurumsal ortamlara dağıtma](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).

> [!div class="step-by-step"]
> [Önceki](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
> [İleri](creating-a-server-farm-with-the-web-farm-framework.md)
