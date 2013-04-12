tldcheck
========

a script to check domain availability on all TLDs and ccTLDs

From: http://blog.postmaster.gr/2010/06/18/tldcheck/

@dstergiou asked:

"I am looking for a tool to see under which TLDs a domain is registered. E.g.
check all TLDs for domains matching “test123″"

One way to check is to visit registrars that cover TLDs and ccTLDs (like
EuroDNS or Gandi) and submit your query to their forms. However since (at
least TTBOMK) none of them offers any query API to check programmatically,
one can script his way to an almost complete solution. ICANN provides a list
of all available TLDs and we can iterate over it.

This hack comes with three problems:

- It uses Net::DNS which makes it a little slow. There is room for improvement.

- It finds out about registered domain names that have domain name servers
  that answer queries about them. This is not always the case. For example in
  .GR one can register a domain without having it served.

- It also does not take into account strict domain hierarchies, like .co.uk,
  .net.uk, .org.uk but minimal changes are needed to test that too.

Somewhat incomplete as a solution, but adequate as a 5 minute hack for most
purposes.

P.S. @stsimb offers a similar solution using dig:

for sfx in TLDs; do dig +short ns test123.$sfx; done
