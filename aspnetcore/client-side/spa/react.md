---
title: Uso de la plantilla de proyecto de React con ASP.NET Core
author: SteveSandersonMS
description: Aprenda cómo comenzar a trabajar con la plantilla de proyecto de aplicación de página única (SPA) de ASP.NET Core para React y create-react-app.
monikerRange: '>= aspnetcore-2.0'
ms.author: scaddie
ms.custom: mvc
ms.date: 02/21/2018
uid: spa/react
ms.openlocfilehash: 721ea1d4197ddd17dde657924f12dee2a6858d97
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2018
ms.locfileid: "36291508"
---
# <a name="use-the-react-project-template-with-aspnet-core"></a><span data-ttu-id="c065a-103">Uso de la plantilla de proyecto de React con ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c065a-103">Use the React project template with ASP.NET Core</span></span>

::: moniker range="= aspnetcore-2.0"

> [!NOTE]
> <span data-ttu-id="c065a-104">Esta documentación no trata sobre la plantilla de proyecto de React incluida en ASP.NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="c065a-104">This documentation isn't about the React project template included in ASP.NET Core 2.0.</span></span> <span data-ttu-id="c065a-105">Trata sobre la nueva plantilla de React que puede actualizar manualmente.</span><span class="sxs-lookup"><span data-stu-id="c065a-105">It's about the newer React template to which you can update manually.</span></span> <span data-ttu-id="c065a-106">La plantilla se incluye de forma predeterminada en ASP.NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="c065a-106">The template is included in ASP.NET Core 2.1 by default.</span></span>

::: moniker-end

