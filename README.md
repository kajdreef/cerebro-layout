# Cerebro-Layout

## How to run?
### Collecting Data
Collecting the data is done by using the tool [tacoco](github.com/spideruci). Tacoco is a tool which allows us to run the test suite of a java program independent of its build system with a prespecified isntrumenter. In our case we are interested in capturing the runtime data at method level of the program, we do this by using [Blinky](github.com/spideruci/blinky) (an on-the-fly java bytecode instrumenter).

The following steps need to be taken to setup up our data collecting system:
1. Get the projects (and their dependencies) and compile them (further instructions can be found on their respective project wiki's):
```
git clone https://github.com/inf295uci-2015/primitive-hamcrest.git  
cd primitive-hamcrest  
mvn test # just to make sure that everything works  
mvn install
cd ..
git clone https://github.com/spideruci/blinky.git
cd blinky/
mvn compile && mvn test
cd ..
git clone https://github.com/spideruci/tacoco.git
cd tacoco
mvn compile && mvn test
```
2. Modify the blinky **blinky-analyzer.config** in [blinky-tacoco](https://github.com/spideruci/blinky/blob/master/blinky-tacoco/src/main/resources/blinky-analyzer.config).
    + The -javaagent should point to your compiled blinky-core
    + the -cp should also point to your compiled blinky-tacoco
3. Modify the run-blinky-tacoco script in tacoco/script make sure to modify the **/abs/path/to/** to your own directories:
    + -Dtacoco.inst.xboot=~/.m2/repository/org/ow2/asm/asm-all/5.0/asm-all-5.0.jar:**/abs/path/to/**blinky/blinky-core/target\
    + -Danalyzer.opts="**/abs/path/to/**blinky/blinky-tacoco/src/main/resources/blinky-analyzer.config"\
    + -Dtacoco.inst=/**/abs/path/to/**blinky/blinky-core/target/blinky-core-0.0.1-SNAPSHOT.jar\
4. Run the ./script/run-blinky-tacoco from the tacoco root directory. The traces will be located in: tacoco-output/

### Run Cerebro-Layout on Collected Data

1. Compile and package cebro-layout by running mvn package in the root of cerebro-layout
2. Run the program
```

```

## Visualize using Cerebro