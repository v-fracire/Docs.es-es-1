---
title: "Información general de las API de consumidor"
author: rick-anderson
description: 
keywords: "Núcleo de ASP.NET,"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: f69beb9d-a519-43a8-857c-f6b01886a903
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/consumer-apis/overview
ms.openlocfilehash: d23a6ce50eef71f393124b9420f4ba473904d8b4
ms.sourcegitcommit: 0b6c8e6d81d2b3c161cd375036eecbace46a9707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2017
---
# <a name="consumer-apis-overview"></a><span data-ttu-id="c38b9-103">Información general de las API de consumidor</span><span class="sxs-lookup"><span data-stu-id="c38b9-103">Consumer APIs overview</span></span>

<span data-ttu-id="c38b9-104">Las interfaces IDataProtectionProvider y IDataProtector son las interfaces básicas a través del cual los consumidores utilizan el sistema de protección de datos.</span><span class="sxs-lookup"><span data-stu-id="c38b9-104">The IDataProtectionProvider and IDataProtector interfaces are the basic interfaces through which consumers use the data protection system.</span></span> <span data-ttu-id="c38b9-105">Se encuentran en el paquete Microsoft.AspNetCore.DataProtection.Abstractions.</span><span class="sxs-lookup"><span data-stu-id="c38b9-105">They are located in the Microsoft.AspNetCore.DataProtection.Abstractions package.</span></span>

## <a name="idataprotectionprovider"></a><span data-ttu-id="c38b9-106">IDataProtectionProvider</span><span class="sxs-lookup"><span data-stu-id="c38b9-106">IDataProtectionProvider</span></span>

<span data-ttu-id="c38b9-107">La interfaz del proveedor representa la raíz del sistema de protección de datos.</span><span class="sxs-lookup"><span data-stu-id="c38b9-107">The provider interface represents the root of the data protection system.</span></span> <span data-ttu-id="c38b9-108">Directamente no puede usarse para proteger o desproteger los datos.</span><span class="sxs-lookup"><span data-stu-id="c38b9-108">It cannot directly be used to protect or unprotect data.</span></span> <span data-ttu-id="c38b9-109">En su lugar, el consumidor debe obtener una referencia a un IDataProtector mediante una llamada a IDataProtectionProvider.CreateProtector(purpose), donde el propósito es una cadena que describe el caso de uso previsto del consumidor.</span><span class="sxs-lookup"><span data-stu-id="c38b9-109">Instead, the consumer must get a reference to an IDataProtector by calling IDataProtectionProvider.CreateProtector(purpose), where purpose is a string that describes the intended consumer use case.</span></span> <span data-ttu-id="c38b9-110">Vea [propósito cadenas](purpose-strings.md) para mucho más información sobre la intención de este parámetro y cómo elegir un valor adecuado.</span><span class="sxs-lookup"><span data-stu-id="c38b9-110">See [Purpose Strings](purpose-strings.md) for much more information on the intent of this parameter and how to choose an appropriate value.</span></span>

## <a name="idataprotector"></a><span data-ttu-id="c38b9-111">IDataProtector</span><span class="sxs-lookup"><span data-stu-id="c38b9-111">IDataProtector</span></span>

<span data-ttu-id="c38b9-112">La interfaz de protector devuelto por una llamada a CreateProtector, y es esta interfaz que los consumidores pueden usar para realizar proteger y desproteger las operaciones.</span><span class="sxs-lookup"><span data-stu-id="c38b9-112">The protector interface is returned by a call to CreateProtector, and it is this interface which consumers can use to perform protect and unprotect operations.</span></span>

<span data-ttu-id="c38b9-113">Para proteger un elemento de datos, pase los datos para el método de protección.</span><span class="sxs-lookup"><span data-stu-id="c38b9-113">To protect a piece of data, pass the data to the Protect method.</span></span> <span data-ttu-id="c38b9-114">La interfaz básica define un método que byte convierte [] -> byte [], pero también hay una sobrecarga (proporcionada como un método de extensión) que convierte la cadena -> cadena.</span><span class="sxs-lookup"><span data-stu-id="c38b9-114">The basic interface defines a method which converts byte[] -> byte[], but there is also an overload (provided as an extension method) which converts string -> string.</span></span> <span data-ttu-id="c38b9-115">La seguridad proporcionada por los dos métodos es idéntica; el desarrollador debe elegir cualquier sobrecarga es más conveniente para sus casos de uso.</span><span class="sxs-lookup"><span data-stu-id="c38b9-115">The security offered by the two methods is identical; the developer should choose whichever overload is most convenient for their use case.</span></span> <span data-ttu-id="c38b9-116">Con independencia de la sobrecarga elegida, el valor devuelto por el proteja método ahora está protegido (descifra y compatible con tecnologías de manipulaciones) y la aplicación puede enviar a un cliente no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="c38b9-116">Irrespective of the overload chosen, the value returned by the Protect method is now protected (enciphered and tamper-proofed), and the application can send it to an untrusted client.</span></span>

