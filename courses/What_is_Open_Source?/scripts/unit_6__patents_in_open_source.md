# Patents in Open Source

Granting explicit patent rights means that users and/or contributors of software containing patented technologies licensed under those terms are also granted rights to those patents with the license. Fundamentally, a patent doesn't provide more rights to its custodian than to license owners. Yet, being a form of intellectual property typically granted by an institution (e.g. a government), owning a patent may provide additional weight in a legal recourse when trying to enforce a license. And this is why patents are still sometimes seen in open source landscapes.

It remains, however, a polarising topic. For instance, the GNU GPLv3 license goes as far as stating the following:

Every program is threatened constantly by software patents. States should not allow patents to restrict the development and use of software on general-purpose computers. However, in those that do, we wish to avoid the special danger that patents applied to a free program could make it effectively proprietary.

GNU GENERAL PUBLIC LICENSE, Version 3, 29 June 2007.

Others, like MPL-2.0 or Apache-2.0, include patent retaliation clauses as an extra protective measure. Such clauses usually entail that if anyone — contributors or users — attempts to sue another user or contributor for patent infringement, they lose rights primarily granted by the license. 

Retaliation clauses discourage attempts to bypass the license terms via patent litigation. This can be effective when software contains patents held by different contributors.

Indeed, suing any contributor for patent infringement also immediately revokes one's license and ability to use patent rights previously granted for the same licensed work. Given how software is built today with many layers of dependencies, this can mean a lot!

For example, imagine you are building a software service that uses 50 other software libraries licensed under Apache-2.0. And you decide to patent some of the new techniques you develop in your software, which you also distribute under Apache-2.0. 

Then, you notice someone has forked your project and made a few changes. For example, they improved your patented techniques for their own needs. Should you decide to sue them for patent infringement, you'd automatically lose all license rights from the 50 libraries you depend on, which, in many cases, represent a substantial part of your larger work.

## Questions

1. What does granting explicit patent rights mean in the context of open-source software licenses?
A. It restricts users from modifying patented technologies
B. It requires users to pay for patent usage
C. It prevents any patents from being applied to the software
**D. It grants users and contributors rights to patents included in the licensed software**

2. According to the text, why might owning a patent provide additional legal weight in open-source contexts?
A. It allows the patent owner to restrict all software distribution
**B. It provides leverage in legal recourse when enforcing a license**
C. It automatically makes the software proprietary
D. It eliminates the need for an open-source license

3. What is the purpose of patent retaliation clauses in licenses like MPL-2.0 or Apache-2.0?
**A. To revoke license rights if someone sues for patent infringement, discouraging such actions**
B. To encourage patent litigation among contributors
C. To grant additional patent rights to contributors who sue
D. To require all contributors to patent their work

