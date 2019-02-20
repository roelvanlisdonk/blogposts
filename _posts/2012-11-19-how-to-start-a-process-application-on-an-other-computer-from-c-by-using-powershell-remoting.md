---
ID: 2948
post_title: 'How to start a process / application on an other computer from C#, by using PowerShell remoting'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2012/11/19/how-to-start-a-process-application-on-an-other-computer-from-c-by-using-powershell-remoting/
published: true
post_date: 2012-11-19 12:05:43
---
<p>&#160;</p>  <p>You van execute a process on an other machine from C#, by using the code below:</p>  <p>&#160;</p>  <p><strong>Example for calling the function</strong></p>  <pre class="code"><span style="background: white; color: blue">var </span><span style="background: white; color: black">rc = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">RemotingComponent</span><span style="background: white; color: black">(</span><span style="background: white; color: blue">null</span><span style="background: white; color: black">);
rc.RunRemoteProcess
(
    </span><span style="background: white; color: #a31515">@&quot;MyMachine1&quot;</span><span style="background: white; color: black">, 
    </span><span style="background: white; color: #a31515">&quot;MyMachine1\Administrator&quot;</span><span style="background: white; color: black">, 
    </span><span style="background: white; color: #a31515">&quot;MyPassword1&quot;</span><span style="background: white; color: black">, 
    </span><span style="background: white; color: #a31515">@&quot;C:\Windows\System32\notepad.exe&quot;</span><span style="background: white; color: black">,
    </span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Empty
 );</span></pre>

<p><strong>C# class</strong></p>

<pre class="code"><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Collections.Generic;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.IO;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Linq;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Management.Automation;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Management.Automation.Runspaces;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Security;
</span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Text;

</span><span style="background: white; color: blue">namespace <font color="#000000">Research</font></span><span style="background: white; color: black">
{
    </span><span style="background: white; color: blue">public interface </span><span style="background: white; color: #2b91af">IRemotingComponent
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">void </span><span style="background: white; color: black">RunRemoteProcess(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">machineName, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">userName, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">password, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">processPath, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">processArguments);
    }

    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">RemotingComponent </span><span style="background: white; color: black">: </span><span style="background: white; color: #2b91af">IRemotingComponent
    </span><span style="background: white; color: black">{
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">RunRemoteProcess(</span><span style="background: white; color: blue">string </span><span style="background: white; color: black">machineName, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">userName, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">password, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">processPath, </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">processArguments)
        {
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">connectTo = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">Uri</span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">String</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">&quot;http://{0}:5985/wsman&quot;</span><span style="background: white; color: black">, machineName));

            _logger.Info(</span><span style="background: white; color: #a31515">&quot;Building powershell command.&quot;</span><span style="background: white; color: black">);
            </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">command = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">StringBuilder</span><span style="background: white; color: black">();
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$pinfo = New-Object System.Diagnostics.ProcessStartInfo&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">@&quot;$pinfo.FileName = &quot;&quot;{0}&quot;&quot;&quot;</span><span style="background: white; color: black">, processPath));
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$pinfo.UseShellExecute = $false&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$pinfo.RedirectStandardError = $true&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$pinfo.RedirectStandardOutput = $true&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$pinfo.CreateNoWindow = $true&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">@&quot;$pinfo.WorkingDirectory = &quot;&quot;{0}&quot;&quot;&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">FileInfo</span><span style="background: white; color: black">(processPath).Directory.FullName));
            command.AppendLine(</span><span style="background: white; color: blue">string</span><span style="background: white; color: black">.Format(</span><span style="background: white; color: #a31515">@&quot;$pinfo.Arguments = &quot;&quot;{0}&quot;&quot;&quot;</span><span style="background: white; color: black">, processArguments));
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$p = New-Object System.Diagnostics.Process&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$p.StartInfo = $pinfo&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$p.Start() | Out-Null&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$output = $p.StandardOutput.ReadToEnd()&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$p.WaitForExit()&quot;</span><span style="background: white; color: black">);
            command.AppendLine(</span><span style="background: white; color: #a31515">&quot;$output&quot;</span><span style="background: white; color: black">);
            
            </span><span style="background: white; color: blue">string </span><span style="background: white; color: black">shell = </span><span style="background: white; color: #a31515">@&quot;http://schemas.microsoft.com/powershell/Microsoft.PowerShell&quot;</span><span style="background: white; color: black">;
            </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">passing = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">SecureString</span><span style="background: white; color: black">())
            {
                </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">char </span><span style="background: white; color: black">c </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">password.ToCharArray())
                {
                    passing.AppendChar(c);
                }
                passing.MakeReadOnly();
                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">credentials = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">PSCredential</span><span style="background: white; color: black">(userName, passing);

                </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">connection = </span><span style="background: white; color: blue">new </span><span style="background: white; color: #2b91af">WSManConnectionInfo</span><span style="background: white; color: black">(connectTo, shell, credentials);
                </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">runspace = </span><span style="background: white; color: #2b91af">RunspaceFactory</span><span style="background: white; color: black">.CreateRunspace(connection))
                {
                 </span><span style="background: white; color: black">   runspace.Open();

                    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">powershell = </span><span style="background: white; color: #2b91af">PowerShell</span><span style="background: white; color: black">.Create())
                    {
                        powershell.Runspace = runspace;
                        powershell.AddScript(command.ToString());

                 </span><span style="background: white; color: black">       </span><span style="background: white; color: blue">var </span><span style="background: white; color: black">results = powershell.Invoke();
                        runspace.Close();

                        </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: blue">var </span><span style="background: white; color: black">obj </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">results.Where(o =&gt; o != </span><span style="background: white; color: blue">null</span><span style="background: white; color: black">))
                        {
                            Console.Writeline(string.Format(</span><span style="background: white; color: #a31515">&quot;Output: [{0}].&quot;</span><span style="background: white; color: black">, obj));
                        }
                    }
                }
            }
        }
    }
}
</span></pre>