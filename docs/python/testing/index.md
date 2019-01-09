#Python testing

In general we use [pytest](http://docs.pytest.org/en/latest/) for testing Python code. You might ask why! Well, this is why: [testandcode]

## Motivation

Reasons to test code are plentiful; performance, quality, usability, security, and stability. However, the focus will be on testing to ensure _expected behavior_.

The main idea is that your suite of tests should insprire confidence that the code performs as expected. Any additional updates should pass all tests before being considered in the main branch. This way, developer who contribtute to the project don’t fear breaking something 🐞.

One more thing: when you write tests for your code, you write code which is easy to test. The result is functional, maintainable, and composable!

## The habit loop

A habit is formed when you no longer need to motivate yourself to perform a routine. You do it automatically. Following a cue, acting out your routine, and claiming your reward.

It’s only natural to feel like tests are but an additional step that you would rather skip and just deploy! But without tests you will never feel confident about the execution of your code. Just like working out, writing tests is a perfect activity to design a habit around.

This is my own habit loop for testing: my cue is writing or altering a function. The routine is writing tests for it. My reward is better/complete [test coverage]. I now crave to maintain a green badge of 100% coverage and peace of mind that executing my code does what I expect.

It’s important to make this loop as simple as possible. That’s why you should invest time in learning and setting up test automation.

> Read more about habits and how to master them in [The Power of Habit], by Charles Duhigg.

## Strategy: GIVEN-WHEN-THEN

It can be difficult to get started writing tests. Where do I begin? My routine is to follow step-by-step instructions in a very simple model: GIVEN-WHEN-THEN.

    GIVEN: describe the prerequisets for the test you will run and optionally make assertions about your setup
    WHEN: run your function and explain what is supposed to happen
    THEN: assert the outcome of your test; return values or side effects

Here’s a quick example:

```
# GIVEN the database doesn't contain any rows
assert DatabaseRow.query.count() == 0
# WHEN adding a new row to the database
new_name = 'Paul'
add_row(name=new_name, age=12)
# THEN there should be ONE new row added to the database
assert DatabaseRow.query.count() == 1
# ... with the expected name
assert DatabaseRow.query.first().name == new_name
```

By being explicit about what you're testing, you can get past the initial mental obstacles. It also adds relevancy to writing tests. Without clear comments it can often feel like indecipherable lines that does something you’ve long forgot.

This tutorial was originally written by our favorite alumni: [Robin Andeer]!

[testandcode]: https://testandcode.com/
[pytest]: http://docs.pytest.org/en/latest/
[test coverage]: https://en.wikipedia.org/wiki/Code_coverage
[The Power of Habit]: http://charlesduhigg.com/the-power-of-habit/
[Robin Andeer]: https://www.robinandeer.com/blog/2016/06/18/how-i-test-my-code-part-1/
