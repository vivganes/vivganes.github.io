---
layout: post
section-type: post
title: What is MapReduce? - An Exercise using Activity Based Learning
date: '2014-03-22 18:17:23 +0530'
comments: true
categories: hadoop mapreduce teaching
published: true
---
Whenever I have the chance to explain somebody the process of MapReduce, I find it demoralising that "Word Count" is the only example found on almost all places in the internet.  I could not recommend any reading material which gives them more insight than a simple word count.  Yet, something good came out of this problem.  I was forced to think of a simple-enough-scenario to apply MapReduce and write a blog post about it.  And, here I am, writing a blog post titled "What is MapReduce?".

I am going to let out a super secret that I have been keeping for a while.  I am going to tell you how I would actually teach a person about MapReduce, if I am the teacher.  This blog post is based on "Activity Based Learning" where the students would do some real activity and learn from the same.

Enough of front matter, let me get on to the topic.  We are going to start with a story that will be the base to our activity.  And, here is that story.

## The Story - Choosing the Husband

Long long ago, there was a nation ruled by a mighty king.  He had a beautiful daughter, who was adored by everyone in the kingdom.  As she reached the age of marriage, five young men from the country proposed to her.  Their names were  

1. Jaja  
2. Jiji  
3. Juju  
4. Jojo  
5. Jinjin   
  
Actually, these five young men were already friends of the princess.

Now, the choice rests with the princess.  The princess liked the five equally.  But, she can marry only one among the five.

After a lot of thought process, she came up with a plan.  One fine day, she called all the five young men.  She said, "I like each of you.  But, I can marry only one.  I want to choose my better half using a fair process. Here is the plan.  I like to travel a lot.  I want my life partner to have similar likings as me.  So, I will set up secret cameras (come on, don't cry, this is just a story) in the places I like to visit in this country.  These secret cameras will take still photos at random times.  This will go on for one month."

She added, "For the next one month, you guys go on with your usual life.  Whoever occurs most in the photos captured by the secret cameras will be my husband.I will announce my husband publicly on the day next to the end of one month."

She also warned, "Beware, any foul-plays will automatically disqualify you."

A full month passed by.  The princess checked the photos from cameras and found that there were 16,000 photos in total.  Yes, sixteen thousand!  She has a deadline of one day to announce the results.  How is she going to process all sixteen thousand photos in a day?
Yes, she is currently facing a Big Data problem.

The princess thought of her problem and came to the only person whom she thought had the brains to help her in this problem, you :)  Yes, she came to you and asked for help.

## The Action - Choosing the Husband 

The story ends here and our action starts here. For the purpose of simplicity, let us assume we have 16 photos and not 16,000 photos.  You have a team of five people under your command to perform whatever you order them to do.

### Step-1: Identification
The first and foremost problem is to identify the people in the photos.  For that, we need reference photos of those five people.  Here is a single image, which shows the faces of all the five guys, along with their names.

![](/images/character_names.png)

For a successful identification of a person in any photo, play close attention to the following details.  

1. The Hair style  
2. Does the person wear spectacles or not  
3. Beard

These three features are enough to identify a person in the photos.

Now, coming to the photos, here are they.  I have made these photos in such a way that each photo contains two and only two of our guys.  There might be a third person in some photos.  But, that third person will not be one of our guys and you can ignore him.

![](/images/1.png)
![](/images/2.png)
![](/images/3.png)
![](/images/4.png)
![](/images/5.png)
![](/images/6.png)
![](/images/7.png)
![](/images/8.png)
![](/images/9.png)
![](/images/10.png)
![](/images/11.png)
![](/images/12.png)
![](/images/13.png)
![](/images/14.png)
![](/images/15.png)
![](/images/16.png)


Split your team into two sub-teams.  Give 8 photos to one sub-team and the remaining 8 to the next sub-team.  Ask the teams to identify the persons in the photos and record it in a sheet of paper.

STOP HERE! There is a rule which I forgot to tell you.  The sub-teams have to record the identification in a particular format.  For each person they identify in each photo, an entry has to be made like this in the sheet of paper given to them.

```text
<name> - 1
```

For example, in the first photo, if the sub-team finds Jaja and Jojo, then the sheet should contain entries as follows.

```text
jaja - 1
jojo - 1
```
In the second photo, if Jaja is found again, a fresh entry has to be made in the sheet and the count of the already existing `jaja` should not be touched.  So, for example, if the second photo contains Jaja and Jiji, then, the sheet must look like the one below.

```text
jaja - 1
jojo - 1
jaja - 1
jiji - 1
```

Now, ask the sub-teams to do their job and once they are done with all the eight photos given to each of the sub-teams, there will be 16 lines in each sheet of paper.  This is because, each photo will certainly contain two of our guys.

