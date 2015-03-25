---
layout: post
title:  "Flush SOLR index"
date:   2015-03-25 13:01:22
category: devops
tags: [devops, solr]
---

Sometimes, specially in QA/UAT environments, it is required to delete all documents indexed in your [Solr][solr] index. The folling scripts will get that done:

{% highlight bash %}
#!/bin/bash

SOLR_URL="http://localhost"
SOLR_PORT="8983"
SOLR_PATH="/solr"
DELETE="stream.body=<delete><query>*:*</query></delete>"
COMMIT="stream.body=<commit/>"

curl "'${SOLR_URL}:${SOLR_PORT}${SOLR_PATH}/update?${DELETE}'"
curl "'${SOLR_URL}:${SOLR_PORT}${SOLR_PATH}/update?${COMMIT}'"
{% endhighlight %}

The first `curl` call requests the index to be deleted and the second one commits the change in case it's not enabled on the server.

[solr]:   http://lucene.apache.org/solr
