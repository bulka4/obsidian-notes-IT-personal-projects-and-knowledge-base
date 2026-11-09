Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
- SWC (Speedy Web Compiler) transforms JSX elements ([[React - Components and elements|link]]) into JavaScript that creates React elements.
  
  For example, a JSX element like this:
	```javascript
	<h1>Hello</h1>
	``` 
  will be transformed into the following JavaScript expression
	```javascript
	jsx("h1", { children: "Hello" })
	``` 
- React processes those elements and updates the browser's DOM ([[Frontend - DOM|link]]).

