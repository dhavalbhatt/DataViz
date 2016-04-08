# DataViz

The output is always going to be in hdfs format. We will have nested directory structures.

So Each aggregation will have its own directory. Inside this directory we have multiple directories with timestamp as part of the name. This timestamp represents the timestamp of the aggregation. Each timestamp directory has a bunch of files. It could also have no
files or empty files. We are only interested in filenames that start with part-.

So a single data file might be in the location
/output/tweet-aggregation/t-14856235000/part-00032

Another output file could be at
/output/hashtag-aggregation/h-14856235000/part-00000

Note that the timestamp is in milliseconds.
So for any ttimestamp you will further have to aggregate results from all part- files inside.
for realtime visualization, new timestamp directories will keep getting added at regular intervals.

Each part file will have tsv format(tab separated values). non-tab chacters will be part of data The first column will always be keywords or strings. These may not always be quoted strings. 

The rest of the columns will most likely have floating points or integers except in some cases such as bigrams where second column will
also be a word. 

There are two geolocation outputs, places and locations.

If you were looking in locations/ directory, the numbers there are coordinates, latitude and longitude.

For states, please look at places/ directory.

At the time of the analysis output, the tweets were not restricted to US. So you will have to extract state from the output if you are working with this output.

If the tweets were from US, you'll get "place, state" in the first column, for non-US tweets you'll get "city/region, country".
In the future, all tweets might come from US, so you won't have to handle the other countries. But it helps to have a clause in place for that.

In this sample output, the second and third columns are average sentiments and will always be floating point numbers. The last number is the number of tweets and will always be an integer. Sometimes you might only get numbers and the first column might be blank.
I have removed these outputs, but they might still be there in this sample output.

For most use cases, when you see integers, they will most likely be counts.

Contents of one of the files in the output
>>> cat ./output/places/p-1458672200000/part-00002
St Louis, MO    0.0     0.0     4
Manhattan, NY   0.0     0.0     4
California, USA 0.0     0.0     4
Vancouver, British Columbia     0.0     0.0     4
Palo Alto, CA   0.0     0.0     4
Florida, USA    0.0     0.0     4
Catalina Foothills, AZ  0.0     0.0     4
Ukraine 0.0     0.0     4

I am attaching a gzipped output directory with the above structure.
