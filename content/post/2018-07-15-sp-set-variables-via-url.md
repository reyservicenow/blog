---
author: 'jace'
category: ''
date: '2018-07-15'
exerpt: 'This answers how to have a catalog item on a service portal use url parameters.  This could be helpful for a number of reasons.'
layout: 'post'
tags:
 - service portal
title: 'Setting variables via URL Scheme on Service Portal'
aliases: 
 - "/sp-set-variables-via-url/"
 - "/2018/07/15/sp-set-variables-via-url/"
---
The other day, [a post was made, asking how to do this](https://community.servicenow.com/community?id=community_question&sys_id=d1de646cdbc7d74423f4a345ca961916)
and I had to answer.  I knew you could read the URL via `$window` but that isn't available in client scripts.  So how can this be done?

<!--more-->

I came up with the following solution.

Create a Variable type of macro, with a widget that has the following client script;

```js
function($scope, $window) {
  // This is the controller, we've included
  // $scope in the function above because
  // it's easy to work with
  var c = this;
  // We are going to simplify accessing 
  // g_form within the client script by
  // setting it as a variable named g_form
  var g_form = $scope.page.g_form;
  //We are going to simplify accessing
  // g_form within the HTML by setting
  // it as a $scope attribute
  $scope.g_form = $scope.page.g_form;
  // from here you can just iterate over
  // the url params;
  var params = $window.location.href.split('?')[1];
  console.log(params);
  var paramsToString = params.toString();
  var paramsArr = paramsToString.split('&');
  paramsArr.map(function(keyValue){
    var key = keyValue.split('=')[0];
    var value = keyValue.split(key + '=').join('');
    value = decodeURIComponent(value);
    try {
      var message = 'Setting ' + key + ' to ';
      message += value + ' from url parameter.';
      console.log(message);
      $scope.g_form.setValue(key,value);
    } catch (error) {
      console.log('Error setting field', error);
    }
  });
}


```

This will try to set all the attributes on the form so in the following url;

`https://dev32369.service-now.com/sp?id=sc_cat_item&sys_id=b480811a0f021300fc69cdbce1050ece&description=test`

The following will tried to be set;

| Parameter   | Value                              |
| ----------- | ---------------------------------- |
| id          | `sc_cat_item`                      |
| sys_id      | `b480811a0f021300fc69cdbce1050ece` |
| description | `test`                             |