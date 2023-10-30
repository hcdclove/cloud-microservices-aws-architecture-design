ECOMMERCE CLOUD MICROCROSERVICES ARCHITECTURE DESIGN

![Alt text](image.png)

The goal is to let the System Architecture design abosrve the complexity of the system while keeping the code simple, always observice the single responsibility pattern.

When the user successfully verify the OTS challenges, the user detail is stored in a dynamoDB table and the user is added to Cognito user pool.

I am using amplify for simplicity!  Also amplify handles the token life extention process in the background.  One less thing to have to code or worry about.

Using an S3 bucket for the web app is very cheap. while cloudfront handles the incoming traffic from the users.

Using a WAF also allows us to control all incoming requests from users into the system.

Activating Cloudfront chaching rules allows the app to be served from the chache on subsequest requests rather that having to go through the steps all over again.

In this deaign, I use several architecture patterns such as Orchestration, Choreograph, and CQRS + Materialize view.

Note: There are still  several additional critical global services to be added as part of the overall software design architecture for this system, such as loggin, monitoring, security, etc.