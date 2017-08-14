### [Multiple data sources without joining or blending](http://kb.tableau.com/articles/howto/connecting-multiple-data-sources-without-joining-or-blending)
* Create a new Worksheet. 
* Using the top menu bar, select Data > New Data Source. (This can also be done with Ctrl+D)
### Show measure on title, let everything else be empty
* Double click on the sheet title, to edit it
* Create calculated field with str(value to add) 
  * e.g. ```str(avg(some_measure)) + " minutes"```
* Click _Insert_ and specify value to insert
* Click on the graph and select _Hide_