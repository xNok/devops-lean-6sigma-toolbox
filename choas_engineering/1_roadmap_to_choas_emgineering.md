# Road Map to Choas: Major disruption

Major disruption that impact everyday business operations do happend. To convince yourself you can have a look at the [Timeline of AWS major Outages](https://awsmaniac.com/aws-outages/). So if your services are hosted in one of those affected Datacenters you may suffer important financial lose.

Preparing for those scenarios is the best insurance policies to mitigate the impact of such events. On top of that making sur you are prepare briges many benefits:
* Better overall achitectur design
* Less firefighting and less employe burnout 
* Better engagement in supporting production environnement

This were Chaos engineering comes into play

> Chaos engineering is the discipline of experimenting on a software system in production in order to build confidence in the system's capability to withstand turbulent and unexpected conditions ([Principles of chaos engineering](https://principlesofchaos.org/s))

Choas engineering provides theores, best practices and tools to get your company to many type of disruption. I like to categorise disruptions into 4 categorie and tackle them independantly.

![](./severity.drawio.svg)

When starting with Choas Engineering I recomment strating with the most critical senarios (Severity 1) because they lead to the most improvement for your company.

For instance, they forces you to lay the fondation for Incident response and incident management.

## 1. Build a Base line

The main requirement to start with chaos enginering is a good Alerting and Monitoring system. Indeed you cannot go blind and simulate disasters in your production environmement.

> Start by defining ‘steady state’ as some measurable output of a system that indicates normal behavior. 

You should start with monitoring health, and availability. There is [three types monitoring](https://www.browserstack.com/guide/continuous-monitoring-in-devops) you will need to have inplace:

* **Network Monitoring**: Validate that the network component of functionning properly. It includes firewalls, routers, switches, servers, Virtual Machines, etc. Network issues could be very damageble, because that often have a big blast radius.
* **Infrastructure Monitoring**: Validate the IT infrastructure is up and running. This includes external providers, services, servers, storage, plaftform, shared services, etc.  
* **Application Monitoring**: Validate that the software is behaving properly. This includes log, errors code, performances, user behaviours.

I suggest that you construct you dashboard and metrics around a check-list that represent a boot sequence of your entire system. Ex:

* Network configuration ready
* Number instance up vs number of instance required
* Number of backing services up vs number requires
* Number of microservices deployed vs number required
* Health status of all services
* Traffic in user/min vs expected traffic

## 2. Destroy your Dev environnement every days

Once you have establish a baseline and work on you monitoring and Observabily it is time to put you system under stress to validate what you have achieved so far. You are going to shut down all you dev/staging/pre-prod envirenement once a day and recreate them from scratch.

Unless you have a very internationnal team there is always a window where no-one is working, while your environnement are still up and running. If no one is working then the envirement sould be shut down to save cost and test you infrastructure scripts.

It may not be wise to start with a big bang appreach (aka. deleting everything at once). Unstead use a progesssive approach. For instance start by deleting microservices every night and redeploying them the morning using your CI/CD pipeline. Next add the deletion of databases, you shoud validate that you backup and restore procedure is working properly. Finally delete infrastructure componement everyday and recreate them from scratch the next day.

Once you can achieve this daily routine without issue it means that you have a solide set of automation scripts to manage you infrastructure. This exercice sould also be the perfect ocasion to perfect you monitoring.

Getting an eviremement up dans down is the easi part if yu did your job properly from day 1 this should almost be granted. If not it means that you have accumulated technical debt. Lucky for you by deleting envirement every day you reduce the chance of having technical dept. If someone does something manually their day of work would be reduce to ashes the next day. Believe me everone will soon learn the lesson and everythong as code will thrive

## 3. Migrate dev Environnement to another data center

The next task to be ready to a catastrofic event is to make you infrastructure a bit more configuratble. Their is no reason for an automated script to lock you product in one region of the world. Thus you should refactor you code and configuration such that you can deploy in any region you cloud provider offers.

Beware region have some specificites (type of instance, service availbles, etc.). Now is the time to know more about your cloud provider. You should also study different strategies to migrate to a different region:

* Active-Active:
* Active-Passive:
* Active-Recovery:

So now you should be able once a week, for instance, to redeploy you environnement in a different region and no-one should see the difference.


## 4. Build your incident response Strategy

At this point, you are technically ready to face any disaster. But do you have a clear idea of what to do? Most likely not.

It is important to define an incident responce strategy. Document how people should act in case a problem accure and it requires you to deploy your entire stack somewhere else.

* How do we detect such problem?
* Who is en charge of coordinating the response to the incident?
* Who should be contacted to handle the incident?
* How do you communicate the incident internally and externally?
* How long should it take at most to be back online?

## 5. Orginise a Game day

Last you need pracitice. Choose an date get everyone involve and act is if the incident accured.

1. Follow the response procedure (validate that everythin make sense)
2. Migrate you infrastructure in a new regions
3. Wait a couple day
4. Migrate again to the original region.

# References

* [chaos engineering](https://searchitoperations.techtarget.com/definition/chaos-engineering#:~:text=Chaos%20engineering%20is%20the%20process,it%20can%20withstand%20unexpected%20disruptions.&text=The%20goal%20of%20chaos%20engineering,introduce%20random%20and%20unpredictable%20behavior.)
* [PRINCIPLES OF CHAOS ENGINEERING](https://principlesofchaos.org/)
* [The Complete History of AWS Outages](https://awsmaniac.com/aws-outages/)
* [The Complete Guide to Metrics, Monitoring and Alerting](https://sematext.com/blog/monitoring-alerting/)