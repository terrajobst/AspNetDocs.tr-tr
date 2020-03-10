---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms ile çalışmaya başlama-Bölüm 2 | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566012"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms ile çalışmaya başlama-2. Bölüm

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="the-entitydatasource-control"></a>EntityDataSource denetimi

Önceki öğreticide bir Web sitesi, bir veritabanı ve bir veri modeli oluşturdunuz. Bu öğreticide, bir Entity Framework veri modeliyle çalışmayı kolaylaştırmak için ASP.NET tarafından sağlanan `EntityDataSource` denetimiyle çalışırsınız. Öğrenci verilerini görüntüleme ve düzenlemeyle ilgili bir `GridView` denetimi, yeni öğrenciler eklemek için bir `DetailsView` denetimi ve bir departmanı seçmeye yönelik bir `DropDownList` denetimi oluşturacaksınız (Bu, daha sonra ilişkili kursları görüntülemek için kullanacaksınız).

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

Bu uygulamada, veritabanını güncelleştiren sayfalara giriş doğrulaması eklememezsiniz ve bir üretim uygulamasında gerekli olduğu gibi bazı hata işlemenin bir kısmı sağlam olmayacaktır. Bu, öğreticiyi Entity Framework odaklanmasını ve çok uzun sürmasını önler. Bu özellikleri uygulamanıza ekleme hakkında ayrıntılı bilgi için bkz. [ASP.NET Web sayfalarında Kullanıcı girişini doğrulama](https://msdn.microsoft.com/library/7kh55542.aspx) ve [ASP.NET sayfalarında ve uygulamalarında hata işleme](https://msdn.microsoft.com/library/w16865z6.aspx).

## <a name="adding-and-configuring-the-entitydatasource-control"></a>EntityDataSource denetimini ekleme ve yapılandırma

`People` varlık kümesinden `Person` varlıkları okumak için bir `EntityDataSource` denetimi yapılandırarak başlayacaksınız.

Visual Studio 'Yu açık olduğundan ve 1. bölümde oluşturduğunuz projeyle çalıştığınızdan emin olun. Projeyi veri modelini oluştururken veya yaptığınız son değişiklikten bu yana oluşturmadıysa, projeyi şimdi oluşturun. Veri modelindeki değişiklikler, proje derlenene kadar tasarımcı için kullanılamaz hale getirilmez.

**Ana sayfa şablonunu kullanarak Web formunu** kullanarak yeni bir Web sayfası oluşturun ve bunu *öğrenciler. aspx*olarak adlandırın.

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

Ana sayfa olarak *site. Master* belirtin. Bu öğreticiler için oluşturduğunuz tüm sayfalar, bu ana sayfayı kullanacaktır.

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

**Kaynak** görünümü ' nde, aşağıdaki örnekte gösterildiği gibi `Content2`adlı `Content` denetimine `h2` başlığını ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

**Araç kutusunun** **veri** sekmesinden, sayfaya bir `EntityDataSource` denetimi sürükleyin, BAŞLıĞıN altına bırakın ve kimliği `StudentsEntityDataSource`olarak değiştirin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

**Tasarım** görünümüne geçiş yapın, veri kaynağı denetiminin akıllı etiketine tıklayın ve **veri kaynağını Yapılandır sihirbazını başlatmak** için **veri kaynağını Yapılandır** ' a tıklayın.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

**ObjectContext yapılandırma** Sihirbazı adımında, **adlandırılmış bağlantı**değeri olarak **sseçlentities** ' i seçin ve **DefaultContainerName** değeri olarak **sseçlentities** ' i seçin. Ardından **İleri**'ye tıklayın.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

Note: Bu noktada aşağıdaki iletişim kutusunu alırsanız devam etmeden önce projeyi derlemeniz gerekir.

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

**Veri seçimini Yapılandır** adımında, **entitySetName**değeri olarak **kişiler** ' i seçin. **Seç**' in altında, **bir ll Seç** onay kutusunun seçili olduğundan emin olun. Ardından güncelleştirme ve silmeyi etkinleştirme seçeneklerini belirleyin. İşiniz bittiğinde **son**' a tıklayın.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>Veritabanı kurallarını silmeye Izin verecek şekilde yapılandırma

Kullanıcıların, diğer tablolarla (`Course`, `StudentGrade`ve `OfficeAssignment`) üç ilişkisi bulunan `Person` tablosundan öğrencileri silmesine imkan tanıyan bir sayfa oluşturacaksınız. Varsayılan olarak, diğer tablolardan birinde ilgili satırlar varsa, veritabanı `Person` bir satırı silmenizi önler. Önce ilişkili satırları el ile silebilir veya bir `Person` satırı sildiğinizde veritabanını otomatik olarak silecek şekilde yapılandırabilirsiniz. Bu öğreticideki öğrenci kayıtları için veritabanını ilgili verileri otomatik olarak silecek şekilde yapılandıracaksınız. Öğrencilerin yalnızca `StudentGrade` tablosunda ilişkili satırları olabileceğinden, üç ilişkilerden yalnızca birini yapılandırmanız gerekir.

Bu öğreticiye giden projeden indirdiğiniz *okul. mdf* dosyasını kullanıyorsanız, bu yapılandırma değişiklikleri zaten yapıldığından bu bölümü atlayabilirsiniz. Veritabanını bir komut dosyası çalıştırarak oluşturduysanız, aşağıdaki yordamları gerçekleştirerek veritabanını yapılandırın.

**Sunucu Gezgini**bölümünde, Bölüm 1 ' de oluşturduğunuz veritabanı diyagramını açın. `Person` ve `StudentGrade` arasındaki ilişkiye sağ tıklayın (tablolar arasındaki çizgi) ve ardından **Özellikler**' i seçin.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

**Özellikler** penceresinde **INSERT ve Update Specification** ' ı genişletin ve **DeleteRule** özelliğini **Cascade**olarak ayarlayın.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

Diyagramı kaydedin ve kapatın. Veritabanını güncelleştirmek isteyip istemediğiniz sorulursa **Evet**' e tıklayın.

Modelin bellekte bulunan varlıkların veritabanının yaptığı verilerle eşitlenmiş olduğundan emin olmak için, veri modelinde karşılık gelen kuralları ayarlamanız gerekir. *SchoolModel. edmx*' i açın, `Person` ve `StudentGrade`arasındaki ilişki hattına sağ tıklayın ve sonra **Özellikler**' i seçin.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

**Özellikler** penceresinde **uç1 OnDelete** öğesini **Cascade**olarak ayarlayın.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

*SchoolModel. edmx* dosyasını kaydedip kapatın ve ardından projeyi yeniden derleyin.

Genel olarak, veritabanı değiştiğinde modelin eşitlenmesi için çeşitli seçenekleriniz vardır:

- Belirli değişiklik türleri (tablo, görünüm veya saklı yordam ekleme veya yenileme gibi) için tasarımcıya sağ tıklayın ve tasarımcı değişiklikleri otomatik hale getirmek için **veritabanından modeli Güncelleştir** ' i seçin.
- Veri modelini yeniden oluşturun.
- Bunun gibi el ile güncelleştirmeler gerçekleştirin.

Bu durumda, modeli yeniden oluşturabilirsiniz veya ilişki değişikliğinden etkilenen tabloları yeniledi, ancak alan adı değişikliğini bir daha (`FirstName` `FirstMidName`) yapmanız gerekir.

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>Varlıkları okumak ve güncelleştirmek için bir GridView denetimi kullanma

Bu bölümde öğrencileri göstermek, güncelleştirmek veya silmek için `GridView` bir denetim kullanacaksınız.

*Öğrenciler. aspx* ' i açın veya değiştirin ve **Tasarım** görünümü ' ne geçin. **Araç kutusunun** **veri** sekmesinden `EntityDataSource` denetiminin sağına bir `GridView` denetimini sürükleyin, `StudentsGridView`adlandırın, akıllı etikete tıklayın ve sonra veri kaynağı olarak **StudentsEntityDataSource** ' yi seçin.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

**Şemayı Yenile** ' ye tıklayın (onaylamanız istenirse **Evet** ' e tıklayın), ardından **sayfalama etkinleştir**, **sıralamayı etkinleştir**, **Düzenle**etkinleştir ve **silmeyi etkinleştir**' e tıklayın.

