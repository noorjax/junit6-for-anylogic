**junit6-for-anylogic**

A lightweight library that enables JUnit 6 unit testing inside AnyLogic.
Created and maintained by Noorjax Consulting — https://www.noorjax.com

This library is completely free to use.

✅ How to Use It in an Existing AnyLogic Model
1. Add the JAR

Download the JAR and add it to your model dependencies.

2. Create a Custom Experiment

Create a custom experiment.
Name it for example: Tester.

3. Create Another Custom Experiment

Create a second custom experiment.
Name it for example: RunAllTests.

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
AnyLogicJUnitLauncher.doTest(CalculatorTest.class);
```

This will execute all tests inside CalculatorTest.

Note:
Technically you can call doTest anywhere, but placing it inside the RunAllTests experiment is the recommended approach.

The launcher and all required JUnit 6 dependencies are bundled inside this library, so you don't need to configure Maven or deal with test engines manually.

🧪 Running Tests That Require a Simulation

If your tests involve agents or classes that do not require running a simulation, you can simply test them directly — nothing special is needed.

If your tests require a simulation to be executed, use @BeforeEach to initialize the engine and environment.
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

We provide examples in the repository, and more tutorials will be added soon.

📟 Test Output in the AnyLogic Console

Thanks to the launcher, test results always appear cleanly formatted inside the AnyLogic console.
Example:

✘ Some tests failed (1/3) for CalculatorTest
----
Test: add 2 numbers  ❌
  Message : expected: <20.0> but was: <30.0>

✔ All tests passed (1/1) for FactorialTest
✔ All tests passed (4/4) for StudentServiceTest
