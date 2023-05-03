Download Link: https://assignmentchef.com/product/solved-cs2030-lab-6-class-roster
<br>



<h1>Task Content</h1>

<table width="680">

 <tbody>

  <tr>

   <td colspan="3" width="680"><strong>Class Roster</strong><strong>Topic Coverage</strong>OptionalFunctional Interface and Lambda<strong>Problem Description</strong>Your task is to read in a roster of students, the modules they take, the assessments they have completed, and the grade for each assessment. Then, given a query consisting of a triplet: a student, a module, and an assessment, retrieve the corresponding grade.For instance, if the input is:

    <table width="607">

     <tbody>

      <tr>

       <td width="607">Steve CS1010 Lab3 ASteve CS1231 Test A+ Bruce CS2030 Lab1 C</td>

      </tr>

     </tbody>

    </table>and the query is Steve CS1231 Test, the program should print A+.In our scenario, a roster has zero or more students; a student takes zero or more modules, a module has zero or more assessments, and each assessment has exactly one grade. Each of these entities can be uniquely identified by a string.This lab is a continuation of the lab on <a href="https://codecrunch.comp.nus.edu.sg/task_view.php?tid=5183">Immutable Map</a>.You will need to refer to the <a href="https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Optional.html">Java documentation of Optional</a> to familiarize yourself with the APIs available.<strong>Level 1</strong>Write a Student class that stores the modules he/she reads in an immutable map via the put method. A student can read zero or more modules, with each module having a unique module code as its key.</td>

  </tr>

  <tr>

   <td width="37"> </td>

   <td width="607">jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”)$.. ==&gt; Optional[{Lab1: B}] jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))$.. ==&gt; Tony: {CS2040: {{Lab1: B}}} jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get($.. ==&gt; Optional[CS2040: {{Lab1: B}}] jshell&gt; Student natasha = new Student(“Natasha”);</td>

   <td width="37">“CS204</td>

  </tr>

 </tbody>

</table>

<table width="566">

 <tbody>

  <tr>

   <td width="566">class KeyableMap&lt;V extends Keyable&gt; implements Keyable {… }</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”)$.. ==&gt; Optional[{Lab1: B}] jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)))$.. ==&gt; Tony: {CS2040: {{Lab1: B}}} jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get(“CS204$.. ==&gt; Optional[CS2040: {{Lab1: B}}] jshell&gt; Student natasha = new Student(“Natasha”); natasha ==&gt; Natasha: {} jshell&gt; natasha = natasha.put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))) natasha ==&gt; Natasha: {CS2040: {{Lab1: B}}} jshell&gt; natasha.put(new Module(“CS2030”).put(new Assessment(“PE”, “A+”)).put(new Assessment(“Lab2$.. ==&gt; Natasha: {CS2040: {{Lab1: B}}, CS2030: {{PE: A+}, {Lab2: C}}} jshell&gt; Student tony = new Student(“Tony”);tony ==&gt; Tony: {} jshell&gt; tony = tony.put(new Module(“CS1231”).put(new Assessment(“Test”, “A-“)))tony ==&gt; Tony: {CS1231: {{Test: A-}}} jshell&gt; tony.put(new Module(“CS2100”).put(new Assessment(“Test”, “B”)).put(new Assessment(“Lab1”,$.. ==&gt; Tony: {CS1231: {{Test: A-}}, CS2100: {{Test: B}, {Lab1: F}}} jshell&gt; new Module(“CS1231”).put(new Assessment(“Test”, “A-“)) instanceof KeyableMap$.. ==&gt; true jshell&gt; new Student(“Tony”).put(new Module(“CS1231”)) instanceof KeyableMap$.. ==&gt; true jshell&gt; /exit |  Goodbye</td>

  </tr>

 </tbody>

</table>

natasha ==&gt; Natasha: {}




jshell&gt; natasha = natasha.put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))) natasha ==&gt; Natasha: {CS2040: {{Lab1: B}}}




jshell&gt; natasha.put(new Module(“CS2030”).put(new Assessment(“PE”, “A+”)).put(new Assessment(“Lab2

$.. ==&gt; Natasha: {CS2040: {{Lab1: B}}, CS2030: {{PE: A+}, {Lab2: C}}}




jshell&gt; Student tony = new Student(“Tony”);

tony ==&gt; Tony: {}




jshell&gt; tony = tony.put(new Module(“CS1231”).put(new Assessment(“Test”, “A-“)))

tony ==&gt; Tony: {CS1231: {{Test: A-}}}




jshell&gt; tony.put(new Module(“CS2100”).put(new Assessment(“Test”, “B”)).put(new Assessment(“Lab1”, $.. ==&gt; Tony: {CS1231: {{Test: A-}}, CS2100: {{Test: B}, {Lab1: F}}}

<h1>Level 2</h1>

You will notice that the implementations of the Student and Module classes are very similar. Hence, by applying the <em>abstraction principle</em>, write a generic class KeyableMap to reduce the duplication.

<em>Hint:</em> KeyableMap&lt;V&gt; is a generic class that wraps around a String key (i.e. implements Keyable) and a

Map&lt;String,V&gt;. KeyableMap models an entity that contains an immutable map, but is also itself contained in another container (e.g. a student contains a map of modules but could be contained in a roster). The parameter type V is the type of the value of items stored in the immutable map; V must be a subtype of Keyable.

The class KeyableMap provides two core methods:

get(String key) which returns the item with the given key;

put(V item) which adds the key-value pair (item.getKey(),item) into the immutable map. The put method returns a KeyableMap. How do we restrict the classes bound to type V to be able to invoke the getKey method? The trick is to define the type parameter of Keyable as follows:

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”)$.. ==&gt; Optional[{Lab1: B}] jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).getGrade()|  Error:|  cannot find symbol|    symbol:   method getGrade()|  new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).getGrade()|  ^————————————————————————^ jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).map(x -&gt; x.getGrade()) $.. ==&gt; Optional[B]</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get(“CS204$.. ==&gt; Optional[{Lab1: B}] jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get(“CS204 $.. ==&gt; Optional[B]</td>

  </tr>

 </tbody>

</table>

<h1>Level 3</h1>

Notice that method chains below result in compilation errors:

jshell&gt; new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).getGrade()

|  Error:

|  cannot find symbol

|    symbol:   method getGrade()

|  new Module(“CS2040”).put(new Assessment(“Lab1”, “B”)).get(“Lab1”).getGrade()

|  ^————————————————————————^




jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get(“CS204

|  Error:

|  method get in class java.util.Optional&lt;T&gt; cannot be applied to given types;

|    required: no arguments

|    found: java.lang.String

|    reason: actual and formal argument lists differ in length

|  new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get(“CS2040” ).

|  ^———————————————————————————————

This is because the Optional class does not have a getGrade() or get(String) method defined (although it does define a get() method which, other than for debugging purposes, should typically be avoided). Rather than chaining in the usual way, we do it through a map or flatMap. Let’s start with map.

As expected, invoking getGrade() on an Optional results in a compilation error. However, we can perform a similar chaining effect by passing in the functionality of getGrade (either in the form of a lambda or method reference) to Optional’s map method. Notice the return value is actually wrapped in another Optional. When using map, you can think of the operation as “taking the value out of the Optional box, transforming it via the function passed to map, and wrap the transformed value back in another Optional”.

Now this is where things start to get interesting! Look at the following:

jshell&gt; new Student(“Tony”).put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))).get(“CS204 $.. ==&gt; Optional[Optional[{Lab1: B}]]

Observe that the return value is an Optional wrapped around another Optional that wraps around the desired value! Why is this so? The difference lies in the return type of Assessment::getGrade (read getGrade method of the Assessment class) and Module::get. The former returns a String, while the latter returns an Optional.

In x -&gt; x.getGrade() (or Assessment::getGrade), the transformed value is simply the grade, and this is wrapped in an Optional. However, passing x -&gt; x.get(“Lab1”) in the above code snippet results in a transformed value of Optional. And this transformed value is wrapped around another Optional via the map operation!

As such, we use the flatMap method instead. You may think of flatMap as flattening the Optionals into a single one.

Now you are ready to create a roster.

Define a Roster class that stores the students in an immutable map via the put method. A roster can have zero or more students, with each student having a unique id as its key. Once again, notice the similarities between Roster, Student and Module.

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; Student natasha = new Student(“Natasha”); natasha ==&gt; Natasha: {} jshell&gt; natasha = natasha.put(new Module(“CS2040”).put(new Assessment(“Lab1”, “B”))) natasha ==&gt; Natasha: {CS2040: {{Lab1: B}}} jshell&gt; natasha = natasha.put(new Module(“CS2030”).put(new Assessment(“PE”, “A+”)).put(new Assessnatasha ==&gt; Natasha: {CS2040: {{Lab1: B}}, CS2030: {{PE: A+}, {Lab2: C}}} jshell&gt; Student tony = new Student(“Tony”);tony ==&gt; Tony: {} jshell&gt; tony = tony.put(new Module(“CS1231”).put(new Assessment(“Test”, “A-“)))tony ==&gt; Tony: {CS1231: {{Test: A-}}} jshell&gt; tony = tony.put(new Module(“CS2100”).put(new Assessment(“Test”, “B”)).put(new Assessment(tony ==&gt; Tony: {CS1231: {{Test: A-}}, CS2100: {{Test: B}, {Lab1: F}}} jshell&gt; Roster roster = new Roster(“AY1920”).put(natasha).put(tony)roster ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: B}}, CS2030: { … : {{Test: B}, {Lab1: F}}}} jshell&gt; roster roster ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: B}}, CS2030: {{PE: A+}, {Lab2: C}}}, Tony: {CS1231: jshell&gt; roster.get(“Tony”).flatMap(x -&gt; x.get(“CS1231”)).flatMap(x -&gt; x.get(“Test”)).map(Assessme$.. ==&gt; Optional[A-] jshell&gt; roster.get(“Natasha”).flatMap(x -&gt; x.get(“CS2040”)).flatMap(x -&gt; x.get(“Lab1”)).map(Asses$.. ==&gt; Optional[B] jshell&gt; roster.get(“Tony”).flatMap(x -&gt; x.get(“CS1231”)).flatMap(x -&gt; x.get(“Exam”)).map(Assessme$.. ==&gt; Optional.empty jshell&gt; roster.get(“Steve”).flatMap(x -&gt; x.get(“CS1010”)).flatMap(x -&gt; x.get(“Lab1”)).map(Assessm$.. ==&gt; Optional.empty jshell&gt; roster.getGrade(“Tony”,”CS1231″,”Test”)$.. ==&gt; “A-” jshell&gt; roster.getGrade(“Natasha”,”CS2040″,”Lab1″)$.. ==&gt; “B” jshell&gt; roster.getGrade(“Tony”,”CS1231″,”Exam”);$.. ==&gt; “No such record: Tony CS1231 Exam” jshell&gt; roster.getGrade(“Steve”,”CS1010″,”Lab1″);$.. ==&gt; “No such record: Steve CS1010 Lab1” jshell&gt; new Roster(“AY1920”).put(new Student(“Tony”)) instanceof KeyableMap $.. ==&gt; true</td>

  </tr>

 </tbody>

</table>

<table width="606">

 <tbody>

  <tr>

   <td width="606">jshell&gt; Roster roster = new Roster(“AY1920”) roster ==&gt; AY1920: {} jshell&gt; roster = roster.add(“Natasha”, “CS2040”, “Lab1” , “B”)roster ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: B}}}} jshell&gt; roster.add(“Tony”, “CS1231”, “Test”, “A-“)$.. ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: B}}}, Tony: {CS1231: {{Test: A-}}}} jshell&gt; roster.add(“Natasha”, “CS1231”, “Test”, “A-“)$.. ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: B}}, CS1231: {{Test: A-}}}}</td>

  </tr>

 </tbody>