**Sütunları Düzenle**' ye tıklayın.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

**Seçili alanlar** kutusunda, **PersonID**, **LastName**ve **HireDate**öğesini silin. Genellikle kullanıcılara bir kayıt anahtarı görüntülememeniz, işe alım tarihi öğrencilerle ilgili değildir ve adın her iki parçasını da bir alana yerleştirip ad alanlarından yalnızca birine ihtiyacınız vardır.)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

**Firstmidname** alanını seçin ve ardından **Bu alanı TemplateField olarak Dönüştür ' e**tıklayın.

Kayıt **tarihi**için de aynısını yapın.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

**Tamam** ' a tıklayın ve ardından **kaynak** görünümü ' ne geçin. Kalan değişiklikler doğrudan biçimlendirmede daha kolay olacaktır. `GridView` denetim biçimlendirmesi artık aşağıdaki örneğe benzer şekilde görünür.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

Komut alanından sonraki ilk sütun, şu anda ilk adı görüntüleyen bir şablon alanıdır. Bu şablon alanının işaretlemesini aşağıdaki örneğe benzer şekilde değiştirin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

Görüntüleme modunda, iki `Label` denetim adı ve soyadı görüntüler. Düzenleme modunda, adı ve soyadınızı değiştirebilmek için iki metin kutusu sağlanır. Görüntüleme modundaki `Label` denetimlerde olduğu gibi, doğrudan veritabanlarına bağlanan ASP.NET veri kaynağı denetimlerinde yaptığınız gibi `Bind` ve `Eval` ifadelerini tam olarak kullanırsınız. Tek fark, veritabanı sütunları yerine varlık özelliklerini belirtmektir.

