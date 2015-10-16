# data-filters
Data Filters is a JavaScript extension of DataTables that generates filterable fields in the footer of your table, 
  allowing filters to be applied directly to specific columns. 
  
The extension supports Search, Dropdowns, and Range Filters (both Inclusive and Exclusive). 

It also supports hierarchy based tables with the use of the jQuery treetable plugin overlaid on top of a DataTable.
  Found here: http://plugins.jquery.com/treetable/
  
Data Filters - Basic Initialization:
```javascript
// Import the script
<script src="js/data-filter-1.0.0.js"></script>

// Create the object for your table
var columnFilter = {
  filterType: "heirarchy",
  filterInfo: [
    {
      type: "search"
      columns: ["descr", "fullDescr", "alias"],
    }, {
      columns: null
    }, {
      type: "dropdown"
      name: "status",
      columns: ["status"],
    }, {
      type: "range"
      name: "utilization",
      columns: ["utilization"],
    }
  ]
};

// Create the filters 
createFilters(table, columnFilters);
```

Filter Info:
Type: The Type of filter you'd like to create (search, dropdown, range)
Name: The Name of the column in your table
Column: The column(s) that the filter should search

1) All columns of the table must be included (in _order_) in the columnFilter - filterInfo object.
  A "column: null" just indicates that no filter will be created for this column.
    
2) For Search Filters: "column: ["field", "otherField", "etc"]" allows the user to search on 
    multiple fields within the table (including hidden fields - what wizardry is this!?!).

  
# SPECIAL NOTES: 
In regards to treetable plugin for use with hierarchy type tables:

1. I have made one custom tweak to the treetable plugin (version 3.2.0) to improve the draw speed of the table. 
   The draw speed was excruciatingly slow for tables larger than a few hundred lines.
  
  ```  
   Changing the following: "In Node.prototype.expand()"
    "$(this.row).is(":visible")"
   To: 
    "!this.row[0].hidden" 
  ```
  
  This appears to alleviate the issue, without any negative repurcussions. 
  For a more thorough explanation of this bug see the following issue: https://github.com/ludo/jquery-treetable/issues/144 

2. There is no possible way to be able to generate or figure out your data-tt-id and data-tt-parent-id's. 
    You gotta figure that out on your own! :P
