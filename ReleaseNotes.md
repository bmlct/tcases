# Release Notes #

## 1.5.4 ##

  * Fixes the ```tcases``` and ```tcases-reducer``` commands to correctly support the ```-R``` option.

  * Refactor XML document readers to use ```org.xml.sax.Attributes.getQName()```. This is more correct than ```getLocalName()```,
    which can return an empty string in some JVM implementations, resulting in a parser failure.

## 1.5.3 ##

  * Fixes a defect that caused the ```tcases``` command to fail when reading a system input definition from standard input.

  * Reducer: When ```newSeed``` is true, ensure that a new seed is written even when the initial round is already minimal.

  * Suppose a variable only has N values, but the number of test cases generated is more than N. Assuming there are no constraints on these N values, you'd like
    for each of them to be used by roughly the same number of test cases. 
    This release fixes a defect that was blocking that even distribution of values.
    Why does this matter? Because this increases test case variety, which could make it more likely that some test case will expose a defect.

## 1.5.2 ##

Ever wonder if a different random seed might lead to more interesting test cases? Now it's easier to find out: try the ```-R``` option at the ```tcases``` command line. Or, if you're using the Tcases Maven Plugin, the ```newSeed``` parameter does the same thing. This is like the ```-r``` option (or the ```seed``` parameter), except that Tcases picks the seed value for you.

Similarly, when using the Tcases Reducer, you might wonder if a different seed might produce an equally small but more interesting set of test cases.
So you can also use ```-R``` (or ```newSeed```) with the Tcases Reducer, which tells it to ignore any previous random seed
in the current generator definition and to search for a new minimizing seed value.

## 1.5.1 ##

  * HTML test case reports: Tcases output is often used to guide manual testing. But let's face it -- reading XML is not a lot of fun. So now you can ask Tcases to produce test case definitions in the form of an [HTML report](http://www.cornutum.org/tcases/docs/Tcases-Guide.htm#html).

## 1.5.0 ##

  * Better performance: Due to an improved constraint solver, Tcases generates results much faster, even for large and complex input models that previously caused Tcases to "freeze". Although some models may still face problematic performance, these cases are now better described in the [Troubleshooting FAQs](http://www.cornutum.org/tcases/docs/Tcases-Guide.htm#trouble), along with suggestions for fixes. But note that this change is not completely backward-compatible. The test cases produced by this version may not be identical to those produced by previous versions of Tcases, although they will be equivalent in coverage. Also, as a result of the new algorithm, Tcases is slightly less likely to honor "once-only" hints, although this will not affect most input models.

  * Output transformations: For more flexibility when transforming the test definition hierarchy, replace "test case annotations" with "system annotations" and "function annotations".

  * Windows *.bat scripts: Fix initialization of logging control variables.

  * Reducer: Fix a defect that caused Reducer to ignore the actual generator definition during its test case generation rounds.
  
## 1.4.0 ##

  * Introducing [Output Annotations](http://www.cornutum.org/tcases/docs/Tcases-Guide.htm#annotations): For an output transformation to produce concrete test cases, sometimes the basic information in the input model is not enough. You need to add extra information that is not important for generating the test cases but is necessary to form the final output. That's what output annotations are for.

  * JUnit output: To assist completion of test case code, Tcases now adds comments listing all input variable values in the Given section of each @Test method body. But if you prefer the previous output format, you can exclude these comments using the command line option `-p values=false`.
  
  * See [Troubleshooting FAQs](http://www.cornutum.org/tcases/docs/Tcases-Guide.htm#trouble) for more help on what to do when things go wrong. This includes more info on how to control Tcases logging output, including how to redirect logging to standard output. Also, logging messages have been improved to make it easier to understand what's going on.

  * Reducer: For better performance, reduce test cases for each function independently

## 1.3.1 ##

  * To better support embedding in other apps, add stream-based methods for generating ([Tcases.getTests](http://www.cornutum.org/tcases/docs/api/org/cornutum/tcases/Tcases.html)) and exporting ([Tcases.writeTests](http://www.cornutum.org/tcases/docs/api/org/cornutum/tcases/Tcases.html)) test case definitions.

## 1.3.0 ##

  * The **once** attribute applies only to a default 1-tuple for a single variable. But now there is now a more general way to define once-only exceptions to higher-order combinations, by adding [Once elements](http://www.cornutum.org/tcases/docs/Tcases-Guide.htm#once-tuples) to your generator definition.

  * Tcases Maven Plugin: Use parameter=project to more easily select a single project.

## 1.2.2 ##

  * Tcases Guide: Rework to avoid inadvertent substitution of Maven properties.

## 1.2.1 ##

  * Reducer: Improvements to logging make it easier to track progress.

## 1.2.0 ##

  * Introducing the [Tcases Reducer](http://www.cornutum.org/tcases/docs/Tcases-Guide.htm#reduce), which helps automate the search for a smaller set of test cases.

## 1.1.1 ##

  * For XML input files, Tcases now validates the attributes specified for all elements. Tcases reports an error if any attribute is unknown or invalid.

## 1.1.0 ##

  * Restructured as Maven project containing multiple modules, all downloadable from the Maven Central repository. See [HowToDownload](HowToDownload.md).

  * Now available as a [Maven plugin](http://www.cornutum.org/tcases/docs/tcases-maven-plugin/), so you can use Maven to generate test cases directly from the system input definitions for your Maven project.

## 1.0.1 ##

  * If generating JUnit (using the -J option), use a more useful default output file name of the form **${projectName}Test.java**. If necessary, convert the **${projectName}** part of the file name into a valid Java identifier. Consequently, -J does not have to be accompanied by -f to get good results.

  * When reading a system input definition document, report a failure for any reference to an undefined property. Write a WARN log message for any property definition that is not actually used.
