MAIN=WordCount

#OBJ=donq.txt
#OBJ=donk.txt
OBJ=donquijote.txt

SRC= \
  $(MAIN).java \
  $(MAIN)Mapper.java \
  $(MAIN)Reducer.java

CLASSES=$(SRC:.java=.class)

HADOOP_CLASSPATH=$(shell hadoop classpath)

all: makebin $(MAIN).jar

$(MAIN).jar: $(CLASSES:%.class=bin/%.class)
	jar cvfe $@ $(MAIN) -C bin/ .

makebin: 
	mkdir -p bin

bin/%.class: src/%.java
	javac -Xlint:deprecation -sourcepath src -cp $(HADOOP_CLASSPATH) -d bin $<

run:
	hadoop fs -mkdir -p $(MAIN)
	hadoop fs -put -f $(OBJ) $(MAIN)/
	hadoop fs -rm -r -f $(MAIN)/results
	hadoop jar $(MAIN).jar $(MAIN)/$(OBJ) $(MAIN)/results
	hadoop fs -cat $(MAIN)/results/part*
	
clean:
	$(RM) -rf bin *.jar *~ */*~