<span data-ttu-id="c38b9-117">Para desproteger un elemento de datos protegidos anteriormente, pasar los datos protegidos para el método Unprotect.</span><span class="sxs-lookup"><span data-stu-id="c38b9-117">To unprotect a previously-protected piece of data, pass the protected data to the Unprotect method.</span></span> <span data-ttu-id="c38b9-118">(Hay byte []-basada en cadena y basados en sobrecargas para mayor comodidad de desarrollador.) Si la carga protegida fue generada por una llamada anterior a proteger en este mismo IDataProtector, el método Unprotect devolverá la carga sin protección original.</span><span class="sxs-lookup"><span data-stu-id="c38b9-118">(There are byte[]-based and string-based overloads for developer convenience.) If the protected payload was generated by an earlier call to Protect on this same IDataProtector, the Unprotect method will return the original unprotected payload.</span></span> <span data-ttu-id="c38b9-119">Si la carga protegida se ha alterado o ha sido creada por un IDataProtector diferentes, el método Unprotect producirá CryptographicException.</span><span class="sxs-lookup"><span data-stu-id="c38b9-119">If the protected payload has been tampered with or was produced by a different IDataProtector, the Unprotect method will throw CryptographicException.</span></span>

<span data-ttu-id="c38b9-120">El concepto de misma frente a diferentes IDataProtector une hacia el concepto de propósito.</span><span class="sxs-lookup"><span data-stu-id="c38b9-120">The concept of same vs. different IDataProtector ties back to the concept of purpose.</span></span> <span data-ttu-id="c38b9-121">Si dos instancias de IDataProtector generados desde la misma raíz IDataProtectionProvider pero a través de las cadenas de propósito diferente en la llamada a IDataProtectionProvider.CreateProtector, se consideran [diferentes protectores](purpose-strings.md), y uno no podrá desproteger cargas generados por el otro.</span><span class="sxs-lookup"><span data-stu-id="c38b9-121">If two IDataProtector instances were generated from the same root IDataProtectionProvider but via different purpose strings in the call to IDataProtectionProvider.CreateProtector, then they are considered [different protectors](purpose-strings.md), and one will not be able to unprotect payloads generated by the other.</span></span>

## <a name="consuming-these-interfaces"></a><span data-ttu-id="c38b9-122">Consumir estas interfaces</span><span class="sxs-lookup"><span data-stu-id="c38b9-122">Consuming these interfaces</span></span>

<span data-ttu-id="c38b9-123">Para un componente compatible con DI, el uso previsto es que el componente toma un parámetro de IDataProtectionProvider en su constructor y compruebe que el sistema DI automáticamente proporciona este servicio cuando se crea una instancia del componente.</span><span class="sxs-lookup"><span data-stu-id="c38b9-123">For a DI-aware component, the intended usage is that the component take an IDataProtectionProvider parameter in its constructor and that the DI system automatically provides this service when the component is instantiated.</span></span>

> [!NOTE]
> <span data-ttu-id="c38b9-124">Algunas aplicaciones (por ejemplo, las aplicaciones de consola o aplicaciones de ASP.NET 4.x) podrían no ser DI compatible con por lo que no se puede usar el mecanismo descrito aquí.</span><span class="sxs-lookup"><span data-stu-id="c38b9-124">Some applications (such as console applications or ASP.NET 4.x applications) might not be DI-aware so cannot use the mechanism described here.</span></span> <span data-ttu-id="c38b9-125">Para consultar estos escenarios el [no escenarios DI](../configuration/non-di-scenarios.md) documento para obtener más información sobre cómo obtener una instancia de un proveedor de IDataProtection sin pasar por DI.</span><span class="sxs-lookup"><span data-stu-id="c38b9-125">For these scenarios consult the [Non DI Aware Scenarios](../configuration/non-di-scenarios.md) document for more information on getting an instance of an IDataProtection provider without going through DI.</span></span>

