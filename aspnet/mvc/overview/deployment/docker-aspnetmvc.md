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
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="9bb13-104">ASP.NET MVC Uygulamalarını Windows Kapsayıcılarına Geçirme</span><span class="sxs-lookup"><span data-stu-id="9bb13-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="9bb13-105">Bir Windows kapsayıcısında mevcut .NET Framework tabanlı bir uygulamayı çalıştırmak için uygulamanızda herhangi bir değişiklik yapılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9bb13-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="9bb13-106">Uygulamanızı bir Windows kapsayıcısında çalıştırmak için uygulamanızı içeren bir Docker görüntüsü oluşturun ve kapsayıcıyı başlatın.</span><span class="sxs-lookup"><span data-stu-id="9bb13-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="9bb13-107">Bu konu başlığı altında, var olan bir [ASP.NET MVC uygulamasının](http://www.asp.net/mvc) nasıl yapılacağı ve bir Windows kapsayıcısında nasıl dağıtılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9bb13-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="9bb13-108">Mevcut bir ASP.NET MVC uygulamasıyla başlayın ve ardından Visual Studio 'Yu kullanarak yayımlanmış varlıkları derleyin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="9bb13-109">Uygulamanızı içeren ve çalıştıran görüntüyü oluşturmak için Docker 'ı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9bb13-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="9bb13-110">Bir Windows kapsayıcısında çalışan siteye gözatıp uygulamanın çalıştığını doğrularsınız.</span><span class="sxs-lookup"><span data-stu-id="9bb13-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="9bb13-111">Bu makale Docker hakkında temel bir anlayışınızın olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="9bb13-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="9bb13-112">[Docker’a Genel Bakış](https://docs.docker.com/engine/understanding-docker/) makalesini okuyarak Docker hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bb13-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="9bb13-113">Bir kapsayıcıda çalıştıracağınız uygulama, soruları rastgele cevapladığı basit bir Web sitesidir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="9bb13-114">Bu uygulama, kimlik doğrulaması veya veritabanı depolaması olmayan temel bir MVC uygulamasıdır; Web katmanını bir kapsayıcıya taşımaya odaklanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9bb13-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="9bb13-115">Sonraki konularda, Kapsayıcılı uygulamalarda kalıcı depolamayı nasıl taşıyacağınız ve yöneteceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="9bb13-116">Uygulamanızı taşımak şu adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="9bb13-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="9bb13-117">Bir görüntü için varlıklar oluşturmak üzere bir Yayımla görevi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9bb13-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="9bb13-118">Uygulamanızı çalıştıracak bir Docker görüntüsü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9bb13-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="9bb13-119">Görüntünüzü çalıştıran bir Docker kapsayıcısı başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="9bb13-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="9bb13-120">Tarayıcınız kullanılarak uygulama doğrulanıyor.</span><span class="sxs-lookup"><span data-stu-id="9bb13-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="9bb13-121">[Tamamlanmış uygulama](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="9bb13-121">The [finished application](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bb13-122">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9bb13-122">Prerequisites</span></span>

<span data-ttu-id="9bb13-123">Geliştirme makinesi aşağıdaki yazılıma sahip olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="9bb13-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="9bb13-124">[Windows 10 yıldönümü güncelleştirmesi](https://www.microsoft.com/software-download/windows10/) (veya üzeri) veya [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="9bb13-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="9bb13-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) -sürüm kararlı 1.13.0 veya 1,12 beta 26 (veya daha yeni sürümler)</span><span class="sxs-lookup"><span data-stu-id="9bb13-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="9bb13-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="9bb13-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="9bb13-127">Windows Server 2016 kullanıyorsanız [kapsayıcı ana bilgisayar dağıtımı-Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="9bb13-128">Docker’ı yükleyip başlattıktan sonra tepsi simgesine sağ tıklayıp **Windows kapsayıcılarına geç** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="9bb13-129">Bu işlem, Windows temelinde Docker görüntülerini çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="9bb13-130">Bu komutun yürütülmesi birkaç saniye sürer:</span><span class="sxs-lookup"><span data-stu-id="9bb13-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="9bb13-131">![Windows kapsayıcısı][windows-container]</span><span class="sxs-lookup"><span data-stu-id="9bb13-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="9bb13-132">Betiği Yayımla</span><span class="sxs-lookup"><span data-stu-id="9bb13-132">Publish script</span></span>

<span data-ttu-id="9bb13-133">Bir Docker görüntüsüne yüklemeniz gereken tüm varlıkları tek bir yerde toplayın.</span><span class="sxs-lookup"><span data-stu-id="9bb13-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="9bb13-134">Uygulamanız için bir yayımlama profili oluşturmak üzere Visual Studio **Publish** komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bb13-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="9bb13-135">Bu profil, bu öğreticide daha sonra hedef yansımanıza kopyaladığınız bir dizin ağacındaki tüm varlıkları yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="9bb13-136">**Adımları Yayımla**</span><span class="sxs-lookup"><span data-stu-id="9bb13-136">**Publish Steps**</span></span>

1. <span data-ttu-id="9bb13-137">Visual Studio 'da web projesine sağ tıklayın ve **Yayımla**' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="9bb13-138">**Özel profil düğmesine**tıklayın ve ardından Yöntem olarak **dosya sistemi** ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="9bb13-139">Dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-139">Choose the directory.</span></span> <span data-ttu-id="9bb13-140">Kurala göre, indirilen örnek `bin\Release\PublishOutput`kullanır.</span><span class="sxs-lookup"><span data-stu-id="9bb13-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="9bb13-141">![Bağlantıyı Yayımla][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="9bb13-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="9bb13-142">**Ayarlar** sekmesinin **dosya yayımlama seçenekleri** bölümünü açın. **Yayımlama sırasında ön derle**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9bb13-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="9bb13-143">Bu iyileştirme, Docker kapsayıcısında görünümleri derlediğiniz, önceden derlenmiş görünümleri kopyaladığınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="9bb13-144">![Yayımlama ayarları][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="9bb13-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="9bb13-145">**Yayımla**' ya tıklayın ve Visual Studio gerekli tüm varlıkları hedef klasöre kopyalayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9bb13-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="9bb13-146">Görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9bb13-146">Build the image</span></span>

<span data-ttu-id="9bb13-147">Docker görüntünüzü tanımlamak için *dockerfile* adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9bb13-147">Create a new file named *Dockerfile* to define your Docker image.</span></span> <span data-ttu-id="9bb13-148">*Dockerfile* , son görüntüyü oluşturmak için yönergeler içerir ve tüm temel görüntü adlarını, gerekli bileşenleri, çalıştırmak istediğiniz uygulamayı ve diğer yapılandırma görüntülerini içerir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-148">*Dockerfile* contains instructions to build the final image and includes any base image names, required components, the app you want to run, and other configuration images.</span></span> <span data-ttu-id="9bb13-149">*Dockerfile* , görüntüyü oluşturan `docker build` komutuna giriştir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-149">*Dockerfile* is the input to the `docker build` command that creates the image.</span></span>

<span data-ttu-id="9bb13-150">Bu alıştırmada, [Docker Hub 'ında](https://hub.docker.com/r/microsoft/aspnet/)bulunan `microsoft/aspnet` görüntüsünü temel alan bir görüntü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9bb13-150">For this exercise, you will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="9bb13-151">Temel görüntü, `microsoft/aspnet`, bir Windows Server görüntüsüdür.</span><span class="sxs-lookup"><span data-stu-id="9bb13-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="9bb13-152">Windows Server Core, IIS ve ASP.NET 4.7.2 içerir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="9bb13-153">Bu görüntüyü kapsayıcıda çalıştırdığınızda, IIS ve yüklenen Web sitelerini otomatik olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="9bb13-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="9bb13-154">Görüntünüzü oluşturan Dockerfile şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="9bb13-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="9bb13-155">Bu Dockerfile içinde bir `ENTRYPOINT` komutu yoktur.</span><span class="sxs-lookup"><span data-stu-id="9bb13-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="9bb13-156">Gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-156">You don't need one.</span></span> <span data-ttu-id="9bb13-157">IIS ile Windows Server çalıştırırken IIS işlemi, ASPNET temel görüntüsünde başlamak üzere yapılandırılmış giriş noktası olur.</span><span class="sxs-lookup"><span data-stu-id="9bb13-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="9bb13-158">ASP.NET uygulamanızı çalıştıran görüntüyü oluşturmak için Docker Build komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9bb13-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="9bb13-159">Bunu yapmak için, projenizin dizininde bir PowerShell penceresi açın ve çözüm dizinine aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="9bb13-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="9bb13-160">Bu komut, Dockerfile içindeki yönergeleri kullanarak yeni görüntüyü oluşturur ve bu görüntüyü mvcrandomanlar olarak adlandırırın.</span><span class="sxs-lookup"><span data-stu-id="9bb13-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="9bb13-161">Bu, temel görüntünün [Docker Hub 'ından](http://hub.docker.com)çekilerek uygulamanızı bu görüntüye ekleyerek içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="9bb13-162">Komut tamamlandıktan sonra, yeni görüntüyle ilgili bilgileri görmek için `docker images` komutunu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9bb13-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="9bb13-163">GÖRÜNTÜ KIMLIĞI makinenizde farklı olacak.</span><span class="sxs-lookup"><span data-stu-id="9bb13-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="9bb13-164">Şimdi uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="9bb13-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="9bb13-165">Bir kapsayıcı başlatma</span><span class="sxs-lookup"><span data-stu-id="9bb13-165">Start a container</span></span>

<span data-ttu-id="9bb13-166">Aşağıdaki `docker run` komutunu yürüterek bir kapsayıcı başlatın:</span><span class="sxs-lookup"><span data-stu-id="9bb13-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="9bb13-167">`-d` bağımsız değişkeni, Docker 'ın görüntüyü ayrılmış modda başlatmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="9bb13-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="9bb13-168">Bu, Docker görüntüsünün geçerli kabuktan kesilen şekilde çalıştığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="9bb13-169">Birçok Docker örneğinde, kapsayıcıyı ve ana bilgisayar bağlantı noktalarını eşlemek için-p görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bb13-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="9bb13-170">Varsayılan ASPNET görüntüsü, kapsayıcıyı 80 numaralı bağlantı noktasında dinlemek üzere zaten yapılandırdı ve kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="9bb13-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="9bb13-171">`--name randomanswers`, çalışan kapsayıcıya bir ad verir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="9bb13-172">Çoğu komut içinde kapsayıcı KIMLIĞI yerine bu adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bb13-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="9bb13-173">`mvcrandomanswers`, başlatılacak görüntünün adıdır.</span><span class="sxs-lookup"><span data-stu-id="9bb13-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="9bb13-174">Tarayıcıda doğrula</span><span class="sxs-lookup"><span data-stu-id="9bb13-174">Verify in the browser</span></span>

<span data-ttu-id="9bb13-175">Kapsayıcı başlatıldıktan sonra, gösterilen örnekteki `http://localhost` kullanarak çalışan kapsayıcıya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="9bb13-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="9bb13-176">URL 'YI tarayıcınıza yazın ve çalışan siteyi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="9bb13-177">Bazı VPN veya proxy yazılımları sitenizde geziniyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="9bb13-178">Kapsayıcının çalıştığından emin olmak için bunu geçici olarak devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9bb13-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="9bb13-179">GitHub 'daki örnek dizin, sizin için bu komutları yürüten bir [PowerShell betiği](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) içerir.</span><span class="sxs-lookup"><span data-stu-id="9bb13-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="9bb13-180">Bir PowerShell penceresi açın, dizini çözüm dizininiz olarak değiştirin ve şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="9bb13-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="9bb13-181">Yukarıdaki komut görüntüyü oluşturur, makinenizde görüntülerin listesini görüntüler ve bir kapsayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="9bb13-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="9bb13-182">Kapsayıcınızı durdurmak için bir `docker stop` komutu verin:</span><span class="sxs-lookup"><span data-stu-id="9bb13-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="9bb13-183">Kapsayıcıyı kaldırmak için bir `docker rm` komutu verin:</span><span class="sxs-lookup"><span data-stu-id="9bb13-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Windows kapsayıcısına geç"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Dosya sistemine Yayımla"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Yayımlama ayarları"
