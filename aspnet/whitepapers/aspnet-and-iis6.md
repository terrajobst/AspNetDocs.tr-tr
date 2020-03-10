---
uid: whitepapers/aspnet-and-iis6
title: IIS 6,0 ile ASP.NET 1,1 çalıştırma | Microsoft Docs
author: rick-anderson
description: Windows Server 2003 hem IIS 6,0 hem de ASP.NET 1,1 içerdiğinde, bu bileşenler varsayılan olarak devre dışıdır. Bu teknik incelemede IIS 6,0 a 'nın nasıl etkinleştirileceği açıklanmaktadır...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523312"
---
# <a name="running-aspnet-11-with-iis-60"></a>IIS 6.0 ile Çalışan ASP.NET 1.1

> Windows Server 2003 hem IIS 6,0 hem de ASP.NET 1,1 içerdiğinde, bu bileşenler varsayılan olarak devre dışıdır. Bu teknik incelemede IIS 6,0 ve ASP.NET 1,1 ' nin nasıl etkinleştirileceği açıklanır ve IIS ve ASP.NET ' den en iyi performansı elde etmek için çeşitli yapılandırma ayarları önerilmektedir.
> 
> ASP.NET 1,1 ve IIS 6,0 için geçerlidir.

ASP.NET 1,1, Internet Information Server (IIS) sürüm 6,0 ' nin en son sürümünü de içeren Windows Server 2003 ile birlikte gelir. IIS 6,0 ve ASP.NET 1,1, sorunsuz ve ASP.NET Now varsayılan olarak yeni IIS 6,0 çalışan işlem modeliyle tümleştirilecek şekilde tasarlanmıştır.

## <a name="aspnet-11-is-not-installed-by-default"></a>ASP.NET 1,1 varsayılan olarak yüklü değildir

Microsoft 'un sunucu işletim sistemlerinin önceki sürümlerinden farklı olarak Internet Information Server (IIS) varsayılan olarak etkinleştirilmemiştir; ASP.NET 1,1. IIS 'yi etkinleştirmek için iki seçenek vardır:

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a>IIS 'yi etkinleştirme, seçenek #1-Sunucu Yapılandırma Sihirbazı

Windows Server 2003, sunucunuzu istediğiniz modda doğru bir şekilde yapılandırmanıza yardımcı olmak için yeni bir ' Sunucu Yapılandırma Sihirbazı ' ' nı sevk eder.

Sihirbazı başlatmak için, Sihirbazı çalıştırmak üzere yönetici olarak oturum açmış olmanız gerekir; şuraya gidin: Başlat | Programlar | Yönetim Araçları ve ' sunucunuzu yapılandırın ' seçeneğini belirleyin.

' İ seçtikten sonra, ' Sunucu Yapılandırma Sihirbazı ' açma ekranını görmeniz gerekir:

![](aspnet-and-iis6/_static/image1.jpg)

' Ileri &gt;' seçeneğine tıklayın:

![](aspnet-and-iis6/_static/image2.jpg)

' Ileri &gt;' seçeneğine tıklayın

![](aspnet-and-iis6/_static/image3.jpg)

Bu ekranda, yapılandırma seçenekleri olarak ' uygulama sunucusu (IIS, ASP.NET) seçeneğini belirlemeniz gerekir.

' Ileri &gt;' seçeneğine tıklayın.

![](aspnet-and-iis6/_static/image4.jpg)

Sunucuyu bir uygulama sunucusu olarak yapılandırmayı seçtikten sonra bu ekran, hangi ek yeteneklerin yüklenmesi gerektiğine ilişkin istem görüntülenecektir. Hiçbir seçenek varsayılan olarak seçilidir. ASP.NET otomatik olarak etkinleştirmek için, ' ASP 'yi etkinleştir ' i seçmeniz gerekir. NET '.

' Ileri &gt;' seçeneğine tıklayın.

![](aspnet-and-iis6/_static/image5.jpg)

Bu ekran hangi seçeneklerin yükleneceğini gösterir.

' Ileri &gt;' seçeneğine tıklayın.

![](aspnet-and-iis6/_static/image6.jpg)

