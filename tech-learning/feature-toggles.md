decouple deploy and rollout of features

1. isolate risk
    2. deploy and rollout of features are risky
    3. we want to decouple them to isolate the issue
3. Always be able to merge code into the main branch

2. Roll out or rollback in seconds
    3. no need to redeploy
3. Beta Test in production
    4. Only test on 10% of users

Why Feature Toggles?

https://youtu.be/Fj3TvaovPe0


What is a feature flag?

https://youtu.be/-n0weDGWTy8


Why use LaunchDarkly instead of building your own
- funfun functions
    - there are lot of edge cases
- 


One way to use feature toggles
1. have feature flags on the backend
2. have the frontend make an API call to get the feature flag list
    3. store it in redux or a global store
    4. 