Son sütun, kayıt tarihini gösteren bir şablon alanıdır. Bu alanın işaretlemesini aşağıdaki örneğe benzer şekilde değiştirin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

Hem görüntüleme hem de düzenleme modunda, "{0, d}" biçim dizesi tarihin "kısa tarih" biçiminde görüntülenmesine neden olur. (Bilgisayarınız Bu öğreticide gösterilen ekran görüntülerinden farklı şekilde bu biçimi farklı şekilde görüntüleyecek şekilde yapılandırılmış olabilir.)

Bu şablon alanlarının her birinde, tasarımcının varsayılan olarak bir `Bind` ifadesi kullandığına, ancak bunu `ItemTemplate` öğelerindeki bir `Eval` ifadesine değiştirdiğine dikkat edin. `Bind` ifade, verileri koddaki verilere erişmeniz gerekebilmeniz durumunda `GridView` denetim özelliklerinde kullanılabilir hale getirir. Bu sayfada kodda bu verilere erişmeniz gerekmez, böylece daha verimli olan `Eval`kullanabilirsiniz. Daha fazla bilgi için bkz. verilerinizi [veri denetimlerinden alma](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx).

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>, Performansı artırmak için EntityDataSource Denetim biçimlendirmesini yeniden gözden

`EntityDataSource` denetimin biçimlendirmesinde, `ConnectionString` ve `DefaultContainerName` özniteliklerini kaldırın ve bunları bir `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` özniteliğiyle değiştirin. Bu, nesne bağlamı sınıfında sabit kodlanmış bir bağlantı kullanmanız gerekmediği müddetçe, her bir `EntityDataSource` denetimi oluşturduğunuzda yapmanız gereken bir değişiklik olacaktır. `ContextTypeName` özniteliğini kullanmak aşağıdaki avantajları sağlar:

