---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: Veri kaynağı denetimleri | Microsoft Docs
author: microsoft
description: ASP.NET 1. x içindeki DataGrid denetimi Web uygulamalarında veri erişiminde harika bir geliştirme olarak işaretlendi. Ancak, Kullanıcı kullanımı kolay değildi....
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639414"
---
# <a name="data-source-controls"></a>Veri Kaynağı Denetimleri

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 1. x içindeki DataGrid denetimi Web uygulamalarında veri erişiminde harika bir geliştirme olarak işaretlendi. Ancak, Kullanıcı kullanımı kolay değildi. Bu, bundan çok yararlı işlevselliği elde etmek için önemli miktarda kod de gerektirdi. Bu tür, 1. x içindeki tüm veri erişimi endeavors modelidir.

ASP.NET 1. x içindeki DataGrid denetimi Web uygulamalarında veri erişiminde harika bir geliştirme olarak işaretlendi. Ancak, Kullanıcı kullanımı kolay değildi. Bu, bundan çok yararlı işlevselliği elde etmek için önemli miktarda kod de gerektirdi. Bu tür, 1. x içindeki tüm veri erişimi endeavors modelidir.

ASP.NET 2,0, veri kaynağı denetimleriyle birlikte bunu ile ele alınmaktadır. ASP.NET 2,0 sürümündeki veri kaynağı denetimleri, geliştiricilere veri alma, verileri görüntüleme ve verileri düzenlemeyle ilgili bildirime dayalı bir model sağlar. Veri kaynağı denetimlerinin amacı, verilerin kaynağından bağımsız olarak veriye dayalı denetimlere verilerin tutarlı bir gösterimini sağlamaktır. ASP.NET 2,0 ' deki veri kaynağı denetimlerinin kalbi, DataSourceControl soyut sınıfıdır. DataSourceControl sınıfı, veri kaynağı denetimini bir veri kaynağı denetimi (yeni DataSourceID özelliği aracılığıyla) olarak atamanıza olanak sağlayan, IDataSource arabiriminin ve ISource arabiriminin temel bir uygulamasını sağlar. daha sonra açıklanmıştır) ve verileri bir liste olarak kullanıma sunar. Bir veri kaynağı denetiminden alınan her veri listesi bir DataSourceView nesnesi olarak sunulur. DataSourceView örneklerine erişim, IDataSource arabirimi tarafından sağlanır. Örneğin, GetViewNames yöntemi, belirli bir veri kaynağı denetimiyle ilişkili DataSourceViews öğelerinin numaralandırılacağını sağlayan bir ICollection döndürür ve GetView yöntemi, belirli bir DataSourceView örneğine ada göre erişmenizi sağlar.

Veri kaynağı denetimlerinde Kullanıcı arabirimi yoktur. Bunlar, bildirim temelli sözdizimini destekleyeceği ve isterseniz sayfa durumuna erişebilmeleri için sunucu denetimleri olarak uygulanır. Veri kaynağı denetimleri, hiçbir HTML işaretlemesini istemciye işlemez.

> [!NOTE]
> Daha sonra göreceğiniz gibi, veri kaynağı denetimleri kullanılarak da önbelleğe alma avantajları de mevcuttur.

## <a name="storing-connection-strings"></a>Bağlantı dizelerini depolama

Veri kaynağı denetimlerini nasıl yapılandıracağımızı öğrenmek için, ASP.NET 2,0 ' de bağlantı dizelerine ilişkin yeni bir özellik ele alınmalıdır. ASP.NET 2,0 yapılandırma dosyasında, çalışma zamanında dinamik olarak okunabilecek bağlantı dizelerini kolayca depolamanıza olanak tanıyan yeni bir bölüm sunar. &lt;connectionStrings&gt; bölümü, bağlantı dizelerini depolamayı kolaylaştırır.

