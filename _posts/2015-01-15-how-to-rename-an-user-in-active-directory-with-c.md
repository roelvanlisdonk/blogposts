---
ID: 4242
post_title: 'How to rename an user in Active Directory with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2015/01/15/how-to-rename-an-user-in-active-directory-with-c/
published: true
post_date: 2015-01-15 15:10:15
---
&nbsp;

If you want to rename an user in Active Directory by using C#, you can use the following code:
<pre class="code"><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System;
</span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System.Collections.Generic;
</span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System.DirectoryServices;
</span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System.DirectoryServices.AccountManagement;
</span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System.Linq;
</span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System.Text;
</span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">System.Threading.Tasks;

</span><span style="background: white; color: blue;">namespace </span><span style="background: white; color: black;">ConsoleApplication1
{
    </span><span style="background: white; color: blue;">class </span><span style="background: white; color: #2b91af;">Program
    </span><span style="background: white; color: black;">{
        </span><span style="background: white; color: blue;">static void </span><span style="background: white; color: black;">Main(</span><span style="background: white; color: blue;">string</span><span style="background: white; color: black;">[] args)
        {
            </span><span style="background: white; color: blue;">try
            </span><span style="background: white; color: black;">{
                </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"This application will rename a user in active directory."</span><span style="background: white; color: black;">);
                </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #2b91af;">Environment</span><span style="background: white; color: black;">.NewLine);

                </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Enter domain:"</span><span style="background: white; color: black;">);
                </span><span style="background: white; color: blue;">string </span><span style="background: white; color: black;">domain = </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.ReadLine();

                </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Connecting to domaincontroller."</span><span style="background: white; color: black;">);
                </span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">(</span><span style="background: white; color: #2b91af;">PrincipalContext </span><span style="background: white; color: black;">context = </span><span style="background: white; color: blue;">new </span><span style="background: white; color: #2b91af;">PrincipalContext</span><span style="background: white; color: black;">(</span><span style="background: white; color: #2b91af;">ContextType</span><span style="background: white; color: black;">.Domain, domain))
                {
                    </span><span style="background: white; color: blue;">if </span><span style="background: white; color: black;">(context == </span><span style="background: white; color: blue;">null</span><span style="background: white; color: black;">)
                    {
                        </span><span style="background: white; color: blue;">throw new </span><span style="background: white; color: #2b91af;">ApplicationException</span><span style="background: white; color: black;">(</span><span style="background: white; color: #a31515;">"Domain not found."</span><span style="background: white; color: black;">);
                    }

                    </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Enter current username (e.g. john):"</span><span style="background: white; color: black;">);
                    </span><span style="background: white; color: blue;">string </span><span style="background: white; color: black;">currentUserName = </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.ReadLine();
                                        
                    </span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">(</span><span style="background: white; color: #2b91af;">UserPrincipal </span><span style="background: white; color: black;">user = </span><span style="background: white; color: #2b91af;">UserPrincipal</span><span style="background: white; color: black;">.FindByIdentity(context, currentUserName))
                    {
                        </span><span style="background: white; color: blue;">if </span><span style="background: white; color: black;">(user == </span><span style="background: white; color: blue;">null</span><span style="background: white; color: black;">)
                        {
                            </span><span style="background: white; color: blue;">throw new </span><span style="background: white; color: #2b91af;">ApplicationException</span><span style="background: white; color: black;">(</span><span style="background: white; color: #a31515;">"User not found."</span><span style="background: white; color: black;">);
                        }

                        </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Enter new username (e.g. john2):"</span><span style="background: white; color: black;">);
                        </span><span style="background: white; color: blue;">string </span><span style="background: white; color: black;">newUserName = </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.ReadLine();

                        </span><span style="background: white; color: blue;">using </span><span style="background: white; color: black;">(</span><span style="background: white; color: #2b91af;">DirectoryEntry </span><span style="background: white; color: black;">entry = (</span><span style="background: white; color: #2b91af;">DirectoryEntry</span><span style="background: white; color: black;">)user.GetUnderlyingObject())
                        {
                            </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Setting account properties in active directory."</span><span style="background: white; color: black;">);
                            entry.InvokeSet(</span><span style="background: white; color: #a31515;">"uid"</span><span style="background: white; color: black;">, newUserName);
                            entry.InvokeSet(</span><span style="background: white; color: #a31515;">"sAMAccountName"</span><span style="background: white; color: black;">, newUserName);
                            entry.InvokeSet(</span><span style="background: white; color: #a31515;">"userPrincipalName"</span><span style="background: white; color: black;">, </span><span style="background: white; color: blue;">string</span><span style="background: white; color: black;">.Format(</span><span style="background: white; color: #a31515;">"{0}@{1}"</span><span style="background: white; color: black;">, newUserName, domain));
                            entry.CommitChanges();

                            </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Rename common-name (CN)."</span><span style="background: white; color: black;">);
                            entry.Rename(</span><span style="background: white; color: #a31515;">"CN=" </span><span style="background: white; color: black;">+ newUserName);
                            entry.CommitChanges();

                            </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"User successfully renamed."</span><span style="background: white; color: black;">);
                        }
                    }
                }
            }
            </span><span style="background: white; color: blue;">catch </span><span style="background: white; color: black;">(</span><span style="background: white; color: #2b91af;">Exception </span><span style="background: white; color: black;">ex)
            {
                </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(ex.ToString());
            }
            
            </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.WriteLine(</span><span style="background: white; color: #a31515;">"Press enter to continue..."</span><span style="background: white; color: black;">);
            </span><span style="background: white; color: #2b91af;">Console</span><span style="background: white; color: black;">.ReadLine();
        }
    }
}</span></pre>