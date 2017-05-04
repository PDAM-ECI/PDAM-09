# PDAM-09
Uso de servicios HTTP y almacenamiento local en iOS 

## Uso de servicios HTTP
Para la comunicación con servicios externos de HTTP usaremos la libreria AlamoFire que esta disponible como una dependencia de CocoaPods. CocoaPods es un administrador de dependencias para proyectos de Cocoa incluyendo iOS.

* Cree un proyecto de XCode basado en Tabs con base en el laboratorio anterior con el nombre "pdam-09"

## Instalación de dependencias con CocoaPods

A continuación instalaremos CocoaPods para manejar las dependencias del proyecto. Si su computador no le permite instalarlo por favor descargue el proyecto que tiene las dependencias instaladas  en este [link](http://gabo.com.co/pdam/lab-9/pdam-09-cocoa.zip) y pase al siguiente punto de integración con AlamoFire

* Instale CocoaPods
```bash
gem install cocoapods
```

* Cree un Podfile en la carpeta de su proyecto de XCode, donde visualice el archivo (pdam-09.xcodeproj)
```bash
cd carpeta/pdam-09
pod init
```

* Edite el contenido del archivo Podfile con la siguiente información para incluir la libreria de AlamoFire
```bash
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '10.0'
use_frameworks!

target 'pdam-09' do
  pod 'Alamofire', '~> 4.4'
end
```

* Instale la libreria usando CocoaPods
```bash
pod install
```

## Integración con AlamoFire
Si tiene XCode abierto, cierrelo y abra el archivo "pdam-09.xcworkspace" esto es necesario para cargar las dependencias de CocoaPods.

Usando un API de prueba https://jsonplaceholder.typicode.com/ leeremos una lista de Posts y vincularemos los resultados a una lista de elementos en iOS

* Corra la aplicación para asegurar que la libreria sea compilada y pueda incluirse en el proyecto

* Cree un controlador de lista "TableViewController" y agregelo como una tercera opción de los tabs principales usando el mismo método del laboratorio anterior

<img src="http://gabo.com.co/pdam/lab-9/lab-09-01.png" width="50%">

* Cree una clase nueva con el nombre "PostsTableViewController" para el controlador creado en el punto anterior y vincule la clase como lo hizo en el laboratorio anterior.

* Cree una clase nueva con el nombre "PostCell" y con lo aprendido en el laboratorio anterior cree dos elementos de texto dentro de la celda para mostrar el titulo y el contenido del post.

* Incluya la libreria de AlamoFire y haciendo un request al API de prueba almacene los datos recibidos dentro de una colección. Se debe llamar al API de prueba en el evento de carga de la vista (viewDidLoad), complete la clase con el código adecuado para mostrar la información almacenada en la colección de posts

<img src="http://gabo.com.co/pdam/lab-9/lab-09-02.png" width="50%">

* El resultado final debe ser:

<img src="https://media.giphy.com/media/3oKIPkTUOOpugkPWCY/giphy.gif" width="20%">

## Almacenamiento de datos locales

Para el almacenamiento de datos locales se pueden usar varias estrategias, sin embargo usaremos la estrategia por defecto nativa usando CoreData. Añadiremos una opcion a los tabs para agregar elementos (To do) a una lista y guardarlos localmente.

* Añada un nuevo controlador de navegación y vinculelo como cuarta opción en los tabs este por defecto creara un contorlador de lista (TableViewController). como en puntos anteriores cree una clase para el controlador (TodoTableViewController) y otra para la celda de la lista (TodoCell).

* Seleccione el controlador de la vista de lista que acabo de crear haciendo click sobre el icono amarillo en el RootViewController. En el menu principal ubique la opcion "Editor" y seleccione "Embed in" > "Navigation Bar". Esto hará que se duplique el controlador de navegación pero esta vez la vista superior será editable con lo que se podrá añadir la opción de agregar un nuevo elemento.

<img src="http://gabo.com.co/pdam/lab-9/lab-09-03.png" width="50%">

* Selecciona la vista superior de la vista que se acabó de crear, esta estara habilitada para arrastrar elementos. Arrastre un nuevo elemento (Bar Button Item) dentro de la vista. Una vez añadido seleccionelo y ajuste el estilo para que se vea un icono de + . Para esto ajuste la opción de System Item en "add".

<img src="http://gabo.com.co/pdam/lab-9/lab-09-04.png" width="50%">

* Cree una nueva vista desde donde se creará el nuevo Todo arrastrando al storyboard un ViewController

* Seleccione el botón de añadir elemento y usando el boton de 'control' arraste el mouse hasta la vista creada en el punto anterior, esto vinculara la acción de dar click al boton + para que cargue la nueva ventana desde donde se crearan los nuevos elementos.

<img src="https://media.giphy.com/media/xUPGcnzipUbZn1KXzq/giphy.gif" width="50%">

* En la vista de creación inserte un campo de texto y un botón.

<img src="http://gabo.com.co/pdam/lab-9/lab-09-05.png" width="50%">

* Pruebe el funcionamiento de la navegación de la aplicación corriendo el proyecto.

* Cree una clase nueva para almacenar la lógica de creación del Todo (TodoDetailViewController) y como en puntos anteriores vinculela a la interfaz que se creó en puntos anteriores.

<img src="http://gabo.com.co/pdam/lab-9/lab-09-06.png" width="50%">

* Ahora vincularemos la logica con la acción del botón de guardar, esto se hará usando la vista contextual y teniendo seleccionado el botón se arrastrará hasta la vista en donde se seleccionara la vinculación como acción.

<img src="https://media.giphy.com/media/3og0IILcOw1s1TihDa/giphy.gif" width="50%">

* Ubique el archivo "AppDelegate.swift", importe la libreria CoreData, y al final del archivo incluya el código de inicialización del CoreData que está a continuación:

<img src="http://gabo.com.co/pdam/lab-9/lab-09-07.png" width="50%">

```swift
    // MARK: - Core Data stack
    
    lazy var persistentContainer: NSPersistentContainer = {
        /*
         The persistent container for the application. This implementation
         creates and returns a container, having loaded the store for the
         application to it. This property is optional since there are legitimate
         error conditions that could cause the creation of the store to fail.
         */
        let container = NSPersistentContainer(name: "Model")
        container.loadPersistentStores(completionHandler: { (storeDescription, error) in
            if let error = error as NSError? {
                // Replace this implementation with code to handle the error appropriately.
                // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
                
                /*
                 Typical reasons for an error here include:
                 * The parent directory does not exist, cannot be created, or disallows writing.
                 * The persistent store is not accessible, due to permissions or data protection when the device is locked.
                 * The device is out of space.
                 * The store could not be migrated to the current model version.
                 Check the error message to determine what the actual problem was.
                 */
                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
        return container
    }()
    
    // MARK: - Core Data Saving support
    
    func saveContext () {
        let context = persistentContainer.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {
                // Replace this implementation with code to handle the error appropriately.
                // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
                let nserror = error as NSError
                fatalError("Unresolved error \(nserror), \(nserror.userInfo)")
            }
        }
    }
```

* Ahora insertaremos la definición del modelo de datos locales, para esto haga click derecho sobre la capeta del proyecto, y seleccione la opción de añadir archivo nuevo, del menu de opciones seleccione "Data Model" use el nombre "Model" para el nuevo archivo.

<img src="http://gabo.com.co/pdam/lab-9/lab-09-08.png" width="50%">

* Seleccione el archivo, el editor se activara en modo de edición de datos. Cree una nueva entidad con el nombre Item y cree dos atributos en la entidad: 

title:String

done:Boolean

* Esta entidad esta ahora disponible en la lógica de la aplicación mediante la clase Item autogenerada. Ahora integraremos el almacenamiento local con la acción del boton para almacenar un elemento localmente

* Vincule graficamente el input text a la clase TodoDetailViewController para poder leer el valor que el usuario escriba

* Incluya un elemento "switch" dentro de la celda de referencia 

* Complete con el siguiente codigo para guardar la información localmente

<img src="http://gabo.com.co/pdam/lab-9/lab-09-09.png" width="50%">

* El siguiente paso será leer la información local para mostrarla en un listado, para esto ubique el archivo "TodoTableViewController" y edite el codigo para cargar la información cuando la vista quede activa.

<img src="http://gabo.com.co/pdam/lab-9/lab-09-10.png" width="50%">

* El resultado debe ser el siguiente:

<img src="https://media.giphy.com/media/xUPGcorurfiyq3qokE/giphy.gif" width="50%">

* Ahora ajuste el código para que al cambiar el switch, se almacene la propiedad "done" del elemento localmente
