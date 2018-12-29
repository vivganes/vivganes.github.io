---
layout: post
section-type: post
title: Design and Code to Choose the Husband Using MapReduce
date: '2014-03-24 10:37:57 +0530'
comments: true
tags:
  - hadoop mapreduce java
published: false
---
In the last blog post "[What is MapReduce? - An Exercise using Activity Based Learning](http://vivekganesan.com/what-is-mapreduce-an-exercise-using-activity-based-learning//)", the methodology of MapReduce was explained.  In this blog post, let me take it a step further.  Let us do the technical design and Java coding for the same problem "Choosing the Husband" explained in the previous blog post.

### Recap 
Remember that there are three phases in the MapReduce methodology.  
1. Map  
2. Shuffle & Sort (Which I simply call as 'Grouping')  
3. Reduce

Here is a recap of characters in our story.  

![](/images/character_names.png)

Before getting on to explain the technical design of the solution, let me highlight some important points in the MapReduce methodology.  

1. The input is split into multiple input-splits before being passed to Mappers.  
2. Each mapper worker is assigned one input-split.  
3. The Map phase has input format of key,value and output format of key,value.  
4. The Shuffle & Sort phase has input format of key,value and output format of key,{list of values}  
5. The Reduce phase has input format of key,{list of values} and output format of key,value  

### Assumption
"Choosing the Husband" problem explained in the previous blog post has images.  We had to identify people from images.  So, we should be writing code for image processing in this blog post, right?  No!  We are going to get rid of that image processing complexity by a convenient assumption.

The assumption is this: We will have two input files, with eight lines each.  Each line would have two words.  Each of these words denote the name of the person identified in the image.

For example, if the first photo contained Jaja and Jojo, the first line of the first file would read the following.

```text
jaja jojo
```
Second line denotes the people present in second photo and so on upto the first eight photos.  Thereafter, entries go into the second input file.  Thus, we would end up with two files with eight lines each, each line having exactly two words.

### Key-Value Input?? How?
If you have not noticed, see that I have mentioned in the "Recap" section that Map phase has input format of key,value.

Map is the first phase of the MapReduce process.  So, these two files, which we have, with two words in each line, should be the input to the Map phase.  Is this a key,value pair?  Not at all!  

MapReduce framework of Hadoop does this for you by doing the following default assignments for each line in the files.  
**Key** - Character Position of the starting of the line  
**Value** - The actual content of the line

For example, if the first line of the first file contains `jaja jojo`, then, for the first line (or split),  
**Key** - `0`  
**Value** - `jaja jojo`  

If the second line contained `jiji jojo`, then, for that line(or split),   
**Key** - `9`  
**Value** - `jiji jojo`

The key is nothing but the position of the line's first character in the file, starting from zero.  This key is not at all relevant as far as this "Finding the Husband" problem is concerned.

### Mapper - Sample I/O
Hadoop's MapReduce framework, by default, passes one split each to a mapper process.  By default, one split is equal to one line.

Thus, sample input of Mapper is   

```text
jaja jojo
```
According to our logic, we need the following output from this mapper.

```text
jaja - 1
jojo - 1
```

If the second line is

```text
jiji jojo
```

Then, we the output of second Mapper would be

```text
jiji - 1
jojo - 1
```


### Shuffle and Sort - Sample I/O
If both the above mappers' outputs are piped to the input of the next phase, that is, Shuffle and Sort, the output of Shuffle and Sort phase would be  

```text
jaja - {1}
jojo - {1,1}
jiji - {1}
```

### Reducer - Sample I/O
Reducer just adds the number of ones and consolidates the result as a single number.  So, if the above Shuffle and Sort output is piped to reducers, the output of first reducer would be

```text
jaja - 1
```

The output of the second reducer would be

```text
jojo - 2 (that is, 1+1)
```

The output of the third reducer would be

```text
jiji - 1
```

Remember, the above sample values were only "samples", chained all the way through the MapReduce process.  These are not the actual values taken from the sixteen photos in the previous post.  If not, how would we end up with only three reductions.  We must be ending up with five reductions, one for each contestant for the post of husband, right?

Hoping that you follow what I have told until now, I am proceeding to the dare-devilry of writing the code.

