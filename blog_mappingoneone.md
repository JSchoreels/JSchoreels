DDD & Microservices are all fun but when 90% of your code is something like customerDomainB.setFirstname(customerDomainA.getFirstname())
customerDomainB.setLastname(customerDomainA.getLastname())
[...]

It may be a sign that your contexts aren't very well bounded and that you would have been better with those two domain objects in the same domain in the first place.

Ideally, communication between bounded contexts should be minimal. For example, your "Order Service" may just know the customer "UUID" and the address "UUID" to pass to the "Delivery Service" that will resolve both sets of informations for the last final step to trigger the delivery with all the information.

Basically, you should thrive to have minimal set of request parameters like some UUIDs. If you can't, maybe there is some unwanted coupling between your domains.

Also, it would help you greatly to be GDPR-friendly since you can easily "hide" private information by only speaking to UUID until the very last "step" (here, the delivery). Way more convenient to anonymize your data for bug reproduction too.

Some tools may automate those 1:1 mapping, but no tools will fix your architectures :)

