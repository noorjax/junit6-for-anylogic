**junit6-for-anylogic**

A lightweight library that enables JUnit 6 unit testing inside AnyLogic.
Created and maintained by Noorjax Consulting — https://www.noorjax.com

**This library is completely free to use.**  

You can find a tutorial on how to set this up here:  
https://www.youtube.com/watch?v=zW4u-yII2p4  
And another tutorial for assertions and annotations here:  
https://www.youtube.com/watch?v=cPIHCar9h0o&t=9s  
Finally, the video explaining how to structure your models in AnyLogic:   
https://www.youtube.com/watch?v=4Q3104fniJU  

✅ How to Use It in an Existing AnyLogic Model
1. Download the JAR and add it to your model dependencies.

2. Create a custom experiment.
Name it for example: Tester.
Delete all the auto-generated code that comes with it

3. Create Another Custom Experiment

Name it for example: RunAllTests.
Delete all the auto-generated code that comes with it

4. Create Your Test Classes

Create a Java class where your tests will live.
You can create as many test classes as you want.
Example name: MainTest.

⚙️ Configure the RunAllTests Experiment

In the imports section, add:
```
import jUnit6ForAnyLogic.AnyLogicJUnitLauncher;
```

In the code section, run your tests like:
```
AnyLogicJUnitLauncher.doTest(MainTest.class);
```

This will execute all tests inside MainTest.
You can also do AnyLogicJUnitLauncher.doTest(MainTest.class,parallelRuns);  
where parallelRuns is an integer to allow you to decide how many parallel runs are allowed, but you will need to use the @Execution(ExecutionMode.CONCURRENT) annotation along with this.  
The default number of parallel runs is 4.

Note:
Technically you can call doTest anywhere, but placing it inside the RunAllTests experiment is the recommended approach.

The launcher and all required JUnit 6 dependencies are bundled inside this library, so you don't need to configure Maven or deal with test engines manually.

🧪 Running Tests That Require a Simulation

If your tests involve agents or classes that do not require running a simulation, you can simply test them directly — nothing special is needed.

If your tests require a simulation to be executed, use @BeforeEach to initialize the engine and environment (a tutorial on this soon)
A typical setup looks like this:
```
@BeforeEach
void setup() {
    engine = new Tester(null).createEngine();
    engine.getDefaultRandomGenerator().setSeed(1);
    engine.setTimeUnit(SECOND);
    engine.setStartTime(0.0);
    engine.setStopTime(1, HOUR);

    root = new Main(engine, null, null);
    engine.start(root);

    // other initialization here
}
```

We provide examples in the repository and instructions in the videos previously posted.

📟 Test Output in the AnyLogic Console

Thanks to the launcher, test results always appear cleanly formatted inside the AnyLogic console.
Example:

✘ Some tests failed (1/3) for CalculatorTest
----
Test: add 2 numbers  ❌
  Message : expected: <20.0> but was: <30.0>

✔ All tests passed (1/1) for FactorialTest  
✔ All tests passed (4/4) for StudentServiceTest
