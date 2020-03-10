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
# <a name="working-with-ssl-in-web-api"></a><span data-ttu-id="f8ea8-103">Web API'de SSL ile çalışma</span><span class="sxs-lookup"><span data-stu-id="f8ea8-103">Working with SSL in Web API</span></span>

<span data-ttu-id="f8ea8-104">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f8ea8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="f8ea8-105">Birkaç ortak kimlik doğrulama şeması, düz HTTP üzerinden güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-105">Several common authentication schemes are not secure over plain HTTP.</span></span> <span data-ttu-id="f8ea8-106">Özellikle, temel kimlik doğrulaması ve Forms kimlik doğrulaması şifrelenmemiş kimlik bilgileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-106">In particular, Basic authentication and forms authentication send unencrypted credentials.</span></span> <span data-ttu-id="f8ea8-107">Güvenli olması için, bu kimlik doğrulama düzenlerinin SSL kullanması *gerekir* .</span><span class="sxs-lookup"><span data-stu-id="f8ea8-107">To be secure, these authentication schemes *must* use SSL.</span></span> <span data-ttu-id="f8ea8-108">Buna ek olarak, SSL istemci sertifikaları istemcilerin kimliğini doğrulamak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-108">In addition, SSL client certificates can be used to authenticate clients.</span></span>

## <a name="enabling-ssl-on-the-server"></a><span data-ttu-id="f8ea8-109">Sunucuda SSL Etkinleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="f8ea8-109">Enabling SSL on the Server</span></span>

<span data-ttu-id="f8ea8-110">IIS 7 veya sonraki sürümlerde SSL ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-110">To set up SSL in IIS 7 or later:</span></span>

- <span data-ttu-id="f8ea8-111">Bir sertifika oluşturun veya alın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-111">Create or get a certificate.</span></span> <span data-ttu-id="f8ea8-112">Test için otomatik olarak imzalanan bir sertifika oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-112">For testing, you can create a self-signed certificate.</span></span>
- <span data-ttu-id="f8ea8-113">Bir HTTPS bağlaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-113">Add an HTTPS binding.</span></span>

<span data-ttu-id="f8ea8-114">Ayrıntılar için bkz. [IIS 7 ' de SSL ayarlama](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span><span class="sxs-lookup"><span data-stu-id="f8ea8-114">For details, see [How to Set Up SSL on IIS 7](https://www.iis.net/learn/manage/configuring-security/how-to-set-up-ssl-on-iis).</span></span>

<span data-ttu-id="f8ea8-115">Yerel test için, Visual Studio 'dan IIS Express SSL 'yi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-115">For local testing, you can enable SSL in IIS Express from Visual Studio.</span></span> <span data-ttu-id="f8ea8-116">Özellikler penceresi **SSL etkin** ' i **true**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-116">In the Properties window, set **SSL Enabled** to **True**.</span></span> <span data-ttu-id="f8ea8-117">**SSL URL 'si**değerini aklınızda edin; HTTPS bağlantılarını test etmek için bu URL 'YI kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-117">Note the value of **SSL URL**; use this URL for testing HTTPS connections.</span></span>

![](working-with-ssl-in-web-api/_static/image1.png)

### <a name="enforcing-ssl-in-a-web-api-controller"></a><span data-ttu-id="f8ea8-118">Web API denetleyicisinde SSL zorlama</span><span class="sxs-lookup"><span data-stu-id="f8ea8-118">Enforcing SSL in a Web API Controller</span></span>

<span data-ttu-id="f8ea8-119">Hem HTTPS hem de HTTP bağlamaya sahipseniz, istemciler siteye erişmek için yine de HTTP kullanmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-119">If you have both an HTTPS and an HTTP binding, clients can still use HTTP to access the site.</span></span> <span data-ttu-id="f8ea8-120">Bazı kaynakların HTTP üzerinden kullanılabilir olmasını, diğer kaynaklar da SSL gerektirmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-120">You might allow some resources to be available through HTTP, while other resources require SSL.</span></span> <span data-ttu-id="f8ea8-121">Bu durumda, korunan kaynaklar için SSL istemek üzere bir eylem filtresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-121">In that case, use an action filter to require SSL for the protected resources.</span></span> <span data-ttu-id="f8ea8-122">Aşağıdaki kod, SSL 'yi denetleyen bir Web API kimlik doğrulama filtresi gösterir:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-122">The following code shows a Web API authentication filter that checks for SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample1.cs)]

<span data-ttu-id="f8ea8-123">Bu filtreyi SSL gerektiren herhangi bir Web API eylemlerine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-123">Add this filter to any Web API actions that require SSL:</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample2.cs)]

## <a name="ssl-client-certificates"></a><span data-ttu-id="f8ea8-124">SSL Istemci sertifikaları</span><span class="sxs-lookup"><span data-stu-id="f8ea8-124">SSL Client Certificates</span></span>

