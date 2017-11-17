# Isotope
Isotope is a js plugin for filtering and sorting layouts            
<a href="https://www.youtube.com/watch?v=ZfhVm7XPkXk&t" target="_blank"><img src="https://raw.githubusercontent.com/polodev/youtube-isotope-filtering-sorting/master/thumbnail.png"
alt="isotope js plugin tutorial | How to use isotope js in your html web page for filtering and sorting" width="360" border="10" /></a>        
### Objectives
* You will be able to filter, sorting layout in your webpage using isotope js
* You will understand of basic workflow in jquery


## Tuts
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
First write markup for sorting
~~~html
<div class="sort">
  <h1>sorting</h1>
  <button data-name='name' class="btn btn-primary">name</button>
  <button data-name='original-order' class="btn btn-info">original</button>
  <button data-name='random' class="btn btn-dark">random</button>
</div>
~~~
Earlier in initialization, we use only `itemSelector` and `layoutMode` attribute. In order to set user defined sorting add  `getSortData` and give a attribute key with value. In our case attribute name is `name` and value is text of `.grid-item`.
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

### Indication for which sorting or filtering is currently active
I add bootstrap active class to button for indicating which filter and sort currently active. Initially, in case of filter, `all` is active and in case of sort `original-order` is active.
~~~html
<button data-name='*' class="btn btn-info active">All</button>
~~~
Whenever some one click on any filter or sort button, I will remove active class from all button and add active class only to selected button. js code is following


~~~js
//incase of filter
$('.filter button').removeClass('active');
$(this).addClass('active');

//incase of sorting
$('.sort button').removeClass('active');
$(this).addClass('active');
~~~

Hope this will help you. Take care. Thanks for watching and reading.