</table>

Define a method called getGrade in Roster to answer the query from the user. The method takes in three String parameters, corresponds to the student id, the module code, and the assessment title, and returns the corresponding grade.

In cases where there are no such student, or the student does not read the given module, or the module does not have the corresponding assessment, then output No such record followed by details of the query. Here, you might find Optional::orElse useful.

<h1>Level 4</h1>

Include the add method in the Roster class that takes in the student id, the module code, the assessment title and the grade, so as to update the roster as shown in the sample run below:




<table width="681">

 <tbody>

  <tr>

   <td rowspan="2" width="37"> </td>

   <td width="607"> jshell&gt; roster.add(“Natasha”, “CS2040”, “Test”, “A-“) $.. ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: B}, {Test: A-}}}} jshell&gt; roster.add(“Natasha”, “CS2040”, “Lab1”, “A-“)$.. ==&gt; AY1920: {Natasha: {CS2040: {{Lab1: A-}}}} jshell&gt; roster.getGrade(“Natasha”, “CS2040”, “Lab1”)$.. ==&gt; “B” jshell&gt; roster.getGrade(“Natasha”, “CS2040”, “Test”)$.. ==&gt; “No such record: Natasha CS2040 Test” jshell&gt; roster.getGrade(“Natasha”, “CS1231”, “Lab1”)$.. ==&gt; “No such record: Natasha CS1231 Lab1” jshell&gt; roster.getGrade(“Tony”, “CS2040”, “Lab1”)$.. ==&gt; “No such record: Tony CS2040 Lab1”</td>

   <td rowspan="2" width="37"> </td>

  </tr>

  <tr>

   <td width="607"><strong>Level 5</strong>Now use the classes that you have built and write a Main class to deal with program input and output.Firstly, read the following from the standard input:The first token read is an integer N, indicating the number of records to be read.The subsequent inputs consist of N records, each record consists of four words, separated by one or more spaces. The four words correspond to the student id, the module code, the assessment title, and the grade, respectively.The subsequent inputs consist of zero or more queries. Each query consists of three words, separated by one or more spaces. The three words correspond to the student id, the module code, and the assessment title.For each query, if a match in the input is found, print the corresponding grade to the standard output. Otherwise, print “No such record:” followed by the three words given in the query, separated by exactly one space.See sample input and output below. User input is <u>underlined</u>. Input is terminated with a ^D (CTRL-d).

    <table width="606">

     <tbody>

      <tr>

       <td width="606">$ java Main<u>12</u><u>Jack   CS2040 Lab4    B</u><u>Jack   CS2040 Lab6    C</u><u>Jane   CS1010 Lab1    A</u><u>Jane   CS2030 Lab1    A+</u><u>Janice CS2040 Lab1    A+</u><u>Janice CS2040 Lab4    A+</u><u>Jim    CS1010 Lab9    A+</u><u>Jim    CS2010 Lab1    C</u><u>Jim    CS2010 Lab2    B</u><u>Jim    CS2010 Lab8    A+</u><u>Joel   CS2030 Lab3    C</u><u>Joel   CS2030 Midterm A</u><u>Jack   CS2040 Lab4</u><u>Jack   CS2040 Lab6</u><u>Janice CS2040 Lab1</u><u>Janice CS2040 Lab4</u><u>Joel   CS2030 Midterm</u><u>Jason  CS1010 Lab1</u><u>Jack   CS2040 Lab5</u><u>Joel   CS2040 Lab3</u><u>^D</u>BCA+A+ANo such record: Jason CS1010 Lab1No such record: Jack CS2040 Lab5No such record: Joel CS2040 Lab3</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

  <tr>

   <td colspan="3" width="681"></td>

  </tr>

 </tbody>

</table>