<span data-ttu-id="c38b9-126">El siguiente ejemplo muestra tres conceptos:</span><span class="sxs-lookup"><span data-stu-id="c38b9-126">The following sample demonstrates three concepts:</span></span>

1. <span data-ttu-id="c38b9-127">[Agregar el sistema de protección de datos](../configuration/overview.md) al contenedor de servicios,</span><span class="sxs-lookup"><span data-stu-id="c38b9-127">[Adding the data protection system](../configuration/overview.md) to the service container,</span></span>

2. <span data-ttu-id="c38b9-128">Usar DI para recibir una instancia de un IDataProtectionProvider, y</span><span class="sxs-lookup"><span data-stu-id="c38b9-128">Using DI to receive an instance of an IDataProtectionProvider, and</span></span>

3. <span data-ttu-id="c38b9-129">Crear un IDataProtector desde un IDataProtectionProvider y usarla para proteger y desproteger los datos.</span><span class="sxs-lookup"><span data-stu-id="c38b9-129">Creating an IDataProtector from an IDataProtectionProvider and using it to protect and unprotect data.</span></span>

<span data-ttu-id="c38b9-130">[!code-csharp[Main](../using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]</span><span class="sxs-lookup"><span data-stu-id="c38b9-130">[!code-csharp[Main](../using-data-protection/samples/protectunprotect.cs?highlight=26,34,35,36,37,38,39,40)]</span></span>

<span data-ttu-id="c38b9-131">El paquete Microsoft.AspNetCore.DataProtection.Abstractions contiene un método de extensión IServiceProvider.GetDataProtector como una comodidad para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="c38b9-131">The package Microsoft.AspNetCore.DataProtection.Abstractions contains an extension method IServiceProvider.GetDataProtector as a developer convenience.</span></span> <span data-ttu-id="c38b9-132">Encapsula como una única operación tanto recuperar un IDataProtectionProvider desde el proveedor de servicios y una llamada a IDataProtectionProvider.CreateProtector.</span><span class="sxs-lookup"><span data-stu-id="c38b9-132">It encapsulates as a single operation both retrieving an IDataProtectionProvider from the service provider and calling IDataProtectionProvider.CreateProtector.</span></span> <span data-ttu-id="c38b9-133">El ejemplo siguiente muestra su uso.</span><span class="sxs-lookup"><span data-stu-id="c38b9-133">The following sample demonstrates its usage.</span></span>

<span data-ttu-id="c38b9-134">[!code-csharp[Main](./overview/samples/getdataprotector.cs?highlight=15)]</span><span class="sxs-lookup"><span data-stu-id="c38b9-134">[!code-csharp[Main](./overview/samples/getdataprotector.cs?highlight=15)]</span></span>

>[!TIP]
> <span data-ttu-id="c38b9-135">Las instancias de IDataProtectionProvider y IDataProtector son seguras para subprocesos para distintos llamadores.</span><span class="sxs-lookup"><span data-stu-id="c38b9-135">Instances of IDataProtectionProvider and IDataProtector are thread-safe for multiple callers.</span></span> <span data-ttu-id="c38b9-136">Se pretende que una vez que un componente obtiene una referencia a un IDataProtector mediante una llamada a CreateProtector, utilizará dicha referencia para varias llamadas a proteger y llamada de Unprotect.A a Unprotect producirá CryptographicException si la carga protegida no se puede comprobar o descifrarse.</span><span class="sxs-lookup"><span data-stu-id="c38b9-136">It is intended that once a component gets a reference to an IDataProtector via a call to CreateProtector, it will use that reference for multiple calls to Protect and Unprotect.A call to Unprotect will throw CryptographicException if the protected payload cannot be verified or deciphered.</span></span> <span data-ttu-id="c38b9-137">Algunos componentes que desee omitir los errores durante la desproteger operaciones; un componente que lee las cookies de autenticación puede controlar este error y tratar la solicitud como si no tuviera en absoluto ninguna cookie en lugar de producirá un error en la solicitud directamente.</span><span class="sxs-lookup"><span data-stu-id="c38b9-137">Some components may wish to ignore errors during unprotect operations; a component which reads authentication cookies might handle this error and treat the request as if it had no cookie at all rather than fail the request outright.</span></span> <span data-ttu-id="c38b9-138">Los componentes que desea este comportamiento deben detectar específicamente CryptographicException en lugar de admitir todas las excepciones.</span><span class="sxs-lookup"><span data-stu-id="c38b9-138">Components which want this behavior should specifically catch CryptographicException instead of swallowing all exceptions.</span></span>