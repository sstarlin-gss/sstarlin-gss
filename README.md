Hey there,

I'm Steven Starlin and I've been with GSS since August 2023. I've been a software engineer for over a decade and I've worked for small startup companies and mid-to-large sized companies alike, learning, coaching, architecting, and developing systems. These projects have been modernizing legacy systems, designing and building greenfield systems, and building application integrations (like website commerce to Quickbooks). I'm always happy to help, coach, learn, and chat, so feel free to hit me up if you need anything!

One big area I'm passionate about (other than Feature Flag systems) is Specification Testing, which I've outlined below. It's helped me become a more robust and confident developer while supporting the systems I work in through self-documenting code, sustainable test suites, and closed feedback loops in rapid response conditions so I know when I need to change my methodologies.

## Specification Testing

### Premise

Specification Testing (or spec testing, for short) defines a large-scale, end-to-end test using real objects as often as possible. This allows us to get a snapshot of functionality of our internal systems as they consume external resources and transform them into usable objects and data internally.

### Methodology

#### Reading Spec Tested Code

To best understand the spec testing method, read through the code structure like this:

1. Locate a specification test file in the test project
    1. This will show the required setup for objects and systems, as well as their primary functions in a happy-path scenario.
2. Locate the object unit tests in the project (usually under a UnitTests folder)
    2. This file will show the granular interaction tests using mock objects for external interests (e.g. Flags from a vendor vs. the flag service we define internally) as well as the non-happy-path tests that prove the robustness of our code.
3. Locate the real object definitions used by the unit tests and spec test(s) to see how the code is actually used in the environment(s).

#### Writing Spec Tested Code

Spec test-driven development gives us a higher test coverage to code implementation ratio, and forces us to _only_ write code we _need_. This is done through the following methodology:

1. Create a spec test following the Arrange/Act/Assert framework
    1. Arrange the object(s) necessary to perform an action.
    2. Act upon it/them using their own methods.
    3. Assert truths about the functionality of the system.
    4. This assertion will fail until the full process is followed.
    5. **Note:** Initial spec tests will seem very similar to their related unit tests, but unit tests should mock all external needs.
    6. **Note:** Keep each Arrange/Act/Assert clause simple. The simpler the better.
2. Create a unit test that accomplishes the "happy path" of the spec test.
    1. More unit tests will be added throughout the process as the spec test matures
    2. The unit test will fail in the same way the spec test does.
3. Write the code that passes the unit test
    1. This should ultimately "pass" the spec test as well.
4. Add code that breaks the spec test to mature the feature.
5. Start over at step [1](#writing-spec-tested-code).

##### Rules of writing spec tested code

1. Only one spec test and one unit test may fail at a time.
2. The spec test should always be broken first by adding new code to it.
3. Once the spec is broken, add a unit test that matches the intent behind the new spec breakage.
4. Once the unit test is added, the code should satisfy the unit test _as simply as possible_
    1. This means that the actual code implementation will be pretty "dumb" until the feature is matured more.
        - A method signature like this: ```private int FindThing(#test)``` may have a return clause like this: ```return 0;```
        - This is acceptable because we need to write a spec and unit test structure that forces the validation and proper handling of the values inside our feature.
