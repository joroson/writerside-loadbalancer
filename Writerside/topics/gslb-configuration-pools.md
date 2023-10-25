# Pools

The pool ties the elements of the GSLB configuration together. The members are assigned to the pool and the pool is
assigned to the global name. The majority of the configuration is applied within the pool. Due to this part of the GSLB
configuration being the most in depth we will delve into each of the sections and explain them in greater detail.

- **Name:** as with all the other elements so far, this is just a local reference for the pool. It must be an XML-safe
  string.
- **Monitor:** the type of health check monitor that will be perform on the members.
- **LB Method:** the distribution model/method that the pool should employ for incoming requests.

#### Advanced Configuration {collapsible="true"}

##### Monitor Interval

The number of seconds between each health check, the default is every 10 seconds. If you require health checks to be
performed more (or less) frequently.

##### Monitor Timeout

The number of milliseconds that a health check response must be received within to be considered a successful response.
For example, by default if a response is received 5001 milliseconds after being sent, it will be marked as a failed
health check.

##### Monitor Retries

The number of times that a health check will be retried before being declaring a member down. The number of health check
failures permitted by the system is always one more than the number of retries configured. The default configuration is
for two retries which means there will a total of 3 health check failures before a member is marked as being down.

##### Fallback

The fallback method defines what should happen if all the members of a pool are failing health checks. There are two
options: refuse and any

- *any:* This is the default and it will return an answer from the pool for any node that does not have a weight of 0.
  That means when you have a fallback method of any you will get receive a response that points you to a known
  non-working IP.
- *refuse:* The lookup will simply fail in this instance. A DNS response will not be sent as none of the members are
  online (according to health checks) to process requests sent to it.