Aşağıdaki kod parçacığı yeni bir bağlantı dizesi ekler.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;appSettings&gt; bölümünde olduğu gibi, &lt;connectionStrings&gt; bölümü yapılandırma dosyasındaki &lt;System. Web&gt; bölümünün dışında görünür.

Bu bağlantı dizesini kullanmak için, bir sunucu denetiminin ConnectionString özniteliğini ayarlarken aşağıdaki sözdizimini kullanabilirsiniz.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;connectionStrings&gt; bölümü, hassas bilgilerin açığa çıkmaması için de şifrelenebilir. Bu özellik sonraki bir modülde ele alınacaktır.

## <a name="caching-data-sources"></a>Veri kaynaklarını önbelleğe alma

Her DataSourceControl, önbelleğe almayı yapılandırmak için dört özellik sağlar; EnableCaching, CacheDuration, CacheExpirationPolicy ve CacheKeyDependency.

## <a name="enablecaching"></a>EnableCaching

EnableCaching, veri kaynağı denetimi için önbelleğe almanın etkin olup olmadığını belirleyen bir Boolean özelliktir.

## <a name="cacheduration-property"></a>CacheDuration özelliği

CacheDuration özelliği, önbelleğin geçerli kaldığı saniye sayısını ayarlar. Bu özelliğin **0** olarak ayarlanması, açıkça geçersiz kılınana kadar Önbelleğin geçerli kalmasına neden olur.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy özelliği

CacheExpirationPolicy özelliği **mutlak** ya da **kayan**olarak ayarlanabilir. Mutlak olarak ayarlamak, verilerin önbelleğe alınması için geçmesi gereken en uzun süreyi, CacheDuration özelliği tarafından belirtilen saniye sayısıdır. Her işlem gerçekleştirilirken sona erme saati, kayan olarak ayarlanarak sıfırlanır.

## <a name="cachekeydependency-property"></a>CacheKeyDependency özelliği

CacheKeyDependency özelliği için bir dize değeri belirtilmişse, ASP.NET bu dizeye dayalı olarak yeni bir önbellek bağımlılığı ayarlar. Bu, yalnızca CacheKeyDependency değiştirerek veya kaldırarak önbelleği açıkça geçersiz kılabilmeniz için izin verir.

**Önemli**: kimliğe bürünme etkinleştirilmişse ve veri kaynağına erişim ve/veya veri içeriği istemci kimliğine dayanıyorsa, EnableCaching değeri false olarak ayarlanarak önbelleğe alma işleminin devre dışı bırakılması önerilir. Bu senaryoda önbelleğe alma etkinse ve verileri ilk olarak talep eden kullanıcı dışında bir Kullanıcı bir istek sorunu, veri kaynağına yetkilendirme zorlanmaz. Veriler yalnızca önbellekten sunulacaktır.

## <a name="the-sqldatasource-control"></a>SqlDataSource denetimi

SqlDataSource denetimi, bir geliştiricinin ADO.NET 'yi destekleyen herhangi bir ilişkisel veritabanında depolanan verilere erişmesine olanak tanır. System. Data. SqlClient sağlayıcısını, bir SQL Server veritabanına, System. Data. OleDb sağlayıcısına, System. Data. ODBC sağlayıcısına veya System. Data. OracleClient sağlayıcısına erişmek için Oracle 'a erişmek için kullanabilir. Bu nedenle, SqlDataSource yalnızca bir SQL Server veritabanındaki verilere erişmek için kullanılmaz.

SqlDataSource 'ı kullanabilmeniz için, ConnectionString özelliği için bir değer belirtmeniz ve bir SQL komutu veya saklı yordamı belirtmeniz yeterlidir. SqlDataSource denetimi, temel alınan ADO.NET mimarisiyle çalışmayı üstlenir. Bağlantıyı açar, veri kaynağını sorgular veya saklı yordamı yürütür, verileri döndürür ve sonra bağlantıyı kapatır.

