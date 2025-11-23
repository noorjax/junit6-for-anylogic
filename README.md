# junit6-for-anylogic
Library meant to use JUNIT6 to do your unit tests in AnyLogic

How to use it in an AnyLogic model you already created:
1) add the .jar to your model dependencies.  
2) Create a custom experiment. Let's call it Tester  
3) Create another custom experiment, let call it RunAllTests  
4) Create a JAVA class where your tests will live. YOu can create as many of these classes as you want. Let's call this class MainTest  

Configure RunAllTests  
5) you need to import the library in the imports section: import jUnit6ForAnyLogic.AnyLogicJUnitLauncher;  
6) you can run the tests in the code section, for example: AnyLogicJUnitLauncher.doTest(CalculatorTest.class);  
will run all the tests present in the class CalculatorTest 
Note: you can really run the doTest method anywhere, but running it in here seems to be the best option  

If you are testing classes or agents, sometimes you don't need to even run a simulation, in those cases, you don't need to do anything  

If you are testing agents that do need to run the simulation, you can do it using the @BeforeEach annotation... in general it will look something like this:  

@BeforeEach  
	void setup() {    
		engine=new Tester(null).createEngine();  
		engine.getDefaultRandomGenerator().setSeed(1);  
		engine.setTimeUnit( SECOND );  
		engine.setStartTime( 0.0 );  
		engine.setStopTime(1,HOUR);  
		root = new Main( engine, null, null );	  
		engine.start( root );   
    //other initalization here  
	}  

You can check the examples we have available, we will add more plus tutorials.  



Thanks to our launcher library, you will se the tests results always nicely in the AnyLogic console, for example:  

**✘ Some tests failed (1/3) for CalculatorTest  
----  
Test: add 2 numbers  ❌  
  Message : expected: <20.0> but was: <30.0>  
✔ All tests passed (1/1) for FactorialTest  
✔ All tests passed (4/4) for StudentServiceTest  
