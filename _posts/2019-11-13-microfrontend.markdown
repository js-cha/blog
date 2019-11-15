# Things I learned from building a micro-frontend application.

Micro frontends similar to micro services, is when you have features/parts of a website or application owned by independent teams that look after a specific business function or user group, for example user engagement, monetisation, seekers, owners and etc.

The problems we had with our frontend monolith:

* extremely long build times and slow start up times leading to poor developer experience.
* clunky and difficult to deploy. If the build fails during the ci/cd pipeline, you're forced to wait a very long time which impacts productivity.
* low confidence in the application deployment phase leads to fewer changes made to production. 
* ever-increasing complexity making it difficult for any one to fully understand the  of the application.

These were some of the issues we faced.

We decided for our next project, we would build it in a separate, independently deployable frontend application. The benefits were immediately evident to us. We could adopt new technologies and frameworks without having to worry about other parts of the application. We saw increased productivity thanks to faster build times. Deployment was way smoother and pain free. 

One downfall to this approach I experienced was the duplication of logic. Our application content is hidden behind a login requiring us to implement authentication and authorization for all our applications in the middleware layer. I noticed much of this logic was the same with our monolith and I can only assume future micro frontend applications would require the same. One solution would be to expose the auth logic as a private module which can be shared across applications. 

Also, cross communication with other micro frontend applications is also a growing concern and a problem we must address. When the user is traversing through many distinct applications, how do we provide a seamless experience without the user noticing minor details like design inconsistencies, auth checks and redirects and so on.

Coordinating shared component updates also poses a challenge across multiple micro frontend applications, especially at a large scale. It becomes all the more important for cross-function communication and coordination to ensure the end user has a consistent experience across the entire application.
