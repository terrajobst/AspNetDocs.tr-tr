---
uid: whitepapers/overview
title: Teknik incelemeler | Microsoft Docs
author: rick-anderson
description: Bu sayfada, ASP.NET yükleyip yapılandırmanıza ve güvenli, hızlı ve esnek ASP.NET uygulamaları yazmanıza yardımcı olacak teknik incelemeler bulacaksınız.
ms.author: riande
ms.date: 11/15/2011
ms.assetid: d5e79470-01f2-4d65-8077-11c3e10a6784
msc.legacyurl: /whitepapers
msc.type: content
ms.openlocfilehash: 1a3a9fe5d685d4b38efe666fc88ff57016482ada
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640856"
---
# <a name="whitepapers"></a>Teknik İncelemeler

> Bu sayfada, ASP.NET yükleyip yapılandırmanıza ve güvenli, hızlı ve esnek ASP.NET uygulamaları yazmanıza yardımcı olacak teknik incelemeler bulacaksınız.
> 
> - [ASP.NET 4](#aspnet4)
> - [ASP.NET güvenlik teknik Incelemeleri](#security)
> - [Yükleme ve kurulum teknik Incelemeleri](#setup)
> - [SQL Server Teknik Incelemeler](#sql)
> - [Genel Teknik Incelemeler](#general)

<a id="aspnet4"></a>
## <a name="aspnet-4"></a>ASP.NET 4

ASP.NET 4 ve Visual Studio 2010 ile ilgili bilgiler.

[ASP.NET MVC 4 sürüm notları](mvc4-beta-release-notes.md "MVC4-Release-notlar")

Bu belgede, Visual Studio 2010 için ASP.NET MVC 4 geliştirici önizlemesinde sunulan yeni özellikler ve geliştirmeler ve yükleme notları ve bilinen sorunlar açıklanmaktadır.

[ASP.NET MVC 3 sürüm notları](mvc3-release-notes.md "mvc3-Release-notlar")

Bu belgede, ASP.NET MVC 3 ' te sunulan yeni özellikler ve geliştirmeler ve yükleme notları ve bilinen sorunlar açıklanmaktadır.

[ASP.NET 4 ve Visual Studio 2010 Web Geliştirmeye Genel Bakış](aspnet4/index.md "aspnet4")

ASP.NET için pek çok heyecan verici değişiklik .NET Framework sürüm 4 ' te geliyor. Bu belge, yaklaşan sürüme dahil edilen yeni özelliklerin birçoğu için bir genel bakış sunar.

[ASP.NET 4 Beta 2 Son değişiklik](aspnet4/breaking-changes.md "Son değişiklikler")

Bu belgede, ASP.NET 4 Beta 1 sürümü de dahil olmak üzere önceki sürümler kullanılarak oluşturulan uygulamaları etkileyebilecek .NET Framework sürüm 4 Beta 2 sürümü (yani, ASP.NET 4 Beta 2 sürümü) için yapılmış değişiklikler açıklanmaktadır.

[ASP.NET MVC 2 Sürümündeki Yenilikler](what-is-new-in-aspnet-mvc.md "ASPNET MVC 'deki yenilikler")

Bu belge, ASP.NET MVC 2 ' de tanıtılan yeni özellikleri ve geliştirmeleri açıklamaktadır.

[Bir ASP.NET MVC 1.0 Uygulamasını ASP.NET MVC 2 Sürümüne Yükseltme](aspnet-mvc2-upgrade-notes.md "ASPNET-mvc2-Upgrade-notlar")

ASP.NET MVC 2 aynı sunucuda ASP.NET MVC 1,0 ile yan yana yüklenebilir. Bu, ASP.NET MVC 1,0 uygulamasının ASP.NET MVC 2 ' ye ne zaman yükseltileceğini seçerken uygulama geliştiricileri esnekliği sağlar. Bu belge, hem el ile nasıl yükselteceğiniz, ister Visual 'teki bir sihirbazla birlikte...

<a id="security"></a>
## <a name="aspnet-security-whitepapers"></a>ASP.NET güvenlik teknik Incelemeleri

Güvenlik, internet uygulamalarının önemli bir yönüdür ve bu teknik incelemeler, güvenli ASP.NET uygulamalarının nasıl tasarlanacağını ve uygulanacağını tartışır.

[Güvenlik için ASP.NET 2,0 uygulamalarını işaretleme](https://msdn.microsoft.com/library/ms998325.aspx)

Bu, güvenlikle ilgili olayları ve işlemleri izlemek üzere ASP.NET uygulamanızı işaretlemek için özel durum izleme olaylarını nasıl kullanacağınızı gösterir. ASP.NET sürüm 2,0, birçok standart için izleme içeren sistem durumu izleme sağlar...

[ASP.NET 2,0 için bir güvenlik dağıtımı Incelemesi gerçekleştirme](https://msdn.microsoft.com/library/ms998367.aspx)

Bu, uygunsuz yapılandırma ayarları tarafından tanıtılan olası güvenlik açıklarını belirlemek için bir ASP.NET 2,0 uygulaması için nasıl güvenlik dağıtımı incelemesinin gerçekleştirileceğini gösterir. İnceleme işleminin çoğunluğu şunları içerir...

[ASP.NET 2,0 ' de roller için ADAM kullanma](https://msdn.microsoft.com/library/ms998331.aspx)

Bu, ASP.NET rollerini depolamak için Active Directory uygulama modu (ADAM) kullanan bir ASP.NET Web sitesini nasıl geliştirebileceğinizi gösterir. ADAM ve Yetkilendirme Yöneticisi (AzMan) ilke deposunu yapılandırmayı, yeni roller oluşturmayı ve...

[ASP.NET 2,0 ile Yetkilendirme Yöneticisi 'Ni (AzMan) kullanma](https://msdn.microsoft.com/library/ms998336.aspx)

Bu şekilde, Yetkilendirme Yöneticisi 'ni (AzMan) rolleri yönetmek, Kullanıcı rolü üyeliğini denetlemek ve bir AzMan ilke deposuna yönelik belirli işlemleri gerçekleştirmek için rol yetkilendirmek üzere ASP.NET Rol Yöneticisi API 'siyle birlikte nasıl kullanacağınız gösterilmektedir. Nasıl yapılır...

[ASP.NET 2,0 ' de üyelik kullanma](https://msdn.microsoft.com/library/ms998347.aspx)

Bu, ASP.NET sürüm 2,0 uygulamalarında üyelik özelliğinin nasıl kullanılacağını gösterir. İki farklı üyelik sağlayıcısını nasıl kullanacağınızı gösterir: ActiveDirectoryMembershipProvider ve SqlMembershipProvider. Üyelik özelliği...

[ASP.NET 2,0 ' de rol yöneticisini kullanma](https://msdn.microsoft.com/library/ms998314.aspx)

Bu, ASP.NET 2,0 rol yöneticisini nasıl kullanacağınızı gösterir. Rol Yöneticisi, rolleri yönetme ve uygulamanızda rol tabanlı yetkilendirme gerçekleştirme görevini kolaylaştırır. Çeşitli rol sağlayıcılarının ile kullanılmak üzere nasıl yapılandırılacağını gösterir...

[ASP.NET 2,0 ' de Windows kimlik doğrulamasını kullanma](https://msdn.microsoft.com/library/ms998358.aspx)

Bu şekilde, Windows kimlik doğrulamasının bir ASP.NET Web uygulamasında nasıl yapılandırılacağı ve kullanılacağı gösterilmektedir. Windows kimlik doğrulaması, kullanıcılar Windows etki alanının bir parçası olduğunda tercih edilen yaklaşımdır. Bu yaklaşım, mevcut bir kimlik deposunu kullanmanıza olanak sağlar...

[Yönetilen kod için bir güvenlik kodu Incelemesi gerçekleştirin (temel etkinlik)](https://msdn.microsoft.com/library/ms998364.aspx)

Bu, güvenlik kodu incelemelerinin nasıl gerçekleştirileceğini gösterir. Bu modül, etkinliğin içinde yer alan adımları ve sonuçlarınızı analiz eden teknikleri gösterir. "Güvenlik sorusu listesi: yönetilen kod (.NET Framework 2,0)" ile bu yöntemi kullanın...

[ASP.NET 2,0 için bir güvenlik dağıtımı Incelemesi gerçekleştirme](https://msdn.microsoft.com/library/ms998367.aspx)

Bu, uygunsuz yapılandırma ayarları tarafından tanıtılan olası güvenlik açıklarını belirlemek için bir ASP.NET 2,0 uygulaması için nasıl güvenlik dağıtımı incelemesinin gerçekleştirileceğini gösterir. İnceleme işleminin çoğunluğu şunları içerir...

[Windows 2000 için Kerberos temsilcisini uygulama](https://msdn.microsoft.com/library/aa302400.aspx)

Kerberos temsili, bir uygulamanın birden fazla fiziksel katmanında kimlik doğrulamalı bir kimliği, aşağı akış kimlik doğrulamasını ve yetkilendirmeyi desteklemek için Flow olanağı sağlar. Bu, bu işi yapmak için gereken yapılandırma adımlarını gösterir.

[ASP.NET 2,0 'de kimliğe bürünme ve temsili kullanma](https://msdn.microsoft.com/library/ms998351.aspx)

Bu, ASP.NET 2,0 uygulamalarında kimliğe bürünme özelliğini nasıl ve ne zaman kullanacağınızı gösterir. Varsayılan olarak, kimliğe bürünme devre dışıdır ve ASP.NET Web uygulamasının işlem kimliğini kullanarak kaynaklara erişebilirsiniz. Ancak, kullanabilirsiniz...

[Tasarım zamanında bir Web uygulaması için tehdit modeli oluşturma](https://msdn.microsoft.com/library/ms978527.aspx)

Bu, bir Web uygulaması için tehdit modeli oluşturma yaklaşımını açıklar. Tehdit modelleme etkinliği, yatırım yapmadan önce olası güvenlik tasarımı kusurını ve güvenlik açıklarını açığa çıkarmak için güvenlik tasarımınızı modellemenize yardımcı olur...

### <a name="forms-authentication"></a>Forms Kimlik Doğrulaması

[ASP.NET 2,0 'de form kimlik doğrulamasını koruma](https://msdn.microsoft.com/library/ms998310.aspx)

Bu, ASP.NET 2,0 uygulamalarıyla Forms kimlik doğrulamasını nasıl güvenli bir şekilde yapılandıracağınızı ve kullanacağınızı gösterir. Göz önünde bulundurulması gereken önemli etkenler, kimlik doğrulama biletinin güvenli bir şekilde güvenliğini sağlar ve Kullanıcı kimlik deposunun ve bu depoya erişimin güvenliğini sağlar. ...

[ASP.NET 2,0 ' de Active Directory ile Forms kimlik doğrulaması kullanma](https://msdn.microsoft.com/library/ms998360.aspx)

Bu, ActiveDirectoryMembershipProvider kullanarak Forms kimlik doğrulamasının Microsoft® Active Directory® dizin hizmeti ile nasıl kullanılacağını gösterir. Sağlayıcıyı nasıl yapılandıracağınızı ve Kullanıcı oluşturma ve kimlik doğrulama işlemlerinin nasıl yapılacağı gösterilmektedir....

[ASP.NET 2,0 ' de birden çok etki alanında Active Directory ile form kimlik doğrulaması kullanma](https://msdn.microsoft.com/library/ms998345.aspx)

Bu, ActiveDirectoryMembershipProvider kullanarak Forms kimlik doğrulamasının Microsoft® Active Directory® dizin hizmeti ile nasıl kullanılacağını gösterir. Sağlayıcıyı nasıl yapılandıracağınızı ve Kullanıcı oluşturma ve kimlik doğrulama işlemlerinin nasıl yapılacağı gösterilmektedir....

[ASP.NET 2,0 ' de SQL Server ile Forms kimlik doğrulaması kullanma](https://msdn.microsoft.com/library/ms998317.aspx)

Bu, SQL Server üyelik sağlayıcısıyla Forms kimlik doğrulamasını nasıl kullanabileceğinizi gösterir. SQL Server ile form kimlik doğrulaması, uygulamanızın kullanıcılarının Windows etki alanının bir parçası olmadığı ve sonuç olarak,...

[ASP.NET 1,1 'de Forms kimlik doğrulamasıyla GenericPrincipal nesneleri oluşturma](https://msdn.microsoft.com/library/aa302399.aspx)

Bu, Forms kimlik doğrulaması kullanılırken GenericPrincipal ve FormsIdentity nesnelerinin nasıl oluşturulduğunu ve işleneceğini gösterir.

[ASP.NET 1,1 ' de Active Directory ile Forms kimlik doğrulaması kullanma](https://msdn.microsoft.com/library/aa302397.aspx)

Bu nasıl yapılır makalesi, Active Directory kimlik bilgileri deposuna göre form kimlik doğrulamasının nasıl uygulanacağını gösterir.

[ASP.NET 1,1 ' de SQL Server ile Forms kimlik doğrulaması kullanma](https://msdn.microsoft.com/library/aa302398.aspx)

Bu, SQL Server kimlik bilgileri deposuna göre Forms kimlik doğrulamasının nasıl uygulanacağını gösterir. Ayrıca, veritabanında parola dallarını nasıl depolayabileceği de gösterilmektedir.

### <a name="user-input-data-validation"></a>Kullanıcı girişi veri doğrulaması

[İstek Doğrulama - Betik Saldırılarını Önleme](request-validation.md "istek doğrulama")

Bu sayfa, varsayılan olarak uygulamanın sunucuya gönderilen kodlanmamış HTML içeriğini işlemesini engellediği ASP.NET 'in istek doğrulama özelliğini açıklar. Bu istek doğrulama özelliği uygulama olduğunda devre dışı bırakılabilir...

[ASP.NET 'de siteler arası betik oluşturmayı engelle](https://msdn.microsoft.com/library/ms998274.aspx)

Bu, uygun giriş doğrulama tekniklerini kullanarak ve çıktıyı kodlayarak ASP.NET uygulamalarınızı siteler arası betik saldırılarından korumanıza nasıl yardımcı olduğunu gösterir. Ayrıca, içinde kullanabileceğiniz çeşitli koruma mekanizmalarını da açıklar...

[ASP.NET 'de SQL ekleme 'Den koruma](https://msdn.microsoft.com/library/ms998271.aspx)

Bu, ASP.NET uygulamanızı SQL ekleme saldırılarına karşı korumaya yardımcı olmak için çeşitli yollar gösterir. Bir uygulama dinamik SQL deyimlerini oluşturmak için giriş kullandığında veya ' ye bağlanmak için saklı yordamları kullandığında SQL ekleme gerçekleşebilir...

[ASP.NET 'de girişi kısıtlamak için normal Ifadeleri kullanma](https://msdn.microsoft.com/library/ms998267.aspx)

Bu, güvenilmeyen girişi kısıtlamak için ASP.NET uygulamalarında normal ifadeleri nasıl kullanabileceğinizi gösterir. Normal ifadeler ad, adres, telefon numarası ve diğer Kullanıcı bilgileri gibi metin alanlarını doğrulamak için iyi bir yoldur. Kullanabilirsiniz...

### <a name="code-access-security"></a>Kod Erişimi Güvenliği

[ASP.NET 2,0 ' de kod erişim güvenliğini kullanma](https://msdn.microsoft.com/library/ms998326.aspx)

Bu şekilde, uygulamanız için uygun bir güven düzeyini seçme ve gerektiğinde özel bir güven düzeyi tanımlamak için özel bir ASP.NET kod erişim güvenlik ilkesi dosyası oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. Farklı kod erişimi güvenlik güveni kullanabilirsiniz...

[Özel şifreleme Izni oluşturma](https://msdn.microsoft.com/library/aa302362.aspx)

Bu, Win32® veri koruma API 'sinin (DPAPI) sağladığı yönetilmeyen şifreleme işlevlerine programlı erişimi denetlemek için özel bir kod erişim güvenlik izninin nasıl oluşturulacağını açıklar. Bu özel izni yönetilen DPAPI sarmalayıcısı ile kullan...

[Bir derlemeyi kısıtlamak için kod erişimi güvenlik Ilkesi kullanma](https://msdn.microsoft.com/library/aa302361.aspx)

Yönetici, .NET Framework kodun (derlemelerin) işlemlerini kısıtlamak için kod erişimi güvenlik ilkesini yapılandırabilir. Bu şekilde, bir derlemenin dosya g/ç gerçekleştirme ve kısıtlama yeteneğini kısıtlamak için kod erişimi güvenlik ilkesi 'ni yapılandırırsınız...

### <a name="communications-security"></a>İletişim güvenliği

[Web sunucusunda SSL ayarlama](https://msdn.microsoft.com/library/aa302411.aspx)

İstemci uygulamalarından gelen HTTPS bağlantılarını desteklemek için bir Web sunucusunun SSL için yapılandırılmış olması gerekir. Bu, bir Web sunucusunda SSL 'nin nasıl yapılandırılacağını gösterir.

[Istemci sertifikaları ayarlama](https://msdn.microsoft.com/library/aa302412.aspx)

IIS, istemci sertifikası kimlik doğrulamasını destekler. Bu, bir Web uygulamasının istemci sertifikaları gerektirecek şekilde nasıl yapılandırılacağını gösterir. Ayrıca, bir sertifikayı istemci bilgisayara yüklemeyi ve Web uygulamasını çağırırken nasıl kullanacağınızı gösterir.

[Bağlantı noktalarını ve kimlik doğrulamasını filtrelemek için IPSec kullanma](https://msdn.microsoft.com/library/aa302366.aspx)

Internet Protokolü güvenliği (IPSec), IP tabanlı ağ trafiği için şifreleme, bütünlük ve kimlik doğrulama hizmetleri sağlayan bir hizmet değil, bir protokoldür. IPSec sunucudan sunucuya koruma sağladığından, iç tehditleri sayaca yönelik IPSec kullanabilirsiniz...

[Iki sunucu arasında güvenli Iletişim sağlamak için IPSec kullanın](https://msdn.microsoft.com/library/aa302413.aspx)

IPSec, iki sunucu arasında şifrelenmiş kanallar oluşturmanıza olanak tanıyan Windows 2000 tarafından sunulan bir teknolojidir. IPSec, IP trafiğini filtrelemek ve sunucuların kimliğini doğrulamak için kullanılabilir. Bu, IPSec 'i güvenli (şifreli) sağlayacak şekilde nasıl yapılandıracağınızı gösterir...

[SQL Server ile Iletişimi güvenli hale getirmek için SSL kullanma](https://msdn.microsoft.com/library/aa302414.aspx)

Uygulamaların bir SQL Server veritabanı sunucusuna ve bu sunucudan geçirilen verilerin güvenliğini sağlayabilmesi genellikle önemlidir. SQL Server ile, şifreli bir kanal oluşturmak için SSL kullanabilirsiniz. Bu, bir sertifikanın veritabanı sunucusuna nasıl yükleneceğini gösterir,...

[ASP.NET 1,1 ' den Istemci sertifikaları kullanarak bir Web hizmeti çağırma](https://msdn.microsoft.com/library/aa302408.aspx)

Bu, bir ASP.NET Web uygulamasından veya Windows Forms uygulamasından kimlik doğrulaması için bir istemci sertifikasını bir Web hizmetine nasıl geçirebileceğinizi açıklar. İstemci sertifikasını yerel makine deposuna veya Kullanıcı deposuna yükleyebilirsiniz. If...

[ASP.NET 1,1 adresinden SSL kullanarak Web hizmeti çağırma](https://msdn.microsoft.com/library/aa302409.aspx)

Güvenli Yuva Katmanı (SSL) şifreleme, bir Web hizmetinden gelen ve bir Web hizmetine geçirilen iletilerin bütünlüğünü ve gizliliğini güvence altına almak için kullanılabilir. Bu, Web hizmetleriyle SSL 'yi nasıl kullanacağınızı gösterir.

### <a name="cryptography"></a>Şifreleme

[.NET 1,1 'de DPAPI kitaplığı oluşturma](https://msdn.microsoft.com/library/aa302402.aspx)

Bu şekilde, verileri şifrelemek isteyen uygulamalara (örneğin, veritabanı bağlantı dizeleri ve hesap kimlik bilgileri) DPAPI işlevselliği sunan bir yönetilen sınıf kitaplığı oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.

[.NET 1,1 'de şifreleme kitaplığı oluşturma](https://msdn.microsoft.com/library/aa302405.aspx)

Bu, uygulamalar için şifreleme işlevi sağlamak üzere yönetilen bir sınıf kitaplığı oluşturmayı gösterir. Bir uygulamanın şifreleme algoritmasını seçmesine izin verir. Desteklenen algoritmalar DES, Üçlü DES, RC2 ve Rijnbael ' yi içerir.

[ASP.NET 1,1 ' de kayıt defterine şifreli bir bağlantı dizesi depolayın](https://msdn.microsoft.com/library/aa302406.aspx)

Uygulamalar, Windows kayıt defterinde bağlantı dizeleri ve hesap kimlik bilgileri gibi şifrelenmiş verileri depolamayı seçebilir. Bu, kayıt defterinde şifrelenmiş dizelerin nasıl depolanacağını ve alınacağını gösterir.

[ASP.NET 1,1 'ten DPAPI (makine deposu) kullanma](https://msdn.microsoft.com/library/aa302403.aspx)

Bu, hassas verileri şifrelemek için bir ASP.NET Web uygulamasından veya Web hizmetinden DPAPI 'yi nasıl kullanacağınızı gösterir.

[Enterprise Services ile ASP.NET 1,1 'ten DPAPI (Kullanıcı Mağazası) kullanın](https://msdn.microsoft.com/library/aa302404.aspx)

Bu, hassas verileri şifrelemek için bir ASP.NET Web uygulamasından veya hizmetinden DPAPI 'yi nasıl kullanacağınızı gösterir. Bu, bir işlem dışı Enterprise Services bileşeni kullanılmasını gerektiren Kullanıcı deposuyla DPAPI 'yı nasıl kullanır.

<a id="setup"></a>
## <a name="installation-and-setup-whitepapers"></a>Yükleme ve kurulum teknik Incelemeleri

Bu teknik incelemeler, sunucunuza ASP.NET yükleme ve yapılandırmaya yönelik adım adım yönergeler sağlar.

[ASP.NET 2,0 uygulaması için bir hizmet hesabı oluşturma](https://msdn.microsoft.com/library/ms998297.aspx)

Bu, ASP.NET Web uygulaması çalıştırmak için özel bir en düşük ayrıcalıklı hizmet hesabı oluşturmayı ve yapılandırmayı gösterir. Varsayılan olarak, Microsoft Windows Server 2003 ve IIS 6,0 ' deki bir ASP.NET uygulaması yerleşik ağ hizmeti kullanılarak çalışır...

[ASP.NET 2,0 ' de birden çok uygulamayı barındırırken güvenliği geliştirme](https://msdn.microsoft.com/library/aa480478.aspx)

Bu, birden çok uygulamayı bir Web barındırma ortamındaki paylaşılan sistem kaynaklarından farklı bir şekilde nasıl ayırakullanabileceğinizi gösterir. Barındırma ortamı, birden çok barındıran bir Internet servis sağlayıcısı (ISS) tarafından sağlanmış bir Web sunucusu olabilir...

[ASP.NET 2,0 ' de orta düzey güveni kullanma](https://msdn.microsoft.com/library/ms998341.aspx)

Bu, ASP.NET Web uygulamalarının orta güvende çalışacak şekilde nasıl yapılandırılacağını gösterir. Aynı sunucuda birden çok uygulama barındırdıysanız, uygulama yalıtımı sağlamak için kod erişimi güvenliği ve Orta güven düzeyini kullanabilirsiniz. Ayarla...

[ASP.NET 2,0 ' deki kaynaklara erişmek için ağ hizmeti hesabını kullanın](https://msdn.microsoft.com/library/ms998320.aspx)

Bu, yerel ve ağ kaynaklarına erişmek için NT AUTHORITY\Network Service makine hesabını nasıl kullanabileceğinizi gösterir. Windows Server 2003 ' de varsayılan olarak, ASP.NET uygulamalar bu hesabın kimliğini kullanarak çalışır. En az ayrıcalıklı...

[ASP.NET 2,0 'de protokol geçişini ve kısıtlanmış temsilciyi kullanma](https://msdn.microsoft.com/library/ms998355.aspx)

Bu, ASP.NET uygulamanızın özgün çağıran kimliğe bürünme sırasında ağ kaynaklarına erişmesine izin vermek için protokol geçişini ve kısıtlanmış temsilciyi nasıl yapılandıracağınızı ve kullanacağınızı gösterir. Microsoft® Windows® 2000 işletim sistemi...

[ASP.NET .NET Framework 1.0 ve 1.1 Sürümlerini Yan Yana Yürütme](side-by-side-with-10.md "1,0 ile yan yana")

Bu Teknik İnceleme, makinenizde hem .NET 1,0 hem de .NET 1,1 ' nin nasıl yükleneceğini ve bir ASP.NET Web uygulamasının Framework 'ün herhangi bir sürümünde çalışmasına izin verir.

[ASP.NET IIS Dizinlerine Erişim Reddedildi](denied-access-to-iis-directories.md "IIS dizinlerine erişim reddedildi")

Bu teknik incelemede, ASP.NET uygulamanıza yönelik bir istek, " *DirectoryName* dizinine erişim engellendi" hatasını döndürürse ne yapmanız gerektiğini açıklar. Dizin değişikliklerini izleme işlemi başlatılamadı. "

[IIS 6.0 ile Çalışan ASP.NET 1.1](aspnet-and-iis6.md "ASPNET ve IIS6")

Windows Server 2003 hem IIS 6,0 hem de ASP.NET 1,1 içerdiğinde, bu bileşenler varsayılan olarak devre dışıdır. Bu teknik incelemede IIS 6,0 ve ASP.NET 1,1 ' nin nasıl etkinleştirileceği açıklanır ve en iyi şekilde yararlanmak için çeşitli yapılandırma ayarları önerilmektedir...

[IE için güvenlik güncelleştirmesi uygulandıktan sonra ' sunucu uygulaması kullanılamıyor ' hatası için düzeltme](ms03-32-issue.md "MS03-32-sorun")

Bu raporda, Windows XP Professional üzerinde çalışan ASP.NET 1,0 uygulamalarını etkileyen Internet Explorer için MS03-32 güvenlik güncelleştirmesiyle ilgili bir sorunu gideren düzeltme eki açıklanmaktadır.

[ASP.NET 1,1 çalıştırmak Için özel bir hesap oluşturma](https://msdn.microsoft.com/library/aa302396.aspx)

ASP.NET Web uygulamaları, genellikle yerleşik ASPNET hesabını kullanarak çalışır. Bazen bunun yerine özel bir hesap kullanmak isteyebilirsiniz. Bu nasıl yapılır makalesi, ASP.NET Web uygulamalarını çalıştırmak için en az ayrıcalıklı yerel hesap oluşturmayı gösterir. ...

### <a name="configuration"></a>Yapılandırma

[ASP.NET 2,0 ' de makine anahtarını yapılandırma](https://msdn.microsoft.com/library/ms998288.aspx)

Bu, Web. config dosyasında &lt;machineKey&gt; öğesini açıklar ve ViewState, form kimlik doğrulama biletlerinin ve rol tanımlama bilgilerinin üzerinde oynanmaya ve şifrelenmesini denetlemek için &lt;machineKey&gt; öğesinin nasıl yapılandırılacağını gösterir. Görünüm durumu imzalandı...

[DPAPI kullanarak ASP.NET 2,0 içindeki yapılandırma bölümlerini şifreleme](https://msdn.microsoft.com/library/ms998280.aspx)

Bu, yapılandırma dosyalarınızın bölümlerini şifrelemek için Windows Data Protection uygulama programlama arabirimi (DPAPI) ile korunan yapılandırma sağlayıcısı ve ASPNET\_regııs. exe aracının nasıl kullanılacağını gösterir. ASPNET\_regııs. exe aracını şu şekilde kullanabilirsiniz...

[ASP.NET 2,0 içindeki yapılandırma bölümlerini RSA kullanarak şifreleme](https://msdn.microsoft.com/library/ms998283.aspx)

Bu, yapılandırma dosyalarınızın bölümlerini şifrelemek için RSA korumalı yapılandırma sağlayıcısı ve ASPNET\_regııs. exe aracının nasıl kullanılacağını gösterir. ASPNET\_regııs. exe aracını kullanarak, bağlantı dizeleri gibi hassas verileri şifreleyebilirsiniz...

[ASP.NET 2,0 'de kimliğe bürünme ve temsili kullanma](https://msdn.microsoft.com/library/ms998351.aspx)

Bu, ASP.NET 2,0 uygulamalarında kimliğe bürünme özelliğini nasıl ve ne zaman kullanacağınızı gösterir. Varsayılan olarak, kimliğe bürünme devre dışıdır ve ASP.NET Web uygulamasının işlem kimliğini kullanarak kaynaklara erişebilirsiniz. Ancak, kullanabilirsiniz...

<a id="sql"></a>
## <a name="sql-server-whitepapers"></a>SQL Server Teknik Incelemeler

ASP.NET, çeşitli veritabanlarıyla çalışırken, bu teknik incelemeler özellikle ASP.NET uygulamalarını SQL Server 'e bağlamayı de göz atalım.

[ASP.NET 2,0 ' de SQL kimlik doğrulaması kullanarak SQL Server bağlanma](https://msdn.microsoft.com/library/ms998300.aspx)

Bu, veritabanı erişimi kimlik doğrulaması yerel SQL kimlik doğrulaması kullandığında bir ASP.NET uygulamasının Microsoft®™ SQL Server güvenli bir şekilde nasıl bağlanacağını gösterir. Windows kimlik doğrulaması, SQL Server bağlanmak için önerilen yoldur...

[ASP.NET 2,0 ' de Windows kimlik doğrulaması kullanarak SQL Server bağlanma](https://msdn.microsoft.com/library/ms998292.aspx)

Bu, ASP.NET sürüm 2,0 uygulamasından bir Windows hizmet hesabı kullanarak 2000 SQL Server nasıl bağlanagösterdiğini gösterir. ' De kimlik bilgilerini depolamayı önlemenize olanak sağladığından, mümkün olduğunda SQL kimlik doğrulaması yerine Windows kimlik doğrulaması kullanmanız gerekir...

[SQL Server 2000 ile Iletişimi güvenli hale getirmek için SSL kullanma](https://msdn.microsoft.com/library/aa302414.aspx)

Uygulamaların bir SQL Server veritabanı sunucusuna ve bu sunucudan geçirilen verilerin güvenliğini sağlayabilmesi genellikle önemlidir. SQL Server ile, şifreli bir kanal oluşturmak için SSL kullanabilirsiniz. Bu, nasıl bir sertifikanın veritabanı sunucusuna yükleneceğini gösterir,...

<a id="general"></a>
## <a name="general-whitepapers"></a>Genel Teknik Incelemeler

Aşağıdaki örnek durum incelemesi, Microsoft 'un .NET Community Web sitelerini geleneksel bir barındırma ortamından Microsoft Azure geçirmek için kullanılan süreci açıklar.

[Microsoft 'un ASP.NET ve IIS.NET Community Web sitelerini Microsoft Azure 'e geçirme](https://go.microsoft.com/fwlink/?LinkId=400656)

Bu teknik incelemeler, ASP.NET ile ilgili çeşitli konuları kapsar.

[ASP.NET 2,0 'de sistem durumu Izlemeyi kullanma](https://msdn.microsoft.com/library/ms998306.aspx)

Bu, uygulamanızı özel bir olay için işaretlemek üzere durum izlemeyi nasıl kullanacağınızı gösterir. Özel bir sistem durumu izleme olayı oluşturmak için, System. Web. Management. WebBaseEvent öğesinden türeten bir sınıf oluşturun, &lt;healthMonitoring&gt; yapılandırın...

[Yama yönetimini Uygula](https://msdn.microsoft.com/library/aa302364.aspx)

Bu, tek veya birden çok sunucuyu güncel tutma dahil olmak üzere düzeltme eki yönetimi açıklanmaktadır. Microsoft 'tan yüklenebilecek araçlar dışında ek yazılımlar gerekli değildir. İşlemler ve güvenlik ilkesi bir yama yönetimini benimsemelidir...

[Silverlight 3 SDK 'da Silverlight için ASP.NET Server denetimleri](https://go.microsoft.com/fwlink/?LinkId=153377)

ASP.NET MediaPlayer ve Silverlight denetimleri olan Silverlight için ASP.NET sunucu denetimleri ("ASP.NET Silverlight denetimleri"), Silverlight sürüm 3 için Silverlight SDK 'dan kaldırılmıştır. Bu belge, bu ASP.NET ile çalışan geliştiriciler için rehberlik sağlar...

[Yüksek performanslı web uygulamaları oluşturma](https://devexpress.com/act)

Yüksek performanslı web uygulamaları oluşturmak için ASP.NET Ajax Kitaplığı 'ndaki yeni özellikleri nasıl kullanacağınızı öğrenin