> [!NOTE]
> DataSourceControl sınıfı bağlantıyı sizin için otomatik olarak kapattığı için, veritabanı bağlantıları sızdırarak oluşturulan müşteri çağrılarının sayısını azaltmalıdır.

Aşağıdaki kod parçacığı, yukarıda gösterildiği gibi yapılandırma dosyasında depolanan bağlantı dizesini kullanarak bir DropDownList denetimini bir SqlDataSource denetimine bağlar.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

Yukarıda gösterildiği gibi, SqlDataSource 'un DataSourceMode özelliği veri kaynağı için modu belirtir. Yukarıdaki örnekte, DataSourceMode, DataReader olarak ayarlanır. Bu durumda, SqlDataSource salt ileri ve salt okunurdur imleç kullanarak bir IDataReader nesnesi döndürür. Döndürülen belirtilen nesne türü, kullanılan sağlayıcı tarafından denetlenir. Bu durumda, Web. config dosyasının &lt;connectionStrings&gt; bölümünde belirtilen System. Data. SqlClient sağlayıcısını kullanıyorum. Bu nedenle, döndürülen nesne SqlDataReader türünde olacaktır. Veri kümesinin DataSourceMode değerini belirterek, veriler sunucudaki bir veri kümesinde depolanabilir. Bu mod sıralama, sayfalama vb. gibi özellikler eklemenize olanak tanır. Bir GridView denetimine SqlDataSource veri bağladım, veri kümesi modunu seçtim. Ancak, bir DropDownList söz konusu olduğunda, DataReader modu doğru seçimdir.

> [!NOTE]
> Bir SqlDataSource veya bir AccessDataSource önbelleğe alırken, DataSourceMode özelliği DataSet olarak ayarlanmalıdır. DataReader 'ın bir DataSourceMode 'u olan önbelleğe almayı etkinleştirirseniz bir özel durum oluşur.

## <a name="sqldatasource-properties"></a>SqlDataSource özellikleri

Aşağıda SqlDataSource denetiminin bazı özellikleri verilmiştir.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

Parametrelerden biri null olduğunda bir SELECT komutunun iptal edilip edilmeyeceğini belirten bir Boole değeri. Varsayılan olarak true.

### <a name="conflictdetection"></a>ConflictDetection

Birden çok kullanıcının aynı anda bir veri kaynağını güncelleştirilebileceği bir durumda, ConflictDetection özelliği SqlDataSource denetiminin davranışını belirler. Bu özellik ConflictOptions numaralandırması değerlerinden biri olarak değerlendirilir. Bu değerler, **CompareAllValues** ve **OverwriteChanges**değerleridir. OverwriteChanges olarak ayarlandıysa veri kaynağına veri yazılacak son kişi önceki değişikliklerin üzerine yazar. Ancak, ConflictDetection özelliği CompareAllValues olarak ayarlandıysa, SelectCommand tarafından döndürülen sütunlar için oluşturulan Parametreler, Ayrıca, SqlDataSource 'un bir yandan da bu sütunların her birinde orijinal değerleri tutmak için oluşturulur. SelectCommand 'in yürütülmesinden bu yana değerlerin değiştirilip değiştirilmediğini belirleme.

### <a name="deletecommand"></a>DeleteCommand

Veritabanından satırlar silinirken kullanılan SQL dizesini ayarlar veya alır. Bu, bir SQL sorgusu ya da bir saklı yordam adı olabilir.

### <a name="deletecommandtype"></a>DeleteCommandType

Delete komutunun türünü, bir SQL sorgusu (metin) veya saklı yordam (StoredProcedure) olarak ayarlar veya alır.

### <a name="deleteparameters"></a>DeleteParameters

SqlDataSource denetimiyle ilişkili SqlDataSourceView nesnesinin DeleteCommand 'i tarafından kullanılan parametreleri döndürür.

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

