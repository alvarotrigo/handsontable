# Handsontable

Handsontable is minimalistic a jQuery plugin approach to Excel-like table editor.

See the live demo at: http://warpech.github.com/jquery-handsontable/

## Options

The table below presents configurable options that are interpreted by `handsontable()` constructor:

  Option        | Type     | Default     | Description
----------------|----------|-------------|-------------
 `rows`         | Number   | 5           | Initial number of rows
 `cols`         | Number   | 5           | Initial number of columns
 `minWidth`     | Number   | 0           | Handsontable will add as many columns as needed to meet the given width in pixels
 `minHeight`    | Number   | 0           | Handsontable will add as many rows as needed to meet the given height in pixels
 `minSpareCols` | Number   | 0           | When set to 1 (or more), Handsontable will add a new column at the end of grid if there are no more empty columns
 `minSpareRows` | Number   | 0           | When set to 1 (or more), Handsontable will add a new row at the end of grid if there are no more empty rows
 `onChange`     | Function | _undefined_ | Callback to be fired after one or more cells is changed (with changes array as an argument)
 `multiSelect`  | Boolean  | true        | If true, selection of multiple cells using keyboard or mouse is allowed
 `legend`       | Array    | _undefined_ | Legend definitions. See **Defining legend**
 `autocomplete` | Array    | _undefined_ | Autocomplete definitions. See **Defining autocomplete** 

### Defining legend

The `legend` option is an array of mixins that define multiple legends for the grid. 

With your imagination, legend can be used to make any of the grid cells read-only, use different 
text color, or show a tooltip (title) when hovered with mouse cursor.

Example:

```js
legend: [
  {
    match: function (row, col, data) {
      return (row === 0); //if it is first row
    },
    style: {
      color: '#666', //make the text gray and bold
      fontWeight: 'bold'
    },
    title: 'Heading', //make some tooltip
    readOnly: true //make it read-only
  },
  {
    match: function (row, col, data) {
      return (row > 0 && data()[0][col].indexOf('color') > 0); //if first cell in this column contains word "color"
    },
    style: {
      fontStyle: 'italic' //make cells text in this column written in italic
    }
  }
```

### Defining autocomplete

The `autocomplete` option is an array of mixins that define multiple autocomplete providers for the grid. 

To keep Handsontable lightweight, this feature has a dependency on another jQuery plugin: 
[bootstrap-typeahead](https://github.com/twitter/bootstrap/blob/master/js/bootstrap-typeahead.js). 
It is included in the repo.

Example:

```js
autoComplete: [
  {
    match: function (row, col, data) {
      if (data()[0][col].indexOf("color") > -1) { //if column name contains word "color"
        return true;
      }
      return false;
    },
    highlighter: function (item) {
      var query = this.query.replace(/[\-\[\]{}()*+?.,\\\^$|#\s]/g, '\\$&');
      var label = item.replace(new RegExp('(' + query + ')', 'ig'), function ($1, match) {
        return '<strong>' + match + '</strong>';
      });
      return '<span style="margin-right: 10px; background-color: ' + item + '">&nbsp;&nbsp;&nbsp;</span>' + label;
    },
    source: function () {
      return ["yellow", "red", "orange", "green", "blue", "gray", "black", "white"]
    }
  },
  {
    match: function (row, col, data) {
      return (col === 0); //if it is first column
    },
    source: function () {
      return ["BMW", "Chrysler", "Nissan", "Suzuki", "Toyota", "Volvo"]
    }
  }
],
```

## Similar projects

If you are interested in more complicated data grid solutions, consider:
 - [DataTables](http://datatables.net/)
 - [SlickGrid](https://github.com/mleibman/SlickGrid)