- Daha iyi performans. `EntityDataSource` denetimi `ConnectionString` ve `DefaultContainerName` özniteliklerini kullanarak veri modelini başlattığında, her istekte meta verileri yüklemek için ek çalışma gerçekleştirir. `ContextTypeName` özniteliğini belirtirseniz bu gerekli değildir.
- Yavaş yükleme, Entity Framework 4,0 ' de oluşturulan nesne bağlamı sınıflarında (Bu öğreticide `SchoolEntities` gibi) varsayılan olarak açıktır. Bu, gezinti özelliklerinin ihtiyacınız olduğunda otomatik olarak ilgili verilerle birlikte yüklendiği anlamına gelir. Yavaş yükleme, Bu öğreticinin ilerleyen kısımlarında daha ayrıntılı olarak açıklanmıştır.
- Nesne bağlamı sınıfına uyguladığınız özelleştirmeler (Bu durumda `SchoolEntities` sınıfı), `EntityDataSource` denetimini kullanan denetimlerde kullanılabilir. Nesne bağlamı sınıfını özelleştirmek, bu öğretici serisinde kapsanmayan gelişmiş bir konudur. Daha fazla bilgi için bkz. [Entity Framework oluşturulan türleri genişletme](https://msdn.microsoft.com/library/dd456844.aspx).

Biçimlendirme artık aşağıdaki örneğe benzeyecektir (özelliklerin sırası farklı olabilir):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` özniteliği, yabancı anahtar sütunları varlık özellikleri olarak gösterilmediğinden, Entity Framework önceki sürümlerinde gerekli olan bir özelliğe başvurur. Geçerli sürüm *yabancı anahtar ilişkilendirmelerini*kullanmayı mümkün kılar. Bu, yabancı anahtar özelliklerinin hepsi, çoktan çoğa ilişkilendirmeler için kullanıma sunulacak anlamına gelir. Varlıklarınızda yabancı anahtar özellikleri varsa ve [karmaşık tür](https://msdn.microsoft.com/library/bb738472.aspx)yoksa, bu özniteliği `False`olarak bırakabilirsiniz. Varsayılan değer `True`olduğundan, biçimlendirmeden özniteliği kaldırmayın. Daha fazla bilgi için bkz. [nesneleri düzleştirme (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx).

Sayfayı çalıştırın ve öğrenciler ve çalışanların bir listesini görürsünüz (bir sonraki öğreticide yalnızca öğrencilerle filtrelemeniz gerekir). Ad ve soyadı birlikte görüntülenir.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

Görüntüyü sıralamak için bir sütun adına tıklayın.

Herhangi bir satırda **Düzenle** ' ye tıklayın. İlk ve son adı değiştirebileceğiniz metin kutuları görüntülenir.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

**Sil** düğmesi de geçerlidir. Kayıt tarihi olan bir satır için Sil ' e tıklayın ve satır kaybolur. (Kayıt tarihi olmayan satırlar, Eğitmenler 'i temsil eder ve bir bilgi tutarlılığı hatası alabilirsiniz. Bir sonraki öğreticide, bu listeyi yalnızca öğrencileri içerecek şekilde filtrelemeniz gerekir.)

## <a name="displaying-data-from-a-navigation-property"></a>Gezinti özelliğinden verileri görüntüleme

Şimdi her öğrencinin kaç kursu kayıtlı olduğunu öğrenmek istediğinizi varsayalım. Entity Framework, `Person` varlığının `StudentGrades` gezinti özelliğinde bu bilgileri sağlar. Veritabanı tasarımı bir ders atanmaksızın bir öğrenciye kayıt atanmasına izin vermediğinden, bu öğreticide, kurs ile ilişkili `StudentGrade` tablo satırında bir satıra sahip olduğunu varsayabilirsiniz. (`Courses` gezinti özelliği yalnızca eğitmenler içindir.)

`EntityDataSource` denetiminin `ContextTypeName` özniteliğini kullandığınızda, bu özelliğe eriştiğinizde Entity Framework bir gezinti özelliği için bilgileri otomatik olarak alır. Bu, *yavaş yükleme*olarak adlandırılır. Ancak, bu, ek bilgi gerektiğinde veritabanına ayrı bir çağrı ile sonuçlandığından verimsiz olabilir. `EntityDataSource` denetimi tarafından döndürülen her varlık için gezinti özelliğinden veriye ihtiyacınız varsa, ilgili verileri veritabanına tek bir çağrıda varlıkla birlikte almak daha etkilidir. Buna *Eager yükleme*adı verilir ve `EntityDataSource` denetiminin `Include` özelliğini ayarlayarak bir gezinti özelliği için Eager yüklemesi belirlersiniz.

*Öğrenciler. aspx*' te her öğrenciye yönelik kurs sayısını göstermek istersiniz; bu nedenle yükleme en iyi seçenektir. Tüm öğrencileri görüntülüyor, ancak yalnızca birkaç tanesi için (biçimlendirmeye ek olarak bazı kod yazılmasını gerektiren) kurslar sayısını gösteriyorsa, geç yükleme daha iyi bir seçim olabilir.

*Öğrenciler. aspx*' i açın veya geçiş yapın, **Tasarım** görünümü ' nü değiştirin, `StudentsEntityDataSource`' yi seçin ve **Özellikler** penceresinde **Include** özelliğini **studentnotlar**olarak ayarlayın. (Birden çok gezinti özelliği almak isterseniz, adlarını virgülle ayırarak belirtebilirsiniz; Örneğin, **Studentnotlar, kurslar**.)

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

**Kaynak** görünümüne geçin. `StudentsGridView` denetiminde, son `asp:TemplateField` öğesinden sonra aşağıdaki yeni şablon alanını ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

`Eval` ifadesinde, gezinti özelliğine `StudentGrades`başvurabilirsiniz. Bu özellik bir koleksiyon içerdiğinden, öğrencinin kaydolduğu kurslar sayısını göstermek için kullanabileceğiniz bir `Count` özelliğine sahiptir. Daha sonraki bir öğreticide, Koleksiyonlar yerine tek varlıklar içeren gezinti özelliklerinden verileri görüntülemeyi göreceksiniz. (Verileri gezinti özelliklerinden göstermek için `BoundField` öğelerini kullanmayacağınızı unutmayın.)

Sayfayı çalıştırın ve şimdi her öğrencinin kaç kursu kayıtlı olduğunu görürsünüz.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>Varlıkları eklemek için DetailsView denetimi kullanma

Sonraki adım, yeni öğrenciler eklemenize olanak sağlayacak `DetailsView` denetimine sahip bir sayfa oluşturmaktır. Tarayıcıyı kapatın ve ardından *site. Master* ana sayfasını kullanarak yeni bir Web sayfası oluşturun. Sayfayı *StudentsAdd. aspx*olarak adlandırın ve ardından **kaynak** görünümüne geçin.

`Content2`adlı `Content` denetimi için varolan biçimlendirmeyi değiştirmek üzere aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

Bu biçimlendirme,, ekleme işlemini etkinleştirse de, *öğrenciler. aspx*içinde oluşturduğunuz birine benzer bir `EntityDataSource` denetimi oluşturur. `GridView` denetiminde olduğu gibi, `DetailsView` denetiminin bağlı alanları, varlık özelliklerine başvurmaları dışında, doğrudan bir veritabanına bağlanan bir veri denetimine yönelik olarak kodlanır. Bu durumda, `DetailsView` denetimi yalnızca satır eklemek için kullanılır, bu nedenle varsayılan modu `Insert`olarak ayarlamanız gerekir.

Sayfayı çalıştırın ve yeni bir öğrenci ekleyin.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

Yeni bir öğrenci ekledikten sonra hiçbir şey gerçekleşmeyecektir, ancak artık *öğrenciler. aspx*çalıştırırsanız yeni öğrenci bilgilerini görürsünüz.

## <a name="displaying-data-in-a-drop-down-list"></a>Açılan listede verileri görüntüleme

Aşağıdaki adımlarda, bir `DropDownList` denetimini bir `EntityDataSource` denetimini kullanarak bir varlık kümesine vereceksiniz. Öğreticinin bu bölümünde, bu listede çok daha fazlasını yapamayacağız. Daha sonraki bölümlerde, kullanıcıların departmanla ilişkili kursları görüntülemesi için bir departman seçmesini sağlamak üzere listeyi kullanacaksınız.

*Kurslar. aspx*adlı yeni bir Web sayfası oluşturun. **Kaynak** görünümü ' nde, `Content2`adlı `Content` denetimine bir başlık ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

**Tasarım** görünümü ' nde, daha önce yaptığınız gibi sayfaya bir `EntityDataSource` denetimi ekleyin, bu kez `DepartmentsEntityDataSource`adlandırın. **EntitySetName** değeri olarak **Departmanlar** ' ı seçin ve yalnızca **DepartmentID** ve **ad** özelliklerini seçin.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

**Araç kutusunun** **Standart** sekmesinden, sayfaya bir `DropDownList` denetimi sürükleyin, `DepartmentsDropDownList`adlandırın, akıllı etikete tıklayın ve **veri kaynağını seç** ' i seçerek **DataSource Yapılandırma Sihirbazı**'nı başlatın.

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

**Veri kaynağı seçin** adımında, veri kaynağı olarak **DepartmentsEntityDataSource** ' i seçin, **şemayı Yenile**' ye tıklayın ve ardından değer verisi alanı olarak görüntülenecek ve **DepartmentID** veri alanı olarak **ad** ' ı seçin. **Tamam**’a tıklayın.

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Entity Framework kullanarak denetimin kaynağını belirlemek için kullandığınız yöntem, varlıkları ve varlık özelliklerini belirtmediğimizden diğer ASP.NET veri kaynağı denetimleriyle aynıdır.

**Kaynak** görünümüne geçin ve `DropDownList` denetiminden hemen önce "departmanı seçin:" ekleyin.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

Bir anımsatıcı olarak, `ConnectionString` ve `DefaultContainerName` özniteliklerini bir `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` özniteliğiyle değiştirerek `EntityDataSource` denetimin işaretlemesini bu noktada değiştirin. `EntityDataSource` denetim işaretlemesini değiştirmeden önce veri kaynağı denetimine bağlı veriye bağlı denetim oluşturmanızın ardından, tasarımcı, veri bağlantılı denetimde bir **Şemayı yenileme** seçeneği sağlamadığı için genellikle en iyi seçenektir. Bu işlem, tasarımcı, verilere bağlı denetimde bir şema seçeneğini sunmayacak.

Sayfayı çalıştırın ve açılan listeden bir departman seçebilirsiniz.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

Bu, `EntityDataSource` denetimini kullanmaya giriş işlemini tamamlar. Bu denetimle çalışma, genellikle diğer ASP.NET veri kaynağı denetimleriyle çalışmaktan farklı değildir, ancak tablo ve sütun yerine varlıklara ve özelliklere başvurırsınız. Tek özel durum, gezinti özelliklerine erişmek istediğiniz durumdur. Sonraki öğreticide, `EntityDataSource` denetimi ile kullandığınız sözdiziminin, verileri filtreleyip, gruplandırdığınızda ve sipariş ettiğinizde diğer veri kaynağı denetimlerinden de farklı olabileceğini görürsünüz.

> [!div class="step-by-step"]
> [Önceki](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [İleri](the-entity-framework-and-aspnet-getting-started-part-3.md)
