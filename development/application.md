---
title: Applikation
weight: 60
---

# Unit Tests

## Setup

### Mailserver

Der Mailserver läuft auf Port 25000.

{% highlight bash %}
$ php $BASEDIR/scripts/opus-smtp-dumpserver.php 2>&1 >>$BASEDIR/tests/workspace/logs/opus-smtp-dumpserver.log &
{% endhighlight %}
