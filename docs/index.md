- [Introducción](index.md)
- [API](api.md)
- [Características](features.md)

## About
GoogleAPI es un modulo con el que puedes obtener informacion de los diversos servicios de Google.
Este modulo usa Google Scripts mediante solicitudes http para obtener los datos, todos los archivos a los cuales intentes acceder deben pertenecer a la misma cuenta o tener los permisos necesarios. 

## Constructor
GoogleAPI inicialmente pide la ID de un Google Script para iniciar, debes administrar los (limites de solicitudes)[https://developers.google.com/apps-script/guides/services/quotas], puedes añadir mas ID de **diferentes usuarios** con los permisos correctos para amortiguar la carga.
```lua
--    Base
local GoogleModule = require(game:GetService("ServerStorage").GoogleAPI)
local GoogleAPI = GoogleModule(Google Script ID)

--    Add other google script
GoogleAPI:AddScriptID(Google Script ID)
```

