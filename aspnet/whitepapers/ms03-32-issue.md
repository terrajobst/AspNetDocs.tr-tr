---
uid: whitepapers/ms03-32-issue
title: IE için güvenlik güncelleştirmesi uygulandıktan sonra ' sunucu uygulaması kullanılamıyor ' hatası için düzeltme | Microsoft Docs
author: rick-anderson
description: Bu yazıda, Wi üzerinde çalışan ASP.NET 1,0 uygulamalarını etkileyen Internet Explorer için MS03-32 güvenlik güncelleştirmesiyle ilgili bir sorunu gideren düzeltme eki açıklanmaktadır...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: e0b6776cbfe22e341ac7105f03daac5074b480fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574188"
---
# <a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>IE için Güvenlik Güncelleştirmesi Uygulandıktan Sonra Oluşan 'Sunucu Uygulaması Kullanılamıyor' Hatasının Çözümü

> Bu raporda, Windows XP Professional üzerinde çalışan ASP.NET 1,0 uygulamalarını etkileyen Internet Explorer için MS03-32 güvenlik güncelleştirmesiyle ilgili bir sorunu gideren düzeltme eki açıklanmaktadır.
> 
> ASP.NET 1,0 ve Windows XP Professional için geçerlidir.

Microsoft, Windows XP 'de çalışan Internet Explorer güvenlik düzeltme eki ve ASP.NET 1,0 için MS03-32 güvenlik güncelleştirmesiyle ilgili bir sorun belirledi. Bu düzeltme eki, el ile veya Windows Update sitesinden son kritik güncelleştirmeler elde edilebilir.

Bu sorunun belirtisi, düzeltme ekini bir Windows XP makinesine yükledikten sonra, yerel IIS 5,1 Web sunucusunda çalışan ASP.NET uygulamalarına yapılan tüm isteklerin "sunucu uygulaması kullanılamıyor" hatasını bildiren bir hata iletisiyle sonuçlanır. Uzak Web sunucularına gönderilen istekler etkilenmemiştir.

Bu sorun yalnızca Windows XP 'de ASP.NET 1,0 çalıştıran yüklemeleri etkiler. Windows 2000 veya Windows Server 2003 çalıştıran makineleri etkilemez. Ayrıca, ASP.NET 1,1 yüklü Windows XP çalıştıran makineleri etkilemez.

Bu **sorunun ASP.net** ile bir güvenlik hatası olmadığına lütfen unutmayın. Bir ASP.NET uygulaması veya sunucusuna karşı kötü amaçlı **saldırıları açmayın veya buna izin vermez.** Bunun yerine, yalnızca düzeltme ekinin kendisi tarafından oluşan işlevsel bir hatadır.

Bu soruna yönelik kalıcı bir çözüm üzerinde çalışıyoruz. Bu sırada, sorun için geçici bir çözüm olarak aşağıdaki toplu iş dosyasını çalıştırabilirsiniz. Toplu iş dosyası şunları yapar:

1. IIS ve ASP.NET durum hizmetlerini durduruyor
2. ASPNET hesabını bilinen geçici bir parolayla siler ve yeniden oluşturur
3. ASPNET Kullanıcı profili oluşturan bir yürütülebilir dosyayı başlatmak için Windows `runas` komutunu kullanır
4. ASP.NET yeniden kaydettirir. Bu, hesap için yeni bir rastgele parola oluşturur ve varsayılan ASP.NET Access Control ayarlarını uygular
5. IIS hizmetini yeniden başlatır

Toplu iş dosyası, toplu iş dosyası çalıştırıldığında RunAs komutuna girmeniz istenecektir, "<strong>1pass\@Word</strong>" adlı bir sabit kodlanmış geçici parola içerir. Runas komutu tamamlandıktan sonra, ASPNET hesap parolası güçlü bir rastgele değerle yeniden oluşturulur. Sabit kodlanmış parola, ortamınızdaki parola karmaşıklığı gereksinimlerini karşılamıyorsa toplu iş dosyasının başarısız olabileceğini unutmayın. Bu durumda, bunu ortamınız için uygun olan başka bir değerle değiştirebilirsiniz.

*> [!IMPORTANT]* ASPNET hesabı için özel erişim denetimi ayarları veya veritabanı hesabı izinleri eklediyseniz, bu toplu iş dosyası tamamlandıktan sonra yeniden oluşturulması gerekir. Bunun nedeni, hesap yeniden oluşturulduğunda yeni bir güvenlik tanımlayıcısı (SID) alır.

*> [!IMPORTANT]* ASP.NET çalışan işlemini ASPNET hesabı dışında bir özel hesapla çalıştırıyorsanız, bu toplu iş dosyasını çalıştırmamalıdır. Bunun yerine, etkileşimli olarak oturum açmanız veya bu hesap için bir kullanıcı profili oluşturacak bu hesapla runas komutunu kullanmanız gerekir.

Toplu iş dosyası aşağıdaki otomatik ayıklama arşivine dahil edilmiştir. Bunu kullanmak için:

1. Yönetici ayrıcalıklarına sahip bir hesap olarak çalıştırmalısınız
2. [Kendiliğinden ayıklanan yürütülebilir dosyayı indirin ve açın](ms03-32-issue/_static/fixup1.exe)
3. İçeriği c:\ ' a ayıklayın
4. Çalıştır 'ı seçin... Başlat menüsünden `cmd.exe` girin.
5. Açık Komut pencereleri içinde `c:\fixup.cmd`yazın.
6. İstendiğinde, parola olarak <strong>1pass\@sözcüğünü</strong> girin.
7. ASPNET hesabı için daha önce özel erişim denetimi ayarları veya veritabanı hesabı izinleriniz varsa, bu ayarları şimdi yeniden uygulamanız gerekir.

Bu sorun nedeniyle özgürlerimizi çok sayıda. Kullanılabilir hale geldiğinde ek bilgiler göndereceğiz.

Aşağıdaki matris, bu sorundan etkilenen platformların ve sürümlerin ayrıntılarını aşağıda bulabilirsiniz.

| .NET Framework | Platform | Etkilenen |
| --- | --- | --- |
| Sürüm 1,0 | Windows 2000 Professional | Hayır |
| Sürüm 1,0 | Windows 2000 Server | Hayır |
| Sürüm 1,0 | Windows XP Professional | Evet |
| Sürüm 1,0 | Windows Server 2003 | Hayır |
| Sürüm 1,0 | Cassini ile Windows XP giriş | Hayır |
| Sürüm 1,1 | Windows 2000 Professional | Hayır |
| Sürüm 1,1 | Windows 2000 Server | Hayır |
| Sürüm 1,1 | Windows XP Professional | Hayır |
| Sürüm 1,1 | Windows Server 2003 | Hayır |
| Sürüm 1,1 | Cassini ile Windows XP giriş | Hayır |

Teşekkür ederiz,   
 ASP.NET ekibi