Seçtiğiniz seçenekler yüklenirken bu ekran görüntülenir. Hizmetler yüklendiği sürece diğer iletişim kutularının görünmesine bakmak normaldir. Ayrıca, Windows 2003 Server yükleme CD 'sinin konumu istenebilir.

Tamamlandığında ' Ileri &gt;' seçeneğine tıklayın.

![](aspnet-and-iis6/_static/image7.jpg)

' Son ' düğmesine tıklayın. Windows Server 2003 artık IIS 6,0 ve ASP.NET 1,1 ' i destekleyecek şekilde yapılandırılmıştır.

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a>IIS, seçenek #2 etkinleştirme-IIS ve ASP.NET El Ile yapılandırma

' Sunucu Yapılandırma Sihirbazı ' nı kullanmak istemiyorsanız, Denetim Masası 'ndan ' Program Ekle veya Kaldır ' öğesini kullanarak IIS 6,0 ve ASP.NET 1,1 ' ü isteğe bağlı olarak yükleyebilirsiniz.

Önce denetim masasını açın:

![](aspnet-and-iis6/_static/image8.jpg)

Sonra ' Windows Bileşenleri Sihirbazı ' ' nı açacak ' Windows Bileşenlerini Ekle/Kaldır ' seçeneğine tıklayın:

![](aspnet-and-iis6/_static/image9.jpg)

' Uygulama sunucusu ' nu vurgulayın ve denetleyin ve sonra ' Ayrıntılar? ' düğmesine tıklayın Bu

![](aspnet-and-iis6/_static/image10.jpg)

ASP.NET yüklemek için, ' ASP ' yi kontrol edin. NET '.

Windows Bileşen sihirbazına dönmek için ' Tamam 'a tıklayın. Yüklemeye başlamak için Windows Bileşen Sihirbazı 'nda ' Ileri &gt;' seçeneğine tıklayın:

![](aspnet-and-iis6/_static/image11.jpg)

Hizmetler yüklendiği sürece diğer iletişim kutularının görünmesine bakmak normaldir. Ayrıca, Windows 2003 Server yükleme CD 'sinin konumu istenebilir.

Yükleme tamamlandığında, Windows Bileşen Sihirbazı 'nın son ekranını görürsünüz:

![](aspnet-and-iis6/_static/image12.jpg)

IIS 6,0 ve ASP.NET 1,1 artık yapılandırılmıştır ve kullanılabilir.

## <a name="recommended-settings"></a>Önerilen ayarlar

IIS 6,0 ile ASP.NET 1,1 çalıştırılırken, ASP.NET adresinden en iyi performansı elde etmek için önerilen birkaç yapılandırma ayarı vardır:

- Çalışan işlem belleği sınırlarını yapılandırma
- Çalışan işlemi geri dönüşümünü yapılandırma

### <a name="configuring-worker-process-memory-limits"></a>Çalışan işlem belleği sınırlarını yapılandırma

Varsayılan olarak IIS 6,0, IIS 'nin kullanmasına izin verilen bellek miktarı için bir sınır yapmaz. ASP.net. NET ' in önbellek özelliği bir bellek sınırlaması kullanır, bu sayede önbelleğin kullanılmayan öğeleri bellekten önceden kaldırabilmesini sağlayabilirsiniz.

IIS 6,0 'nin bellek geri dönüştürme özelliğini yapılandırmanız önerilir. Bu açık Internet Information Services yöneticisini yapılandırmak için (Başlat | Programlar | Yönetim Araçları | Internet Information Services). ' İ açtıktan sonra ' uygulama havuzları ' klasörünü genişletin:

Her uygulama havuzu için:

![](aspnet-and-iis6/_static/image13.jpg)

1. Uygulama havuzuna sağ tıklayın, örn. ' DefaultAppPool ' ve ' Özellikler ' öğesini seçin:

![](aspnet-and-iis6/_static/image14.jpg)

