# HW4 — Short Answers

Answer each question in 2–3 sentences.

## 1. Rolling-update safety
Why does the Deployment use `maxUnavailable: 0`, and what would change if it were `maxUnavailable: 1`?

> Setting 'maxUnavailable' to zero ensures that old (i.e., unavailable or down) pods are deleted/killed only once a new pod is created to take its place. If 'maxUnavailable' was instead set to one, then one pod would be allowed to be down during a rolling update and this would result in some requests being dropped.  

## 2. Health probes
Why do the liveness/readiness probes target `/health` instead of `/predict`?

> The liveness and readiness probes target '/health' because this will output whether pods are ready to accept traffic rather than confirming predictions can be outputted and the container is running (as with targeting '/predict'). If '/predict' was targeted instead, it would signal that the pods are incorrectly ready for traffic based upon the confirmed running process. Additionally, using '/health' means the pods are confirmed ready before Redis is up and customer features are read.

## 3. Autoscaling under load
Your HPA scales at 40% CPU up to 8 pods. If request volume doubled, what would you expect to happen — and what happens once it reaches the maximum?

> If the request volume doubled and the load pushed CPU past its 40% target, I would anticipate that the HPA would scale from 3 up to 8 pods to balance the request volume better. Once the HPA has scaled to the maximum limits, there would not be an increase in CPU available or additional pods created, so additional large request volume would result in a lag where the container is paused until more CPU is available (increased latency).
