# Introduction

This application derives from the marvelous [aurelia-kendoui-bridge](https://github.com/aurelia-ui-toolkits/aurelia-kendoui-bridge) catalog. But it's a bit more complicated than that because in fact it is made from several repositories which would pave the way for a more generalized approach to deliver a [skeleton for bridge developers](https://github.com/aurelia-ui-toolkits/skeleton-bridge).

It features an Aurelia plugin wrapping a UI library (thus the term bridge here) while at the same time providing a consumer application to test and showcase the components of that bridge. This way, each newly added "wrapper" to [this folder](https://github.com/aurelia-ui-toolkits/aurelia-materialize-bridge/tree/master/src) can immediately be tested in this [embedded application](https://github.com/aurelia-ui-toolkits/aurelia-materialize-bridge/tree/master/sample/src).

As with the KendoUI bridge catalog, this application can now be seen as the **[Catalog](http://aurelia-ui-toolkits.github.io/demo-materialize/#/project-status)** with the __embedded__ **[plugin](https://github.com/aurelia-ui-toolkits/aurelia-materialize-bridge/tree/master/src)**.
