ECOMMERCE CLOUD MICROCROSERVICES ARCHITECTURE DESIGN

![Alt text](image.png)


When the user successfully verifies the OTP challenges, the user´s detail is stored in a dynamoDB table then, the user is added to the Cognito user pool.

AWS Amplify managed service handles the tokens life-extentions in the background which is one less thing to have to code or worry about.

Using an AWS S3-bucket for the web-app is very cheap. while cloudfront handles all incoming user traffic.

Using a WAF also allows us to control all incoming requests from users into the system.

Activating Cloudfront chaching allows the app to be served from the chache on subsequest requests rather that having to go through all the steps all over again.  This not only reduces  latency but also saves on cost as AWS charges for execution time.

In this deaign, I use several architecture patterns such as Orchestration, Choreograph, Citcuit Breaker, and CQRS + Materialize view.



LAMBDA AUTHORIZER DESIGN

![Alt text](image-2.png)

A new layer to check the authenticity of the access request by a user is verified by the lambda authorizer function.

The function receives a token with the access policy on the header from the login web page.  This token is then verified for authenticity with the Cognito managed-service to insure that the user is a member of the access pool.

Next, the access policy id further verified to insure that the user has access to the core backend services through the correct API end-point managed by the AWS API GATEWAY managed-service.

A proper message is sent via the SNS managed-service to the user in the event the user has not access.

The Access policy of the user is attached to the header and passed to the lambda function.  

If the user has the right access, the secion access is cached so that next time to use the stored acess policy instead.