---
title: "dalap-html | Getting Started"
layout: article
---

## About this guide

This guie explains how to setup `dalap-html` in your project,
specificaly:

* How to install this library using maven/leiningen

* How to render a basic template

## What version of dalap-html this guide covers?

This guide covers `dalap-html` version {{site.package_version}}

## Overview

`dalap-html` is a HTML template library. It's main purpose is to allow
the programmer to create composable views easily, and alter them
whenever he seems convenient. The templates will be represented with
Clojure data structures and user custom data types; by doing this the
templates can be easily composed and changed to adapt to different
contexts.

If you are familiar with `hiccup`/`crate`, then this library will be
really easy to pick up, We like to think of `dalap-html` as a superset
of the forementioned libraries.

## Supported Clojure Versions and Clojurescript Versions

This library has been tested with Clojure 1.4, and Clojurescript
version that comes bundled with lein-cljsbuild 0.2.9

## Adding dalap-html to your project

With leiningen:

    [com.birdseye-sw/buster-cljs "{{site.package_version}}"]

With Maven:

    <dependency>
      <groupId>com.birdseye-sw</groupId>
      <artifactId>buster-cljs</artifactId>
      <version>{{site.package_version}}</version>
    </dependency>

## Rendering dalap templates

We will work out how to render dalap-html templates by following
an explained example code, we will start with the namespace definition:

    (ns my-application
      (:require [dalap.html :as html]))

Now we are going to define a layout function that will render our
actions views within a template:

    (defn application-layout [action-id & body]
      (html/html5
        [:head
          [:title "My Awesome Application"]
          [:script {:type "text/javascript"
                    :src "/js/my_application.js"}]]
        [:body.container {:id action-id }
                         body]))

Following, let's say we want to create a view for one action:

    (defn say-hello [msg]
      (application-layout "hello"
        [:div#hello-panel.container msg]))

And finally, to render this into a view, we simply use the `render-html` function

    (defn hello-ring-handler [req]
      {:status 200
       :headers { "Content-Type" "text/html" }
       :body (html/render-html (say-hello (-> req :params :message)))})

## Wrapping up

Congratulations! You know learned how to implement a simple dalap-html template.

## Where to go next

TODO

<!--
There is many other aspects you might want to tackle, like [template transformers][rules] and
using your [templates in clojurescript][clojurescript].
-->

[rules]:{{site.baseurl}}/articles/rules
[clojurescript]:{{site.baseurl}}/articles/clojurescript