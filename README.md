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

* 


