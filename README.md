# Sentiment_analysis_using_social_media_data
Sentiment analysis using twitter data and visualise it using Tableau.

Analyzing sentiment using Twitter Data. Extract data from twitter using flume
and analyzing data using Hive

1. Setting up raw data folders in HDFS and copy the data
make directory(data) and subdirectories(dictionary, time_zone_map, tweets_raw) in /user/cloudera
#hadoop fs -mkdir /user/cloudera/data
#hadoop fs -mkdir /user/cloudera/data/dictionary
#hadoop fs -mkdir /user/cloudera/data/time_zone_map
#hadoop fs -mkdir /user/cloudera/data/tweets_raw

copy the dictionary files and time_zone_map data to the respective folders
#hadoop fs -put /home/cloudera/Data/dictionary/dictionary.tsv /user/cloudera/data/dictionary/dictionary.tsv

#hadoop fs -put /home/cloudera/Data/time_zone_map/time_zone_map.tsv /user/cloudera/data/time_zone_map/time_zone_map.tsv 


2. Extract Data from Twitter using Flume
Step 1: Download file flume-sources-1.0-SNAPSHOT.jar from the url

http://www.thecloudavenue.com/2013/03/analyse-tweets-using-flume-hadoop-and.html

or from

http://files.cloudera.com/samples/flume-sources-1.0-SNAPSHOT.jar

create folder in myjars in /usr/lib/flume-ng. 
#sudo mkdir /usr/lib/flume-ng/myjars

Put this file in /usr/lib/flume-ng/myjars
#sudo cp /home/cloudera/Desktop/Projects/flume-sources-1.0-SNAPSHOT.jar /usr/lib/flume-ng/myjars/


Step 2: Create a new app with apps.twitter.com. Generate the access tokens. Copy the consumer tokens and access tokens and use them in the Twitter.conf file below.

Step 3:
Create a config file called twitter.conf with below data and put it in the folder and provide full access to it(i.e full read and write access)
/usr/lib/flume-ng/conf
#sudo cp /home/cloudera/Desktop/Projects/twitter_conf3.conf /usr/lib/flume-ng/conf/
#sudo chmod -777 /usr/lib/flume-ng/conf/twitter_conf3.conf

Step 4: 
Modify the file /usr/lib/flume-ng/conf/flume-env.sh file. Add the below line

FLUME_CLASSPATH="/usr/lib/flume-ng/myjars/flume-sources-1.0-SNAPSHOT.jar"
#vi /usr/lib/flume-ng/conf/flume-env.sh
(enter i , copy the class path, enter ctrl+esc, enter :wq!)


Step 5: 
Run the following commands
cd /usr/lib/flume-ng/bin 
./flume-ng agent -n TwitterAgent -c conf -f ../conf/twitter_conf3.conf 

(or)

/usr/lib/flume/bin/flume-ng agent -conf ./conf/ -f/etc/flume/conf/twitter_conf.conf -Dflume.root.logger=DEBUG, console -n TwitterAgent


Step 6: Check the downloaded twitter docs in HDFS
hdfs dfs -ls /user/cloudera/data/tweets_raw/flume-23423432453

3. Import data into Hive and perform analysis
step 1: make sure that the hive-hcatalog-core.jar existed in the respective folders.
#ls /usr/lib/hive-hcatalog/share/hcatalog/
if it existed in different folders, need to modify the tweets.sql file


4. Integrate Excel-2013 or Tableau with Hiveserver2
1. Download Tableau from the below link and install it

https://www.tableau.com/products/trial

2. Download and install hive drivers from the below link as per your system configuration and version of Tableau and cloudera version.

http://www.cloudera.com/downloads/connectors/hive/odbc/2-5-12.html

3. Open cloudera vm

4. Tableau - Hadoop integration Instructions
