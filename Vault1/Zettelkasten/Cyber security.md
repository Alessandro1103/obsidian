Date: 2023-11-03
Time: 22:52
Tags: #English #Università
Up: [[Inglese]]

---
# Cyber security

Computers are being used to store sensitive information. The problem is Internet, it's not a safety network to share information. Even govern needs to protect their and other people information. To do so, cybersecurity needs to develop by a systematic system, it can not be achieved through haphazard methods.
For example, few day after the 9/11, an Internet worm cyber attack, called Nimda, spread nationwide in less than an hour. The latest Internet worm, Sapphire, was able to spread worldwide in approximately 10 minutes. 
Everything we do in our life depends on computers and computer networks. Computers are used for controlling and managing manufacturing processes, water supplies, the electric power grid, etc. Even cyber attack that seems "non-critical", or with no purpose, are actually meditated to crush bigger system. 
The perpetrators can be separated by levels:
- **script kiddies**: users that download malicious software, and follow malicious request from the app.
- **hackers**: who are trying to prove what they can do, and the fact that they have control over some system.
- **insiders**: people allowed to access to certain data, for some reasons, like working for some industries.
- **organizations attack**: organizations wants to obtain information about other organizations, and to do so, can provide a big amount of resources for hacker. The benefits are simple, knowing which society the other organization is interested in, i can interfere, offering more money or compromising the image of the other company.
- **national situation**: one nation can spy to cause damage. Even more resources.
One of the most problem are home people, who normally say "i have nothing to hide", which is probably true, but from these people hackers can move to companies, other people and find more importante sensitive information. Computers so, are called zombies to be awaken at a specific time. 
There is not a perfect security, security is a system that must be trade off against user friendliness.

Dictionary:
- **tiger teams**: team used to test security of a system
- **computer security**: protection from unauthorized operation.
- **confidentiality**: sensitive information are accessible by authorized people.
- **integrity**: files can modified/destroyed by specified manner.
- **availability**: usable whenever is possible
- **security policy**: what is and what is not allowed

There are four approaches to achieve a secure computing environment:
- **Procedural approaches**: prescribe the appropriate behavior for user to follow when using a system. We can call them "user guidelines", for example, choosing a password, handling storage that are about to be destroyed. 
- **Function and Mechanism**: 
	- **Authentication mechanisms**: used to assure that a particular user is who he claims to be. A mechanisms we have to mention is "secure attention key", is a key when hit by the user block every other operation, this happens to block "spoofing". Spoofing is fooling the user into believing that he is talking to the system. The most sophisticated authentication devices are those that depend on a unique physiological or behavioral characteristic. The most common bio-metric devices are based on fingerprints, retina patterns.
	- **Access Control**: limiting a user's access to only those files that policy determines should be accessed.
		- **Discretionary access control**: the owner specifies what kind of access other user can have to the object (distributed password).
		- **Mandatory access control**: a user can access a resource based on the security attributes of both the user and the object.
	 To assure that all access control policies are enforced we need a **reference monitor**. This must be isolated from modification, always invoked, small enough to be analyzed and tested.
	- **Inference controls**: these control attempt to restrict database access, you can access to database but cant actually see single data, just a summary statistic.
- **Assurance techniques**: 
	- **penetration analysis**: use a collection of known flaws, generalizes these flaws, and tries to apply them to the system being analyzed.
	- **Formal verification**: demonstrates that ana implementation is consistent with its requirements.
	- **Covert Channel Analysis**: signal information through system facilities not intended for data transfer, and they support this communication using methods not detected or regulated by the access control mechanisms: "storage channels", "timing channels"
- **Intrusion Detection**:to detect any intrusion we can keep record called "audit collection", the data collected is called an "audit log". By an automated tool, called intrusion detection, we can now find violations that might have gone unnoticed before. There are 2 categories of intrusion detection approaches:
	- **Anomaly detection**: relies on models of the intended behavior of users and find deviations. (false positive)
	- **Misuse detection**: relies with attack descriptions, trying to match them against the stream of audit data. (few false positive, can detect only the known attack)



---
# References

