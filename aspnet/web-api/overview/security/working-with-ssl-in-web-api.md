---
uid: web-api/overview/security/working-with-ssl-in-web-api
title: Web API 'de SSL ile çalışma | Microsoft Docs
author: MikeWasson
description: SSL istemci sertifikaları kullanma da dahil olmak üzere ASP.NET Web API 'SI ile SSL 'nin nasıl kullanılacağını gösterir.
ms.author: riande
ms.date: 02/22/2019
ms.assetid: 97f6164f-59cf-45c0-b820-e4aa29b45396
msc.legacyurl: /web-api/overview/security/working-with-ssl-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 31589b3713b1f1a9b98d12906bfef81f8bf5e3f9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598639"
---
# <a name="working-with-ssl-in-web-api"></a>Web API'de SSL ile çalışma

, [Mike te son](https://github.com/MikeWasson)

Birkaç ortak kimlik doğrulama şeması, düz HTTP üzerinden güvenli değildir. Özellikle, temel kimlik doğrulaması ve Forms kimlik doğrulaması şifrelenmemiş kimlik bilgileri gönderir. Güvenli olması için, bu kimlik doğrulama düzenlerinin SSL kullanması *gerekir* . Buna ek olarak, SSL istemci sertifikaları istemcilerin kimliğini doğrulamak için de kullanılabilir.

## <a name="enabling-ssl-on-the-server"></a>Sunucuda SSL Etkinleştiriliyor

IIS 7 veya sonraki sürümlerde SSL ayarlamak için:

- Bir sertifika oluşturun veya alın. Test için otomatik olarak imzalanan bir sertifika oluşturabilirsiniz.
- Bir HTTPS bağlaması ekleyin.

Ayrıntılar için bkz. [IIS 7 ' de SSL ayarlama](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).

Yerel test için, Visual Studio 'dan IIS Express SSL 'yi etkinleştirebilirsiniz. Özellikler penceresi **SSL etkin** ' i **true**olarak ayarlayın. **SSL URL 'si**değerini aklınızda edin; HTTPS bağlantılarını test etmek için bu URL 'YI kullanın.

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a>Web API denetleyicisinde SSL zorlama

Hem HTTPS hem de HTTP bağlamaya sahipseniz, istemciler siteye erişmek için yine de HTTP kullanmaya devam edebilir. Bazı kaynakların HTTP üzerinden kullanılabilir olmasını, diğer kaynaklar da SSL gerektirmesini sağlayabilirsiniz. Bu durumda, korunan kaynaklar için SSL istemek üzere bir eylem filtresi kullanın. Aşağıdaki kod, SSL 'yi denetleyen bir Web API kimlik doğrulama filtresi gösterir:

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

Bu filtreyi SSL gerektiren herhangi bir Web API eylemlerine ekleyin:

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a>SSL Istemci sertifikaları

SSL, ortak anahtar altyapısı sertifikalarını kullanarak kimlik doğrulaması sağlar. Sunucu, istemci için sunucunun kimliğini doğrulayan bir sertifika sağlamalıdır. İstemcinin sunucuya sertifika sağlaması daha yaygındır, ancak bu, istemcilerin kimliğini doğrulamak için bir seçenektir. İstemci sertifikalarını SSL ile kullanmak için, imzalı sertifikaları kullanıcılarınıza dağıtmak için bir yol gerekir. Birçok uygulama türü için bu, iyi bir kullanıcı deneyimi olmayacaktır, ancak bazı ortamlarda (örneğin, kuruluş) uygulanabilir olabilir.

| Yararları | Dezavantajlar |
| --- | --- |
| -Sertifika kimlik bilgileri, Kullanıcı adı/paroladan daha güçlüdür. -SSL, kimlik doğrulama, ileti bütünlüğü ve ileti şifreleme ile tam bir güvenli kanal sağlar. | -PKI sertifikalarını edinmeniz ve yönetmeniz gerekir. -İstemci platformun SSL istemci sertifikalarını desteklemesi gerekir. |

IIS 'yi istemci sertifikalarını kabul edecek şekilde yapılandırmak için, IIS Yöneticisi 'Ni açın ve aşağıdaki adımları gerçekleştirin:

1. Ağaç görünümündeki site düğümüne tıklayın.
2. Orta bölmedeki **SSL ayarları** özelliğine çift tıklayın.
3. **Istemci sertifikaları**' nın altında şu seçeneklerden birini seçin: 

    - **Kabul et**: IIS istemciden bir sertifikayı kabul eder, ancak bir sertifika gerektirmez.
    - **Gerektir**: istemci sertifikası gerektir. (Bu seçeneği etkinleştirmek için "SSL gerektir" seçeneğini de seçmeniz gerekir.

ApplicationHost. config dosyasında da bu seçenekleri ayarlayabilirsiniz:

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

**SslNegotiateCert** bayrağı, IIS 'nin istemciden bir sertifikayı kabul etmesi, ancak bir tane (IIS Yöneticisi 'Nde "kabul etme" seçeneğine denktir) gerekir. Bir sertifika istemek için **SslRequireCert** bayrağını ayarlayın. Test için, bu seçenekleri yerel ApplicationHost içinde IIS Express de ayarlayabilirsiniz. Yapılandırma dosyası, "Documents\IISExpress\config" konumunda bulunur.

### <a name="creating-a-client-certificate-for-testing"></a>Test için Istemci sertifikası oluşturma

Sınama amacıyla, bir istemci sertifikası oluşturmak için [MakeCert. exe](/windows/desktop/SecCrypto/makecert) ' yi kullanabilirsiniz. İlk olarak, bir test kök yetkilisi oluşturun:

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

MakeCert, özel anahtar için bir parola girmenizi ister.

Ardından, sertifikayı test sunucusunun "güvenilen kök sertifika yetkilileri" deposuna aşağıdaki gibi ekleyin:

1. MMC 'YI açın.
2. **Dosya**altında **ek bileşen Ekle/Kaldır**' ı seçin.
3. **Bilgisayar hesabı**' nı seçin.
4. **Yerel bilgisayar** ' ı seçin ve Sihirbazı doldurun.
5. Gezinti bölmesi altında "güvenilen kök sertifika yetkilileri" düğümünü genişletin.
6. **Eylem** menüsünde, **Tüm görevler**' in üzerine gelin ve ardından **Içeri aktar** ' a tıklayarak Sertifika Alma Sihirbazı ' nı başlatın.
7. TempCA. cer sertifika dosyasına gidin.
8. **Aç**' a tıklayın, ardından **İleri** ' ye tıklayın ve Sihirbazı doldurun. (Parolayı yeniden girmeniz istenir.)

Şimdi ilk sertifika tarafından imzalanmış bir istemci sertifikası oluşturun:

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a>Web API 'de Istemci sertifikalarını kullanma

Sunucu tarafında, istek iletisinde [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) çağırarak istemci sertifikasını alabilirsiniz. Yöntemi, istemci sertifikası yoksa null değerini döndürür. Aksi halde, bir **X509Certificate2** örneği döndürür. Sertifikadan veren ve konu gibi bilgileri almak için bu nesneyi kullanın. Daha sonra bu bilgileri kimlik doğrulaması ve/veya yetkilendirme için kullanabilirsiniz.

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