Bu özellik, ConflictDetection özelliğinin CompareAllValues olarak ayarlandığı durumlarda özgün değer parametrelerinin biçimini belirtmek için kullanılır. Varsayılan değer {0}, özgün değer parametrelerinin özgün parametreyle aynı adı alacak olması anlamına gelir. Diğer bir deyişle, alan adı ÇalışanNo ise, özgün değer parametresi @EmployeeID.

### <a name="selectcommand"></a>Döndürmeyen

Veritabanından veri almak için kullanılan SQL dizesini ayarlar veya alır. Bu, bir SQL sorgusu ya da bir saklı yordam adı olabilir.

### <a name="selectcommandtype"></a>SelectCommandType

Select komutunun türünü, bir SQL sorgusu (metin) ya da bir saklı yordam (StoredProcedure) olarak ayarlar veya alır.

### <a name="selectparameters"></a>SelectParameters

SqlDataSource denetimiyle ilişkili SqlDataSourceView nesnesinin SelectCommand 'i tarafından kullanılan parametreleri döndürür.

### <a name="sortparametername"></a>SortParameterName

Veri kaynağı denetimi tarafından alınan verileri sıralarken kullanılan bir saklı yordam parametresinin adını alır veya ayarlar. Yalnızca SelectCommandType, StoredProcedure olarak ayarlandığında geçerlidir.

### <a name="sqlcachedependency"></a>SqlCacheDependency

SQL Server önbellek bağımlılığında kullanılan veritabanlarını ve tabloları belirten noktalı virgülle ayrılmış bir dize. (SQL önbellek bağımlılıkları sonraki bir modülde ele alınacaktır.)

### <a name="updatecommand"></a>Geçirildiğinde

Veritabanındaki veriler güncelleştirilirken kullanılan SQL dizesini ayarlar veya alır. Bu, bir SQL sorgusu ya da bir saklı yordam adı olabilir.

### <a name="updatecommandtype"></a>UpdateCommandType

Bir SQL sorgusu (metin) veya saklı yordam (StoredProcedure) güncelleştirme komutunun türünü ayarlar veya alır.

### <a name="updateparameters"></a>UpdateParameters

SqlDataSource denetimiyle ilişkili SqlDataSourceView nesnesinin UpdateCommand 'i tarafından kullanılan parametreleri döndürür.

## <a name="the-accessdatasource-control"></a>AccessDataSource denetimi

AccessDataSource denetimi SqlDataSource sınıfından türetilir ve bir Microsoft Access veritabanına veri bağlamak için kullanılır. AccessDataSource denetimi için ConnectionString özelliği salt okunurdur. ConnectionString özelliğini kullanmak yerine, veri dosyası özelliği aşağıda gösterildiği gibi Access veritabanına işaret etmek için kullanılır.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

Bu AccessDataSource, her zaman temel SqlDataSource 'un ProviderName öğesini System. Data. OleDb olarak ayarlar ve Microsoft. Jet. OLEDB. 4.0 OLE DB sağlayıcısını kullanarak veritabanına bağlanır. Parola korumalı bir Access veritabanına bağlanmak için AccessDataSource denetimini kullanamazsınız. Parola korumalı bir veritabanına bağlanmanız gerekiyorsa, SqlDataSource denetimini kullanmanız gerekir.

> [!NOTE]
> Web sitesi içinde depolanan erişim veritabanlarının App\_veri dizinine yerleştirilmesi gerekir. ASP.NET bu dizindeki dosyaların taranmasına izin vermez. Access veritabanlarını kullanırken, uygulama\_veri dizinine işlem hesabına okuma ve yazma izinleri vermeniz gerekir.

## <a name="the-xmldatasource-control"></a>XmlDataSource denetimi