<span data-ttu-id="f8ea8-125">SSL, ortak anahtar altyapısı sertifikalarını kullanarak kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-125">SSL provides authentication by using Public Key Infrastructure certificates.</span></span> <span data-ttu-id="f8ea8-126">Sunucu, istemci için sunucunun kimliğini doğrulayan bir sertifika sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-126">The server must provide a certificate that authenticates the server to the client.</span></span> <span data-ttu-id="f8ea8-127">İstemcinin sunucuya sertifika sağlaması daha yaygındır, ancak bu, istemcilerin kimliğini doğrulamak için bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-127">It is less common for the client to provide a certificate to the server, but this is one option for authenticating clients.</span></span> <span data-ttu-id="f8ea8-128">İstemci sertifikalarını SSL ile kullanmak için, imzalı sertifikaları kullanıcılarınıza dağıtmak için bir yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-128">To use client certificates with SSL, you need a way to distribute signed certificates to your users.</span></span> <span data-ttu-id="f8ea8-129">Birçok uygulama türü için bu, iyi bir kullanıcı deneyimi olmayacaktır, ancak bazı ortamlarda (örneğin, kuruluş) uygulanabilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-129">For many application types, this will not be a good user experience, but in some environments (for example, enterprise) it may be feasible.</span></span>

| <span data-ttu-id="f8ea8-130">Yararları</span><span class="sxs-lookup"><span data-stu-id="f8ea8-130">Advantages</span></span> | <span data-ttu-id="f8ea8-131">Dezavantajlar</span><span class="sxs-lookup"><span data-stu-id="f8ea8-131">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="f8ea8-132">-Sertifika kimlik bilgileri, Kullanıcı adı/paroladan daha güçlüdür.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-132">- Certificate credentials are stronger than username/password.</span></span> <span data-ttu-id="f8ea8-133">-SSL, kimlik doğrulama, ileti bütünlüğü ve ileti şifreleme ile tam bir güvenli kanal sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-133">- SSL provides a complete secure channel, with authentication, message integrity, and message encryption.</span></span> | <span data-ttu-id="f8ea8-134">-PKI sertifikalarını edinmeniz ve yönetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-134">- You must obtain and manage PKI certificates.</span></span> <span data-ttu-id="f8ea8-135">-İstemci platformun SSL istemci sertifikalarını desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-135">- The client platform must support SSL client certificates.</span></span> |

<span data-ttu-id="f8ea8-136">IIS 'yi istemci sertifikalarını kabul edecek şekilde yapılandırmak için, IIS Yöneticisi 'Ni açın ve aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-136">To configure IIS to accept client certificates, open IIS Manager and perform the following steps:</span></span>

1. <span data-ttu-id="f8ea8-137">Ağaç görünümündeki site düğümüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-137">Click the site node in the tree view.</span></span>
2. <span data-ttu-id="f8ea8-138">Orta bölmedeki **SSL ayarları** özelliğine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-138">Double-click the **SSL Settings** feature in the middle pane.</span></span>
3. <span data-ttu-id="f8ea8-139">**Istemci sertifikaları**' nın altında şu seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-139">Under **Client Certificates**, select one of these options:</span></span> 

    - <span data-ttu-id="f8ea8-140">**Kabul et**: IIS istemciden bir sertifikayı kabul eder, ancak bir sertifika gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-140">**Accept**: IIS will accept a certificate from the client, but does not require one.</span></span>
    - <span data-ttu-id="f8ea8-141">**Gerektir**: istemci sertifikası gerektir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-141">**Require**: Require a client certificate.</span></span> <span data-ttu-id="f8ea8-142">(Bu seçeneği etkinleştirmek için "SSL gerektir" seçeneğini de seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-142">(To enable this option, you must also select "Require SSL")</span></span>

<span data-ttu-id="f8ea8-143">ApplicationHost. config dosyasında da bu seçenekleri ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-143">You can also set these options in the ApplicationHost.config file:</span></span>

[!code-xml[Main](working-with-ssl-in-web-api/samples/sample3.xml)]

<span data-ttu-id="f8ea8-144">**SslNegotiateCert** bayrağı, IIS 'nin istemciden bir sertifikayı kabul etmesi, ancak bir tane (IIS Yöneticisi 'Nde "kabul etme" seçeneğine denktir) gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-144">The **SslNegotiateCert** flag means IIS will accept a certificate from the client, but does not require one (equivalent to the "Accept" option in IIS Manager).</span></span> <span data-ttu-id="f8ea8-145">Bir sertifika istemek için **SslRequireCert** bayrağını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-145">To require a certificate, set the **SslRequireCert** flag.</span></span> <span data-ttu-id="f8ea8-146">Test için, bu seçenekleri yerel ApplicationHost içinde IIS Express de ayarlayabilirsiniz. Yapılandırma dosyası, "Documents\IISExpress\config" konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-146">For testing, you can also set these options in IIS Express, in the local applicationhost.Config file, located in "Documents\IISExpress\config".</span></span>

