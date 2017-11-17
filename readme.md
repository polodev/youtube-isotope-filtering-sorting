# Isotope
go to https://isotope.metafizzy.co/ website and add isotope js file in your html file.   
write markup for isotope
~~~html
<div class="grid">
  <div class="grid-item flower">...</div>
  <div class="grid-item fruit">...</div>
  <div class="grid-item bard">...</div>
</div>
~~~

initialize isotope plugin with jquery. [dependancy jquery]
~~~js
$grid = $('.grid').isotope({
  // options
  itemSelector: '.grid-item',
  layoutMode: 'fitRows'
});
~~~
### filtering with isotope
write markup for filtering 
~~~html
<div class="filter">
  <h1>Filtering</h1>
  <button data-name='*' class="btn btn-info">All</button>
  <button data-name=".fruit" class="btn btn-primary">fruit</button>
  <button data-name=".flower" class="btn btn-danger">flower</button>
  <button data-name=".bird" class="btn btn-success">bird</button>
</div>
~~~
make a onclick handler for click event. and get the selected button value and filter using isotope function
~~~js
$('.filter button').on("click", function () {
  var value = $(this).attr('data-name');
    $grid.isotope({
      filter: value
    });
})
~~~

### sorting with isotope
First write markup language for sorting
~~~html
<div class="sort">
  <h1>sorting</h1>
  <button data-name='name' class="btn btn-primary">name</button>
  <button data-name='original-order' class="btn btn-info">original</button>
  <button data-name='random' class="btn btn-dark">random</button>
</div>
~~~
Earlier in initialization, we use only `itemSelector` and `layoutMode` attribute. In order to set user defined sorting add a new attribute name with `getSortData` and give a attribute key with value. In our case attribute value is text of `.grid-item`.
~~~js
getSortData: {
  name: function (element) {
    return $(element).text();
  }
}
~~~
Now listen for the sorting button click and call isotope function with specifying `sortBy`. Here `name` only our defined attribute. It has 2 built in attribute. `random` and `original-order`. Js code is following
~~~js
$('.sort button').on("click", function () {
  var value = $(this).attr('data-name');
  $grid.isotope({
    sortBy: value
  });
})
~~~

Hope this will help you. Take care. Thanks for watching and reading.






