NoJS Tabs
=========
Adds interactive tabs for content that is comfortly readable when JavaScript is
not available.

Other tabbing scripts I found have a list of tabs in `<ul>` at the top and then
the tab content is in one heap, with no headings between them, no means to
categorize the content without JavaScript.

NoJS Tabs creates the `<ul>` with a list of tabs dynamically when JavaScript is
present and the content is separated into sections with respective headings,
making it naturally readable.

NoJS Tabs allows you to provide callback methods to handle transitions between
tabs (e.g. add effects) and track tab changes.

## Example
Fully working examples are in directory [examples](examples/).

```html
<div id="tabbar">
	<!-- <ul> with tabs will be created here -->
</div>

<div id="tabs">
	<!-- container for all tabs, every child element represents a tab -->
	<div id="tab1">
		<h1>Title of tab 1</h1>
		<p>Some content...</p>
	</div>
	
	<div id="tab2">
		<h1>Title of tab 2</h1>
		<p>Some different content...</p>
	</div>
	
	<div id="tab3">
		<h1>Title of tab 3</h1>
		<p>Some completely unrelated content...</p>
	</div>
</div>

<script type="text/javascript">
	// Create tabs
	nojsTabs({
		tabs: document.getElementById('tabs'), // element holding tabs
		titleSelector: 'h1', // selector used on every tab to get title
		tabBar: document.getElementById('tabbar'), // where <ul> will be created
		hiddenClass: 'tab-hidden', // class for hidden tabs
		activeClass: 'tab-active' // class for the active tab
	});
</script>
```

## How it works
`<ul>` is created in `tabBar` element and has `<li>` for every child element of
`tabs`. Title for each tab is extracted using `titleSelector` run on the tab
element.

The active tab has class `activeClass` and the other tabs have class
`hiddenClass`.

Initial active tab is searched in order:

 - tab with id that is in hashtag
 - the first tab that has `activeClass` from the start
 - the first tab

Each`<li>` has id set to `tab-anchor-<tab id>`.

If JavaScript is not available, the `<ul>` is not created and the content is
fully readable.

## Options
### `tabs`
Element whose child elements are tabs. Every tab must have it's id set.

### `titleSelector`
If a string, the title is found with
tab.querySelector(`titleSelector`).innerHTML. It can also be a `function (tab)`
that returns the title for given tab.

### `tabBar`
Element in which `<ul>` with tab titles is created. The `tabBar` element must
have a unique id.

### `hiddenClass`
Class that is given to tabs and respective `<li>` when the tab is not active.

### `activeClass`
Class that is given to the tab and respective `<li>` that is active.

### `transition`
`function (fromTab, toTab, callback)` that can be used to transition between
two tabs. When the transition is finished, call the `callback` and it will set
correct tab classes. The callback may be omitted, but you will have to set
the classes yourself.

### `beforeChange`
`function (activeTab, nextTab)` that is called before the tab transition.

### `afterChange`
`function (previousTab, activeTab)` that is called after the tab transition.
This function is called only if `transition` is not set or if it calls the
`callback`.

## License
Released under the MIT license.