XmlDataSource, veri bağlama denetimlerine XML verisi bağlamak için kullanılır. Veri dosyası özelliğini kullanarak bir XML dosyasına bağlanabilir veya veri özelliğini kullanarak bir XML dizesine bağlayabilirsiniz. XmlDataSource XML özniteliklerini bağlanabilir alanlar olarak kullanıma sunar. Öznitelik olarak temsil edilmeyen değerlere bağlamanız gereken durumlarda, bir XSL dönüşümü kullanmanız gerekir. Ayrıca, XML verilerini filtrelemek için XPath ifadelerini de kullanabilirsiniz.

Aşağıdaki XML dosyasını göz önünde bulundurun:

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

XmlDataSource 'un yalnızca &lt;kişi&gt; düğümlerine filtre uygulamak için *kişilerin/kişinin* XPath özelliğini kullandığına dikkat edin. DropDownList daha sonra DataTextField özelliğini kullanarak LastName özniteliğine veri bağlar.

XmlDataSource denetimi öncelikle salt okuma XML verilerine veri bağlama için kullanıldığında, XML veri dosyasını düzenlemek mümkündür. Bu gibi durumlarda, XML dosyasındaki bilgilerin otomatik olarak eklenmesi, güncelleştirilmesi ve silinmesinin diğer veri kaynağı denetimleriyle yaptığı şekilde otomatik olarak gerçekleşmediğini unutmayın. Bunun yerine, XmlDataSource denetiminin aşağıdaki yöntemlerini kullanarak verileri el ile düzenlemek için kod yazmanız gerekir.

### <a name="getxmldocument"></a>GetXmlDocument

XmlDataSource tarafından alınan XML kodunu içeren bir XmlDocument nesnesi alır.

### <a name="save"></a>Kaydet

Bellek içi XmlDocument 'ı veri kaynağına geri kaydeder.

Save yönteminin yalnızca aşağıdaki iki koşul karşılandığında çalışabileceğinizin farkında olmanız gerekir:

1. XmlDataSource, bellek içi XML verilerine bağlanacak veri özelliği yerine bir XML dosyasına bağlamak için veri dosyası özelliğini kullanıyor.
2. Transform veya TransformFile özelliği aracılığıyla hiçbir dönüşüm belirtilmedi.

Ayrıca, Save yönteminin birden çok kullanıcı tarafından aynı anda çağrıldığında beklenmedik sonuçlara neden olabileceğini unutmayın.

## <a name="the-objectdatasource-control"></a>ObjectDataSource denetimi

Bu noktaya kadar katdığımız veri kaynağı denetimleri, veri kaynağı denetiminin doğrudan veri deposuyla iletişim kurduğu iki katmanlı uygulamalar için mükemmel seçimlerdir. Ancak, birçok gerçek dünya uygulaması, veri katmanıyla iletişim kuran bir iş nesnesiyle iletişim kurması gerekebilecek çok katmanlı uygulamalardır. Bu durumlarda, ObjectDataSource, faturayı tamamen doldurur. ObjectDataSource, kaynak nesneyle birlikte çalışarak. ObjectDataSource denetimi, kaynak nesnenin bir örneğini oluşturur, belirtilen yöntemini çağırır ve nesne örneğini tek bir isteğin kapsamı içinde Dispose, çünkü nesneniz statik Yöntemler (Visual Basic içinde paylaşılır) yerine örnek yöntemlerine sahiptir. Bu nedenle, nesnenizin durum bilgisiz olmalıdır. Diğer bir deyişle, nesneniz tek bir isteğin yayılması dahilinde tüm gerekli kaynakları almalıdır ve serbest bırakmalıdır. ObjectDataSource denetiminin ObjectCreated olayını işleyerek kaynak nesnesinin nasıl oluşturulduğunu kontrol edebilirsiniz. Kaynak nesnenin bir örneğini oluşturabilir ve ardından ObjectDataSourceEventArgs sınıfının ObjectInstance özelliğini bu örneğe ayarlayabilirsiniz. ObjectDataSource denetimi, kendi üzerinde bir örnek oluşturmak yerine ObjectCreated olayında oluşturulan örneği kullanacaktır.

