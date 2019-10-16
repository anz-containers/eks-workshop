# The AWS App Mesh Value Proposition

Back when the world was deploying monolithic three-tier architectures - observability was fairly simple, and routing/discovery to an extent too. Your application was probably written in a single language, and deployed to via a single technology platform (EC2 etc). 

With the industry's move to microservices that changed. You may have heard phrases like “Microservices don't solve complexity, they just take it out of the codebase, and into the network”. This is very true. We encourage customers to move to microservices to help scale an organisation. With microservices, teams can develop, release, deploy and scale services independently - thus greatly reducing the burden of change control in most cases - but what you gain in organisational scaling, you pay for in other areas.

Now we have different development teams writing services in multiple programming languages, and deploying to different technologies (containers, serverless, vms etc) - all within the same organisation!

One of the most common questions from organisations moving to microservices (or even those already running them) is “How do I get observability into all of my services?”. Customers want to see at a high level what's working well, what's not working and then have the ability to dive deeper when problems occur.

Historically, if you wanted deep application/traffic/protocol level observability - you needed to embed a vendor's library or SDK into your application.  

This SDK/library approach has two major flaws:

*  Customers don't tend to want to have to modify their applications to achieve this. Nothing slows down adoption like “Oh, you just need to include this language-specific SDK into all of your existing applications.”
* Monitoring SDKs and libraries are language specific - what if your developers want to use a language that's not supported by the monitoring vendor, such as https://en.wikipedia.org/wiki/Brainfuck. They'll end up with a muddle of different monitoring technologies.

This is where service meshes come in. They work differently.

Most services meshes today (like AWS App Mesh (https://aws.amazon.com/app-mesh/), Linkerd (https://linkerd.io/2/overview/), and Istio (https://istio.io/)) work instead by running a small proxy as a sidecar (https://medium.com/@dwdraju/sidecar-pattern-with-use-case-examples-ed6642e5eaf7). This is a generic term for a small application, deployed alongside the main application.

![AWS App Mesh](/images/AppMesh.png)
