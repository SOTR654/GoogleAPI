Usaremos google scripts porque es bastante simple y familiar, pero sientete libre de modificar el modulo.

___

## Pasos para setup
1. Inicia secion e ingresa a [Apps script](https://script.google.com/home).
2. Preciona "nuevo proyecto"
3. Asignale un nombre y reemplaza el codigo por esto:

<details>
<summary>Javascript code</summary>
```javascript
let Options = {
  "GoogleSheets": {
    "List": function (e) {
      let fileId = decodeURIComponent(e.parameter["file"])
      let sheets = SpreadsheetApp.openById(fileId).getSheets()

      // Create list
      let list = []
      for (let i = 0; i < sheets.length; i++) {
        let s = sheets[i]
        list.push({"name": s.getName(), "id": s.getSheetId()})
      }
      return list
    },
    "Set": function (e) {
      let fileId = decodeURIComponent(e.parameter["file"])
      let id = Number(e.parameter["id"])
      
      // Get sheet
      let page = SpreadsheetApp.openById(fileId).getSheetById(id)
      if (!page)   throw new Error("Sheet not found:" + id)

      // Set
      let changes = JSON.parse(decodeURIComponent(e.parameter["changes"]))
      for (let k in changes) {
        var cell = page.getRange(k)
        cell.setValue(changes[k])
      }
    },
    "Page": function (e) {
      let fileId = decodeURIComponent(e.parameter["file"])
      let id = Number(e.parameter["id"])
      
      // Get sheet and get data
      let page = SpreadsheetApp.openById(fileId).getSheetById(id)
      if (!page)   throw new Error("Sheet not found:" + id)
      return page.getDataRange().getValues()
    }
  },
  "GoogleDocument": {
    "Page": function (e) {
      let fileId = decodeURIComponent(e.parameter["file"])
      let file = DocumentApp.openById(fileId)
      
      // Get sheet
      let id = Number(e.parameter["id"])
      if (!file)   throw new Error("Sheet not found:" + id)

      //  Get data
      return file.getDataRange().getValues()
    }
  }
}



//    Core
function doGet(e) {
  let output
  try {
    let mode = e.parameter["mode"]
    let ask = e.parameter["ask"]
    output = {
      "result": "success",
      "object": Options[mode][ask](e),
    }
  } catch (error) {
    output = {
      "result": "error",
      "error": error.message,
      "completeError": error,
      "parameter": e.parameter,
    }
  }
  return ContentService.createTextOutput(JSON.stringify(output)).setMimeType(ContentService.MimeType.JSON);
}
```
</details>

4. aaaaa
5. a