Bir ObjectDataSource denetimi için kaynak nesne, verileri almak ve değiştirmek için çağrılabilecek ortak statik Yöntemler (Visual Basic içinde paylaşılır) ortaya çıkardığı takdirde, bir ObjectDataSource denetimi bu yöntemleri doğrudan çağırır. Bir ObjectDataSource denetiminin Yöntem çağrıları yapmak için kaynak nesnenin bir örneğini oluşturması gerekiyorsa, nesne hiçbir parametre alan bir ortak Oluşturucu içermelidir. Bu Oluşturucu, kaynak nesnenin yeni bir örneğini oluşturduğunda, ObjectDataSource denetimi tarafından çağracaktır.

Kaynak nesne, parametresiz bir ortak Oluşturucu içermiyorsa, Objectcreate olayında ObjectDataSource denetimi tarafından kullanılacak kaynak nesnenin bir örneğini oluşturabilirsiniz.

## <a name="specifying-object-methods"></a>Nesne yöntemlerini belirtme

Bir ObjectDataSource denetimi için kaynak nesne, verileri seçmek, eklemek, güncelleştirmek veya silmek için kullanılan herhangi bir sayıda yöntemi içerebilir. Bu yöntemler, ObjectDataSource denetiminin SelectMethod, InsertMethod, UpdateMethod ya da DeleteMethod özelliği kullanılarak tanımlandığı şekilde, ObjectDataSource denetimi tarafından çağrılır. Kaynak nesne Ayrıca, veri kaynağındaki toplam nesne sayısının sayısını döndüren SelectCountMethod özelliğini kullanarak ObjectDataSource denetimi tarafından tanımlanan isteğe bağlı bir SelectCount yöntemi de içerebilir. Bir Select yöntemi, sayfalama sırasında kullanılmak üzere veri kaynağındaki toplam kayıt sayısını almak için çağrıldıktan sonra SelectCount yöntemini çağırır.

## <a name="lab-using-data-source-controls"></a>Veri kaynağı denetimlerini kullanan laboratuvar

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>Alıştırma 1-SqlDataSource denetimiyle verileri görüntüleme

Aşağıdaki alıştırmada, Northwind veritabanına bağlanmak için SqlDataSource denetimi kullanılmaktadır. SQL Server 2000 örneğindeki Northwind veritabanına erişiminizin olduğunu varsayar.

1. Yeni bir ASP.NET Web sitesi oluşturun.
2. Yeni bir Web. config dosyası ekleyin.

    1. Çözüm Gezgini ' de projeye sağ tıklayın ve yeni öğe Ekle ' ye tıklayın.
    2. Şablonlar listesinden Web yapılandırma dosyası ' nı seçin ve Ekle ' ye tıklayın.
3. &lt;connectionStrings&gt; bölümünü aşağıdaki gibi düzenleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. Kod görünümüne geçin ve aşağıdaki gibi &lt;ASP: SqlDataSource&gt; denetimine bir ConnectionString özniteliği ve bir SelectCommand özniteliği ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. Tasarım görünümü, yeni bir GridView denetimi ekleyin.
6. GridView Tasks menüsündeki veri kaynağı seç açılan menüsünde SqlDataSource1 öğesini seçin.
7. Default. aspx ' e sağ tıklayın ve menüden tarayıcıda görüntüle ' yi seçin. Kaydetmek isteyip istemediğiniz sorulduğunda Evet ' e tıklayın.
8. GridView, Products tablosundaki verileri görüntüler.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>Alıştırma 2-SqlDataSource denetimiyle verileri düzenlemeyle

Aşağıdaki alıştırmada, bildirime dayalı sözdizimini kullanarak bir DropDownList denetimini nasıl bağlayacağınız ve DropDownList denetiminde sunulan verileri düzenlemenize izin verilen gösterilmektedir.

