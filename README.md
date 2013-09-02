jquery.autocomplete
===================

Autocomplete on any element. Data source can be an ajax query response or from provided data. 

## How to use

Here is an autocomplete sample for the text field with id 'autocomplete':

    <input type="text" name="q" id="autocomplete" />
  
You can have multiple instances on a single page.

     var options = { serviceUrl: 'service/autocomplete.ashx' }
     var a = $('#autocomplete').autocomplete(options)

You can add extra options:

    var a = $('#query').autocomplete({
      serviceUrl: 'service/autocomplete.ashx',
      minChars: 2,
      delimiter: /(,|;)\s*/, // regex or character
      maxHeight: 400,
      width: 300, 
      zIndex: 9999,
      deferRequestBy: 0, // miliseconds
      params: { country: 'Yes' }, // additional parameters
      noCache: false, // default is false
      onSelect: function(value, data) { alert('You selected: ' + value + ', ' + data) },
      lookup: ['January', 'February', 'March', 'April', 'May'], // local lookup values
      maxSuggestions: null, // Maximum suggestions to display (applies to local results only)
      searchEverywhere: false, // Search any part of data not just from beginning
                            // only applicable to local data lookups
      prefix: '',  // Only start autocompleting after this character e.g. '@' or '+'
      dataKey: 'data' // Provide values as objects and use this key as the inserted data.
                    // Allows users to specify a template for autocomplete suggestions
    })
  
Use **lookup** option only if you prefer to inject an array of autocompletion options, rather than sending Ajax queries.

### Ajax Responses

Responses from ajax requests much be in the following format:

    {
      query: 'Ba',
      suggestions: ['Bahamas', 'Bahrain', 'Bangladesh', 'Barbados'],
      data: ['BHS', 'BHR', 'BGD', 'BRB']
    }

Notes:

* __query__ - original query value
* __suggestions__ - comma separated array of suggested values
* __data__ (optional) - data array, that contains values for callback function when data is selected.

### Setting options

Autocomplete functionality can be disabled or enabled programmatically.

    var ac = $('#query').autocomplete(options)
    ac.disable()
    ac.enable()
  
Options can be changed programmatically at any time, only options that are passed get set:

    ac.setOptions({ zIndex: 1001 });

If you need to pass additional parameters, you can set them via setOptions too:

    ac.setOptions({ params: { first: 'John', last: 'Doe' } })

### Formatting results

**formatResult**: function that formats values that are displayed in the autosuggest list. It takes two parameters: data we are attempting to autocomplete on and matching data entry. Default function for this:

    function formatResult(value, data, currentValue) {
      if (this.dataKey) data = data[this.dataKey]
      var pattern = '(' + value.replace(this.regEx, '\\$1') + ')'
      return data.replace(new RegExp(pattern, 'gi'), '<strong>$1<\/strong>')
    }

### Styling

Script generates the following HTML (sample query 'Ba'). Active element is marked with class "selected". You can style it any way you wish.

    <div class="autocomplete-w1">
      <div style="width:299px;" id="Autocomplete_1240430421731" class="autocomplete">
        <div><strong>Ba</strong>hamas</div>
        <div><strong>Ba</strong>hrain</div>
        <div><strong>Ba</strong>ngladesh</div>
        <div class="selected"><strong>Ba</strong>rbados</div>
      </div>
    </div>
  
CSS: 

    .autocomplete-w1 { position: absolute; top: 0px; left: 0px; margin: 6px 0 0 6px; }
    .autocomplete { border: 1px solid #999; background: #FFF; cursor: default; text-align: left; max-height: 350px; overflow: auto; margin: -6px 6px 6px -6px; }
    .autocomplete .selected { background: #F0F0F0; }
    .autocomplete div { padding: 2px 5px; white-space: nowrap; overflow: hidden; }
    .autocomplete strong { font-weight: normal; color: #3399FF; }

## Licence 

MIT.

## Source
  
This autocomplete has been updated and adapted from http://www.devbridge.com/projects/autocomplete/jquery/.