### A Good News
There is a good news.  Shuffle and Sort phase is already coded in the Hadoop MapReduce framework.  You have to code for Map and Reduce phases only.  Depending on the lines of code you write in Map and Reduce phases, your MapReduce code could do anything from a simple Word count to some complex Sentimental Analysis.

### Coding the Mapper
We will be using the language Java to code our program.  Refer to the sample I/O section of the mapper above.  Remember that one line is called one split.  Also, a mapper does processing on a split at a time.  

We will be writing a Java class to do the mapping functionality.  This class will be called `MatchMakerMapper`.  At this juncture, I must tell you that all classes doing the mapping functionality must extend another class called `Mapper` and must define a method called `map()`.

Thus, we are going to write a code, which would approximately look like the one below.

{% highlight java %}
pubic class MatchMakerMapper extends Mapper {
  
  public void map(){
  
  
  }

}
{% endhighlight %}

We will add more details to the above skeleton as we progress through this blog post.

We need to specify the input and output data types of the mapper somewhere right?  Even before that, what options do we have for input and output data types?  
1. Text - for string data  
2. IntWritable or LongWritable - for numeric data

There are other data types as well.  But, let us stick with these data types for the sake of simplicity and problem scoping.

Our Mapper will have the following data types:  

**Input**  
*Key* : LongWritable  
*Value* : Text  

**Output**  
*Key* : Text  
*Value* : LongWritable  

Ask yourself! Are these data types correct for Mapper?  If so, why?

We are going to communicate these data types to our Java program in the following way.

{% highlight java %}
public class MatchMakerMapper extends Mapper<LongWritable, Text, Text, LongWritable> {

  @Override
	public void map(LongWritable key, Text value, Context output){
	
	
	}

}
{% endhighlight %}

After the statement `extends Mapper`, you write the following things, in the following order:  
1. Input Key Data Type  
2. Input Value Data Type  
3. Output Key Data Type  
4. Output Value Data Type  

Similarly, as first two arguments of the `map()` method, we write the input key data type and the input value data type.

Now is the time to write the Mapper logic.  The Core Java language acts on Strings and not on Text objects.  To convert Text object to String, we need to invoke `toString()` method.  In String processing, Java provides a method called `split()`.  This method is used to split a sentence into its separate words.  Generally speaking, this method is used to split a string using a specific delimiter.

Remember that our input value will be the content of one line of the input file.  For example, `jaja jojo`.  If this needs to be split into two separate words, we need to invoke `split(" ")` method on this.  Notice that the delimiting character specified is white-space.

Combining the above two paragraphs, we can write the following piece of code.

{% highlight java %}
  String[] names = value.toString().split(" ");
{% endhighlight %}

If you need to emit an output a key, value pair from mapper, you could just call the `output.write()` method with the output key and value.  

In this mapper, we need to produce two outputs.  So, we need to call `output.write()` twice.  First time, key will be the first word, that is, `names[0]` and the second time, the key will be the second word, that is, `names[1]`.  Value will be 1 both the times.

There is a catch here. `names[0]` and `names[1]` are String objects.  But, output key data type is Text.  So, we need to create new Text objects from `names[0]` and `names[1]` like `new Text(names[0])` and `new Text(names[1])` respectively.

Thus, the output-emitting piece of code is here.

{% highlight java %}
  output.write(new Text(names[0]),new LongWritable(1));
  output.write(new Text(names[1]),new LongWritable(1));
{% endhighlight %}

Thus, assembling all the disjoint pieces, here is our complete story.

{% highlight java %}
package com.vivekGanesan;

import java.io.IOException;

import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Mapper;

public class MatchMakerMapper extends Mapper<LongWritable, Text, Text, LongWritable> {
	
	
	@Override
	public void map(LongWritable key, Text value, Context output) throws IOException, InterruptedException {
		
		//If more than one word is present, split using white space.
		String[] words = value.toString().split(" ");
		//each word contributes to a key-value pair
		output.write(new Text(words[0]), new LongWritable(1));
		output.write(new Text(words[1]), new LongWritable(1));
	}
}
{% endhighlight %}

### Coding the Reducer
Remember that the reducer's work starts only after "Shuffle & Sort" has done its work.  That way, each reducer will be called with one group (key,{set of values}) as input at a time.

Similar to the case of Mapper, the Reducer also will have its own input and output data types.

**Input**  
*Key* : Text  
*Value* : LongWritable  

**Output**  
*Key* : Text  
*Value* : LongWritable  