2. Daha sonra, ' en fazla kullanılan bellek ' i (megabayt cinsinden) tıklatarak belleği geri dönüştürmeyi etkinleştirin. Değer, sunucudaki fiziksel (sanal değil) bellek miktarından daha fazla olmamalıdır; Örneğin, 512 MB fiziksel belleği olan bir sunucu için, yaklaşık olarak %60, fiziksel belleğin% ' i 310 seçin. 2 GB 'LIK bir adres alanı kullanırken en fazla 800MB 'yi aşmamalıdır. Sunucunun bellek adres alanı 3GB ise, çalışan işlem için en fazla bellek sınırı 1, 800MB olarak yüksek olabilir:

![](aspnet-and-iis6/_static/image15.jpg)

Özellikler iletişim kutusundan çıkmak için ' Uygula ' ve ' Tamam ' seçeneğine tıklayın. Bunu, kullanılabilir tüm uygulama havuzları için tekrarlayın.

### <a name="configuring-worker-recycling"></a>Çalışan geri dönüşümünü yapılandırma

Varsayılan olarak IIS 6,0, çalışan işlemini 29 saatte bir geri dönüştürmek üzere yapılandırılmıştır. Bu, ASP.NET çalıştıran bir uygulama için biraz ısrarlı ve otomatik çalışan işlem geri dönüştürme işleminin devre dışı bırakılması önerilir.

Otomatik çalışan işlemi geri dönüşümünü devre dışı bırakmak için önce Internet Information Services Manager 'ı açın (Başlat | Programlar | Yönetim Araçları | Internet Information Services). ' İ açtıktan sonra ' uygulama havuzları ' klasörünü genişletin:

![](aspnet-and-iis6/_static/image16.jpg)

Her uygulama havuzu için:

1. Uygulama havuzuna sağ tıklayın, örn. ' DefaultAppPool ' ve ' Özellikler ' öğesini seçin:

![](aspnet-and-iis6/_static/image17.jpg)

2. ' Çalışan işlemini geri kazan (dakika): ' işaretini kaldırın:

![](aspnet-and-iis6/_static/image18.jpg)

Özellikler iletişim kutusundan çıkmak için ' Uygula ' ve ' Tamam ' seçeneğine tıklayın. Bunu, kullanılabilir tüm uygulama havuzları için tekrarlayın.

## <a name="granting-write-access-to-the-file-system"></a>Dosya sistemine yazma erişimi verme

Uygulamanız dosya sistemine yazma erişimi gerektiriyorsa ve NTFS kullanıyorsanız, ASP.NET erişimi sağlamak için klasör veya dosya üzerinde bir Access Control listesini (ACL) değiştirmeniz gerekir.

Örneğin, c:\ınetpub\wwwroot ilk kez açık gezgin 'e ASP.NET yazma erişimi vermek ve dizine gitmek için:

![](aspnet-and-iis6/_static/image19.jpg)

Ardından, dizine sağ tıklayıp, örneğin ' Wwwroot ' ve Özellikler ' i seçin. Özellikler iletişim kutusu açıldıktan sonra ' Güvenlik ' sekmesini seçin:

![](aspnet-and-iis6/_static/image20.jpg)

C:\Inetpub\Wwwroot\ Dizin, ' IIS\_WPG ' özel IIS 6,0 grubunun zaten okuma &amp; yürütme, klasör Içeriğini listeleme ve okuma izinleri vermiş olduğu özel bir dizindir. Bununla birlikte, yazma izni vermek için, yazma için Izin ver onay kutusuna tıklamanız gerekir:

![](aspnet-and-iis6/_static/image21.jpg)

IIS 6,0 artık bu klasörde yazma iznine sahiptir. Diğer klasörlerde yazma izinleri vermek için, bu adımları izleyin, zaten yoksa IIS\_WPG grubunu eklemeniz gerekebileceğini göz önünde bulabilirsiniz.

> [!CAUTION]
> IIS\_WPG 'ye yazma izni verilmesi, tüm ASP.NET uygulamalarının bu dizine yazmasına izin verir.

## <a name="supporting-integrated-authentication-with-sql-server"></a>SQL Server ile tümleşik kimlik doğrulamayı destekleme

