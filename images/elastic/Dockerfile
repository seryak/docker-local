FROM elasticsearch:5.6.15

RUN apt-get update
RUN apt-get install -y mc
 
RUN elasticsearch-plugin install http://dl.bintray.com/content/imotov/elasticsearch-plugins/org/elasticsearch/elasticsearch-analysis-morphology/5.6.15/elasticsearch-analysis-morphology-5.6.15.zip
 