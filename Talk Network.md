lp1 refers to what environment is to be used, lp1 being retail (?).
Using the following code we can perform a DNS enumeration to see what
environments there are:

    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    import socket
    import string
    import itertools
    from multiprocessing import Pool
    
    
    def check_env(env):
        try:
            socket.gethostbyname('sun.hac.{0}1.d4c.nintendo.net'.format(env[0]
                                 + env[1]))
            return '{0}{1}1'.format(env[0], env[1])
        except:
            pass
    
    
    def main():
        pool = Pool()
        potential_environments = itertools.product(string.lowercase,
                string.lowercase)
    
        results = pool.map(check_env, potential_environments)
        pool.close()
        pool.join()
        print set(results)
    
    
    if __name__ == '__main__':
        main()

Which in turn gives us the following: dp1, sp1, lp1, td1, jd1. At some
point we should try and see if we can find any references anywhere as to
what each of these environments are.
--[FrasierCrane](User:FrasierCrane "wikilink")
([talk](User%20talk:FrasierCrane.md "wikilink")) 15:53, 10 May 2018
(CDT)

  -   
    Just added some of these to the Network page. Is "dp1" accurate or
    did you mean "dd1"? Code mentions "dd1" only.
    --[Hexkyz](User:Hexkyz "wikilink")
    ([talk](User%20talk:Hexkyz.md "wikilink")) 16:07, 10 May 2018 (CDT)

<!-- end list -->

  -   
    dp1 is correct. My theory is that the second character refers to
    either (p)roduction (retail unit) or (d)evelopment (SDEV units?).
    dp1 might be an internal retail unit testing backend for Nintendo. I
    can't work out the first characters meaning though, SciresM did a
    big post on reddit that explains some of it and gives other
    potential domains but, the first character is still a mystery.
    Here's all I can think for the first character:

d = Development (Third party developers?) t = Testing (Nintendo Internal
rather than third party?) s = Lotcheck (How s = lotcheck, I don't know,
SciresM reddit post does mention an s domain for lotcheck though. l =
Live (Retail) --[FrasierCrane](User:FrasierCrane "wikilink")
([talk](User%20talk:FrasierCrane.md "wikilink")) 17:12, 10 May 2018
(CDT)

  -   
    Small second note, if the code mentions dd1, by the previous running
    theory, that would mean it's third-party dev using developer unit.
