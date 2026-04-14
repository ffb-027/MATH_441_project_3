# Main feedback

- Objective function/risk term/sample data
  - double check whether $q_i$ should be inside the squared term or outside:
    - current form: $q_i (y_i T_i)^2$
    - alternative: $(q_i y_i T_i)^2$
  - clarify what this term represents:
    - more of a regularization / penalty term than a direct profit term
  - current use of delay probability as a fixed value may be too simple
    - real risk should reflect uncertainty / variance in delay probability
    - e.g. not just $q_i = 0.22$, but something like $0.22 \pm \text{uncertainty}$

- Data / realism (less important)
  - cite the real data source more clearly
  - maybe consider using a common representative route across all airlines (e.g. YVR-LAX)
    - would make average fares more comparable
  - revisit the sample values for:
    - premium sensitivity
    - compensation sensitivity
  - current sensitivity parameters may look too arbitrary unless justified better

- Model perspective
  - decide clearly whose perspective the model is from:
    - insurance company
    - or consumer
  - right now it seems mostly from the insurance company perspective
  - if so, some constraints/objective interpretations should be revised accordingly

- Constraint 4 (consistency) - **VERY important**
  - current logic is weak if model is from insurer perspective
  - why require:
    - $x_i \le y_i$?
  - as an insurance company, compensation does not need to exceed premium on each airline
  - it may be reasonable to allow:
    - compensation $<$ premium
    - especially if that supports higher premiums or better allocation elsewhere
  - rethink whether this is a consumer-attractiveness assumption rather than an insurer-side necessity

- Constraint 1 (budget/expense cap) - **VERY important**
  - reconsider hard cap:
    - $\sum q_i y_i T_i \le B$
  - if the solution does not come close to using all of $B$, is this constraint actually active?
  - if it is never binding, it may not matter much
  - ask whether a hard expense cap is the right insurer-side modeling choice

- Constraint interaction - **VERY important**
  - there may not be much interaction among the hard cap constraints
  - do not spend too much emphasis on constraints 2 and 3 unless they are actually active
  - **check whether removing or loosening them changes results meaningfully!!!!**
    - if not, then they are not driving the solution much
  - focus more on the constraints/terms that actually shape the optimization outcome

  ## Results comments

- **Figure 1 vs Figure 3**
  - expected payouts (green bars) behave differently across the two figures
  - in Figure 1:
    - payouts are fairly similar across airlines
    - relatively little variation
  - in Figure 3:
    - payouts vary much more across airlines
  - worth explaining this mathematically:
    - smaller $\lambda$ allows larger compensations
    - larger compensations create more variation in expected payouts
    - larger $\lambda$ penalizes large compensation choices more strongly
  - connect this back to the risk/regularization term in the objective


  ## Overall todo

- choose one consistent viewpoint:
  - insurer-side model seems most natural
- then revise:
  - objective interpretation
  - Constraint 1
  - Constraint 4
- test which constraints are actually binding
- improve realism of:
  - fare data
  - delay-risk modeling
  - sensitivity parameters