### Step-2: Grouping
Now, collect the two sheets of papers with 16 lines each from the sub-teams.  Remember that your team size is 5.  Now, lets assign work to each individual and you will also do a part of the work.

Take five blank sheets of paper and write each guy's name on the top of the sheet.  For example, the first sheet will have `JAJA` written on top of it, the second sheet will have `JIJI` and so on.

Give each sheet to each person in the team.  So, each person in your team will end up having one sheet each.

Remember that you have two sheets as output of step-1.  You, the commander, should read-out each line in those sheets one by one.  And, the team members, should listen for their guy's mention.

For example, you shout "jaja - 1", then, the guy who holds the JAJA paper would write `1` in his paper.  Next, you shout "jojo - 1" the, the guy who holds the JOJO paper would write `1` in his paper.  If a name repeats, another `1` has to be written.  The existing `1` should never be disturbed.

Thus, following the above rules, the JAJA sheet could possibly look like the one below.

```text 
1
1
1
1
1
```
### Step-3: Consolidating

The next step is the easiest one.  Now, collect the sheet of papers from your team members and distribute the same sheets but to different people.  In short, the person holding JAJA sheet in second step should not hold JAJA sheet in this step.

Ask the five team members to count the number of `1`s in each sheet and write the number in BIG letters in the reverse side of the same sheet.  Also, ask them to write the guy's name in BIG letters in the reverse side of the sheet also.

So, for example, if JAJA paper had 5 ones, the reverse of that paper would look like the following.

```text
JAJA
========
5
```
Now, at the end of this step, you would know how many times each person has appeared in the photos and you can tell the princess who her husband would be.

An interesting fact is that, without even knowing, you have used MapReduce manually to select the husband of the princess.

## What is MapReduce?
MapReduce is a framework/philosophy/algorithm/methodology which helps us solve certain complex problems by divide-and-rule technique.  

MapReduce assumes that you have more than one workers, who can do the work for you.  In our case, we had 5 workers and 1 master.  MapReduce takes the advantage of parallel processing done by many workers so that more work is done in less time.

Not all jobs can be parallelly executed.  Only certain jobs can be executed parallely.  In the example above, consolidation and identification cannot be parallely executed.  It is necessary that consolidation can be done only after identification and grouping has happened.

## Phases of MapReduce
Similar to our exercise above, MapReduce has three phases.

### Phase 1 - Mapping
Mapping is nothing but the identification.  In our example, you mapped a number, that is, 1 to a name.  Or, you put the number 1 in the bucket named 'JAJA'.  This association or identification is called mapping.

Output of mapper is always a set of key-value pairs.  Here, in our example, key is the name of the person and value is always one.

### Phase 2 - Shuffle & Sort
Shuffle and sort is nothing but grouping all the mapped values according to the key.  Remember, the key in the mapper is the name of the person.  In our example, we grouped all the values, that is, the ones under the persons' names.

We could also have chosen to sort the groups based on key, that is the name of the person.  That way, we would have arranged the papers in the order Jaja, Jiji, Jinjin, Jojo and Juju if we followed alphabetic sorting.

The output of shuffle & sort phase is always a set of key-value pairs where each value is again a set of values.  For example, Jaja is the key and value = {1,1,1,1,1}

### Phase 3 - Reducing
Reducing is the job of consolidating several numbers(ones) into a single number for each group resulting from Phase 2.  This final single number for a group is the net result targeted by the problem, with which we can arrive at a final solution to the problem.

For example, looking at the numbers on the reverse of the sheet, we can know who has appeared most number of times in the photos and hence, we could advise the princess about who her husband would be.

### A Note on Parallel Processing
Throughout our entire process, the following parallel processings took place.  
1. Parallel processing of sub-teams (Mappers) in Phase - 1  
2. Parallel processing of team members (Reducers) in Phase - 3

In other words, Phase - 2 is the only non-parallel process in the whole work flow.  If we had 16,000 photos also, it would just be a matter of number of workers to solve the problem within one day.

Thus, adjusting the number of workers, we can arrive at a solution today, tomorrow or next week.  This is called scaling.  MapReduce is the hot topic in BigData Processing because it can scale.

That's it from my side for this post.  You can refer to all the materials referred in this post in the github repository named [vivganes/what-is-mapreduce-blog-post](https://github.com/vivganes/what-is-mapreduce-blog-post)

Hope this blog post was interesting and enlightening.  I am eager to hear your comments.  Please post your comments here or email me at vivek@vivekganesan.com.

P.S.: I snap-shotted the pictures from [BitStrips Facebook App](https://apps.facebook.com/bitstrips/)
