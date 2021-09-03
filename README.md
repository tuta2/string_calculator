## rspec-intro
# How to get started:
```
  bundle install
  bundle exec rspec
```
# TDD is Test Driven Development. 
*This means writing a test that fails because the specified functionality doesn't exist, then writing the simplest code that can make the test pass, then refactoring to remove duplication, etc. You repeat this Red-Green-Refactor loop over and over until you have a complete feature.

# BDD is Behavior Driven Development. 
*This means creating an executable specification that fails because the feature doesn't exist, then writing the simplest code that can make the spec pass. You repeat this until a release candidate is ready to ship.
Those seem pretty similar, right? They are. The key difference is the scope. TDD is a development practice while BDD is a team methodology. In TDD, the developers write the tests while in BDD the automated specifications are created by users or testers (with developers wiring them to the code under test.)

### Rspec
It is a DSL language(Domain Specific Language).
* - describe ClassName (must start wit a capital letter)
  - end
* Followed by subsequent describe methods.
 - describe ".add" do
 - end
 * We are using another describe block to describe the add class method. By convention, class methods are prefixed with a dot (".add"), and instance methods with a dash ("#add").

* We are using another describe block to describe the add class method. By convention, class methods are prefixed with a dot (".add"), and instance methods with a dash ("#add").
 * We are using a context block to describe the context under which the add method is expected to return zero. context is technically the same as describe, but is used in different places, to aid reading of the code.
 * We are using an it block to describe a specific example, which is RSpec’s way to say “test case”. Generally, every example should be descriptive, and together with the context should form an understandable sentence. This one reads as “add class method: given an empty string, it returns zero“.
 * expect(...).to and the negative variant expect(...).not_to are used to define expected outcomes. The Ruby expression they are given (in our case, StringCalculator.add("")) is combined with a matcher to fully define an expectation on a piece of code. The matcher we are using here is eq, a basic equality matcher.

 ```
  expect(result).to   eq(3)
  expect(list).not_to be_empty
  pi.should be > 3
```
### Object identity
```
  expect(actual).to be(expected) # passes if actual.equal?(expected)
```
### Object equivalence
```
  expect(actual).to eq(expected) # passes if actual == expected
```
### Optional APIs for identity/equivalence
```
  expect(actual).to eql(expected)   # passes if actual.eql?(expected)
  expect(actual).to equal(expected) # passes if actual.equal?(expected)
  # NOTE: `expect` does not support `==` matcher.
```
### Comparisons
```
  expect(actual).to be >  expected
  expect(actual).to be >= expected
  expect(actual).to be <= expected
  expect(actual).to be <  expected
  expect(actual).to be_between(minimum, maximum).inclusive
  expect(actual).to be_between(minimum, maximum).exclusive
  expect(actual).to match(/expression/)
  expect(actual).to be_within(delta).of(expected)
  expect(actual).to start_with expected
  expect(actual).to end_with expected
  # NOTE: `expect` does not support `=~` matcher.
```
### Types/classes/response
```
  expect(actual).to be_instance_of(expected)
  expect(actual).to be_kind_of(expected)
  expect(actual).to respond_to(expected)
```
### Truthiness and existentialism
```
  expect(actual).to be_truthy    # passes if actual is truthy (not nil or false)
  expect(actual).to be true      # passes if actual == true
  expect(actual).to be_falsey    # passes if actual is falsy (nil or false)
  expect(actual).to be false     # passes if actual == false
  expect(actual).to be_nil       # passes if actual is nil
  expect(actual).to exist        # passes if actual.exist? and/or actual.exists? are truthy
  expect(actual).to exist(*args) # passes if actual.exist?(*args) and/or actual.exists?(*args) are truthy
```
### Expecting errors
```
  expect { ... }.to raise_error
  expect { ... }.to raise_error(ErrorClass)
  expect { ... }.to raise_error("message")
  expect { ... }.to raise_error(ErrorClass, "message")
```
### Expecting throws
```
  expect { ... }.to throw_symbol
  expect { ... }.to throw_symbol(:symbol)
  expect { ... }.to throw_symbol(:symbol, 'value')
```
### Predicate matchers
```
  expect(actual).to be_xxx         # passes if actual.xxx?
  expect(actual).to have_xxx(:arg) # passes if actual.has_xxx?(:arg)
```
### Examples
```
  expect([]).to      be_empty
  expect(:a => 1).to have_key(:a)
```
### Collection membership
```
  expect(actual).to include(expected)
  expect(array).to match_array(expected_array)
  # ...which is the same as:
  expect(array).to contain_exactly(individual, elements)
```
### Examples
```
  expect([1, 2, 3]).to     include(1)
  expect([1, 2, 3]).to     include(1, 2)
  expect(:a => 'b').to     include(:a => 'b')
  expect("this string").to include("is str")
  expect([1, 2, 3]).to     contain_exactly(2, 1, 3)
  expect([1, 2, 3]).to     match_array([3, 2, 1])
```
### Ranges (1.9+ only)
```
  expect(1..10).to cover(3)
```
### Change observation
```
  expect { object.action }.to change(object, :value).from(old).to(new)
  expect { object.action }.to change(object, :value).by(delta)
  expect { object.action }.to change(object, :value).by_at_least(minimum_delta)
  expect { object.action }.to change(object, :value).by_at_most(maximum_delta)
```
### Examples
```
  expect { a += 1 }.to change { a }.by(1)
  expect { a += 3 }.to change { a }.from(2)
  expect { a += 3 }.to change { a }.by_at_least(2)
```
### Satisfy
```
  expect(actual).to satisfy { |value| value == expected }
```
### Output capture
```
  expect { actual }.to output("some output").to_stdout
  expect { actual }.to output("some error").to_stderr
```
### Block expectation
```
  expect { |b| object.action(&b) }.to yield_control
  expect { |b| object.action(&b) }.to yield_with_no_args           # only matches no args
  expect { |b| object.action(&b) }.to yield_with_args              # matches any args
  expect { |b| object.action(&b) }.to yield_successive_args(*args) # matches args against multiple yields
```
### Examples
```
  expect { |b| User.transaction(&b) }.to yield_control
  expect { |b| User.transaction(&b) }.to yield_with_no_args
  expect { |b| 5.tap(&b)            }.not_to yield_with_no_args         # because it yields with `5`
  expect { |b| 5.tap(&b)            }.to yield_with_args(5)             # because 5 == 5
  expect { |b| 5.tap(&b)            }.to yield_with_args(Integer)       # because Integer === 5
  expect { |b| [1, 2, 3].each(&b)   }.to yield_successive_args(1, 2, 3)
```
