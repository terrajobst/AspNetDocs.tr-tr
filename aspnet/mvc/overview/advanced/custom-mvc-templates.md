---
uid: mvc/overview/advanced/custom-mvc-templates
title: Özel MVC şablonu | Microsoft Docs
author: joeloff
description: VSıX uzantısı olarak bir şablon oluşturun.
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616356"
---
# <a name="custom-mvc-template"></a>Özel MVC Şablonu

[Jtanışes Eloff](https://github.com/joeloff) tarafından

Visual Studio 2010 için MVC 3 araç güncelleştirmesi sürümü, MVC projeleri için ayrı bir proje Sihirbazı sunmuştur. Değişiklik iki faktöre göre yönlendiriliyor. İlk olarak, MVC 3 ' teki yeni şablonların tanıtımı ve Razor gibi ek görünüm motorları için Visual Studio 'da yeni proje iletişim kutusunu ortaya çıkmasına yönelik destek. İkinci olarak, müşterilerin genişletilebilirlik noktaları istemesi gerekiyordu ve yeni MVC proje Sihirbazı bu isteklere yanıt vermek için bir fırsat sunuyor.

Özel şablon eklemek, yeni şablonları MVC proje Sihirbazı 'nda görünür hale getirmek için kayıt defterini kullanmayı kolaylaştıran bir dizi işlemdir. Yeni bir şablonun yazarı, gerekli kayıt girdilerinin yük zamanında oluşturulmasını sağlamak için onu bir MSI içinde sarmalıdır. Alternatif, şablonu içeren bir ZIP dosyası oluşturmak ve son kullanıcının gerekli kayıt defteri girişlerini el ile oluşturması gerekiyordu.

Yukarıda bahsedilen yaklaşımlardan hiçbiri ideal olmadığından, Visual Studio 2012 için MVC 4 ile başlayan özel MVC şablonlarını yazmayı, dağıtmayı ve yüklemeyi daha kolay hale getirmek için [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) uzantıları tarafından sunulan mevcut altyapıdan faydalanabilir. Bu yaklaşım tarafından sunulan avantajlardan bazıları şunlardır:

- VSıX uzantısı, farklı dilleri (C# ve Visual Basic) ve birden çok görünüm ALTYAPıSıNı (aspx ve Razor) destekleyen birden çok şablon içerebilir.
- Bir VSıX uzantısı, Visual Studio 'nun Express SKU 'Ları dahil birden çok SKU 'su hedefleyebilir.
- [Visual Studio Galerisi](https://visualstudiogallery.msdn.microsoft.com/) , uzantının geniş bir hedef kitleye dağıtılmasını kolaylaştırır.
- VSıX uzantıları, özel şablonlarınıza düzeltmeler ve güncelleştirmeler yazmak daha kolay hale getirilmesi için yükseltilebilir.

## <a name="prerequisites"></a>Önkoşullar

- Kullanıcıların, Vstemplate dosyaları için gerekli biçimlendirme dahil olmak üzere proje şablonları yazma konusunda bilgi sahibi olmaları gerekir.
- Kullanıcıların Visual Studio Professional ve daha yüksek bir sürümü yüklü olması gerekir. Express SKU 'Ları VSıX projeleri oluşturmayı desteklemez.
- [Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) yüklendi.

## <a name="example"></a>Örnek

İlk adım, ya da C# Visual Basic kullanarak yenı bir VSIX projesi oluşturmaktır. **Yeni proje > dosya**' yı seçin, ardından sol bölmedeki **genişletilebilirlik** ' e tıklayın ve **VSIX projesini**seçin.

![Yeni Proje](custom-mvc-templates/_static/image1.jpg)

Proje oluşturulduktan sonra VSıX Tasarımcısı açılır.

![Proje Tasarımcısı meta verileri](custom-mvc-templates/_static/image2.jpg)

Tasarımcı, uzantıyı yüklediklerinde kullanıcılara gösterilecek genel özelliklerden bazılarını düzenlemek veya Visual Studio 'daki yüklü uzantılara (**araçlar > Uzantılar ve güncelleştirmeler**) taramak için kullanılabilir. Genel bilgileri tamamladıktan sonra, **hedefleri yüklensin sekmesine**tıklayın.

![Proje Tasarımcısı yüklemesi hedefleri](custom-mvc-templates/_static/image3.jpg)

Bu sekme, uzantınızın desteklediği SKU 'Ları ve Visual Studio sürümlerini belirtmek için kullanılır. Tüm kullanıcıların VSıX 'in makine başına yüklemelerini etkinleştirmesi için **Bu VSIX 'in yüklü** onay kutusunu seçin. Web geliştirici Express (VWD) gibi ek SKU 'Lar eklemek için sağdaki **Yeni** düğmesine tıklayın.

![Yeni yükleme hedefi Ekle](custom-mvc-templates/_static/image4.jpg)

Tüm profesyonel ve daha yüksek SKU 'Ları (profesyonel, Premium ve Ultimate) desteklemek istiyorsanız, yalnızca **Microsoft.VisualStudio.Pro**, ailesinden en düşük SKU 'yı seçmeniz gerekir. Install hedeflerini tamamladıktan sonra tüm değişikliklerinizi kaydetmeyi unutmayın.

![Proje Tasarımcısı yüklemesi hedefleri](custom-mvc-templates/_static/image5.jpg)

**Varlıklar** sekmesi, tüm IÇERIK dosyalarınızı VSIX 'e eklemek için kullanılır. MVC özel meta veriler gerektirdiğinden, içerik eklemek için **varlıklar** sekmesini kullanmak yerine VSIX bildirim dosyasının ham xml 'sini de düzenleyebilirsiniz. Şablon içeriğini VSıX projesine ekleyerek başlayın. Klasör ve içerik yapısının projenin yerleşimini yansıtması önemlidir. Aşağıdaki örnek, temel MVC proje şablonundan türetilmiş dört proje şablonu içerir. Proje şablonunuzu (ProjectTemplates klasörü altındaki her şey) oluşturan tüm dosyaların VSıX proje dosyasındaki **içerik** ItemGroup 'a eklendiğinden ve aşağıdaki örnekte gösterildiği gibi her bir öğenin **CopyToOutputDirectory** ve **ıncludeınsix** meta veri kümesini içerdiğinden emin olun.

&lt;Içerik ekleme =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

CopyToOutputDirectory&gt;her zaman&lt;/CopyToOutputDirectory &lt;&gt;

&lt;ınclude6&gt;true&lt;/ıncludefaturalanmış altı&gt;

&lt;/Content&gt;

Aksi takdirde, derleme VSıX oluştururken şablonun içeriğini derlemeye çalışır ve muhtemelen bir hata görürsünüz. Şablonlarda kod dosyaları genellikle proje şablonu örneği oluşturulurken Visual Studio tarafından kullanılan özel [şablon parametrelerini](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) içerir ve bu nedenle IDE 'de derlenemez.

![Çözüm Gezgini](custom-mvc-templates/_static/image6.jpg)

VSıX tasarımcısını kapatın, **Çözüm Gezgini** ' de **kaynak. Extension. manifest** dosyasına sağ tıklayın ve **birlikte Aç** ' ı seçin ve **XML (metin) düzenleyici** seçeneğini belirleyin.

![Iletişim kutusuyla aç](custom-mvc-templates/_static/image7.jpg)

&lt;bir varlık **&gt;** öğesi oluşturun ve VSIX 'e dahil olması gereken her bir dosya için bir **&lt;varlık&gt;** öğesi ekleyin. Her bir **&lt;varlık&gt;** öğesinin **tür** özniteliği **Microsoft. VisualStudio. Mvc. Template**olarak ayarlanmalıdır. Bu, yalnızca MVC proje sihirbazının anladığı özel bir ad alanıdır. Bildirim dosyasının yapısı ve düzeni hakkında daha fazla bilgi için VSıX 2,0 şema belgelerine bakın.

Yalnızca VSıX 'e dosya eklemek, şablonları MVC Sihirbazı ile kaydetmek için yeterli değildir. MVC sihirbazına şablon adı, açıklama, desteklenen görünüm motorları ve programlama dili gibi bilgiler sağlamanız gerekir. Bu bilgiler, her **vstemplate** dosyası Için **&lt;varlık&gt;** öğesiyle ilişkili özel özniteliklerde taşınır.

&lt;varlık D:valtalt yol =&quot;Projecttemplates\mymvcwebapplicationprojecttemplate.exe&quot;

Tür =&quot;Microsoft. VisualStudio. Mvc. Template&quot;

d:Source =&quot;dosya&quot;

Yol =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Dil =&quot;C#&quot;

ViewEngine =&quot;aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

Title =&quot;özel temel Web uygulaması&quot;

Description = temel MVC web uygulamasından (Razor) türetilmiş özel bir şablon&quot;&quot;

Sürüm =&quot;4,0&quot;/&gt;

Aşağıda, mevcut olması gereken özel özniteliklerin bir açıklaması verilmiştir:

- **ProjectType** , MVC olarak ayarlanmalıdır.
- **Dil** , şablon tarafından desteklenen geliştirme dilini belirtir. Geçerli değerler ya da C# vb.
- **ViewEngine** , şablon tarafından desteklenen aspx veya Razor gibi görünüm altyapısını belirler. Bu alan için özel bir değer belirtebilirsiniz.
- **TemplateId** , şablonları gruplandırmak için kullanılır. Değer var olan bir şablon KIMLIĞIYLE eşleşiyorsa, daha önce MVC sihirbazıyla kaydedilen şablonlar geçersiz kılınır.
- **Başlık** her proje ŞABLONUNUN altındaki MVC sihirbazında görünen kısa açıklamayı belirler.
- **Açıklama** , şablonun daha ayrıntılı bir açıklamasını belirtir.

Tüm dosyaları bildirime ekledikten ve kaydettikten sonra, tasarımcı 'daki **varlıklar** sekmesinin, **vstemplate** dosyaları için **&lt;varlık&gt;** öğelerine eklediğiniz özel öznitelikleri gösterdiğine dikkat edin.

![Proje Tasarımcısı varlıkları](custom-mvc-templates/_static/image8.jpg)

Şimdi, VSıX projesini derlemek ve yüklemek artık devam etmektedir.

Visual Studio 'nun tüm örneklerinin VSıX uzantısını test etmek istediğiniz makinede kapatıldığından emin olun. Visual Studio başlangıç sırasında yeni uzantıları tarar, bu nedenle bir VSıX yüklenirken IDE açıksa, Visual Studio 'Yu yeniden başlatmanız gerekir. Visual **Studio 'yu başlatmak**Için, Explorer 'da VSIX dosyasını çift tıklatın, **yükleme** ' ye tıklayın ve ardından Visual Studio 'yu başlatın.

![VSıX yükleyicisi](custom-mvc-templates/_static/image9.jpg)

Genişletmenin yüklendiğini onaylamak için menüden **araçlar > Uzantılar ve güncelleştirmeler** ' i seçin. VSıX yükleyicisi, uzantının yüklenmesi sırasında herhangi bir hata bildirmezse, daha fazla bilgi için VSıX yükleyicisi günlüğünü görüntüleyebilirsiniz. Günlük genellikle uzantıyı yükleyen kullanıcının **% Temp%** klasöründe oluşturulur (örneğin, **C:\users\bob\appdata\local\temp**).

![Uzantılar ve güncelleştirmeler](custom-mvc-templates/_static/image10.jpg)

Pencereyi kapattıktan sonra, yeni şablonlarınızın MVC sihirbazında gösterilip gösterilmediğini görmek için MVC 4 projesi oluşturabilirsiniz.

![Yeni ASP.NET MVC 4 Proje](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>Sınırlamalar

1. MVC Sihirbazı yerelleştirilmiş özel şablonları desteklemez.
2. Sihirbaz özel şablonları bulamıyorsa hata bildirmeyecektir. Gerekli özel özniteliklerin herhangi biri yoksa, şablon yalnızca sihirbazdan hariç tutulur.
