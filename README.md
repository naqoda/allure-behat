##What it is

This is a Behat extension with Formatter that produces report data for [Yandex Allure](http://allure.qatools.ru/) test
reporting tool.

### Installation

To install using composer, add `"allure-framework/allure-behat"` to `composer.json`:

    ...
    "require": {
    ...
        "allure-framework/allure-behat": "1.0.0",
    ...
    },
    "repositories": [
    ...
        {
            "type": "vcs",
            "url": "git@github.com:eduard-sukharev/behat-allure-adapter.git"
        }
    ...
    ]
    ...

### 1.0 Milestones:

 - [x] Fix `Without Behavior` and `Without story` report issue
 - [x] Add proper extension parametrization
 - [x] Test with background
 - [x] Test with scenario outlines
 - [x] Test on existing project

### How does it work?

As you may already know, Behat has following test structure: It has Features described in separate feature files.
Each Feature comprise of Scenarios. Each scenario is composed from Steps. Allure reports have a bit different hierarchy.
Each report combines Test Suites, which consist of Test Cases fromed by Test Steps.
On the other hand, Allure also supports grouping Test Cases by Feature, by Story or by Severity level.

Behat Allure formatter does the following mapping:

 - Each Behat test run is considered as Test Suite.
 - Each Behat Scenario (and every single Example in Scenario Outline, too) is considered a Test Case
 - Each Behat Sentence is considered a Test Step
 - Behat Scenarios are annotated with it's feature title and description to be grouped into Allure Feature.

Behat also has tags and they are also can be used in Allure reports:

 - If a tag appears in ignored_tags configuration parameter, then it will be ignored and will not appear on Allure report
 - If a tag starts with severity_tag_prefix, then formatter will try to interpret it's affixed part as Allure Severity annotation
 - In all other cases tag will be parsed as Allure Story annotation

By default, this formatter will use `build/allure-results` folder to put it's output XML to. Each Behat run will empty
that folder. To override this behavior, define `output` and `delete_previous_results` parameters respectively.

### Feedback

This formatter is needs your input. Open issues on Github and propose your changes. Pull requests are welcome.
