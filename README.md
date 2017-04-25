# PDAM-09
Uso de servicios HTTP y almacenamiento local en iOS 

## Uso de servicios HTTP
Para la comunicación con servicios externos de HTTP usaremos la libreria AlamoFire que esta disponible como una dependencia de CocoaPods. CocoaPods es un administrador de dependencias para proyectos de Cocoa incluyendo iOS.

* Cree un proyecto de XCode con base en el laboratorio anterior con el nombre "pdam-09"

## Instalación de dependencias con CocoaPods

A continuación instalaremos CocoaPods para manejar las dependencias del proyecto. Si su computador no le permite instalarlo por favor descargue el proyecto que tiene las dependencias instaladas y pase al siguiente punto de integración con AlamoFire

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
Si tiene XCode abierto, cierrelo y abra el archivo "pdam-09.xcworkspace" esto es necesario para cargar las dependencias de CocoaPods