Tümleşik kimlik doğrulaması, SQL Server SQL Server oturum açma hesaplarını doğrulamak için Windows NT kimlik doğrulamasının yararlanmasını sağlar. Bu, kullanıcının standart SQL Server oturum açma işlemini atlamasına izin verir. Bu yaklaşımda, SQL Server Windows NT ağ güvenlik işlemindeki Kullanıcı ve parola bilgilerini elde ettiğinden, bir ağ kullanıcısı ayrı bir oturum açma kimliği veya parola sağlamadan SQL Server veritabanına erişebilir.

Uygulamanız için bağlantı dizeniz içinde hiçbir kimlik bilgisi depolanmadığından, ASP.NET uygulamaları için tümleşik kimlik doğrulaması seçme iyi bir seçimdir. Bunun yerine, SQL 'e bağlanmak için kullanılan bağlantı dizesi aşağıdaki gibi görünür:

`"server=localhost; database=Northwind;Trusted_Connection=true"`

Bu bağlantı dizesi, SQL Server SQL Server erişmeye çalışan uygulamanın Windows kimlik bilgilerini kullanmasını söyler. ASP.NET/IIS 6 durumunda bu, IIS\_WPG grubunda bir hesap olabilir.

SQL Server ve ASP.NET arasında tümleşik kimlik doğrulamasını etkinleştirmek için öncelikle SQL Server tümleşik kimlik doğrulaması veya karma mod kimlik doğrulaması için yapılandırılmış olduğundan emin olmanız gerekir. bunu öğrenmek için SQL Server bu iki moddan birinde ise, tümleşik kimlik doğrulaması kullanabilirsiniz.

SQL Server Enterprise Yöneticisi 'Ni açın (Başlat | Programlar | Microsoft SQL Server | Enterprise Manager), uygun sunucuyu seçin ve Güvenlik klasörünü genişletin:

![](aspnet-and-iis6/_static/image22.jpg)

' BUıLT\ııS\_WPG ' grubu listelenmiyorsa, oturum açma bilgileri ' ne sağ tıklayın ve ' yeni Login' ' ı seçin:

![](aspnet-and-iis6/_static/image23.jpg)

' Name: ' metin kutusunda ' [sunucu/etki alanı adı] \ııS\_WPG ' girin veya Windows NT Kullanıcı/Grup seçicisini açmak için üç nokta düğmesine tıklayın:

![](aspnet-and-iis6/_static/image24.jpg)

Geçerli makinenin IIS\_WPG grubunu seçin ve seçiciyi kapatmak için ' Ekle ' ve Tamam ' ı tıklatın.

Daha sonra, varsayılan veritabanını ve veritabanına erişmek için izinleri de ayarlamanız gerekir. Varsayılan Veritabanı Seç ' i açılan listeden seçin. Örneğin, Northwind 'nin altında:

![](aspnet-and-iis6/_static/image25.jpg)

Ardından, veritabanı erişimi sekmesine tıklayın:

![](aspnet-and-iis6/_static/image26.jpg)

Erişimine izin vermek istediğiniz her veritabanı için Izin ver onay kutusuna tıklayın. Ayrıca, veritabanı rolleri ' ni seçmeniz gerekir. veritabanı\_sahibi, oturum açma izninizin seçili veritabanını yönetmek ve kullanmak için gereken tüm izinlere sahip olduğundan emin olur.

Özellik iletişim kutusundan çıkmak için Tamam ' ı tıklatın. ASP.NET uygulamanız artık tümleşik SQL Server kimlik doğrulamasını destekleyecek şekilde yapılandırılmıştır.

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a>IIS 6,0 Native modda ASP.NET 1,0 çalıştırma

IIS 6,0 üzerinde ASP.NET 1,0 yalnızca IIS 5 uyumluluk modunda desteklenir.

ASP.NET 1,0 'i IIS 5,0 uyumluluk modunda çalışacak şekilde yapılandırmak için İnternet Hizmetleri Yöneticisi açın ve Web siteleri ' ne sağ tıklayıp Özellikler ' i seçin:

![](aspnet-and-iis6/_static/image27.jpg)

Hizmet sekmesine geçip emin misiniz? WWW hizmetini IIS 5,0 yalıtım modunda çalıştırın mi?:

![](aspnet-and-iis6/_static/image28.jpg)
