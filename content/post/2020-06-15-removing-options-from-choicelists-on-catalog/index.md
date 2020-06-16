---
title: "How to remove options from a select box"
subtitle: "You'd think this is simple."
summary: "Removing options from select boxes on catalog items can cause problems"
authors: ["jace"]
tags: []
categories: []
date: 2020-06-15T22:55:23-05:00
lastmod: 2020-06-15T22:55:23-05:00
featured: false
draft: false

image:
  caption: ""
  focal_point: ""
  preview_only: false

projects: []
---

In the past people have asked How do I [Remove an option from select box variable in the catalog item form](https://community.servicenow.com/community?id=community_question&sys_id=1f5fb2a9db58dbc01dcaf3231f96199a)?  And you'd think it would be something as simple as a `active` flag.  However if you look there is no `active` flag on select box options.  That is truly unfortunate.

If you delete it, the values will still hold their `value` but if there was a display for the value it won't show that.

## How do I go forward?

There's really only one way I know of.  Client script and remove the option until you can safely delete it.

The client script would be really small

```js
function onLoad(){
  g_form.removeOption('duration','twelve_months');
}
```

## Related things
- Related Question: https://community.servicenow.com/community?id=community_question&sys_id=1f5fb2a9db58dbc01dcaf3231f96199a
- Related Post: https://www.servicenowguru.com/scripting/client-scripts-scripting/removing-disabling-choice-list-options