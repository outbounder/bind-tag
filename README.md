# bind-tag

Adds binding support to riotjs Tags

## install

```
$ npm install bind-tag
```

## usage

### one way binding

Automatically calls `tag.update` when dataObject is modified (recursively)

```
<my-tag>
  <script>
    var tag = this
    require('bind-tag')(tag)
    var dataObject = {
      property: {
        value: 42
      }
    }
    tag.bind('myState', dataObject)
    setInterval(function () {
      tag.myState.property.value += 1
    }, 1000)
  </script>
  <div>{myState.property.value}</div>
</my-tag>
```

### two way binding

Automatically synchronizes dom elements' `.value` with dataObject

```
<my-tag>
  <script>
    var tag = this
    require('bind-tag')(tag)
    var dataObject = {
      property: {
        value: "42"
      }
    }
    tag.bind('myState', dataObject)
    tag.resetValue = function (e) {
      tag.myState.property.value = "42"
    }
    tag.printValue = function (e) {
      console.log(tag.myState.property.value)
    }
  </script>
  <input tag-value={bindProp('myState.property.value')} />
  <button onclick={resetValue}>reset value</button>
  <button onclick={printValue}>print vlaue</button>
</my-tag>
```

## api

### bind(propertyName, obj, deep, update)

* `propertyName` - String
* `obj` - Object
* `deep` - Boolean default `true`, recursively bind to `obj` ?
* `update` - Boolean default `true`, call `tag.update()` when `tag.propertyName` changes

### bindOpt(propertyName, optName, onbind, deep)

Automatically binds value provided in `tag.opts[optName]`

* `propertyName` - String
* `optName` - String
* `onbind` - Function
* `deep` - Boolean default `true`, recursively bind to `obj` ?

### bindProp(modelPath)

* `modelPath` - String
