Tags: [[__Frontend_engineering]] [[_HTML]]
#Frontend #HTML 

# Introduction
The HTML `<select>` element creates a dropdown list allowing to choose one of available options.

Example:
```html
<select id="language" onchange="handleChange(event)">
    <option value="python">Python</option>
    <option value="javascript">JavaScript</option>
    <option value="java">Java</option>
</select>

<script>
    function handleChange(event) {
        console.log(event.target.value);
    }
</script>
```
# `onchange` attribute
The `onchange` attribute sets up a function that is triggered when an option is selected. 

The `event.taget` variable contains data of the selected option. For example, when choosing the `python` option, then `event.target.value = "python"`.
# `select.value` attribute
The `select.value` attribute determines what value is displayed currently:
```html
<select value="displayed_value" ... >
	<option ...
```

