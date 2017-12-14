---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: Use ViewData e implemente ViewModel clases | Documentos de Microsoft
author: microsoft
description: "Paso 6 se muestra cómo habilita la compatibilidad de forma más completa que modificar escenarios y también se explican dos enfoques que pueden utilizarse para pasar datos de controladores a vistas:..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: 36b9e87cc24f74f7f2cc592afb5102709b598f74
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2017
---
<a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="eb1ad-103">Use ViewData e implemente ViewModel clases</span><span class="sxs-lookup"><span data-stu-id="eb1ad-103">Use ViewData and Implement ViewModel Classes</span></span>
====================
<span data-ttu-id="eb1ad-104">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="eb1ad-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="eb1ad-105">Descarga de PDF</span><span class="sxs-lookup"><span data-stu-id="eb1ad-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="eb1ad-106">Este es el paso 6 de una segunda ["" la aplicación NerdDinner](introducing-the-nerddinner-tutorial.md) que los recorridos de obtención de cómo generar una pequeña, pero completa, la aplicación web mediante ASP.NET MVC 1.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="eb1ad-107">Paso 6 se muestra cómo habilita la compatibilidad de forma más completa que modificar escenarios y también se explican dos enfoques que pueden utilizarse para pasar datos de controladores a vistas: ViewData y modelo de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="eb1ad-108">Si usa ASP.NET MVC 3, se recomienda que siga el [obtener iniciado con MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) o [tienda de música de MVC](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutoriales.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="eb1ad-109">NerdDinner paso 6: ViewData y ViewModel</span><span class="sxs-lookup"><span data-stu-id="eb1ad-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="eb1ad-110">Hemos cubierto un número de escenarios de envío de formulario y se explica cómo implementar crear, actualizar y eliminar el soporte técnico (CRUD).</span><span class="sxs-lookup"><span data-stu-id="eb1ad-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="eb1ad-111">Ahora podrá tomamos nuestra implementación DinnersController aún más y habilitar la compatibilidad con escenarios de edición de forma más completa.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="eb1ad-112">Al hacer esto analizaremos dos enfoques que pueden utilizarse para pasar datos de controladores a vistas: ViewData y modelo de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="eb1ad-113">Pasar los datos de controladores en las plantillas de vista</span><span class="sxs-lookup"><span data-stu-id="eb1ad-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="eb1ad-114">Una de las características que definen el modelo de MVC es la "separación de aspectos" strict ayuda a aplicar entre los distintos componentes de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="eb1ad-115">Modelos, controladores y vistas de cada uno de ellos también definida roles y responsabilidades, y se comunican entre sí de maneras bien definidos.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="eb1ad-116">Esto ayuda a promover la capacidad de prueba y reutilización del código.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="eb1ad-117">Cuando una clase de controlador decide representar una respuesta HTML a un cliente, es responsable de pasar explícitamente a la plantilla de vista de todos los datos necesitan para representar la respuesta.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="eb1ad-118">Plantillas de vista nunca deberían realizar cualquier lógica de aplicación o de recuperación de datos – y en su lugar, deben limitar propios para solo tiene código de representación que se basa en el modelo/datos que recibe el controlador.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="eb1ad-119">Ahora los datos del modelo que se pasa por nuestro DinnersController clase a nuestras plantillas de vista es sencilla y directa: una lista de objetos de la cena en el caso de Index() y una sola cena el objeto en el caso de Details(), Edit(), Create() y Delete().</span><span class="sxs-lookup"><span data-stu-id="eb1ad-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="eb1ad-120">Tal y como se agregan más capacidades de interfaz de usuario para nuestra aplicación, que vamos a menudo es necesario pasar algo más que estos datos para procesar respuestas de HTML en nuestras plantillas de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="eb1ad-121">Por ejemplo, tengamos que queremos cambiar el campo "País" dentro de nuestro editar y crear vistas ante un cuadro de texto HTML a dropdownlist.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="eb1ad-122">En lugar de codificar la lista desplegable de nombres de país en la plantilla de vista, tengamos que queremos generar en una lista de países admitidos que se rellenan de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="eb1ad-123">Necesitamos una manera de pasar el objeto de cena *y* la lista de países de nuestro controlador a nuestras plantillas de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="eb1ad-124">Echemos un vistazo a dos maneras que podemos lograr esto.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="eb1ad-125">Mediante el diccionario ViewData</span><span class="sxs-lookup"><span data-stu-id="eb1ad-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="eb1ad-126">La clase base del controlador expone una propiedad de diccionario "ViewData" que puede utilizarse para pasar los elementos de datos adicionales de controladores a vistas.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="eb1ad-127">Por ejemplo, para admitir el escenario donde queremos cambiar el cuadro de texto "País" dentro de la vista de edición desde que se va a un cuadro de texto HTML en un dropdownlist, podemos actualizar el método de acción Edit() para pasar (además de un objeto de la cena) un objeto SelectList que puede usarse como m. odelo de dropdownlist países.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="eb1ad-128">El constructor de la anterior SelectList acepta una lista de los condados para rellenar la colocación downlist con, así como el valor seleccionado actualmente.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="eb1ad-129">A continuación, podemos actualizar nuestra plantilla de vista Edit.aspx para utilizar el método de aplicación auxiliar de Html.DropDownList() en lugar del método de aplicación auxiliar de Html.TextBox() que hemos usado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="eb1ad-130">El método de aplicación auxiliar de Html.DropDownList() anterior toma dos parámetros.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="eb1ad-131">El primero es el nombre del elemento de formulario HTML para la salida.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="eb1ad-132">El segundo es el modelo de "SelectList" se pasan a través del diccionario ViewData.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="eb1ad-133">Estamos usando C# "como" (palabra clave) para convertir el tipo en el diccionario como un SelectList.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="eb1ad-134">Y ahora cuando se ejecución la aplicación y el acceso del */Dinners/Edit/1* dirección URL dentro de nuestro navegador, veremos que se ha actualizado la interfaz de usuario de edición para mostrar una dropdownlist de países en lugar de un cuadro de texto:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="eb1ad-135">Dado que también se representan la plantilla de vista de edición desde el método HTTP POST Editar (en escenarios cuando se producen errores), queremos Asegúrese de que también se actualiza este método para agregar el SelectList a ViewData cuando la plantilla de vista se presenta en escenarios de error:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="eb1ad-136">Y ahora nuestro escenario de edición DinnersController admite DropDownList.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="eb1ad-137">Utilizar un modelo de ViewModel</span><span class="sxs-lookup"><span data-stu-id="eb1ad-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="eb1ad-138">El diccionario ViewData tiene la ventaja de ser bastante rápida y fácil de implementar.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="eb1ad-139">Algunos desarrolladores no como con diccionarios basados en cadena, sin embargo, puesto que pueden provocar errores tipográficos errores que no se detectarán en tiempo de compilación.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="eb1ad-140">El diccionario ViewData sin tipo también requiere mediante el operador "como" o de conversión cuando se usa un lenguaje fuertemente tipado como C# en una plantilla de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="eb1ad-141">Un método alternativo que podríamos usar es uno conoce a menudo como el patrón "ViewModel".</span><span class="sxs-lookup"><span data-stu-id="eb1ad-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="eb1ad-142">Si utiliza este modelo, crear clases fuertemente tipadas que están optimizados para cuatro escenarios de vista específicos, y que exponen propiedades de los valores o contenido dinámico necesita nuestras plantillas de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="eb1ad-143">Las clases de controlador, a continuación, pueden rellenar y pasar estas clases con optimización para ver a nuestra plantilla de vista que se usará.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="eb1ad-144">Esto permite la seguridad de tipos, comprobar tiempo de compilación e intellisense del editor de plantillas de vista.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="eb1ad-145">Por ejemplo, para habilitar escenarios de edición podemos crear un "DinnerFormViewModel" clase como a continuación de formularios de cena que expone dos propiedades fuertemente tipadas: un objeto de la cena y el modelo de SelectList necesarios para rellenar la dropdownlist países:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="eb1ad-146">Podemos actualizar, a continuación, el método de acción de Edit() para crear el DinnerFormViewModel utilizando el objeto de la cena que recuperamos de nuestro repositorio y, a continuación, se pasa a la plantilla de vista:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="eb1ad-147">Te enviaremos un mensaje, a continuación, nuestra plantilla de vista de modo que TI espera un "DinnerFormViewModel" en lugar de una "cena" objeto cambiando el atributo "inherits" en la parte superior de la página edit.aspx de actualización de este modo:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="eb1ad-148">Después de hacer esto, se actualizará para reflejar el modelo de objetos del tipo DinnerFormViewModel que estamos pasando las características de intellisense de la propiedad "Modelo" dentro de la plantilla de vista:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="eb1ad-149">A continuación, podemos actualizar el código de vista para trabajar fuera de él.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="eb1ad-150">Observe a continuación cómo no cambiar los nombres de los elementos de entrada, vamos a crear (los elementos de formulario todavía se denominarán "Título", "País"), pero estamos actualizando los métodos auxiliares de HTML para recuperar los valores de uso de la clase DinnerFormViewModel:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="eb1ad-151">También podrá Actualizamos nuestro método post de edición para utilizar la clase DinnerFormViewModel cuando errores de representación:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="eb1ad-152">Podemos también Actualizamos nuestro Create() los métodos de acción para volver a usar justo lo mismo *DinnerFormViewModel* clase para permitir a los países DropDownList dentro de las que también.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="eb1ad-153">A continuación se muestra la implementación de HTTP-GET:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="eb1ad-154">A continuación se muestra la implementación del método HTTP POST crear:</span><span class="sxs-lookup"><span data-stu-id="eb1ad-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="eb1ad-155">Y ahora admiten nuestras pantallas editar y crear los desplegables para seleccionar el país.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="eb1ad-156">Clases de ViewModel en forma de personalizado</span><span class="sxs-lookup"><span data-stu-id="eb1ad-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="eb1ad-157">En el escenario anterior, nuestra clase DinnerFormViewModel expone directamente el objeto de modelo de la cena como una propiedad, junto con una propiedad de modelo SelectList auxiliar.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="eb1ad-158">Este enfoque funciona perfectamente en escenarios donde la interfaz de usuario de HTML que desea crear dentro de la plantilla de vista corresponde relativamente estrechamente con nuestros objetos del modelo de dominio.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="eb1ad-159">Para escenarios donde no es el caso, una opción que puede usar es crear una clase ViewModel en forma personalizada cuyo modelo de objetos está más optimizado para su uso por la vista – y que podría ser completamente diferente del objeto de modelo de dominio subyacente.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="eb1ad-160">Por ejemplo, pudieron exponer los nombres de propiedad diferente o agregadas propiedades recopiladas por múltiples objetos de modelo.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="eb1ad-161">Pueden ser en forma de personalizar las clases de ViewModel usa tanto para pasar datos de controladores a las vistas para representar, así como para ayudar a administrar los datos de formulario que se devuelve al método de acción del controlador.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="eb1ad-162">En este escenario más adelante, puede que tenga el método de acción Actualizar un objeto de modelo de vista con los datos expuestos por el formulario y, a continuación, usar la instancia ViewModel para asignar o recuperar un objeto de modelo de dominio real.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="eb1ad-163">Clases de ViewModel en forma de personalizado pueden proporcionar una gran cantidad de flexibilidad y son algo para investigar cualquier momento que se encuentra el código de representación dentro de las plantillas de vista o el código de envío de formulario dentro de los métodos de acción empezando a ser demasiado complicado.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="eb1ad-164">Por lo general, suele ser un inicio de sesión que los modelos de dominio correctamente no corresponden a la interfaz de usuario que se va a generar, y que puede ayudar una clase ViewModel intermedia de forma personalizada.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="eb1ad-165">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="eb1ad-165">Next Step</span></span>

<span data-ttu-id="eb1ad-166">Ahora veamos cómo podemos usar parciales y las páginas maestras para reutilizar y compartir la interfaz de usuario a través de nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="eb1ad-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="eb1ad-167">[Anterior](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Siguiente](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="eb1ad-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>