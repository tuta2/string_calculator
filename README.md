## rspec-intro
# How to get started:
```
  bundle install
  bundle exec rspec
```
* BBD (behavior driven development);

# TDD is Test Driven Development. 
*This means writing a test that fails because the specified functionality doesn't exist, then writing the simplest code that can make the test pass, then refactoring to remove duplication, etc. You repeat this Red-Green-Refactor loop over and over until you have a complete feature.

# BDD is Behavior Driven Development. 
*This means creating an executable specification that fails because the feature doesn't exist, then writing the simplest code that can make the spec pass. You repeat this until a release candidate is ready to ship.
Those seem pretty similar, right? They are. The key difference is the scope. TDD is a development practice while BDD is a team methodology. In TDD, the developers write the tests while in BDD the automated specifications are created by users or testers (with developers wiring them to the code under test.)