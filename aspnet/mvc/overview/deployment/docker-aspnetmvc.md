---
uid: mvc/overview/deployment/docker
title: ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme
description: Mevcut bir ASP.NET MVC uygulamasını nasıl alabileceğinizi ve Windows Docker kapsayıcısında nasıl çalıştıracağınızı öğrenin
keywords: Windows kapsayıcıları, Docker, ASP. NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: ef184f4256c20e2a66de8fd2d4f8e67f07d9a086
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583631"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a>ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme

Bir Windows kapsayıcısında mevcut .NET Framework tabanlı bir uygulamayı çalıştırmak için uygulamanızda herhangi bir değişiklik yapılması gerekmez. Uygulamanızı bir Windows kapsayıcısında çalıştırmak için uygulamanızı içeren bir Docker görüntüsü oluşturun ve kapsayıcıyı başlatın. Bu konu başlığı altında, var olan bir [ASP.NET MVC uygulamasının](http://www.asp.net/mvc) nasıl yapılacağı ve bir Windows kapsayıcısında nasıl dağıtılacağı açıklanmaktadır.

Mevcut bir ASP.NET MVC uygulamasıyla başlayın ve ardından Visual Studio 'Yu kullanarak yayımlanmış varlıkları derleyin. Uygulamanızı içeren ve çalıştıran görüntüyü oluşturmak için Docker 'ı kullanırsınız. Bir Windows kapsayıcısında çalışan siteye gözatıp uygulamanın çalıştığını doğrularsınız.

Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar. [Docker’a Genel Bakış](https://docs.docker.com/engine/understanding-docker/) makalesini okuyarak Docker hakkında bilgi edinebilirsiniz.

Bir kapsayıcıda çalıştıracağınız uygulama, soruları rastgele cevapladığı basit bir Web sitesidir. Bu uygulama, kimlik doğrulaması veya veritabanı depolaması olmayan temel bir MVC uygulamasıdır; Web katmanını bir kapsayıcıya taşımaya odaklanmanızı sağlar. Sonraki konularda, Kapsayıcılı uygulamalarda kalıcı depolamayı nasıl taşıyacağınız ve yöneteceğiniz gösterilmektedir.

Uygulamanızı taşımak şu adımları içerir:

1. [Bir görüntü için varlıklar oluşturmak üzere bir Yayımla görevi oluşturma.](#publish-script)
1. [Uygulamanızı çalıştıracak bir Docker görüntüsü oluşturma.](#build-the-image)
1. [Görüntünüzü çalıştıran bir Docker kapsayıcısı başlatılıyor.](#start-a-container)
1. [Tarayıcınız kullanılarak uygulama doğrulanıyor.](#verify-in-the-browser)

[Tamamlanmış uygulama](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) GitHub üzerinde.

## <a name="prerequisites"></a>Önkoşullar

Geliştirme makinesi aşağıdaki yazılıma sahip olmalıdır:

- [Windows 10 yıldönümü güncelleştirmesi](https://www.microsoft.com/software-download/windows10/) (veya üzeri) veya [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (veya üzeri)
- [Docker for Windows](https://docs.docker.com/docker-for-windows/) -sürüm kararlı 1.13.0 veya 1,12 beta 26 (veya daha yeni sürümler)
- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> Windows Server 2016 kullanıyorsanız [kapsayıcı ana bilgisayar dağıtımı-Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)yönergelerini izleyin.

Docker’ı yükleyip başlattıktan sonra tepsi simgesine sağ tıklayıp **Windows kapsayıcılarına geç** öğesini seçin. Bu işlem, Windows temelinde Docker görüntülerini çalıştırmak için gereklidir. Bu komutun yürütülmesi birkaç saniye sürer:

![Windows kapsayıcısı][windows-container]

## <a name="publish-script"></a>Betiği Yayımla

Bir Docker görüntüsüne yüklemeniz gereken tüm varlıkları tek bir yerde toplayın. Uygulamanız için bir yayımlama profili oluşturmak üzere Visual Studio **Publish** komutunu kullanabilirsiniz. Bu profil, bu öğreticide daha sonra hedef yansımanıza kopyaladığınız bir dizin ağacındaki tüm varlıkları yerleştirir.

**Adımları Yayımla**

1. Visual Studio 'da web projesine sağ tıklayın ve **Yayımla**' yı seçin.
1. **Özel profil düğmesine**tıklayın ve ardından Yöntem olarak **dosya sistemi** ' ni seçin.
1. Dizini seçin. Kurala göre, indirilen örnek `bin\Release\PublishOutput`kullanır.

![Bağlantıyı Yayımla][publish-connection]

**Ayarlar** sekmesinin **dosya yayımlama seçenekleri** bölümünü açın. **Yayımlama sırasında ön derle**'yi seçin. Bu iyileştirme, Docker kapsayıcısında görünümleri derlediğiniz, önceden derlenmiş görünümleri kopyaladığınızı gösterir.

![Yayımlama ayarları][publish-settings]

**Yayımla**' ya tıklayın ve Visual Studio gerekli tüm varlıkları hedef klasöre kopyalayacaktır.

## <a name="build-the-image"></a>Görüntü oluşturma

Docker görüntünüzü tanımlamak için *dockerfile* adlı yeni bir dosya oluşturun. *Dockerfile* , son görüntüyü oluşturmak için yönergeler içerir ve tüm temel görüntü adlarını, gerekli bileşenleri, çalıştırmak istediğiniz uygulamayı ve diğer yapılandırma görüntülerini içerir. *Dockerfile* , görüntüyü oluşturan `docker build` komutuna giriştir.

Bu alıştırmada, [Docker Hub 'ında](https://hub.docker.com/r/microsoft/aspnet/)bulunan `microsoft/aspnet` görüntüsünü temel alan bir görüntü oluşturacaksınız.
Temel görüntü, `microsoft/aspnet`, bir Windows Server görüntüsüdür. Windows Server Core, IIS ve ASP.NET 4.7.2 içerir. Bu görüntüyü kapsayıcıda çalıştırdığınızda, IIS ve yüklenen Web sitelerini otomatik olarak başlatır.

Görüntünüzü oluşturan Dockerfile şöyle görünür:

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

Bu Dockerfile içinde bir `ENTRYPOINT` komutu yoktur. Gerekli değildir. IIS ile Windows Server çalıştırırken IIS işlemi, ASPNET temel görüntüsünde başlamak üzere yapılandırılmış giriş noktası olur.

ASP.NET uygulamanızı çalıştıran görüntüyü oluşturmak için Docker Build komutunu çalıştırın. Bunu yapmak için, projenizin dizininde bir PowerShell penceresi açın ve çözüm dizinine aşağıdaki komutu yazın:

```console
docker build -t mvcrandomanswers .
```

Bu komut, Dockerfile içindeki yönergeleri kullanarak yeni görüntüyü oluşturur ve bu görüntüyü mvcrandomanlar olarak adlandırırın. Bu, temel görüntünün [Docker Hub 'ından](http://hub.docker.com)çekilerek uygulamanızı bu görüntüye ekleyerek içerebilir.

Komut tamamlandıktan sonra, yeni görüntüyle ilgili bilgileri görmek için `docker images` komutunu çalıştırabilirsiniz:

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

GÖRÜNTÜ KIMLIĞI makinenizde farklı olacak. Şimdi uygulamayı çalıştıralım.

## <a name="start-a-container"></a>Bir kapsayıcı başlatma

Aşağıdaki `docker run` komutunu yürüterek bir kapsayıcı başlatın:

```console
docker run -d --name randomanswers mvcrandomanswers
```

`-d` bağımsız değişkeni, Docker 'ın görüntüyü ayrılmış modda başlatmasını söyler. Bu, Docker görüntüsünün geçerli kabuktan kesilen şekilde çalıştığı anlamına gelir.

Birçok Docker örneğinde, kapsayıcıyı ve ana bilgisayar bağlantı noktalarını eşlemek için-p görebilirsiniz. Varsayılan ASPNET görüntüsü, kapsayıcıyı 80 numaralı bağlantı noktasında dinlemek üzere zaten yapılandırdı ve kullanıma sunar.

`--name randomanswers`, çalışan kapsayıcıya bir ad verir. Çoğu komut içinde kapsayıcı KIMLIĞI yerine bu adı kullanabilirsiniz.

`mvcrandomanswers`, başlatılacak görüntünün adıdır.

## <a name="verify-in-the-browser"></a>Tarayıcıda doğrula

Kapsayıcı başlatıldıktan sonra, gösterilen örnekteki `http://localhost` kullanarak çalışan kapsayıcıya bağlanın. URL 'YI tarayıcınıza yazın ve çalışan siteyi görmeniz gerekir.

> [!NOTE]
> Bazı VPN veya proxy yazılımları sitenizde geziniyor olabilir.
> Kapsayıcının çalıştığından emin olmak için bunu geçici olarak devre dışı bırakabilirsiniz.

GitHub 'daki örnek dizin, sizin için bu komutları yürüten bir [PowerShell betiği](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) içerir. Bir PowerShell penceresi açın, dizini çözüm dizininiz olarak değiştirin ve şunu yazın:

```console
./run.ps1
```

Yukarıdaki komut görüntüyü oluşturur, makinenizde görüntülerin listesini görüntüler ve bir kapsayıcı başlatır.

Kapsayıcınızı durdurmak için bir `docker stop` komutu verin:

```console
docker stop randomanswers
```

Kapsayıcıyı kaldırmak için bir `docker rm` komutu verin:

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows kapsayıcısına geç"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Dosya sistemine Yayımla"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Yayımlama ayarları"
