---
layout: page
excerpt: 'Vivek Ganesan - A Techie, An Author, A Teacher, a blah, blah and a Blah!'
tags:
  - Vivek
  - Ganesan
  - Blameless Continuous Integration
  - Agile
  - Coach
  - CSM
  - SAFe
  - Big Data
  - Hadoop
published: true
title: Who is Vivek?
---



Vivek Ganesan is the author of the book [Blameless Continuous Integration](https://www.amazon.com/dp/1482889633/ref=sr_1_1?s=books&ie=UTF8&qid=1493349176&sr=1-1) and a secret 'super hero' at [SolutionsIQ](http://solutionsiq.in/) who helps organizations, teams and individuals to be better and happier than they are. He lives in Hyderabad and spends his leisure time envisioning and [writing](http://vivekganesan.com/posts/) about technology and agile software development and sometimes, [singing](https://soundcloud.com/vivek-ganesan/tracks) in his bathroom.

{% include youtubePlayer.html playlistid=PLtQT0a2cx00ZLO9sclfoWeoeE4JyWtCtD %}

Vivek is an agile practitioner.  He is a [Certified Agile Coach](https://icagile.com/Learning-Roadmap/Agile-Coaching/Agile-Coaching), [SAFe Agilist][], [Certified Scrum Professional][] (CSP), [Certified ScrumMaster][] (CSM), a learner and a public speaker too.  He spoke at [Agile India 2015](http://2015.agileindia.org/), [DevOps Conference - Bangalore](http://www.agileglobalevent.com/conference/devops/devops-conference-bangalore), [Discuss Agile Conferences](http://www.discussagile.com/), [XP Conference](http://xpconference.in/), [Business Agility Roadshow 2017](http://baroadshow.agilecoffeetalk.com/), [BizDevOps Master Webinar Series](https://www.youtube.com/watch?v=i4CpS14E7Eo&list=PLaM7bIEFx40uTfQFcSWA_wKd9uXvkFLDx&index=2), etc.

Vivek is an [open-source enthusiast](https://github.com/vivganes/) and has contributed to open-source projects like [Mozilla.org][], [Hadoop][], [HBase][], [Karma][], etc.  He also authored some tutorials in the Community Tutorials section of [Hortonworks Sandbox][] VM.

Vivek has spoken at various tech conferences including [Dreamforce 2014][], [Dreamforce 2015][], [JavaOne][] India 2013, Powe’R’ ahead with Data Science, etc. He is a [Data Science][] enthusiast.

You can follow Vivek on [Twitter][], if you would like to catch up with his thoughts.

  [Gainsight]: http://www.gainsight.com
  [JavaOne]: http://www.oracle.com/javaone/index.html
  [Data Science]: http://en.wikipedia.org/wiki/Data_science
  [Mozilla.org]: http://www.mozilla.org
  [Hadoop]: http://hadoop.apache.org
  [HBase]: http://hbase.apache.org
  [Karma]: https://github.com/karma-runner/karma
  [Hortonworks Sandbox]: https://github.com/hortonworks/hadoop-tutorials/
  [Dreamforce 2014]: http://www.salesforce.com/dreamforce/DF14/
  [Dreamforce 2015]: http://www.salesforce.com/dreamforce/DF15/
  [Twitter]: https://twitter.com/Vivek_Ganesan
  [SAFe Agilist]: http://www.scaledagileacademy.com/default.asp?page=safeagilistsa
  [Certified Scrum Professional]: https://www.scrumalliance.org/certifications/practitioners/csp-certification
  [Certified ScrumMaster]: https://www.scrumalliance.org/certifications/practitioners/certified-scrummaster-csm
  
  <div>
    <h2>Recent Posts</h2>
    <ul id="recent_posts">
      {% for post in site.posts limit: site.recent_posts %}
      <li>
        <a href="{{ root_url }}{{ post.url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ul>
  </div>
