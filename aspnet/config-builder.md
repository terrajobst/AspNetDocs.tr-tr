---
uid: config-builder
title: ASP.NET için yapılandırma oluşturucuları
author: rick-anderson
description: Dış kaynaklardaki Web. config değerlerinden farklı kaynaklardan yapılandırma verileri alma hakkında bilgi edinin.
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586759"
---
# <a name="configuration-builders-for-aspnet"></a>ASP.NET için yapılandırma oluşturucuları

, [Stephen Moldova](https://github.com/StephenMolloy) ve [Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

Yapılandırma oluşturucuları, dış kaynaklardan yapılandırma değerlerini almak için ASP.NET uygulamalarına yönelik modern ve çevik bir mekanizma sağlar.

Yapılandırma oluşturucuları:

* .NET Framework 4.7.1 ve üzeri sürümlerde kullanılabilir.
* Yapılandırma değerlerini okumak için esnek bir mekanizma sağlar.
* Bir kapsayıcıya ve bulut odaklı ortama geçiş yaparken uygulamaların temel ihtiyaçlarını ele alırlar.
* , .NET yapılandırma sisteminde daha önce kullanılamayan (örneğin, Azure Key Vault ve ortam değişkenleri) kaynaklardan çizerek yapılandırma verilerinin korunmasını geliştirmek için kullanılabilir.

## <a name="keyvalue-configuration-builders"></a>Anahtar/değer yapılandırma oluşturucuları

Yapılandırma oluşturucuları tarafından işlenebilen yaygın bir senaryo, anahtar/değer düzenlerini izleyen yapılandırma bölümleri için temel bir anahtar/değer değiştirme mekanizması sağlamaktır. Configurationbuilder 'lar .NET Framework kavramı, belirli yapılandırma bölümleri veya desenlerle sınırlı değildir. Ancak, `Microsoft.Configuration.ConfigurationBuilders` ([GitHub](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) içindeki yapılandırma oluşturucuların çoğu anahtar/değer düzeniyle çalışır.

## <a name="keyvalue-configuration-builders-settings"></a>Anahtar/değer yapılandırma oluşturucuları ayarları

Aşağıdaki ayarlar `Microsoft.Configuration.ConfigurationBuilders`içindeki tüm anahtar/değer yapılandırma oluşturucuları için geçerlidir.

### <a name="mode"></a>Mod

Yapılandırma oluşturucuları, yapılandırma sisteminin seçili anahtar/değer öğelerini doldurmak için anahtar/değer bilgilerinin dış kaynağını kullanır. Özellikle, `<appSettings/>` ve `<connectionStrings/>` bölümleri yapılandırma oluşturucularından özel bir işleme alır. Oluşturucular üç modda çalışır:

* `Strict`-varsayılan mod. Bu modda, yapılandırma Oluşturucusu yalnızca iyi bilinen anahtar/değer merkezli yapılandırma bölümlerinde çalışır. `Strict` modu, bölümündeki her anahtarı numaralandırır. Dış kaynakta eşleşen bir anahtar bulunursa:

   * Yapılandırma oluşturucuları, elde edilen yapılandırma bölümündeki değeri dış kaynaktaki değerle değiştirir.
* `Greedy`-Bu mod, `Strict` moduyla yakından ilgilidir. Özgün yapılandırmada zaten var olan anahtarlarla sınırlı olmamak yerine:

  * Yapılandırma oluşturucuları, dış kaynaktaki tüm anahtar/değer çiftlerini elde edilen yapılandırma bölümüne ekler.

* `Expand`-ham XML üzerinde, bir yapılandırma bölümü nesnesine ayrıştırmadan önce çalışır. Bir dizedeki belirteçleri genişletme olarak düşünülebilir. `${token}` düzeniyle eşleşen ham XML dizesinin herhangi bir bölümü, belirteç genişletmesi için bir adaydır. Dış kaynakta karşılık gelen bir değer bulunamazsa, belirteç değiştirilmez. Bu moddaki oluşturucular `<appSettings/>` ve `<connectionStrings/>` bölümlerle sınırlı değildir.

*Web. config* dosyasındaki aşağıdaki biçimlendirme, `Strict` modunda [Environmentconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) 'ı etkinleştirmesine izin verebilir:

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

Aşağıdaki kod, önceki *Web. config* dosyasında gösterilen `<appSettings/>` ve `<connectionStrings/>` okur:

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:

* Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *Web. config* dosyasındaki değerler.
* Ayarlanırsa, ortam değişkeninin değerleri.

Örneğin, `ServiceID` şunları içerir:

* Ortam değişkeni `ServiceID` ayarlanmamışsa, "Web. config 'den ServiceId değeri".
* Ayarlanmışsa `ServiceID` ortam değişkeninin değeri.

Aşağıdaki görüntüde, ortam Düzenleyicisi 'nde ayarlanan önceki *Web. config* dosyası `<appSettings/>` anahtarları/değerleri gösterilmektedir:

![ortam Düzenleyicisi](config-builder/static/env.png)

Note: ortam değişkenlerindeki değişiklikleri görmek için çıkmanız ve Visual Studio 'Yu yeniden başlatmanız gerekebilir.

### <a name="prefix-handling"></a>Önek işleme

Anahtar ön ekleri anahtarları ayarlamayı kolaylaştırabilir, çünkü:

* .NET Framework yapılandırması karmaşıktır ve iç içe geçmiş.
* Dış anahtar/değer kaynakları genellikle temel ve doğası gereği düz niteliktedir. Örneğin, ortam değişkenleri iç içe değildir.

`<appSettings/>` ve `<connectionStrings/>` ortam değişkenleri aracılığıyla yapılandırmaya eklemek için aşağıdaki yaklaşımlardan herhangi birini kullanın:

* Varsayılan `Strict` modundaki `EnvironmentConfigBuilder` ve yapılandırma dosyasında uygun anahtar adları ile. Yukarıdaki kod ve biçimlendirme bu yaklaşımı alır. Bu yaklaşımı kullanarak hem `<appSettings/>` hem de `<connectionStrings/>`**aynı şekilde adlandırılmış anahtarlara sahip olabilirsiniz** .
* Farklı ön ekler ve `stripPrefix`ile `Greedy` modunda iki `EnvironmentConfigBuilder`kullanın. Bu yaklaşımla, uygulama yapılandırma dosyasını güncelleştirmeye gerek duymadan `<appSettings/>` ve `<connectionStrings/>` okuyabilir. Sonraki bölümde, [stripPrefix](#stripprefix), bunun nasıl yapılacağını gösterir.
* Farklı öneklerle `Greedy` modda iki `EnvironmentConfigBuilder`s kullanın. Bu yaklaşımda, anahtar adları ön eke göre farklılık gösterdiğinden yinelenen anahtar adlarına sahip olabilirsiniz.  Örneğin:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

Yukarıdaki biçimlendirme ile, aynı düz anahtar/değer kaynağı iki farklı bölüm için yapılandırmayı doldurmak üzere kullanılabilir.

Aşağıdaki görüntüde, ortam düzenleyicisinde ayarlanan önceki *Web. config* dosyasından `<appSettings/>` ve `<connectionStrings/>` anahtarları/değerleri gösterilmektedir:

![ortam Düzenleyicisi](config-builder/static/prefix.png)

Aşağıdaki kod, önceki *Web. config* dosyasında bulunan `<appSettings/>` ve `<connectionStrings/>` anahtarlar/değerleri okur:

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:

* Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *Web. config* dosyasındaki değerler.
* Ayarlanırsa, ortam değişkeninin değerleri.

Örneğin, önceki *Web. config* dosyasını, önceki ortam Düzenleyicisi görüntüsündeki anahtarları/değerleri ve önceki kodu kullanarak, aşağıdaki değerler ayarlanır:

|  Anahtar              | Değer |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | Env değişkenlerinden AppSetting_ServiceID|
|    AppSetting_default            | Env 'dan değer AppSetting_default |
|       ConnStr_default         | Env ConnStr_default Val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`: Boolean, varsayılan olarak `false`. 

Önceki XML biçimlendirmesi, uygulama ayarlarını bağlantı dizelerinden ayırır, ancak *Web. config* dosyasındaki tüm anahtarların belirtilen öneki kullanmasını gerektirir. Örneğin `AppSetting` ön eki `ServiceID` anahtarına eklenmelidir ("AppSetting_ServiceID"). `stripPrefix`, önek *Web. config* dosyasında kullanılmaz. Ön ek, yapılandırma Oluşturucu kaynağında (örneğin, ortamında) gereklidir. Çoğu geliştiricinin `stripPrefix`kullanacağı tahmin ederiz.

Uygulamalar genellikle ön eki devre dışı bırakır. Aşağıdaki *Web. config* ön eki şeritleri:

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

Önceki *Web. config* dosyasında `default` anahtarı hem `<appSettings/>` hem de `<connectionStrings/>`.

Aşağıdaki görüntüde, ortam düzenleyicisinde ayarlanan önceki *Web. config* dosyasından `<appSettings/>` ve `<connectionStrings/>` anahtarları/değerleri gösterilmektedir:

![ortam Düzenleyicisi](config-builder/static/prefix.png)

Aşağıdaki kod, önceki *Web. config* dosyasında bulunan `<appSettings/>` ve `<connectionStrings/>` anahtarlar/değerleri okur:

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

Yukarıdaki kod, özellik değerlerini şu şekilde ayarlar:

* Anahtarlar ortam değişkenlerinde ayarlanmamışsa, *Web. config* dosyasındaki değerler.
* Ayarlanırsa, ortam değişkeninin değerleri.

Örneğin, önceki *Web. config* dosyasını, önceki ortam Düzenleyicisi görüntüsündeki anahtarları/değerleri ve önceki kodu kullanarak, aşağıdaki değerler ayarlanır:

|  Anahtar              | Değer |
| ----------------- | ------------ |
|     ServiceId           | Env değişkenlerinden AppSetting_ServiceID|
|    {1&gt;default&lt;1}            | Env 'dan değer AppSetting_default |
|    {1&gt;default&lt;1}         | Env ConnStr_default Val|

### <a name="tokenpattern"></a>Tokenmodel

`tokenPattern`: dize, varsayılan olarak `@"\$\{(\w+)\}"`

Oluşturucuların `Expand` davranışı, `${token}`gibi görünen belirteçler için ham XML arar. Arama, varsayılan normal ifade `@"\$\{(\w+)\}"`yapılır. `\w` eşleşen karakter kümesi, XML 'den daha sıkı ve birçok yapılandırma kaynağına izin verir. Belirteç adında `@"\$\{(\w+)\}"` daha fazla karakter gerektiğinde `tokenPattern` kullanın.

`tokenPattern`: dize:

* Geliştiricilerin belirteç eşleştirmesi için kullanılan Regex 'yi değiştirmesine izin verir.
* İyi biçimlendirilmiş, tehlikeli olmayan bir Regex olduğundan emin olmak için doğrulama yapılmaz.
* Bir yakalama grubu içermesi gerekir. Tüm Regex tüm belirteçle eşleşmelidir. İlk yakalama, yapılandırma kaynağında aranacak belirteç adı olmalıdır.

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>Microsoft. Configuration. Configurationoluşturucular içindeki yapılandırma oluşturucuları

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[Environmentconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* Yapılandırma oluşturucuların en kolay olanıdır.
* Ortamdan değerleri okur.
* Ek yapılandırma seçeneklerine sahip değildir.
* `name` öznitelik değeri rastgele.

**Note:** Bir Windows kapsayıcı ortamında, çalışma zamanında ayarlanan değişkenler yalnızca EntryPoint işlem ortamına eklenir. Hizmet olarak çalışan uygulamalar veya giriş noktası olmayan bir işlem, kapsayıcıda bir mekanizmaya eklenmediği sürece bu değişkenleri kullanmaz. [Iıs](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.net](https://github.com/Microsoft/aspnet-docker)tabanlı kapsayıcılar Için, [ServiceMonitor. exe](https://github.com/Microsoft/iis-docker/pull/41) ' nin geçerli sürümü bunu yalnızca *DefaultAppPool* ' de gerçekleştirir. Diğer Windows tabanlı kapsayıcı türevleri, giriş noktası olmayan işlemlere yönelik kendi ekleme mekanizmalarının geliştirilmesi gerekebilir.

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> Kaynak kodundaki parolaları, hassas bağlantı dizelerini veya diğer hassas verileri hiçbir şekilde depolamayin. Üretim gizli dizileri geliştirme veya test için kullanılmamalıdır.

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

Bu yapılandırma Oluşturucusu, [ASP.NET Core gizli bir yöneticiye](/aspnet/core/security/app-secrets)benzer bir özellik sağlar.

[Usersecretsconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) .NET Framework projelerinde kullanılabilir, ancak bir gizli dizi dosyası belirtilmelidir. Alternatif olarak, proje dosyasında `UserSecretsId` özelliğini tanımlayabilir ve ham gizli dizileri dosyayı okumak için doğru konumda oluşturabilirsiniz. Dış bağımlılıkları projenizden tutmak için, gizli dosya XML olarak biçimlendirilir. XML biçimlendirmesi bir uygulama ayrıntısının yanı sıra biçim üzerinde güvenilmemelidir. .NET Core projeleriyle bir *gizlilikler. JSON* dosyası paylaşmanız gerekiyorsa, [Simplejsonconfigbuilder](#simplejsonconfigbuilder)' ı kullanmayı düşünün. .NET Core için `SimpleJsonConfigBuilder` biçimi de bir uygulama ayrıntısı konusunun değiştirilmesini kabul etmelidir.

`UserSecretsConfigBuilder`için yapılandırma öznitelikleri:

* `userSecretsId`-bu, bir XML gizli dizi dosyasını tanımlamak için tercih edilen yöntemdir. Bu tanımlayıcıyı depolamak için `UserSecretsId` proje özelliği kullanan .NET Core ile benzerdir. Dize benzersiz olmalıdır, GUID olması gerekmez. Bu öznitelikle `UserSecretsConfigBuilder`, bu tanımlayıcıya ait bir gizli dizi dosyası için iyi bilinen bir yerel konuma (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) bakar.
* `userSecretsFile`-gizli dizileri içeren dosyayı belirten isteğe bağlı bir öznitelik. `~` karakteri uygulama köküne başvurmak için başlangıçta kullanılabilir. Bu öznitelik veya `userSecretsId` özniteliği gereklidir. Her ikisi de belirtilirse, `userSecretsFile` öncelik alır.
* `optional`: Boolean, varsayılan değer `true`-gizlilikler dosyası bulunamazsa bir özel durumu engeller. 
* `name` öznitelik değeri rastgele.

Gizli dizileri dosyası aşağıdaki biçimdedir:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) [Azure Key Vault](/azure/key-vault/key-vault-whatis)depolanan değerleri okur.

`vaultName` gereklidir (kasanın adı ya da kasadaki bir URI). Diğer öznitelikler, hangi kasanın bağlanacağı konusunda denetime izin verir, ancak yalnızca uygulama `Microsoft.Azure.Services.AppAuthentication`ile çalışan bir ortamda çalışmıyorsa gereklidir. Azure Hizmetleri kimlik doğrulama kitaplığı, mümkünse yürütme ortamından bağlantı bilgilerini otomatik olarak almak için kullanılır. Bağlantı dizesi sağlayarak bağlantı bilgilerini otomatik olarak çekmeyi geçersiz kılabilirsiniz.

* `vaultName`, `uri` sağlanmazsa gereklidir. Anahtar/değer çiftlerinin okunacağı Azure aboneliğinizdeki kasasının adını belirtir.
* `connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support) tarafından kullanılabilen bir bağlantı dizesi
* `uri`-belirtilen `uri` değeri ile diğer Key Vault sağlayıcılarına bağlanır. Belirtilmemişse, Azure (`vaultName`) kasa sağlayıcısıdır.
* `version` Azure Key Vault, gizli dizileri için sürüm oluşturma özelliği sağlar. `version` belirtilirse, Oluşturucu yalnızca bu sürümle eşleşen gizli dizileri alır.
* `preloadSecretNames`, varsayılan olarak, bu Oluşturucu başlatıldığında anahtar kasasındaki **Tüm** anahtar adlarını sorgular. Tüm anahtar değerlerini okumayı engellemek için, bu özniteliği `false`olarak ayarlayın. Bunu `false` olarak ayarlamak tek seferde parolaları okur. Tek seferde gizli dizileri okumak, kasa "liste" erişimini "Al" erişimine izin veriyorsa "bir yandan" erişim sağlar. **Note:** `Greedy` modu kullanılırken, `preloadSecretNames` `true` olmalıdır (varsayılan.)

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

[Keyperfileconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) , dizin dosyalarını değer kaynağı olarak kullanan temel bir yapılandırma kurucudır. Dosyanın adı anahtardır ve içerik değerdir. Bu yapılandırma Oluşturucusu, genişletilmiş bir kapsayıcı ortamında çalışırken yararlı olabilir. Docker Sısınma ve Kubernetes gibi sistemler, bu dosya başına bu anahtarda düzenlenmiş Windows kapsayıcılarına `secrets` sağlar.

Öznitelik ayrıntıları:

* `directoryPath`-gerekli. Değerlere bakmak için bir yol belirtir. Docker for Windows gizli dizileri *C:\programdata\docker\gizlilikler* dizininde varsayılan olarak depolanır.
* `ignorePrefix`-bu önek ile başlayan dosyalar hariç tutulur. Varsayılan olarak "Yoksay" olarak belirlenmiştir.
* `keyDelimiter` varsayılan değer `null`. Belirtilmişse, yapılandırma Oluşturucusu dizinin birden çok düzeyine geçiş yaparken bu sınırlayıcıyla anahtar adları oluşturuyor. Bu değer `null`ise, yapılandırma Oluşturucusu yalnızca dizinin en üst düzeyine bakar.
* `optional` varsayılan değer `false`. Kaynak dizin yoksa yapılandırma oluşturucusunun hatalara neden olup olmayacağını belirtir.

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> Kaynak kodundaki parolaları, hassas bağlantı dizelerini veya diğer hassas verileri hiçbir şekilde depolamayin. Üretim gizli dizileri geliştirme veya test için kullanılmamalıdır.

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET Core projeleri genellikle yapılandırma için JSON dosyalarını kullanır. [Simplejsonconfigbuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) oluşturucusu, .NET Framework .NET Core JSON dosyalarının kullanılmasına izin verir. Bu yapılandırma Oluşturucusu, düz bir anahtar/değer kaynağından .NET Framework yapılandırmanın belirli bir anahtar/değer alanına temel bir eşleme sağlar. Bu yapılandırma Oluşturucusu hiyerarşik **yapılandırmalar sağlamıyor.** JSON yedekleme dosyası karmaşık hiyerarşik bir nesne değil, bir sözlüğe benzerdir. Çok düzeyli hiyerarşik bir dosya kullanılabilir. Bu sağlayıcı, `:` bir sınırlayıcı olarak kullanarak her düzeyde özellik adını ekleyerek derinliği `flatten`.

Öznitelik ayrıntıları:

* `jsonFile`-gerekli. Okunacak JSON dosyasını belirtir. `~` karakteri uygulama köküne başvurmak için başlangıçta kullanılabilir.
* `optional`-Boolean, varsayılan değer `true`. JSON dosyası bulunamazsa özel durum üretilmesini önler.
* `jsonMode` - `[Flat|Sectional]`. `Flat` varsayılandır. `jsonMode` `Flat`, JSON dosyası tek bir düz anahtar/değer kaynağıdır. `EnvironmentConfigBuilder` ve `AzureKeyVaultConfigBuilder` aynı zamanda tek düz anahtar/değer kaynaklarıdır. `SimpleJsonConfigBuilder` `Sectional` modunda yapılandırıldığında:

  * JSON dosyası kavramsal olarak yalnızca en üst düzeyde birden fazla sözlüklere bölünmüştür.
  * Sözlüklerin her biri yalnızca, bunlara iliştirilmiş en üst düzey Özellik adıyla eşleşen yapılandırma bölümüne uygulanır. Örneğin:

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>Özel anahtar/değer yapılandırma Oluşturucusu uygulama

Yapılandırma oluşturucular gereksinimlerinizi karşılamıyorsa, özel bir tane yazabilirsiniz. `KeyValueConfigBuilder` temel sınıfı değiştirme modlarını ve çoğu önek kaygılarını işler. Yalnızca uygulama gerektiren bir proje gereklidir:

* Temel sınıftan devralma ve `GetValue` ve `GetAllValues`bir temel anahtar/değer çiftleri kaynağı uygulama:
* Projeye [Microsoft. Configuration. Configurationoluşturucular. Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) ekleyin.

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder` temel sınıfı, anahtar/değer yapılandırma oluşturucuları arasında çalışmanın ve tutarlı davranışların çoğunu sağlar.

## <a name="additional-resources"></a>Ek kaynaklar

* [Yapılandırma oluşturucular GitHub deposu](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [.NET kullanarak Azure Key Vault için hizmetten hizmete kimlik doğrulaması](/azure/key-vault/service-to-service-authentication#connection-string-support)
