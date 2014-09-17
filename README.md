====== Responsive Framework ======

===== How to Use the Framework =====

**A basic use case :**

  * create a column with @include column(x,y,z);
  * x= beginning column (1-12)
  * y = ending column (1-12)
  * z= margins (acceptable values are [blank] for regular margins, no-margin, no-margin-left, or no-margin-right)

For example, if your column is three columns wide and starts at column 1, you would say @include(1,3)

**Other options:** 

**1. Fixed**: All items are fluid (percentage-widths). If you need to have a fixed, pixel width item, but still want to use the grid, you can add a "fixed" parameter to the list of arguments. An example would be a form, where the labels and input fields need to line up to a grid, but you don't want the input fields to get smaller with the page width. Here's an example of how it would look:

<code css>
label {
	@include column(1,3);
	font-size: 12px;
	margin-top: 4px;
	text-align: right;
 }
input, select {
	@include column(1,2, margin, fixed);
 }
</code>

If you have a nested grid, since these values are fixed, pixel width values, you may need to adjust your values accordingly, because everything will be based on a 960 grid. You also have the option of changing your grid size, by using an extra parameter to change the size of your container. For example, if your outer container is 8 columns wide, the parameter would be "in-8". Here's an example: 

<code css>

 label {
	@include column(1,3);
	font-size: 12px;
	margin-top: 4px;
	text-align: right;
 }
 input, select {
	@include column(1,2, margin, fixed, in-1-8);
 }
</code>

If your container is not a perfect grid width, let's say for example that you have some padding on your container, then using @include column(1,2, margin, fixed, in-8, margin); will not give you the correct container width, so you can also find the actual width of the container and pass it in as an option (for non-funnel pages). You will get a fixed size element of two columns wide based upon our grid ratios sized to fit into a 918px container.:

<code css>

 label {
	@include column(1,3);
	font-size: 12px;
	margin-top: 4px;
	text-align: right;
 }
 input, select {
	@include column(1,2, margin, fixed, in-918);
 }
</code>


The non-funnel layouts also have the ability to declare whether the containing object has a margin or not, since in some cases, this can be the difference of 32 pixels. The nomenclature is just like the margin for the element: 
<code css>

 label {
	@include column(1,3);
	font-size: 12px;
	margin-top: 4px;
	text-align: right;
 }
 input, select {
	@include column(1,2, margin, fixed, in-1-12, no-margin);
 }
</code>


**Note:** "margin, "fixed", "in-x", and "container-margin" are all optional parameters, but if you want to use "fixed", "in-x", or "container-margin",  you will need to define all preceeding parameters.

**2. Startat**: If you need to start an element at a column other than 1, and there are no other elements to the left of the element, you can use the "startat" mixin. So, for example, you have your form with labels and input fields, but you also want a button and validation text that lines up with the input fields. "Startat" aligns your element to the column that you choose. For example: 


<code css>
label {
	@include column(1,3);
	font-size: 12px;
	margin-top: 4px;
	text-align: right;
}
input, select {
	@include column(1,2, margin, fixed);
}
span.field-validation-error {
	clear: left;
	display: block;
	@include startat(3);
}
button {
	clear: both;
	margin-top: 16px;
	margin-left: 75px;
	@include startat(3);
}

</code>

Startat can also take a margin parameter. The "margin" parameter starts at the column plus a left margin. leaving it blank will line the element up to the edge of the margin. So, @include startat(3, margin) would line the element up with an element above or below that has a left margin.

