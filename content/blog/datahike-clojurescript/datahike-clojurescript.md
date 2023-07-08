---
title: Datahike in ClojureScript with IndexedDB support.
description: We demonstrate the upcoming ClojureScript support of Datahike.
date: 2021-03-03
---
<link rel="canonical" href="https://lambdaforge.io/2021/03/03/datahike-clojurescript.html" />

<p>Original post can be found <a href="https://lambdaforge.io/2021/03/03/datahike-clojurescript.html"> here </a>.</p>

<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/e9ad51e5e6f34b06ba535c6f5eff657b?sid=12441379-430c-4df1-92a2-247c6c848086" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

Web browsers are now extremely capable, but building a non-trivial web application still remains a boatload of work. Especially when building for an application that is capable of being offline and handling intermittent connectivity. This is without factoring in the complexity of modelling the domain of your application. Which by the way we think Datalog is exceptionally good at.

To build a web application you will have to use something to manage your client side UI state and data. Then figure out how you persist it. Do you persist it on the client? On the server? Across peers? Maybe you persist the data with a combination of these. How do you keep it synchronised? Each one of these questions is a rabbit hole. Which often results in ad hoc solutions being built. There is one thing that serves as the backbone to almost all modern web applications. That is a database. So the most logical solution is to create a universal database. One with a consistent interface and data distribution built-in.

Write data. Query data. Show data. Sounds much nicer right?

As a major step in this direction we are pleased to provide a tech preview of ClojureScript support for Datahike with persistence to IndexedDB in the browser.

What can I do with this preview?
This preview is supposed to be a basis for prototyping to help us guide our development and make sure Datahike will fit your use case. It is not intended for production use yet, but it should be solid enough to build a full fledged app.

Usage
The following functionality is included:

Create a store (memory & IndexedDB)
Transact
Query
Entity
History functionality
Pull API
Setup
You can include this preview in your deps.edn with the code below. This is currently only tested with shadow-cljs using the browser-repl. Further work is needed for advanced compilation (feedback on experiences welcome in Discord).
```clojure
io.replikativ/datahike {:git/url "https://github.com/replikativ/datahike.git"
                        :sha "b07247fc80ee06858e3417fa04d3015761e61975"}
```
The following is an example of how to use Datahike in your project.
```clojure
(ns my-app.prototype
  (:require [datahike.api :as d]
            [datahike.impl.entity :as de]
            [clojure.core.async :as async :refer [go <!]]))

(def schema [{:db/ident       :name
              :db/cardinality :db.cardinality/one
              :db/index       true
              :db/unique      :db.unique/identity
              :db/valueType   :db.type/string}
             {:db/ident       :sibling
              :db/cardinality :db.cardinality/many
              :db/valueType   :db.type/ref}
             {:db/ident       :age
              :db/cardinality :db.cardinality/one
              :db/valueType   :db.type/number}
             {:db/ident       :friend
              :db/cardinality :db.cardinality/many
              :db/valueType :db.type/ref}])


(def cfg-idb {:store  {:backend :indexeddb :id "idb-sandbox"}
              :keep-history? false
              :schema-flexibility :write
              :initial-tx schema})
```
Instead of :backend :indexeddb you can also use the memory backend with :memory.

Database interaction
We now show how to interact with the database interactively. All API calls return core.async channels, so if you want to use it inside of your application logic you need to wrap them in a go block and take from each resulting channel.
```clojure
  ;; Create an indexeddb store.
  (d/create-database cfg-idb)

  ;; Connect to the indexeddb store.
  (go (def conn-idb (<! (d/connect cfg-idb))))

  ;; Transact some data to the store.
  (d/transact conn-idb [{:name "Alice"
                         :age  26}
                        {:name "Bob"
                         :age  35
                         :_friend [{:name "Mike"
                                    :age 28}]}
                        {:name  "Charlie"
                         :age   45
                         :sibling [[:name "Alice"] [:name "Bob"]]}])

  ;; Run a query against the store.
  (go (println (<! (d/q '[:find ?e ?a ?v ?t
                          :in $ ?a
                          :where [?e :name ?v ?t] [?e :age ?a]]
                        @conn-idb
                        35))))

  ;; Use the Entity API for "Bob".
  (go
    (let [e (<! (d/entity @conn-idb 6))]
      (println (<! (e :name)))))


  ;; Use the pull API
  (go (println (<! (d/pull @conn-idb [:name :age] 6))))
  (go (println (<! (d/pull-many @conn-idb '[:name :age] [5 6]))))

  ;; Release the connection from the store.
  ;; This is necessary for deletion.
  (d/release conn-idb)

  ;; Delete the store. 
  ;; This can be done immediately after creation.
  ;; In a fresh browser session or after releasing the connection. 
  (d/delete-database cfg-idb) 
```
You can inspect the resulting IndexedDB through your browser dev tools and should be able to retrieve the durable data after reloading your browser tab.

For more database interactions you can find more at the branch README

How we currently develop this
To hack on this prototype clone this repository. The namespace for the api sandbox is located:

- dev/api_sandbox.cljs

You can also find the demo namespace that was used in the video at

- dev/demo.cljs

You will need Clojure and shadow-cljs installed.

The settings for starting your ClojureScript repl is as follows:

- Project type: shadow-cljs
- Build selection: :app
- Build to connect to: browser-repl

Our goal is merging the port including new features such as tuple support and improved transaction performance in the next months. We will support all major browsers, web workers, node.js and embedded JS environments. Our vision is a distributed unified address space for client and server side databases along the lines of the semantic web, but built based on fast P2P replication of our read scalable, immutable fractal tree data structure.

Ways to contribute
We are interested in tooling experience and suggestions. In particular we care about our API design, performance, integration into existing ecosystems (react with our partner Homebase, Electron, JS backends, Chrome apps, react native).