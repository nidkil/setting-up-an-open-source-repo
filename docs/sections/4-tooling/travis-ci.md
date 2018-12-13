# Travis CI

Continuous Integration is the practice of merging in small code changes frequently - rather than merging in a large change at the end of a development cycle. The goal is to build healthier software by developing and testing in smaller increments. This is where [Travis CI](https://travis-ci.com) comes in.

As a continuous integration platform, Travis CI supports your development process by automatically building and testing code changes, providing immediate feedback on the success of the change. Travis CI can also automate other parts of your development process by managing deployments and notifications.

Read more about CI concepts [here](https://docs.travis-ci.com/user/for-beginners/).

1. Setup Travis CI

    Go to the [Travis CI website](https://travis-ci.com) and setup the integration with your GitHub repository.

2. Create a `.travis.yml` configuration file in the root directory of the project and add the following contents.

    ```yml
    language: node_js
    node_js:
      - "v8.12.0"
      - "node"
    sudo: false
    cache:
      - "node_modules"
    script:
      - npm test
    after_script:
      - npm run coveralls
    ```