### <a name="creating-a-client-certificate-for-testing"></a><span data-ttu-id="f8ea8-147">Test için Istemci sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8ea8-147">Creating a Client Certificate for Testing</span></span>

<span data-ttu-id="f8ea8-148">Sınama amacıyla, bir istemci sertifikası oluşturmak için [MakeCert. exe](/windows/desktop/SecCrypto/makecert) ' yi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-148">For testing purposes, you can use [MakeCert.exe](/windows/desktop/SecCrypto/makecert) to create a client certificate.</span></span> <span data-ttu-id="f8ea8-149">İlk olarak, bir test kök yetkilisi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-149">First, create a test root authority:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample4.cmd)]

<span data-ttu-id="f8ea8-150">MakeCert, özel anahtar için bir parola girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-150">Makecert will prompt you to enter a password for the private key.</span></span>

<span data-ttu-id="f8ea8-151">Ardından, sertifikayı test sunucusunun "güvenilen kök sertifika yetkilileri" deposuna aşağıdaki gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-151">Next, add the certificate to the test server's "Trusted Root Certification Authorities" store, as follows:</span></span>

1. <span data-ttu-id="f8ea8-152">MMC 'YI açın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-152">Open MMC.</span></span>
2. <span data-ttu-id="f8ea8-153">**Dosya**altında **ek bileşen Ekle/Kaldır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-153">Under **File**, select **Add/Remove Snap-In**.</span></span>
3. <span data-ttu-id="f8ea8-154">**Bilgisayar hesabı**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-154">Select **Computer Account**.</span></span>
4. <span data-ttu-id="f8ea8-155">**Yerel bilgisayar** ' ı seçin ve Sihirbazı doldurun.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-155">Select **Local computer** and complete the wizard.</span></span>
5. <span data-ttu-id="f8ea8-156">Gezinti bölmesi altında "güvenilen kök sertifika yetkilileri" düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-156">Under the navigation pane, expand the "Trusted Root Certification Authorities" node.</span></span>
6. <span data-ttu-id="f8ea8-157">**Eylem** menüsünde, **Tüm görevler**' in üzerine gelin ve ardından **Içeri aktar** ' a tıklayarak Sertifika Alma Sihirbazı ' nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-157">On the **Action** menu, point to **All Tasks**, and then click **Import** to start the Certificate Import Wizard.</span></span>
7. <span data-ttu-id="f8ea8-158">TempCA. cer sertifika dosyasına gidin.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-158">Browse to the certificate file, TempCA.cer.</span></span>
8. <span data-ttu-id="f8ea8-159">**Aç**' a tıklayın, ardından **İleri** ' ye tıklayın ve Sihirbazı doldurun.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-159">Click **Open**, then click **Next** and complete the wizard.</span></span> <span data-ttu-id="f8ea8-160">(Parolayı yeniden girmeniz istenir.)</span><span class="sxs-lookup"><span data-stu-id="f8ea8-160">(You will be prompted to re-enter the password.)</span></span>

<span data-ttu-id="f8ea8-161">Şimdi ilk sertifika tarafından imzalanmış bir istemci sertifikası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f8ea8-161">Now create a client certificate that is signed by the first certificate:</span></span>

[!code-console[Main](working-with-ssl-in-web-api/samples/sample5.cmd)]

### <a name="using-client-certificates-in-web-api"></a><span data-ttu-id="f8ea8-162">Web API 'de Istemci sertifikalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="f8ea8-162">Using Client Certificates in Web API</span></span>

<span data-ttu-id="f8ea8-163">Sunucu tarafında, istek iletisinde [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) çağırarak istemci sertifikasını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-163">On the server side, you can get the client certificate by calling [GetClientCertificate](https://msdn.microsoft.com/library/system.net.http.httprequestmessageextensions.getclientcertificate.aspx) on the request message.</span></span> <span data-ttu-id="f8ea8-164">Yöntemi, istemci sertifikası yoksa null değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-164">The method returns null if there is no client certificate.</span></span> <span data-ttu-id="f8ea8-165">Aksi halde, bir **X509Certificate2** örneği döndürür.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-165">Otherwise, it returns an **X509Certificate2** instance.</span></span> <span data-ttu-id="f8ea8-166">Sertifikadan veren ve konu gibi bilgileri almak için bu nesneyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-166">Use this object to get information from the certificate, such as the issuer and subject.</span></span> <span data-ttu-id="f8ea8-167">Daha sonra bu bilgileri kimlik doğrulaması ve/veya yetkilendirme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ea8-167">Then you can use this information for authentication and/or authorization.</span></span>

[!code-csharp[Main](working-with-ssl-in-web-api/samples/sample6.cs)]
