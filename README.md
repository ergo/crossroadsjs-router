# \<polymer-crossroadsjs\>


### DISCONTINUED
Because crossroads.js does not have a maintainer and there appear to be implementation problems inside the library, nor there are no PR's being merged into the project I discontinued the development of this component (anyone if free to pick up the work though, crossroads is looking for a maintainer). 

I've created another router based on Angular's `ui-router-core` that is very well maintained and has an active community. You can find the code here https://github.com/ergo/polymer-ui-router, https://www.webcomponents.org/element/ergo/polymer-ui-router. The new project provides tons of new better functionality and I advise everyone to migrate when you can. It also is tested to work on both Polymer 1 and 2.



[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://beta.webcomponents.org/element/ergo/crossroadsjs-router)

`crossroadsjs-router`
wraps [Crossroads.js](http://millermedeiros.github.io/crossroads.js) router inside a polymer element.

It has all the features of the `app-route` element plus:

- Named routes
- URL generation from path definitions (for client side AND 
  server side definitions)
- Allows for global router setup
- Supports for router nesting
- Route data can contain information for every path segment matched
- Provides elements for segment data extraction and link generation around other
  elements
- Optional matched route parameters typecasting
- Additional match rule support for every rule definition
- Additional per-route custom callback support when an url is matched or not found

Using `crossroadsjs-route-data` with nested routes and an element like `iron-lazy-pages`
can achieve functionality comparable to solutions like `angular-ui-router`
(see the nested routes demo).

You can use the router with both nested routes approach and "flat" routes - 
when using nesting, every level of routes will have its own router created 
and `pipe()`'d to parent router.

If you want to use route nesting the name of route has to contain `_` 
character as delimiter:

- first route name: master
- second route name: master_other

means that route `master_other` is piped into `master` router. This element will create all the necessary
routers and chain them together. Remember that you need to pass the `subroute*` to route definitions
for this to work correctly.

Example flat usage:


    <crossroadsjs-router id="router1" crossroads-path="[[path]]" crossroads-hash="[[hash]]"
                         crossroads-query="[[query]]" crossroads-matched-data="{{routerMatchedData}}"
                         crossroads-matched-routes="{{routerMatchedRoutes}}"
                         crossroads-routes="{{routesHolder}}">
        <crossroadsjs-route name="index"
                            route="/"></crossroadsjs-route>
        <crossroadsjs-route name="prefix"
                            route="/prefix"></crossroadsjs-route>
        <crossroadsjs-route name="prefixSection"
                            route="/prefix/{section}:?query:"></crossroadsjs-route>
        <crossroadsjs-route name="prefixSectionActionId"
                            route="/prefix/{section}/{action}/{objectId}/:slug*:"></crossroadsjs-route>
    </crossroadsjs-router>

Example nested usage:

    <iron-location path="{{path}}" hash="{{hash}}" query="{{query}}"></iron-location>

    <crossroadsjs-router id="router1" crossroads-path="[[path]]" crossroads-hash="[[hash]]"
                         crossroads-query="[[query]]" crossroads-matched-data="{{routerMatchedData}}"
                         crossroads-matched-routes="{{routerMatchedRoutes}}"
                         crossroads-routes="{{routesHolder}}">
      <crossroadsjs-route name="index"
                          route="/"></crossroadsjs-route>
      <crossroadsjs-route name="prefix"
                          route="/prefix/:subroute*:"></crossroadsjs-route>
      <crossroadsjs-route name="prefix_section"
                          route="/prefix/{section}/:?query::subroute*:"></crossroadsjs-route>
      <crossroadsjs-route name="prefix_section_actionId"
                          route="/prefix/{section}/{action}/{objectId}/:slug*:"></crossroadsjs-route>
      <crossroadsjs-route name="admin_section"
                          route="/admin/{section}:subroute*:"></crossroadsjs-route>
      <crossroadsjs-route name="admin_section_actionId"
                          route="/admin/{section}/{action}/{objectId}/:slug:"></crossroadsjs-route>
    </crossroadsjs-router>


### Supporting elements.

#### <crossroadsjs-route-data>

`<crossroadsjs-route-data>` element provides you with easy way to extract
route information from router matched data object into your templates via binding.

Example usage:

    <crossroadsjs-route-data crossroads-route-data="{{extractedDataObject}}"
                             crossroads-route-name="route_name"
                             crossroads-matched-data="[[routerMatchedData]]"></crossroadsjs-route-data>

    <p>Section param value from router: <strong>[[extractedDataObject.somevalue]]</strong></p>

#### <crossroadsjs-href>

`<crossroadsjs-href>` element provides you with easy way to generate urls from
named routes passed from `crossroadjs-router` elements.
It automatically converts `param-*` attributes you passed to the element as
to object used in `crossroads.interpolate()`.

Example usage:

    <crossroadsjs-href
    crossroads-route-name="prefix_section_actionId"
    param-section$="items"
    param-action$="edit"
    param-object-id$="[[elemId]]"
    param-slug*$="slug"
    param-hash-string="someanchor"
    param-query-object='{ "first": "a", "last": "b" }'
    crossroads-routes="[[routesHolder]]">
    <span>Edit</span></crossroadsjs-href>


## Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your application locally.

## Viewing Your Application

```
$ polymer serve
```

## Building Your Application

```
$ polymer build
```

This will create a `build/` folder with `bundled/` and `unbundled/` sub-folders
containing a bundled (Vulcanized) and unbundled builds, both run through HTML,
CSS, and JS optimizers.

You can serve the built versions by giving `polymer serve` a folder to serve
from:

```
$ polymer serve build/bundled
```

## Running Tests

```
$ polymer test
```

Your application is already set up to be tested via [web-component-tester](https://github.com/Polymer/web-component-tester). Run `polymer test` to run your application's test suite locally.