1. Tasarım görünümü ' de, GridView denetimini default. aspx konumundan silin. 

    **Önemli**: SqlDataSource denetimini sayfada bırakın.
2. Default. aspx ' e bir DropDownList denetimi ekleyin.
3. Kaynak görünümüne geçin.
4. &lt;ASP: DropDownList&gt; denetimine şu şekilde bir DataSourceID, DataTextField ve DataValueField özniteliği ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Default. aspx ' i kaydedin ve tarayıcıda görüntüleyin. DropDownList 'in Northwind veritabanındaki tüm ürünleri içerdiğini unutmayın.
6. Tarayıcıyı kapatın.
7. Default. aspx kaynak görünümünde, DropDownList denetiminin altına yeni bir TextBox denetimi ekleyin. TextBox 'ın ID özelliğini txtProductName olarak değiştirin.
8. TextBox denetimi altında yeni bir düğme denetimi ekleyin. Düğmenin ID özelliğini btnUpdate olarak, Text özelliğini ise **ürün adını güncelleştirmek**için değiştirin.
9. Default. aspx kaynak görünümünde, SqlDataSource etiketine aşağıdaki gibi bir UpdateCommand özelliği ve iki yeni UpdateParameters ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Bu koda iki güncelleştirme parametresi (ProductName ve ProductID) eklendiğini unutmayın. Bu parametreler, txtProductName TextBox 'ın metin özelliğine ve ddlProducts DropDownList 'in SelectedValue özelliğine eşlenir.
10. Tasarım görünümü geçin ve bir olay işleyicisi eklemek için düğme denetimine çift tıklayın.
11. Aşağıdaki kodu btnUpdate 'e ekleyin\_kod tıklayın: 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default. aspx öğesine sağ tıklayın ve tarayıcıda görüntülemeyi seçin. Tüm değişiklikleri kaydetmek isteyip istemediğiniz sorulduğunda Evet ' e tıklayın.
13. ASP.NET 2,0 kısmi sınıflar, çalışma zamanında derleme için izin verir. Kod değişikliklerinin etkili olması için bir uygulama oluşturmak gerekli değildir.
14. DropDownList 'ten bir ürün seçin.
15. Metin kutusuna seçili ürün için yeni bir ad girin ve ardından Güncelleştir düğmesine tıklayın.
16. Ürün adı veritabanında güncelleştirilir.

## <a name="exercise-3-using-the-objectdatasource-control"></a>Alıştırmalar denetimini kullanarak 3. alıştırma

Bu alıştırma, Northwind veritabanıyla etkileşim kurmak için ObjectDataSource denetimini ve kaynak nesnesini nasıl kullanacağınızı gösterir.

1. Çözüm Gezgini ' de projeye sağ tıklayın ve yeni öğe Ekle ' ye tıklayın.
2. Şablonlar listesinden Web formu ' nu seçin. Adı Object. aspx olarak değiştirin ve Ekle ' ye tıklayın.
3. Çözüm Gezgini ' de projeye sağ tıklayın ve yeni öğe Ekle ' ye tıklayın.
4. Şablonlar listesinden Class ' ı seçin. Sınıfın adını NorthwindData.cs olarak değiştirin ve Ekle ' ye tıklayın.
5. Sınıfı uygulama\_kodu klasörüne eklemek isteyip istemediğiniz sorulduğunda Evet ' e tıklayın.
6. Aşağıdaki kodu NorthwindData.cs dosyasına ekleyin: 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Aşağıdaki kodu Object. aspx kaynak görünümüne ekleyin: 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. Tüm dosyaları kaydedin ve Object. aspx 'e gözatamazsınız.
9. Ayrıntıları görüntüleyerek, çalışanları düzenleyerek, çalışanlar ekleyerek ve çalışanları silerek arabirimiyle etkileşime geçin.
