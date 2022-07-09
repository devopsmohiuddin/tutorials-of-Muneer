- do not deploy application load balancer controller
- do not deploy openid connect provider








aws elbv2 describe-listeners \
--load-balancer-arn arn:aws:elasticloadbalancing:us-east-1:424432388155:loadbalancer/net/a852b4f6ff0be41dfa1505018b083488/e8cf16c1a71e2a37

$(aws elbv2 describe-load-balancers \
--region $AGW_AWS_REGION \
--query "LoadBalancers[?contains(DNSName, '$(kubectl get service authorservice \
-o jsonpath="{.status.loadBalancer.ingress[].hostname}")')].LoadBalancerArn" \
--output text) \
--region $AGW_AWS_REGION \
--query "Listeners[0].ListenerArn" \
--output text




aws elbv2 describe-listeners \
--load-balancer-arn $(aws elbv2 describe-load-balancers \
--region us-east-1 \
--query "LoadBalancers[?contains(DNSName, '$(kubectl get service authorservice \
-o jsonpath="{.status.loadBalancer.ingress[].hostname}")')].LoadBalancerArn" \
--output text) \
--region us-east-1 \
--query "Listeners[0].ListenerArn" \
--output text






curl https://h6a9iroazf.execute-api.us-east-1.amazonaws.com/dev/echo