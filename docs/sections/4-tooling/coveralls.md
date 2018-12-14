# Coveralls

[Coveralls](https://coveralls.io/) is a web service to help you track your code coverage over time, and ensure that all your new code is fully covered.

# Setup

1. Creating an account is fast and easy, just authorize Coveralls to access your repos - no forms to fill out.

    - Click the [Sign in](https://coveralls.io/sign-in) button for your git service
    - Click the `Add some repos` button to add your repos
    - Click on the repos you added and copy the `repo_token` values.

2. Login to [Travis CI](https://travis-ci.com) dashboard and go to the settings of the repos you added Coveralls to.

    - Login to the [Travis CI](https://travis-ci.com) dashboard
    - Click on the repo you want to add the environment settings to
    - From `More options` (right hand side under your avatar) select `settings`
    - Add an environment variable with the `COVERALLS_REPO_TOKEN` use the value you copied in the previous step.

3. Add an entry to the `scripts` section of the `package.json` file.

   ```json
   {
     "scripts": {
       "coveralls": "npm run coverage && cat ./coverage/lcov.info | coveralls && rm -rf ./coverage",
     }
   }
   ```

4. To test locally set the environmental variable `COVERALLS_REPO_TOKEN`.

   Windows

   ```bash
   set COVERALLS_REPO_TOKEN=<the-value-you-copied-in-step-1>
   ```

   Linux

   ```bash
   export COVERALLS_REPO_TOKEN=<the-value-you-copied-in-step-1>
   ```