<span data-ttu-id="c065a-107">La plantilla de proyecto actualizada de React ofrece un práctico punto de partida para las aplicaciones ASP.NET Core que usan React y las convenciones [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) para implementar una completa interfaz de usuario (UI) en el lado cliente.</span><span class="sxs-lookup"><span data-stu-id="c065a-107">The updated React project template provides a convenient starting point for ASP.NET Core apps using React and [create-react-app](https://github.com/facebookincubator/create-react-app) (CRA) conventions to implement a rich, client-side user interface (UI).</span></span>

<span data-ttu-id="c065a-108">La plantilla es equivalente a crear un proyecto de ASP.NET Core para que funcione como un back-end de API y un proyecto de React de CRA estándar para que funcione como interfaz de usuario, pero con la comodidad de hospedar ambos en un único proyecto de aplicación que se puede compilar y publicar como una sola unidad.</span><span class="sxs-lookup"><span data-stu-id="c065a-108">The template is equivalent to creating both an ASP.NET Core project to act as an API backend, and a standard CRA React project to act as a UI, but with the convenience of hosting both in a single app project that can be built and published as a single unit.</span></span>

## <a name="create-a-new-app"></a><span data-ttu-id="c065a-109">Creación de una nueva aplicación</span><span class="sxs-lookup"><span data-stu-id="c065a-109">Create a new app</span></span>

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="c065a-110">Si usa ASP.NET Core 2.0, asegúrese de que ha [instalado la plantilla de proyecto actualizada de React](xref:spa/index#installation).</span><span class="sxs-lookup"><span data-stu-id="c065a-110">If using ASP.NET Core 2.0, ensure you've [installed the updated React project template](xref:spa/index#installation).</span></span>

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="c065a-111">Si tiene ASP.NET Core 2.1 instalado, no hay ninguna necesidad de instalar la plantilla de proyecto de reaccionar.</span><span class="sxs-lookup"><span data-stu-id="c065a-111">If you have ASP.NET Core 2.1 installed, there's no need to install the React project template.</span></span>

::: moniker-end

<span data-ttu-id="c065a-112">En un símbolo del sistema, cree un nuevo proyecto con el comando `dotnet new react` en un directorio vacío.</span><span class="sxs-lookup"><span data-stu-id="c065a-112">Create a new project from a command prompt using the command `dotnet new react` in an empty directory.</span></span> <span data-ttu-id="c065a-113">Por ejemplo, los siguientes comandos crean la aplicación en un directorio *my-new-app* y cambian a ese directorio:</span><span class="sxs-lookup"><span data-stu-id="c065a-113">For example, the following commands create the app in a *my-new-app* directory and switch to that directory:</span></span>

```console
dotnet new react -o my-new-app
cd my-new-app
```

<span data-ttu-id="c065a-114">Ejecute la aplicación desde Visual Studio o la CLI de .NET Core:</span><span class="sxs-lookup"><span data-stu-id="c065a-114">Run the app from either Visual Studio or the .NET Core CLI:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="c065a-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c065a-115">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="c065a-116">Abra el archivo *.csproj* generado y, desde ahí, ejecute la aplicación de la manera habitual.</span><span class="sxs-lookup"><span data-stu-id="c065a-116">Open the generated *.csproj* file, and run the app as normal from there.</span></span>

<span data-ttu-id="c065a-117">El proceso de compilación restaura las dependencias npm en la primera ejecución, lo que puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="c065a-117">The build process restores npm dependencies on the first run, which can take several minutes.</span></span> <span data-ttu-id="c065a-118">Las compilaciones posteriores son mucho más rápidas.</span><span class="sxs-lookup"><span data-stu-id="c065a-118">Subsequent builds are much faster.</span></span>

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="c065a-119">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="c065a-119">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="c065a-120">Asegúrese de tener una variable de entorno denominada `ASPNETCORE_Environment` con un valor de `Development`.</span><span class="sxs-lookup"><span data-stu-id="c065a-120">Ensure you have an environment variable called `ASPNETCORE_Environment` with value of `Development`.</span></span> <span data-ttu-id="c065a-121">En Windows (en los avisos que no son de PowerShell), ejecute `SET ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="c065a-121">On Windows (in non-PowerShell prompts), run `SET ASPNETCORE_Environment=Development`.</span></span> <span data-ttu-id="c065a-122">En Linux o macOS, ejecute `export ASPNETCORE_Environment=Development`.</span><span class="sxs-lookup"><span data-stu-id="c065a-122">On Linux or macOS, run `export ASPNETCORE_Environment=Development`.</span></span>

<span data-ttu-id="c065a-123">Ejecute [dotnet build](/dotnet/core/tools/dotnet-build) para comprobar que la aplicación se compila correctamente.</span><span class="sxs-lookup"><span data-stu-id="c065a-123">Run [dotnet build](/dotnet/core/tools/dotnet-build) to verify your app builds correctly.</span></span> <span data-ttu-id="c065a-124">En la primera ejecución, el proceso de compilación restaura las dependencias de npm, lo que puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="c065a-124">On the first run, the build process restores npm dependencies, which can take several minutes.</span></span> <span data-ttu-id="c065a-125">Las compilaciones posteriores son mucho más rápidas.</span><span class="sxs-lookup"><span data-stu-id="c065a-125">Subsequent builds are much faster.</span></span>

<span data-ttu-id="c065a-126">Ejecute [dotnet run](/dotnet/core/tools/dotnet-run) para iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c065a-126">Run [dotnet run](/dotnet/core/tools/dotnet-run) to start the app.</span></span>

---

<span data-ttu-id="c065a-127">La plantilla de proyecto crea una aplicación ASP.NET Core y una aplicación de React.</span><span class="sxs-lookup"><span data-stu-id="c065a-127">The project template creates an ASP.NET Core app and a React app.</span></span> <span data-ttu-id="c065a-128">El uso previsto de la aplicación ASP.NET Core es el acceso a los datos, la autorización y otros problemas relativos al servidor.</span><span class="sxs-lookup"><span data-stu-id="c065a-128">The ASP.NET Core app is intended to be used for data access, authorization, and other server-side concerns.</span></span> <span data-ttu-id="c065a-129">La aplicación de React, que reside en el subdirectorio *ClientApp*, está diseñada para utilizarse para su uso con todos los problemas de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="c065a-129">The React app, residing in the *ClientApp* subdirectory, is intended to be used for all UI concerns.</span></span>

## <a name="add-pages-images-styles-modules-etc"></a><span data-ttu-id="c065a-130">Adición de páginas, imágenes, estilos, módulos, etc.</span><span class="sxs-lookup"><span data-stu-id="c065a-130">Add pages, images, styles, modules, etc.</span></span>

<span data-ttu-id="c065a-131">El directorio *ClientApp* es una aplicación de React de CRA estándar.</span><span class="sxs-lookup"><span data-stu-id="c065a-131">The *ClientApp* directory is a standard CRA React app.</span></span> <span data-ttu-id="c065a-132">Para más información, consulte la [documentación oficial de CRA](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md).</span><span class="sxs-lookup"><span data-stu-id="c065a-132">See the official [CRA documentation](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md) for more information.</span></span>

<span data-ttu-id="c065a-133">Existe pequeñas diferencias entre la aplicación de React creada mediante este plantilla y la creada mediante CRA propiamente dicho; sin embargo, las funcionalidades de la aplicación permanecen sin cambios.</span><span class="sxs-lookup"><span data-stu-id="c065a-133">There are slight differences between the React app created by this template and the one created by CRA itself; however, the app's capabilities are unchanged.</span></span> <span data-ttu-id="c065a-134">La aplicación creada con la plantilla contiene un diseño basado en [arranque](https://getbootstrap.com/) y un ejemplo de enrutamiento básico.</span><span class="sxs-lookup"><span data-stu-id="c065a-134">The app created by the template contains a [Bootstrap](https://getbootstrap.com/)-based layout and a basic routing example.</span></span>

## <a name="install-npm-packages"></a><span data-ttu-id="c065a-135">Instalar paquetes de npm</span><span class="sxs-lookup"><span data-stu-id="c065a-135">Install npm packages</span></span>

<span data-ttu-id="c065a-136">Para instalar paquetes de npm de otro fabricante, use un símbolo del sistema en el subdirectorio *ClientApp*.</span><span class="sxs-lookup"><span data-stu-id="c065a-136">To install third-party npm packages, use a command prompt in the *ClientApp* subdirectory.</span></span> <span data-ttu-id="c065a-137">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c065a-137">For example:</span></span>

```console
cd ClientApp
npm install --save <package_name>
```

## <a name="publish-and-deploy"></a><span data-ttu-id="c065a-138">Publicación e implementación</span><span class="sxs-lookup"><span data-stu-id="c065a-138">Publish and deploy</span></span>

<span data-ttu-id="c065a-139">En el desarrollo, la aplicación se ejecuta en modo optimizado para comodidad del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="c065a-139">In development, the app runs in a mode optimized for developer convenience.</span></span> <span data-ttu-id="c065a-140">Por ejemplo, agrupaciones de JavaScript contienen asignaciones de origen (de modo que durante la depuración, puede ver el código fuente original).</span><span class="sxs-lookup"><span data-stu-id="c065a-140">For example, JavaScript bundles include source maps (so that when debugging, you can see your original source code).</span></span> <span data-ttu-id="c065a-141">La aplicación inspecciona los cambios en los archivos de JavaScript, HTML y CSS en el disco y, automáticamente, realiza una nueva compilación y recarga cuando observa que esos archivos han cambiado.</span><span class="sxs-lookup"><span data-stu-id="c065a-141">The app watches JavaScript, HTML, and CSS file changes on disk and automatically recompiles and reloads when it sees those files change.</span></span>

<span data-ttu-id="c065a-142">En producción, use una versión de la aplicación que esté optimizada para el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c065a-142">In production, serve a version of your app that's optimized for performance.</span></span> <span data-ttu-id="c065a-143">Esto se configura para que tenga lugar automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c065a-143">This is configured to happen automatically.</span></span> <span data-ttu-id="c065a-144">Al publicar, la configuración de compilación emite una compilación transpilada reducida del código de cliente.</span><span class="sxs-lookup"><span data-stu-id="c065a-144">When you publish, the build configuration emits a minified, transpiled build of your client-side code.</span></span> <span data-ttu-id="c065a-145">A diferencia de la compilación de desarrollo, la compilación de producción no requiere la instalación de Node.js en el servidor.</span><span class="sxs-lookup"><span data-stu-id="c065a-145">Unlike the development build, the production build doesn't require Node.js to be installed on the server.</span></span>

<span data-ttu-id="c065a-146">Puede usar [métodos de implementación y hospedaje de ASP.NET Core](xref:host-and-deploy/index) estándar.</span><span class="sxs-lookup"><span data-stu-id="c065a-146">You can use standard [ASP.NET Core hosting and deployment methods](xref:host-and-deploy/index).</span></span>

## <a name="run-the-cra-server-independently"></a><span data-ttu-id="c065a-147">Ejecución del servidor de CRA de forma independiente</span><span class="sxs-lookup"><span data-stu-id="c065a-147">Run the CRA server independently</span></span>

<span data-ttu-id="c065a-148">El proyecto está configurado para iniciar su propia instancia del servidor de desarrollo de CRA en segundo plano cuando la aplicación ASP.NET Core se inicia en modo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c065a-148">The project is configured to start its own instance of the CRA development server in the background when the ASP.NET Core app starts in development mode.</span></span> <span data-ttu-id="c065a-149">Esto resulta útil porque significa que no tiene que ejecutar manualmente un servidor independiente.</span><span class="sxs-lookup"><span data-stu-id="c065a-149">This is convenient because it means you don't have to run a separate server manually.</span></span>

<span data-ttu-id="c065a-150">Sin embargo, esta configuración predeterminada tiene un inconveniente.</span><span class="sxs-lookup"><span data-stu-id="c065a-150">There's a drawback to this default setup.</span></span> <span data-ttu-id="c065a-151">Cada vez que modifica el código de C# y la aplicación ASP.NET Core debe reiniciarse, el servidor de CRA se reinicia.</span><span class="sxs-lookup"><span data-stu-id="c065a-151">Each time you modify your C# code and your ASP.NET Core app needs to restart, the CRA server restarts.</span></span> <span data-ttu-id="c065a-152">Se necesitan unos segundos para iniciar la copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c065a-152">A few seconds are required to start back up.</span></span> <span data-ttu-id="c065a-153">Sin realiza frecuentes modificaciones en el código de C# y no quiere esperar a que se reinicie el servidor de CRA, ejecute el servidor de CRA externamente, con independencia del proceso de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c065a-153">If you're making frequent C# code edits and don't want to wait for the CRA server to restart, run the CRA server externally, independently of the ASP.NET Core process.</span></span> <span data-ttu-id="c065a-154">Para ello:</span><span class="sxs-lookup"><span data-stu-id="c065a-154">To do so:</span></span>

1. <span data-ttu-id="c065a-155">En un símbolo del sistema, cambie al subdirectorio *ClientApp* e inicie el servidor de desarrollo de CRA:</span><span class="sxs-lookup"><span data-stu-id="c065a-155">In a command prompt, switch to the *ClientApp* subdirectory, and launch the CRA development server:</span></span>

    ```console
    cd ClientApp
    npm start
    ```

2. <span data-ttu-id="c065a-156">Modifique la aplicación ASP.NET Core para usar la instancia del servidor de CRA externo en lugar de iniciar una de las suyas.</span><span class="sxs-lookup"><span data-stu-id="c065a-156">Modify your ASP.NET Core app to use the external CRA server instance instead of launching one of its own.</span></span> <span data-ttu-id="c065a-157">En la clase *Startup*, reemplace la invocación de `spa.UseReactDevelopmentServer` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c065a-157">In your *Startup* class, replace the `spa.UseReactDevelopmentServer` invocation with the following:</span></span>

    ```csharp
    spa.UseProxyToSpaDevelopmentServer("http://localhost:3000");
    ```

<span data-ttu-id="c065a-158">Cuando inicie la aplicación ASP.NET Core, no se iniciará un servidor de CRA.</span><span class="sxs-lookup"><span data-stu-id="c065a-158">When you start your ASP.NET Core app, it won't launch a CRA server.</span></span> <span data-ttu-id="c065a-159">En su lugar, se usa la instancia que inició manualmente.</span><span class="sxs-lookup"><span data-stu-id="c065a-159">The instance you started manually is used instead.</span></span> <span data-ttu-id="c065a-160">Esto le permite iniciar y reiniciar con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="c065a-160">This enables it to start and restart faster.</span></span> <span data-ttu-id="c065a-161">Ya no tiene que esperar a que la aplicación de React se recompile de una vez a otra.</span><span class="sxs-lookup"><span data-stu-id="c065a-161">It's no longer waiting for your React app to rebuild each time.</span></span>