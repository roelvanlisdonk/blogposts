---
ID: 4032
post_title: 'Reliable bring external process window to foreground with C#'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2014/09/05/reliable-bring-external-process-window-to-foreground-without-c/
published: true
post_date: 2014-09-05 14:37:07
---
<p>If you want to reliable bring the main window of an external process to the foreground in C#, use the “simulate alt key” technique found at: <a title="http://stackoverflow.com/questions/10740346/setforegroundwindow-only-working-while-visual-studio-is-open" href="http://stackoverflow.com/questions/10740346/setforegroundwindow-only-working-while-visual-studio-is-open">http://stackoverflow.com/questions/10740346/setforegroundwindow-only-working-while-visual-studio-is-open</a></p>  <p>Just start Notepad, then run the following test in Visual Studio.</p>  <p>It should bring Notepad as a maximized window in the foreground.</p>  <pre class="code"><span style="background: white; color: blue">namespace </span><span style="background: white; color: black">Research.EndToEndTests
{
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">Microsoft.VisualStudio.TestTools.UnitTesting;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Diagnostics;
    </span><span style="background: white; color: blue">using </span><span style="background: white; color: black">System.Runtime.InteropServices;

    [</span><span style="background: white; color: #2b91af">TestClass</span><span style="background: white; color: black">]
    </span><span style="background: white; color: blue">public class </span><span style="background: white; color: #2b91af">ResearchTester
    </span><span style="background: white; color: black">{
        
        [</span><span style="background: white; color: #2b91af">TestMethod</span><span style="background: white; color: black">]
        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Test()
        {
            Reliable_set_window_to_forground();
            </span><span style="background: white; color: #2b91af">Assert</span><span style="background: white; color: black">.IsTrue(</span><span style="background: white; color: blue">true</span><span style="background: white; color: black">);
        }

        </span><span style="background: white; color: blue">public void </span><span style="background: white; color: black">Reliable_set_window_to_forground()
        {
            </span><span style="background: white; color: #2b91af">Process</span><span style="background: white; color: black">[] processes = </span><span style="background: white; color: #2b91af">Process</span><span style="background: white; color: black">.GetProcesses();
            </span><span style="background: white; color: blue">foreach </span><span style="background: white; color: black">(</span><span style="background: white; color: #2b91af">Process </span><span style="background: white; color: black">proc </span><span style="background: white; color: blue">in </span><span style="background: white; color: black">processes)
            {
                </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(ProcessIsNotepad(proc))
                {
                    ActivateWindow(proc.MainWindowHandle);
                }
            }
        }

        </span><span style="background: white; color: blue">public bool </span><span style="background: white; color: black">ProcessIsNotepad(</span><span style="background: white; color: #2b91af">Process </span><span style="background: white; color: black">proc) 
        {
            </span><span style="background: white; color: blue">return </span><span style="background: white; color: black">proc.MainWindowTitle.EndsWith(</span><span style="background: white; color: #a31515">&quot;Notepad&quot;</span><span style="background: white; color: black">, </span><span style="background: white; color: #2b91af">StringComparison</span><span style="background: white; color: black">.InvariantCultureIgnoreCase);
        }
        
        </span><span style="background: white; color: blue">private const int </span><span style="background: white; color: black">ALT = 0xA4;
        </span><span style="background: white; color: blue">private const int </span><span style="background: white; color: black">EXTENDEDKEY = 0x1;
        </span><span style="background: white; color: blue">private const int </span><span style="background: white; color: black">KEYUP = 0x2;
        </span><span style="background: white; color: blue">private const int </span><span style="background: white; color: black">SHOW_MAXIMIZED = 3;

        [</span><span style="background: white; color: #2b91af">DllImport</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;user32.dll&quot;</span><span style="background: white; color: black">)]
        </span><span style="background: white; color: blue">private static extern </span><span style="background: white; color: #2b91af">IntPtr </span><span style="background: white; color: black">GetForegroundWindow();
        [</span><span style="background: white; color: #2b91af">DllImport</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;user32.dll&quot;</span><span style="background: white; color: black">)]
        </span><span style="background: white; color: blue">private static extern void </span><span style="background: white; color: black">keybd_event(</span><span style="background: white; color: blue">byte </span><span style="background: white; color: black">bVk, </span><span style="background: white; color: blue">byte </span><span style="background: white; color: black">bScan, </span><span style="background: white; color: blue">uint </span><span style="background: white; color: black">dwFlags, </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">dwExtraInfo);
        [</span><span style="background: white; color: #2b91af">DllImport</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;user32.dll&quot;</span><span style="background: white; color: black">)]
        </span><span style="background: white; color: blue">private static extern bool </span><span style="background: white; color: black">SetForegroundWindow(</span><span style="background: white; color: #2b91af">IntPtr </span><span style="background: white; color: black">hWnd);
        [</span><span style="background: white; color: #2b91af">DllImport</span><span style="background: white; color: black">(</span><span style="background: white; color: #a31515">&quot;user32.dll&quot;</span><span style="background: white; color: black">)]
        </span><span style="background: white; color: blue">private static extern bool </span><span style="background: white; color: black">ShowWindow(</span><span style="background: white; color: #2b91af">IntPtr </span><span style="background: white; color: black">hWnd, </span><span style="background: white; color: blue">int </span><span style="background: white; color: black">nCmdShow);
        
        </span><span style="background: white; color: blue">public static void </span><span style="background: white; color: black">ActivateWindow(</span><span style="background: white; color: #2b91af">IntPtr </span><span style="background: white; color: black">mainWindowHandle)
        {
            </span><span style="background: white; color: green">// Guard: check if window already has focus.
            </span><span style="background: white; color: blue">if </span><span style="background: white; color: black">(mainWindowHandle == GetForegroundWindow()) </span><span style="background: white; color: blue">return</span><span style="background: white; color: black">;

            </span><span style="background: white; color: green">// Show window maximized.
            </span><span style="background: white; color: black">ShowWindow(mainWindowHandle, SHOW_MAXIMIZED);
            
            </span><span style="background: white; color: green">// Simulate an &quot;ALT&quot; key press.
            </span><span style="background: white; color: black">keybd_event((</span><span style="background: white; color: blue">byte</span><span style="background: white; color: black">)ALT, 0x45, EXTENDEDKEY | 0, 0);
                        
            </span><span style="background: white; color: green">// Simulate an &quot;ALT&quot; key release.
            </span><span style="background: white; color: black">keybd_event((</span><span style="background: white; color: blue">byte</span><span style="background: white; color: black">)ALT, 0x45, EXTENDEDKEY | KEYUP, 0);

            </span><span style="background: white; color: green">// Show window in forground.
            </span><span style="background: white; color: black">SetForegroundWindow(mainWindowHandle);
        }
    }
}
</span></pre>