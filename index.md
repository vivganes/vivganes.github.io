---
layout: page
excerpt: 'Vivek Ganesan - A Techie, A Teacher, a blah, blah and a Blah!'
tags:
  - Vivek
  - Ganesan
  - Agile
  - Coach
  - CSM
  - SAFe
  - Big Data
  - Hadoop
published: true
title: Who is Vivek?
---



Vivek Ganesan is a secret 'super hero' who holds a full time job as a Servant Leader for awesome self-organizing teams at [Gainsight][], a Big Data Customer Success Start-up. He lives in Hyderabad and spends his leisure time envisioning and writing about technology and agile software development, writing [blogs advocating men's rights](http://in.avoiceformen.com/author/vivek/) and sometimes, singing in his bathroom.

![](/images/super_hero.png)

Vivek is an admirer of Agile philosophy.  He is a [Certified Agile Coach](https://icagile.com/Learning-Roadmap/Agile-Coaching/Agile-Coaching), [SAFe Agilist][], [Certified Scrum Professional][] (CSP), [Certified ScrumMaster][] (CSM), a learner, an aspiring Agile Coach and a public speaker too.  He spoke at [Agile India 2015](http://2015.agileindia.org/), [Discuss Agile Conferences](http://www.discussagile.com/), [XP Conference](http://xpconference.in/), etc.

Vivek is an [open-source enthusiast](https://github.com/vivganes/) and has contributed to open-source projects like [Mozilla.org][], [Hadoop][], [HBase][].  He also authored some tutorials in the Community Tutorials section of [Hortonworks Sandbox][] VM.

Vivek has spoken at various tech conferences including [Dreamforce 2014][], [Dreamforce 2015][], [JavaOne][] India 2013, Powe’R’ ahead with Data Science, etc. He is a [Data Science][] enthusiast.

You can follow Vivek on [Twitter][], if you would like to catch up with his thoughts.

P.S: Don't tell anyone that he is the Chief Admin & Editor of [A Voice for Men (India)](http://in.avoiceformen.com/)

  [Gainsight]: http://www.gainsight.com
  [JavaOne]: http://www.oracle.com/javaone/index.html
  [Data Science]: http://en.wikipedia.org/wiki/Data_science
  [Mozilla.org]: http://www.mozilla.org
  [Hadoop]: http://hadoop.apache.org
  [HBase]: http://hbase.apache.org
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
