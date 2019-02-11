# Object-to-object mapping framework microbenchmark

Multi-layered applications often require to map between different object models (e.g. DTOs and entities). 
Writing such boiler plate mapping code is a tedious and error-prone task.
A lot of object-to-object mapping Java frameworks aims to simplify this work and automate it.
Some uses code instrospection (eg. Dozer). Other uses code generation (ex: MapStruct).
This micro-benchmark compares performance of 6 frameworks. Results could be compared to the benchmark of a code written manually. 

Benchmark are powered by a tool called [JMH](http://openjdk.java.net/projects/code-tools/jmh/) or also known as "Java Microbenchmarking Harness".
JMH is developed by the OpenJDK team. 

## Benchmarked object to object mapper frameworks

- [Dozer](https://github.com/DozerMapper/dozer)
- [MapStruct](http://mapstruct.org/)
- [ModelMapper](http://modelmapper.org/)
- [Selma](http://www.selma-java.org/)
- [Orika](https://github.com/orika-mapper/orika)
- [JMapper](https://github.com/jmapper-framework/jmapper-core)
- [BULL](https://github.com/HotelsDotCom/bull)

## Contributing to benchmark


Github is for social coding platform: if you want to add another mapping framework or optimize an existing one, we encourage contributions through pull requests from [forks of this repository](http://help.github.com/forking/). If you want to contribute code this way, please reference a GitHub ticket as well covering the specific issue you are addressing.


## Data model

The data model used by this benchmark is very basic. It comes from the [Comparison](https://github.com/jhalterman/modelmapper/blob/master/core/src/test/java/org/modelmapper/performance/Comparison.java) class from the ModelMapper framework.
It includes combinations which usually appear in Java Beans, such as:

* Object types
* Collections

![Data model UML diagram](/model.png)

## Launch the benchmark

_Pre-requisites: Maven 3.x and a JDK 7 (or above)_

``git clone git://github.com/arey/java-object-mapper-benchmark.git``

``mvn clean install``

``java -jar target/benchmarks.jar``

Optional: To run a single benchmark, such as MapStruct, use `java -jar target/benchmarks.jar MapStruct`

## Interpreting the Results

The benchmarks measure throughput, given in "ops/time". The time unit used is seconds.
Generally, the score represents the number of graph object mapped per second; the higher the score, the better.

## Results

Tests has been performed on:

* OS: macOS High Sierra
* CPU: 3.1 GHz Intel Core i7, 2 cores, L2 Cache (per Core): 256 KB,  L3 Cache: 4 MB
* RAM: 16 GB 1867 MHz DDR3
* JVM: Oracle 1.8.0_74-b02 64 bits

<table>
    <tr>
        <th>Benchmark</th><th>Mode</th><th>Samples</th><th>Score</th><th>Margin error (+/-)</th><th>Units</th>
    </tr>
    <tr>
        <th>Manual</th><td>thrpt</td><td>200</td><td>27 598 750</td><td>346 265</td><td>ops/s</td>
    </tr>
    <tr>        
        <th>MapStruct</th><td>thrpt</td><td>200</td><td>27 206 021</td><td>133 009</td><td>ops/s</td>
    </tr>
    <tr>
        <th>Selma</th><td>thrpt</td><td>200</td><td>26 205 612</td><td>185 326</td><td>ops/s</td>
    </tr>
    <tr>
        <th>JMapper</th><td>thrpt</td><td>200</td><td>23 377 962</td><td>124 537</td><td>ops/s</td>
    </tr>
    <tr>
        <th>Orika</th><td>thrpt</td><td>200</td><td>4 097 030</td><td>21 220</td><td>ops/s</td>
    </tr>
    <tr>       
        <th>ModelMaper</th><td>thrpt</td><td>200</td><td>323 791</td><td>3 172</td><td>ops/s</td>
    </tr>
    <tr>
        <th>Dozer</th><td>thrpt</td><td>200</td><td>84 113</td><td>331</td><td>ops/s</td>
    </tr>
    <tr>
        <th>BULL</th><td>thrpt</td><td>200</td><td>108 289</td><td>802</td><td>ops/s</td>
    </tr>
</table>

![Framework Comparison](results.png)


## Documentation

* [Micro-benchmark of Java mapping object frameworks](http://javaetmoi.com/2015/09/benchmark-frameworks-java-mapping-objet/) (french article)

## Generating plot

1. Run benchmark while exporting results to csv with `java -jar target/benchmarks.jar -rff results.csv -rf csv`
2. Use gnuplot to generate plot with `gnuplot benchmark.plt`. This will output `results.png`.

## Credits

* Uses [Maven](http://maven.apache.org/) as a build tool
* Uses [JMH](http://openjdk.java.net/projects/code-tools/jmh/) for Java Microbenchmarking Harness