Similar to the case of Mapper, any class which does the Reducing functionality should extend a `Reducer` class and should define a `reduce()` method.

So, our skeleton reducer goes like this:

{% highlight java %}
public class MatchMakerReducer extends Reducer {
  
  public void reduce(){
  
  }

}
{% endhighlight %}

Similar to the case of Mapper, same conventions apply here as to which data types go where.  Thus, we end up having the following code in Reducer.

{% highlight java %}
public class MatchMakerReducer extends Reducer<Text, LongWritable, Text, LongWritable> {	
	@Override
	public void reduce(Text key, Iterable<LongWritable> values, Context output) {
		
	}
}
{% endhighlight %}

Oops! I forgot to tell you what an `Iterable` is.  `Iterable` is anything which can be sequentially traversed.  Thus, our set of {1,1,1,...,1} falls under the category of `Iterable`.

In order to traverse an `Iterable`, we can use a `for` loop.  In each iteration, we need to increment a counter to count the number of times a person has appeared in the photos.

Thus, we get the following code.

{% highlight java %}
        int count = 0;
		for(LongWritable value: values){
			count+= value.get();
		}
{% endhighlight %}

Then, we need a single `output.write()` method to collect the output key and value.  Output key is nothing but the input key, the name of the person.  Output value is the count.  Thus, we would write:

{% highlight java %}
      output.write(key, new LongWritable(count));
{% endhighlight %}

Hereby, we present the full reducer as follows.

{% highlight java %}
package com.vivekGanesan;

import java.io.IOException;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Reducer;

public class MatchMakerReducer extends Reducer<Text, LongWritable, Text, LongWritable> {
	
	@Override
	public void reduce(Text key, Iterable<LongWritable> values, Context output)
			throws IOException, InterruptedException {
		int count = 0;
		for(LongWritable value: values){
			count+= value.get();
		}
		output.write(key, new LongWritable(count));
	}
}
{% endhighlight %}

### Coding the Driver
The work does not stop here.  We need to code a common templatized driver class to invoke the Mapper and Reducer.  Here is the templatized driver class called  `MatchMakerDriver`.

{% highlight java %}
package com.vivekGanesan;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;


public class MatchMakerDriver extends Configured implements Tool{
	
	public static void main(String[] args) throws Exception {
		int res = ToolRunner.run(new Configuration(), new MatchMakerDriver(), args);
		System.exit(res);		
	}

	@Override
	public int run(String[] args) throws Exception {
		if (args.length != 2) {
			System.out.println("usage: [input] [output]");
			System.exit(-1);
		}

		Job job = Job.getInstance(new Configuration());
		job.setOutputKeyClass(Text.class);
		job.setOutputValueClass(IntWritable.class);

		job.setMapperClass(MatchMakerMapper.class);
		job.setReducerClass(MatchMakerReducer.class);

		job.setInputFormatClass(TextInputFormat.class);
		job.setOutputFormatClass(TextOutputFormat.class);

		FileInputFormat.setInputPaths(job, new Path(args[0]));
		FileOutputFormat.setOutputPath(job, new Path(args[1]));

		job.setJarByClass(MatchMakerDriver.class);

		job.submit();
		return 0;
	}
}
{% endhighlight %}

Here ends our coding effort.

### Packaging the Code
In order to run in Hadoop environment, the code has to be packaged in the form of a Java Archive (JAR) file.  If you would like to run your code in [Hortonworks Sandbox](http://hortonworks.com/products/hortonworks-sandbox/) VM, make sure you compile your code using Java 6.

### Running - Finding the Husband
The Husband can be found by running the JAR file in a Hadoop environment.  Refer to the [Hortonworks Community Tutorial](https://github.com/hortonworks/hadoop-tutorials/blob/master/Community/T09_Write_And_Run_Your_Own_MapReduce_Java_Program_Poll_Result_Analysis.md) for instructions on how to run this in [Hortonworks Sandbox](http://hortonworks.com/products/hortonworks-sandbox/) VM.

### Download the Code
You can download all the code mentioned in this tutorial, along with dependencies from the github repository named [vivganes/what-is-mapreduce-blog-post](https://github.com/vivganes/what-is-mapreduce-blog-post).


I hope that this post was informative and useful.  Feel free to pen down your comments here or to email me at vivek@vivekganesan.com.
