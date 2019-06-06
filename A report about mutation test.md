## A report about the mutation test

---

这是学校CS306 软件工程 的一个作业。
This is an assignment of CS306 Software Engineering in Sustech.

---

[TOC]

---

### Requirement

> Write a short essay to analyze Mutation Testing, at least 800 words.
Choose two or more from these keywords:
current state, pros, cons, how to improve, compared to other technique

### Why we need Mutation Test?

Before we talk about the Mutation Test, it would be helpful to introduce the ordinary test methods.

Normal test coverage can be divided into four parts:

- Function Coverage
- Statement Coverage
- Decision Coverage
- Condition Coverage
  
And they are easily implemented in most of the test tools like JUnit.

However, it is weak in full-bug free tests and will miss some more complex or deep-level bugs.

Some code or the problems will not find even in the status of 100% Coverage.

That’s the reason for the idea of Mutation Test.

### What is Mutation Test?

Just like the overview in the [official site](http://pitest.org/), it is a useful tool to change the code behaviors under the method of editing the code in one position, obviously, make sure the syntax is correct.

### How does it work?

The explanation of the work motivation in PItest website is complex and hard to understanding :(

It just gives the connection between the final results and the mutated codes:
> When the application code changes, it should produce different results and cause the unit tests to fail.
>
> If a unit test does not fail in this situation, it may indicate an issue with the test suite.
The goal of Mutation Test just like TDD(Test-driven development). Both of them speak highly of XP(Extreme programming).

Therefore, the motivation will be easy understanding:

Base on XP, the code doesn’t exist the redundant part, so that almost all the editing(mutation) on the code will change the conduction in results or outputs, and will lead the failure in testing.

That means if the mutation doesn’t cause the failure, whether it exists the redundancy or the existing test cases cannot find this mutation.

In summary, it just:
**Good tests shall fail.**

### Pros

1. It is more flexible and introduces many methods and operators (call mutators) to realize the deep-level bug finding.
2. base on a new idea, it can repeat boundary and special bugs.
3. It can also find redundant code in programs.
4. It is more automatic since it can testing in different aspects base on a finite number of test cases.
5. More powerful in data-flow programs.

### Cons

1. Just like most of the test tools, it is a waste of time to use.
2. The original test cases need to generate by hand.
3. Not such intelligence. From the example of the Triangle, it finds some impossible
condition. Just like

```Java
// <- mutation may change it to "99<=100"
// even though it is useless but it actually survives
if (99<100){
doSomeThing();
}
```

4. Also, it will mislead some thoughts. In the example of the Triangle, the bug locates in line 4, while it only detects the errors in the next few lines.

    Test engineers may spend much useless time in the fault localization in the detected position and ignore the actual bugs.

### Improvement

Now it comes to the modification. Since mutation test is so useful, the question we fact is how to eliminate the influence of disadvantages.

1. Just import and take the test to the necessary program codes.

    Mutation test will test all possible positions of the codes. We can just abstract the lines of codes that we need, which may reduce the time taking in the testing part.

2. Improve the quality of the test cases.

    As we all know, one of the goals for mutation test is to measure the performance of the test cases.

    However, on the other hand, the better quality of test cases can also have a positive effect on the mutation test.

    Just like positive feedback.

### Comparison

| \ | coverage-based test | mutation test |
| :------: | :------: | :------: |
| action object | test cases | program code |
| judgment standard | passing rate | survival rate |
| time-required | high | moderate |
| redundancy detection | No | Yes |
| fault localization | accurate | moderate |
