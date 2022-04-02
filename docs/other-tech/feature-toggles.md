## Benefits
2. Roll out or rollback in seconds
1. decouple deploy and rollout of features
    2. decouple them to isolate the issues (deploy vs feature issue)
3. Beta Test in production
    4. Only test on 10% of users
5. Always be able to merge code (even if incomplete) into the main branch
    6. fewer merge issues

Why Feature Toggles?

https://youtu.be/Fj3TvaovPe0


What is a feature flag?

https://youtu.be/-n0weDGWTy8


## Why use LaunchDarkly instead of building your own
- funfun functions
    - there are lot of edge cases
- 

## Using Launch Darkly
1. have feature flags on the backend
2. have the frontend make an API call to get the feature flag list
    3. store it in redux or a global store


### How to test feature flags
How to have tests with feature flags?
* Providers???