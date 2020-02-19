---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: Veri depolama seçenekleri (Azure ile gerçek dünyada bulut uygulamaları oluşturma) | Microsoft Docs
author: MikeWasson
description: Azure e-Book ile gerçek dünyada bulut uygulamaları oluşturma, Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. 13 desen ve şunları yapabilir...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 9357ed5aef39bed501cdac9ac26d46c884d4fae0
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457186"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>Veri depolama seçenekleri (Azure ile gerçek dünyada bulut uygulamaları oluşturma)

, [Mike te son](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Tom Dykstra](https://github.com/tdykstra) tarafından

[Onarma projesini indirin](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) veya [E-kitabı indirin](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-book **Ile gerçek dünyada bulut uygulamaları oluşturma** , Scott Guthrie tarafından geliştirilen bir sunuyu temel alır. Bulut için Web Apps 'i başarılı bir şekilde geliştirmeye yardımcı olabilecek 13 desen ve uygulamaları açıklar. E-kitap hakkında daha fazla bilgi için [ilk bölüme](introduction.md)bakın.

Çoğu kişi ilişkisel veritabanları için kullanılır ve bir bulut uygulaması tasarlarken diğer veri depolama seçeneklerini çok daha fazla inceleyelim. [NoSQL](http://en.wikipedia.org/wiki/NoSQL) (ilişkisel olmayan) veritabanları, bazı görevleri ilişkisel veritabanlarından daha verimli bir şekilde işleyebildiğinden, sonuç en az performans, yüksek masraf veya daha kötü olabilir. Müşteriler önemli bir veri depolama sorununu çözmenize yardımcı olmak için, bu genellikle NoSQL seçeneklerinden birinin daha iyi çalıştığı ilişkisel bir veritabanına sahip olduğu için. Bu durumlarda, uygulamayı üretime dağıtmaya başlamadan önce NoSQL çözümünü uyguladıysanız, müşteri daha iyi bir şekilde kapalıdır.

Diğer taraftan, bir NoSQL veritabanının her şeyi de ve yeterince iyi yapabildiği varsayımında de bir hata olabilir. Tüm veri depolama görevleri için tek bir en iyi veri yönetimi seçimi yoktur; farklı veri yönetimi çözümleri farklı görevler için iyileştirilmiştir. Çoğu gerçek dünyada bulut uygulamalarının çeşitli veri depolama gereksinimleri vardır ve genellikle birden çok veri depolama çözümünün bir birleşimiyle en iyi şekilde sunulur.

Bu bölümün amacı, bir bulut uygulaması tarafından kullanılabilen veri depolama seçenekleri hakkında daha geniş bir fikir sahibi olmak ve senaryonuza uygun olanları seçme hakkında bazı temel kılavuzumuzu sağlamaktır. Size sunulan seçenekleri bilmeniz ve bir uygulama geliştirmeden önce güçlü ve zayıf yönleri hakkında düşünün. Bir üretim uygulamasındaki veri depolama seçeneklerini değiştirmek, düzlem uçuş sırasında bir Jet motorunu değiştirmek gibi son derece zor olabilir.

## <a name="data-storage-options-on-azure"></a>Azure 'da veri depolama seçenekleri

Bulut, çeşitli ilişkisel ve NoSQL veri depolarının kullanımını nispeten kolaylaştırır. Azure 'da kullanabileceğiniz bazı veri depolama platformları aşağıda verilmiştir.

![](data-storage-options/_static/image1.png)

Tabloda dört tür NoSQL veritabanı gösterilmektedir:

- [Anahtar/değer veritabanları](https://msdn.microsoft.com/library/dn313285.aspx#sec7) her anahtar değeri için tek bir seri hale getirilmiş nesne depolar. Belirli bir anahtar değeri için bir öğe almak istediğiniz büyük hacimde verilerin depolanması ve öğenin diğer özelliklerine göre sorgu yapmanız gerekmez.

    [Azure Blob depolama](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/) , dosya ve dosya adlarına karşılık gelen anahtar değerleriyle bulutta dosya depolama gibi işlev gören bir anahtar/değer veritabanıdır. Dosya içeriğindeki değerleri arayarak değil, klasör ve dosya adına göre bir dosya alırsınız.

    [Azure Tablo Depolaması](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/) Ayrıca bir anahtar/değer veritabanıdır. Her değere bir *varlık* (bir bölüm anahtarı ve satır anahtarı tarafından tanımlanan bir satıra benzer) ve birden çok *özellik* (sütunlara benzer ancak tablodaki tüm varlıkların aynı sütunları paylaşması gerekmez) olarak adlandırılır. Anahtar dışındaki sütunlarda sorgulama son derece verimsiz olur ve kaçınılmalıdır. Örneğin, tek bir kullanıcı hakkında bilgi depolayan bir bölümle Kullanıcı profili verilerini saklayabilirsiniz. Kullanıcı adı, Parola karması, Doğum tarihi vb. gibi verileri, bir varlığın ayrı özelliklerinde veya aynı bölümdeki ayrı varlıklarda saklayabilirsiniz. Ancak belirli bir Doğum tarihi aralığına sahip tüm kullanıcıları sorgulamak istemezsiniz ve profil tablonuz ile başka bir tablo arasında bir JOIN sorgusu çalıştıramazsınız. Tablo depolama, ilişkisel bir veritabanından daha ölçeklenebilir ve daha pahalıdır, ancak karmaşık sorguları veya birleştirmeleri etkinleştirmez.
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8) , değerleri *Belgeler*olan anahtar/değer veritabanlarıdır. Burada "belge" sözcük veya Excel belgesi açısından kullanılmaz, ancak bir alt belge olabilecek adlandırılmış alanlar ve değerler koleksiyonu anlamına gelir. Örneğin, bir sipariş geçmişi tablosunda sipariş belgesi sipariş numarası, sipariş tarihi ve müşteri alanları olabilir; ve müşteri alanında ad ve adres alanları bulunabilir. Veritabanı, alan verilerini XML, YAML, JSON veya BSON; gibi bir biçimde kodlar. ya da düz metin kullanabilir. Anahtar/değer veritabanlarından ayrı olarak belge veritabanlarını ayarlayan bir özellik, anahtar olmayan alanları sorgulama ve sorgu kullanımını daha verimli hale getirmek için ikincil dizinler tanımlama olanağıdır. Bu özellik bir belge veritabanını, ölçütlere göre verileri alması gereken uygulamalar için belge anahtarı değerinden daha karmaşık hale getirir. Örneğin, bir satış siparişi geçmişi belge veritabanında ürün KIMLIĞI, müşteri KIMLIĞI, müşteri adı vb. gibi çeşitli alanlarda sorgulama yapabilirsiniz. [MongoDB](http://www.mongodb.org/) , popüler bir belge veritabanıdır.
- [Sütun ailesi veritabanları](https://msdn.microsoft.com/library/dn313285.aspx#sec9) , veri depolamayı sütun aileleri adlı ilgili sütunların koleksiyonlarına yapınızı sağlayan anahtar/değer veri depolarıdır. Örneğin, bir görselleştirmenizdeki veritabanında bir kişinin adı (ilk, orta, son), kişi adresi için bir grup ve kişinin profil bilgileri (DOB, cinsiyet vb.) için bir grup sütun grubu olabilir. Veritabanı daha sonra her bir sütun ailesini ayrı bir bölümde saklayabilir, bu arada aynı anahtarla ilgili tüm verileri bir kişi için tutun. Daha sonra tüm ad ve adres bilgilerini de okumak zorunda kalmadan tüm profil bilgilerini okuyabilirsiniz. [Cassandra](http://cassandra.apache.org/) popüler bir sütun ailesi veritabanıdır.
- [Grafik veritabanları](https://msdn.microsoft.com/library/dn313285.aspx#sec10) , bir nesne ve ilişki koleksiyonu olarak bilgi depolar. Grafik veritabanının amacı, bir uygulamanın nesne ağını ve bunlar arasındaki ilişkileri engelleyen sorguları verimli bir şekilde gerçekleştirmesini sağlamaktır. Örneğin, nesneler insan kaynakları veritabanında çalışanlar olabilir ve "Scott için doğrudan veya dolaylı olarak çalışan tüm çalışanları bul" gibi sorguları kolaylaştırmak isteyebilirsiniz. [Neo4j](http://www.neo4j.org/) , popüler bir grafik veritabanıdır.

İlişkisel veritabanlarına kıyasla NoSQL seçenekleri, yapılandırılmamış verilerin depolanması ve çözümlenmesi için çok daha fazla ölçeklenebilirlik ve maliyet verimliliği sunar. Zorunluluğunu getirir, ilişkisel veritabanlarının zengin queryabilirlik ve sağlam veri bütünlüğü özelliklerini sağlamayadır. NoSQL, JOIN sorgularına gerek olmadan yüksek hacimle ilgili olan IIS günlük verileri için iyi çalışır. NoSQL, mutlak veri bütünlüğü gerektiren ve firmayla ilgili diğer verilerle birçok ilişki içeren bankacılık işlemleri için de çalışmayacaktır.

Bir NoSQL veritabanının ölçeklenebilirliğini, ilişkisel bir veritabanının queryabilirliği ve işlemsel bütünlüğüyle birleştiren [newsql](http://en.wikipedia.org/wiki/NewSQL) adlı yeni bir veritabanı platformu kategorisi de vardır. NewSQL veritabanları, genellikle "OldSQL" veritabanlarında uygulanması zor olan dağıtılmış depolama ve sorgu işleme için tasarlanmıştır. [Nuodb](http://www.nuodb.com/) , Azure 'da kullanılabilen bir newsql veritabanı örneğidir.

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop ve MapReduce

NoSQL veritabanlarında depoladığınız yüksek hacimde verilerin zamanında etkili bir şekilde analiz edilmesi zor olabilir. Bunu yapmak için, [MapReduce](http://en.wikipedia.org/wiki/MapReduce) Işlevlerini uygulayan [Hadoop](http://hadoop.apache.org/) gibi bir çerçeve kullanabilirsiniz. Aslında MapReduce işleminin ne olduğu aşağıda verilmiştir:

- Yalnızca gerçekten çözümlemeniz gereken verilerin veri deposu dışına seçim yaparak işlenmesi gereken verilerin boyutunu sınırlayın. Örneğin, Kullanıcı tabanınızı Doğum yılından daha sonra öğrenmek istiyorsunuz, bu nedenle Kullanıcı profili veri deponuzdan yalnızca Doğum yılından birini seçersiniz.
- Verileri parçalara ayırın ve işlenmek üzere farklı bilgisayarlara gönderin. Bilgisayar A, 1950-1959 tarih olan kişi sayısını, bilgisayar B 'yi 1960-1969, vb. hesaplar. Bu bilgisayar grubuna *Hadoop kümesi*denir.
- Parçaların üzerinde işleme yapıldıktan sonra her bölümün sonuçlarını bir araya getirin. Artık her bir Doğum yılı için kaç kişinin ve bu genel listedeki yüzdeleri hesaplama görevinin görece bir listesi vardır.

Azure 'da, [HDInsight](https://azure.microsoft.com/services/hdinsight/) , Hadoop gücünü kullanarak büyük verilerden yeni Öngörüler elde etmenizi, çözümlemenize ve bu yenilikleri almanıza olanak sağlar. Örneğin, Web sunucusu günlüklerini çözümlemek için kullanabilirsiniz:

- Depolama hesabınızda Web sunucusu günlüğünü etkinleştirin. Bu, Azure 'u uygulamanıza yönelik her HTTP isteği için günlükleri blob hizmetine yazacak şekilde ayarlar. Blob hizmeti temel olarak bulut dosya deposıdır ve HDInsight ile birlikte tümleştirilir.

    ![Blob depolamaya Günlükler](data-storage-options/_static/image2.png)
- Uygulama trafik aldığından, Web sunucusu IIS günlükleri blob depolamaya yazılır.

    ![Web sunucusu günlükleri](data-storage-options/_static/image3.png)
- Portalda, **yeni** - **veri hizmetleri** - **HDInsight** - **hızlı oluştur**' a tıklayın ve bir HDInsight küme adı, küme boyutu (HDInsight kümesi veri düğümü sayısı) ve HDInsight kümesi için bir Kullanıcı adı ve parola belirtin.

    ![HDInsight](data-storage-options/_static/image4.png)

Şimdi günlüklerinizi analiz etmek ve şu soruların yanıtlarını almak için MapReduce işlerini ayarlayabilirsiniz:

- Uygulamamın en fazla veya en az trafik aldığı gün sayısı nedir?
- Trafiğim hangi ülkelerde geliyor?
- Trafimin geldiği alanların ortalama komşu geliri nedir? (Size, IP adresine göre komşu gelir sağlayan genel bir veri kümesi vardır ve bunu Web sunucusu günlüklerindeki IP adresiyle eşleştirebilirsiniz.)
- Komşu gelir sitedeki belirli sayfalarla veya ürünlerle nasıl ilişkilendirimidir?

Daha sonra, bir müşterinin ilgilenme olasılığını veya belirli bir ürünü satın almasını sağlamak üzere reklamları hedeflemek için bunlar gibi soruların yanıtlarını kullanabilirsiniz.

[Her şeyi otomatikleştirin](automate-everything.md)bölümünde açıklandığı gibi, portalda yapabileceğiniz çoğu işlev otomatik hale getirilebilir ve bu da HDInsight analiz işlerini ayarlamayı ve yürütmeyi içerir. Tipik bir HDInsight betiği aşağıdaki adımları içerebilir:

- Bir HDInsight kümesi sağlayın ve BLOB depolama girişi için depolama hesabınıza bağlayın.
- MapReduce iş yürütülebilir dosyalarını (. jar veya. exe dosyaları) HDInsight kümesine yükleyin.
- Çıktı verilerini blob depolamaya depolayan bir MapReduce gönderebilirsiniz.
- İşin tamamlanmasını bekleyin.
- HDInsight kümesini silin.
- Blob depolamasındaki çıktıya erişin.

Tüm bunu yapan bir betiği çalıştırarak, HDInsight kümesinin sağlandığı süreyi en aza indirmiş olursunuz. Bu, maliyetlerinizi en aza indirir.

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>Hizmet olarak platform (PaaS) ve hizmet olarak altyapı (IaaS)

Daha önce listelenen veri depolama seçenekleri hem hizmet olarak platform (PaaS) hem de hizmet olarak altyapı (IaaS) çözümlerini içerir. PaaS, donanım ve yazılım altyapısını yönettiğimiz ve yalnızca hizmeti kullandığınız anlamına gelir. SQL veritabanı, Azure 'un PaaS özelliğidir. Veritabanları için sorun ve arka planda Azure kümeleri, VM 'Leri yapılandırır ve veritabanlarını ayarlar. VM 'lere doğrudan erişiminiz yok ve bunları yönetmek zorunda değilsiniz. IaaS, veri merkezi altyapımızda çalışan VM 'Leri ayarlamış, yapılandırmanıza ve yönetmenize ve bunlara istediğiniz her şeyi yerleştireceğiniz anlamına gelir. Ortak VM yapılandırmalarına yönelik önceden yapılandırılmış VM görüntülerinin galerisini sunuyoruz. Örneğin, Windows Server 2008, Windows Server 2012, BizTalk Server, Oracle WebLogic Server, Oracle Database vb. için önceden yapılandırılmış VM görüntülerini yükleyebilirsiniz.

Azure 'un sunduğu PaaS veri çözümleri şunlardır:

- Azure SQL veritabanı (eski adıyla SQL Azure). SQL Server temel alan bulut ilişkisel veritabanı.
- Azure Tablo depolaması. Bir anahtar/değer NoSQL veritabanı.
- Azure Blob depolama. Bulutta dosya depolama alanı.

IaaS için, bir sanal makineye yükleyebildiği her şeyi çalıştırabilirsiniz, örneğin:

- SQL Server, Oracle, MySQL, SQL Compact, SQLite veya Postgres gibi ilişkisel veritabanları.
- Memönbelleğe alınmış, Red, Cassandra ve Riak gibi anahtar/değer veri depoları.
- HBase gibi sütun veri depoları.
- MongoDB, Rayvendb ve Couşdb gibi belge veritabanları.
- Neo4j gibi grafik veritabanları.

![Azure 'da veri depolama seçenekleri](data-storage-options/_static/image5.png)

IaaS seçeneği neredeyse sınırsız miktarda veri depolama seçeneği sunar ve önceden yapılandırılmış görüntüleri kullanarak VM 'Ler oluşturabileceğiniz için çoğu daha kolay bir şekilde kullanılır. Örneğin, yönetim portalında **sanal makineler**' e gidin, **görüntüler** sekmesine tıklayın ve **VM deposu 'e**git ' e tıklayın.

![VM Deposuna Gözat](data-storage-options/_static/image6.png)

Daha sonra [yüzlerce önceden yapılandırılmış sanal makine](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)görüntüsünün listesini görürsünüz ve MongoDB, Neo4J, Red, Cassandra veya Couşdb gibi bir veritabanı yönetim sistemi önceden yüklenmiş bir görüntüden sanal makine oluşturabilirsiniz:

![VM 'de MongoDB deposu](data-storage-options/_static/image7.png)

Azure, IaaS veri depolama seçeneklerini mümkün olduğunca kolay hale getirir, ancak PaaS tekliflerinin birçok senaryo için daha uygun maliyetli ve pratik hale getiren birçok avantajı vardır:

- VM oluşturmanız gerekmez, yalnızca portalı veya bir komut dosyası kullanarak bir veri deposu kurabilirsiniz. 200 terabaytlık bir veri deposu istiyorsanız, yalnızca bir düğmeye tıklayabilir veya bir komut çalıştırabilir ve saniyeler içinde kullanabileceğiniz şekilde bu şekilde kullanılabilir.
- Hizmet tarafından kullanılan VM 'Leri yönetmeniz veya yama yapmanız gerekmez; Microsoft bunu sizin için otomatik olarak yapar.-altyapıyı ölçekleme veya yüksek kullanılabilirlik için ayarlama konusunda endişelenmeniz gerekmez; Microsoft, sizin için tüm bunları işler.
- Lisans satın almanız gerekmez; lisans ücretleri hizmet ücretlerine dahildir.
- Sadece kullandığınız kadar ödersiniz.

Azure 'daki PaaS veri depolama seçenekleri, üçüncü taraf sağlayıcıların tekliflerini içerir. Örneğin, bir hizmet olarak MongoDB veritabanı sağlamak için Azure Mağazası 'ndan [MongoLab eklentisini](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/) seçebilirsiniz.

## <a name="choosing-a-data-storage-option"></a>Veri depolama seçeneği seçme

Tüm senaryolar için hiç bir yaklaşım yok. Birisi bu teknolojinin yanıt olduğunu söyliyorsa, sorabileceğiniz ilk şey "soru nedir?" olarak kabul edilir çünkü farklı çözümler farklı şeyler için iyileştirilmiştir. İlişkisel modelin kesin avantajları vardır; Bu nedenle çok uzun süre içinde. Ancak SQL 'e bir NoSQL çözümüyle ilgili olarak da alt kenarlar de vardır.

Genellikle en iyi iş görtiğimiz, tek bir çözümde SQL ve NoSQL kullandığınız bir kompozisyon yaklaşımda. İnsanlar NoSQL 'i öğreniyor olsa da, çok sayıda farklı NoSQL çerçevesi kullandığının ne olduğunu fark ederseniz, bu [nesnelerin daha fazla](http://redis.io/)farklı NoSQL [çerçeveleri kullandığını](http://wiki.apache.org/couchdb/Introduction)öğrenirsiniz. [](http://basho.com/riak/) NoSQL kullanan Facebook bile, hizmetin farklı parçaları için farklı NoSQL çerçeveleri kullanır. Veri depolama yaklaşımlarının karıştırilmesi ve eşleşmesi, birden çok veri çözümü kullanmak ve bunları tek bir uygulamada bütünleştirmek için oldukça iyi bir uygulamadır.

Bir yaklaşım seçerken göz önünde bulundurabileceğiniz bazı sorular aşağıda verilmiştir:

| Veri anlam | -Temel veri depolama ve veri erişimi anlam nedir (ilişkisel veya yapılandırılmamış verileri depoluyor?)? Medya dosyaları gibi yapılandırılmamış veriler, blob depolamada en iyi şekilde uyum verir; Ürünler, envanterler, tedarikçiler, müşteri siparişleri vb. gibi ilgili verilerin bir koleksiyonu, ilişkisel bir veritabanında en iyi şekilde uyar. |
| --- | --- |
| Sorgu desteği | -Verileri sorgulamak için ne kadar kolay? -Ne tür soruların etkin olarak sorulabileceği? Anahtar/değer veri depoları, önemli bir değer verilen ancak karmaşık sorgular için uygun olmayan tek bir satır almak için çok uygundur. Her zaman belirli bir kullanıcı için veri aldığınız bir kullanıcı profili veri deposu için bir anahtar/değer veri deposu iyi çalışabilir; çeşitli ürün özniteliklerine göre farklı gruplandırmalar almak istediğiniz ürün kataloğu için, ilişkisel bir veritabanının daha iyi bir şekilde çalışmasını sağlayabilirsiniz. NoSQL veritabanları, büyük hacimlerinizi verimli bir şekilde saklayabilir, ancak veritabanını uygulamanın verileri nasıl sorguladığı ve bu da geçici sorguların daha zor hale getirebileceği şekilde yapısal olarak oluşturmanız gerekir. İlişkisel bir veritabanı sayesinde neredeyse her türlü sorgu oluşturabilirsiniz. |
| İşlevsel projeksiyon | -Sorular, toplamalar vb. olabilir, sunucu tarafı yürütülürler? SQL 'deki bir tablodan SELECT COUNT (\*) öğesini çalıştırdım, sunucudaki tüm işleri etkili bir şekilde işler ve aradığım sayıyı döndürür. Toplamayı desteklemeyen bir NoSQL veri deposundan aynı hesaplamayı istersem, bu verimsiz bir "sınırsız sorgu" ve muhtemelen zaman aşımına uğrar. Sorgu başarılı olsa bile sunucudan istemciye tüm verileri almam ve istemcideki satırları saymalıyım. -Hangi diller veya ifade türleri kullanılabilir? İlişkisel bir veritabanı ile SQL 'i kullanabilirsiniz. Azure Tablo depolaması gibi bazı NoSQL veritabanlarında, [OData](http://www.odata.org/)kullanıyorum ve tek yapacağım, birincil anahtar üzerinde filtrelenebilir ve tahminleri alabilir (kullanılabilir alanların bir alt kümesini seçin). |
| Ölçeklenebilirlik kolaylığı | -Verilerin ne sıklıkta ve ne kadar ölçeklendirilmesi gerekir? -Platform, ölçeği yerel olarak uygular mi? -Kapasite ekleme/kaldırma işlemi ne kadar kolay (boyut ve üretilen iş)? İlişkisel veritabanları ve tablolar, ölçeklenebilir hale getirmek için otomatik olarak bölümlenmez, bu sayede belirli sınırlamaların ötesinde ölçeklendirilmesi zordur. Azure Tablo depolama, her şeyi Azure Table Storage ve bölüm ekleme için neredeyse hiçbir sınır olmadığı gibi NoSQL veri depoları. Tablo depolama alanını 200 terabayta kadar kolayca ölçeklendirebilirsiniz, ancak Azure SQL veritabanı için en fazla veritabanı boyutu 500 gigabayttır. İlişkisel verileri birden çok veritabanına bölümleyerek ölçeklendirebilirsiniz, ancak bu modeli desteklemek için bir uygulama ayarlamak çok sayıda programlama işi içerir. |
| İzleme ve yönetilebilirlik | -Ne kadar kolay bir şekilde işaretleme, izleme ve yönetme platformu? Veri mağazalarınızın sistem durumu ve performansı hakkında bilgi sahibi olmanız gerekir. bu nedenle, bir platformun size ücretsiz olarak size verdiği ölçümleri ve kendinizi geliştirmek için gerekenleri bilmeniz gerekir. |
| İşlemler | -Azure 'da dağıtım ve çalıştırma platformu ne kadar kolay? PaaS? IaaS? Linux? Tablo depolama ve SQL veritabanı, Azure 'da kolayca ayarlanabilir. Yerleşik Azure PaaS çözümleri olmayan platformlar daha fazla çaba gerektirir. |
| API desteği | -Platformla çalışmayı kolaylaştıran bir API var mı? Azure Tablo hizmetinde, .NET API 'SI olan ve .NET 4,5 zaman uyumsuz programlama modelini destekleyen bir SDK vardır. Bir .NET uygulaması yazıyorsanız, API veya daha az kapsamlı bir tane olmayan başka bir anahtar/değer sütunu veri deposu platformuna kıyasla Azure Tablo hizmeti için kod yazmak ve test etmek çok daha kolay olacaktır. |
| İşlem bütünlüğü ve veri tutarlılığı | -Platformun veri tutarlılığını güvence altına almak için işlemleri desteklemesi kritik öneme sahip mi? Gönderilen toplu e-postaların izlenmesi için performans ve düşük veri depolama maliyeti, veri platformundaki işlemler veya başvuru bütünlüğü için otomatik destekten daha önemli olabilir, böylece Azure Tablo hizmeti iyi bir seçimdir. Banka hesabı bakiyelerinin veya satın alma siparişlerinin izlenmesi için, güçlü işlem garantisi sağlayan bir ilişkisel veritabanı platformu daha iyi bir seçimdir. |
| İş sürekliliği | -Yedekleme, geri yükleme ve olağanüstü durum kurtarma ne kadar kolay? Daha erken veya daha sonraki üretim verileri bozulmuş olur ve geri alma işlevine ihtiyacınız olacaktır. İlişkisel veritabanları genellikle zaman içindeki bir noktaya geri yükleme özelliği gibi daha ayrıntılı geri yükleme özelliklerine sahiptir. Göz önünde bulundurmanız gereken her platformda hangi geri yükleme özelliklerinin kullanılabildiğini anlamak, dikkate alınması gereken önemli bir faktördür. |
| Maliyet | -Birden fazla platform veri iş yükünüzü destekleyebileceğinden, maliyetleri nasıl karşılaştırırsınız? Örneğin, ASP.NET Identity kullanıyorsanız, Kullanıcı profili verilerini Azure Tablo hizmeti veya Azure SQL veritabanı 'nda saklayabilirsiniz. SQL veritabanı 'nın zengin sorgulama özelliklerine ihtiyacınız yoksa, belirli bir depolama alanı için maliyeti çok daha az olduğu için Azure tabloları kısmen tercih edebilirsiniz. |

Veri depolama çözümlerinizi seçmeden önce, bu kategorilerin her birinde soruların yanıtını bilmeniz genellikle önerilir.

Ayrıca, iş yükünüz bazı platformların diğerlerinden daha iyi destekleyebileceğini belirli gereksinimlere sahip olabilir. Örneğin:

- Uygulamanız denetim özellikleri gerektiriyor mu?
- Veri lontçekimi gereksinimleriniz nelerdir? otomatik arşivleme veya temizleme özellikleri mi gerekiyor?
- Özelleştirilmiş güvenlik gereksinimleriniz var mı? Örneğin, veriler PII (kişisel olarak tanımlanabilir bilgiler) içerir, ancak PII 'nin sorgu sonuçlarından dışlandığından emin olmanız gerekir.
- Yasal düzenlemeler veya teknolojik nedenlerle bulutta depolanabilecek bazı verileriniz varsa, şirket içi depolamayla tümleştirmeyi kolaylaştıran bir bulut veri depolama platformuna ihtiyacınız olabilir.

## <a name="demo--using-sql-database-in-azure"></a>Demo – Azure 'da SQL veritabanı 'nı kullanma

BT BT uygulaması, görevleri depolamak için ilişkisel bir veritabanı kullanır. [Her şeyi otomatikleştirin](automate-everything.md) bölümünde gösterilen ortam oluşturma Windows PowerShell BETIĞI Iki SQL veritabanı örneği oluşturur. Bunları portalda **SQL veritabanları** sekmesine tıklayarak görebilirsiniz.

![Portalda SQL veritabanları](data-storage-options/_static/image8.png)

Ayrıca Portal kullanarak veritabanı oluşturmak da kolaydır.

**Yeni--veri hizmetleri** -- **SQL veritabanı** -- **hızlı oluştur**' a tıklayın, bir veritabanı adı girin, hesabınızda zaten bulunan bir sunucuyu seçin veya yeni bir tane oluşturun ve **SQL veritabanı oluştur**' a tıklayın.

![Yeni SQL Veritabanı](data-storage-options/_static/image9.png)

Birkaç saniye bekleyin ve Azure 'da kullanabileceğiniz bir veritabanınız var.

![Yeni SQL veritabanı oluşturuldu](data-storage-options/_static/image10.png)

Böylece Azure, şirket içi ortamda bir gün veya hafta veya daha uzun sürebilir. Bir komut dosyasında veya bir yönetim API 'SI kullanarak veritabanlarını otomatik olarak kolayca oluşturabileceğiniz için, uygulamanız bu şekilde programlandığı sürece verilerinizi birden çok veritabanına dağıtarak dinamik olarak ölçeklendirebilirsiniz.

Bu, hizmet olarak platform modelimize bir örnektir. Sunucuları yönetmeniz gerekmez, biz bunu yaptık. Yedeklemeler hakkında endişelenmeniz gerekmez. Yüksek kullanılabilirlik ile çalışıyor. veritabanındaki veriler otomatik olarak üç sunucu arasında çoğaltılır. Bir makine olursa otomatik olarak yük devreder ve veri kaybettik. Sunucu düzenli olarak düzeltme eki uygulanıyorsa, bu konuda endişelenmeniz gerekmez.

Bir düğmeye tıklayın ve ihtiyacınız olan tam bağlantı dizesini alın ve yeni veritabanını hemen kullanmaya başlayabilirsiniz.

![Bağlantı dizeleri](data-storage-options/_static/image11.png)

Pano, bağlantı geçmişi ve kullanılan depolama alanı miktarını gösterir.

![SQL veritabanı panosu](data-storage-options/_static/image12.png)

Portaldaki veritabanlarını veya SQL Server Management Studio (SSMS) ve Visual Studio Araçları SQL Server Nesne Gezgini (SSOX) ve Sunucu Gezgini dahil, zaten bildiğiniz SQL Server araçları kullanarak yönetebilirsiniz.

![SSOX](data-storage-options/_static/image13.png)

Fiyatlandırma modeli daha iyi bir şeydir. Ücretsiz 20 MB 'lik bir veritabanıyla geliştirme başlatabilir ve bir üretim veritabanı ayda yaklaşık $5 ile başlar. En fazla kapasiteyi değil yalnızca veritabanında depoladığınız veri miktarı için ödeme yaparsınız. Lisans satın almanız gerekmez.

SQL veritabanı kolayca Ölçeklendirilecek. BT BT uygulaması için, Otomasyon betiğimizde oluşturduğumuz veritabanı 1 GB 'a göre belirlenir. Bu süreyi 150 GB 'a kadar ölçeklendirmek istiyorsanız, portala gidip bu ayarı değiştirebilir veya bir REST API komutu yürütebilir ve saniyeler içinde veri dağıtabileceğiniz 150 GB veritabanınıza sahip olursunuz.

![SQL veritabanı sürümleri ve boyutları](data-storage-options/_static/image14.png)

Bu, bulutun gücünü hızlı ve kolay bir şekilde oluşturup hemen kullanmaya başlayabilmenizi sağlar.

BT BT uygulaması, biri üyelik (kimlik doğrulama ve yetkilendirme) ve bir veri için olmak üzere iki SQL veritabanı kullanır ve bunu sağlamak ve ölçeklendirmek için yapmanız gerekir. Windows PowerShell betikleri aracılığıyla veritabanlarının nasıl sağlanacağı hakkında daha fazla gördünüz ve artık portalda ne kadar kolay olması gerektiğini de gördünüz.

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>ADO.NET kullanarak doğrudan veritabanı erişimine karşı Entity Framework

BT BT uygulaması, .NET uygulamaları için Microsoft 'un önerdiği ORM (nesne ilişkisel Eşleyici) Entity Framework kullanarak bu veritabanlarına erişir. ORM, geliştirici üretkenliğini kolaylaştıran harika bir araçtır ancak verimlilik, bazı senaryolarda performansın düşürülme masrafına gelir. Gerçek dünyada bir bulut uygulamasında EF kullanma veya doğrudan ADO.NET kullanma arasında seçim yapmayacaksınız. her ikisini de kullanabilirsiniz. Veritabanıyla birlikte çalışarak, en yüksek performans elde etmek önemli değildir ve Entity Framework ile elde ettiğiniz Basitleştirilmiş kodlama ve testlerin avantajlarından yararlanabilirsiniz. EF yükünün kabul edilemez performansa neden olduğu durumlarda, saklı yordamları çağırarak ADO.NET kullanarak kendi sorgularınızı yazabilir ve çalıştırabilirsiniz.

Veritabanına erişmek için hangi yöntemi kullanırsanız kullanın, "azaltmaya" öğesini mümkün olduğunca en aza indirmek istersiniz. Diğer bir deyişle, ihtiyacınız olan tüm verileri onlarca veya yüzlerce daha küçük bir sorgu sonuç kümesinde elde edebilirsiniz, bu genellikle tercih edilir. Örneğin, öğrencileri ve kaydolduğu kursları listeetmeniz gerekiyorsa, tek bir sorgudaki öğrencileri almak ve her öğrencinin Kursu için ayrı sorgular yürütmek yerine tek bir JOIN sorgusunda tüm verilerin alınması daha iyidir.

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>SQL veritabanları ve BT BT uygulamasındaki Entity Framework

BT BT uygulamasını onarma bölümünde, Entity Framework `DbContext` sınıfından türetilen `FixItContext` sınıfı, veritabanını tanımlar ve veritabanındaki tabloları belirtir. Bağlam, görevler için bir varlık kümesi (tablo) belirtir ve kod, bağlantı dizesi adının bağlamına geçirilir. Bu ad, Web. config dosyasında tanımlanan bir bağlantı dizesine başvurur.

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

*Web. config* dosyasındaki bağlantı dizesi appdb olarak adlandırılır (burada yerel geliştirme veritabanına işaret edilir):

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

Entity Framework, `FixItTask` varlık sınıfına dahil olan özellikleri temel alan bir *Fixittasks* tablosu oluşturur. Bu basit bir POCO (düz eski CLR nesnesi) sınıfıdır ve bu, Entity Framework hiçbir bağımlılığı olmadığı anlamına gelir. Bununla birlikte, bunu temel alan bir tablo oluşturmayı ve ile CRUD (oluşturma-okuma-güncelleştirme-silme) işlemlerini nasıl yürüteceğini Entity Framework.

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks tablosu](data-storage-options/_static/image15.png)

BT BT uygulaması, veri deposuyla çalışan CRUD işlemleri için kullandığı bir depo arabirimi içerir.

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

Depo yöntemlerinin tümünün zaman uyumsuz olduğuna ve tüm veri erişiminin tamamen zaman uyumsuz bir şekilde yapılabilmesini unutmayın.

Depo uygulama, LINQ sorguları ve INSERT, Update ve DELETE işlemleri de dahil olmak üzere verilerle çalışacak Entity Framework zaman uyumsuz Yöntemler çağırır. Bu, bir düzelme görevi aramaya yönelik koda bir örnek aşağıda verilmiştir.

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

Burada ayrıca, daha sonra [izleme ve telemetri](monitoring-and-telemetry.md)bölümünde yer alan bir zamanlama ve hata günlüğü kodu görürsünüz.

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>Azure 'da SQL veritabanı (PaaS) ve VM 'de SQL Server (IaaS) seçme

SQL Server ve Azure SQL veritabanı ile ilgili iyi bir şey, her ikisi için de temel programlama modelinin aynı olmasıdır. Her iki ortamda da aynı becerilerin çoğunu kullanabilirsiniz. Geliştirme ve bulutta bulunan bir SQL veritabanı örneği olan bir SQL Server veritabanı da kullanabilirsiniz.

Alternatif olarak, IaaS VM 'lerine yükleyerek şirket içinde çalıştırdığınız bulutta aynı SQL Server çalıştırabilirsiniz. Bazı eski uygulamalarda, bir VM 'de SQL Server çalıştırmak daha iyi bir çözüm olabilir. Bir SQL Server veritabanı ayrılmış bir VM üzerinde çalıştığı için, bu, paylaşılan bir sunucuda çalışan SQL veritabanı veritabanından daha fazla kaynağa sahip olur. Bu, bir SQL Server veritabanının daha büyük olabileceği ve yine de devam ettiği anlamına gelir. Genel olarak, veritabanı boyutu ve tablo boyutu ne kadar küçükse, SQL veritabanı (PaaS) için daha iyi kullanım durumu kullanılır.

İki model arasından seçim yapma hakkında bazı yönergeler aşağıda verilmiştir.

| Azure SQL Veritabanı (PaaS) | Bir sanal makinede SQL Server (IaaS) |
| --- | --- |
| **Profesyonelleri** -VM 'leri oluşturmanız veya yönetmeniz, işletim SISTEMINI veya SQL 'i güncelleştirmeyi veya düzeltme ekini almak zorunda değilsiniz; Azure bunu sizin için yapar. -Veritabanı düzeyinde SLA ile yerleşik yüksek kullanılabilirlik. -Toplam sahip olma maliyeti (TCO), yalnızca kullandığınız kadar ödeyin (lisans gerekmez). -Çok sayıda daha küçük veritabanını (&lt;= 500 GB) işlemek için iyi. -Ölçeği genişletmek için dinamik olarak yeni veritabanları oluşturmak kolaydır. | ***Profesyonelleri*** -şirket içi SQL Server uyumlu. -VM düzeyi SLA ile 2 + VM 'lerde [AlwaysOn aracılığıyla SQL Server yüksek kullanılabilirliği](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx) uygulayabilir. -SQL 'in yönetilme konusunda tam denetiminiz vardır. -Zaten sahip olduğunuz SQL lisanslarını yeniden kullanabilir veya bir saat ile ödeme yapabilirsiniz. -Daha az ancak daha büyük (1 TB +) veritabanını işlemek için iyidir. |
| **Dezavantajları** -şirket içi SQL Server kıyasla bazı özellik boşlukları ( [clr tümleştirmesi](https://technet.microsoft.com/library/ms131102.aspx), [tde](https://technet.microsoft.com/library/bb934049.aspx), [sıkıştırma desteği](https://technet.microsoft.com/library/cc280449.aspx), [SQL Server Reporting Services](https://technet.microsoft.com/library/ms159106.aspx), vb.)-500 GB 'lık veritabanı boyutu sınırı. | ***Dezavantajlar*** -güncelleştirmeler/yamalar (OS ve SQL), yaklaşık olarak 8000 (16 veri sürücüsü aracılığıyla) ile sınırlı olan sorumluluk-disk IOPS (saniye başına giriş/çıkış işlemleri) ile sınırlıdır. |

Bir VM 'de SQL Server kullanmak istiyorsanız, kendi SQL Server lisansınızı kullanabilir veya saatlik bir süre için ödeme yapabilirsiniz. Örneğin, portalda veya REST API aracılığıyla SQL Server bir görüntü kullanarak yeni bir sanal makine oluşturabilirsiniz.

![SQL Server VM oluşturma](data-storage-options/_static/image16.png)

![SQL Server VM görüntülerinin listesi](data-storage-options/_static/image17.png)

SQL Server görüntüyle bir VM oluşturduğunuzda, sanal makinenin kullanımına bağlı olarak, SQL Server lisans maliyetini saate göre ücretlendiriyoruz. Yalnızca birkaç ay boyunca çalıştırılacak bir projeniz varsa, bu, saatlik olarak ödeme yapacak. Projenizin en son yıllardır olduğunu düşünüyorsanız, lisansı normalde yaptığınız şekilde satın alabilirsiniz.

## <a name="summary"></a>Özet

Bulut bilgi işlem, uygulamanızın ihtiyaçlarını en iyi şekilde karşılayacak şekilde veri depolama yaklaşımının karışmasını ve eşleşmesini pratik hale getirir. Yeni bir uygulama oluşturuyorsanız, uygulamanız büyüdükçe iyi çalışmaya devam edecek yaklaşımları seçmek için burada listelenen soruları dikkatle düşünün. [Sonraki bölümde](data-partitioning-strategies.md) , birden çok veri depolama yaklaşımını birleştirmek için kullanabileceğiniz bazı bölümleme stratejileri açıklanmaktadır.

## <a name="resources"></a>Kaynaklar

Daha fazla bilgi için aşağıdaki kaynaklara bakın.

Veritabanı platformu seçme:

- [Yüksek düzeyde ölçeklenebilir çözümler Için veri erişimi: SQL, NoSQL ve çok yönlü kalıcılığı kullanma](https://aka.ms/dag-doc). Microsoft düzenleri ve uygulamalarına göre, bulut uygulamaları için kullanılabilen farklı veri depolarının çeşitleriyle ilgili ayrıntılı olarak yer alan E-kitap.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/ff898430.aspx). Veri tutarlılığı öncü, veri çoğaltma ve eşitleme Kılavuzu, dizin tablo kalıbı, gerçekleştirilmiş görünüm düzenine bakın.
- [Taban: ACID alternatifi](http://queue.acm.org/detail.cfm?id=1394128). Veri tutarlılığı ve ölçeklenebilirlik arasındaki dengeler hakkında makale.
- [Yedi hafta Içinde yedi veritabanı: modern veritabanlarına ve NoSQL hareketine yönelik bir kılavuz](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921). Eric Redmond ve Jim R. Solson tarafından kitap. Günümüzde sunulan veri depolama platformları aralığına yönelik olarak kendinizi önemle öneririz.

SQL Server ve SQL veritabanı arasında seçim yapma:

- [SQL veritabanı Kılavuzu Için Premium önizleme](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx). SQL Veritabanı Premium bir giriş ve SQL veritabanı Web ve Business sürümleri üzerinde ne zaman seçim yapabileceğiniz hakkında rehberlik.
- [Yönergeler ve sınırlamalar (Azure SQL veritabanı)](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx). SQL Database 'in desteklemediği SQL Server özelliklerine odaklanan bir de dahil olmak üzere SQL veritabanı sınırlamaları hakkında belgelere bağlantı veren Portal sayfası.
- [Azure sanal makineler 'de SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx). Azure 'da SQL Server çalıştırma hakkındaki belgelere bağlanan Portal sayfası.
- [Scott Guthrie, Azure 'DA SQL veritabanlarını açıklar](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/). 6 dakikalık video Scott Guthrie tarafından SQL veritabanı 'na giriş.
- [Azure sanal makinelerinde SQL Server Için uygulama desenleri ve geliştirme stratejileri](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx).

ASP.NET Web uygulamasında Entity Framework ve SQL veritabanı kullanma

- [MVC 5 kullanarak EF 6 Ile çalışmaya](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)başlama. EF kullanan ve veritabanını Azure 'a ve SQL veritabanı 'na dağıtan bir MVC uygulaması oluşturma konusunda size yol gösteren dokuz parçalı öğretici serisi.
- [Visual Studio kullanarak Web dağıtımı ASP.net](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). Code First kullanarak bir veritabanının nasıl dağıtılacağı hakkında daha ayrıntılı bilgi içeren on iki bölümden oluşan öğretici serisi.
- [Üyelik, OAuth ve SQL veritabanı ile bir Azure Web sitesine güvenli bir ASP.NET MVC 5 uygulaması dağıtın](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/). Kimlik doğrulaması kullanan bir Web uygulaması oluşturma, üyelik veritabanında uygulama tabloları depolama, veritabanı şemasını değiştirme ve uygulamayı Azure 'a dağıtır hakkında adım adım öğretici.
- [ASP.NET veri erişimi Içerik Haritası](https://go.microsoft.com/fwlink/p/?LinkId=282414). EF ve SQL veritabanı ile çalışmaya yönelik kaynakların bağlantıları.

Azure 'da MongoDB 'yi kullanma:

- [Azure 'Da MongoLab-MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/). Azure 'da MongoDB çalıştırma hakkındaki belgeler için Portal sayfası.
- [Azure 'daki bir sanal makinede çalışan MongoDB 'ye bağlanan bir Azure Web sitesi oluşturun](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/). Bir ASP.NET Web uygulamasında MongoDB veritabanının nasıl kullanılacağını gösteren adım adım öğretici.

HDInsight (Azure 'da Hadoop):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/). [Azure](https://azure.microsoft.com/) Web sitesindeki HDInsight 'a yönelik belgeler.
- [Hadoop ve HDInsight: Azure 'Da büyük veri](https://msdn.microsoft.com/magazine/dn385705.aspx). Azure 'da Hadoop 'a yönelik Bruno Terkaly ve Ricardo Villaloboş 'ın MSDN Magazine makalesi.
- [Microsoft desenleri ve uygulamaları-Azure Kılavuzu](https://msdn.microsoft.com/library/dn568099.aspx). MapReduce düzenine bakın.

> [!div class="step-by-step"]
> [Önceki](single-sign-on.md)
> [İleri](data-partitioning-strategies.md)
